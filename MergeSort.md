## Merge Sort

### Idea

Divide the array into two halves, recursively sort each half, and then merge the sorted halves.

---

### Loop Invariant (Merge Step)

During the merge process, at any step, the merged array contains the smallest elements from both subarrays in sorted order.

---

### Proof

**1. Initialization**

Before merging begins, both subarrays are already sorted (by recursion).

**2. Maintenance**

At each step, the algorithm compares the smallest remaining elements of the two subarrays and places the smaller one into the merged array.

Thus, the merged portion remains sorted.

**3. Termination**

When all elements from both subarrays are merged, the resulting array is fully sorted.

---

### Properties of Merge Sort

**Stable**

Equal elements preserve their relative order after sorting.

**Not In-place**

Requires additional memory for merging.

Space Complexity: `O(n)`

**Not Adaptive**

Time complexity does not improve even if the array is already sorted.

---

### Complexity

Time Complexity:

- Best: `O(n log n)`
- Average: `O(n log n)`
- Worst: `O(n log n)`

Space Complexity:

- `O(n)`

---

### Implementation (C++)

```cpp
void merge(vector<int>& a, int l, int m, int r) {
    vector<int> temp;
    int i = l, j = m + 1;

    while (i <= m && j <= r) {
        if (a[i] <= a[j]) temp.push_back(a[i++]);
        else temp.push_back(a[j++]);
    }

    while (i <= m) temp.push_back(a[i++]);
    while (j <= r) temp.push_back(a[j++]);

    for (int k = 0; k < temp.size(); k++)
        a[l + k] = temp[k];
}

void mergeSort(vector<int>& a, int l, int r) {
    if (l >= r) return;

    int m = (l + r) / 2;
    mergeSort(a, l, m);
    mergeSort(a, m + 1, r);
    merge(a, l, m, r);
}
```

## Why Merge Sort is $O(n \log n)$

### Recurrence Relation

Merge Sort divides the array into two halves and merges them.

$T(n) = 2T\left(\frac{n}{2}\right) + O(n)$

- $2T(n/2)$: recursively sorting two halves
- $O(n)$: merging two sorted arrays

---

### Recursion Tree Intuition

At each level of recursion:

- Total work = $O(n)$

Number of levels:

$\log_2 n$

---

### Total Work

$\text{Total} = O(n) \times \log n = O(n \log n)$

---

### Step-by-step Intuition

Level 0:
$n$

Level 1:
$\frac{n}{2} + \frac{n}{2} = n$

Level 2:
$\frac{n}{4} + \frac{n}{4} + \frac{n}{4} + \frac{n}{4} = n$

...

Each level does $n$ work, and there are $\log n$ levels.

$$
2^k = n
$$

---

### Final Result
$T(n) = O(n \log n)$

## Solve Recurrence: $T(n) = 2T\left(\frac{n}{2}\right) + O(n)$

### Method 1: Master Theorem

Compare with standard form:

$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$

Here:

- a = 2
- b = 2
- f(n) = O(n)

---

Compute:

$$n^{\log_b a} = n^{\log_2 2} = n^1 = n$$

---

Compare f(n) with 
$$n^{\log_b a}$$
:

$$f(n) = \Theta(n)$$

So this is **Case 2** of Master Theorem:

$$T(n) = \Theta(n \log n)$$

---

### Final Answer

$$T(n) = O(n \log n)$$
