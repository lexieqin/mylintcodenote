[Next Greater Element I]
- 思路
    - 一般思路用两个循环就可以解决
    - 使用了哈希表和栈，但是这里的哈希表和上面的不一样，这里是建立每个数字和其右边第一个较大数之间的映射，没有的话就是-1。我们遍历原数组中的所有数字，如果此时栈不为空，且栈顶元素小于当前数字，说明当前数字就是栈顶元素的右边第一个较大数，那么建立二者的映射，并且去除当前栈顶元素，最后将当前遍历到的数字压入栈。当所有数字都建立了映射，那么最后我们可以直接通过哈希表快速的找到子集合中数字的右边较大值
- 代码

        public int[] nextGreaterElement(int[] nums1, int[] nums2) {
            if (nums1 == null || nums1.length == 0) return nums1;
            int[] result = new int[nums1.length];
            Stack<Integer> stack = new Stack<>();
            Map<Integer, Integer> map = new HashMap<>();
            for (int i = nums2.length - 1; i >= 0; i--) {
                int curr = nums2[i];
                while (!stack.isEmpty() && curr > stack.peek()) {
                    stack.pop();
                }
                if (stack.isEmpty()) {
                    map.put(curr, -1);
                } else {
                    map.put(curr, stack.peek());
                }
                stack.push(curr);
            }
            for (int i = 0; i < nums1.length; i++) {
                result[i] = map.get(nums1[i]);
            }
            return result;
        }