[Minimum Window Substring]
- 思路：
    - 扫描target string， 把出现的字母以及出现次数存在hashmap里面
    - 扫描source string， 如果碰到字母存在hashmap里面的，把相应的次数减一，如果剩下的次数大于零，count增加一
    - 如果count等于target的长度，开始判断当前长度，如果比minSize小，就更新res，并且开始开始移动滑窗的左边界，如果遇到target里面的字母，count减一
- 代码：

        public String minWindow(String source , String target) {
            // write your code here
            if (source == null || source.length() == 0) return source;
            if (target == null || target.length() == 0) return target;
            Map<Character, Integer> map = new HashMap<>();
            int minSize = Integer.MAX_VALUE;
            int left = 0;
            String res = "";
            for (int i = 0; i < target.length(); i++) {
                char curr = target.charAt(i);
                map.put(curr, map.getOrDefault(curr, 0) + 1);
            }
            int count = 0;
            for (int i = 0; i < source.length(); i++) {
                char curr = source.charAt(i);
                int occurance = map.getOrDefault(curr, 0) - 1;
                map.put(curr, occurance);
                if (occurance >= 0) {
                    count += 1;
                }
                while (count == target.length()) {
                    if (minSize > i - left + 1) {
                        minSize = i - left + 1;
                        res = source.substring(left, i+1);
                    }
                    int temp = map.getOrDefault(source.charAt(left), 0) + 1;
                    map.put(source.charAt(left), temp);
                    if (temp > 0) {
                        count -= 1;
                    }
                    left++;
                }
            }
            return res;
        }