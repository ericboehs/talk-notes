# Inside Ruby's VM: The TMI Edition by Aaron Patterson

## Pre
Javascript - Everything is Broken

Aarron is on both ruby and rails core.
  - This means he's bad at saying no
Works on the MangeIQ team at RedHat. Their app is open source.

Didn't want waitress to forget ice cream so he said "Remember the a la mode".

## Ruby's Virtual Machine - and its interals

He tried to build an AOT (ahead of time) compiler. He says it was a failure. But maybe not since he's still working on it.

Rebranding failure as "potential for success".

## What does it mean to run `ruby myprogram.rb`?
  - Stuff that happens before the program runs
    - Lexer
      - Takes code and turns into tokens
    - Parser
      - Takes tokens and turns into AST
      - AST Interpreter 1.9+ uses YARV
    - Compiler
    - Most of the time happens between parser and compiler
  - Run the actual program
    - Virtual Machine
      - If you have a real machine, you have a chip that defines instructions (i.e assembly language)
      - Stack based and register based virtual machines
        - Ruby's VM is stack based
      - A stack based vm is like an hp calculator.
        - `9 * 18 = 9 <ENTER> 18 <enter> * <enter>`
        - They have instructions: `9` is pushed onto stack, `18` is pushed on stack. `*` pops the tack twice and puts result back on stack.
        - YARV has `putobject 9`, `putobject 18`, `opt_mult`
        - Ruby's compiler is a multipass compiler
        - AST -> Linked List -> Optimizations -> Byte Code
        - Byte code can be accessed via RubyVM::InstructionSequence
          - This is what `ruby myprogram.rb` calls
        - Has a cool way to see what instructions a ruby program compiles to

- AST
- Linked List
  - List of items that are connected to points
    - Doubley linked lists are linked back up
  - C Code Walk-through
- Optimizations
  - `iseq_optimize` - compile time optimizations (vs vm optimizations)
    - Lots of them. Going to look at `peephole_optimization` and specialized instructions
    - Peephole - eliminates stuff you don't need
    - Specialized Instructions
- Byte Code - a list of integers (addresses)
  - Direct Thread Interpretation (is what ruby does)

## Failing at AOT Compiling
  So much C code.

"If learn anything from this talk"
  insns.def
  iseq_compile_node


Book to read:
  - Ruby under a microscope

This code didn't hit home for me. My goal for this conference was to get something out of each talk that I could use in my day-to-day job.
