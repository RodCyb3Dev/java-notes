# Java Notes Solving Problems

1. Solve the Longest Palindromic Substring problem using the dynamic programming approach.

```Java
class Solution {
  public String longestPalindrome(String s) {
    if (s == null || s.length() < 1) {
      return "";
    }

    int start = 0, end = 0;

    for (int i = 0; i < s.length(); i++) {
      int len1 = expandAroundCenter(s, i, i);
      int len2 = expandAroundCenter(s, i, i + 1);
      int len = Math.max(len1, len2);

      if (len > end - start) {
        start = i - (len - 1) / 2;
        end = i + len / 2;
      }
    }

    return s.substring(start, end + 1);
  }

  private int expandAroundCenter(String s, int left, int right) {
      while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
      }

      return right - left - 1;
  }
}

// Test this solution:
public class Main {
  public static void main(String[] args) {
    Solution solution = new Solution();

    // Example 1
    String s1 = "babad";
    System.out.println(solution.longestPalindrome(s1));  // Output: "bab" or "aba"

    // Example 2
    String s2 = "cbbd";
    System.out.println(solution.longestPalindrome(s2));  // Output: "bb"
  }
}
```
