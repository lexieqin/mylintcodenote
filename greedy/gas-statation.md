[Gas Station]

- 解题思路：贪心算法，设计到的数学概念为---如果一个非负的数列，一定能找到一个起点，使其前进过程的累加和不小于0. 记录每一步的累加和，如果当前小于零，即往前跳，重置start
- 代码：

public int canCompleteCircuit(int[] gas, int[] cost) {<br/>
    // write your code here<br/>
    if (gas == null || gas.length == 0) return 0;<br/>
    int curr = 0;<br/>
    int remain = 0;<br/>
    int start = 0;<br/>
    int len = gas.length;<br/>
    for (int i = 0; i < len; i++) {<br/>
        curr += gas[i];<br/>
        curr -= cost[i];<br/>
        remain += gas[i] - cost[i];<br/>
        if (curr < 0) {<br/>
            start = i + 1;<br/>
            curr = 0;<br/>
        }<br/>
    }<br/>
    if (remain >= 0) {<br/>
        return start;<br/>
    }        <br/>
    return -1;<br/>
}<br/>