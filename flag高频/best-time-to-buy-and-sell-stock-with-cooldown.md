[Best Time to Buy and Sell Stock with Cooldown]

- 思路
    - 三个辅助的数组分别为buy[], sell[], cooldown[]， 分别表示第i次操作为买卖或者冷却时候的最大收益
    - 如果当前的操作为买，那当前的最大值取上一次买或者上一次冷却然后当前天买的最大值：buy[i]  = max(rest[i-1] - price, buy[i-1])；  
    - 如果当前的操作为卖，那前一天必为买： sell[i] = buy[i-1] + price
    - 如果当前操作为冷却，那取前一天为冷却或者卖出的最大值：rest[i] = max(sell[i-1], rest[i-1])
    
- 代码

        public int maxProfit(int[] prices) {
            if (prices == null || prices.length <= 1) return 0;
            
            int len = prices.length;
            int[] buy = new int[len+1];
            int[] sell = new int[len+1];
            int[] cooldown = new int[len+1];
            
            buy[0] = Integer.MIN_VALUE;
            sell[0] = 0;
            cooldown[0] = 0;
            
            for (int i = 1; i <= len; i++) {
                buy[i] = Math.max(buy[i-1], cooldown[i-1]-prices[i-1]);
                sell[i] = buy[i-1] + prices[i-1];
                cooldown[i] = Math.max(cooldown[i-1], sell[i-1]);
            }
            return Math.max(sell[len], cooldown[len]);
        }
        
        
        or O(1) 空间复杂度
        public int maxProfit(int[] prices) {
            if (prices == null || prices.length <= 1) return 0;
            int len = prices.length;
            int buy = Integer.MIN_VALUE;
            int sell = 0;
            int cooldown = 0;
            int res = Integer.MIN_VALUE;
            for (int i = 1; i <= len; i++) {
                int tempBuy = buy;
                buy = Math.max(buy, cooldown-prices[i-1]);
                cooldown = Math.max(cooldown, sell);
                sell = tempBuy + prices[i-1];
                res = Math.max(Math.max(sell, cooldown), res);
            }
            return res;
        }
        
        