# Using Ruby in Security Critical Applications By Tom Macklin

## Pre

The reasonable expectations of your CTO by Uncle Bob (2012)

## Assurance
Assurance isn't about telling you that everythign will be okay. It's about talking about assurance/evidence that you can decide for yourself if everything is okay.

Fast, Reliable and Cheap. Pick two.

We're going to make mistakes. There will be bugs in our code.

A security-critical system should have the right security controls, in the right places with the right assurances.

## Architecture

Keep it NEAT

### Non-bypassible
Like a circuit breaker. Has to be the only way from point A to point B.

### Evaluatable
Check flog. Keep your code simple and you should be below 20 (flog score).

### Always Invoked
Make the insecure option non-default

### Tamper Evident
Gave an example of a canary in a coal mine.
Stack Canaries


## Checklist (Assurances and Controls)

### OS Controls
- Mandatory Access Controls (MAC)

Separate databases with OS access policies + logic servers mediating write operations = MAC data separation

Takeaways
 - Abstract OS "hooks" with FFI
 - Stub OS controls for development
 - Don't give your app system privileges

A bunch of compile time binary protection stuff. See PoC||GTFO.

### Application Layer
Try to avoid XML. Processing it is very complicated.

Then he talked about a bunch of OS control stuff again.

## Security (Penetration) Testing

