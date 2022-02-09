### Day 2
## Longest Substring Without Repeating Characters
1. bruce force
two loop plus hashmap
2. only one loop, record the character position appeared last time, then calc the distance between two repeatable characters.
## Longest Palindromic Substring
We observe that a palindrome mirrors around its center. Therefore, a palindrome can be expanded from its center, and there are only 
2
n
−
1
2n−1 such centers.

You might be asking why there are 
2
n
−
1
2n−1 but not 
n
n centers? The reason is the center of a palindrome can be in between two letters. Such palindromes have even number of letters (such as "abba") and its center are between the two 'b's.
