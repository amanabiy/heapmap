# heapmap

A thread-safe heap that behaves like a dict but maintains heap ordering.

**Features:**

* Supports both **min-heap** and **max-heap** modes via a simple flag
* Dictionary-style access:

  * `h[key] = priority` (insert/update)
  * `prio = h[key]` (lookup)
  * `del h[key]` (remove)
* Bulk initialization: `HeapMap({'a':1, 'b':2})`
* Priority operations:

  * `h.popitem()` & `h.peekitem()` for root (min or max)
  * `h.update(key, new_prio)` to change an existing key’s priority
* Introspection:

  * `len(h)`, `key in h`, `h.is_empty()`
* Safe iteration:

  * `.keys()`, `.values()`, `.items()`, and plain `for k, v in h:`
  * Detects concurrent modifications and raises `RuntimeError`

---

## Installation

```bash
pip install heapmap
```

## Quickstart

```python
from heapmap import HeapMap

# Min-heap example
h = HeapMap({'a':5, 'b':2, 'c':3})
print(h.peekitem())  # ('b', 2)

# Insert
h['d'] = 1
print(h.popitem())   # ('d', 1)

# Update
h.update('a', 0)
print(h.peekitem())  # ('a', 0)

# Iterate
for key, prio in h.items():
    print(f"{key} -> {prio}")
```

## API Reference

```python
class HeapMap(MutableMapping):
    def __init__(self, initial=None, is_max_heap=False):
        """Initialize with optional dict and heap mode."""

    def __getitem__(self, key):
        """Get priority for key."""

    def __setitem__(self, key, priority):
        """Insert or update key with priority."""

    def __delitem__(self, key):
        """Remove key from heap."""

    def popitem(self):
        """Remove and return root (min or max) item."""

    def peekitem(self):
        """Return root item without removing it."""

    def update(self, key, new_priority):
        """Change priority and reheapify."""

    def clear(self):
        """Remove all items."""

    def is_empty(self):
        """Return True if heap is empty."""

    def keys(self):
        """Iterator over keys (safe to detect mods)."""

    def values(self):
        """Iterator over priorities."""

    def items(self):
        """Iterator over (key, priority) pairs."""

    def __len__(self):
        """Number of items in heap."""

    def __contains__(self, key):
        """Membership test."""
```

## Testing

```bash
pip install -e .[test]  # installs pytest
pytest
```

## Contributing

1. Fork the repo
2. Create a topic branch
3. Submit a PR

## License

MIT © Your Name
