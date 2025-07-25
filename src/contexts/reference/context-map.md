# `ContextMap`

---

```rust
pub struct ContextManager<K, V, S = RandomState> { ... }
```

## `impl<K, V> ContextManager<K, V, RandomState>`

### `K: Hash + Eq`

---

> ```rust
> pub fn with_empty() -> Self
> ```
> 
> Creates a context manager initialized with an empty context.
> 
> ```rust
> let mut manager = ContextManager::with_empty();
> 
> manager.insert("x", 1);
> 
> assert_eq!(&manager["x"], &1);
> ```

> ```rust
> pub fn new() -> Self
> ```
> 
> Creates an empty context manager.
> 
> ```rust
> let mut manager = ContextManager::new();
> 
> manager.insert("x", 1);
> 
> assert!(!manager.contains_key("x"));
> ```

> ```rust
> pub fn with_capacity(capacity: usize) -> Self
> ```
> 
> Creates an empty context manager with space for capacity contexts.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.insert("x", 1);
> 
> assert!(!manager.contains_key("x"));
> ```

> ```rust
> pub fn collapse(self) -> HashMap<K, V>
> ```
> 
> Aggregates all contexts into a single map where keys have their most recent value.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("y", 3)]));
> manager.push(HashMap::from([("w", 1), ("x", 2)]));
> manager.push(HashMap::from([("y", 4), ("z", 3)]));
> 
> let map = manager.collapse();
> 
> assert_eq!(&map["w"], &1);
> assert_eq!(&map["x"], &2);
> assert_eq!(&map["y"], &4);
> assert_eq!(&map["z"], &3);
> ```

> ```rust
> pub fn push_empty(&mut self)
> ```
> 
> Adds an empty local context.
> 
> ```rust
> let mut manager = ContextManager::with_empty();
> 
> manager.insert("x", 1);
> 
> assert_eq!(manager.get_local("x"), Some(&1));
> 
> manager.push_empty();
> 
> assert_eq!(manager.get_local("x"), None);
> ```


## `impl<K, V, S> ContextManager<K, V, S>`

---

> ```rust
> pub fn is_empty(&self) -> bool
> ```
> 
> Returns the number of contexts in the manager.
> 
> ```rust
> let mut manager = ContextManager::<&str, i32>::new();
> 
> assert!(manager.is_empty());
> 
> manager.push_empty();
> 
> assert!(!manager.is_empty());
> 
> manager = ContextManager::with_empty();
> 
> assert!(!manager.is_empty());
> ```

> ```rust
> pub fn len(&self) -> usize
> ```
> 
> Returns the number of contexts in the manager.
> 
> ```rust
> let mut manager = ContextManager::<&str, i32>::new();
> 
> assert_eq!(manager.len(), 0);
> 
> manager.push_empty();
> 
> assert_eq!(manager.len(), 1);
> 
> manager = ContextManager::with_empty();
> 
> assert_eq!(manager.len(), 1);
> ```

> ```rust
> pub fn pop(&mut self) -> Option<HashMap<K, V, S>>
> ```
> 
> Removes the local context if one is present.
> 
> ```rust
> let mut manager = ContextManager::with_empty();
> 
> manager.insert("x", 1);
> 
> let popped = manager.pop();
> 
> assert!(popped.is_some());
> assert_eq!(popped.unwrap().get("x"), Some(&1));
> assert_eq!(manager.pop(), None);
> ```

> ```rust
> pub fn push(&mut self, context: HashMap<K, V, S>)
> ```
> 
> Adds a new local context.
> 
> ```rust
> let mut manager = ContextManager::with_empty();
> 
> manager.insert("x", 1);
> 
> assert_eq!(&manager["x"], &1);
> assert_eq!(manager.get("y"), None);
> 
> manager.push(HashMap::from([("y", 2)]));
> 
> assert_eq!(&manager["y"], &2);
> ```


## `impl<K, V, S> ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher`

---

> ```rust
> pub fn collapse_into(self, src: &mut HashMap<K, V, S>)
> ```
> 
> Aggregates all contexts storing each key and its most recent value into src.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("y", 4)]));
> manager.push(HashMap::from([("w", 2), ("x", 3)]));
> 
> let mut map = HashMap::from([("v", 1), ("x", 2), ("z", 5)]);
> 
> manager.collapse_into(&mut map);
> 
> assert_eq!(&map["v"], &1);
> assert_eq!(&map["w"], &2);
> assert_eq!(&map["x"], &3);
> assert_eq!(&map["y"], &4);
> assert_eq!(&map["z"], &5);
> ```

> ```rust
> pub fn contains_key<Q>(&self, key: &Q) -> bool
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Whether a key is present in the context.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("x", 2)]));
> 
> assert!(manager.contains_key(&"w"));
> assert!(manager.contains_key(&"x"));
> assert!(!manager.contains_key(&"y"));
> ```

> ```rust
> pub fn contains_local_key<Q>(&self, key: &Q) -> bool
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Whether a key is present in the local context
> 
> ```rust
> let mut manager = ContextManager::new();
> 
> manager.push(HashMap::from([("w", 1)]));
> 
> assert!(manager.contains_local_key("w"));
> 
> manager.push_empty();
> 
> assert!(!manager.contains_local_key("w"));
> ```

