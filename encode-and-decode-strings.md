[Link](https://leetcode.com/problems/encode-and-decode-strings/)

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder();
        for (String str : strs) {
            sb.append(str.length());
            sb.append('#');
            sb.append(str);
        }
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List<String> res = new ArrayList<String>();
        int i = 0;
        int len = 0;
        while (i < s.length()) {
            char c = s.charAt(i);
            if (c != '#') {
                len = len * 10 + c - '0';
                i++;
            } else {
                res.add(s.substring(i + 1, i + 1 + len));
                i = i + 1 + len;
                len = 0;   
            }
        }
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```
