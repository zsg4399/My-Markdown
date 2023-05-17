 

### 文章目录

*   *   [Java 中 String 类的常用方法](#Java__String__2)
    *   *   [一、String 类的概念](#String__4)
        *   [二、常用的构造方法](#_13)
        *   [三、常用方法](#_22)
        *   *   [1、toString()](#1toString_24)
            *   [2、length()](#2length_33)
            *   [3、getBytes()](#3getBytes_42)
            *   [4、toCharArray()](#4toCharArray_56)
            *   [5、charAt(int index)](#5charAtint_index_68)
            *   [6、isEmpty()](#6isEmpty_79)
            *   [7、equals(Object anObject)](#7equalsObject_anObject_105)
            *   [8、compareTo(String anotherString)](#8compareToString_anotherString_118)
            *   [9、contains(CharSequence s)](#9containsCharSequence_s_137)
            *   [10、trim()](#10trim_148)
            *   [11、toUpperCase() 和 toLowerCase()](#11toUpperCase__toLowerCase_159)
            *   [12、substring(...)](#12substring_173)
            *   [13、replace(...)](#13replace_228)
            *   [14、split(String regex)](#14splitString_regex_240)
            *   [15、startsWith(...) 和 endsWith(...)](#15startsWith__endsWith_250)
            *   [16、indexOf(...) 和 lastIndexOf(...)](#16indexOf__lastIndexOf_267)

Java 中 String 类的常用方法
--------------------

### 一、String 类的概念

*   java.lang.String 类用于描述字符串，Java程序中所有的字符串面值都可以用该类的对象加以描述。
*   该类由 **final** 关键字修饰，表示该类**不能被继承**。
*   从 jdk1.9开始该类的底层不使用 char\[\] 来存储数据，而是改成 **byte\[\]** 加上编码标记，从而节约了一些空间。
*   该类描述的字符串内容是个**常量**，不可更改，可以被共享使用。

[常量池](https://so.csdn.net/so/search?q=%E5%B8%B8%E9%87%8F%E6%B1%A0&spm=1001.2101.3001.7020)（了解）：由于String类型描述的字符串内容是常量不可改变，因此 Java 虚拟机将首次出现的字符串放入**常量池**中，若后续代码中出现了相同字符串内容则直接使用池中已有的字符串对象而无需申请内存及创建对象，从而提高了性能。

### 二、常用的构造方法

方法声明

功能介绍

String()

使用无参方式构造对象得到**空字符序**

String(byte\[\] bytes)

使用 bytes 数组中的所有内容构造对象

String(char\[\] value)

使用 value 数组中的所有内容构造对象

String(String original)

根据参数指定的字符串内容来构造对象，新创建对象为参数对象的副本

### 三、常用方法

#### 1、toString()

> toString() 方法：返回字符串本身，返回值为 **String** 类型

    String str = new String("Hello World");
    System.out.println("str = " + str);//Hello World
    

#### 2、length()

> length() 方法：返回字符串字符序列的长度（空格也算），返回值为 **int** 类型

    String str = new String("Hello World");
    System.out.println(str.length());//11
    

#### 3、getBytes()

> getBytes() 方法：将当前字符串内容转换为 byte 数组并返回，返回值为 **byte\[\]**，该方法的返回值可作为 String 构造方法的参数

    //将String类型转换为byte数组类型并打印
    //先将字符串拆分为字符，再将每个字符转换为byte类型，也就是获取所有字符的ASCII码
    String str = new String("Hello World");
    byte[] bytes = str.getBytes();
    for (int i = 0; i < bytes.length; i++) {
    	System.out.println("下标为" + i + "的元素为：" + bytes[i]);//打印的是每个字母对应的ASCII码
    }
    

#### 4、toCharArray()

> toCharArray() 方法：将当前字符串内容转换为 char 数组并返回，返回值为 **char\[\]**，该方法的返回值可作为 String 构造方法的参数

    String str = new String("Hello World");
    char[] cArr = str.toCharArray();
    for (int i = 0; i < str.length(); i++) {
        System.out.println("下标为" + i + "的元素为：" + cArr[i]);//打印的是每个字母
    }
    

#### 5、charAt(int index)

> charAt(int index) 方法：用于返回字符串指定位置的字符，返回值为 **char** 类型，参数为 **int** 类型

    String str = new String("Hello World");
    for (int i = 0; i < str.length(); i++) {
        System.out.println("下标为" + i + "的元素为：" + str.charAt(i));//打印的是每个字母
    }
    

#### 6、isEmpty()

> isEmpty() 方法：判断字符串是否为空，返回值为 **boolean** 类型，查看该方法的源码可知字符串的 length 为0则为空
> 
> **注意**：开发中判断字符串是否为空一般采用 **org.apache.commons.lang3** 下的 **StringUtils** 中的静态方法 **isEmpty()** 和 **isBlank()**；
> 
> StringUtils 类与 String 类的区别在于：StringUtils 类是 null 安全的，即如果输入参数 String 为 null，则不会抛出 NullPointerException 空指针异常，代码考虑更全面

    String str1 = null;
    String str2 = "";
    String str3 = " ";
    System.out.println(str2.isEmpty());//true
    System.out.println(str3.isEmpty());//false
    System.out.println(str1.isEmpty());//java.lang.NullPointerException
    
    //拓展StringUtils.isBlank()和StringUtils.isEmpty()
    StringUtils.isBlank(null)      = true
    StringUtils.isBlank("")        = true
    StringUtils.isBlank(" ")       = true
    
    StringUtils.isEmpty(null)      = true
    StringUtils.isEmpty("")        = true
    StringUtils.isEmpty(" ")       = false
    

#### 7、equals(Object anObject)

> equals(Object anObject) 方法：比较**字符串内容**是否相等并返回，返回值为 **boolean** 类型
> 
> equalsIgnoreCase(String anotherString)方法：比较字符串内容是否相等并返回，返回值为 **boolean** 类型，**不考虑大小写**， 如：'A’和’a’是相等

    String str = new String("Hello World");
    //注意：开发中作比较一般常量值在前，变量值在后
    System.out.println("hello world".equals(str));//false
    System.out.println("hello world".equalsIgnoreCase(str));//true
    

#### 8、compareTo(String anotherString)

> compareTo(String anotherString) 方法：比较调用对象和参数对象的大小关系，返回值为 **int** 类型
> 
> compareToIgnoreCase(String str) 方法：比较调用对象和参数对象的大小关系，返回值为 **int** 类型，不考虑大小写，也就是’a’和’A’是相等的关系
> 
> 比较大小的方法：例如 A.compareTo(B)，拿方法调用者(A)的字符依次与方法参数(B)的字符作比较，即用 A 的 ASCII码减去 B 的ASCII码；结果有三种：负整数、正整数、零。负整数即按字典顺序 A 在 B 之前，正整数即 A 在 B 之后，零则为字符串相等。
> 
> 注意：比较出大小就不往后进行，即从第一个字符串开始比较，相同则比较下一个，直到比较出大小或比较到最后一个字符。

    String str = "hello";
    System.out.println(str.compareTo("world"));  // 'h' - 'w' => 104 - 119 => -15
    System.out.println(str.compareTo("haha"));   // 'e' - 'a' => 101 - 97  => 4
    System.out.println(str.compareTo("heihei")); // 'l' - 'i' => 108 - 105 => 3
    System.out.println(str.compareTo("helloworld")); // 长度： 5 - 10 => -5
    System.out.println(str.compareToIgnoreCase("HELLO")); // 0
    

#### 9、contains([CharSequence](https://so.csdn.net/so/search?q=CharSequence&spm=1001.2101.3001.7020) s)

> contains(CharSequence s) 方法：判断当前字符串是否包含参数指定的内容，返回值为 **boolean** 类型，参数CharSequence 为一个接口，CharSequence 是 char 值的可读序列，参数可以为String、StringBuilder、StringBuffer等类型

    String str = "Give you some color to see see";
    System.out.println(str.contains("some"));//true
    System.out.println(str.contains("Some"));//false
    

#### 10、trim()

> trim() 方法：返回去掉前导和尾随空白的字符串，返回值为 **String** 类型

    String str = " Hello World ";
    System.out.println(str.trim());//Hello World
    System.out.println(str.length());//13
    System.out.println(str.trim().length());//11
    

#### 11、toUpperCase() 和 toLowerCase()

> toUpperCase() 方法：返回字符串的大写形式，返回值为 **String** 类型
> 
> toLowerCase() 方法：返回字符串的小写形式，返回值为 **String** 类型
> 
> 此两种方法经常用于在对字符串做判断时使用，因为要判断的字符串可能为驼峰式或者不规则的方式，故先将判断的字符串转为大写或者小写，然后与常量去做比较。

    String str = "Hello World";
    System.out.println(str.toLowerCase());//hello world
    System.out.println(str.toUpperCase());//HELLO WORLD
    

#### 12、substring(…)

该方法有两个重载的方法，分别为：

> substring(int beginIndex, int endIndex) 方法：返回字符串中从下标 beginIndex(包括) 开始到 endIndex(不包括) 结束的子字符串，返回值为 **String** 类型，参数为 **int** 类型
> 
> substring(int beginIndex) 方法：返回字符串中从下标 beginIndex(包括) 开始到字符串结尾的子字符串，返回值为 **String** 类型，参数为 **int** 类型
> 
> 注意：Java 中涉及到区间的问题，一般都为 **左边包括，右边不包括**，即左开右闭，“\[ x , y )”

    /**
    * 根据传入的Map的value值来处理脱敏数据，脱敏规则规则如下：
    * 大于5位: 前后各保留2位，中间显示星号,
    * 3-4位: 前后保留一位，中间星号,
    * 2位: 第一位星号，第二位保留,
    * 1位: 直接显示星号
    *
    * @param value value值
    * @return 脱敏处理过后的value
    */
    private Object updateMaskingValue(Object value){
        String str = value.toString();
        int length = value.toString().length();
        if(1 == length){
            return "*";
        }
        if(2 == length){
            StringBuilder stringBuilder = new StringBuilder();
            stringBuilder.append("*" + str.substring(1));
            return stringBuilder.toString();
        }
        if(3 == length || 4 == length){
            StringBuilder stringBuilder = new StringBuilder();
            stringBuilder.append(str.substring(0,1));
            for (int i = 0; i < length - 2; i++) {
                stringBuilder.append("*");
            }
            stringBuilder.append(str.substring(length - 1));
            return stringBuilder;
        }
        if(5 <= length){
            StringBuilder stringBuilder = new StringBuilder();
            stringBuilder.append(str.substring(0,2));
            for (int i = 0; i < length - 4; i++) {
                stringBuilder.append("*");
            }
            stringBuilder.append(str.substring(length - 2));
            return stringBuilder.toString();
        }else {
            return "";
        }
    }
    

#### 13、replace(…)

> replace(char oldChar, char newChar) 方法：使用参数newChar替换此字符串中出现的所有参数oldChar，返回值为 **String** 类型，参数为 **char** 类型
> 
> replace(CharSequence target, CharSequence replacement) 方法：用新字符串replacement替换所有的旧字符串target，返回值为 **String** 类型，参数为 CharSequence 接口

    System.out.println("Hello World".replace('o', 'e'));//Helle Werld
    System.out.println("JonL".replace('q', 'x'));//JonL 无改变则返回原字符串
    System.out.println("aaa".replace("aa", "b"));//ba
    

#### 14、split(String regex)

> split(String regex) 方法：参数regex为正则表达式，以regex所表示的字符串为分隔符，将字符串拆分成字符串数组，结尾的空字符串不包含在结果数组中，返回值为 **String\[\]** 类型，参数为 **String** 类型

    String str = "boo:and:foo";
    String[] split = str.split(":");//结果为："boo", "and", "foo"
    String[] split = str.split("o");//结果为："b", "", ":and:f"
    

#### 15、startsWith(…) 和 endsWith(…)

> startsWith(String prefix) 方法：判断字符串是否以参数字符串开头，返回值为 **boolean** 类型，参数为 **String** 类型
> 
> startsWith(String prefix, int toffset) 方法：从指定位置开始是否以参数字符串开头，返回值为 **boolean** 类型，参数 prefix 为 **String** 类型，toffset 为 **int** 类型
> 
> endsWith(String suffix) 方法：判断字符串是否以参数字符串结尾，返回值为 **boolean** 类型，参 数为 **String** 类型

    String str = "Give you some color to see see";
    System.out.println(str.startsWith("G"));//true
    System.out.println(str.startsWith(" "));//false
    System.out.println(str.startsWith("you", 5));//true
    System.out.println(str.endsWith(" "));//false
    System.out.println(str.endsWith("see"));//true
    

#### 16、indexOf(…) 和 lastIndexOf(…)

**方法声明**

**功能介绍**

int indexOf(int ch)

用于返回当前字符串中参数 ch 指定的字符第一次出现的下标

int indexOf(int ch, int fromIndex)

用于从 fromIndex(包含) 位置开始查找ch指定的字符

int indexOf(String str)

在字符串中检索 str 返回其第一次出现的位置，若找不到返回-1

int indexOf(String str, int fromIndex)

表示从字符串的 fromIndex(包含) 位置开始检索str第一次出现的位置

int lastIndexOf(int ch)

用于返回参数 ch 指定的字符最后一次出现的下标

int lastIndexOf(int ch, int fromIndex)

用于从 fromIndex(包含) 位置开始反向查找 ch 指定字符出现的下标，若找不到返回-1

int lastIndexOf(String str)

返回 str 指定字符串最后一次出现的下标

int lastIndexOf(String str, int fromIndex)

用于从 fromIndex(包含) 位置开始反向搜索的第一次出现的下标

    String str = "Good Good Study, Day Day Up!";
    System.out.println(str.indexOf('g')); // -1  代表查找失败
    System.out.println(str.indexOf('G')); // 0   该字符第一次出现的索引位置
    System.out.println(str.indexOf('G', 0)); // 0
    System.out.println(str.indexOf('G', 1)); // 5
    
    // 查找字符串
    System.out.println(str.indexOf("day")); // -1
    System.out.println(str.indexOf("Day")); // 17   字符串中第一个字符的下标
    System.out.println(str.indexOf("Day", 17)); // 17   字符串中第一个字符的下标
    System.out.println(str.indexOf("Day", 18)); // 21   字符串中第一个字符的下标
    
    // 字符串内容的反向查找
    System.out.println(str.lastIndexOf("Day")); // 21
    System.out.println(str.lastIndexOf("Day",  21)); // 21
    System.out.println(str.lastIndexOf("Day", 20)); // 17
    System.out.println(str.lastIndexOf("Day", 15)); // -1## 目标


### 原理
