[Reconstruct Itinerary]
- 思路：
    - 用一个hashmap去记录以某个站点为起点开始的和它能到的所有目的地，注意用pq来存储目的地以达到可以排序的目的
    - 最后用深度优先搜索的方式以“JFK”为起点遍历map里面所有以它为起点的终点站，不过要先dfs再加入最后一个目的地
    - 返回的时候要额外的revers一下order
- 代码：

        public List<String> findItinerary(List<List<String>> tickets) {
            List<String> res = new ArrayList<>();
            if (tickets == null || tickets.size() == 0) return res;
            String curr = "JFK";
            Map<String, PriorityQueue<String>> map = new HashMap<>();
            for (List<String> lst: tickets) {
                String start = lst.get(0);
                if (!map.containsKey(start)) {
                    map.put(start, new PriorityQueue<String>());
                }
                map.get(start).add(lst.get(1));
            }
            
            dfs(curr, res, map);
            Collections.reverse(res);
            return res;
        }
        private void dfs(String curr, List<String> res, Map<String, PriorityQueue<String>> map) {
            while (map.containsKey(curr) && !map.get(curr).isEmpty()) {
                dfs(map.get(curr).poll(), res, map);
            }
            res.add(curr);
        }