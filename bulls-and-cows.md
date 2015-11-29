[Link](https://leetcode.com/problems/bulls-and-cows/)

```java
public class Solution {
    public String getHint(String secret, String guess) {
        int A = 0;
        int B = 0;
        HashMap<Character, Integer> map1 = new HashMap<Character, Integer>(); // cnt 
        HashMap<Character, Integer> map2 = new HashMap<Character, Integer>();
        for (int i = 0; i < guess.length(); i++) {
            if (secret.charAt(i) == guess.charAt(i)) {
                A++;
            } else {
                char c1 = secret.charAt(i);
                if (map1.containsKey(c1)) {
                    map1.put(c1, map1.get(c1) + 1);
                } else {
                    map1.put(c1, 1);
                }
                char c2 = guess.charAt(i);
                if (map2.containsKey(c2)) {
                    map2.put(c2, map2.get(c2) + 1);
                } else {
                    map2.put(c2, 1);
                }
            }
        }
        for (char c : map1.keySet()) {
            if (map2.containsKey(c)) {
                B += Math.min(map1.get(c), map2.get(c));
            }
        }
        return A + "A" + B + "B";
    }
}
```
