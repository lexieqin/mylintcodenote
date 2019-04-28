[Number of Islands]

* 思路：
    - customize class for coordinate
    - search through all location in grid
    - BFS - 用栈记录当前点，然后一层一层搜索且同时标记走过的grid为false
* 代码

        <
        class Coord {
            int x;
            int y;
            public Coord(int x, int y) {
                this.x = x;
                this.y = y;
            }
        }
        public int numIslands(boolean[][] grid) {
            // write your code here
            if (grid == null || grid.length == 0) return 0;
            
            int row = grid.length;
            int col = grid[0].length;
            int island = 0;
            
            for (int i = 0; i < row; i++) {
                for (int j = 0; j < col; j++) {
                    if (grid[i][j]) {
                        BFS(grid, i, j);
                        island++;
                    }
                }
            }
            return island;
        }
        
        private boolean isBound(boolean[][] grid, int x, int y) {
            return x >= 0 && x < grid.length && y >= 0 && y < grid[0].length; 
        }
        
        private void BFS(boolean[][] grid, int i, int j) {
            int[] X = new int[]{0, 0, -1, 1};
            int[] Y = new int[]{1, -1, 0, 0};
            
            Queue<Coord> queue = new LinkedList<>();
            queue.offer(new Coord(i, j));
            grid[i][j] = false;
            
            while (!queue.isEmpty()) {
                Coord curr = queue.poll();
                for (int n = 0; n < 4; n++) {
                    Coord coord = new Coord(curr.x + X[n], curr.y + Y[n]);
                    if (isBound(grid, coord.x, coord.y)) {
                        if (grid[coord.x][coord.y]) {
                            queue.offer(coord);
                            grid[coord.x][coord.y] = false;
                        }
                    }
                }
            }
        }
        >
