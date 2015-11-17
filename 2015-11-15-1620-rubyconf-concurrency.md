# Writing Concurrent Libraries For All Ruby Runtimes by Petr Chalupa

concurrent-ruby gem (used by rails 5, and other good things)

## Implementing a concurrent abstractions
- Processor or compiler are free to reorder
  - As long as it keeps sequential consistency
  - Unless we tell it not to reorder
  - Desirable
- Another thread may see strange value
- All possible orders have to be considered
- A framework is needed to reason about the orders

## Future

Reference of a value which is not yet computed

~ Code example
