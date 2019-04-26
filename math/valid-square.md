[Valid Square]

* 思路：非常迷和神奇的思路，如果是一个合法正方形，计算出四个点所能产生的所有距离的值，只能有两种，用hashset存就行了
* 代码


        <
        public boolean validSquare(int[] p1, int[] p2, int[] p3, int[] p4) {
            // Write your code here
            if (p1 == null || p1.length != 2 || p2 == null || p2.length != 2 
            || p3 == null || p3.length != 2 || p4 == null || p4.length != 2) {
                return false;
            }
            
            Set<Integer> dis = new HashSet<>();
            dis.add(getDistance(p1, p2));
            dis.add(getDistance(p1, p3));
            dis.add(getDistance(p1, p4));
            dis.add(getDistance(p2, p3));
            dis.add(getDistance(p2, p4));
            dis.add(getDistance(p3, p4));
            
            return dis.size() == 2;
            
        }
        
        private int getDistance(int[] p1, int[] p2) {
            return (p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]);
        }
        >