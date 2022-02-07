### Day 1
## Two sum
1. Bruce force: 
Time Complexity: O(n^2)
Space Complexity: O(1)

2. Using Hashmap
For a given input array this algorithm does the following steps:
  Create a hashmap which accepts integer datatype as key and value.
  Iterate through each element in the given array starting from the first element.
  In each iteration check if required number (required  number = target sum - current number) is present in the given array.
  If present, return {required number index, current number index} as  result.
  Otherwise add the current iteration number as key and its index as value to the hashmap. Repeat this  until you find the result.
Python could use a dict, and use "if xxx in xxx" to justify whether 'target - i' is in the dict.
Java could use 'HashMap<Integer,Integer> indexMap = new HashMap<Integer,Integer>();' indexMap.put(numbers[i], i);

Time Complexity: O(n)
Space Complexity: O(n)
 
