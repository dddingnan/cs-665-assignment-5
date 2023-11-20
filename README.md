| CS-665     | Software Design & Patterns |
| ---------- | -------------------------- |
| Name       | Dingnan Hsu                |
| Date       | 11/19/2023                 |
| Course     | 2023 Fall                  |
| Assignment | 5                          |

# Assignment Overview

Examine the Caffeine project and identify at least three instances of design presentation. Description utilized (identifying the relevant components), how it functions the designated design patterns, and implementation details.

- Caffeine:
  - https://github.com/ben-manes/caffeine
  - Caffeine is a high-performance, near-optimal caching library.

# Design Patterns And Implementation Description

1. `Strategy Design Pattern`:

   - See PDF Reference -> Here
   - `Strategy Interface (Policy<K, V>)`:

     - This serves as the primary strategy interface in the codebase. It defines a set of methods that are common to all caching strategies, such as `isRecordingStats(), getIfPresentQuietly(), refreshes(), eviction(), expireAfterAccess(), expireAfterWrite(), expireVariably(), and refreshAfterWrite().` These methods define the operations that can be performed on a cache, which may vary depending on the specific eviction and expiration policies used.

   - `Concrete Strategies (VarExpiration<K, V>, FixedExpiration<K, V>, FixedRefresh<K, V>, Eviction<K, V>)`:

     - These classes implement the `Policy<K, V>` interface and provide concrete behavior for cache entry management, such as how and when a cache entry should expire or be evicted.

   - `Context (CacheEntry<K, V>)`:

     - These utilize the Policy interface to manage cache entries. This context would hold a reference to a `Policy<K, V>` and delegate cache operations to the underlying strategy, whether it's for eviction, expiration, or refresh.

   - The `Policy` interface and its related concrete strategy interfaces encapsulate different cache policies that can be interchanged as needed, which is the essence of the Strategy design pattern.

2. `Iterator Design Pattern`:

   - See PDF Reference -> Here
   - `Iterator (Iterator Interface)`:

     - This is the core interface in the Iterator pattern that defines the standard for traversal operations.
       - The methods include:
         - `hasNext()`: Checks if there are more elements to iterate over.
         - `next()`: Moves the iterator to the next element and returns it.
         - `remove()`: Removes the last element returned by the iterator from the underlying collection.

   - `Concrete Iterator (EntryIterator<K, V>, ValueIterator<K, V>, KeyIterator<K, V>)`:

     - `EntryIterator<K, V>`: Iterates over key-value pairs.
     - `ValueIterator<K, V>`: Iterates over values.
     - `KeyIterator<K, V>`: Iterates over keys.

   - `Aggregate (EntrySetView<K, V>, ValuesView<K, V>, KeySetView<K, V>)`:

     - These are the collections that provide iterators.

   - `Spliterator (EntrySpliterator<K, V>, ValueSpliterator<K, V>, KeySpliterator<K, V>`:

     - These are designed to provide additional capabilities, such as splitting the set of elements into parts for parallel processing or providing more detailed information about the collection.

   - The Iterator pattern provides a unified way to iterate over different views of a cache without exposing the internal structure of the cache itself, whether iterating over entries, keys, or values.

3. `Lazy Loading Pattern`: This pattern can be beneficial for your application in managing resource usage efficiently, especially when dealing with large sets of flight data that might not all need to be loaded into memory at once.

# GitHub Repository Link:

https://github.com/dddingnan/cs-665-assignment-5
