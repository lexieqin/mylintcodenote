[Find the Celebrity]
- 思路：名人就是row全为0，column全为1
- 代码：

        public int findCelebrity(int n) {
            if (n == 0) return -1;
            for (int i = 0; i < n; i++) {
                boolean knowNone = false;
                for (int j = 0; j < n; j++) {
                    if (i == j) continue;
                    if (knows(i, j)) {
                        knowNone = true;
                        break;
                    }
                }
                if (!knowNone) {
                    boolean allKnow = true;
                    for (int m = 0; m < n; m++) {
                        if (m == i) continue;
                        if(!knows(m, i)) {
                            allKnow = false;
                            break;
                        }
                    }
                    if (allKnow) return i;
                }
            }
            return -1;
        }