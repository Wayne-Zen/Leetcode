
* `str.length()` `arr.length`
* 默认排序是ascending
* Integer.valueof() 只接受 String， int
* Integer.MIN_VALUE 是 -2147483648，绝对值超出int的范围，所以Math.abs(-2147483648) 还是 -2147483648
* Java 是值传递，对象传的是地址，所以方法外定义， 方法内赋值很危险。
* 两层while循环，要注意内层循环是否会破坏外层条件, 考虑是否可以用if代替

## java 容器

* 读取容器，一定要判断是否为空

* Stack
  * peek()
  * pop()
  * push()

* PriorityQueue
  * 若要指定comparator, 第一个参数必须是size
  * size不能为0, 一定要进行参数检查

## two pointer
* 千万不要忘记更新指针， ＋＋／－－
* 一块一慢， 一前一后，对冲
* 链表 dummynode


## DFS
* 走过之后还能用前面的，需要viisted数组。

## binary tree
* root 检查是第一步
* 左右节点不见得存在，注意查空


