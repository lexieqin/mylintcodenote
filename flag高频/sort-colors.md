- 思路： three pointers，遇到0和左边换，遇到2和右边换，需要注意的是如果左边的指针比中间大就要换一下位置
- 代码

        public void sortColors(int[] nums) {
            // write your code here
            if (nums == null || nums.length == 0) return;
            int l = 0, m = 0, r = nums.length - 1;
            while (m <= r) {
                if (nums[m] == 0) {
                    nums[m] = nums[l];
                    nums[l] = 0;
                    l++;
                    if (m < l) {
                        int temp = m;
                        m = l;
                        l = temp;
                    }
                } else if (nums[m] == 1) {
                    m++;
                } else {
                    nums[m] = nums[r];
                    nums[r] = 2;
                    r--;
                }
            }
        }