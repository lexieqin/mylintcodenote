[Container With Most Water]
- 思路：two pointer，左边右边设置，计算搭起来的矩形的面积，移动的时候移动短的那个指针即可
- 代码：

        <
        public int maxArea(int[] height) {
            if (height == null || height.length == 0) {
                return 0;
            }
            
            int left = 0, right = height.length - 1;
            int max = 0;
            
            while (left < right) {
                int l = height[left];
                int r = height[right];
                max = Math.max(max, Math.min(l, r) * (right - left));
                if (l < r) {
                    left++;
                } else {
                    right--;
                }
            }
            
            return max;
        }
        >