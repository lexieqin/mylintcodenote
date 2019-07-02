[Shortest Word Distance III]
- 思路
    - 利用两个list存单词的出现位置
    - 在查找的时候使用一个0（n^2)粗暴查找找到所有出现的dis中最小的，注意的是如果index相等，跳过
    
- 代码

        public int shortestWordDistance(String[] words, String word1, String word2) {
            if (words == null || words.length == 0) return 0;
            List<Integer> lst1 = new ArrayList<>();
            List<Integer> lst2 = new ArrayList<>();
            for (int i = 0; i < words.length; i++) {
                String curr = words[i];
                if (curr.equals(word1)) {
                    lst1.add(i);
                }
                if (curr.equals(word2)) {
                    lst2.add(i);
                }
            }
            
            int dis = words.length;
            for (int i: lst1) {
                for (int j: lst2) {
                    if (i == j) continue;
                    int curr = Math.abs(i-j);
                    dis = Math.min(curr, dis);
                }
            }
            return dis;
        }