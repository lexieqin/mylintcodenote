- 思路： 
    - 动态规划：二维动归数组
    - 状态转移方程：当前组合等于少一种硬币的组合数和新硬币加入之后的组合数，
    - dp[i][j] = dp[i-1][j] + (j >= coins[i-1]?dp[i][j - coins[i-1]]:0)
- 代码

        public int change(int amount, int[] coins) {
            // write your code here
            if (coins == null || coins.length == 0) return 0;
            
            int[][] dp = new int[coins.length+1][amount+1];
            
            dp[0][0] = 1;
            
            for (int i = 1; i < dp.length; i++) {
                dp[i][0] = 1;
            }
            
            for (int i = 1; i < dp[0].length; i++) {
                dp[0][i] = 0;
            }
            
            for (int i = 1; i <= coins.length; i++) {
                for (int j = 1; j <= amount; j++) {
                    dp[i][j] = dp[i-1][j] + (j >= coins[i-1]? dp[i][j - coins[i - 1]]:0);
                }
            }
            
            return dp[coins.length][amount];
            
        }