# A Tale of Two Feature Flags by Rebecca Sliter

## What is a feature flag

- I have an idea! But...
  - It's a lot of work
  - I'm worried about deploying months of code
  - How does it perform for a set of users?
  - External dependencies

  Solution? Put it behind a feature flag.

  ```
  - if feature_on? :coupons
    div#coupons
    # ...
  ```

- Finder grained toggling (admin-only, location/language specific)
- A/B Testing
- Graceful degradation when a feature fails

## Feature flags in practice

Story time!

  One clearly-defined feature behind a single flag

  Project changed. Let's release different parts to different users. So they created two-flags. But unfortunately they turned out to be tightly coupled.

Feature flags ought to be simple. Very simple boolean. Don't nest them or think hard about them. If you spend a lot of time implementing a flag, then feature flags aren't the answer.

__Moral: Stick to one flag per feature__

## Where to flag?
Treat flagged code as new code

## How to kill old flags?
Flags have a maintainer and deadline attached. CI server raises hell when deadline is passed.
