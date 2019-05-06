# Data Structure and Performance

There are some new data sctructures that have been added in the last versions of the PHP language such as:

### Collection

Collection is the base interface which covers common functionality like foreach, echo, count, print_r, var_dump, serialize, json_encode, and clone. All collections also serve as iterators, allowing you to loop over them as if they were simple PHP arrays.

- [Eloquent Collections](https://laravel.com/docs/5.8/eloquent-collections)
- [Doctrine Collections](https://www.doctrine-project.org/projects/doctrine-collections/en/1.6/index.html)

### Sequence

Sequence describes the behaviour of values arranged in a single, linear dimension. Some languages refer to this as a List. It’s similar to an array that uses incremental integer keys, with the exception of a few characteristics:

Values will always be indexed as **[0, 1, 2, …, size - 1]**.
Removing or inserting updates the position of all successive values.
Only allowed to access values by index in the range **[0, size - 1]**.

### Vector

A Vector is a Sequence of values in a contiguous buffer that grows and shrinks automatically. It’s the most efficient sequential structure because a value’s index is a direct mapping to its index in the buffer, and the growth factor isn't bound to a specific multiple or exponent.

### Hashable

An interface which allows objects to be used as keys. It’s an alternative to spl_object_hash, which determines an object’s hash based on its handle: this means that two objects that are considered equal by an implicit definition would not be treated as equal because they are not the same instance.

### Final Thoughts

Those data structures are a very powerful tool is we are smart enough to use them in the right situation. There are some scenarios when we will need to rely on database query instead of using collections to iterate over a large dataset. For example, if we need to group by a collection which constaing more than 1,000 elements, we should consider to refactor our code and previously group by our date when retrieving that information from the database.

### Documentation

- [PHPs new hashtable implementation](https://nikic.github.io/2014/12/22/PHPs-new-hashtable-implementation.html)