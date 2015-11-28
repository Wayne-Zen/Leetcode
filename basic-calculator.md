[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> num = new Stack<Integer>();
        Stack<Character> op = new Stack<Character>();
        int val = -1;
        for (int i = -1; i <= s.length(); i++) {
            // c
            char c = ' ';
            if (i == -1) {
                c = '(';
            } else if (i == s.length()) {
                c = ')';
            } else {
                c = s.charAt(i);
            }
            
            // handle number
            if (Character.isDigit(c)) {
                if (val == -1) {
                    val = c - '0';
                } else {
                    val = 10 * val + c - '0';
                } 
            } else {
                if (val != -1) { 
                    num.push(val);
                    val = -1;
                }
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
