# Longest Palindromic Substring
## https://leetcode.com/problems/longest-palindromic-substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
```
Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Example 2:

Input: "cbbd"
Output: "bb"
```
# Implementation 1 : O(n^2)
```java
class Solution {
    int resultStart;
    int resultLength;

    public String longestPalindrome(String s) {
        int strLength = s.length();
        if (strLength < 2) {
            return s;
        }
        for (int start = 0; start < strLength - 1; start++) {
            expandRange(s, start, start);
            expandRange(s, start, start + 1);
        }
        return s.substring(resultStart, resultStart + resultLength);
    }

    private void expandRange(String str, int begin, int end) {
       while (begin >= 0 && end < str.length() && str.charAt(begin) == str.charAt(end)) {
            begin--;
            end++;
        }
       if (resultLength < end - begin - 1) {
            resultStart = begin + 1;
            resultLength = end - begin - 1;
        }
    }
}
```

## Implementation 2 : Dynamic Programming O(n^2)
```java
class Solution {
    public String longestPalindrome(String s) {
        int n = s.length();
        if (n == 0) 
            return "";

        boolean[][] dp = new boolean[n][n];
        int startIndex = 0, endIndex = 1;
        
        for (int i = 0; i < n; i++)
            dp[i][i] = true;
        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
            if(dp[i][i + 1]) {
               startIndex = i; endIndex = i + 2;
            }
        }
        for (int len = 3; len <= n; len++) {
            for (int i = 0, j = i + len - 1; j < n; i++, j++) {
                dp[i][j] = (s.charAt(i) == s.charAt(j)) && dp[i + 1][j - 1];
                if(dp[i][j]) {
                   startIndex = i; endIndex = j+1;
                } 
            }
        }
        return s.substring(startIndex,endIndex);
    }
}
```

# References :
1. https://www.youtube.com/watch?v=DK5OKKbF6GI
2. https://www.youtube.com/watch?v=y2BD4MJqV20
3. https://www.youtube.com/watch?v=XmSOWnL6T_I
