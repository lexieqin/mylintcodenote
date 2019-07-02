[Longest Palindromic Subsequence]

- 思路： 动态规划，induction rule关键是判断两端字母是否相等，如果相等就可以把问题变成xxx+2或者max(xx1, xx2)
- 代码

        public int longestPalindromeSubseq(String s) {
            // write your code here
            if (s == null || s.length() == 0) return 0;
            
            int len = s.length();
            int[] dp = new int[len];
            
            for (int i = len - 1; i >= 0; i--) {
                dp[i] = 1;
                int leftBottom = 0;
                for (int j = i + 1; j < len; j++) {
                    int max = 0;
                    if (s.charAt(i) == s.charAt(j)) {
                        max = 2 + leftBottom;
                    } else {
                        max = Math.max(dp[j], dp[j-1]);
                    }
                    
                    leftBottom = dp[j];
                    dp[j] = max;
                }
            }
            return dp[len - 1];
        }