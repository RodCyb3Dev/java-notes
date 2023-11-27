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

2. Solve the "Best Time to Buy and Sell Stock" problem using a simple approach that keeps track of the minimum stock price and calculates the maximum profit.

```Java
class Solution {
  public int maxProfit(int[] prices) {
    if (prices == null || prices.length == 0) {
      return 0;
    }

    int minPrice = prices[0];
    int maxProfit = 0;

    for (int i = 1; i < prices.length; i++) {
      if (prices[i] < minPrice) {
        minPrice = prices[i];
      } else if (prices[i] - minPrice > maxProfit) {
        maxProfit = prices[i] - minPrice;
      }
    }

    return maxProfit;
  }
}
```

Test this solution with the following test cases:

```Java
public class Main {
  public static void main(String[] args) {
    Solution solution = new Solution();

    // Example 1
    int[] prices1 = {7, 1, 5, 3, 6, 4};
    System.out.println(solution.maxProfit(prices1));  // Output: 5

    // Example 2
    int[] prices3 = {7, 6, 4, 3, 1};
    System.out.println(solution.maxProfit(prices3));  // Output: 0
  }
}
```

3. Solve the "Best Time to Buy and Sell Stock II" problem using a simple approach that calculates the maximum profit by adding the difference between the consecutive elements of the array if the second element is larger than the first one.

```Java
class Solution {
  public int maxProfit(int[] prices) {
    if (prices == null || prices.length <= 1) {
      return 0;
    }

    int maxProfit = 0;

    for (int i = 1; i < prices.length; i++) {
      int profit = prices[i] - prices[i - 1];
      if (profit > 0) {
        maxProfit += profit;
      }
    }

    return maxProfit;
  }
}
```

Test this solution with the following test cases:

```Java
public class Main {
  public static void main(String[] args) {
    Solution solution = new Solution();

    // Example 1
    int[] prices1 = {7, 1, 5, 3, 6, 4};
    System.out.println(solution.maxProfit(prices1));  // Output: 7

    // Example 2
    int[] prices2 = {1, 2, 3, 4, 5};
    System.out.println(solution.maxProfit(prices2));  // Output: 4

    // Example 3
    int[] prices3 = {7, 6, 4, 3, 1};
    System.out.println(solution.maxProfit(prices3));  // Output: 0
  }
}
```

4. Solve the "Best Time to Buy and Sell Stock III" problem using the dynamic programming approach.
  
```Java
class Solution {
  public int maxProfit(int[] prices) {
    if (prices == null || prices.length == 0) {
      return 0;
    }

    int n = prices.length;
    int[] left = new int[n];
    int[] right = new int[n];

    int min = prices[0];

    for (int i = 1; i < n; i++) {
      left[i] = Math.max(left[i - 1], prices[i] - min);
      min = Math.min(min, prices[i]);
    }

    int max = prices[n - 1];

    for (int i = n - 2; i >= 0; i--) {
      right[i] = Math.max(right[i + 1], max - prices[i]);
      max = Math.max(max, prices[i]);
    }

    int maxProfit = 0;

    for (int i = 0; i < n; i++) {
      maxProfit = Math.max(maxProfit, left[i] + right[i]);
    }

    return maxProfit;
  }
}
```

Test this solution with the following test cases:

```Java
public class Main {
  public static void main(String[] args) {
    Solution solution = new Solution();

    // Example 1
    int[] prices1 = {3, 3, 5, 0, 0, 3, 1, 4};
    System.out.println(solution.maxProfit(prices1));  // Output: 6

    // Example 2
    int[] prices2 = {1, 2, 3, 4, 5};
    System.out.println(solution.maxProfit(prices2));  // Output: 4

    // Example 3
    int[] prices3 = {7, 6, 4, 3, 1};
    System.out.println(solution.maxProfit(prices3));  // Output: 0
  }
}
```

5. Solve the "Best Time to Buy and Sell Stock IV" problem using the dynamic programming approach.

```Java
class Solution {
  public int maxProfit(int k, int[] prices) {
    if (prices == null || prices.length == 0) {
      return 0;
    }

    int n = prices.length;

    if (k >= n / 2) {
      int maxProfit = 0;

      for (int i = 1; i < n; i++) {
        if (prices[i] > prices[i - 1]) {
          maxProfit += prices[i] - prices[i - 1];
        }
      }

      return maxProfit;
    }

    int[][] dp = new int[k + 1][n];

    for (int i = 1; i <= k; i++) {
      int maxDiff = -prices[0];

      for (int j = 1; j < n; j++) {
        dp[i][j] = Math.max(dp[i][j - 1], prices[j] + maxDiff);
        maxDiff = Math.max(maxDiff, dp[i - 1][j] - prices[j]);
      }
    }

    return dp[k][n - 1];
  }
}
```

Test this solution with the following test cases:

```Java
public class Main {
  public static void main(String[] args) {
    Solution solution = new Solution();

    // Example 1
    int k1 = 2;
    int[] prices1 = {2, 4, 1};
    System.out.println(solution.maxProfit(k1, prices1));  // Output: 2

    // Example 2
    int k2 = 2;
    int[] prices2 = {3, 2, 6, 5, 0, 3};
    System.out.println(solution.maxProfit(k2, prices2));  // Output: 7
  }
}
```
