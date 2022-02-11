### Day 4
## Reverse Integer
1. using string. Convert integer to string and reverse the string.  
Reverse string: using slice in python. like ```s=y[::-1]```

2. Using java and just using % 10 and / 10. In the process, we need a checker to tell us whether the reverse number will be larger than 2^31. 
```java
class Solution {
    public int reverse(int x) {
        int sol = 0; 
        
        while (x != 0) {
            sol += x % 10;
            int checker = sol;
            
            x /= 10;
            
            if (x != 0) {
                sol *= 10;
                if (sol / 10 != checker) {
                    return 0;
                }
            }
        }
        
        return sol;
    }
}
```
## String to Integer (atoi)
1. using python, for s in string, using if to see whether we need it to add on the result. s.isdigit() is very useful and will speed up the code.
2. 
```java
public int myAtoi(String str) {
    int index = 0, sign = 1, total = 0;
    //1. Empty string
    if(str.length() == 0) return 0;

    //2. Remove Spaces
    while(str.charAt(index) == ' ' && index < str.length())
        index ++;

    //3. Handle signs
    if(str.charAt(index) == '+' || str.charAt(index) == '-'){
        sign = str.charAt(index) == '+' ? 1 : -1;
        index ++;
    }
    
    //4. Convert number and avoid overflow
    while(index < str.length()){
        int digit = str.charAt(index) - '0';
        if(digit < 0 || digit > 9) break;

        //check if total will be overflow after 10 times and add digit
        if(Integer.MAX_VALUE/10 < total || Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE %10 < digit)
            return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;

        total = 10 * total + digit;
        index ++;
    }
    return total * sign;
}
```
3.Deterministic Finite Automaton (DFA)  not familiar with.
https://leetcode.com/problems/string-to-integer-atoi/Figures/8/Slide10.JPG![image](https://user-images.githubusercontent.com/35773174/153543789-72edabbe-1b7f-4fe1-b62d-3be18387f5fa.png)
