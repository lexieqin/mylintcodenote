[Combination Sum]

* 思路：标准的递归题目，每次传入当前的target，由于数字可以重复使用，所以需要传一个index，在helper函数里面需要注意去重。最后数组需要先排序
* 代码

        <
        public List<List<Integer>> combinationSum(int[] candidates, int target) {
            // write your code here
            List<List<Integer>> res = new ArrayList<>();
            List<Integer> sol = new ArrayList<>();
            Arrays.sort(candidates);
            if (candidates == null || candidates.length == 0) return res;
            helper(res, sol, candidates, target, 0);
            return res;
        }
        
        private void helper(List<List<Integer>> res, List<Integer> sol, int[] candidates, int target, int index) {
            if (target < 0) return;
            if (target == 0) {
                res.add(new ArrayList<Integer>(sol));
                return;
            }
            for (int i = index; i < candidates.length; i++) {
                if (i != 0 && candidates[i] == candidates[i-1]) {
                    continue;
                }
                sol.add(candidates[i]);
                helper(res, sol, candidates, target - candidates[i], i);
                sol.remove(sol.size() - 1);
            }
            
        }
        >