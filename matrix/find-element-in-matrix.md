[Find Elements in Matrix]

* 解题思路为先把所有的行进行排序，然后取第一行的每一个数一次在剩下的行中做对比，找出同时出现在每一行的数，查找的过程使用了二分法
* 代码

        <public int FindElements(int[][] Matrix) {
             // write your code here
             if (Matrix == null || Matrix.length == 0) return -1;
             
             for (int i = 0; i < Matrix.length; i++) {
                 Arrays.sort(Matrix[i]);
             }
             
             for (int i = 0; i < Matrix[0].length; i++) {
                 int curr = Matrix[0][i];
                 boolean[] found = new boolean[Matrix.length - 1];
                 for (int j = 1; j < Matrix.length; j++) {
                     int left = 0;
                     int right = Matrix[j].length - 1;
                     while (left < right - 1) {
                         int mid = left + (right - left) / 2;
                         if (Matrix[j][mid] < curr) {
                             left = mid;
                         } else {
                             right = mid;
                         }
                     }
                     if (Matrix[j][left] == curr) {
                         found[j-1] = true;
                     }
                     if (Matrix[j][right] ==  curr) {
                         found[j-1] = true;
                     }
                 }
                 boolean res = true;
                 for (int n = 0; n < found.length; n++) {
                     if (!found[n]) {
                         res = false;
                         break;
                     }
                 }
                 if (res) return curr;
             }
             
             return -1;
         }>
         
* 九章的标准解法为用hashset存数，这样在查找的时候可以节约一些时间，但是有一些额外的空间消耗


        <public int FindElements(int[][] Matrix) {
             // write your code here
             int w = Matrix[0].length;
             int l = Matrix.length;
             ArrayList<Integer> list = new ArrayList<Integer>();
             for(int i = 0; i < w; i ++){
                 list.add(Matrix[0][i]);
             }
             for(int i = 1; i < l; i ++){
                 Set<Integer> set = new HashSet<Integer>();
                 for(int j = 0; j < w; j ++){
                     set.add(Matrix[i][j]);
                 }
                 for(int j = 0; j < list.size(); j ++){
                     if(!set.contains(list.get(j))){
                         list.remove(list.get(j));
                     }
                 }
             }
             int m = list.get(0);
             return m;
             
         }>