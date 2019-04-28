[Merge Intervals]

* 思路：先通过interval的start对list进行排序，然后通过设置last 和 curr interval，遍历所有的interval，判断curr interval的start跟last interval的end的大小
* 代码

        <
        class IntervalComparator implements Comparator<Interval> {
            @Override
            public int compare(Interval a, Interval b) {
                return a.start - b.start;
            }
        }
        public List<Interval> merge(List<Interval> intervals) {
            // write your code here
            if (intervals == null || intervals.size() <= 1) return intervals;
            
            Collections.sort(intervals, new IntervalComparator());
            List<Interval> res = new ArrayList<>();
            
            Interval last = intervals.get(0);
            for (int i = 1; i < intervals.size(); i++) {
                Interval curr = intervals.get(i);
                if (curr.start <= last.end) {
                    last.end = Math.max(curr.end, last.end);
                } else {
                    res.add(last);
                    last = curr;
                }
            }
            
            res.add(last);
            return res;
        }
        >