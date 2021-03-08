Key-Value Store Coding Exercise
===============================

Implement a key-value store with the following interface.

Basic operations
----------------

1. Sets a key -> value pair in the store.
 
`set(key: string, value: int)`

2. Gets a value from the store using a key. What should this do if this key isn't found in the store?

`get(key: string): int`

3. Deletes a specified key from the store.

`unset(key: string)`

Transactions
------------

Next we'd like to be able to initiate transactions that allow us to either commit the operations performed in transaction, or roll them back. For example:

```
kv.set("a", 1)
kv.get("a") // => 1

// Transaction with rollback:
kv.transaction()
kv.set("a", 10)
kv.get("a") // => 10

kv.rollback()
kv.get("a") // => 1

// Transaction with commit: 
kv.transaction()
kv.set("a", 123)

kv.commit()
kv.get("a") => 123
```

4. Starts a new transaction:

`transaction()`

5. Rolls back a transaction, reversing all operations and ending the transaction:

`rollback()`

6. Commits the operations performed in a transaction so they are permanent:

`commit()`

Nested transactions
-------------------

What changes would we need to make to support nested transactions?

```
// Transaction 1
kv.transaction()
kv.set("a", 1)

// Transaction 2
kv.transaction()
kv.set("a", 10)

// First rollback
kv.rollback()
kv.get("a") // => 1

// Second rollback
kv.rollback()
kv.get("a") // => key doesn't exist
```
