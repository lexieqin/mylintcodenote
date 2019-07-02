[Top K Frequent Words]
- 思路：
    - priority queue，需要implement一个comparator，需要注意比较的时候有限比较出现的次数，如果次数一样要比较单词的字典顺序
    - 额外需要的辅助数据结构，作为queue里面储存的结构，需要包含单词本身和出现的次数
    - 最后在取出queue里面的元素的时候，需要倒着加入
- 代码

        class Pair {
            String word;
            int count;
            public Pair(String word, int count) {
                this.word = word;
                this.count = count;
            }
        }
        public List<String> topKFrequent(String[] words, int k) {
            List<String> res = new ArrayList<>();
            if (words == null || words.length == 0) return res;
            
            Map<String, Integer> map = new HashMap<>();
            for (String s: words) {
                map.put(s, map.getOrDefault(s, 0)+1);
            }
            
            Comparator<Pair> pairComparator = new Comparator<Pair>() {
                public int compare(Pair left, Pair right) {
                    if (left.count != right.count) {
                        return left.count - right.count;
                    }
                    return right.word.compareTo(left.word);
                }
            };
            PriorityQueue<Pair> topK = new PriorityQueue<Pair>(k, pairComparator);
            
            for (String s: map.keySet()) {
                if (topK.size() < k) {
                    topK.offer(new Pair(s, map.get(s)));
                } else {
                    Pair top = topK.peek();
                    if (top.count < map.get(s)) {
                        topK.poll();
                        topK.offer(new Pair(s, map.get(s)));
                    } else if (top.count == map.get(s)) {
                        if (top.word.compareTo(s) > 0) {
                            topK.poll();
                            topK.offer(new Pair(s, map.get(s)));
                        }
                    }
                }
            }
            
            // System.out.println(topK.size());
            
            while (!topK.isEmpty()) {
                Pair p = topK.poll();
                System.out.println(p.word);
                res.add(0, p.word);
            }
            return res;
        }