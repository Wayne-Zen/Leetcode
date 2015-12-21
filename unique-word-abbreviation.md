[Link](https://leetcode.com/problems/unique-word-abbreviation/)

```java
public class ValidWordAbbr {
    HashMap<String, String> map = new HashMap<String, String>();
    public ValidWordAbbr(String[] dictionary) {
        for (String str : dictionary) {
            if (str.length() <= 2) {
                continue;
            }
            String s = shorten(str);
            if (map.containsKey(s)) {
                if (!map.get(s).equals(str)) {
                    map.put(s, "");
                }
            } else {
                map.put(s, str);
            }
        }
    }

    public boolean isUnique(String word) {
        if (word.length() <= 2) {
            return true;
        }
        String s = shorten(word);
        if (map.containsKey(s) && !map.get(s).equals(word)) {
            return false;
        }
        return true;
    }
    
    private String shorten(String str) {
        return "" + str.charAt(0) + (str.length() - 2) + str.charAt(str.length() - 1);
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```
