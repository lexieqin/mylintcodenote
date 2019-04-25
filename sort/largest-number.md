[Largest Number]

* 思路：把两个数拼在一起，然后再把这两个数换个顺序再拼在一起，这时候就可以直接比较了。实现一个comparator
* 代码

        <
        class NumbersComparator implements Comparator<String> {
            @Override
            public int compare(String s1, String s2) {
                return (s2 + s1).compareTo(s1 + s2);
            }
        }
        public String largestNumber(int[] nums) {
            String[] strs = new String[nums.length];
             for (int i = 0; i < nums.length; i++) {
                 strs[i] = Integer.toString(nums[i]);
             }
             Arrays.sort(strs, new NumbersComparator());
             StringBuilder sb = new StringBuilder();
             boolean isAllZeros = true;
             for (int i = 0; i < nums.length; i++) {
                 if (nums[i] != 0) {
                     isAllZeros = false;
                 }
             }
             for (int i = 0; i < strs.length; i++) {
                 sb.append(strs[i]);
             }
             return isAllZeros?"0":sb.toString();
        }
        >
