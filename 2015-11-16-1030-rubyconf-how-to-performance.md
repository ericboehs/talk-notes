# How To Performance by Eileen M. Uchitelle

## Pre
Purpose of Talk: to show how to make integration talk sfaster


## Benchmarking and Profiling
- Benchmarking
Measure how slow your code is

- Profiling
Tells us what is slow

Use them together.

- Get a baseline
- She created github.com/eileencodes/integration_performance_test app to test the stuff
- She used Ruby 2.1.5 and Rails 4.2.0

Benchmarked Controller and Integration tests

They are very similiar but controller tests were 23% slower.

But... Time isn't a good benchmarking metric. Need to do to ips (evanphx/benchmark-ips)

IPS: Integrations were 2.3x slower than controller test.

Upgraded to ruby 2.2.0 and rails master.

Turns out they were slightly slower (2.53x).

## Find out what's slowing
ruby-prof/ruby-prof

It's good because it uses a C extension. It's also been around a while.

StackProf - tmm1/stackprof
- Focused profiling

StackProf don't use cpu time on OS X! Use wall time! (There's a bug)

ko1/allocation_tracer - Helps trace GC allocations

Optimizations are available in 4.2.x.

## Questions
Q: Are there tools to auto benchmarking on git commit?
A: Nah. How would automate benchmarking that?

Q: Did you use other tools not in the talk?
A: Nope. But if she need sql profiling she'd use miniprofiler.
