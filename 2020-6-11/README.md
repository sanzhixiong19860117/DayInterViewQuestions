随机数组找出出现单数次的那个数

解法：最快的方式使用异或

```java
private static void demo2() {
    int[] a = {1, 1, 2, 2, 3, 3, 4, 4, 4};
    int emp = 0;
    for (int i = 0; i < a.length  ; i++) {
        emp^= a[i];
    }
    System.out.println("数据为="+emp);
}
```

