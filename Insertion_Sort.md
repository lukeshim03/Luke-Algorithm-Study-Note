## Problem

- Input: Sequence of n number

$$
n = a_1, a_2, a_3, ... a_n
$$

- Output:

$$
n = a_1', a_2', a_3', ... a_n'\\ where \ a_1<= a_2'<= a_3' <=... a_n'
$$

## Pseudo code

```cpp
for i = 2 to n
		key = A[i]
		// Put A[i] into sorted array A[1:i-1]
		j = i - 1
		while j > 0 and A[j] > key
				A[j + 1] = A[j]
				j = j - 1
		A[j + 1] = key
```

## C++

```cpp
void insertSort(vector<int>& arr) {
		for (int i = 1; i < arr.size(); i++) {
				int key = arr[i];
				int j = i - 1;
				while (j >= 0 && arr[j] > key) {
						arr[j + 1] = arr[j];
						j--;
				}
				arr[j + 1] = key;
		}
}
```

## C++ Short Cut

```cpp
void insertSort(vector<int>& a) {
	for (int i=1;i<a.size();i++){
		int key=a[i],j=i-1;
		while(j>=0&&a[j]>key) 
				a[j+1]=a[j--];
		a[j+1]=key;
	}
}
```

## Insertion Sort

### Loop Invariant

At the start of each iteration of the for loop (index i),  
the subarray `arr[0..i-1]` is already sorted and contains the same elements as the original array but in sorted order.

### Proof

**1. Initialization**

Before the first iteration (`i = 1`), the subarray `arr[0..0]` contains only one element.  
A single element is always sorted.  
Therefore, the invariant holds.

**2. Maintenance**

Assume that before iteration `i`, the subarray `arr[0..i-1]` is sorted.  
During the iteration, the algorithm inserts `arr[i]` into the correct position in the sorted subarray by shifting larger elements one position to the right.  
After insertion, the subarray `arr[0..i]` becomes sorted.  
Thus, the invariant is maintained.

**3. Termination**

When the loop terminates (`i = n`), the subarray `arr[0..n-1]` is sorted.  
Therefore, the entire array is sorted.

---

### Properties of Insertion Sort

**Stable**

Equal elements preserve their relative order after sorting.

**In-place**

The algorithm uses only a constant amount of extra memory.

Space Complexity: `O(1)`

**Adaptive**

If the array is already or nearly sorted, the algorithm runs faster.

Best-case Time Complexity: `O(n)`
