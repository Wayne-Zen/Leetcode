[Link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

```java
public class Solution {
    public List<String> letterCombinations(String digits) {
        HashMap<Integer, String> map = new HashMap<Integer, String>();
        map.put(2, "abc");
        map.put(3, "def");
        map.put(4, "ghi");
        map.put(5, "jkl");
        map.put(6, "mno");
        map.put(7, "pqrs");
        map.put(8, "tuv");
        map.put(9, "wxyz");
        map.put(0, "");
     
        ArrayList<String> result = new ArrayList<String>();
     
        if(digits == null || digits.length() == 0)
            return result;
     
        ArrayList<Character> now = new ArrayList<Character>();
        getString(digits, now, result, map, 0);
     
        return result;
    }
    
    private void getString(String digits, ArrayList<Character> now, 
            ArrayList<String> result, HashMap<Integer, String> map, int pos) {
        if (now.size() == digits.length()) {
            char[] now_arr = new char[digits.length()];
            for (int i = 0; i < now_arr.length; i++) {
                now_arr[i] = now.get(i);
            }
            result.add(String.valueOf(now_arr));
            return;
        }    
        String s = map.get(Integer.valueOf(digits.substring(pos, pos + 1)));
        for (int i = 0; i < s.length(); i++) {
            now.add(s.charAt(i));
            getString(digits, now, result, map, pos + 1);
            now.remove(now.size() - 1);
        }
    }
 

}
```
