[Subarray Sum Equals K]
- 思路：
    - 使用prefix sum，在累加的过程当中使用hashmap记录，每次计算prefix sum之后，只需要查找hashmap里面是否存在一个prefixsum-k的值，就可以确实那个subarray到当前位置的中间一段subarray中间那段的sum是k
    - 在计算的时候有几个prefix sum-k存在就加几个，再把当前得到的sum存到hashmap里面
    - 初始化的时候需要加入（0， 1）这一对pair
    
- 代码

        public int subarraySum(int[] nums, int k) {
            if (nums == null || nums.length == 0) return 0;
            
            Map<Integer, Integer> map = new HashMap<>();
            map.put(0, 1);
            int prefixSum = 0;
            int count = 0;
            for (int i = 0; i < nums.length; i++) {
                prefixSum += nums[i];
                if (map.containsKey(prefixSum - k)) {
                    count += map.get(prefixSum - k);
                } 
                map.put(prefixSum, map.getOrDefault(prefixSum, 0) + 1);
            }
            
            return count;
        }