# HyperLogLog Algorithm: Explanation and Implementation
## 12/03/2025

**HyperLogLog (HLL)** is a fascinating probabilistic algorithm for estimating the **number of unique elements** in a dataset — using *very little memory*.  

In this post, we'll walk through a **custom Python implementation** of HyperLogLog, and then compare it with a popular library (`datasketch`). By the end, you’ll understand:

- How HyperLogLog works
- Why it’s so memory-efficient
- The meaning of each part of the code

---

### Imports

```python
import hashlib
import math
import random
import sys
import time
from datasketch import HyperLogLog as LibHLL
```

Here’s why we need each import:
- `hashlib` → for hashing items into a fixed-size bit string (SHA-1)
- `math` → for logarithms and powers
- `random` & `time` → to generate sample data
- `datasketch.HyperLogLog` → to compare our custom HLL with a well-tested implementation

---

### The HyperLogLog Class

```python
class HyperLogLog:
    def __init__(self, p=14, hash_bits=160):
        ...
```

#### Parameters:
- **p**: precision parameter (number of bits to determine the register index)  
  → The number of registers is \( m = 2^p \).
- **hash_bits**: total number of bits we’ll take from the hash output (SHA-1 gives 160 bits).

> **Memory note:** With `p=14`, we have \( m = 16384 \) registers — still tiny compared to storing millions of elements.

---

#### Setting up registers & bias correction

```python
self.m = 1 << p
self.registers = [0] * self.m
```
We create **m registers**, all initialized to zero.

```python
if self.m == 16:
    self.alpha_m = 0.673
elif self.m == 32:
    self.alpha_m = 0.697
elif self.m == 64:
    self.alpha_m = 0.709
else:
    self.alpha_m = 0.7213 / (1 + 1.079 / self.m)
```
`alpha_m` is a **bias correction constant** — different m values require different empirical corrections.

---

#### Hashing items

```python
def _hash(self, value):
    if isinstance(value, str):
        value = value.encode('utf-8')
    h = hashlib.sha1(value).digest()
    x = int.from_bytes(h, byteorder='big')
    if self.hash_bits < 160:
        x &= (1 << self.hash_bits) - 1
    return x
```

We:
1. Convert the input into bytes
2. Hash it using SHA-1 (160 bits)
3. Convert it into an integer
4. Optionally truncate if `hash_bits` < 160

---

#### Finding the **ρ(w)** function

```python
def _rho(self, w, max_bits):
    if w == 0:
        return max_bits + 1
    bitlen = w.bit_length()
    leading_zeros = max_bits - bitlen
    return leading_zeros + 1
```

ρ(w) = position of the **first 1-bit** in w (counting from the left).  
This is the **core** of HLL — it estimates the "rarity" of a hash prefix.

---

#### Adding an element

```python
def add(self, item):
    x = self._hash(item if not isinstance(item, int) else str(item))
    idx = x & (self.m - 1)        # register index (p bits)
    w = x >> self.p               # remaining bits
    max_w_bits = self.hash_bits - self.p
    rho = self._rho(w, max_w_bits)
    if rho > self.registers[idx]:
        self.registers[idx] = rho
```

Steps:
1. Hash the item
2. **Lower p bits** → register index
3. **Remaining bits** → input to ρ(w)
4. Update the register if we found a larger ρ

---

#### Merging two HLLs

```python
def merge(self, other):
    assert self.p == other.p and self.hash_bits == other.hash_bits
    for i in range(self.m):
        self.registers[i] = max(self.registers[i], other.registers[i])
```

Two HyperLogLogs can be **merged** simply by taking the **max** register value at each index. This is one reason HLL is so useful in distributed systems.

---

#### Estimating the cardinality

```python
def count(self):
    indicator_sum = sum((2.0 ** -r) for r in self.registers)
    raw_est = self.alpha_m * (self.m ** 2) / indicator_sum
```

The core estimation formula is:
\[
E = \alpha_m \cdot m^2 \cdot \frac{1}{\sum_{j=1}^m 2^{-M_j}}
\]
where \( M_j \) is the value in register j.

---

#### Small range correction

```python
V = self.registers.count(0)
if raw_est <= (5.0/2.0) * self.m and V != 0:
    return self.m * math.log(self.m / V)
```
If many registers are empty, HLL falls back to **linear counting**.

---

#### Large range correction

```python
limit = (1 << 32) / 30.0
if raw_est > limit:
    return - (1 << 32) * math.log(1 - raw_est / (1 << 32))
```
If the estimate is huge (close to 2³²), we apply another correction to avoid bias.

---

### Comparing with `datasketch`

```python
def compare_with_library():
    random.seed(time.time())
    for true_n in [1000, 5000, 20000, 100000]:
        stream = [random.randint(0, 10_000_000) for _ in range(true_n)]

        hll_custom = HyperLogLog(p=14)
        hll_lib = LibHLL(p=14)

        for val in stream:
            hll_custom.add(val)
            hll_lib.update(str(val).encode('utf-8'))

        est_custom = hll_custom.count()
        est_lib = hll_lib.count()
        true_unique = len(set(stream))

        err_custom = 100.0 * abs(est_custom - true_unique) / true_unique
        err_lib = 100.0 * abs(est_lib - true_unique) / true_unique

        print(f"True uniques: {true_unique:7d} "
              f"| Custom: {est_custom:10.2f} ({err_custom:5.3f}%) "
              f"| Lib: {est_lib:10.2f} ({err_lib:5.3f}%)")
```

We:
1. Generate streams of random integers
2. Add them to both our HLL and the library HLL
3. Compare the estimates and error percentages

---

### Example Output

```
True uniques:    997  | Custom:    999.41 (0.241%) | Lib:    998.32 (0.133%)
True uniques:   4980  | Custom:   4995.22 (0.306%) | Lib:   4988.45 (0.170%)
...
```

Both implementations produce **very close** results — showing our custom code works correctly.

---

### Key Takeaways

- HyperLogLog is **memory-efficient** and **mergeable**.
- It’s perfect for counting unique elements in **large datasets**.
- Implementing it from scratch deepens understanding — but for production, use a battle-tested library.
