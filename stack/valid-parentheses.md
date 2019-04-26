[Valid Parentheses]

* 思路：主要是利用stack来解题，如果是空的栈，判断进入的符号是不是右半边，如果是就返回不合法；不是右半边，就持续push。当栈不为空的时候，判断来的跟当前最顶上的是不是一对，不是一对但是是左半边的可以继续push，不是一对但是是右半边的直接返回不合法。最后判断栈是否为空
* 代码

        <
        public boolean isValidParentheses(String s) {
            // write your code here
            if (s == null || s.length() == 0) return true;
            
            Stack<Character> stack = new Stack<>();
            for (int i = 0; i < s.length(); i++) {
                char c = s.charAt(i);
                if (stack.isEmpty()) {
                    if (c == ')' || c == ']' || c == '}') {
                        return false;
                    } else {
                        stack.push(c);
                    }
                } else {
                    char top = stack.peek();
                    if ((top == '(' && c == ')') || (top == '[' && c == ']') || (top == '{' && c == '}')) {
                        stack.pop();
                    } else {
                        if (c == '(' || c == '[' || c == '{') {
                            stack.push(c);
                        } else {
                            return false;
                        }
                    }
                }
            }
            
            return stack.isEmpty();
        }
        >