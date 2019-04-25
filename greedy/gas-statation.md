[Gas Station]

- 解题思路：贪心算法，设计到的数学概念为---如果一个非负的数列，一定能找到一个起点，使其前进过程的累加和不小于0. 记录每一步的累加和，如果当前小于零，即往前跳，重置start
- 代码：

public int canCompleteCircuit(int[] gas, int[] cost) {
    // write your code here
    if (gas == null || gas.length == 0) return 0;
    int curr = 0;
    int remain = 0;
    int start = 0;
    int len = gas.length;
    for (int i = 0; i < len; i++) {
        curr += gas[i];
        curr -= cost[i];
        remain += gas[i] - cost[i];
        if (curr < 0) {
            start = i + 1;
            curr = 0;
        }
    }
    if (remain >= 0) {
        return start;
    }        
    return -1;
}