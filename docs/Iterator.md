# `module Iterator`

# Types and aliases

## `namespace Iterator`

### `type AppendIterator i1 i2 = unbox struct { ...fields... }`

#### field `iter1 : Std::Option i1`

#### field `iter2 : i2`

### `type ConsIterator i a = unbox struct { ...fields... }`

#### field `head : Std::Option a`

#### field `tail : i`

### `type CountUpIterator = unbox struct { ...fields... }`

#### field `next : Std::I64`

### `type EmptyIterator a = unbox struct { ...fields... }`

Iterators that yields no elements.

### `type FilterIterator i a = unbox struct { ...fields... }`

#### field `iter : i`

#### field `pred : a -> Std::Bool`

### `type FilterMapIterator i a b = unbox struct { ...fields... }`

#### field `iter : i`

#### field `f : a -> Std::Option b`

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

Iterators that yields reversed elements of an iterator.

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

## `namespace Iterator::Array`

### `type ArrayIterator a = unbox struct { ...fields... }`

Iterators that yields elements of an array.

#### field `arr : Std::Array a`

#### field `idx : Std::I64`

## `namespace Iterator::String`

### `type StringSplitIterator = unbox struct { ...fields... }`

#### field `idx : Std::I64`

#### field `str : Std::String`

#### field `strlen : Std::I64`

#### field `sep : Std::String`

#### field `sep_len : Std::I64`

# Traits and aliases

## `namespace Iterator`

### `trait iter : Iterable`

The trait Iterable is a trait for types that can be iterated over.

#### associated type `Item iter`

#### method `advance : iter -> Std::Option (iter, Iterator::Iterable::Item iter)`

# Trait implementations

### `impl [i1 : Iterator::Iterable, i2 : Iterator::Iterable] Iterator::AppendIterator i1 i2 : Iterator::Iterable`

### `impl Iterator::Array::ArrayIterator a : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::ConsIterator i a : Iterator::Iterable`

### `impl Iterator::CountUpIterator : Iterator::Iterable`

### `impl Iterator::EmptyIterator a : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::FilterIterator i a : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::FilterMapIterator i a b : Iterator::Iterable`

### `impl [i2 : Iterator::Iterable, i1 : Iterator::Iterable] Iterator::FlattenIterator i2 i1 : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::IntersperseIterator i a : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::MapIterator i a b : Iterator::Iterable`

### `impl [i1 : Iterator::Iterable, i2 : Iterator::Iterable] Iterator::ProductIterator i1 i2 a b : Iterator::Iterable`

### `impl Iterator::RangeIterator : Iterator::Iterable`

### `impl Iterator::RangeStepIterator : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::ReverseIterator i a : Iterator::Iterable`

### `impl Iterator::StateIterator s a : Iterator::Iterable`

### `impl Iterator::String::StringSplitIterator : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::TakeIterator i : Iterator::Iterable`

### `impl [i : Iterator::Iterable] Iterator::TakeWhileIterator i a : Iterator::Iterable`

### `impl [i1 : Iterator::Iterable, i2 : Iterator::Iterable] Iterator::ZipIterator i1 i2 : Iterator::Iterable`

### `impl Std::Iterator a : Iterator::Iterable`

# Values

## `namespace Iterator`

### `append : [i1 : Iterator::Iterable, i2 : Iterator::Iterable, Iterator::Iterable::Item i1 = a, Iterator::Iterable::Item i2 = a] i2 -> i1 -> Iterator::AppendIterator i1 i2`

Append two iterators.

NOTE: Since this function is designed so that `iter1.append(iter2)` appends `iter2` after `iter1`, `append(iter1, iter2)` appends iterators in the opposite order.

### `bang : [iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] iter -> Iterator::Array::ArrayIterator a`

Convert any iterator to an array iterator.

All elements of the input iterator are collected into an array. Therefore, this function may consume a lot of memory.
On the other hand, iteration may be faster by banging.

### `collect_m : [m : Std::Monad, iter : Iterator::Iterable, Iterator::Iterable::Item iter = m a] iter -> m (Std::Array a)`

Executes monadic actions and collects the results into an array.

### `count_up : Std::I64 -> Iterator::CountUpIterator`

Create an iterator that counts up from a number.

`count_up(start)` generates an infinite sequence of numbers starting from `start`.

### `empty : Iterator::EmptyIterator a`

An iterator that yields no elements.

NOTE: When using this iterator, you may need to specify the type of the iterator explicitly, e.g, `(empty : EmptyIterator I64)`.

### `filter : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] (a -> Std::Bool) -> i -> Iterator::FilterIterator i a`

Filter the elements of an iterator by a predicate.

`iter.filter(pred)` returns an iterator that only yields elements of `iter` for which `pred` returns `true`.

### `filter_map : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] (a -> Std::Option b) -> i -> Iterator::FilterMapIterator i a b`

Filter and map the elements of an iterator.

`iter.filter_map(f)` returns an iterator that applies `f` to each element of `iter` and yields the result if it is `some`.

### `flatten : [i2 : Iterator::Iterable, i1 : Iterator::Iterable, Iterator::Iterable::Item i2 = i1] i2 -> Iterator::FlattenIterator i2 i1`

Flatten an iterator of iterators.

### `fold : [iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] s -> (a -> s -> s) -> iter -> s`

Fold the elements of an iterator from left to right.

Conceptually, `[a0, a1, a2, ...].fold(s, op) = s.op(a0).op(a1).op(a2)...`.

### `fold_m : [m : Std::Monad, iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] s -> (a -> s -> m s) -> iter -> m s`

Fold the elements of an iterator from left to right by monadic action.

### `from_map : (Std::I64 -> a) -> Iterator::MapIterator Iterator::CountUpIterator Std::I64 a`

