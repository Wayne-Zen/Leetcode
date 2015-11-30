[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> num = new Stack<Integer>();
        Stack<Character> op = new Stack<Character>();
        int val = 0;
        boolean numFlag = false;
        s = "(" + s + ")";
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            while (Character.isDigit(c)) {
                val = val * 10 + c - '0';
                c = s.charAt(++i);
                numFlag = true;
            }
            if (numFlag) {
                num.push(val);
                val = 0;
                numFlag = false;
            }
            if (c == ' ') {
                continue;
            }
            // handle operator
            if (c == '(' || c == '+' || c == '-') {
                op.push(c);
            } else if (c == ')') {
                int temp = 0;
                while (op.peek() != '(') {
                    char o = op.pop();
                    int v = num.pop();
                    if (o == '-') {
                        temp += -v;
                    } else if (o == '+') {
                        temp += v;
                    }
                }
                num.push(num.pop() + temp);
                op.pop();
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
