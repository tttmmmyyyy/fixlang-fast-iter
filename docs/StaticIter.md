# `module StaticIter`

# Types and aliases

## `namespace StaticIter`

### `type AppendIterator i1 i2 = unbox struct { ...fields... }`

#### field `iter1 : Std::Option i1`

#### field `iter2 : i2`

### `type ArrayIterator a = unbox struct { ...fields... }`

#### field `arr : Std::Array a`

#### field `idx : Std::I64`

### `type ConsIterator i a = unbox struct { ...fields... }`

#### field `head : Std::Option a`

#### field `tail : i`

### `type CountUpIterator = unbox struct { ...fields... }`

#### field `next : Std::I64`

### `type DynamicIterator a = unbox struct { ...fields... }`

#### field `next : () -> Std::Option (StaticIter::DynamicIterator a, a)`

### `type EmptyIterator a = unbox struct { ...fields... }`

### `type FilterIterator i a = unbox struct { ...fields... }`

#### field `iter : i`

#### field `pred : a -> Std::Bool`

### `type FlattenIterator i2 i1 = unbox struct { ...fields... }`

#### field `i2 : i2`

#### field `i1 : Std::Option i1`

### `type IntersperseIterator i a = unbox struct { ...fields... }`

#### field `iter : i`

#### field `sep : a`

#### field `next_is_sep : Std::Bool`

### `type MapIterator i a b = unbox struct { ...fields... }`

#### field `iter : i`

#### field `f : a -> b`

### `type ProductIterator i1 i2 a b = unbox struct { ...fields... }`

#### field `iter1 : i1`

#### field `iter2 : i2`

#### field `e2 : Std::Option b`

#### field `iter1_org : i1`

### `type RangeIterator = unbox struct { ...fields... }`

#### field `next : Std::I64`

#### field `end : Std::I64`

### `type RangeStepIterator = unbox struct { ...fields... }`

#### field `next : Std::I64`

#### field `end : Std::I64`

#### field `step : Std::I64`

### `type ReverseIterator i a = unbox struct { ...fields... }`

#### field `idx : Std::I64`

#### field `arr : Std::Array a`

### `type StateIterator s a = unbox struct { ...fields... }`

#### field `state : Std::Option s`

#### field `transit : s -> Std::Option (s, a)`

### `type TakeIterator i = unbox struct { ...fields... }`

Takes at most `n` elements from an iterator.

#### field `iter : i`

#### field `n : Std::I64`

### `type TakeWhileIterator i a = unbox struct { ...fields... }`

#### field `iter : i`

#### field `pred : a -> Std::Bool`

### `type ZipIterator i1 i2 = unbox struct { ...fields... }`

#### field `iter1 : i1`

#### field `iter2 : i2`

# Traits and aliases

## `namespace StaticIter`

### `trait iter : Iterable`

The trait Iterable is a trait for types that can be iterated over.

#### associated type `Item iter`

#### method `advance : iter -> Std::Option (iter, StaticIter::Iterable::Item iter)`

# Trait implementations

### `impl [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable] StaticIter::AppendIterator i1 i2 : StaticIter::Iterable`

### `impl StaticIter::ArrayIterator a : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::ConsIterator i a : StaticIter::Iterable`

### `impl StaticIter::CountUpIterator : StaticIter::Iterable`

### `impl StaticIter::DynamicIterator : Std::Monad`

### `impl StaticIter::DynamicIterator a : StaticIter::Iterable`

### `impl StaticIter::EmptyIterator a : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::FilterIterator i a : StaticIter::Iterable`

### `impl [i2 : StaticIter::Iterable, i1 : StaticIter::Iterable] StaticIter::FlattenIterator i2 i1 : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::IntersperseIterator i a : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::MapIterator i a b : StaticIter::Iterable`

### `impl [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable] StaticIter::ProductIterator i1 i2 a b : StaticIter::Iterable`

### `impl StaticIter::RangeIterator : StaticIter::Iterable`

### `impl StaticIter::RangeStepIterator : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::ReverseIterator i a : StaticIter::Iterable`

### `impl StaticIter::StateIterator s a : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::TakeIterator i : StaticIter::Iterable`

### `impl [i : StaticIter::Iterable] StaticIter::TakeWhileIterator i a : StaticIter::Iterable`

### `impl [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable] StaticIter::ZipIterator i1 i2 : StaticIter::Iterable`

# Values

## `namespace StaticIter`

### `append : [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable, StaticIter::Iterable::Item i1 = a, StaticIter::Iterable::Item i2 = a] i2 -> i1 -> StaticIter::AppendIterator i1 i2`

Append two iterators.

NOTE: Since this function is designed so that `iter1.append(iter2)` appends `iter2` after `iter1`, `append(iter1, iter2)` appends iterators in the opposite order.

### `bang : [iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] iter -> StaticIter::ArrayIterator a`

Convert any iterator to an array iterator.

### `count_up : Std::I64 -> StaticIter::CountUpIterator`

Create an iterator that counts up from a number.

`count_up(start)` generates an infinite sequence of numbers starting from `start`.

### `empty : StaticIter::EmptyIterator a`

An iterator that yields no elements.

NOTE: When using this iterator, you may need to specify the type of the iterator explicitly, e.g, `(empty : EmptyIterator I64)`.

### `filter : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] (a -> Std::Bool) -> i -> StaticIter::FilterIterator i a`

Filter the elements of an iterator by a predicate.

`iter.filter(pred)` returns an iterator that only yields elements of `iter` for which `pred` returns `true`.

