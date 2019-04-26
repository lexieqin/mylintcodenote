[Flip Game]

* 思路：用遍历的方式找到所有的“++”出现的位置，但是过程中要及时更新i的位置为前一个找到“++”的，然后再用substring替换一下就可以了
* 代码：

        <
        public List<String> generatePossibleNextMoves(String s) {
            // write your code here
            List<String> res = new ArrayList<>();
            if (s == null || s.length() <= 1) return res;
            
            for (int i = 0; i < s.length(); i++) {
                int index = s.indexOf("++", i);
                if (index == -1) {
                    break;
                }
                String sol = s.substring(0, index) + "--" + s.substring(index+2);
                res.add(sol);
                i = index;
            }
            
            return res;
        }
        >