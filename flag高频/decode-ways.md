[Decode Ways]
- 思路：一般的动归，需要判断的是
    - 1）当前的是否在[0,9]范围内，不是就是0是之前一个字母的decode
    - 2）继续判断当前字母跟前一个字母是否可以构成[10, 26]内的一个是的话还要加上两个字母前的decode ways
    
- 代码

        public int numDecodings(String s) {
            if (s == null || s.length() == 0) return 0;
            if (s.length() == 1 && s.charAt(0) == '0') return 0;
            int[] decode = new int[s.length()+1];
            decode[0] = 1;
            
            for (int i = 1; i <= s.length(); i++) {
                decode[i] = (s.charAt(i-1) == '0')?0:decode[i-1];
                if (i > 1 && (s.charAt(i - 2) == '1' || (s.charAt(i - 2) == '2' && s.charAt(i - 1) <= '6'))) {
                    decode[i] += decode[i-2];
                }
            }
            return decode[s.length()];
        }