## 数组与集合互转

```java
// 数组转List 
String[]arr = new String[]{"123","345","456"};
List<String> list = Arrays.asList(arr);

// List转数组
String[] strings = list.toArray(new String[list.size()]);
```

