### Day 2
## Longest Substring Without Repeating Characters
1. bruce force
two loop plus hashmap
2. only one loop, record the character position appeared last time, then calc the distance between two repeatable characters.
## Longest Palindromic Substring\
1. bruce force (time excess)
2. Reverse S. To rectify this, each time we find a longest common substring candidate, we check if the substring’s indices are the same as the reversed substring’s original indices. If it is, then we attempt to update the longest palindrome found so far; if not, we skip this and find the next candidate.
3. We observe that a palindrome mirrors around its center. Therefore, a palindrome can be expanded from its center, and there are only 2n−1 such centers.
The reason is the center of a palindrome can be in between two letters. Such palindromes have even number of letters (such as "abba") and its center are between the two 'b's.  
```java
class Solution {
    private int max = 0;
    private int init = 0;
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len < 2) {
            return s;
        }
        for (int i = 0; i < len - 1; i++) {
            exPal(s, i, i);
            exPal(s, i, i + 1);
        }
        return s.substring(init, max + init);


    }
    public void exPal(String s, int i, int j) {
        int len = s.length();
        while (i >= 0 && j <= len - 1 && s.charAt(i) == s.charAt(j)) {
            i -= 1;
            j += 1;
        }
        if (max < j - i - 1) {
            max = j - i - 1;
            init = i + 1;
        }
    }
}
```

4. Dynamic Programming

