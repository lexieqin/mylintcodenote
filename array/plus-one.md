[Plus One]
* 思路：找出原始数据，然后做加法，最后还愿成数组
* 代码

        <
        public int[] plusOne(int[] digits) {
            // write your code here
            if (digits == null || digits.length == 0) return digits;
            
            long sum = 0;
            for (int i = digits.length - 1; i >= 0; i--) {
                sum += digits[digits.length - i - 1] * Math.pow(10, i);
            }
            
            sum += 1;
            int count = 1;
            while (true) {
                if ((int)(sum / Math.pow(10, count)) > 0) {
                    count++;
                } else {
                    break;
                } 
            }
            int[] res = new int[count];
            for (int i = count - 1; i >= 0; i--) {
                res[count - i - 1] = (int)(sum / Math.pow(10, i));
                sum %= Math.pow(10, i);
            }
            
            return res;
        }
        >