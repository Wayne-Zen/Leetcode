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
        while (s.length() > 0) {
            int loc = 0;
            for (int i = 0; i < s.length(); i++) {
                if (s.charAt(i) == '#') {
                    loc = i;
                    break;
                }
            }
            int len = Integer.valueOf(s.substring(0, loc));
            res.add(s.substring(loc + 1, loc + 1 + len));
            s = s.substring(loc + 1 + len);
        }
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```
