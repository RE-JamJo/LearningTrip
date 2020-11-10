# String类


## 定义
String类代表字符串。同时是Object类的一个子类。Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现。

字符串是常量；它们的值在创建之后不能更改。字符串缓冲区支持可变的字符串。因为 String 对象是不可变的，所以可以共享。（这里所谓的不可变，是指一个字符串对象一旦被创建，如果要修改字符串，总是创建新的字符串对象，在新的字符串对象中，修改字符序列）
- 1、一个字符串对象一旦创建好之后，这个字符串对象所代表的字符序列就固定了
- 2、对已有字符串对象，所代表的字符序列的修改，只会发生在jvm新创建的字符串对象中

每一个字符串字面值常量，对应的字符串对象，都存储在字符串常量池中。
- 字符串常量池jdk6及以前存储在方法区中
- jdk7开始就存储在堆上

进行字符串拼接时，先在字符串常量池创建对象，再在堆上创建一个对象指向这两个字符串，即我们的对象指向的是堆上的jvm创建的对象。

要点：String s = new String("Hello") 和 String s = "Hello"
- 只要是new就是在堆上创建对象
- 而字符串字面值常量存储在字符串常量池中

字符串拼接何时会在堆上，创建新的字符串对象，何时不会呢？
- 当参与拼接的两个字符串中，至少有一个是以字符串的引用变量的形式出现，此时拼接运算，必然会在堆上创建新的字符串对象
- 只有参与字符串拼接运算两个字符串，都是字符串常量的时候，此时不会在堆上创建新的字符串对象，而是直接拼接

## 构造方法

- String() 
    - 初始化一个新创建的 String 对象，使其表示一个空字符序列。
    - 注意：空字符串不代表null，这两个完全不同。
- String(byte[] bytes) 
    - 通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String 
- String(byte[] bytes, int offset, int length) 
    - 通过使用平台的默认字符集解码指定的 byte 子数组，构造一个新的 String。
- String(char[] value) 
    - 分配一个新的 String，使其表示字符数组参数中当前包含的字符序列。
- String(int[] codePoints, int offset, int count) 
    - 分配一个新的 String，它包含 Unicode 代码点数组参数一个子数组的字符。
- String(String original) 
    - 初始化一个新创建的 String 对象，使其表示一个与参数相同的字符序列；换句话说，新创建的字符串是该参数字符串的副本。

## 成员方法

### 判断
- boolean equals(Object anObject) 
    - 将此字符串与指定的对象比较。

- boolean equalsIgnoreCase(String anotherString) 
    - 将此 String 与另一个 String 比较，不考虑大小写。

- boolean contains(String str)
	- 判断当前字符串对象是否包含，目标字符串的字符序列。

- boolean startsWith(String prefix) 
    - 测试此字符串是否以指定的前缀开始。 

- boolean endsWith(String suffix) 
    - 测试此字符串是否以指定的后缀结束。

- boolean isEmpty() 
    - 当且仅当length()为0时返回true。
    - **注意：如果是null会出现空指针异常。**

### 获取

- char charAt(int index) 
    - 返回指定索引处的 char 值。
    - 可以用于遍历字符串。

- int length() 
    - 返回此字符串的长度。

- int indexOf(int ch) 
    - 返回指定字符在此字符串中第一次出现处的索引。

- int indexOf(int ch, int fromIndex) 
    - 返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。 

- int indexOf(String str) 
    - 返回指定子字符串在此字符串中第一次出现处的索引。

- int indexOf(String str, int fromIndex) 
    - 返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。

- String substring(int beginIndex) 
    - 返回一个新的字符串，它是此字符串的一个子字符串。
 
- String substring(int beginIndex, int endIndex) 
    - 返回一个新字符串，它是此字符串的一个子字符串。

### 转换

- byte[] getBytes() 
    - 使用平台的默认字符集将此String编码为byte序列，并将结果存储到一个新的byte数组中。 

- char[] toCharArray() 
    - 将此字符串转换为一个新的字符数组。

- static String valueOf(int i) 
    - 返回 int 参数的字符串表示形式。（把整数转换成一个字符串）

- String toLowerCase() 
    - 使用默认语言环境的规则将此 String 中的所有字符都转换为小写。

- String toUpperCase() 
    - 使用默认语言环境的规则将此 String 中的所有字符都转换为大写。 

- String concat(String str) 
    - 将指定字符串连接到此字符串的结尾。
    - 等价于+号实现的字符串拼接。

### 替换

- String replace(char oldChar, char newChar) 
    - 返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。 

- String replace(String old,String new)
	- 在新的字符串中，用新new字符串，替换旧的old字符串。

### 去除字符串头，尾的空格

- String trim()

### 比较功能

- int compareTo(String str)
	- 比较当前字符串和目标字符串的大小

- int compareToIgnoreCase(String str)
	
- 字符串大小如何比较？
	- 在字典中，先出现的字符串小，后出现的字符串大
	- 具体到编程语言，是根据两个字符串从左往右数，第一个对应位置的不同字符，来决定字符串的大小

