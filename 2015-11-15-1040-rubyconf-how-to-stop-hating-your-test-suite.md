# How to Stop Hating your Test Suite by Justin Searls

Super awesome talk. High energy and he is very articulate. Make sure you've had 10 cups of coffee so you can keep up.

"Built talk in AppleWorks for Mac OS 9". Funny.


## Test Structre
- Big objects are hard to deal with
- Tests make big objects even worse
- Rule of Product (on wikipedia)
  - Says that a method will n arguments means there is n^n test cases to write.

Test should do 3 things
- Sets stuff up
- Invokes a thing
- Checks behicever

Arrange
Act
Assert

 or

 Given
 When
 Then

 Uses minitest! Wahoo.

 Also uses Rpsec. :( But I think he secretly likes Minitest.

Try to minimize each phase to just 1 line.

Maintains rpsec-given which makes a BDD like rpsec tests. Maybe also maintains minitest-given?

Test code is untested code. SO MAKE IT SIMPLE.

ALWAYS call the thing your testing SUBJECT.
ALWAYS call the thing your asserting on RESULT or RESULTS.
Use 100s of consistent tests. Not unique unicorns.o

Test data should be minimal but meanigfully minimal.

## Test Isoluation
Define sucess
  - Is this tested?
  - And something else. Omg this guy is fast.
  - is.gd/breaking_up (Talk on Breaking up with your test suite)

Realistic Tests suck because of a bunch of reasons but that slide was up for like 5 seconds.

Redundant coverage can kill a teams morale.
 - Run a coverage report and look at avg hits / line. High does not = good. If you change a method with a high hits/line, you're going to break a lot of tests.

Another strat, try your hand at outside-in TDD. London school TDD, GOOS, Mockist. Discovery testing (is.gd/discovery_testing).

### Test Double
Fake object, stub, mock, spy.

Justin isn't completely pro-mock.

Use Thoughtful Isolation. Not haphazard mocking.


## Frameworks or something
Integration concerns.

Framework Dilemma
- Focus on integration problems
- Test helpers are very integrated
- Users only write integration tests

Bad failutre messages can easily offset your tests fastness.

minitest-given keeps calling the object to output useful failure information.

## Feedback loops

Profile your own feedback loops. How long does it take to run a test suite?


## Painful test data
|---|-----|----------|-----|--------|
inline fixtures data dump self-priming

Inline for models
Fixtures for intgration tests
Data dump for smoke tests
Self-priming against staging/production (ghost inspector?)

## Superlinear build slow down
Set a firm cap on build duration and then enforce it.
- Then make stuff faster or delete a test

## False negatives
What does it mean when a test fails

True negative means the test was right and the code needs to change
False negative means the test was wrong and the code doesn't need to change

True negatives are depressingly rare.

False negatives erode confidence in our tests. They're why CI build bums you out.

Top causes of fale negatives:
- Redudant coverage
- Slow tests (too slow to run so screw it)
  - Integration tests are slow

Track weather each build failure is tru oe fasle. And how long does it take to fix.
Use failure data to analyze root cause

Hire @testdouble if your team needs test help. Senior dev consults on staff.

TL;DR: Please write fewer integration tests
