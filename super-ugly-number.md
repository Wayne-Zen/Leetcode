[Link](https://leetcode.com/problems/super-ugly-number/)

```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] indexes = new int[primes.length];
        int[] res = new int[n];
        res[0] = 1;
        int cnt = 1;
        while (cnt < n) {
            cnt++;
            int min = Integer.MAX_VALUE;
            for (int i = 0; i < primes.length; i++) {
                min = Math.min(min, primes[i] * res[indexes[i]]);
            }
            res[cnt - 1] = min;
            for (int i = 0; i < primes.length; i++) {
                if (min == primes[i] * res[indexes[i]]) {
                    indexes[i]++;
                }
            }
        }
        return res[n - 1];
    }
}
```
```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        if (primes == null || primes.length == 0 || n < 1) {
            throw new IllegalArgumentException();
        }
        
        List<Integer> res = new ArrayList<Integer>();
        res.add(1);
        int[] indexes = new int[primes.length];
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>();
        for (int i = 0; i < primes.length; i++) {
            heap.offer(primes[i] * res.get(indexes[i]));
        }
        while (n > 1) {
            int min = heap.peek();
            res.add(min);
            for (int i = 0; i < primes.length; i++) {
                if (primes[i] * res.get(indexes[i]) == min) {
                    heap.poll();
                    indexes[i]++;
                    heap.offer(primes[i] * res.get(indexes[i]));
                }
            }
            n--;
        }
        return res.get(res.size() - 1);
    }
}
```

```java
public class Solution {
    class Unit {
        int val;
        int primeIndex;
        public Unit(int val, int primeIndex) {
            this.val = val;
            this.primeIndex = primeIndex;
        }
    }
    public int nthSuperUglyNumber(int n, int[] primes) {
        if (primes == null || primes.length == 0 || n < 1) {
            throw new IllegalArgumentException();
        }
        
        List<Integer> res = new ArrayList<Integer>();
        res.add(1);
        int[] indexes = new int[primes.length];
        PriorityQueue<Unit> heap = new PriorityQueue<Unit>(primes.length, 
                new Comparator<Unit>(){
                    public int compare(Unit u1, Unit u2) {
                        return u1.val - u2.val;
                    }
                });
        for (int i = 0; i < primes.length; i++) {
            heap.offer(new Unit(primes[i] * res.get(indexes[i]), i));
        }
        while (n > 1) {
            int min = heap.peek().val;
            res.add(min);
            while (heap.peek().val == min) {
                Unit u = heap.poll();
                indexes[u.primeIndex]++;
                heap.offer(new Unit(primes[u.primeIndex] * res.get(indexes[u.primeIndex]), u.primeIndex));
            }
            n--;
        }
        return res.get(res.size() - 1);
    }
}
```
