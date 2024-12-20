## Array Data Structure and Algorithms for Interviews

### Part 1: Documentation

#### Overview of Arrays

- **Definition**: An array is a linear data structure that stores elements of the same data type in contiguous memory locations.
- **Key Features**:
  - Fixed size: The size of an array is defined at the time of declaration and cannot be changed.
  - Random access: Elements can be accessed directly using their index.
  - Homogeneous data: Arrays store elements of the same data type.
- **Complexity**:
  - Access: O(1)
  - Search: O(n) for unsorted arrays, O(log n) for sorted arrays (binary search)
  - Insert/Delete: O(n) (due to shifting of elements)

#### Common Algorithms and Problems on Arrays

##### 1. **Traversal**

- Iterating through the array to access or modify each element.
- **Time Complexity**: O(n)
- **Example in C#**:
  ```csharp
  int[] numbers = { 1, 2, 3, 4, 5 };
  foreach (int number in numbers)
  {
      Console.WriteLine(number);
  }
  ```

##### 2. **Searching**

- **Linear Search**: Sequentially check each element.
  - Complexity: O(n)
  - **Example in C#**:
    ```csharp
    int[] numbers = { 10, 20, 30, 40 };
    int targetValue = 30;
    for (int index = 0; index < numbers.Length; index++)
    {
        if (numbers[index] == targetValue)
        {
            Console.WriteLine("Element found at index " + index);
            break;
        }
    }
    ```
- **Binary Search**: Efficient search on sorted arrays by repeatedly dividing the search interval in half.
  - Complexity: O(log n)
  - **Example in C#**:
    ```csharp
    int[] sortedNumbers = { 10, 20, 30, 40, 50 };
    int targetValue = 30;
    int leftIndex = 0, rightIndex = sortedNumbers.Length - 1;
    while (leftIndex <= rightIndex)
    {
        int middleIndex = leftIndex + (rightIndex - leftIndex) / 2;
        if (sortedNumbers[middleIndex] == targetValue)
        {
            Console.WriteLine("Element found at index " + middleIndex);
            break;
        }
        else if (sortedNumbers[middleIndex] < targetValue)
            leftIndex = middleIndex + 1;
        else
            rightIndex = middleIndex - 1;
    }
    ```

##### 3. **Sorting**

- Common algorithms:
  - **Bubble Sort**: Repeatedly swap adjacent elements if they are in the wrong order.
    - Complexity: O(n²)
    - **Example in C#**:
      ```csharp
      int[] unsortedNumbers = { 64, 34, 25, 12, 22, 11, 90 };
      for (int i = 0; i < unsortedNumbers.Length - 1; i++)
      {
          for (int j = 0; j < unsortedNumbers.Length - i - 1; j++)
          {
              if (unsortedNumbers[j] > unsortedNumbers[j + 1])
              {
                  int temp = unsortedNumbers[j];
                  unsortedNumbers[j] = unsortedNumbers[j + 1];
                  unsortedNumbers[j + 1] = temp;
              }
          }
      }
      Console.WriteLine(string.Join(", ", unsortedNumbers));
      ```

##### 4. **Two-Pointer Technique**

- Useful for problems like finding pairs with a given sum, reversing an array, or merging two sorted arrays.
- **Example Problem**: Given a sorted array, find two numbers that add up to a target.
  - Complexity: O(n)
  - **Example in C#**:
    ```csharp
    int[] sortedNumbers = { 1, 2, 3, 4, 6 };
    int targetSum = 6;
    int leftPointer = 0, rightPointer = sortedNumbers.Length - 1;
    while (leftPointer < rightPointer)
    {
        int currentSum = sortedNumbers[leftPointer] + sortedNumbers[rightPointer];
        if (currentSum == targetSum)
        {
            Console.WriteLine("Pair found: " + sortedNumbers[leftPointer] + ", " + sortedNumbers[rightPointer]);
            break;
        }
        else if (currentSum < targetSum)
            leftPointer++;
        else
            rightPointer--;
    }
    ```

##### 5. **Sliding Window Technique**

- Efficient for finding subarrays with specific properties (e.g., maximum sum, minimum length).
- **Example Problem**: Find the maximum sum of a subarray of size k.
  - Complexity: O(n)
  - **Example in C#**:
    ```csharp
    int[] numbers = { 2, 1, 5, 1, 3, 2 };
    int subarraySize = 3, maximumSum = 0, currentWindowSum = 0;
    for (int index = 0; index < numbers.Length; index++)
    {
        currentWindowSum += numbers[index];
        if (index >= subarraySize - 1)
        {
            maximumSum = Math.Max(maximumSum, currentWindowSum);
            currentWindowSum -= numbers[index - (subarraySize - 1)];
        }
    }
    Console.WriteLine("Maximum sum: " + maximumSum);
    ```

