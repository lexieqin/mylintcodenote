[Shortest Word Distance]
- 思路
    - 初始化word1和word2的index为-1，然后遍历word list，遇到任意一个单词就更新index，如果两个index都不为-1，及证明找到了，比较之后更新结果
    
- 代码

        public int shortestDistance(String[] words, String word1, String word2) {
            if (words == null || words.length == 0) return 0;
            int p1 = -1, p2 = -1;
            int dis = words.length;
            for (int i = 0; i < words.length; i++) {
                String curr = words[i];
                if (curr.equals(word1)) {
                    p1 = i;
                } 
                
                if (curr.equals(word2)) {
                    p2 = i;
                }
                
                if (p1 != -1 && p2 != -1) {
                    dis = Math.min(dis, Math.abs(p1 - p2));
                }
            }
            return dis;
        }