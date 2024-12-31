# fixlang-fast-iter

High performance iterator library for Fix.

This library aims to replace `Std::Iterator` in Fix in the future.
It is recommended to hide `Std::Iterator` when using this library as follows.

```
import Iterator; // Import this library.
import Std hiding {Iterator::*, Array::to_iter, String::split}; // Hide entities conflicting with this library. Note that `Std::Iterator` is still imported.
```

The important changes from `Std::Iterator` are as follows.

- Create "static" iterators as much as possible.
  - For example, `Iterator::range` returns a `RangeIterator`, and `Iterator::map` returns a `MapIterator`. These types implement the `advance` function as a method of the `Iterable` trait. This makes the call to `advance` statically dispatched, and a significant performance improvement can be expected for `Std::Iterator`.
  - As a trade-off, since the types of each iterator are different, it is not possible to implement traits such as `Functor`, `Monad`, `Eq`, `Add` for iterators. So `Std::Iterator`, "dynamic iterator", is still useful, and this library provides a bridge between `Iterable` trait and `Std::Iterator`. `Std::Iterator` implements `Iterable` trait, and `to_dyn` converts any `Iterable` to `Std::Iterator`.
- The type of the `advance` function is `[iter : Iterable] iter -> Option (iter, Item iter);`, and the order of the elements in the return pair is reversed from `Std::Iterator::advance`.
  - This is to make it closer to the convention of implementing the state monad.
- The type of the `fold` function is `[iter : Iterable, Item iter = a] s -> (a -> s -> s) -> iter -> s`, and the order of the arguments of the operator is reversed from `Std::Iterator::fold`.
  - `Std::Iterator` adopted the same order as Haskell, but it was changed to a more Fix-like order. For example, in Fix, the order of arguments is `push_back : a -> Array a -> Array a`.
  - The order of arguments of `fold_m`, `loop_iter`, and `loop_iter_m` has also been changed in the same way.

Other functions provided in this module are as follows.

- `to_iter : Array a -> ArrayIterator a` is provided in this module for future replacement of `Std::Array::to_iter`.
- `split : String -> String -> StringSplitIterator` is provided in this module for future replacement of `Std::String::split`.
- Other functions that is good to have in the iterator library.

## Future plan

In a future, `Std::Iterator::*` (i.e., all functions related to `Std::Iterator`, except the type `Std::Iterator`) will be removed from Fix, and this library will be put in `Std`.