##### 6. **Kadane’s Algorithm**

- Finds the maximum sum of a contiguous subarray.
- Complexity: O(n)
- **Example in C#**:
  ```csharp
  int[] numbers = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };
  int currentMaximum = numbers[0], globalMaximum = numbers[0];
  for (int index = 1; index < numbers.Length; index++)
  {
      currentMaximum = Math.Max(numbers[index], currentMaximum + numbers[index]);
      if (currentMaximum > globalMaximum)
          globalMaximum = currentMaximum;
  }
  Console.WriteLine("Maximum sum: " + globalMaximum);
  ```

##### 7. **Prefix Sum**

- Precomputes cumulative sums to efficiently answer range queries.
- **Example Problem**: Given an array, find the sum of elements between two indices.

  - Complexity: O(1) for queries after O(n) preprocessing.
  - **Example in C#**:

    ```csharp
    int[] numbers = { 10, 20, 30, 40, 50 };
    int[] prefixSumArray = new int[numbers.Length];
    prefixSumArray[0] = numbers[0];
    for (int index = 1; index < numbers.Length; index++)
        prefixSumArray[index] = prefixSumArray[index - 1] + numbers[index];

    int startIndex = 1, endIndex = 3; // Example query indices
    int rangeSum = prefixSumArray[endIndex] - (startIndex > 0 ? prefixSumArray[startIndex - 1] : 0);
    Console.WriteLine("Sum between indices " + startIndex + " and " + endIndex + ": " + rangeSum);
    ```

##### 8. **Matrix Problems (2D Arrays)**

- Traversal, searching, or performing operations on rows and columns.
- **Example Problem**: Rotate a matrix 90 degrees clockwise.
  - Complexity: O(n²)
  - **Example in C#**:
    ```csharp
    int[,] matrix = {
        { 1, 2, 3 },
        { 4, 5, 6 },
        { 7, 8, 9 }
    };
    int size = matrix.GetLength(0);
    for (int row = 0; row < size; row++)
    {
        for (int col = row; col < size; col++)
        {
            int temp = matrix[row, col];
            matrix[row, col] = matrix[col, row];
            matrix[col, row] = temp;
        }
    }
    for (int row = 0; row < size; row++)
    {
        for (int col = 0, reverseCol = size - 1; col < reverseCol; col++, reverseCol--)
        {
            int temp = matrix[row, col];
            matrix[row, col] = matrix[row, reverseCol];
            matrix[row, reverseCol] = temp;
        }
    }
    for (int row = 0; row < size; row++)
    {
        for (int col = 0; col < size; col++)
        {
            Console.Write(matrix[row, col] + " ");
        }
        Console.WriteLine();
    }
    ```

### Part 2: Practice Problems

#### Basic Problems

1. **Array Traversal**:

   - Write a function to print all elements of an array.

2. **Find the Maximum and Minimum**:

   - Given an array, find the maximum and minimum elements.

3. **Reverse an Array**:

   - Reverse the elements of an array in place.

4. **Move Zeroes to End**:
   - Rearrange the array so all zeroes are at the end while maintaining the order of non-zero elements.

#### Intermediate Problems

5. **Two Sum**:

   - Given a sorted array and a target, find two numbers that add up to the target.

6. **Rotate an Array**:

   - Rotate an array to the right by k steps.

7. **Subarray Sum Equals K**:

   - Find the number of subarrays whose sum equals k.

8. **Merge Sorted Arrays**:
   - Merge two sorted arrays into one sorted array.

#### Advanced Problems

9. **Maximum Subarray Sum (Kadane’s Algorithm)**:

   - Find the contiguous subarray with the largest sum.

10. **Trapping Rain Water**:

    - Calculate the amount of rainwater trapped between the bars.

11. **Longest Increasing Subsequence**:

    - Find the longest increasing subsequence in an array.

12. **Find the Duplicate Number**:
    - Given an array of n+1 integers where each integer is between 1 and n, find the duplicate.

#### Matrix Problems

13. **Search in a 2D Matrix**:

    - Search for a value in a matrix where rows and columns are sorted.

14. **Rotate a Matrix**:

    - Rotate a 2D array 90 degrees clockwise.

15. **Spiral Order Traversal**:
    - Traverse a 2D array in a spiral order.

#### Tips for Interviews

- Always clarify the problem requirements and constraints with the interviewer.
- Start with a brute force solution and then optimize it.
- Be prepared to explain your thought process and trade-offs.
- Write clean and readable code with proper variable names and comments.
