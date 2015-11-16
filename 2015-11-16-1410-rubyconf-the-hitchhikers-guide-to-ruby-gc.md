# The Hitchhiker's Guide To Ruby Gc By Eric Weinstein

## Part 0: Ruby is not slow

Okay maybe. But not for the reasons you think.

- DB queies (N+1)
- Superliner time complexity
- Ruby being an interpreted language

But! GC slows down ruby as well.

Everything is an object

## Part 1

We're talking MRI (YARV)

Rubinius and JRuby have different GCs

- 1.8.7
  - Ruby GC is tracing
  - Mark and sweep
  - Mark and swwp was invented by John McCarthy for LISP in 1959
  - Ruby allocates some memory
  - When there's no mor efree memory, ruby marks active objects then combines (sweeps) inactive ojbects intoa  single list

EVERYTHING stops. When GCing (mark/sweep).

- 1.9.3
  - Lazy mark and sweep: sweep in phases to reduce the length of each sweep pause
  - Like 1.8.7, subverts native copy-on-write (to be continued)

- 2.0
  - Bitmap marking: we no longer mark objects directly, so we're free to leverage copy-on-wirte

- 2.1
  - Generational GC (two generations: young and old)
  - If you survive 3 collections, you become old
  - Because most objects die young, you perform fast minor GC frequently and slower- stop the world major GC rarely
  - The RGengc algorythm

## Part 2: (Ruby 2.2)

- Symbol GC: no more symbol DoS
- Incremental major GC (the RincGC algorithm)
- Tricolor marking: white (unmarked), gray (marked but may refer to white objects), and black (marked, without reference to white objects)

### Write Barriers

- They're super effective
- We also have write barrier protected and write barrier unprotected objects
- Pause time is relative to the number of living write barrier unprotected objects
- Most objects (string, array ,hash ,user defined pros) a re write barrier protected objects, so the pause time for unprotected objects is acceptable

### GC Tuning
- Don't do it!
- (Experts): Don't do it yet

- Turning it to 11
  - `RUBY_GC_HEAP_GROWTH_FACTOR` - triggers more frequent young object collection
  - `RUBY_GC_HEAP_GROWTH_MAX_SLOTS` - same above
  - `RUBY_GC_MALLOC_LIMIT/MAX/GROWTH_FACTOR` - triggers more GC

This is not a silver bullet.

## Part 3: Case Study

A suite of 7 sinatra apps.. smashed together

- Ruby objects are 40-bytes RValue structures, which ruby allocates into heaps of 16KB each
- You get ~400 Ruby objects per heap
- Ruby gives you about 100 heaps to start

```
GC.start
GC.stat
#=> :heap_live_number => 500123
```

For this sinatra app this seemed completely wrong. They weren't using activerecord, just api calls.

### The RValue
Flags -> Contains FL_MARK
Value -> Object contents
Next -> Pointer to next RStruct

### Mark and Sweep
- Ruby heaps comprise linked lists of RValues
- When there are no more free RValues, ruby 1.9 sets FL_MARK on all active ruby objects
- Then moves to the free list

### Copy on write
- When our production processes call fork, the new child process hares all memory with the parent
- Copies are only made when changes are written, but marking objects as live on the objects themselves forces a write.
- Ruby 1.9.3 GC subverts native copy on write

### Bitmap marking (Ruby 2.0)
- Ruby 2.0 includes a header at the beginning of each heap that contains a pointer to a bitmap represent...


- No 1: Upgrade to 2.0
- No 2: Profiled
- No 2: Tuned GC

## Further reading
- Why you should be excited about gc in ruby 2.0 (blog post)
- Ruby under a microscope
- Ruby performance optimization (Alexander Dymo)
- Koichi Sasada (youtube video)

## Questions
Q: Are the variables compilation variables (e.g. RUBY_GC_HEAP_GROWTH_FACTOR)
A: Just ENV vars, set in your environment and restart

Q: How do you think about out-of-band GC?
A: Essentially you tell GC to run when you want; don't run in the middle of an important request.

Q: How long should a major garbage collection take?
A: Definitely not several seconds. Less than a second.

Q: How to monitor GC collection in production?
A: Not sure. Do it in staging.