Create an iterator by a function that returns element at each index.

### `generate : s -> (s -> Std::Option (s, a)) -> Iterator::StateIterator s a`

Create an iterator that generates elements by the state transition function.

### `get_front : [iter : Iterator::Iterable] iter -> Iterator::Iterable::Item iter`

Get the first element of an iterator.

If the iterator is empty, this function aborts the program.

### `get_size : [iter : Iterator::Iterable] iter -> Std::I64`

Get the number of elements in an iterator.

### `intersperse : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] a -> i -> Iterator::IntersperseIterator i a`

Intersperse an element between elements of an iterator.

Example:
```
assert_eq(|_|"", [1, 2, 3].from_array.intersperse(0).to_array, [1, 0, 2, 0, 3]);;
```

### `is_empty : [iter : Iterator::Iterable] iter -> Std::Bool`

Is an iterator empty?

### `loop_iter : [iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] s -> (a -> s -> Std::LoopState s s) -> iter -> s`

Loop over the elements of an iterator.

This function is similar to `fold` but a more general version of it. It allows the user to break out of the loop early.

### `loop_iter_m : [m : Std::Monad, iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] s -> (a -> s -> m (Std::LoopState s s)) -> iter -> m s`

Loop over the elements of an iterator by monadic action.

### `map : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] (a -> b) -> i -> Iterator::MapIterator i a b`

Map a function over an iterator.

`iter.map(f)` returns an iterator that applies `f` to each element of `iter`.

### `pop_front : [iter : Iterator::Iterable] iter -> iter`

Remove the first element of an iterator.

If the iterator is empty, this function does nothing.

### `product : [i1 : Iterator::Iterable, i2 : Iterator::Iterable, Iterator::Iterable::Item i1 = a, Iterator::Iterable::Item i2 = b] i2 -> i1 -> Iterator::ProductIterator i1 i2 a b`

Create an iterator that yields the Cartesian product of two iterators.

NOTE: Since this function is designed so that `iter1.product(iter2)` yields the Cartesian product, the elements of `product(iter2, iter1)` are in the opposite order.

Example:
```
assert_eq(|_|"", range(1, 4).product(['a', 'b'].from_array).to_array, [(1, 'a'), (2, 'a'), (3, 'a'), (1, 'b'), (2, 'b'), (3, 'b')]);;
```

### `push_front : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] a -> i -> Iterator::ConsIterator i a`

Push an element to an iterator.

### `range : Std::I64 -> Std::I64 -> Iterator::RangeIterator`

Create an iterator that generates a range of numbers.

`range(a, b)` generates a range of numbers from `a` to `b - 1`.

If `a` is greater than or equal to `b`, the iterator will an infinite sequence of `a`.

### `range_step : Std::I64 -> Std::I64 -> Std::I64 -> Iterator::RangeStepIterator`

Create an iterator that generates a range of numbers with a step.

### `reverse : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] i -> Iterator::ReverseIterator i a`

Reverses an iterator.

NOTE: This function puts all elements of the iterator into an array, so it may consume a lot of memory.

### `sum : [iter : Iterator::Iterable, a : Std::Additive, Iterator::Iterable::Item iter = a] iter -> a`

Calcculate sum of the elements of an iterator.

### `take : [i : Iterator::Iterable] Std::I64 -> i -> Iterator::TakeIterator i`

Take the first `n` elements of an iterator.

### `take_while : [i : Iterator::Iterable, Iterator::Iterable::Item i = a] (a -> Std::Bool) -> i -> Iterator::TakeWhileIterator i a`

Take elements from an iterator while a predicate holds.

### `to_array : [iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] iter -> Std::Array a`

Convert an iterator to an array.

### `to_dyn : [iter : Iterator::Iterable, Iterator::Iterable::Item iter = a] iter -> Std::Iterator a`

Convert an iterator into a dynamic iterator.

NOTE:

The advantage of dynamic iterator (i.e., `Std::Iterator`) is that it hides how the iterator is constructed and simplifies the type.
This allows, for example,
- `Iterator` can be instances of traits such as `Monad`, `Eq`, etc.
- In a function, it is possible to return two iterators with different constructions depending on the branch.

However, iterating over `Iterator` are much slower than iterating over other iterators provided in this namespace.
Therefore, if performance is important, it is better to avoid using `Iterator`.
In particular, if you iterate over the same `Iterator` multiple times,
consider converting it to an `ArrayIterator` using `bang` before iterating.

### `zip : [i1 : Iterator::Iterable, i2 : Iterator::Iterable] i2 -> i1 -> Iterator::ZipIterator i1 i2`

Zip two iterators.

NOTE: Since this function is designed so that `iter1.zip(iter2)` zips `iter1` and `iter2`, the elements of `zip(iter2, iter1)` are in the opposite order.

## `namespace Iterator::Array`

### `to_iter : Std::Array a -> Iterator::Array::ArrayIterator a`

Convert an array to an iterator.

## `namespace Iterator::Iterable`

### `advance : [iter : Iterator::Iterable] iter -> Std::Option (iter, Iterator::Iterable::Item iter)`

## `namespace Iterator::String`

### `split : Std::String -> Std::String -> Iterator::String::StringSplitIterator`

`str.split(sep)` splits `str` by `sep` into an iterator.

Example:
```
assert_eq(|_|"Ex. 1", "ab,c,".split(",").to_array, ["ab", "c", ""]);;
assert_eq(|_|"Ex. 2", "abc".split(",").to_array, ["abc"]);;
assert_eq(|_|"Ex. 3", "abc".split("").to_array, ["a", "b", "c"]);; // Special behavior when the separator is empty.
```