### `flatten : [i2 : StaticIter::Iterable, i1 : StaticIter::Iterable, StaticIter::Iterable::Item i2 = i1] i2 -> StaticIter::FlattenIterator i2 i1`

Flatten an iterator of iterators.

### `fold : [iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] s -> (a -> s -> s) -> iter -> s`

Fold the elements of an iterator from left to right.

Conceptually, `[a0, a1, a2, ...].fold(s, op) = s.op(a0).op(a1).op(a2)...`.

### `fold_m : [m : Std::Monad, iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] s -> (a -> s -> m s) -> iter -> m s`

Fold the elements of an iterator from left to right by monadic action.

### `from_array : Std::Array a -> StaticIter::ArrayIterator a`

Convert an array to an iterator.

### `generate : s -> (s -> Std::Option (s, a)) -> StaticIter::StateIterator s a`

Create an iterator that generates elements by the state transition function.

### `get_front : [iter : StaticIter::Iterable] iter -> StaticIter::Iterable::Item iter`

Get the first element of an iterator.

If the iterator is empty, this function aborts the program.

### `get_size : [iter : StaticIter::Iterable] iter -> Std::I64`

Get the number of elements in an iterator.

### `intersperse : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] a -> i -> StaticIter::IntersperseIterator i a`

Intersperse an element between elements of an iterator.

Example:
```
assert_eq(|_|"", [1, 2, 3].from_array.intersperse(0).to_array, [1, 0, 2, 0, 3]);;
```

### `is_empty : [iter : StaticIter::Iterable] iter -> Std::Bool`

Is an iterator empty?

### `loop_iter : [iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] s -> (a -> s -> Std::LoopState s s) -> iter -> s`

Loop over the elements of an iterator.

This function is similar to `fold` but a more general version of it. It allows the user to break out of the loop early.

### `loop_iter_m : [m : Std::Monad, iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] s -> (a -> s -> m (Std::LoopState s s)) -> iter -> m s`

Loop over the elements of an iterator by monadic action.

### `map : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] (a -> b) -> i -> StaticIter::MapIterator i a b`

Map a function over an iterator.

`iter.map(f)` returns an iterator that applies `f` to each element of `iter`.

### `pop_front : [iter : StaticIter::Iterable] iter -> iter`

Remove the first element of an iterator.

If the iterator is empty, this function does nothing.

### `product : [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable, StaticIter::Iterable::Item i1 = a, StaticIter::Iterable::Item i2 = b] i2 -> i1 -> StaticIter::ProductIterator i1 i2 a b`

Create an iterator that yields the Cartesian product of two iterators.

NOTE: Since this function is designed so that `iter1.product(iter2)` yields the Cartesian product, the elements of `product(iter2, iter1)` are in the opposite order.

Example:
```
assert_eq(|_|"", range(1, 4).product(['a', 'b'].from_array).to_array, [(1, 'a'), (2, 'a'), (3, 'a'), (1, 'b'), (2, 'b'), (3, 'b')]);;
```

### `push_front : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] a -> i -> StaticIter::ConsIterator i a`

Push an element to an iterator.

### `range : Std::I64 -> Std::I64 -> StaticIter::RangeIterator`

Create an iterator that generates a range of numbers.

`range(a, b)` generates a range of numbers from `a` to `b - 1`.

If `a` is greater than or equal to `b`, the iterator will an infinite sequence of `a`.

### `range_step : Std::I64 -> Std::I64 -> Std::I64 -> StaticIter::RangeStepIterator`

Create an iterator that generates a range of numbers with a step.

### `reverse : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] i -> StaticIter::ReverseIterator i a`

Reverses an iterator.

NOTE: This function puts all elements of the iterator into an array, so it may consume a lot of memory.

### `take : [i : StaticIter::Iterable] Std::I64 -> i -> StaticIter::TakeIterator i`

Take the first `n` elements of an iterator.

### `take_while : [i : StaticIter::Iterable, StaticIter::Iterable::Item i = a] (a -> Std::Bool) -> i -> StaticIter::TakeWhileIterator i a`

Take elements from an iterator while a predicate holds.

### `to_array : [iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] iter -> Std::Array a`

Convert an iterator to an array.

### `to_dyn : [iter : StaticIter::Iterable, StaticIter::Iterable::Item iter = a] iter -> StaticIter::DynamicIterator a`

Convert an iterator to a dynamic iterator.

NOTE:

The advantage of `DynamicIterator` is that it hides how the iterator is constructed and simplifies the type,
especially allowing the use of monadic operations.
However, iterating over `DynamicIterator` are much slower than other iterators provided in this module.
Therefore, if performance is important, it is better to avoid using `DynamicIterator`.

In particular, if you iterate over the same `DynamicIterator` multiple times,
consider converting it to an `ArrayIterator` using `bang` before iterating.

### `zip : [i1 : StaticIter::Iterable, i2 : StaticIter::Iterable] i2 -> i1 -> StaticIter::ZipIterator i1 i2`

Zip two iterators.

NOTE: Since this function is designed so that `iter1.zip(iter2)` zips `iter1` and `iter2`, the elements of `zip(iter2, iter1)` are in the opposite order.

## `namespace StaticIter::DynamicIterator`

### `empty : StaticIter::DynamicIterator a`

### `singleton : a -> StaticIter::DynamicIterator a`

## `namespace StaticIter::Iterable`

### `advance : [iter : StaticIter::Iterable] iter -> Std::Option (iter, StaticIter::Iterable::Item iter)`