[Coin Change]
- 思路：
    - 思路跟coin change 2差不多，不过可以用一维的数组来解决；
    - induction rule：1) coin种类少一个 2）如果当前钱比coin当前的面值大，可以回退到减去coin面值那个值+1
    
- 代码：

        public int coinChange(int[] coins, int amount) {
            if (coins == null || coins.length == 0) return 0;
            int[] dp = new int[amount+1];
            dp[0] = 0;
            
            for (int i = 1; i <= amount; i++) {
                dp[i] = amount + 1;
            }
            
            for (int i = 1; i <= amount; i++) {
                for (int j = 0; j < coins.length; j++) {
                    if (i >= coins[j]) {
                        dp[i] = Math.min(dp[i], dp[i-coins[j]]+1);
                    }
                }
            }
            
            return dp[amount]==amount+1?-1:dp[amount];
        }