> ```rust
> pub fn get<Q>(&self, key: &Q) -> Option<&V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a reference to the value associated with key.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("x", 2)]));
> 
> assert_eq!(manager.get(&"w"), Some(&1));
> assert_eq!(manager.get(&"x"), Some(&2));
> assert_eq!(manager.get(&"y"), None);
> ```

> ```rust
> pub fn get_all<Q>(&self, key: &Q) -> Vec<&V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a vector of references to all values associated with key, ordered by precedence.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("w", 2)]));
> manager.push(HashMap::from([("w", 3)]));
> 
> assert_eq!(manager.get_all(&"w"), vec![&3, &2, &1]);
> assert_eq!(manager.get_all(&"x"), Vec::<&i32>::new());
> ```

> ```rust
> pub fn get_from<Q>(&self, index: usize, key: &Q) -> Option<&V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a reference to the value associated with key starting with the context at index.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("x", 2)]));
> manager.push(HashMap::from([("w", 3)]));
> 
> assert_eq!(manager.get_from(0, &"w"), Some(&3));
> assert_eq!(manager.get_from(1, &"w"), Some(&1));
> assert_eq!(manager.get_from(2, &"w"), Some(&1));
> assert_eq!(manager.get_from(3, &"w"), None);
> ```

> ```rust
> pub fn get_local<Q>(&self, key: &Q) -> Option<&V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a reference to the value associated with key in the local context.
> 
> ```rust
>  let mut manager = ContextManager::from([("w", 1)]);
> 
>  assert_eq!(manager.get_local(&"w"), Some(&1));
> 
>  manager.push_empty();
> 
>  assert_eq!(manager.get_local(&"w"), None);
> ```

> ```rust
> pub fn get_local_mut<Q>(&mut self, key: &Q) -> Option<&mut V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a mutable reference to the value associated with key in the local context.
> 
> ```rust
>  let mut manager = ContextManager::from([("w", 1)]);
> 
>  if let Some(w) = manager.get_local_mut("w") {
>      *w = 2;
>  }
> 
>  assert_eq!(manager.get(&"w"), Some(&2));
> 
>  manager.push_empty();
> 
>  assert_eq!(manager.get_local_mut(&"w"), None);
> ```

> ```rust
> pub fn get_mut<Q>(&mut self, key: &Q) -> Option<&mut V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a mutable reference to the value associated with key.
> 
> ```rust
> let mut manager = ContextManager::from([("w", 1)]);
> 
> if let Some(v) = manager.get_mut("w") {
>     *v = 2;
> }
> 
> assert_eq!(&manager["w"], &2);
> assert_eq!(manager.get_mut(&"x"), None);
> ```

> ```rust
> pub fn get_mut_from<Q>(&mut self, index: usize, key: &Q) -> Option<&mut V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Returns a reference to the value associated with key starting with the context at index.
> 
> ```rust
> let mut manager = ContextManager::new();
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("w", 2)]));
> 
> if let Some(v) = manager.get_mut_from(1, "w") {
>     *v = 3;
> }
> 
> assert_eq!(manager.get_from(0, "w"), Some(&2));
> assert_eq!(manager.get_from(1, "w"), Some(&3));
> assert_eq!(manager.get_mut_from(2, "w"), None);
> ```

> ```rust
> pub fn insert(&mut self, key: K, value: V) -> Option<V>
> ```
> 
> Associates value with key in the local context if there is one.
> 
> ```rust
> let mut manager = ContextManager::new();
> 
> assert_eq!(manager.insert("w", 1), None);
> assert_eq!(manager.get("w"), None);
> 
> manager.push_empty();
> 
> manager.insert("w", 1);
> 
> assert_eq!(manager.insert("w", 2), Some(1));
> 
> manager.push_empty();
> 
> assert_eq!(manager.insert("w", 3), None);
> ```

