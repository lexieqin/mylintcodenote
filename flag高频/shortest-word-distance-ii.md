[Shortest Word Distance II]
- 思路
    - 初始化的时候新建一个hashmap，记录所有单词出现的位置
    - 在查找的时候使用一个0（n^2)粗暴查找找到所有出现的dis中最小的
    
- 代码

        Map<String, List<Integer>> map;
        public WordDistance(String[] words) {
            map = new HashMap<>();
            for (int i = 0; i < words.length; i++) {
                if (!map.containsKey(words[i])) {
                    map.put(words[i], new ArrayList<Integer>());
                }
                map.get(words[i]).add(i);
            }
        }
        
        public int shortest(String word1, String word2) {
            List<Integer> lst1 = map.get(word1);
            List<Integer> lst2 = map.get(word2);
            int dis = Integer.MAX_VALUE;
            for (int i:lst1) {
                for (int j:lst2) {
                    int currDis = Math.abs(i-j);
                    dis = Math.min(currDis, dis);
                }
            }
            return dis;
        }