# Arrays.asList()方法 返回的ArrayList 抛出 UnsupportedOperationException



出错一段代码

```java
List<Integer> list1=new ArrayList<Integer>();
list = Arrays.<Integer>asList(1, 2, 3);
list.add(1);
```

执行后

```xml
Exception in thread "main" java.lang.UnsupportedOperationException
	at java.util.AbstractList.add(Unknown Source)
```



这个异常估计大家比较熟悉，debug代码到下面方法时候尴尬

debug找不到源码，根据提示把项目导入也没生效

自己看看源代码分析吧,下面是`AbstractList#add`方法

```java
    public boolean add(E e) {
        add(size(), e);
        return true;
    }



    public void add(int index, E element) {
        throw new UnsupportedOperationException();
    }


原来这个默认``AbstractList`add方法没有实现的话，会抛出不支持这种操作的异常，你的 `Arrays`内部类`ArrayList` 默认没有实现

add方法所以会抛出标题的错，有没有实现remove()

>  [内部类字节码详细解释](https://blog.csdn.net/qq_33330687/article/details/77915345)