> ```rust
> pub fn remove<Q>(&mut self, key: &Q) -> Option<V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Removes key from the local context if one is present.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> assert_eq!(manager.remove("w"), None);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("w", 2)]));
> 
> assert_eq!(manager.remove("w"), Some(2));
> assert_eq!(manager.remove("w"), None);
> assert_eq!(&manager["w"], &1);
> ```

> ```rust
> pub fn remove_all<Q>(&mut self, key: &Q) -> Vec<V>
> where
>     K: Borrow<Q>,
>     Q: ?Sized + Hash + Eq
> ```
> 
> Removes all instances of key from the context manager, returning a vector of the values, ordered by precedence.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("w", 2)]));
> manager.push(HashMap::from([("w", 3)]));
> 
> assert_eq!(manager.remove_all(&"w"), vec![3, 2, 1]);
> assert_eq!(manager.remove_all(&"x"), vec![]);
> ```

## `impl<K, V, S> ContextManager<K, V, S>`

### `K: Hash + Eq + Clone, V: Clone, S: BuildHasher + Clone`

---

> ```rust
> pub fn fork(&self) -> Option<ContextManager<K, V, S>>
> ```
> 
> Creates a new context manager initialized with a clone of the current local context.
> 
> Equivalent to `manager.fork_from(0)`.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> assert_eq!(manager.fork(), None);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("x", 2)]));
> manager.push(HashMap::from([("y", 3)]));
> 
> let forked = manager.fork().unwrap();
> 
> assert_eq!(forked.get("w"), None);
> assert_eq!(forked.get("x"), None);
> assert_eq!(&forked["y"], &3);
> ```

> ```rust
> pub fn fork_from(&self, index: usize) -> Option<ContextManager<K, V, S>>
> ```
> 
> Creates a new context manager initialized with clones of all contexts from the local one up to 
> and including the one at index.
> 
> `manager.fork_from(manager.len() - 1)` is equivalent to `manager.clone()`.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("w", 1)]));
> manager.push(HashMap::from([("x", 2)]));
> manager.push(HashMap::from([("y", 3)]));
> 
> let forked = manager.fork_from(1).unwrap();
> 
> assert_eq!(forked.get("w"), None);
> assert_eq!(&forked["x"], &2);
> assert_eq!(&forked["y"], &3);
> 
> let invalid_fork = manager.fork_from(3);
> 
> assert_eq!(invalid_fork, None);
> ```

> ```rust
> pub fn push_local(&mut self)
> ```
> 
> Adds a new context that is a clone of the local context, if one is present.
> 
> ```rust
> let mut manager = ContextManager::from([("w", 1)]);
> manager.push_local();
> 
> assert_eq!(&manager["w"], &1);
> 
> let w = manager.get_mut("w").unwrap();
> 
> *w = 2;
> 
> assert_eq!(&manager["w"], &2);
> 
> manager.pop();
> 
> assert_eq!(&manager["w"], &1);
> ```

> ```rust
> pub fn push_with_local(&mut self, context: HashMap<K, V, S>)
> ```
> 
> Adds a new local context merged with the previous local context.
> 
> The new context has higher precedence.
> 
> ```rust
> let mut manager = ContextManager::from([("w", 1)]);
> let context = HashMap::from([("x", 2)]);
> 
> manager.push_with_local(context);
> 
> assert_eq!(manager.get_local("w"), Some(&1));
> assert_eq!(&manager["x"], &2);
> 
> manager.pop();
> 
> assert_eq!(&manager["w"], &1);
> assert_eq!(manager.get("x"), None);
> ```

## `impl<K, V, S> ContextManager<K, V, S>`

### `K: Ord`

---

> ```rust
> pub fn collapse_ordered(self) -> BTreeMap<K, V>
> ```
> 
> Aggregates all contexts into a single map where keys have their most recent value.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("y", 3)]));
> manager.push(HashMap::from([("w", 1), ("x", 2)]));
> manager.push(HashMap::from([("y", 4), ("z", 3)]));
> 
> let map = manager.collapse_ordered();
> 
> assert_eq!(&map["w"], &1);
> assert_eq!(&map["x"], &2);
> assert_eq!(&map["y"], &4);
> assert_eq!(&map["z"], &3);
> ```

> ```rust
> pub fn collapse_into_ordered(self, src: &mut BTreeMap<K, V>)
> ```
> 
> Aggregates all contexts storing each key and its most recent value into src.
> 
> ```rust
> let mut manager = ContextManager::with_capacity(3);
> 
> manager.push(HashMap::from([("y", 4)]));
> manager.push(HashMap::from([("w", 2), ("x", 3)]));
> 
> let mut map = BTreeMap::from([("v", 1), ("x", 2), ("z", 5)]);
> 
> manager.collapse_into_ordered(&mut map);
> 
> assert_eq!(&map["v"], &1);
> assert_eq!(&map["w"], &2);
> assert_eq!(&map["x"], &3);
> assert_eq!(&map["y"], &4);
> assert_eq!(&map["z"], &5);
> ```

