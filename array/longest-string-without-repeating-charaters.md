[Longest Substring Without Repeating Characters]
- 思路：著名的sliding window问题。基本思想就是移动的时候逐渐增加长度，并且用hashmap记录每一个字母的最后出现的index，如果新出现的字母出现在hashmap里面，更新左边的index为重复字母的下一位即可
- 代码：

        <
        public int lengthOfLongestSubstring(String s) {
            if (s == null || s.length() == 0) return 0;
            Map<Character, Integer> map = new HashMap<>();
            int left = 0, max = 0;
            for (int i = 0; i < s.length(); i++) {
                char curr = s.charAt(i);
                if (map.containsKey(curr) && map.get(curr) >= left) {
                    left = map.get(curr) + 1;
                }
                map.put(curr, i);
                max = Math.max(i - left + 1, max);
            }
            return max;
        }
        >