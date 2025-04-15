# Counting-Sort-Algorithm

Counting Sort is a non-comparison-based sorting algorithm. It is particularly efficient when the range of input values is small compared to the number of elements to be sorted. The basic idea behind Counting Sort is to count the frequency of each distinct element in the input array and use that information to place the elements in their correct sorted positions.

- For example, for input [1, 4, 3, 2, 2, 1], the output should be [1, 1, 2, 2, 3, 4]. The important thing to notice is that the range of input elements is small and comparable to the size of the array.
- If the max element is of order more than n Log n where n is size of the array, then we can better sort the array using a standard comparison based sorting algorithm.

# Working of Counting Sort
## Step1 :

- Find out the maximum element from the given array.
<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230920182425/1.png" width="400">
</div>

## Step 2:

- Initialize a countArray[] of length max+1 with all elements as 0. This array will be used for storing the occurrences of the elements of the input array.

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230920182436/2.png" width="400">
</div>


## Step 3:

- In the countArray[], store the count of each unique element of the input array at their respective indices.
- For Example: The count of element 2 in the input array is 2. So, store 2 at index 2 in the countArray[]. Similarly, the count of element 5 in the input array is 1, hence store 1 at index 5 in the countArray[].
Maintain count of each element in countArray[].

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230922132754/3.png" width="400">
</div>

## Step 4:

- Store the cumulative sum or prefix sum of the elements of the countArray[] by doing countArray[i] = countArray[i – 1] + countArray[i]. This will help in placing the elements of the input array at the correct index in the output array.
Store the cumulative sum in countArray[].

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230920182646/4.png" width="400">
</div>


## Step 5:

- Iterate from end of the input array and because traversing input array from end preserves the order of equal elements, which eventually makes this sorting algorithm stable.

```
Update outputArray[ countArray[ inputArray[i] ] – 1] = inputArray[i]. 
Also, update countArray[ inputArray[i] ]  = countArray[ inputArray[i] ]– -.
```


# Counting Sort Algorithm:

- Declare an auxiliary array countArray[] of size max(inputArray[])+1 and initialize it with 0.
- Traverse array inputArray[] and map each element of inputArray[] as an index of countArray[] array, i.e., execute countArray[inputArray[i]]++ for 0 <= i < N.
- Calculate the prefix sum at every index of array inputArray[].
- Create an array outputArray[] of size N.
- Traverse array inputArray[] from end and update outputArray[ countArray[ inputArray[i] ] – 1] = inputArray[i]. Also, update countArray[ inputArray[i] ] = countArray[ inputArray[i] ]- – .
- Below is the implementation of the above algorithm:

# Code:

```
#include <bits/stdc++.h>
using namespace std;

vector<int> countSort(vector<int>& inputArray)
{

    int N = inputArray.size();

    // Finding the maximum element of array inputArray[].
    int M = 0;

    for (int i = 0; i < N; i++)
        M = max(M, inputArray[i]);

    // Initializing countArray[] with 0
    vector<int> countArray(M + 1, 0);

    // Mapping each element of inputArray[] as an index
    // of countArray[] array

    for (int i = 0; i < N; i++)
        countArray[inputArray[i]]++;

    // Calculating prefix sum at every index
    // of array countArray[]
    for (int i = 1; i <= M; i++)
        countArray[i] += countArray[i - 1];

    // Creating outputArray[] from countArray[] array
    vector<int> outputArray(N);

    for (int i = N - 1; i >= 0; i--)

    {
        outputArray[countArray[inputArray[i]] - 1]
            = inputArray[i];

        countArray[inputArray[i]]--;
    }

    return outputArray;
}

// Driver code
int main()

{

    // Input array
    vector<int> inputArray = { 4, 3, 12, 1, 5, 5, 3, 9 };

    // Output array
    vector<int> outputArray = countSort(inputArray);

    for (int i = 0; i < inputArray.size(); i++)
        cout << outputArray[i] << " ";

    return 0;
}
```

# Output:

```
1 3 3 4 5 5 9 12
```

# Complexity Analysis of Counting Sort:

- Time Complexity: O(N+M), where N and M are the size of inputArray[] and countArray[] respectively.
  - Worst-case: O(N+M).
  - Average-case: O(N+M).
  - Best-case: O(N+M).
- Auxiliary Space: O(N+M), where N and M are the space taken by outputArray[] and countArray[] respectively.






  