## `impl<K, V, S> Clone for ContextManager<K, V, S>`

### `K: Clone, V: Clone, S: Clone`

---

> ```rust
> fn clone(&self) -> Self
> ```
> 
> Returns a duplicate of the value. Read more

> ```rust
> const fn clone_from(&mut self, source: &Self)
> ```
> 
> Performs copy-assignment from source. Read more

## `impl<K, V, S> Debug for ContextManager<K, V, S>`

### K: Debug, V: Debug, S: Debug

---

> ```rust
> fn fmt(&self, f: &mut Formatter<'_>) -> Result
> ```
> 
> Formats the value using the given formatter. Read more

## `impl<K, V, S> Default for ContextManager<K, V, S>`

> ```rust
> fn default() -> Self
> ```
> 
> Creates an empty context manager

## `impl<K, V, S> Extend<(K, V)> for ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher + Default`

---

> ```rust
> fn extend<I: IntoIterator<Item = (K, V)>>(&mut self, iter: I)
> ```
> 
> Adds key-value pairs from an iterator to the context manager.
> 
> If the context manager is empty, a new HashMap<K, V, S> is created with the default hasher.

> ```rust
> fn extend_one(&mut self, item: A)
> ```
> 
> 🔬This is a nightly-only experimental API. (extend_one)
> 
> Extends a collection with exactly one element.

> ```rust
> fn extend_reserve(&mut self, additional: usize)
> ```
> 
> 🔬This is a nightly-only experimental API. (extend_one)
> 
> Reserves capacity in a collection for the given number of additional elements. Read more

## `impl<K, V, const N: usize> From<[(K, V); N]> for ContextManager<K, V, RandomState>`

### `K: Hash + Eq`

---

> ```rust
> fn from(initial: [(K, V); N]) -> Self
> ```
> 
> Creates a new context manager with a first context initialized from the key-value pairs in initial.
> 
> Repeated keys will have all but one of the values dropped.

## `impl<K, V, S, const N: usize> From<[HashMap<K, V, S>; N]> for ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher`

---

> ```rust
> fn from(initial: [HashMap<K, V, S>; N]) -> Self
> ```
> 
> Creates a new context manager initialized with the contexts in initial.
> 
> Precedence proceeds from the first context toward the last.

## `impl<K, V, S> From<HashMap<K, V, S>> for ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher`

---

> ```rust
> fn from(initial: HashMap<K, V, S>) -> Self
> ```
> 
> Creates a new context manager with initial as the first context.

## `impl<K, V, S> FromIterator<(K, V)> for ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher + Default`

---

> ```rust
> fn from_iter<I: IntoIterator<Item = (K, V)>>(initial: I) -> Self
> ```
> 
> Creates a new context manager with a first context initialized from the key-value pairs in initial.
> 
> Repeated keys will have all but one of the values dropped.

## `impl<K, V, S> FromIterator<HashMap<K, V, S>> for ContextManager<K, V, S>`

### `K: Hash + Eq, S: BuildHasher`

---

> ```rust
> fn from_iter<I: IntoIterator<Item = HashMap<K, V, S>>>(iter: I) -> Self
> ```
> 
> Creates a new context manager initialized with the contexts in initial.
> 
> Precedence proceeds from the first context toward the last.

## `impl<K, Q, V, S> Index<&Q> for ContextManager<K, V, S>`

### `K: Hash + Eq + Borrow<Q>, Q: ?Sized + Hash + Eq, S: BuildHasher`

---

> ```rust
> fn index(&self, key: &Q) -> &V
> ```
> 
> Returns a reference to the value associated with key.
> 
> Panics if the context manager is empty, or key is not found in any contexts.
> 
> ```rust
> type Output = V
> ```
> 
> The returned type after indexing.

## `impl<K, V, S> PartialEq for ContextManager<K, V, S>`

### `K: Hash + Eq, V: PartialEq, S: BuildHasher`

> ```rust
> fn eq(&self, other: &ContextManager<K, V, S>) -> bool
> ```
> 
> Tests for self and other values to be equal, and is used by ==.

> ```rust
> const fn ne(&self, other: &Rhs) -> bool
> ```
> 
> Tests for !=. The default implementation is almost always sufficient, and should not be overridden without very good reason.

## `impl<K, V, S> Eq for ContextManager<K, V, S>`

### `K: Hash + Eq, V: Eq, S: BuildHasher`