# A Guided Read To Minitest by Nate Berkopec

## Pre
Minitest wouldn't let him stub an instance method.
  - Because ruby let's you do that already. It's called a _singleton method_.

This talk is about pain.

## Rspec
_Minitest is reactionary_

Original minitest was 90 lines of code:
  tinyurl.com/originalminitest

~ Talk note: Ryan Davis is sitting in the front row

Minitest lives in one gem (no dependencies)
  - `cloc` for minitest: Ruby code: 1586. Doc code: 1699
  - `cloc` for rpsec: Ruby code: 1586. Doc code: 1699

Rspec has 4 major components:
  - Rspec-core, expectations, mocks and support

Minitest is 1/10th the size in total.

Rpsec-mocks is 28 times larger than minitest/mock.

Statism is good.
  - A stateist tester asserts that a method returns a particular value. A mockist tester asserts that a method triggers a specific set of interactions with the object's dependencies.

Minitest knows whats best for you. You should adopt their style.
 - Don't expect a huge amount of configuration

## Code

`require 'minitest/autorom'`
  - Minitest installs an `at_exit` hook.

Aside:
  What does your ruby code need to look like, without using paranthesis, to be readable?

  Pain is good. Pain is signal.
  - I feel pain here. So what should I do? Is there a way to make it go away without hiding it?

  Paranthesis are sometimes a band-aid on a problem we should fix.

Stdlib is used very heavily in the minitest codebase.
- It also uses the system diff tool to print a diff on objects
  - Rspec implements that in ruby
Rspec has it's own Set, `flat_map`, thread local variables and even `rand()`.

Minitest philospohy: Use what is given to you

## Defining tests in minitest
  - Code examples (rspec sucks)

## Reduce the API Surface
  - Code examples (rspec sucks)

Abstraction is the Enemy
 - Learning to write abstractions well is the hardest thing we do as programers

TL;DR With minitest you have to learn ruby better, with rspec you have to learn how to use rpsec better.

## Questions
Q: Long time rspec user, was forced to use minitest. Wow it's simple. But Wow I can't do a ton of stuff. (no question)
A: I'm looking for this thing in rpsec. Shared examples don't exist in rspec. Modules are a great alternative
