+++ 
date = "2020-06-30"
title = "The Dutch National Flag Program"
tags = ["leetcode","array"]
+++

### 6.1 in EPI java, 5.1 in EPI python.
> Takes an array A and an index i into A, and rearranges the elements such that all elements less than A[i] (the "pivot") appear first, followed by elements equal to the pivot, followed by elements greater than the pivot.

> e.g.: A={0,1,2,0,2,1,1}, index=3, A[3]=0, so a valid partitioning is {0,0,1,2,2,1,1}.

The first round, we move number smaller than pivot to the left side, the second turn we do the bigger side.
```java
public static void dutchFlagPartition(int pivotIndex, List<Color> A) {
  // TODO - you fill in here.
  int pivotNum = A.get(pivotIndex).ordinal();
  int smallIndex = 0;
  for (int i = 0; i < A.size(); i++) {
    if (A.get(i).ordinal() < pivotNum) {
      Collections.swap(A, i, smallIndex++);
    }
  }
  int bigIndex = A.size()-1;
  for (int j=A.size()-1; j>-1 && A.get(j).ordinal()>=pivotNum; j-- ) {
    if (A.get(j).ordinal() > pivotNum) {
      Collections.swap(A, j, bigIndex--);
    }
  }
  return;
}```

The time complexity is O(n), the space complexity is O(1).

Another better solution is to do it in one round with two index.

```python
def dutch_flag_partition(pivot_index: int, A: List[int]) -> None:
    # A.sort()
    pivot_num = A[pivot_index]
    begin, end = 0, len(A)-1
    i = 0
    while i <= end:
        if A[i] < pivot_num:
            A[begin], A[i] = A[i], A[begin]
            begin += 1
            i += 1
        elif A[i] > pivot_num:
            A[end], A[i] = A[i], A[end]
            end -= 1
        elif A[i] == pivot_num:
            i += 1
    return
```

My mistake:
1. use another if condition to only determine when to i+=1, (equal+=1), but A[i] is already changed. Less and clean if, better
2. end = len(A)-1 or end = len(A) ? either above, notice __i<=end__, or
i< end rather than <=, in the if, at first -1, then swap
```
end = len(A)
while i < end:
	elif A[i] > pivot_num:
		end -= 1
		swap
```
Think in this way: the 'end' index at first is checked or not, not checked, then as the orignal code, it should be checked later. If it's checked(swapped), only i < end here.
