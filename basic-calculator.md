[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> num = new Stack<Integer>();
        Stack<Character> op = new Stack<Character>();
        Stack<Integer> numR = new Stack<Integer>();
        Stack<Character> opR = new Stack<Character>();
        StringBuilder sb = new StringBuilder();
        for (int i = -1; i <= s.length(); i++) {
            char c = ' ';
            if (i == -1) {
                c = '(';
            } else if (i == s.length()) {
                c = ')';
            } else {
                c = s.charAt(i);
            }
            
            if (Character.isDigit(c)) {
                sb.append(c);
            } else {
                if (sb.length() != 0) {
                    num.push(Integer.valueOf(sb.toString()));
                    sb = new StringBuilder();
                }
                
                if (c == '(' || c == '+' || c == '-') {
                    op.push(c);
                } else if (c == ')') {
                    while (op.peek() != '(') {
                        opR.push(op.pop());
                        numR.push(num.pop());
                    }
                    op.pop();
                    if (!opR.isEmpty()) {
                        numR.push(num.pop());
                        while (!opR.isEmpty()) {
                            char o = opR.pop();
                            int v1 = numR.pop();
                            int v2 = numR.pop();
                            if (o == '+') {
                                numR.push(v1 + v2);
                            } else if (o == '-') {
                                numR.push(v1 - v2);
                            }
                        }
                        num.push(numR.pop());
                    }
                }
            }
        }
        return num.pop();
    }
}
```

```java
public int calculate(String s) {
    Stack<Integer> stack = new Stack<Integer>();
    int result = 0;
    int number = 0;
    int sign = 1;
    for(int i = 0; i < s.length(); i++){
        char c = s.charAt(i);
        if(Character.isDigit(c)){
            number = 10 * number + (int)(c - '0');
        }else if(c == '+'){
            result += sign * number;
            number = 0;
            sign = 1;
        }else if(c == '-'){
            result += sign * number;
            number = 0;
            sign = -1;
        }else if(c == '('){
            //we push the result first, then sign;
            stack.push(result);
            stack.push(sign);
            //reset the sign and result for the value in the parenthesis
            sign = 1;   
            result = 0;
        }else if(c == ')'){
            result += sign * number;  
            number = 0;
            result *= stack.pop();    //stack.pop() is the sign before the parenthesis
            result += stack.pop();   //stack.pop() now is the result calculated before the parenthesis

        }
    }
    if(number != 0) result += sign * number;
    return result;
}
```
