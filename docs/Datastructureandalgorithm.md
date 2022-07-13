## 一. 数据类型转化技巧

### 1 简单数据类型之间的转换

在Java中整型、实型、字符型被视为简单数据类型，这些类型由低级到高级分别为(byte，short，char)–int–long–float–double
简单数据类型之间的转换又可以分为：
●低级到高级的自动类型转换
●高级到低级的强制类型转换
●包装类过渡类型能够转换
低级变量可以直接转换为高级变量，自动类型转换：

```java
byte b;
int i=b;
long l=b;
float f=b;
double d=b;
char c='8';
int i=c - '0';
System.out.println("output:" i);
//输出：output:99;
```

对于byte,short,char三种类型而言，他们是平级的，因此不能相互自动转换，可以使用下述的[强制类型转换](https://so.csdn.net/so/search?q=强制类型转换&spm=1001.2101.3001.7020):

```java
short i=99;
char c=(char)i;
System.out.println("output:" c);
//输出：output:c;
```

但根据笔者的经验，byte,short,int三种类型都是整型，因此如果操作整型数据时，最好统一使用int型。将高级变量转换为低级变量时，情况会复杂一些，你可以使用强制类型转换。即你必须采用下面这种语句格式：

```java
int i=99;
byte b=(byte)i;
char c=(char)i;
float f=(float)i;
```

```java
//1、float型转换为double型：
float f1=100.00f;
Float F1=new Float(f1);

//F1.doubleValue()为Float类的返回double值型的方法
double d1=F1.doubleValue();

//2、double型转换为int型：
double d1=100.00;
Double D1=new Double(d1);
int i1=D1.intValue();

//3、int型转换为double型：
int i1=200;
double d1=i1;
```

### 2 字符串与其它数据类型的转换

#### 1. 其它类型向字符串的转换

①调用类的串转换方法:`X.toString()`;
       ②自动转换:`X+""`;
       ③基本类型都可以使用String的方法:`String.volueOf(X)`;

#### 2.字符串作为值,向其它基本类型的转换

①先转换成相应的封装器实例,再调用对应的方法转换成其它类型
		例如，字符中"32.1"转换double型的值的格式为**:`new Float(“32.1”).doubleValue()`**;
        也可以用:`Double.valueOf(“32.1”).doubleValue()`;
       ②静态parseXXX方法

```java
String s = "1";
byte b = Byte.parseByte( s );
short t = Short.parseShort( s );
int i = Integer.parseInt( s );
long l = Long.parseLong( s );
Float f = Float.parseFloat( s );
Double d = Double.parseDouble( s );
```

#### 3. 字符串转化为char[]数组

```java
String str = 'nx1111';
char[] chArray = str.toCharArray();
```

### 3 字符数组char[]转String

`String.valueOf(char[] charArray)`

`new String(char[] charArray)`

```java
char[] str = {'h','e', 'l', 'l', 'o', '  ', '1','2','3'};  //创建一个字符数组
	String string1 = new String(str);
	String string2 = String.valueOf(str);
	System.out.println(string1);  //hello 123
	System.out.println(string2);
	System.out.println(string1 == string2);  //false
	System.out.println(string1.equals(string2));  //true
/*两者的结果不一样，因为在string1 == string2中，比较的是地址，由于string1 和 string2是两个不同的对象，string1是通过new方法创建的，string2是由valueOf()方法返回的对象，所以二者的地址不一样，等式的结果就是false。
而String的equals()方法比较的是值
*/

```



### 4 日期格式设置

```java
Date date = new Date();
SimpleDateFormat sy1=new SimpleDateFormat("yyyy-MM-dd");
String dateFormat=sy1.format(date);
```

### 5 List< String >集合转数组String[ ]

调用数组对象的toArray方法，参数传入String数组类型，内部做类型转换
`strList.toArray(new String[strList.size()])`

```java
List<String> strList= new ArrayList<>();
    strList.add("牛八少爷");
    strList.add("欧阳无敌");
    strList.add("西门吹雪");
    String [] strArray = strList.toArray(new String[strList.size()]);
    for (String string : strArray) {
        System.out.println(string);
    }
```

### 6  String[ ]数组转集合List < String >

#### 1 数组工具类的asList()

但是这种方法却有其局限性，如果传入的参数是一个数组，那么这个数组一定要是引用类型才能将其转换为List集合，当传入基本数据类型数组时则会将这个数组对象当成一个引用类型对象存进List集合。

![1401949-20190805132932520-555863570](Datastructureandalgorithm.assets/1401949-20190805132932520-555863570.png)

![1660253-20190417223551607-1371188487](Datastructureandalgorithm.assets/1660253-20190417223551607-1371188487.png)

可以看到传入基本数据类型时，打印该列表是打印了传入的数组的地址值。你也可以直接将其传入asList()方法的参数中,就像这样

```java
//String不是基本数据类型，输出结果是1
String[] strArray = {"1", "2" ,"3"};
List list = Arrays.asList(strArray);
System.out.println(list.get(0));
```

ArrayList可以存放不同类型的数据

![1660253-20190417224546736-1897541673](Datastructureandalgorithm.assets/1660253-20190417224546736-1897541673.png)

这种方法显然不太好用，那怎么将一组基本数据类型的数组转换成集合呢，我们首先想到的是将该基本类型数组转换成其对应包装类类型的数组(遍历转换也可以)原文链接](https://zhidao.baidu.com/question/628312636366178684.html))。

![1660253-20190417230403671-1142295552](Datastructureandalgorithm.assets/1660253-20190417230403671-1142295552.png)

#### 2 使用Spring框架

```java
int[]  a = {1,2,3};
List list = CollectionUtils.arrayToList(a);
System.out.println(list);
```

#### 3 JDK8新特性

![img](Datastructureandalgorithm.assets/1660253-20190417230431839-1358725408.png)

#### 4  Collections工具类

```java
//创建数组与集合
String[] string=new String[5];
ArrayList<String> list = new ArrayList<String>();
//把数组转成集合，也就是把数组里面的数据存进集合；
Collections.addAll(list, string);
```



### 7 字符集合List< Character > path转字符串String str

```java
//字符集合转为字符串对象
StringBuilder str = new StringBuilder();
for (Character character : path) {// 对ArrayList进行遍历，将字符放入StringBuilder中
	str.append(character);
	}
```

### 8 二维字符数组char[][] charArray转List< String >

```java
public List Array2List(char[][] chessboard) {
        List<String> list = new ArrayList<>();

        for (char[] c : chessboard) {
            list.add(String.copyValueOf(c));
        }
        return list;
    }
```

### 9 字符串截取函数substring()方法

- 语法

  ```java
  public String substring(int beginIndex)
  或
  public String substring(int beginIndex, int endIndex)
  ```

- 参数

  - **beginIndex** -- 起始索引（包括）, 索引从 0 开始。
  - **endIndex** -- 结束索引（不包括）。

  ![img](Datastructureandalgorithm.assets/java-substring-20201208.png)

### 10 集合转集合

```java
 ArrayList<ArrayList<Integer>> res = new ArrayList();
 ArrayList<Integer> valPath = new ArrayList();
 ArrayList<Integer> path = new ArrayList<Integer>(valPath)
```

### 11 数组直接赋值

```java
String[] s = new String(){"a","b","c"};
```



## 二. 笔试输入输出框架

### 1 多行输入元素

以三行输入为例，第一行输入两个数字m，n，分别表示数组num1和num2的长度，第二行和第三行输入num1和num2的元素，以空格分隔。

```java
// 输入如下
3 4
10 2 3 
11 4 5 6
```

```java
import java.util.Arrays;
import java.util.Scanner;

public class myScanner {
    public static void main(String[] args) {
        System.out.println("输入：");
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        int n = sc.nextInt();
        int[] num1 = new int[m];
        int[] num2 = new int[n];
        // 换成其他数据类型也一样，其他数值类型就修改int跟nextInt就可以了，
        //String就把nextInt()换成next(),nextInt空格分隔读取
        for(int i = 0; i < m; i ++) {
            num1[i] = sc.nextInt();  // 一个一个读取
        }
        for(int i = 0; i < n; i ++) {
            num2[i] = sc.nextInt();
        }
        System.out.println("输出：");
        System.out.println(Arrays.toString(num1));
        System.out.println(Arrays.toString(num2));
    }
}
```

### 2 单行输入多个参数

以空格（也可用其他的符号）为分割

```java
// 输入如下
ABB CCC DDD  EEE 123 435
```

```java
import java.util.Arrays;
import java.util.Scanner;

public class myScanner {
	Scanner sc = new Scanner(System.in);
	public static void main(String[] args) {
		System.out.println("输入：");
		Scanner sc = new Scanner(System.in);
		String str = sc.nextLine();  // 读取一行
		System.out.println("输出：");
		System.out.println(str);
		String[] strIn = str.trim().split(" ");  // 以空格分割
		System.out.println(Arrays.toString(strIn));
	}
}
```

### 3 多行输入多个参数，每行参数个数不定

假设第一行输入m，n，m表示后面有m行，n表示每行最多有n个(可用来截断某一行多输入的参数，不详细分析了)

```java
// 输入如下
3 4
AA bcd 123 54
AA BB
A B C

```

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Scanner;

public class myScanner {
	Scanner sc = new Scanner(System.in);
	public static void main(String[] args) {
		System.out.println("输入：");
		Scanner sc = new Scanner(System.in);
		int m = sc.nextInt();
		sc.nextLine();  // 很重要，跳到第二行
		// 若直接确定行数，注释掉上面两行，加入下面一行
		// int m = 3;
		String[] strArr = new String[m];
		// 从第二行开始读取
		for(int i = 0; i < m; i++) {
			strArr[i] = sc.nextLine();
		}
		System.out.println("输出：");
		System.out.println(Arrays.toString(strArr));
		ArrayList<String[]> strToOne = new ArrayList<String[]>();
		for(int i = 0; i < m; i ++) {
			String[] tmp = strArr[i].trim().split(" ");
			strToOne.add(tmp);
		}
		System.out.println(strToOne);
		// 形象点显示
		System.out.print("[");
		for(int i = 0; i < strToOne.size(); i++) {
			System.out.print(Arrays.toString(strToOne.get(i)));
			if(i != strToOne.size()-1)
				System.out.print(", ");
		}
		System.out.print("]");
	}
}

```

### 4 输入矩阵

```java
3 4 
请输入数组元素
1 2 3 4
5 6 7 8
9 10 11 12
```

```java
public class Main {

    public static void main(String arg[]) {
        Scanner s = new Scanner(System.in);
        System.out.println("请输入数组行数和列数");
        int x = s.nextInt();//行数
        int y = s.nextInt();//列数
        int[][] awarry = new int[x][y];
        System.out.println("请输入数组元素");

        for (int i = 0; i < x; i++) {
            for (int j = 0; j < y; j++) {
                awarry[i][j] = s.nextInt();
            }
        }
        System.out.println("你输入的数组为");

        for (int i = 0; i < x; i++) {
            for (int j = 0; j < y; j++) {
                System.out.print(awarry[i][j] + "\t");
            }
            System.out.println();
        }
    }

}
```

### 5 两行输入

**遇到的问题：**在调用了nextInt()后，我们可以先调用一次nextLine(),将该行剩下的内容抛弃；

```java
int option = input.nextInt();
input.nextLine();  // Consume newline left-over
String str1 = input.nextLine();
```

全部都使用nextLine()读入，然后将其读入的数据转换为Integer。

```java
int option = 0;
try {
    option = Integer.parseInt(input.nextLine());
} catch (NumberFormatException e) {
    e.printStackTrace();
}
String str1 = input.nextLine();
```

```java
 public static void main(String arg[]) {
        System.out.println("输出：");
        Scanner sc = new Scanner(System.in);
        int m = Integer.parseInt(sc.nextLine().trim());
        String s = sc.nextLine();
        String[] s1 = s.trim().split(" ");
        int[] num1 = new int[s1.length];

        for(int i = 0; i < s1.length; i ++) {
            num1[i] = Integer.parseInt(s1[i]);
        }
        System.out.println("输出：");
        System.out.println(Arrays.toString(num1));
    }
```

```java
public static void main(String arg[]) {
        System.out.println("输出：");
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        sc.nextLine();//丢弃读取Int的这一行
        String s = sc.nextLine();
        String[] s1 = s.trim().split(" ");
        int[] num1 = new int[s1.length];

        for(int i = 0; i < s1.length; i ++) {
            num1[i] = Integer.parseInt(s1[i]);
        }
        System.out.println("输出：");
        System.out.println(Arrays.toString(num1));
    }
```



## 1.贪心算法

### 1.1 主持人调度（二）

- 描述

  有n个活动即将举办，每个活动都有开始时间和结束时间，第i个活动开始时间是start~i~,第i个活动的结束时间是end~i~,举办某个活动就需要为该活动准备一个活动主持人。

  一个活动主持人在同一时间只能参加一个活动，并且活动主持人需要全程参与活动，换句话说，一个主持人参与了第i个活动，那么该主持人在（start~i~,end~i~）这个时间段不能参加其他任何活动。求成功举办这n个活动，最少需要多少名主持人。

  数据范围：1≤n≤10^5^,-2^32^ <= start~i~ <= end~i~ <= 2^31^-1

  复杂度要求：时间复杂度O(nlogn),空间复杂度O(n)

  ```java
  输入：2,[[1,2],[2,3]]
  返回值：1
  说明：只需要一个主持人就能成功举办这两个活动      
  ```

- 贪心思想

  - 首先建立两个数组分别存储开始时间（记为start）和结束时间（记为end）。
  - 然后分别对start和end数组进行排序。(结束时间依次往后面推)
  - 接着遍历start数组，判断当前开始时间是否大于等于最小的结束时间，如果是，则说明当前主持人就可以搞定（对应当前最小的结束时间的那个活动）；如果否，则需要新增一个主持人，并将end数组下标后移（表示对应的活动已经有人主持）。

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
      /**
       * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
       * 计算成功举办活动需要多少名主持人
       * @param n int整型 有n个活动
       * @param startEnd int整型二维数组 startEnd[i][0]用于表示第i个活动的开始时间，startEnd[i][1]表示第i个活动的结束时间
       * @return int整型
       */
      public int minmumNumberOfHost (int n, int[][] startEnd) {
          //初始化两个数组，分别记录开始时间和结束时间
          int[] start=new int[n];
          int[] end=new int[n];
  
          //将活动的开始和结束时间赋值道start和end数组
          for(int i=0;i<n;i++){
              start[i]=startEnd[i][0];
              end[i]=startEnd[i][1];
          }
  
          //按从小到大的顺序对start和end数组排序
          Arrays.sort(start);
          Arrays.sort(end);
  
          int res=0,index=0;
          for(int i=0;i<n;i++){
              //如果大于等于当前最小的结束时间，说明当前主持人可以搞定
              if(start[i]>=end[index]){
                  index++;
              }
              //否则，需要新增主持人
              else{
                  res++;
              }
          }
  
          return res;
  
      }
  }
  ```

### 1.2 跳跃游戏

- 描述

  给定一个非负整数数组nums，你最初位于数组的第一个下标，数组中的每个元素代表你在该位置可以跳跃的最大长度，判断你是否能够到达最后一个下标。

  ```java
  输入：nums = [2,3,1,1,4]
  输出：true
  解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。	
  
  输入：nums = [3,2,1,0,4]
  输出：false
  解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
  
  ```

- 思路（贪心思想）

  我们可以用贪心的方法解决这个问题。

  设想一下，对于数组中的任意一个位置 y，我们如何判断它是否可以到达？根据题目的描述，只要存在一个位置 xx，它本身可以到达，并且它跳跃的最大长度为 x+nums[x]，这个值大于等于 y，即 x+nums[x]≥y，那么位置 y 也可以到达。

  换句话说，对于每一个可以到达的位置 x，它使得x+1,x+2,⋯,x+nums[x] 这些连续的位置都可以到达。

  这样以来，我们依次遍历数组中的每一个位置，并实时维护 最远可以到达的位置。对于当前遍历到的位置 x，如果它在 最远可以到达的位置 的范围内，那么我们就可以从起点通过若干次跳跃到达该位置，因此我们可以用 x+nums[x] 更新 最远可以到达的位置。

  在遍历的过程中，如果 最远可以到达的位置 大于等于数组中的最后一个位置，那就说明最后一个位置可达，我们就可以直接返回 True 作为答案。反之，如果在遍历结束后，最后一个位置仍然不可达，我们就返回 False 作为答案。

- 代码

  ```java
  public class Solution {
      public boolean canJump(int[] nums) {
          int n = nums.length;
          int rightmost = 0;
          for (int i = 0; i < n; ++i) {
              if (i <= rightmost) {
                  //维护可以跳到的最大位置
                  rightmost = Math.max(rightmost, i + nums[i]);
                  if (rightmost >= n - 1) {
                      return true;
                  }
              }
          }
          return false;
      }
  }
  ```



## 2.链表

![image-20210322165146288](Datastructureandalgorithm.assets/image-20210322165146288.png)

### 2.1 单链表反转

- 链表是真实存在于内存中的，在栈中可以存在多个指向链表的指针，手动将其中的一个指针赋值为null，其他指针依然指向该链表。只有真实地修改了链表的结构，其他指向的链表的全指针才会部发生改变，

```java
 public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode pre = null;//前一个节点
        ListNode cur = head;//当前节点
        ListNode temp = null;//后一个节点
        while(cur != null ){
            temp  = cur.next;//后一个节点赋值
            cur.next = pre;//当前节点的下一个节点指向当前节点的前一个节点
            pre = cur;//前一个节点向后移动，当前节点变为前一个节点
            cur = temp;//当前节点向后移动，后一个节点变为当前节点
        }
        return pre;


    }

```

### 2.2 链表指定区间反转

- 将一个节点数为 size 链表 m 位置到 n 位置之间的区间反转，要求时间复杂度 O(n)*O*(*n*)，空间复杂度 O(1)*O*(1)。
  例如：
  给出的链表为 $1\to 2 \to 3 \to 4 \to 5 \to NULL, m=2,n=4$
  返回 $1\to 4\to 3\to 2\to 5\to NULL$

  数据范围： 链表长度 $0 < size \le 1000，0 < m \le n \le size$，链表中每个节点的值满足 $|val| \le 1000$

  要求：时间复杂度 O*(*n*) ，空间复杂度 O*(n)

  进阶：时间复杂度 O*(*n*)，空间复杂度 O*(1)

```java
public class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode preStart = dummy;
        ListNode start = head;
        for (int i = 1; i < m; i ++ ) {
            preStart = start;
            start = start.next;
        }
        // reverse
        for (int i = 0; i < n - m; i ++ ) {
            ListNode temp = start.next;
            start.next = temp.next;
            temp.next = preStart.next;
            preStart.next = temp;
        }
        return dummy.next;
    }
}
	
```

### 2.3 链表中的节点每K个一组翻转

- 将给出的链表中的节点每 k 个一组翻转，返回翻转后的链表
  如果链表中的节点数不是 k 的倍数，将最后剩下的节点保持原样
  你不能更改节点中的值，只能更改节点本身。

  数据范围： \ 0 \le n \le 2000 0≤*n*≤2000 ， 1 \le k \le 20001≤*k*≤2000 ，链表中每个元素都满足 0 \le val \le 10000≤*v**a**l*≤1000
  要求空间复杂度 O(1)*O*(1)，时间复杂度 O(n)*O*(*n*)

  例如：

  给定的链表是 1\to2\to3\to4\to51→2→3→4→5

  对于 k = 2*k*=2 , 你应该返回 2\to 1\to 4\to 3\to 52→1→4→3→5

  对于 k = 3*k*=3 , 你应该返回 3\to2 \to1 \to 4\to 53→2→1→4→5

```java
public class Solution {
    public static ListNode reverseKGroup(ListNode head, int k) {
		if(head == null || head.next == null || k < 2) return head;
		ListNode dummy = new ListNode(0);
		dummy.next = head;
		ListNode pre = dummy, cur = head, temp;
		int len = 0;
		while (head != null) {
			len ++ ;
			head = head.next;
		}
		for (int i = 0; i < len / k; i ++ ) {
			for (int j = 1; j < k; j ++ ) {
				temp = cur.next;
				cur.next = temp.next;
				temp.next = pre.next;
				pre.next = temp;
			}
			pre = cur;
			cur = cur.next;
		}
		return dummy.next;
	}
}
```

### 2.4 合并两个有序链表

- 输入两个递增的链表，单个链表的长度为n，合并这两个链表并使新链表中的节点仍然是递增排序的。

  数据范围： 0 \le n \le 10000≤*n*≤1000，-1000 \le 节点值 \le 1000−1000≤节点值≤1000
  要求：空间复杂度 O(1)*O*(1)，时间复杂度 O(n)*O*(*n*)

  如输入{1,3,5},{2,4,6}时，合并后的链表为{1,2,3,4,5,6}，所以对应的输出为{1,2,3,4,5,6}

- 普通思路（一个链表依次添加）

```java
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        ListNode res = new ListNode(0);
        ListNode head = res;
        while(list1 != null && list2 != null){
            if(list1.val < list2.val){
                res.next = list1;
                list1 = list1.next;
            }else{
                res.next = list2;
                list2 = list2.next;
            }
            res = res.next;  
        }
        if(list1 == null && list2 !=null){
            res.next = list2;
        }else if(list1 != null && list2 ==null){
            res.next = list1;
        }
        return head.next;
    }
}
```

- 递归法：

```java
     //合并两个有序链表（和力扣的21题一样）
    public ListNode merge(ListNode l1,ListNode l2){
        if(l1==null)return l2;
        if(l2==null) return l1;
        if(l1.val<l2.val) {
            l1.next=merge(l1.next,l2);
            return l1;
        }else{
            l2.next=merge(l1,l2.next);
            return l2;
        }
    }
```

### 2.5 合并K组有序链表（分而治之）

- 合并 k 个升序的链表并将结果作为一个升序的链表返回其头节点。

  输入：

  [{1,2,3},{4,5,6,7}]

  返回值：

  {1,2,3,4,5,6,7}

```java
public class Solution {
        //合并K个有序链表的方法
    public ListNode mergeKLists(ArrayList<ListNode> lists) {
        return mergeList(lists,0,lists.size()-1);
    }
    public ListNode mergeList(ArrayList<ListNode> lists,int left,int right){
        if(left==right) return lists.get(left);
        if(left>right) return null;
        int mid=left+(right-left)/2;
        return merge(mergeList(lists,left,mid),mergeList(lists,mid+1,right));
    }
        //合并两个有序链表（和力扣的21题一样）
    public ListNode merge(ListNode l1,ListNode l2){
        if(l1==null)return l2;
        if(l2==null) return l1;
        if(l1.val<l2.val) {
            l1.next=merge(l1.next,l2);
            return l1;
        }else{
            l2.next=merge(l1,l2.next);
            return l2;
        }
    }
}

```

### 2.6 快慢指针链表有环

- 自己的：

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null || head.next == null) return false;
        ListNode slow = head , fast = head.next;
        while(slow != null && fast != null){
            if(slow==fast) return true;
            slow = slow.next;
            if(fast.next == null) return false;
            fast = fast.next.next;
        }
        return false;
    }
}
```

- 别人的：

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null)
            return false;
        ListNode fast=head;
        ListNode slow=head;
        while(fast!=null&&fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
            if(fast==slow)
                return true;
        }
        return false; 
    }
}

```

### 2.7 环形链表的入口节点

- Hash表法

```java
public ListNode EntryNodeOfLoop(ListNode pHead) {
        // 使用set来记录出现的结点
        HashSet<ListNode> set = new HashSet<>();
        while(pHead != null){
           // 当set中包含结点，说明第一次出现重复的结点，即环的入口结点
            if(set.contains(pHead)){
                return pHead;
            }
            // set中加入未重复的结点
            set.add(pHead);
            pHead = pHead.next;
        }
        return null;
    }
```

- 公式推导

![环形入口节点](Datastructureandalgorithm.assets/环形入口节点.png)



```java
public ListNode EntryNodeOfLoop(ListNode pHead) {
        if(pHead == null) return null;
        // 定义快慢指针
        ListNode slow = pHead;
        ListNode fast = pHead;
        while(fast != null && fast.next != null){
            // 快指针是满指针的两倍速度
            fast = fast.next.next;
            slow = slow.next;
            // 记录快慢指针第一次相遇的结点
            if(slow == fast) break;
        }
        // 若是快指针指向null，则不存在环
        if(fast == null || fast.next == null) return null;
        // 重新指向链表头部
        fast = pHead;
        // 与第一次相遇的结点相同速度出发，相遇结点为入口结点
        while(fast != slow){
            fast = fast.next;
            slow = slow.next;
        }
        return fast;
    }
```

### 2.8 链表中倒数最后K个节点

- 输入一个长度为 n 的链表，设链表中的元素的值为 ai ，返回该链表中倒数第k个节点。

  如果该链表长度小于k，请返回一个长度为 0 的链表。

  数据范围：0 \leq n \leq 10^50≤*n*≤105，0 \leq a_i \leq 10^90≤*a**i*≤109，0 \leq k \leq 10^90≤*k*≤109

  要求：空间复杂度 O(n)*O*(*n*)，时间复杂度 O(n)*O*(*n*)

  进阶：空间复杂度 O(1)*O*(1)，时间复杂度 O(n)*O*(*n*)

  例如输入{1,2,3,4,5},2时，对应的链表结构如下图所示：

  ![5407F55227804F31F5C5D73558596F2C](Datastructureandalgorithm.assets/5407F55227804F31F5C5D73558596F2C.png)

  其中蓝色部分为该链表的最后2个结点，所以返回倒数第2个结点（也即结点值为4的结点）即可，系统会打印后面所有的节点来比较。

- 快慢指针法

  ![B27699765EEF6CA0E75AF0D1A4B9BCAC](Datastructureandalgorithm.assets/B27699765EEF6CA0E75AF0D1A4B9BCAC.png)

```java
 public ListNode FindKthToTail (ListNode pHead, int k) {
        // write code here
        if(pHead == null || k ==0) return null;
         ListNode slow = pHead , fast = pHead;
        for(int i = 1 ; i < k ; i++){
            if(fast.next == null) return null; 
            fast = fast.next;
        }
        while(fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
        
    }
```

- 先全部入栈
- 出栈前面K个元素

![C9E011A3DA1FB56916001C45812DEAA7](Datastructureandalgorithm.assets/C9E011A3DA1FB56916001C45812DEAA7.png)

```java
 public ListNode FindKthToTail (ListNode pHead, int k) {
        // write code here
       if(pHead == null || k == 0) return null;
        Stack<ListNode> stack = new Stack();
        while(pHead != null){
            stack.push(pHead);
            pHead = pHead.next;
        }
        ListNode res = null;
        if(stack.size() < k) return null;
        for(int i = 0 ; i < k ; i++){
           ListNode temp =  stack.pop();
            temp.next = res;
            res = temp;
        }
        return res;
 }
```

### 2.9 删除链表倒数第N个节点

```java
 public ListNode removeNthFromEnd (ListNode head, int n) {
        ListNode temp = head;
        if(head == null || n == 0) return head;
        Stack<ListNode> stack = new Stack<>();
        while(temp != null){
            stack.push(temp);
            temp = temp.next;
        }
        if(stack.size() < n) return head;
        if(n==stack.size()) {
            ListNode res = head.next;
            head.next = null;
            return res;
        }
        ListNode pre = null , cur = null;
        for(int i = 0 ; i < n + 1 ; i++){
            cur = pre;
            pre = stack.pop();
        }
        pre.next = cur.next;
        cur.next = null;
        return head;
    }
```

### 2.10 两个链表的第一个公共节点

![img](Datastructureandalgorithm.assets/394BB7AFD5CEA3DC64D610F62E6647A6.png)

```java
示例1：
输入：
{1,2,3},{4,5},{6,7}
复制
返回值：
{6,7}
复制
说明：
第一个参数{1,2,3}代表是第一个链表非公共部分，第二个参数{4,5}代表是第二个链表非公共部分，最后的{6,7}表示的是2个链表的公共部分
这3个参数最后在后台会组装成为2个两个无环的单链表，且是有公共节点的    
如果没有公共节点，返回null
```

### 2.11 链表相加

例如：链表 1 为 9->3->7，链表 2 为 6->3，最后生成新的结果链表为 1->0->0->0。

![img](Datastructureandalgorithm.assets/C2DB572B01B0FDC03C097BE7ABA45114.png)

完整代码：

```java
import java.util.*;
public class Solution {
    public ListNode addInList (ListNode head1, ListNode head2) {
        // 进行判空处理
        if(head1 == null)
            return head2;
        if(head2 == null){
            return head1;
        }
        // 反转h1链表
        head1 = reverse(head1);
        // 反转h2链表
        head2 = reverse(head2);
        // 创建新的链表头节点
        ListNode head = new ListNode(-1);
        ListNode nHead = head;
        // 记录进位的数值
        int tmp = 0;
        while(head1 != null || head2 != null){
            // val用来累加此时的数值（加数+加数+上一位的进位=当前总的数值）
            int val = tmp;
            // 当节点不为空的时候，则需要加上当前节点的值
            if (head1 != null) {
                val += head1.val;
                head1 = head1.next;
            }
            // 当节点不为空的时候，则需要加上当前节点的值
            if (head2 != null) {
                val += head2.val;
                head2 = head2.next;
            }
            // 求出进位
            tmp = val/10;
            // 进位后剩下的数值即为当前节点的数值
            nHead.next = new ListNode(val%10);
            // 下一个节点
            nHead = nHead.next;
 
        }
        // 最后当两条链表都加完的时候，进位不为0的时候，则需要再加上这个进位
        if(tmp > 0){
            nHead.next = new ListNode(tmp);
        }
        // 重新反转回来返回
        return reverse(head.next);
    }

    // 反转链表
    ListNode reverse(ListNode head){
        if(head == null)
            return head;
        ListNode cur = head;
        ListNode node = null;
        while(cur != null){
            ListNode tail = cur.next;
            cur.next = node;
            node = cur;
            cur = tail;
        }
        return node;
    }
}
```

### 2.12 单链表的排序

解题思路：主要通过递归实现链表归并排序，有以下两个环节：

1、分割 cut 环节： 找到当前链表中点，并从中点将链表断开（以便在下次递归 cut 时，链表片段拥有正确边界）； 使用 fast,slow 快慢双指针法，奇数个节点找到中点，偶数个节点找到中心左边的节点。找到中点 slow 后，执行 `slow.next = null` 将链表切断。递归分割时，输入当前链表左端点 head 和中心节点 slow 的下一个节点 tmp(因为链表是从 slow 切断的)。  cut 递归终止条件： 当head.next == None时，说明只有一个节点了，直接返回此节点

2、合并 merge 环节： 将两个排序链表合并，转化为一个排序链表。双指针法合并，建立辅助ListNode h 作为头部。设置两指针 left, right 分别指向两链表头部，比较两指针处节点值大小，由小到大加入合并链表头部，指针交替前进，直至添加完两个链表。返回辅助ListNode h 作为头部的下个节点 h.next。时间复杂度O(NlogN)：N表示链表结点数量，二分归并算法O(NlogN) ,空间复杂度O(1)：仅使用常数级变量空间		3、特殊情况，当题目输入的 head == null 时，直接返回null。

**图解：**

![img](Datastructureandalgorithm.assets/A42227C97389C374618E9F1DAFA2A2F2.png)

```java
import java.util.*;
public class Solution {
    public ListNode sortInList (ListNode head) {
        // write code here
        if (head == null || head.next == null)
            return head;
        // 使用快慢指针寻找链表的中点
        ListNode fast = head.next, slow = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode tmp = slow.next;
        slow.next = null;
        // 递归左右两边进行排序
        ListNode left = sortInList(head);
        ListNode right = sortInList(tmp);
        // 创建新的链表
        ListNode h = new ListNode(0);
        ListNode res = h;
        // 合并 left right两个链表
        while (left != null && right != null) {
            // left  right链表循环对比
            if (left.val < right.val) {
                h.next = left;
                left = left.next;
            } else {
                h.next = right;
                right = right.next;
            }
            h = h.next;
        }
        // 最后添加未对比的链表部分判断左链表是否为空
        h.next = left != null ? left : right;
        return res.next;
    }
}
```

### 2.13 判断链表是否是回文结构

```java
输入：
{1,2,2,1}
返回值：
true
说明：
1->2->2->1
```

思路：链表入栈，`while(stack.pop().val == head.val)`一直出栈，奇数个链表退出条件：`if(head == last ) return true;`,偶数个链表退出条件：`if(temp2 == head && temp1 == last ) return true;`

完整AC代码:

```java
import java.util.*;
public class Solution {
    public boolean isPail (ListNode head) {
      Stack<ListNode> stack = new Stack();
        if(head == null) return false;
        if(head.next == null) return true;
        ListNode temp = head;
        while(temp != null){
            stack.push(temp);
            temp = temp.next;
        }
        ListNode last = stack.pop();
        ListNode temp1 = head , temp2 = last;
        while(last.val == head.val){
            temp1 = head;
            temp2 = last;
            head = head.next;
            last = stack.pop();
            if(head == last ) return true;
            if(temp2 == head && temp1 == last ) return true;
        }
        return false;
    }
    
}
```

### 2.14 链表的奇偶重排

- 描述：给定一个单链表，请设定一个函数，将链表的奇数位节点和偶数位节点分别放在一起，重排后输出，注意是节点的编号而非节点的数值。

```java
输入：
{1,4,6,3,7}
返回值：
{1,6,7,4,3}
说明：
1->4->6->3->7->NULL
重排后为
1->6->7->4->3->NULL
奇数位节点有1,6,7，偶数位节点有4,3。重排后为1,6,7,4,3
```



- ==**思路**==：从头结点依次`head = head.next`扫描,设置标志位`flag`,将奇数和偶数分别存放在两条链表里，注意记录奇数链表的最后一个奇数位置，`temp1.next = temp22.next`合并奇数和偶数链表。

```java
import java.util.*;
public class Solution {
    public ListNode oddEvenList (ListNode head) {
        ListNode temp1 = new ListNode(0),temp2 = new ListNode(0) , temp11 = temp1 , temp22 = temp2;
        boolean flag = true;//奇数为true
        while(head != null){
            if(flag){
                temp1.next = head;
                head = head.next;
                temp1.next.next = null;
                temp1 = temp1.next;
                flag = !flag;
            }else{
                temp2.next = head;
                head = head.next;
                temp2.next.next = null;
                temp2 = temp2.next;
                flag = !flag;  
            }
        }
        temp1.next = temp22.next;//奇数尾部与偶数头部合并
        return temp11.next;
    }
}
```



### 2.15 删除有序链表重复的元素I

删除给出链表中的重复元素（链表中元素从小到大有序），使链表中的所有元素都只出现一次
例如：
给出的链表为1→1→2,返回1→2.
给出的链表为1→1→2→3→3,返回1→2→3.

==**操作原始链表**==

```java
import java.util.*;
public class Solution {
    public ListNode deleteDuplicates (ListNode head) {

        if(head == null || head.next ==null) return head;
        int lastNum = -1;
         ListNode res = head ,cur = head;
        while(head != null){
            if(lastNum  != head.val){//如果不重复
                lastNum =head.val;//更新重复值
                cur = head;//cur移到head位置
            }else{
               cur.next=head.next;//依次往后遍历，如果与前一个节点值重复，当前节点下一个节点指向重复节点的下一个节点
            }
            head = head.next;//head后移
        }
        
       return res;
        
    }
}
```

- ==**栈思路**==：依次入栈，遇到重复元素跳过，反向输出连接栈输出的节点

```java
import java.util.*;
public class Solution {
    public ListNode deleteDuplicates (ListNode head) {

        if(head == null || head.next ==null) return head;
        int lastNum = -1;
         Stack<ListNode> stack = new Stack();
        while(head != null){
            if(lastNum != head.val){
                lastNum = head.val;
                stack.push(head);
                head = head.next; 
            }else{
                head = head.next;
                continue;
            }
        }
        ListNode res = null , cur = null;
        while(stack.size() != 0){
           cur = stack.pop();
           cur.next = res;
           res = cur;
        }
        return res;
    }
}
```



### 2.16 删除有序链表重复元素II

给出一个升序排序的链表，删除链表中的所有重复出现的元素，只保留原链表中只出现一次的元素。
例如：
给出的链表为1→2→3→3→4→4→5, 返回1→2→5.
给出的链表为1→1→1→2→3, 返回2→3.

- ==**栈思路**==：维护一个数字`lastNum`，用来判别重复，如果当前`head.val != lastNum` , 那么将链表入栈并更新`lastNum数值`，如果`head.next.val == lastNum`，就	`stack.pop()`一个数，并且设置标志位为`false`，后面再有重复的数，就`continue`跳过，依次遍历到结尾。最后依次`stack.pop()`节点，反向连接即可。

```java
import java.util.*;
public class Solution {
    public ListNode deleteDuplicates (ListNode head) {
        if(head == null || head.next ==null) return head;
        int lastNum = -1 ; 
        boolean flag = false;
        Stack<ListNode> stack = new Stack();
        while(head != null){
            if(lastNum != head.val){
                lastNum = head.val;
                stack.push(head);
                head = head.next;
                flag = true;
            }else{
                if(flag){
                     stack.pop();
                     flag = false; 
                    head = head.next;
                }else{
                    head = head.next;
                    continue;
                }
               
            }
             
        }
        ListNode res = null , cur = null;
        while(stack.size() != 0){
           cur = stack.pop();
           cur.next = res;
           res = cur;
        }
        return res;
    }
         
}
```

### 2.17 删除无序链表中值重复出现的节点

给定一个无序链表，删除其中值重复出现的节点(保留当中顺序遍历第一个出现的节点)。

- 输入描述:

```
第一行一个整数 n，表示单链表的节点数量。
第二行 n 个整数表示单链表的节点的值。
```

- 输出描述:

```
顺序输出单链表每个节点的值。
```

- 输入

```
5
1 3 2 3 1
```

- 输出

```
1 3 2
```

- 思路：不考虑空间复杂度的话还是比较容易实现O(n)时间复杂度的，直接重构一个链表就行： 遍历原始链表，并用一个集合记录已经出现过的节点值，如果当前值已经出现过，就直接跳过，否则创建一个新的节点追加在当前链表的后面。

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.HashSet;

class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine().trim());
        String[] strList = br.readLine().trim().split(" ");
        ListNode head = new ListNode(Integer.parseInt(strList[0]));
        ListNode cur = head;
        for(int i = 1; i < n; i++){
            cur.next = new ListNode(Integer.parseInt(strList[i]));
            cur = cur.next;
        }
        head = removeDuplicates(head, n);
        while(head != null){
            System.out.print(head.val + " ");
            head = head.next;
        }
    }
    
    private static ListNode removeDuplicates(ListNode head, int len) {
        ListNode cur = head;
        HashSet<Integer> set = new HashSet<>();
        ListNode newHead = new ListNode(head.val);
        ListNode newCur = newHead;
        while(cur != null){
            if(!set.contains(cur.val)){//这里会直接加入链表头部，造成head重复
                set.add(cur.val);
                newCur.next = new ListNode(cur.val);
                newCur = newCur.next;
            }
            cur = cur.next;
        }
        return newHead.next;     // 注意头结点重复了一次，直接跳过
    }
}
```

### 2.18 删除链表中指定值的节点

给出一个链表和一个整数 num，输出删除链表中节点值等于 num 的节点之后的节点。

```java
第一行一个整数 n，n 表示单链表的节点数量。
第二行 n 个整数表示单链表的各个节点的值。
第三行一个整数 num。
输入：
4 
1 2 3 4
3
输出：
1 2 4
```

```java
class ListNode{
    int val;
    ListNode next;
    ListNode(int val){
        this.val=val;
    }
}
 
public class Main{
 
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int[] a=new int[n];
        for(int i=0;i<n;i++){
            a[i]=sc.nextInt();
        }
        ListNode head=new ListNode(a[0]);
        ListNode cur=head;
        for(int i=1;i<n;i++){
            cur.next=new ListNode(a[i]);
            cur=cur.next;
        }
        cur.next=null;
        int val=sc.nextInt();
        ListNode node=removeElements(head,val);
        printList(node);
    }
    public static void printList(ListNode head){
        while(head!=null){
            System.out.print(head.val+" ");
            head=head.next;
        }
    }
    
    //核心方法
    public static ListNode removeElements(ListNode head,int val){
        if(head == null ) return head;
         ListNode res = head ,cur = head;
        while(head != null){
            if(val  != head.val){//如果不重复
                cur = head;//cur移到head位置
            }else{
               cur.next=head.next;//依次往后遍历，如果与前一个节点值重复，当前节点下一个节点指向重复节点的下一个节点（删除操作）
            }
            head = head.next;//head后移
        }
        
       return res;
    }
}
```



### 2.19 逆序打印单链表

- 创建一个栈，将各结点压入栈，先进后出
- 遍历这个栈然后输出

```java
public static void reversePrint(HeroNode head) {
    if (head.next == null || head.next.next == null) {
        return;
    }
    //创建一个栈，将各结点压入栈，先进后出
    Stack<HeroNode> stack = new Stack<HeroNode>();
    HeroNode cur = head.next;
    while (cur != null) {
        stack.push(cur);    //相当于add
        cur = cur.next;
    }

    while (stack.size() > 0) {
        System.out.println(stack.pop());    //重写了toString方法
    }
}
```





## 3.堆/栈/队列

### 3.1数组模拟栈

```java
class ArrayStack {
    private int maxSize;
    private int[] stack;
    private int top = -1;   //栈顶

    public ArrayStack(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    //栈满
    public boolean isFull() {
        return top == maxSize - 1;
    }

    //栈空
    public boolean isEmpty() {
        return top == -1;
    }

    //入栈
    public void push(int value) {
        if (isFull()) {
            System.out.println("栈满");
            return;
        }
        top++;
        stack[top] = value;
    }

    //出栈
    public int pop() {
        if (isEmpty()) {
            throw new RuntimeException("栈空");
        }
        int value = stack[top];
        top--;
        return value;
    }

    //遍历栈(从栈顶开始显示数据)
    public void list() {
        if (isEmpty()) {
            System.out.println("栈空");
            return;
        }
        for (int i = top; i >= 0; i--) {
            System.out.printf("stack[%d]=%d\n", i, stack[i]);
        }
    }
}
```

### 3.2栈实现中缀表达式计算器

- Stack类继承于Vector类，Vector：作为List接口的古老实现类；线程安全的，效率低；底层使用Object[] elementData存储。

- 中缀表达式：即常见的表达式：3+2*6-2

- 思路：

  1. 将String类型的字符串表达式分隔开存入一个List（多位数用String.match(正则表达式)）

  2. 创建一个数栈和符号栈，遍历这个List

  3. 发现数字直接入数栈

  4. 发现符号分两种情况：

     若当前符号栈为空或当前操作符大于栈顶操作符的优先级，直接入栈

     若当前操作符小于或等于栈顶操作符的优先级，从数栈pop出两个数，从符号栈pop出一个符号，进行计算，结果入数栈，再将当前操作符入符号栈（栈顶元素-或/次顶元素）。

  5. 当表达式遍历完，顺序从数栈或者符号栈取出数和符号计算，结果入数栈，最后得到结果

```java
public class Calculator {
    public static void main(String[] args) {
        String expression = "30+2*6-2";

        //一个数字栈，一个符号栈
        ArrayStack numStack = new ArrayStack(10);
        ArrayStack operStack = new ArrayStack(10);
        //定义需要的相关变量
        int index = 0;  //用于扫描
        int num1 = 0;
        int num2 = 0;
        int oper = 0;
        int res = 0;
        char ch = ' ';  //将每次扫描得到的char保存到ch
        String keepNum = "";    //用于拼接多位数

        while (true) {
            ch = expression.substring(index, index + 1).charAt(0);
            if (operStack.isOper(ch)) {     //如果是是运算符
                if (!operStack.isEmpty()) {  //符号栈不为空
                    //当前操作符优先级小于或者等于栈中的，需要从数字栈pop出两个数
                    //再从符号栈中pop出一个符号，进行计算，结果入数字栈，然后将当前操作符入栈
                    if (operStack.Priority(ch) <= operStack.Priority(operStack.peek())) {
                        num1 = numStack.pop();
                        num2 = numStack.pop();
                        oper = operStack.pop();
                        res = numStack.cal(num1, num2, oper);
                        numStack.push(res);
                        operStack.push(ch);
                    } else {
                        //当前操作符优先级大于栈中的，直接入符号栈
                        operStack.push(ch);
                    }
                } else {                    //符号栈为空直接入栈
                    operStack.push(ch);
                }
            } else {
                //如果是数，判断是否是多位数
                //需要向后再看
                //需要定义一个字符串变量用于拼接
                keepNum += ch;

                //当ch是最后一位直接入栈
                if (index == expression.length() - 1) {
                    numStack.push(ch - 48);
                }else {
                    //多次拼接多位数的index++在while外
                    if (operStack.isOper(expression.substring(index + 1, index + 2).charAt(0))) {
                        //如果后一位是符号，入栈
                        numStack.push(Integer.parseInt(keepNum));
                        keepNum = "";   //keepNum清空
                    }
                }

            }
            //让index+1，并判断是否到expression的最后
            index++;
            if (index >= expression.length()) {
                break;
            }
        }

        //扫描完毕后，就顺序的从数字栈和符号栈pop出相应的数和符号，并运行
        while (true) {
            //当符号栈为空，数字栈只有一个数字（结果）
            if (operStack.isEmpty()) {
                break;
            }
            num1 = numStack.pop();
            num2 = numStack.pop();
            oper = operStack.pop();
            res = numStack.cal(num1, num2, oper);
            numStack.push(res);
        }

        System.out.printf("表达式%s = %d", expression, numStack.pop());
    }

}

class ArrayStack {
    private int maxSize;
    private int[] stack;
    private int top = -1;   //栈顶

    public ArrayStack(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    //栈满
    public boolean isFull() {
        return top == maxSize - 1;
    }

    //栈空
    public boolean isEmpty() {
        return top == -1;
    }

    //入栈
    public void push(int value) {
        if (isFull()) {
            System.out.println("栈满");
            return;
        }
        top++;
        stack[top] = value;
    }

    //出栈
    public int pop() {
        if (isEmpty()) {
            throw new RuntimeException("栈空");
        }
        int value = stack[top];
        top--;
        return value;
    }

    //遍历栈(从栈顶开始显示数据)
    public void list() {
        if (isEmpty()) {
            System.out.println("栈空");
            return;
        }
        for (int i = top; i >= 0; i--) {
            System.out.printf("stack[%d]=%d\n", i, stack[i]);
        }
    }

    //返回运算符的优先级，优先级使用数字表示
    //数字越大，优先级越高
    public int Priority(int oper) {
        if (oper == '*' || oper == '/') {
            return 1;
        } else if (oper == '+' || oper == '-') {
            return 0;
        } else {
            return -1;
        }
    }

    //判断是不是运算符
    public boolean isOper(char val) {
        return val == '+' || val == '-' || val == '*' || val == '/';
    }

    //计算方法
    public int cal(int num1, int num2, int oper) {
        int res = 0;
        switch (oper) {
            case '+':
                res = num1 + num2;
                break;
            case '-':
                res = num2 - num1;
                break;
            case '*':
                res = num1 * num2;
                break;
            case '/':
                res = num2 / num1;
                break;
        }
        return res;
    }

    //看一眼栈顶的值，不弹出
    public int peek() {
        return stack[top];
    }
}
```

### 3.2栈实现逆波兰计算器

- 前缀表达式：又称**波兰式**，前缀表达式的运算符位于操作数之前，(3+4)×5-6 对应的前缀表达式就是 - × + 3 4 5 6
- 计算器求值方式：**从右至左**扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个数，用运算符对它们做相应的计算（栈顶元素 和 次顶元素），并将结果入栈；重复上述过程直到表达式最左端，最后运算得出的值即为表达式的结果（栈顶元素-或/次顶元素）
- 后缀表达式：又称**逆波兰表达式**,与前缀表达式相似，只是运算符位于操作数之后， (3+4)×5-6 对应的后缀表达式就是 3 4 + 5 × 6 –
- 计算器求值方式：**从左至右**扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个数，用运算符对它们做相应的计算（次顶元素 和 栈顶元素），并将结果入栈；重复上述过程直到表达式最右端，最后运算得出的值即为表达式的结果（次顶元素-或/栈顶元素）



```java
public static void main(String[] args) {
    //"3 4 + 5 * 6"  =  (3+4)*5-6
    String suffixExpression = "3 4 + 5 * 20 -";

    List<String> rpnList = getListString(suffixExpression);
    System.out.println("rpnList=" + rpnList);

    System.out.println(calculate(rpnList));
}

//将suffixExpression按空格分割存入数组
public static List<String> getListString(String suffixExpression) {
    String[] split = suffixExpression.split(" ");
    List<String> list = new ArrayList<String>();
    for (String ele : split) {
        list.add(ele);
    }
    return list;

}

public static int calculate(List<String> ls) {
    //创建一个栈
    Stack<String> stack = new Stack<String>();
    //遍历ls
    for (String item : ls) {
        //使用正则表达式取出数
        if (item.matches("\\d+")) { //匹配的是多位数
            stack.push(item);
        } else {
            //pop出两位数，运算并入栈
            int num2 = Integer.parseInt(stack.pop());
            int num1 = Integer.parseInt(stack.pop());
            int res = 0;
            if (item.equals("+")) {
                res = num1 + num2;
            } else if (item.equals("-")) {
                res = num1 - num2;
            } else if (item.equals("*")) {
                res = num1 * num2;
            } else if (item.equals("/")) {
                res = num1 / num2;
            }
            stack.push(String.valueOf(res));
            //stack.push(res + "");
        }
    }

    //最后留在里面的就是结果
    return Integer.parseInt(stack.pop());
}
```

### 3.4中缀表达式转后缀表达式

1. 初始化两个栈，运算符栈s1与储存中间结果的栈s2

2. 从左到右扫描中缀表达式

3. 遇到操作数压s2

4. 遇到运算符，比较其与s1栈顶的运算符的优先级：

   若s1为空或者栈顶为"(",直接入栈

   若优先级比栈顶运算符高，直接入栈

   否则，将s1栈顶的运算符弹出压入到s2，再次重复与s1栈顶的比较操作

5. 遇到括号：

   左括号"("直接压入s1

   右括号")"时，依次弹出s1的运算符并压入s2，直到遇到左括号，将这对括号舍弃

6. 扫描完毕后，将s1中剩余的运算符依次弹出并压入s2

7. 依次弹出s2的元素，结果的逆序即为对应的后缀表达式

如将  **"1+((2+3)*4)-5"**  转化为  **"1 2 3 + 4 * + 5 -"**

```java
public class InvPolandNotation {
    public static void main(String[] args) {
        String str = "1+((2+3)*4)-5";
        List<String> list = getList(str);
        System.out.println(list);
        String trans = trans(list);
        System.out.println(trans);
    }

    //将中缀表达式转化为List储存(包含多位数)
    public static List<String> getList(String str){
        String numKeep = "";
        List<String> list = new ArrayList<>();
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) < 48 || str.charAt(i) > 57) {
                list.add("" + str.charAt(i));
            } else {
                while (i < str.length() && (str.charAt(i) >= 48 && str.charAt(i) <= 57)) {
                    numKeep = numKeep + str.substring(i, i + 1);
                    i++;
                }
                list.add(numKeep);
                numKeep = "";
                i--;    //重要
            }
        }
        return list;
    }

    public static String trans(List<String> list) {
        Stack<String> s1 = new Stack<>();
        Stack<String> s2 = new Stack<>();
        String invPolandNotation = "";
        for (String str : list) {
            if (str.equals("+") || str.equals("-") || str.equals("*") || str.equals("/")) {
                while (!(s1.isEmpty()) && !(s1.peek().equals("(")) && !(priority(str) > priority(s1.peek()))) {
                    s2.push(s1.pop());
                }
                s1.push(str);
            } else if (str.equals("(")) {
                s1.push(str);
            } else if (str.equals(")")) {
                while (!(s1.peek().equals("("))) {
                    s2.push(s1.pop());
                }
                s1.pop();
            } else {
                s2.push(str);
            }
        }

        while (!s1.isEmpty())
            s2.push(s1.pop());

        //反转
        while (!s2.empty()) {
            s1.push(s2.pop());
        }

        while (!s1.empty()) {
            invPolandNotation += s1.pop();
            invPolandNotation += " ";
        }

        int length = invPolandNotation.length();
        invPolandNotation = invPolandNotation.substring(0, length - 2);
        return invPolandNotation;
    }

    //返回运算符的优先级，优先级使用数字表示
    //数字越大，优先级越高
    public static int priority(String oper) {
        if (oper == "*" || oper == "/") {
            return 1;
        } else if (oper == "+" || oper == "-") {
            return 0;
        } else {
            return -1;
        }
    }
}
```

完整的逆波兰计算器包括：

1. 支持+-*/()
2. 支持多位数、小数
3. 过滤任何空白字符，包括换行符，制表符等等

### 3.5 用两个栈实现队列

思路：

- 入队：将元素进栈A；
- 出队：判断栈B是否为空，如果为空，则将栈A中所有元素pop，并push进栈B，栈B出栈；如果不为空，栈B直接出栈。
- 不用管push，队列push的元素，最后才pop出去

```java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }
    
    public int pop() {
        if(stack2.size() <= 0){
            while(stack1.size()!= 0){
                stack2.push(stack1.pop());
             }
        }
        
        return stack2.pop();
    }
}
```

### 3.6 用两个队列实现栈

- 问题描述

  请你仅使用两个队列实现一个后入先出的栈，并支持普通栈的全部四种操作（push、top、pop 和 empty），输入数据保证 pop、top函数操作时，栈中一定有元素。 

```java
void push(int element) 将元素 element 压入栈顶。 
int pop() 移除并返回栈顶元素。 
int top() 返回栈顶元素。 
bool empty() 如果栈是空的，返回 true ；否则，返回 false 
输入:    ["MTY","PSH1","TOP","MTY"]
输出:    ["true","1","false"]
解析:
"MTY"表示当前栈是不是为空=>当前为空，返回"true"
"PSH1"表示将1压入栈中，栈中元素为1
"TOP"表示获取栈顶元素==>返回"1"
"MTY"表示当前栈是不是为空=>当前不为空，返回"false"
```

- 思路：
  为了满足栈的特性，即最后入栈的元素最先出栈，在使用队列实现栈时，应满足队列前端的元素是最后入栈的元素。可以使用两个队列实现栈的操作，其中 queue1用于存储栈内的元素，queue2 作为入栈操作的辅助队列。入栈操作时，首先将元素入队到 queue2，然后将queue1 的全部元素依次出队并入队到 queue2 ，此时 queue2 的前端的元素即为新入栈的元素，再将 queue1 和 queue2互换，则queue1的元素即为栈内的元素，queue1 的前端和后端分别对应栈顶和栈底。由于每次入栈操作都确保queue1  的前端元素为栈顶元素，因此出栈操作和获得栈顶元素操作都可以简单实现。出栈操作只需要移除queue1 的前端元素并返回即可，获得栈顶元素操作只需要获得 queue1 的前端元素并返回即可（不移除元素）。由于 queue1 用于存储栈内的元素，判断栈是否为空时，只需要判断 queue1  是否为空即可。

![fig1](Datastructureandalgorithm.assets/225_fig1-165478397283815.gif)

- 代码

```java
import java.util.*;
class MyStack {
    Queue<Integer> queue1;
    Queue<Integer> queue2;

    public MyStack() {
        queue1 = new LinkedList<Integer>();
        queue2 = new LinkedList<Integer>();
    }
    
    public void push(int x) {
        queue2.offer(x);
        while (!queue1.isEmpty()) {
            queue2.offer(queue1.poll());
        }
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }
    
    public int pop() {
        return queue1.poll();
    }
    
    public int top() {
        return queue1.peek();
    }
    
    public boolean empty() {
        return queue1.isEmpty();
    }
}
```

### 3.7 包含min函数的栈

- 问题描述：定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的 min 函数，输入操作时保证 pop、top 和 min 函数操作时，栈中一定有元素。此栈包含的方法有：

```java
push(value):将value压入栈中
pop():弹出栈顶元素
top():获取栈顶元素
min():获取栈中最小元素
```

- 思路

我们都知道栈结构的push、pop、top操作都是O(1)O(1)*O*(1)，但是`min`函数做不到，于是想到在push的时候就将最小值记录下来，由于栈先进后出的特殊性，我们可以构造一个单调栈，保证栈内元素都是递增的，栈顶元素就是当前最小的元素。此外主栈pop的时候，辅助栈也需要相应的pop。

![图片说明](Datastructureandalgorithm.assets/BF24FE790ACB10342DE5628AEC3283ED.gif)

- 代码

```java
import java.util.Stack;
public class Solution {
    Stack<Integer> stack1 = new Stack();
    Stack<Integer> stack2 = new Stack();
    public void push(int node) {
        stack1.push(node);
        if(stack2.isEmpty() || stack2.peek() > node){
            stack2.push(node);
        }else{
            stack2.push(stack2.peek());
        }
    }
    public void pop() {
        stack1.pop();
        stack2.pop();
    }
    public int top() {
        return stack1.peek();
    }
    public int min() {
        return stack2.peek();
    }
}
```

### 3.8 最小的K个数

- 问题描述

  给定一个长度为 n 的可能有重复值的数组，找出其中不去重的最小的 k 个数。例如数组元素是4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4(任意顺序皆可)。

- 示例

```java
输入：[4,5,1,6,2,7,3,8],4 
输出：[1,2,3,4]
```

- 思路

  建立一个容量为k的大顶堆（堆顶存放堆中的最大的元素）的优先队列。遍历一遍元素，如果堆中元素个数<k,就直接入堆，否则，让当前元素与堆顶元素相比，如果堆顶元素大，则堆顶元素出队，将当前元素入堆

- 代码

```java
import java.util.*;

public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList();
        if(input.length < k || k == 0) return res;
        Queue<Integer> queue = new PriorityQueue<>(k ,new Comparator<Integer>(){
            public int compare(Integer o1 , Integer o2){
                return o2 -o1;
            }
        });
        for(int i = 0 ; i < input.length ; i++){
            if( queue.size() < k){
                queue.add(input[i]);
            }else{
                if(queue.peek() > input[i]){
                    queue.poll();
                    queue.add(input[i]);
                }
            }
        }
        while(!queue.isEmpty()){
            res.add(queue.poll());
        }
        return res;
    }
}
```

### 3.9 寻找第K大的数（快速排序\小顶堆）

- 描述

  ```java
  有一个整数数组，请你根据快速排序的思路，找出数组中第K大的数。
  给定一个整数数组a,同时给定它的大小n和要找的K(K在``1``到n之间)，请返回第K大的数，保证答案存在。
  ```

- 代码1：小顶堆(堆大小为K，堆顶就是倒数第K大的元素)

  ```java
  import java.util.*;
  public class Solution {
     public int findKth(int[] a, int n, int K){
      // 暂存K个较大的值，优先队列默认是自然排序（升序），队头元素（根）是堆内的最小元素，也就是小根堆
      PriorityQueue<Integer> queue = new PriorityQueue<>(K);
      // 遍历每一个元素，调整小根堆
      for (int num : a) {
          // 对于小根堆来说，只要没满就可以加入（不需要比较）；如果满了，才判断是否需要替换第一个元素
          if (queue.size() < K) {
              queue.add(num);
          } else {
              // 在小根堆内，存储着K个较大的元素，根是这K个中最小的，如果出现比根还要大的元素，说明可以替换根
              if (num > queue.peek()) {
                  queue.poll(); // 高个中挑矮个，矮个淘汰
                  queue.add(num);
              }
          }
      }
      return queue.isEmpty() ? 0 : queue.peek();
  	}
  
  }
  ```

- 代码2：快速排序 + 二分法

  - 思路：
  - step 1：进行一次快排，大元素在左，小元素在右，得到的中轴p点。
  - step 2：如果 p - low + 1 = k ，那么p点就是第K大。
  - step 3：如果 p - low + 1 > k，则第k大的元素在左半段，更新high = p - 1，执行step 1。
  - step 4：如果 p - low + 1 < k，则第k大的元素在右半段，更新low = p + 1, 且 k = k - (p - low + 1)，排除掉前面部分更大的元素，再执行step 1.

  ```java
  import java.util.*;
  
  public class Solution {
      public int findKth(int[] a, int n, int K) {
          return quickSort(a, 0, a.length - 1, K);
      }
  
      private int quickSort(int[] arr, int left, int right, int k){
          int p = partition(arr, left, right);
          // 改进后，很特殊的是，p是全局下标，只要p对上topK坐标就可以返回
          if (p == arr.length - k) {
              return arr[p];
          }else if (p < arr.length - k) {
              // 如果基准在左边，这在右边找
              return quickSort(arr, p + 1, right,k);
          }else {
              return quickSort(arr, left, p - 1,k);
          }
      }
  
      private int partition(int[] arr, int left, int right) {
          // 可优化成随机，或中位数
          int key = arr[left];
          while (left < right) {
              while (left < right && arr[right] >= key) right--;
              arr[left] = arr[right];
              while (left < right && arr[left] <= key) left++;
              arr[right] = arr[left];
          }
          arr[left] = key;
          return left;
      }
  }
  
  ```

### 3.10 数据流中的中位数

- 题目描述

  如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。

-  解题思路

  - 先用java集合PriorityQueue来设置一个小顶堆和大顶堆
  - 主要的思想是：因为要求的是中位数，那么这两个堆，**大顶堆用来存较小的数，从大到小排列**；
  - 小顶堆存较大的数，从小到大的顺序排序**，显然中位数就是大顶堆的根节点与小顶堆的根节点和的平均数。

  - ⭐保证：小顶堆中的元素都大于等于大顶堆中的元素，所以每次塞值，并不是直接塞进去，而是从另一个堆中poll出一个最大（最小）的塞值

  - ⭐当数目为偶数的时候，将这个值插入大顶堆中，再将大顶堆中根节点（即最大值）插入到小顶堆中；

  - ⭐当数目为奇数的时候，将这个值插入小顶堆中，再讲小顶堆中根节点（即最小值）插入到大顶堆中；

  - ⭐取中位数的时候，如果当前个数为偶数，显然是取小顶堆和大顶堆根结点的平均值；如果当前个数为奇数，显然是取小顶堆的根节点

- 思路验证

  例如，传入的数据为：[5,2,3,4,1,6,7,0,8],那么按照要求，输出是"5.00 3.50 3.00 3.50 3.00 3.50 4.00 3.50 4.00 "那么整个程序的执行流程应该是（用min表示小顶堆，max表示大顶堆）：

  - 5先进入大顶堆，然后将大顶堆中最大值放入小顶堆中，此时min=[5],max=[无]，avg=[5.00]

  - 2先进入小顶堆，然后将小顶堆中最小值放入大顶堆中，此时min=[5],max=[2],avg=[(5+2)/2]=[3.50]

  - 3先进入大顶堆，然后将大顶堆中最大值放入小顶堆中，此时min=[3,5],max=[2],avg=[3.00]

  - 4先进入小顶堆，然后将小顶堆中最小值放入大顶堆中，此时min=[4,5],max=[3,2],avg=[(4+3)/2]=[3.50]

  - 1先进入大顶堆，然后将大顶堆中最大值放入小顶堆中，此时min=[3,4,5],max=[2,1]，avg=[3/00]

  - 6先进入小顶堆，然后将小顶堆中最小值放入大顶堆中，此时min=[4,5,6],max=[3,2,1],avg=[(4+3)/2]=[3.50]

  - 7先进入大顶堆，然后将大顶堆中最大值放入小顶堆中，此时min=[4,5,6,7],max=[3,2,1],avg=[4]=[4.00]

  - 0先进入小顶堆，然后将小顶堆中最大值放入小顶堆中，此时min=[4,5,6,7],max=[3,2,1,0],avg=[(4+3)/2]=[3.50]

  - 8先进入大顶堆，然后将大顶堆中最小值放入大顶堆中，此时min=[4,5,6,7,8],max=[3,2,1,0],avg=[4.00]

- 代码

  ```java
  import java.util.PriorityQueue;
  import java.util.Comparator;
  public class Solution {
      //小顶堆
      private PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();
      
      //大顶堆
      private PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(15, new Comparator<Integer>() {
          @Override
          public int compare(Integer o1, Integer o2) {
              return o2 - o1;
          }
      });
      
      //记录偶数个还是奇数个
      int count = 0;
      //每次插入小顶堆的是当前大顶堆中最大的数
      //每次插入大顶堆的是当前小顶堆中最小的数
      //这样保证小顶堆中的数永远大于等于大顶堆中的数
      //中位数就可以方便地从两者的根结点中获取了
      public void Insert(Integer num) {
          //个数为偶数的话，则先插入到大顶堆，然后将大顶堆中最大的数插入小顶堆中
          if(count % 2 == 0){
              maxHeap.offer(num);
              int max = maxHeap.poll();
              minHeap.offer(max);
          }else{
              //个数为奇数的话，则先插入到小顶堆，然后将小顶堆中最小的数插入大顶堆中
              minHeap.offer(num);
              int min = minHeap.poll();
              maxHeap.offer(min);
          }
          count++;
      }
      public Double GetMedian() {
          //当前为偶数个，则取小顶堆和大顶堆的堆顶元素求平均
          if(count % 2 == 0){
              return new Double(minHeap.peek() + maxHeap.peek())/2;
          }else{
              //当前为奇数个，则直接从小顶堆中取元素即可
              return new Double(minHeap.peek());
          }
      }
  }
  
  ```

### 3.11 表达式求值

对于「任何表达式」而言，我们都使用两个栈 `nums` 和 `ops`：

- `nums` ： 存放所有的数字
- `ops` ：存放所有的数字以外的操作

然后从前往后做，对遍历到的字符做分情况讨论：

- 空格 : 跳过
- `(` : 直接加入 `ops` 中，等待与之匹配的 `)`
- `)` : 使用现有的 `nums` 和 `ops` 进行计算，直到遇到左边最近的一个左括号为止，计算结果放到 `nums`
- 数字 : 从当前位置开始继续往后取，将整一个连续数字整体取出，加入 `nums`
- `+ - *` : 需要将操作放入 `ops` 中。**在放入之前先把栈内可以算的都算掉（只有「栈内运算符」比「当前运算符」优先级高/同等，才进行运算）**，使用现有的 `nums` 和 `ops` 进行计算，直到没有操作或者遇到左括号，计算结果放到 `nums`

我们可以通过 🌰 来理解 **只有「栈内运算符」比「当前运算符」优先级高/同等，才进行运算** 是什么意思：

因为我们是从前往后做的，假设我们当前已经扫描到 `2 + 1` 了（此时栈内的操作为 `+` ）。

1. 如果后面出现的 `+ 2` 或者 `- 1` 的话，满足「栈内运算符」比「当前运算符」优先级高/同等，可以将 `2 + 1` 算掉，把结果放到 `nums` 中；
2. 如果后面出现的是 `* 2` 的话，不满足「栈内运算符」比「当前运算符」优先级高/同等，这时候不能计算 `2 + 1`。

一些细节：

- 由于第一个数可能是负数，为了减少边界判断。一个小技巧是先往 `nums` 添加一个 0
- 为防止 () 内出现的首个字符为运算符，将所有的空格去掉，并将 `(-` 替换为 `(0-`，`(+` 替换为 `(0+`（当然也可以不进行这样的预处理，将这个处理逻辑放到循环里去做）
- 从理论上分析，`nums` 最好存放的是 `long`，而不是 `int`。因为可能存在 `大数 + 大数 + 大数 + … - 大数 - 大数` 的表达式导致中间结果溢出，最终答案不溢出的情况

 **事实上，我提供这套解决方案不仅仅能解决只有 `+ - \* ( )` 或者 `+ - \* / ( )` 的表达式问题，还能解决 `+ - \* / ^ % ( )` 的完全表达式问题。**甚至支持		自定义运算符，只要在运算优先级上进行维护即可。

```java
import java.util.*;
public class Solution {
    // 使用 map 维护一个运算符优先级
    // 这里的优先级划分按照「数学」进行划分即可
    Map<Character, Integer> map = new HashMap<Character, Integer>(){{
        put('-', 1);
        put('+', 1);
        put('*', 2);
        put('/', 2);
        put('%', 2);
        put('^', 3);
    }};
    public int solve(String s) {
        // 将所有的空格去掉
        s = s.replaceAll(" ", "");
        char[] cs = s.toCharArray();
        int n = s.length();
        // 存放所有的数字
        Deque<Integer> nums = new ArrayDeque<>();
        // 为了防止第一个数为负数，先往 nums 加个 0
        nums.addLast(0);
        // 存放所有「非数字以外」的操作
        Deque<Character> ops = new ArrayDeque<>();
        for (int i = 0; i < n; i++) {
            char c = cs[i];
            if (c == '(') {
                ops.addLast(c);
            } else if (c == ')') {
                // 计算到最近一个左括号为止
                while (!ops.isEmpty()) {
                    if (ops.peekLast() != '(') {
                        calc(nums, ops);
                    } else {
                        ops.pollLast();
                        break;
                    }
                }
            } else {
                if (isNumber(c)) {
                    int u = 0;
                    int j = i;
                    // 将从 i 位置开始后面的连续数字整体取出，加入 nums
                    while (j < n && isNumber(cs[j])) u = u * 10 + (cs[j++] - '0');
                    nums.addLast(u);
                    i = j - 1;
                } else {
                    if (i > 0 && (cs[i - 1] == '(' || cs[i - 1] == '+' || cs[i - 1] == '-')) {
                        nums.addLast(0);
                    }
                    // 有一个新操作要入栈时，先把栈内可以算的都算了 
                    // 只有满足「栈内运算符」比「当前运算符」优先级高/同等，才进行运算
                    while (!ops.isEmpty() && ops.peekLast() != '(') {
                        char prev = ops.peekLast();
                        if (map.get(prev) >= map.get(c)) {
                            calc(nums, ops);
                        } else {
                            break;
                        }
                    }
                    ops.addLast(c);
                }
            }
        }
        // 将剩余的计算完
        while (!ops.isEmpty() && ops.peekLast() != '(') calc(nums, ops);
        return nums.peekLast();
    }
    // 计算逻辑：从 nums 中取出两个操作数，从 ops 中取出运算符，然后根据运算符进行计算即可
    void calc(Deque<Integer> nums, Deque<Character> ops) {
        if (nums.isEmpty() || nums.size() < 2) return;
        if (ops.isEmpty()) return;
        int b = nums.pollLast(), a = nums.pollLast();
        char op = ops.pollLast();
        int ans = 0;
        if (op == '+') ans = a + b;
        else if (op == '-') ans = a - b;
        else if (op == '*') ans = a * b;    
        else if (op == '/') ans = a / b;    
        else if (op == '^') ans = (int)Math.pow(a, b);
        else if (op == '%') ans = a % b;
        nums.addLast(ans);
    }
    boolean isNumber(char c) {
        return Character.isDigit(c);
    }
}
```

### 3.12 有效的括号

- 算法原理

  栈先入后出特点恰好与本题括号排序特点一致，即若遇到左括号入栈，遇到右括号时将对应栈顶左括号出栈，则遍历完所有括号后 stack 仍然为空；
  建立哈希表 map 构建左右括号对应关系：key左括号，value右括号；这样查询 22 个括号是否对应只需 O(1) 时间复杂度；建立栈 stack，遍历字符串 s 并按照算法流程一一判断。

- 算法流程

  如果 c 是左括号，则入栈 push；
  否则通过哈希表判断括号对应关系，若 stack 栈顶出栈括号 `stack.pop()` 与当前遍历括号 c 不对应，则提前返回 false。

- 解决边界问题

  - 栈为空：此时`stack.pop()`就会报错；给stack赋初值，当stack为空且c为右括号时，可以正常返回`false`；
  - 字符串以左括号结尾：此情况下可以正常遍历完整个 `s`，但 `stack` 中遗留未出栈的左括号；因此，最后需返回 `len(stack) == 1`，以判断是否是有效的括号组合。

![GIF 2022-6-13 20-00-10](Datastructureandalgorithm.assets/GIF 2022-6-13 20-00-10.gif)

- 代码

  ```java
  class Solution {
      private static final Map<Character,Character> map = new HashMap<Character,Character>(){{
          put('{','}'); put('[',']'); put('(',')'); put('?','?');
      }};
      public boolean isValid(String s) {
          if(s.length() > 0 && !map.containsKey(s.charAt(0))) return false;
          LinkedList<Character> stack = new LinkedList<Character>() {{ add('?'); }};
          for(Character c : s.toCharArray()){
              if(map.containsKey(c)) stack.addLast(c);//如果有左括号，就加入栈中
              else if(map.get(stack.removeLast()) != c) return false;//左右括号成一对
          }
          return stack.size() = 1;
      }
  }
  ```

### 3.13 用数组模拟队列

```java
//使用数组模拟环形队列   留一个为空
class CircleArrayQueue {
    private int maxSize;
    private int front;
    private int rear;
    private int[] arr;  //模拟队列

    public CircleArrayQueue(int arrMaxSize) {
        maxSize = arrMaxSize;
        arr = new int[maxSize];
        front = 0; //指向队列头部
        rear = 0;//指向队列尾部的后一个
    }

    public boolean isFull() {
        return (rear + 1) % maxSize == front;
    }

    public boolean isEmpty() {
        return front == rear;
    }

    public void addQueue(int data) {
        if (isFull()) {
            System.out.println("队列满");
            return;
        }
        arr[rear] = data;
        rear++;
        rear %= maxSize;
    }

    public int getQueue() {
        if (isEmpty()) {
            throw new RuntimeException("队列空");
        }
        int value = front;
        front++;
        front %= maxSize;
        return arr[value];
    }

    public void showQueue() {
        if (isEmpty()) {
            System.out.println("队列空");
            return;
        }
        // i < front+队列中元素个数（(rear+maxSize-front)%maxSize）
        for (int i = front; i < front + size(); i++) {  
            System.out.printf("arr[%d]=%d\n", i % maxSize, arr[i % maxSize]);
        }
    }

    public int size() {
        return (rear + maxSize - front) % maxSize;
    }

    //显示队列头部数据
    public int headqueue() {
        if (isEmpty()) {
            throw new RuntimeException("队列空");
        }
        return arr[front];
    }
}
```



## 4.动态规划

### 4.1最小花费爬楼梯

- 描述

  给定一个整数数组 cost ，其中 cost[i]  是从楼梯第i 个台阶向上爬需要支付的费用，下标从0开始。一旦你支付此费用，即可选择向上爬一个或者两个台阶。你可以选择从下标为 0 或下标为 1 的台阶开始爬楼梯。请你计算并返回达到楼梯顶部的最低花费。

  ![alt](Datastructureandalgorithm.assets/CD2B95CDF3D0BEA28A46D1C0172B9F61.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int minCostClimbingStairs (int[] cost) {
          //dp[i]表示爬到第i阶楼梯需要的最小花费
          int[] dp = new int[cost.length + 1]; 
          for(int i = 2; i <= cost.length; i++)
              //每次选取最小的方案
              dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]); 
          return dp[cost.length];
      }
  }
  
  ```

### 4.2最长公共子序列(返回序列字符个数)

- 描述

  给定两个字符串 text1 和 text2，返回这两个字符串的最长 公共子序列 的长度。如果不存在 公共子序列 ，返回 0 。

  一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。
  两个字符串的 公共子序列 是这两个字符串所共同拥有的子序列。

  ```java
  输入：text1 = "abcde", text2 = "ace" 
  输出：3  
  解释：最长公共子序列是 "ace" ，它的长度为 3 。
  ```

- 思路

  求两个数组或者字符串的最长公共子序列问题，肯定是要用动态规划的。下面的题解并不难，你肯定能看懂。

  首先，区分两个概念：子序列可以是不连续的；子数组（子字符串）需要是连续的；
  另外，动态规划也是有套路的：单个数组或者字符串要用动态规划时，可以把动态规划 dp[i] 定义为 `nums[0:i]` 中想要求的结果；当两个数组或者字符串要用动态规划时，可以把动态规划定义成两维的 `dp[i][j]` ，其含义是在 `A[0:i] 与 B[0:j]` 之间匹配得到的想要的结果。

  - 状态定义

    定义`dp[i][j]`表示`text1[0:i-1]和text2[0:j-1]`的最长公共子序列（注：`text1[0:i-1]` 表示的是 `text1` 的 第 0 个元素到第 i - 1 个元素，两端都包含）之所以 `dp[i][j] 的定义不是 text1[0:i] 和 text2[0:j]` ，是为了方便当 i = 0 或者 j = 0 的时候，`dp[i][j]`表示的为空字符串和另外一个字符串的匹配，这样 `dp[i][j]` 可以初始化为 0.

  - 状态转移方程

    当 text1[i - 1] == text2[j - 1] 时，说明两个子字符串的最后一位相等，所以最长公共子序列又增加了 1，所以 `dp[i][j] = dp[i - 1][j - 1] + 1`；举个例子，比如对于 ac 和 bc 而言，他们的最长公共子序列的长度等于 a 和 b 的最长公共子序列长度 0 + 1 = 1。
    当 text1[i - 1] != text2[j - 1] 时，说明两个子字符串的最后一位不相等，那么此时的状态 `dp[i][j]` 应该是 `dp[i - 1][j] 和 dp[i][j - 1]` 的最大值。举个例子，比如对于 ace 和 bc 而言，他们的最长公共子序列的长度等于 ① ace 和 b 的最长公共子序列长度0 与 ② ac 和 bc 的最长公共子序列长度1 的最大值，即 1。

    ```java
    dp[i][j]=dp[i−1][j−1]+1, 当 text1[i - 1] == text2[j - 1];
    dp[i][j]=max(dp[i−1][j],dp[i][j−1]), 当 text1[i - 1] != text2[j - 1]
    ```

  - 状态初始化

    初始化就是要看当 i = 0 与 j = 0 时， `dp[i][j]` 应该取值为多少。

    当 i = 0 时，`dp[0][j]` 表示的是 text1 中取空字符串 跟 text2 的最长公共子序列，结果肯定为 0.
    当 j = 0 时，`dp[i][0]` 表示的是 text2 中取空字符串 跟 text1 的最长公共子序列，结果肯定为 0.
    综上，当 i = 0 或者 j = 0 时，`dp[i][j]` 初始化为 0.

  - 最终返回结果

    由于`dp[i][j]`的含义是`text1[0:i-1]和text2[0:j-1]`的最长公共子序列，所以需要返回的是`dp[text1.length][text2.length]`

- 代码

  ```java
  class Solution {
      public int longestCommonSubsequence(String text1, String text2) {
          int M = text1.length();
          int N = text2.length();
          int[][] dp = new int[M + 1][N + 1];
          for (int i = 1; i <= M; ++i) {
              for (int j = 1; j <= N; ++j) {
                  if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                      dp[i][j] = dp[i - 1][j - 1] + 1;
                  } else {
                      dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                  }
              }
          }
          return dp[M][N];
      }
  }
  ```

- 复杂度分析

  - 时间复杂度：$O(M*N)$
  - 空间复杂度：$O(M*N)$

### 4.3最长公共子序列（返回最长序列String）

- 描述

  给定两个字符串str1和str2，输出两个字符串的最长公共子序列。如果最长公共子序列为空，则返回"-1"，目前给出的数据，仅仅会存在一个最长的公共子序列，数据范围：$0<=|str1|,|str2|<=2000$，要求：$空间复杂度O(n^2),时间复杂度O(n^2)$

  **子序列定义**：一个字符串的子序列是由原字符串在不改变字符相对顺序的情况下删除某些字符（也可以不删任何字符）后组成的新字符串。

  - 例如，`"ace"` 是 `"abcde"` 的子序列，但 `"aec"` 不是 `"abcde"` 的子序列。

  ```java
  输入："1A2C3D4B56","B1D23A456A"
  返回值："123456"
  ```

- 思路

  `c[8][9]` = 5，且`S1[8] != S2[9]`，所以倒推回去，`c[8][9]`的值来源于`c[8][8]`的值(因为`c[8][8] > c[7][9]`)。

  `c[8][8] = 5,  且S1[8] = S2[8],` 所以倒推回去，`c[8][8]`的值来源于 `c[7][7]`。

  以此类推，如果遇到`S1[i] != S2[j] ，且c[i-1][j] = c[i][j-1]` 这种存在分支的情况，这里请都选择一个方向（之后遇到这样的情况，也选择相同的方向）。第一种结果为：

  ![img](Datastructureandalgorithm.assets/Center.jpeg)

  这就是倒推回去的路径，棕色方格为相等元素，即 最长子序列为 {3,4,6,7,8}，这是其中一个结果。如果如果遇到`S1[i] != S2[j] ，且c[i-1][j] = c[i][j-1]` 这种存在分支的情况，选择另一个方向，会得到另一个结果{3,5,7,7,8}。

  ![img](Datastructureandalgorithm.assets/Center-165536858224015.jpeg)

- 代码

  ```java
  import java.util.*;
  
  
  public class Solution {
      /**
       * longest common subsequence
       * @param s1 string字符串 the string
       * @param s2 string字符串 the string
       * @return string字符串
       */
       public String LCS (String s1, String s2) {
          int len1 = s1.length();
          int len2 = s2.length();
          if(len1 == 0 || len2 == 0)
              return "-1";
          int[][] dp = new int[len1+1][len2+1];
          for(int i = 0; i < len1+1; i++){
              for(int j = 0; j < len2+1; j++){
                  //初始化行列第一个元素
                  if(i == 0 || j == 0){
                      dp[i][j] = 0;
                      continue;
                  }
                  if(s1.charAt(i-1) == s2.charAt(j-1)){
                      dp[i][j] = dp[i-1][j-1]+1;
                  }else{
                      dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                  }
              }
          }
          //找出一个最长的公共子序列
          StringBuilder sb = new StringBuilder();
          int s1L = len1, s2L = len2;
          while(s1L != 0 && s2L != 0){
              if (s1.charAt(s1L-1) == s2.charAt(s2L-1)){
                  sb.append(s1.charAt(s1L - 1));
                  s1L--;
                  s2L--;
              }else{
                  if (dp[s1L-1][s2L] > dp[s1L][s2L-1]){
                      s1L--;
                  }else{
                      s2L--;
                  }
              }
          }
          if(sb.length() == 0)
              return "-1";
          return sb.reverse().toString();
      }
  }
  ```

### 4.4最长公共子串

- 描述

  给定两个字符串str1和str2,输出两个字符串的最长公共子串，题目保证str1和str2的最长公共子串存在且唯一。

  输入：

  ```java
  输入："1AB2345CD","12345EF"
  输出："2345"
  ```

  数据范围：$ 1\le|str1|,|str2|\le5000 $
  要求： 空间复杂度 $O(n^2)$,时间复杂度  $O(n^2)$

- 思路

  ![图片说明](Datastructureandalgorithm.assets/E0DAECB00AA87023651AACD533597F0C.png)

  一看到两个字符串的“最值”问题，一般想到二维dp。很自然地想到把str1前i个字符和str2前j个字符最长公共子串的长度作为`dp[i][j]`，但由于子串定义必须是原字符串连续的序列，这样定义无法找到递推关系，因此需要加限定条件——以`str1[i-1]`和`str2[j-1]`结尾的最长公共子串长度。

  也就是str1的第i个字符和str2的第j个字符为最后一个元素所构成的最长公共子串，我们首先需要判断这两个字符是否相等。

  - 如果不相等，那么他们就不能构成公共子串，也就是
    `dp[i][j]=0`
  - 如果相等，我们还需要计算前面相等字符的个数，其实就是dp[i-1][j-1]，所以
    `dp[i][j]=dp[i-1][j-1]+1`

  ```java
  public String LCS(String str1, String str2) {
      int maxLenth = 0;//记录最长公共子串的长度
      //记录最长公共子串最后一个元素在字符串str1中的位置
      int maxLastIndex = 0;
      int[][] dp = new int[str1.length() + 1][str2.length() + 1];
      for (int i = 0; i < str1.length(); i++) {
          for (int j = 0; j < str2.length(); j++) {
              //递推公式，两个字符相等的情况
              if (str1.charAt(i) == str2.charAt(j)) {
                  dp[i + 1][j + 1] = dp[i][j] + 1;
                  //如果遇到了更长的子串，要更新，记录最长子串的长度，
                  //以及最长子串最后一个元素的位置
                  if (dp[i + 1][j + 1] > maxLenth) {
                      maxLenth = dp[i + 1][j+1];
                      maxLastIndex = i;
                  }
              } else {
                  //递推公式，两个字符不相等的情况
                  dp[i + 1][j+1] = 0;
              }
          }
      }
      //最字符串进行截取，substring(a,b)中a和b分别表示截取的开始和结束位置
      return str1.substring(maxLastIndex - maxLenth + 1, maxLastIndex + 1);
  }
  ```

  

### 4.5不同路径的数目

- 描述

  一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。问总共有多少条不同的路径？

  

![img](Datastructureandalgorithm.assets/robot_maze.png)

```java
输入：m = 3, n = 7
输出：28
```

- 思路

  - 排列组合：因为机器到底右下角，向下几步，向右几步都是固定的，比如，m=3, n=2，我们只要向下 1 步，向右 2 步就一定能到达终点。$C^{m-1}_{m+n-2}$

  - 动态规划：我们令`dp[i][j]`是到达`i,j`的最多路径
    - 动态方程：`dp[i][j] = dp[i-1][j] + dp[i][j-1]`,从左边来的路径和加上从右边来的路径和就是当前位置的路径数
    - 动态方程初始化：对于第一行 `dp[0][j]`，或者第一列 `dp[i][0]`，由于都是在边界，所以只能为 1
    - 时间复杂度：O(m*n)O(m∗n)
    - 空间复杂度：O(m * n)O(m∗n)
    - 优化：因为我们每次只需要 `dp[i-1][j],dp[i][j-1]`

  

- 代码

  ```java
  class Solution {
      public int uniquePaths(int m, int n) {
          int[][] dp = new int[m][n];
         //对于第一行 dp[0][j]，或者第一列 dp[i][0]，由于都是在边界，所以只能为 1
          for (int i = 0; i < n; i++) dp[0][i] = 1;
          for (int i = 0; i < m; i++) dp[i][0] = 1;
          for (int i = 1; i < m; i++) {
              for (int j = 1; j < n; j++) {
                  dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
              }
          }
          return dp[m - 1][n - 1];  
      }
  }
  ```

### 4.6矩阵的最小路径和

- 描述

  给定一个包含非负整数的 `m x n` 网格 `grid` ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

  **说明：**每次只能向下或者向右移动一步。

  ![img](Datastructureandalgorithm.assets/minpath.jpg)

  ```java
  输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
  输出：7
  解释：因为路径 1→3→1→1→1 的总和最小。
  ```

- 思路（动态规划）

  - 状态定义：设`dp`为大小为`m x n`的矩阵，其中`dp[i][j]`的值表示走到（i , j）的最小路径和

  - 转移方程：

    - 题目要求，只能向右或向下走，换句话说，当前单元格 `(i,j)` 只能从左方单元格 `(i−1,j)` 或上方单元格`(i,j−1)` 走到，因此只需要考虑矩阵左边界和上边界。

      走到当前单元格 `(i,j)(i,j)` 的最小路径和 = 从左方单元格 `(i−1,j)` 与 从上方单元格 `(i,j−1)` 走来的 两个最小路径和中较小的 + 当前单元格值 `grid[i][j]` 。具体分为以下 4 种情况：

      - 当左边和上边都不是矩阵边界时：即`i != 0 , j != 0`,`dp[i][j] = Math.min(dp[i-1][j] , dp[i][j-a] ) + grid[i][j] `
      - 当只有左边是矩阵边界时：即`i = 0 , j != 0` ,`dp[i][j] = dp[i][j-1] + grid[i][j]`
      - 当只有上边是矩阵边界时：即`i != 0 , j = 0` , `dp[i][j] = dp[i-1][j] + grid[i][j]`

      - 当左边和右边都是矩阵边界时：即`i = 0 , j = 0` , `dp[i][j] = grid[i][j]`

  - 初始状态：dp初始化即可，不需要修改初始0值

  - 返回值：返回dp矩阵右下角值，即走到终点的最小路径和

    其实我们完全不需要建立 dp矩阵浪费额外空间，直接遍历 `grid[i][j]` 修改即可。这是因为：`grid[i][j] = min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j]` ；原 grid 矩阵元素中被覆盖为 dp 元素后（都处于当前遍历点的左上方），不会再被使用到。

  - 复杂度分析

    - 时间复杂度 `O(M×N)` ： 遍历整个 grid 矩阵元素。
    - 空间复杂度 `O(1)` ： 直接修改原矩阵，不使用额外空间。

  - 代码

    ```java
    class Solution {
        public int minPathSum(int[][] grid) {
            for(int i = 0; i < grid.length; i++) {
                for(int j = 0; j < grid[0].length; j++) {
                    if(i == 0 && j == 0) continue;
                    else if(i == 0)  grid[i][j] = grid[i][j - 1] + grid[i][j];
                    else if(j == 0)  grid[i][j] = grid[i - 1][j] + grid[i][j];
                    else grid[i][j] = Math.min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j];
                }
            }
            return grid[grid.length - 1][grid[0].length - 1];
        }
    }
    ```

###4.7 把数字翻译成字符串(一)

- 描述

  有一种将字母编码成数字的方式：'a'->1, 'b->2', ... , 'z->26'。我们把一个字符串编码成一串数字，再考虑逆向编译成字符串。由于没有分隔符，数字编码成字母可能有多种编译结果，例如 11 既可以看做是两个 'a' 也可以看做是一个 'k' 。但 10 只可能是 'j' ，因为 0 不能编译成任何结果。现在给一串数字，返回有多少种可能的译码结果

  数据范围：字符串长度满足 $0 < n \le90$

  进阶：空间复杂度 $O(n)$，时间复杂度 $O(n)$

   其实按照题目要求，一定是可以把数字串转为字符串的，应为这个数字串是从字符串转过来的，但是测试用例有几个是不能转过去的

- 思路（动态规划）

  - 状态定义：`dp[i]`表示`num[0:i]`的可能编码个数
  - 转移方程：
    - 如果`num[i]==0` 则`num[i]`需要牵连上一个字符`num[i-1]`，所以`dp[i] = dp[i-2]`
    - 如果`num[i-1]==0 || num[i-1]*10 + num[i] > 26` 则`num[i]`与前面的字符串不产生关联，所以`dp[i] = dp[i-1]`
    - 如果` num[i-1]*10 + num[i] <= 26` 则`dp[i] = dp[i-1] + dp[i-2]`
  - 状态初始化：`dp[0] == 1`
  - 结果返回：`dp[num.length - 1]`

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int solve (String nums) {
          char[] c = nums.toCharArray();
          int[] num = new int [c.length];
          for(int j =0 ; j < c.length ;j++){
              num[j] = c[j] - '0';
          }
          int[] dp = new int[c.length];
          dp[0] = 1;
          if(c.length==1) return dp[0];
          if(num[1] == 0 || num[0]*10 + num[1] > 26) {
              dp[1] = 1;
          }else if (num[0]*10 + num[1] <= 26){
              dp[1] = 2;
          }
          for(int i = 2 ; i < c.length ; i++){
              if(num[i] == 0 ){
                  if(num[i-1] > 2) return 0;
                  dp[i] = dp[i-2];
              }else if(num[i-1] == 0 || num[i-1]*10 + num[i] > 26){
                  dp[i] = dp[i-1];
              }else if(num[i-1]*10 + num[i] <= 26){
                  dp[i] = dp[i-1] + dp[i-2];
              }
          }
          return dp[c.length - 1];
      }
  }
  ```

### 4.8把数字翻译成字符串（二）

- 描述

  给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

  ```java
  输入: 12258
  输出: 5
  解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
  ```

- 思路

  ![Picture1.png](Datastructureandalgorithm.assets/e231fde16304948251633cfc65d04396f117239ea2d13896b1d2678de9067b42-Picture1.png)

  - 状态定义：设动态规划表dp，dp[i]代表以xi结尾的翻译方案数量

  - 转移方程：

    - 如果xi和xi-1组成的两位数字可以被翻译，则`dp[i] = dp[i -1] + dp[i - 2]`

    - 否则 dp[i] = dp[i-1]

      可被翻译的两位数区间：$当 x_{i-1} = 0$时，组成的两位数是无法被翻译的（例如 00, 01, 02, ⋯ ），因此区间为 [10, 25] 。
      $dp[i] = \begin{cases} dp[i - 1] + dp[i - 2] & {, 10 x_{i-1} + x_i \in [10,25]} \\ dp[i - 1] & {, 10 x_{i-1} + x_i \in [0, 10) \cup (25, 99]} \end{cases}$

  - 初始状态： `dp[0] = dp[1] = 1 ，即 “无数字” 和 “第 11 位数字” 的翻译方法数量均为 1 ；
  - 返回值： `dp[n]` ，即此数字的翻译方案数量。

- 代码

  ```java
  class Solution {
      public int translateNum(int num) {
          String s = String.valueOf(num);
          int a = 1, b = 1;
          for(int i = 2; i <= s.length(); i++) {
              String tmp = s.substring(i - 2, i);
              int c = tmp.compareTo("10") >= 0 && tmp.compareTo("25") <= 0 ? a + b : a;
              b = a;
              a = c;
          }
          return a;
      }
  }
  ```

### 4.9兑换零钱

- 描述

  给你一个整数数组 coins ，表示不同面额的硬币；以及一个整数 amount ，表示总金额。计算并返回可以凑成总金额所需的 最少的硬币个数 。如果没有任何一种硬币组合能组成总金额，返回 -1 。你可以认为每种硬币的数量是无限的。

  ```java
  输入：coins = [1, 2, 5], amount = 11
  输出：3 
  解释：11 = 5 + 5 + 1
  ```

- 思路

  为什么说它符合最优子结构呢？比如你想求 `amount = 11` 时的最少数（原问题），如果你知道凑出 `amount = 10` 的最少数（子问题）

  - 状态定义：dp(n)表示目标金额为n的最少零钱组合数量

  - 初始状态：dp[0] = 0,显然目标金额为0时所需的组合数量为0

  - 状态转移：

    尝试dp[i - coin]的组合数，去凑coin，两者就少了零钱数组中的一个元素的值

    ```java
    for(int coin : coins){
        if( i - coin < 0)  continue;
        //状态转移方程
        dp[i] = Math.min(dp[i], 1 + dp[i - coin]);
    }
    ```

  - 结果

    如果都不符合，dp[amount]没修改，直接返回-1，如果dp[amount]修改后，就返回dp[amount]的值

- 代码

  ```java
  import java.util.Arrays;
  public class Solution {
      public int coinChange(int[] coins, int amount) {
          int[] dp = new int[amount+1];
          Arrays.fill(dp,amount+1);
          dp[0] = 0;
          //外层遍历所有状态的所有取值
          for(int i = 0 ; i < dp.length ;i++){
              //内层循环求所有选择的最小值
              for(int coin : coins){
                  if( i - coin < 0)  continue;
                  //状态转移方程
                  dp[i] = Math.min(dp[i], 1 + dp[i - coin]);
              }
          }
          return (dp[amount] == amount + 1) ? -1 : dp[amount];
      }
  }
  ```

  

### 4.10兑换零钱（二）

- 描述

  给你一个整数数组coins表示不同面额的硬币，另给一个整数amount表示总金额，请你计算并返回可以凑成总金额的硬币组合数，如果任何硬币组合都无法凑出金额，返回0。假设每一种硬币有无数个。

  ```java
  输入：amount = 5, coins = [1, 2, 5]
  输出：4
  解释：有四种方式可以凑成总金额：
  5=5
  5=2+2+1
  5=2+1+1+1
  5=1+1+1+1+1
  ```

- 思路

  - 回溯算法（超时）

    - 代码

      ```java
      class Solution {
          private int res = 0;
          public int change(int amount, int[] coins) {
              int len = coins.length;
              if(len == 0) return res;
              List<Integer> path = new ArrayList<>();
              backtrack(coins,path,0,0,amount,len);
              return res;
      
          }
      
          public void backtrack(int[] coins ,  List<Integer> path , int start ,int sum ,int target ,int len){
              if(sum == target){
                  res++;
                  return;
              }
              for(int i = start ; i < len ; i++){
                  if(sum + coins[i] > target){
                      continue;
                  }
                  path.add(coins[i]);
                  backtrack(coins,path,i,sum+coins[i],target,len);
                  path.remove(path.size() - 1);
              }
          }
      }
      ```

  - 动态规划

    - 状态定义：dp[j]:凑成总金额j的货币组合数为dp[j]

    - 状态转移方程：dp[j] （考虑coins[i]的组合总和） 就是所有的dp[j - coins[i]]相加`dp[j] += dp[j - coins[i]]`

    - 状态初始化：首先dp[0]一定要为1，dp[0] = 1是 递归公式的基础。从dp[i]的含义上来讲就是，凑成总金额0的货币组合数为1。下标非0的dp[j]初始化为0，这样累计加dp[j - coins[i]]的时候才不会影响真正的dp[j]

    - 代码如下：

      ```CPP
      for (int i = 0; i < coins.size(); i++) { // 遍历物品
          for (int j = coins[i]; j <= amount; j++) { // 遍历背包容量
              dp[j] += dp[j - coins[i]];
          }
      }
      ```

      假设：coins[0] = 1，coins[1] = 5。

      那么就是先把1加入计算，然后再把5加入计算，得到的方法数量只有{1, 5}这种情况。而不会出现{5, 1}的情况。

      **所以这种遍历顺序中dp[j]里计算的是组合数！**

      如果把两个for交换顺序，代码如下：

      ```cpp
      for (int j = 0; j <= amount; j++) { // 遍历背包容量
          for (int i = 0; i < coins.size(); i++) { // 遍历物品
              if (j - coins[i] >= 0) dp[j] += dp[j - coins[i]];
          }
      }
      ```

      背包容量的每一个值，都是经过 1 和 5 的计算，包含了{1, 5} 和 {5, 1}两种情况。

      **此时dp[j]里算出来的就是排列数！**

- 代码

  ```java
  class Solution {
      public int change(int amount, int[] coins) {
          //递推表达式
          int[] dp = new int[amount + 1];
          //初始化dp数组，表示金额为0时只有一种情况，也就是什么都不装
          dp[0] = 1;
          for (int i = 0; i < coins.length; i++) {
              for (int j = coins[i]; j <= amount; j++) {
                  dp[j] += dp[j - coins[i]];
              }
          }
          return dp[amount];
      }
  }
  ```

### 4.11最长上升子序列（一）

- 描述

  给定一个长度为 n 的数组 arr，求它的最长严格上升子序列的长度。
  所谓子序列，指一个数组删掉一些数（也可以不删）之后，形成的新数组。例如 [1,5,3,7,3] 数组，其子序列有：[1,3,3]、[7] 等。但 [1,6]、[1,3,5] 则不是它的子序列。当且仅当该序列不存在两个下标i和j满足$i<j且arr_i \ge arr_j$.

  数据范围：$0 \le n \le1000$

  要求：时间复杂度$O(n^2)$,空间复杂度$O(n)$

  ```java
  输入：
  [6,3,1,5,2,3,7]
  返回值：4
  说明：该数组最长上升子序列为 [1,2,3,7] ，长度为4
  ```

- 思路（动态规划）

  - 状态定义：dp[i]表示以nums[i]结尾的上升子序列的长度，num[i]必须被选取且必须是这个子序列的最后一个元素

  - 状态转移方程：如果一个更大的数接在小的数后面，就会形成一个长度加一的子序列，只要num[i]严格大于在它位置之前的某个数，那么num[i]就可以接在这个数后面形成一个更长的上升子序列。

    $$dp[i] = max_{0\le j <i , nums[j] < nums[i]}(dp[j] + 1)$$

  - 状态初始化：dp[i] = 1,一个字符显然长度是1的上升子序列

  - 返回值：

  - 不能返回最后一个状态值，最后一个状态值只表示以 nums[len - 1] 结尾的「上升子序列」的长度，状态数组 dp 的最大值才是题目要求的结果。

    $\max_{1 \le i \le N} dp[i]$
    
    

    

- 代码

  ```java
  import java.util.Arrays;
  
  public class Solution {
  
      public int lengthOfLIS(int[] nums) {
          int len = nums.length;
          if (len < 2) {
              return len;
          }
          //dp数组长度保持和数组nums一致
          int[] dp = new int[len];
          Arrays.fill(dp, 1);
          //填充每一个dp[i]值
          for (int i = 1; i < len; i++) {
  //状态转移：如果一个更大的数接在小的数后面，就会形成一个长度加一的子序列，只要num[i]严格大于在它位置之前的某个数，那么num[i]就可以接在这个数后面形成一个更长的上升子序列。
              for (int j = 0; j < i; j++) {
                  if (nums[j] < nums[i]) {
                      dp[i] = Math.max(dp[i], dp[j] + 1);
                  }
              }
          }
          int res = 0;
          for (int i = 0; i < len; i++) {
              res = Math.max(res, dp[i]);
          }
          return res;
      }
  }
  ```

### 4.12连续子数组的最大和

- 描述

  输入一个长度为n的整型数组array，数组中的一个或连续多个整数，组成一个子数组，子数组最小长度为1，求所有子数组的和的最大值。

  数据范围：$0\le n\le 2*10^5,-100\le a[i]\le100$

  复杂度要求：时间$O(n)$,空间$O(n)$

  ```java
  输入：
  [1,-2,3,10,-4,7,2,-5]
  返回值：18
  说明：经分析可知，输入数组的子数组[3,10,-4,7,2]可以求得最大和为18         
  ```

- 动态规划

  - 状态定义：dp[i]表示以当前元素nums[i]结尾的`nums[0:i]`的数组的最大值

  - 状态转移方程：
    - 如果dp[i-1]<0,表示加上前面的序列的数值反而减少，则以当前数为最大值，dp[i] = nums[i]
    - 否则，dp[i] = dp[i-1] + nums[i]

  - 状态初始化：dp[i] = nums[i]
  - 返回结果：遍历dp[]数组，取最大值，$\max_{1 \le i \le N} dp[i]$

- 代码

  ```java
  public class Solution {
      public int FindGreatestSumOfSubArray(int[] array) {
          int[] dp = new int[array.length];
          dp[0] = array[0];
         for(int i  = 1 ; i < array.length ;i++){
             //状态转移方程
             if(dp[i-1]<0){
                 dp[i]=array[i];
             }else{
                 dp[i] = dp[i-1] + array[i];
             }
         }
          //设置一个全局最小量
          int res = -200;
          for(int c : dp){
              res = Math.max(res,c);
          }
          return res;
      }
  }
  ```

### 4.13最长回文子串

- 描述

  对于长度为n的一个字符串A（仅包含数字，大小写英文字母），请设计一个高效算法，计算其中最长回文子串的长度

  数据范围：$1\le n \le1000$

  复杂度：$空间复杂度O(1),时间复杂度O(n^2)$

  进阶：$空间复杂度O(n),时间复杂度O(n)$

  ```java
  输入："ababc"
  返回值：3
  说明：最长的回文子串为"aba"与"bab"，长度都为3  
  ```

- 动态规划

  - 状态定义：定义二维数组`dp[length][length]`，如果`dp[left][right]`为true，则表示字符串从left到right是回文子串，如果`dp[left][right]`为false，则表示字符串从`left`到`right`不是回文子串。

  - 状态转移方程：如果`dp[left+1][right-1]`为true，我们判断`s.charAt(left)`和`s.charAt(right)`是否相等，如果相等，那么`dp[left][right]`肯定也是回文子串，否则`dp[left][right]`一定不是回文子串。

    **如果s.charAt(left)！=s.charAt(right)**，那么字符串从left到right是不可能构成子串的，直接跳过即可。

    **如果s.charAt(left)==s.charAt(right)**，字符串从left到right能不能构成回文子串还需要进一步判断

    - 如果`left==right`，也就是说只有一个字符，我们认为他是回文子串。即`dp[left][right]=true（left==right）`
    - 如果`right-left<=2`，类似于`"aa"`，或者`"aba"`，我们认为他是回文子串。即`dp[left][right]=true（right-left<=2）`
    - 如果`right-left>2`，我们只需要判断`dp[left+1][right-1]`是否是回文子串，才能确定`dp[left][right]`是否为true还是false。即`dp[left][right]=dp[left+1][right-1]`

- 代码

  ```java
  import java.util.*;
  public class Solution {
      /**
       * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
       * @param A string字符串 
       * @return int整型
       */
          public int getLongestPalindrome(String A) {
          //边界条件判断
              int n = A.length();
          if (n < 2)
              return A.length();
          //start表示最长回文串开始的位置，
          //maxLen表示最长回文串的长度
          int maxLen = 1;
          boolean[][] dp = new boolean[n][n];
          for (int right = 1; right < n; right++) {
              for (int left = 0; left <= right; left++) {
                  //如果两种字符不相同，肯定不能构成回文子串
                  if (A.charAt(left) != A.charAt(right))
                      continue;
  
                  //下面是s.charAt(left)和s.charAt(right)两个
                  //字符相同情况下的判断
                  //如果只有一个字符，肯定是回文子串
                  if (right == left) {
                      dp[left][right] = true;
                  } else if (right - left <= 2) {
                      //类似于"aa"和"aba"，也是回文子串
                      dp[left][right] = true;
                  } else {
                      //类似于"a******a"，要判断他是否是回文子串，只需要
                      //判断"******"是否是回文子串即可
                      dp[left][right] = dp[left + 1][right - 1];
                  }
                  //如果字符串从left到right是回文子串，只需要保存最长的即可
                  if (dp[left][right] && right - left + 1 > maxLen) {
                      maxLen = right - left + 1;
                  }
              }
          }
          //最长的回文子串
          return maxLen;
      }
  }
  ```

### 4.14数字字符串转化为IP地址

- 描述

  现在有一个只包含数字的字符串，将该字符串转化为ip地址的形式，返回所有可能的情况。

  例如：

  给出的字符串为"25525522135"

  返回：["255,255,22,135","255,255,221,35"] (顺序没有关系)

  数据范围：字符串长度`0<=n<12`

  要求：时间O（n!）,空间O（n!）

  注意：注意：ip地址是由四段数字组成的数字序列，格式如 "x.x.x.x"，其中 x 的范围应当是 [0,255]。

- 思路

  - 回溯框架法

    ```java
    //深搜
    import java.util.ArrayList;
    
    public class Solution {
        public ArrayList<String> restoreIpAddresses(String s) {
            ArrayList<String> res = new ArrayList<>();
            ArrayList<String> ip = new ArrayList<>();  //存放中间结果
            dfs(s, res, ip, 0);
            return res;
        }
        
        private void dfs(String s, ArrayList<String> res, ArrayList<String> ip, int start){
            if(ip.size() == 4 && start == s.length()){  //找到一个合法解
                res.add(ip.get(0) + '.' + ip.get(1) + '.' + ip.get(2) + '.' + ip.get(3));
                return;
            }
            if(s.length() - start > 3 * (4 - ip.size()))  //剪枝
                return;
            if(s.length() - start < (4 - ip.size()))  //剪枝
                return;
            int num = 0;
            for(int i = start; i < start + 3 && i < s.length(); i++){
                num = num * 10 + (s.charAt(i) - '0');
                if(num < 0 || num > 255)  //剪枝
                    continue;
                ip.add(s.substring(start, i + 1));
                dfs(s, res, ip, i + 1);
                ip.remove(ip.size() - 1);
                
                if(num == 0)  //不允许前缀0
                    break;
            }
        }
    }
    ```

### 4.15打家劫舍（一）

- 描述

  你是一个经验丰富的小偷，准备偷沿街的一排房子，每一个房子都存在一定的现金，为了防止被发现，你不能偷相邻的两家。

  给定一个整数数组nums，数组中的元素表示每个房间存有的现金数额，请你计算在不被发现的前提下最多偷窃的金额。

  数据范围：数组长度满足 $1 \le n \le 2\times 10^5$ ，数组中每个值满足 $1 \le num[i] \le 5000$  

- 思路（动态规划）
  - 状态定义：`dp[i]`表示以nums[0:i]数组可以偷窃的最大金额，而且必须是以nums[i]结尾
  - 状态转移方程：
    - 除去与当前nums[i]相邻的数，遍历dp[i-3:i-2]，取最大值和nums[i]相加，`dp[i] = dp[i-3:i-2].max + nums[i]`
  - 状态初始化：dp[0] = nums[0],dp[1] = nums[1],dp[2] = nums[0] + nums[2]
  - 返回结果：dp[]数组中的最大值

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int rob (int[] nums) {
          int[] dp = new int[nums.length];
          //状态初始化dp[0],dp[1],dp[2]
          if(nums.length < 2) return nums[0];
          dp[0] = nums[0];
          dp[1] = nums[1];
          if(nums.length >= 3) {
              dp[2] = nums[0]+nums[2];
          }
          for(int i = 3 ; i < nums.length ;i++){
             	 //因为要隔家抢，但是肯定间隔不会超过2家以上。(如果全部遍历，将超出时间限制)
  			//比如说[1,2,1,1,2,1,1]，和[1,2,1,1,1,2,1]，前者是2+2+1，后者是2+1+2。
  			//所以DP时只需要比较（dp[i-1],dp[i-2]+nums[i],dp[i-3]+nums[i]）
              for(int j = i-3 ; j < i - 1 ; j++){
                  dp[i] = Math.max(dp[i] , dp[j]);
              }
              dp[i] = dp[i] + nums[i];
          }
          int res =0;
          for(int dpt : dp){
              res = Math.max(res,dpt);
          }
          return res;
      }
  }
  ```

### 4.16打家劫舍（二）

- 描述

  你是一个经验丰富的小偷，准备偷沿湖的一排房间，每个房间都存在一定的现金，为了防止被发现，你不能偷相邻的两家。沿湖的房间组成一个闭合的圆形，即第一个房间和最后一个房间视为相邻。

  给定一个长度为n的整数数组nums，数组中的每一个房间都表示房间里存有的现金金额，请你计算在不被发现的前提下最多的偷窃金额。

  数据范围：数组长度满足 $1 \le n \le 2\times 10^5$ ，数组中每个值满足 $1 \le num[i] \le 5000$  

  ```java
  输入：[1,2,3,4]
  返回值：6
  说明：最优方案是偷第 2 4 个房间  
   
  输入：[1,3,6]
  返回值：6
  说明：由于 1 和 3 是相邻的，因此最优方案是偷第 3 个房间  
  ```

- 思路(动态规划)

  环状排列意味着第一个房子和最后一个房子中只能选择一个偷窃，因此可以把此环状排列房间问题约化为两个单排排列房间子问题：

  在不偷窃第一个房子的情况下（即 nums[1:]），最大金额是 p1；
  在不偷窃最后一个房子的情况下（即 nums[:n-1]，最大金额是 p2；

  取两者最大值

  思路同打家劫舍（一）

- 代码

  ```java
  import java.util.*;
  public class Solution {
     
     public int rob(int[] nums){
          if(nums.length < 2) return nums[0];
         return Math.max(robOne((int[])Arrays.copyOfRange(nums,0,nums.length-1)),robOne((int[])Arrays.copyOfRange(nums,1,nums.length)));
     }
     
  
      public int robOne (int[] nums) {
          int[] dp = new int[nums.length];
          //状态初始化dp[0],dp[1],dp[2]
          if(nums.length < 2) return nums[0];
          dp[0] = nums[0];
          dp[1] = nums[1];
          if(nums.length >= 3) {
              dp[2] = nums[0]+nums[2];
          }
          for(int i = 3 ; i < nums.length ;i++){
             	 //因为要隔家抢，但是肯定间隔不会超过2家以上。(如果全部遍历，将超出时间限制)
  			//比如说[1,2,1,1,2,1,1]，和[1,2,1,1,1,2,1]，前者是2+2+1，后者是2+1+2。
  			//所以DP时只需要比较（dp[i-1],dp[i-2]+nums[i],dp[i-3]+nums[i]）
              for(int j = i-3 ; j < i - 1 ; j++){
                  dp[i] = Math.max(dp[i] , dp[j]);
              }
              dp[i] = dp[i] + nums[i];
          }
          int res =0;
          for(int dpt : dp){
              res = Math.max(res,dpt);
          }
          return res;
      }
  }
  ```

###   4.17买卖股票的最好时机(一)

- 描述

  假设你有一个数组prices，长度为n，其中prices[i]是股票在第i天的价格，请根据这个价格数组，返回买卖股票能获得的最大收益。

  - 你可以买入一次股票和卖出一次股票，并非每天都可以买入或卖出一次，总共只能买入和卖出一次，且买入必须在卖出的前面的某一天
  - 如果不能获取到任何利润，请返回0
  - 假设买入卖出均没有手续费

  - 数据范围： $0 \le n \le 10^5 , 0 \le val \le 10^4$

    要求：空间复杂度 O*(1)，时间复杂度 O*(*n*)

  ```java
  输入：[8,9,2,5,4,7,1]
  返回值：5
  说明：在第3天(股票价格 = 2)的时候买入，在第6天(股票价格 = 7)的时候卖出，最大利润 = 7-2 = 5 ，不能选择在第2天买入，第3天卖出，这样就亏损7了；同时，你也不能在买入前卖出股票。         
  ```

- 思路(动态规划)

  - 状态定义：dp[i]表示截止到i，价格的最低点是多少
  - 状态转移方程：
    - 如果dp[i - 1] < prices[i],dp[i]=dp[i-1];
    - 否则dp[i] = prices[i]
  - 状态初始化：dp[0] = prices[0];
  - 返回值：用一个数字，记录当前点卖出的最大利润，并返回`res = Math.max(res,prices[i]-dp[i]);`

- 代码

  - 空间复杂度O（n）

    ```java
    import java.util.*;
    public class Solution {
     
        public int maxProfit (int[] prices) {
            if(prices.length < 2) return 0;
            int[] dp = new int[prices.length];
            int res = 0;
            dp[0] = prices[0];
            for(int i = 1 ; i< prices.length ;i++){
                dp[i] = (dp[i-1] < prices[i]) ? dp[i-1]:prices[i];
                res = Math.max(res,prices[i]-dp[i]);
            }
            return res;
        }
    }
    ```

  - 空间复杂度O（1）

    ```java
    public class Solution {
        public int maxProfit(int prices[]) {
            int minprice = Integer.MAX_VALUE;
            int maxprofit = 0;
            for (int i = 0; i < prices.length; i++) {
                if (prices[i] < minprice) {
                    minprice = prices[i];
                } else if (prices[i] - minprice > maxprofit) {
                    maxprofit = prices[i] - minprice;
                }
            }
            return maxprofit;
        }
    }
    ```

### 4.18买卖股票的最好时机（二）

- 描述

  假设你有一个prices数组，长度为n，其中prices[i]是某只股票在第i天的价格，请根据这个价格数组，返回买卖股票能获得的最大收益

  - 你可以**多次**买卖该只股票，但是在此购买前必须卖出之前的股票
  - 如果不能获取收益，请返回0
  - 假设买入卖出均没手续费

  数据范围： $1 \le n \le 1 \times 10^5， 1 \le prices[i] \le 10^4$

  要求：空间复杂度 O(n)，时间复杂度 O(n)

  进阶：空间复杂度 O(1)，时间复杂度 O(n)

  ```java
  输入：[8,9,2,5,4,7,1]
  返回值：7
  说明：
  在第1天(股票价格=8)买入，第2天(股票价格=9)卖出，获利9-8=1
  在第3天(股票价格=2)买入，第4天(股票价格=5)卖出，获利5-2=3
  在第5天(股票价格=4)买入，第6天(股票价格=7)卖出，获利7-4=3
  总获利1+3+3=7，返回7  
  ```

- 思路（动态规划，比较难想，贪心算法非常好用）

  - 状态定义：`dp[i][j]`表示到下标i的这一天，持股状态为j时，我们手上拥有的最大现金数。

    **注意**：限定持股状态为j是为了方便推导状态转移方程，这样的做法满足无后效性

    其中：

    - 第一维i表示下标为i的那一天
    - **第二维j表示下标为i的那一天是持有股票，还是持有现金，0表示持有现金可以买入股票，1表示持有股票可以卖出股票**

  - 状态转移方程：

    ```java
    dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
    ```

  - 状态初始值：

    - 如果什么都不做，`dp[0][0] = 0`；
    - 如果持有股票，当前拥有的现金数是当天股价的相反数，即 `dp[0][1] = -prices[i]`；

  - 返回值：终止的时候，上面也分析了，输出 `dp[len - 1][0]`，因为一定有 `dp[len - 1][0] > dp[len - 1][1]`。

- 代码

  ```java
  public class Solution {
  
      public int maxProfit(int[] prices) {
          int len = prices.length;
          if (len < 2) {
              return 0;
          }
  
          // 0：持有现金
          // 1：持有股票
          // 状态转移：0 → 1 → 0 → 1 → 0 → 1 → 0
          int[][] dp = new int[len][2];
  
          dp[0][0] = 0;
          dp[0][1] = -prices[0];
  
          for (int i = 1; i < len; i++) {
              // 这两行调换顺序也是可以的
              dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
              dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
          }
          return dp[len - 1][0];
      }
  }
  ```

- 贪心算法思路

  仔细观察上面的式子，按照贪心算法，在下标为 1、2、3 的这三天，我们做的操作应该是买进昨天的，卖出今天的，虽然这种操作题目并不允许，但是它等价于：在下标为 0 的那一天买入，在下标为 3 的那一天卖出。

  

  - 这道题 「贪心」 的地方在于，对于 「今天的股价 - 昨天的股价」，得到的结果有 3 种可能：① 正数，② 00，③负数。贪心算法的决策是： **只加正数** 。

- 代码

  ```java
  public class Solution {
  
      public int maxProfit(int[] prices) {
          int len = prices.length;
          if (len < 2) {
              return 0;
          }
  
          int res = 0;
          for (int i = 1; i < len; i++) {
              //只加正数
              res += Math.max(prices[i] - prices[i - 1], 0);
          }
          return res;
      }
  }
  ```

### 4.19买卖股票的最好时机（三）

- 描述

  给定一个数组，他的i个元素是一支给定的股票在第i天的价格

  设计一个算法来计算你所能获取的最大利润，最多可以完成两笔交易

  注意：你不能同时参与多笔交易（你必须在再次购买前出售之前的股票）

  ```java
  输入：prices = [3,3,5,0,0,3,1,4]
  输出：6
  解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
       随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
  ```

- 思路

  一天结束时，可能有持股、可能未持股、可能卖出过1次、可能卖出过2次、也可能未卖出过

  所以定义状态转移数组dp[天数] [当前是否持股] [卖出的次数]

  具体一天结束时的6种状态：

  1. 未持股，未卖出过股票：说明从未进行过买卖，利润为0
  2. `dp[i][0][0]=0`
  3. 未持股，卖出过1次股票：可能是今天卖出，也可能是之前卖的（昨天也未持股且卖出过）
  4. `dp[i][0][1]=max(dp[i-1][1][0]+prices[i],dp[i-1][0][1])`
  5. 未持股，卖出过2次股票:可能是今天卖出，也可能是之前卖的（昨天也未持股且卖出过）
  6. `dp[i][0][2]=max(dp[i-1][1][1]+prices[i],dp[i-1][0][2])`
  7. 持股，未卖出过股票：可能是今天买的，也可能是之前买的（昨天也持股）
  8. `dp[i][1][0]=max(dp[i-1][0][0]-prices[i],dp[i-1][1][0])`
  9. 持股，卖出过1次股票：可能是今天买的，也可能是之前买的（昨天也持股）
  10. `dp[i][1][1]=max(dp[i-1][0][1]-prices[i],dp[i-1][1][1])`
  11. 持股，卖出过2次股票：最多交易2次，这种情况不存在
  12. `dp[i][1][2]=float('-inf')`

- 代码（动态规划（困难）

  ```java
  public int maxProfitDP(int[] prices) {
          if (prices == null || prices.length <= 1) return 0;
          int[][][] dp = new int[prices.length][2][3];
          int MIN_VALUE = Integer.MIN_VALUE / 2;//因为最小值再减去1就是最大值Integer.MIN_VALUE-1=Integer.MAX_VALUE
          //初始化
          dp[0][0][0] = 0;//第一天休息
          dp[0][0][1] = dp[0][1][1] = MIN_VALUE;//不可能
          dp[0][0][2] = dp[0][1][2] = MIN_VALUE;//不可能
          dp[0][1][0] = -prices[0];//买股票
          for (int i = 1; i < prices.length; i++) {
              dp[i][0][0] = 0;
              dp[i][0][1] = Math.max(dp[i - 1][1][0] + prices[i], dp[i - 1][0][1]);
              dp[i][0][2] = Math.max(dp[i - 1][1][1] + prices[i], dp[i - 1][0][2]);
              dp[i][1][0] = Math.max(dp[i - 1][0][0] - prices[i], dp[i - 1][1][0]);
              dp[i][1][1] = Math.max(dp[i - 1][0][1] - prices[i], dp[i - 1][1][1]);
              dp[i][1][2] = MIN_VALUE;
          }
          return Math.max(0, Math.max(dp[prices.length - 1][0][1], dp[prices.length - 1][0][2]));
      }
  ```

  



## 5.排序

### 5.1时间复杂度

- 时间频度：一个算法中语句的执行次数，记为T(n)

- 时间复杂度：O(f(n))，f(n)是T(n)的同量级函数

  用常数1代替T(n)中的加法常数

  只保留T(n)中最高阶项

  去掉T(n)中最高阶项的系数

- 常见的时间复杂度（一般讨论最坏情况下的时间复杂度）：

  1）常数阶O(1)：没有循环等复杂结构

  2）对数阶O(log2 n)：

```java
int i=1;
while(i<n) {
	i = i * 2;
}
```

​		3）线性阶O(n)：

```java
for(int i=1; i<n; i++) {
	sum+=i;
}
```

​	4）线性对数阶O(nlog N)：对数阶外嵌套一个线性阶

​	5）平方阶O(n^2)：线性阶外嵌套一个线性阶

​	6）立方阶和K次方阶同理

- 空间复杂度：算法所耗费的存储空间（不是主要的）



### 5.2冒泡排序BubbleSorting   (n^2)

```java
public class BubbleSort {
    public static void main(String[] args) {

        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        int temp;

        for (int i = 0; i < arr.length - 1; i++) {
            boolean flag = true;    //可提前结束冒泡

            for (int j = 0; j < arr.length - 1 - i; j++) {
                if (arr[j] < arr[j + 1]) {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    flag = false;
                }
            }
            if (flag) {
                break;
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}
```



### 5.3简单选择排序SelectSorting   n^2   n*(n+1)/2

- 第一次从arr[0]到arr[n-1]中选取最小值后，再与arr[0]交换
- 第二次从arr[1]到arr[n-1]中选取最小值后，再与arr[1]交换
- 以此类推
- 速度比冒泡排序快

```java
public class SelectSorting {
    public static void main(String[] args) {
        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        int temp = 0;

        for (int i = 0; i < arr.length - 1; i++) {
            int minSign = i;

            for (int j = i; j < arr.length; j++) {
                if (arr[j] > arr[minSign]) {
                    minSign = j;
                }
            }

            temp = arr[i];
            arr[i] = arr[minSign];
            arr[minSign] = temp;
        }

        System.out.println(Arrays.toString(arr));
    }
}
```



### 5.4直接插入排序InsertSorting

将n个待排元素看成一个有序表和一个无序表，刚开始有序表只有一个元素而无序表有n-1个元素，依次取出无序表的元素并与有序表元素比较后插入

```java
public class InsertSorting {
    public static void main(String[] args) {
        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        int temp;

        for (int i = 1; i < arr.length; i++) {
            temp = arr[i];
            int index = i - 1;  //index+1为要插入的有序表的位置
            while (index >= 0 && temp < arr[index]) {
                arr[index + 1] = arr[index];
                index--;
            }
            arr[index + 1] = temp;
        }

        System.out.println(Arrays.toString(arr));
    }
}
```



### 5.5希尔排序ShellSorting

是一种插入排序（缩小增量排序），把数据按下标的一定增量分组，对每组使用直接插入排序，随着增量减小，每组包含的数据越多，当增量减少至1时，整个数据被分为一组（再进行一次排序），完成排序，**是对直接插入排序的改进**

分为：

- 交换法：每组内部采用冒泡排序（速度很慢）
- 移动法：每组内部采用插入排序

![image-20210511152306229](Datastructureandalgorithm.assets/image-20210511152306229.png)

```java
public class ShellSorting {
    public static void main(String[] args) {
        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        int temp = 0;
        

        //gap代表分组步长(初始组数为总数的一半，组数一直除2直至只有一组)
        for (int gap = arr.length / 2; gap > 0; gap /= 2) {
            //遍历组里所有元素(所有组的无序表类似冒泡的操作)
            for (int i = gap; i < arr.length; i++) {
                //每遍历到组内的一个元素，进行一次冒泡操作
                //每次操作将当前的最小值冒泡到组内最前端
                //遍历完后组内整个冒泡操作也做完变成有序的了
                for (int j = i - gap; j >= 0; j -= gap) {
                    if (arr[j] > arr[j + gap]) {
                        temp = arr[j];
                        arr[j] = arr[j + gap];
                        arr[j + gap] = temp;
                    }
                }
            }
        }

        //gap代表分组步长(初始组数为总数的一半，组数一直除2直至只有一组)
        for (int gap = arr.length / 2; gap > 0; gap /= 2) {
            //遍历所有组(所有组的无序表进行插入排序)
            for (int i = gap; i < arr.length; i++) {
                int j = i;
                temp = arr[i];
                while (j - gap >= 0 && temp < arr[j - gap]) {
                    //移动
                    arr[j] = arr[j - gap];
                    j -= gap;
                }
                //退出while循环时，找到temp的插入位置
                arr[j] = temp;
            }
        }

        System.out.println(Arrays.toString(arr));
    }
}
```



### 5.6快速排序QuickSorting(最坏n^2 , 最好是nlogn)

- 选取一个基准值，经过一次排序，基准值左边的数据比基准值都要小或者相等，基准值右边的数据比基准值都要大或者相等
- 一次排序中，基准值的值不变，但位置可能会发生变化
- 一次排序完成后，该基准值不再参与排序，左边与右边进行迭代递归

![image-20210511152655933](Datastructureandalgorithm.assets/image-20210511152655933.png)

```java
public class QuickSorting {
    public static void main(String[] args) {
        //int arr[] = new int[10000];
        //for (int i = 0; i < arr.length; i++) {
        //    arr[i] = (int) (Math.random() * 10000);
        //}
        int arr[] = {1, 2, 3, 10, 8, 9, 8, 18, 5};
        int temp = 0;
        quicksorting(arr,0, arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    public static void quicksorting(int[] arr, int left, int right) {
        int l = left;   //左下标
        int r = right;  //右下标
        int temp;
        int pivot = arr[(left + right) / 2];    //中间值
        //while循环目的是让比pivot值小的(或等于)放到左边，大的(或等于)放到右边
        //与pivot值相同的不一定靠在一起
        while (l < r) {
            //在pivot的左边找到一个大于等于pivot的值
            //最坏情况是其本身
            while (arr[l] < pivot) {
                l += 1;
            }
            //在pivot的右边找到一个小于等于pivot的值
            //最坏情况是其本身
            while (arr[r] > pivot) {
                r -= 1;
            }
            //如果左右都没找到符合的值,提前跳出
            //即pivot左边全是小于其的值，右边全是大于其的值
            if (l == r) {
                break;
            }
            //找到了进行交换
            temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            //下面两个if是防止有多个与pivot相等的值陷入死循环
            //若只有一个pivot，交换也没关系，只是改变了pivot的位置
            //如果交换完后发现arr[l] == pivot，r前移，即之前的arr[r] == pivot
            if (arr[l] == pivot) {
                r -= 1;
            }
            //如果交换完后发现arr[r] == pivot，l后移，
            if (arr[r] == pivot) {
                l += 1;
            }
        }
        //也必然是l==r，上面的循环才会结束；
        //必须l++，r--，否则出现栈溢出（已经排好的pivot值不参与接下来的排序了）
        //此时l == r也就是pivot的下标，但可能较前发生了变化（有多个值与pivot相等）
        if (l == r) {
            l++;
            r--;
        }
        //向左递归
        if (left < r) { //递归终止条件
            quicksorting(arr, left, r);
        }
        //向右递归
        if (right > l) {    //递归终止条件
            quicksorting(arr, l, right);
        }
    }
}
```



### 5.7归并排序MergeSorting (nlogn)

分治思想（divide and conquer）

![image-20210803204705136](Datastructureandalgorithm.assets/image-20210803204705136.png)

![img](Datastructureandalgorithm.assets\v2-9541d116b9ad191437cb0f9acce7baf6_b.webp)

```java
public class MergeSorting {
    public static void main(String[] args) {
        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        int[] temp = new int[arr.length];
        mergeSort(arr, 0, arr.length - 1, temp);

        System.out.println(Arrays.toString(arr));
    }

    public static void mergeSort(int[] arr, int left, int right, int[] temp) {
        if (left < right) { //（终止条件）直至全部分成只包含一个数据的有序序列
            int mid = (left + right) / 2;   //中间索引
            //向左递归分解
            mergeSort(arr, left, mid, temp);
            //向右递归分解
            mergeSort(arr, mid+1, right, temp);
            //最后一次将两个元素向左向右分解开，无法再递归分解，开始从栈顶开始回溯合并
            //merge()的参数即为当前调用mergeSort()的参数
            merge(arr, left, mid, right, temp);
        }
    }
    

    /**
     * @param arr: 排序的原始数组
     * @param left: 左边有序序列的初始索引
     * @param mid: 中间索引(左边有序序列的末尾)
     * @param right: 右边索引
     * @param temp: 做中转的数组
     * @return int
     * @Description: 合并的方法
     */
    public static void merge(int[] arr, int left, int mid, int right, int[] temp) {
        int i = left;   //左边有序序列的初始索引
        int j = mid + 1;    //右边有序序列的初始索引
        int t = left;      //temp数组的当前索引
        //（一）先把左右两边的数据按大小顺序填充到temp数组
        //直到左右两边有序序列有一边处理完毕为止
        //极限情况，一个数据也是有序序列
        while (i <= mid && j <= right) {
            //合并两个数组
            if (arr[i] <= arr[j]) {
                temp[t] = arr[i];
                t++;
                i++;
            } else {
                temp[t] = arr[j];
                t++;
                j++;
            }
        }
        //（二）把有剩余数据的一边依次填充到temp数组
        while (i <= mid) {  //左边有序序列还有剩余元素
            temp[t] = arr[i];
            t++;
            i++;
        }
        while (j <= right) { //右边有序序列还有剩余元素
            temp[t] = arr[j];
            t++;
            j++;
        }
        //（三）将temp元素拷贝到arr(并不是每次拷贝所有)
        t = left;
        while (t <= right) {
            arr[t] = temp[t];
            t++;
        }
    }
}
```



### 5.8基数排序RadixSorting

- 属于分配式排序（distribution sort），是桶排序的扩展，属于效率高的稳定性排序法
- 经典的牺牲空间换时间的算法，占用内存大，容易造成OutOfMemoryError
- 基本思想：将所有待比较的数据统一为同样的数位长度，数位较短的数前面补0，然后，从最低位开始，依次进行一次排序，一直到最高位排序完成，数列就变成一个有序序列。
- 有负数的数组需要对其改进

![image-20210512125946805](Datastructureandalgorithm.assets/image-20210512125946805.png)

![image-20210512125905584](Datastructureandalgorithm.assets/image-20210512125905584.png)

```java
public class RadixSorting {
    public static void main(String[] args) {
        int arr[] = new int[10000];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * 10000);
        }
        radixSort(arr);
        System.out.println(Arrays.toString(arr));
    }

    public static void radixSort(int[] arr) {
        //先得到最大值的位数
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        int maxLength = (max + "").length();
        //定义一个二维数组，表示10个桶(0~9)，一个一位数组则是一个桶
        //空间换时间的经典算法
        int[][] bucket = new int[10][arr.length];
        //一个一维数组记录各个桶每次放入数据的个数
        int[] bucketEleCounts = new int[10];
        //开始对所有数位进行基数排序
        for (int i = 0; i < maxLength; i++) {
            for (int j = 0; j < arr.length; j++) {
                int digitOfElement = arr[j] / (int) Math.pow(10, i) % 10;
                //放到对应的桶中
                bucket[digitOfElement][bucketEleCounts[digitOfElement]] = j;
                bucketEleCounts[digitOfElement]++;
            }
            int index = 0;  //arr数据的指示
            //按照桶的顺序，将数据放回原来数组
            for (int k = 0; k < bucket.length; k++) {
                for (int x = 0; x < bucketEleCounts[k]; x++) {
                    arr[index] = bucket[k][x];
                    index++;
                }
                //每个桶操作完后，记录桶内数据个数的值需要置0
                bucketEleCounts[k] = 0;
            }
        }
    }
}
```

### 5.9 堆排序

- 堆是具有以下性质的**完全二叉树**：每个结点的值都大于或等于其左右孩子结点的值，称为大顶堆, 每个结点的值都小于或等于其左右孩子结点的值，称为小顶堆

- 大顶堆举例说明：

  ![image-20210729151251530](Datastructureandalgorithm.assets/image-20210729151251530.png)

- 堆排序是一种**选择排序，**它的最坏，最好，平均时间复杂度均为O(nlogn)，它也是不稳定排序。

- 一般升序采用大顶堆，降序采用小顶堆。

- 堆排序基本思想（以升序为例）：

  - 首先将一个排序序列构造成一个大顶堆：
  - 从最后一个非叶子结点开始下沉，循环向前（相当于每次在堆顶加入一个新元素）
  - 每个非叶子结点的下沉是与其左右子结点比较并交换，非叶子结点的值不再交换时结束下沉
  - 此时大顶堆的堆顶元素为最大值，将其与末尾元素交换，此时待排序序列的长度-1
  - 末尾元素也是此大顶堆的一个新元素，继续向下沉得到新的大顶堆，重复这两个操作直至待排序序列的长度为1

- 步骤详细分析

  - 假设给定无序序列结构如下

    ![image-20220610161727974](Datastructureandalgorithm.assets/image-20220610161727974.png)

  - 从最后一个非叶子节点开始（叶节点自然不用调整，第一个非叶子节点`arr.length/2 - 1 = 1`也就是下面的6节点），找到左子节点和右子节点中最大的数，并与根节点交换，按照上述规则从左至右，从下到上操作非叶子节点。

    ![image-20220610162201636](Datastructureandalgorithm.assets/image-20220610162201636.png)

  - 找到第二个非叶子节点4，由于`[4,9,8]`中9元素最大，4和9交换

    ![image-20220610162824839](Datastructureandalgorithm.assets/image-20220610162824839.png)

  - 交换导致字根`[4,5,6]`结构混乱，继续调整，`[4,5,6]`中6最大，交换4和6

    ![image-20220610163106584](Datastructureandalgorithm.assets/image-20220610163106584.png)

    此时就将一个无序序列构造成了一个大顶堆。

  **将堆顶元素与末尾元素进行交换，使末尾元素最大，然后继续调整堆，再将堆顶元素与末尾元素交换，得到第二大的元素，如此反复交换，重建，交换**

  - 堆顶元素与末尾元素交换

    ![image-20220610163644170](Datastructureandalgorithm.assets/image-20220610163644170.png)

  - 重新调整结构，满足堆定义（不需要管末尾的元素9）

    ![image-20220610163919727](Datastructureandalgorithm.assets/image-20220610163919727.png)

  - 交换8和5

    ![image-20220610164049556](Datastructureandalgorithm.assets/image-20220610164049556.png)

  - 依次交换，调整，交换

    ![image-20220610164138299](Datastructureandalgorithm.assets/image-20220610164138299.png)



```java
public class HeapSort {
    public static void main(String[] args) {
        int arr[] = {4, 6, 8, 5, 9};
        heapSort(arr);
    }

    /**
     * Description: 堆排序方法
     * @param arr:
     * @return void:
     */
    public static void heapSort(int arr[]) {
        int temp;
        //构造初始堆（升序采用大顶堆，降序采用小顶堆），从左到右，从下到上
        //i = arr.length / 2 - 1为最后一个非叶子结点
        for (int i = arr.length / 2 - 1; i >= 0; i--) {
            adjustHeap(arr,i, arr.length);
        }
        //将堆顶元素与末尾元素交换，此时只改变了堆顶元素的值，
        //所以从堆顶开始继续调整使其满足大顶堆的定义
        for (int j = arr.length - 1; j > 0; j--) {
            temp = arr[j];
            arr[j] = arr[0];
            arr[0] = temp;
            adjustHeap(arr, 0, j);
        }
        System.out.println(Arrays.toString(arr));

    }

    /**
     * Description: 数组索引为i的非叶子结点，作为根节点，调整所有的子树构成一个堆的结构
     * {4, 6, 8, 5, 9}  i = 1 ->  {4, 9, 8, 5, 6}  
     * {4, 9, 8, 5, 6}  i = 0 ->  {9, 6, 8, 5, 4}
     * @param arr:
     * @param i: 非叶子结点在数组的索引
     * @param length: 表示对数组前length个元素进行调整
     * @return void:
     */
    public static void adjustHeap(int arr[], int i, int length) {

        int temp = arr[i];
        //k = i * 2 + 1是i结点的左子结点，k = i * 2 + 2是i结点的右子结点，k = k * 2 + 1表示找到上层交换下来的数，可能影响下面一层，需要再次循环
        for (int k = i * 2 + 1; k < length; k = k * 2 + 1) {
            if (k + 1 < length && arr[k] < arr[k + 1]) {  //左子结点的值小于右子结点
                //k指向右子结点
                k++;
            }
            if (arr[k] > temp) {    //如果子结点大于父结点
                arr[i] = arr[k];
                //将i指向k(k的值已经交换给了i)继续循环比较
                i = k;
            } else {
                break;
            }
        }
        arr[i] = temp;  //将temp值放到调整后的位置
    }
}
```



### 5.10 常用排序算法总结和对比

![image-20210729094323286](Datastructureandalgorithm.assets/image-20210729094323286.png)

![image-20210512132412367](Datastructureandalgorithm.assets/image-20210512132412367.png)

**相关术语解释：**

​	1)**稳定**：如果a原本在b前面，而a=b，排序之后a仍然在b的前面；

​	2)**不稳定**：如果a原本在b的前面，而a=b，排序之后a可能会出现在b的后面；

​	3)**内排序**：所有排序操作都在内存中完成；

​	4)**外排序**：由于数据太大，因此把数据放在磁盘中，而排序通过磁盘和内存的数据传输才能进行；

​	5)**时间复杂度：** 一个算法执行所耗费的时间。

​	6)**空间复杂度**：运行完一个程序所需内存的大小。

​	7)**n:** 数据规模

​	8)**k:** “桶”的个数

​	9)**In-place:**  不占用额外内存

​	10)**Out-place:** 占用额外内存



## 6.查找

### 6.1线性查找

- 有序数组或无序数组都可使用
- 暴力遍历

```java
public class SeqSearch {
    public static void main(String[] args) {
        int arr[] = {1, 9, 11, -1, 34, 89};
        int index = seqSearch(arr, 11);
        if (index == -1) {
            System.out.println("NotFound！");
        } else {
            System.out.println("index = " + index);
        }
    }
    
    /**
     * @param arr: 
     * @param value: 
     * @return int: 
     * @Description: 查找到一个数据就返回
     */
    public static int seqSearch(int[] arr, int value) {
        //线性查找逐一比对
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == value) {
                return i;
            }
        }
        return -1;
    }
}
```

### 6.2二分查找

- 要求有序数组
- 递归查找

```java
public class BinarySearch {
    public static void main(String[] args) {
        int[] arr = {1, 6, 7, 9, 12, 16, 19, 23, 24, 28, 36, 39, 42};
        int index = binarySearch(arr, 0, arr.length - 1, 9);
        if (index == -1) {
            System.out.println("NotFound！");
        } else {
            System.out.println("index = " + index);
        }

    }

    public static int binarySearch(int[] arr, int left, int right, int value) {

        //递归终止条件
        if (left > right) {
            return -1;
        }
        
        int mid = (left + right) / 2;
        int midVal = arr[mid];
        if (value == midVal) {
            return mid;
        } else if (value < midVal) {
            return binarySearch(arr, left, mid - 1, value);
        } else {
            return binarySearch(arr, mid + 1, right, value);
        }
    }
}
```

- 有多个待查找的值时

```java
public class BinarySearch1 {
    public static void main(String[] args) {
        int[] arr = {1, 6, 7, 9, 12, 16, 19, 19, 19, 23, 24, 28, 36, 39, 42};
        ArrayList<Integer> integers = binarySearch1(arr, 0, arr.length - 1, 19);
        if (integers == null) {
            System.out.println("NotFound！");
        } else {
            System.out.println("index = " + integers.toString());
        }

    }

    public static ArrayList<Integer> binarySearch1(int[] arr, int left, int right, int value) {

        ArrayList<Integer> integers = new ArrayList<>();
        //递归终止条件
        if (left > right) {
            return null;
        }

        int mid = (left + right) / 2;
        int midVal = arr[mid];
        if (value == midVal) {
            int temp = mid - 1;
            while (true) {
                if (temp < 0 || arr[temp] != value) {
                    break;
                }
                integers.add(temp);
                temp--;
            }
            integers.add(mid);
            temp = mid + 1;
            while (true) {
                if (temp > arr.length - 1 || arr[temp] != value) {
                    break;
                }
                integers.add(temp);
                temp++;
            }
            return integers;
        } else if (value < midVal) {
            return binarySearch1(arr, left, mid - 1, value);
        } else {
            return binarySearch1(arr, mid + 1, right, value);
        }
    }
}
```

### 6.3插值查找

- 插值查找算法类似于二分查找，不同的是插值查找每次从**自适应**mid处开始查找
- 对于数据量大，关键字分布比较均匀的查找表来说，采用插值查找速度较快，当不均匀的情况下，不一定比二分查找好
- int mid = left + (right – left) * (findVal – arr[left]) / (arr[right] – arr[left])

```java
public class InsertValueSearch {
    public static void main(String[] args) {
        int[] arr = {1, 6, 7, 9, 12, 16, 19, 23, 24, 25, 28, 36, 39, 42};
        int index = insertValueSearch(arr, 0, arr.length - 1, 9);
        if (index == -1) {
            System.out.println("NotFound！");
        } else {
            System.out.println("index = " + index);
        }

    }

    public static int insertValueSearch(int[] arr, int left, int right, int value) {

        //递归终止条件
        if (left > right) {
            return -1;
        }
        //插值查找
        int mid = left + (value - arr[left]) / (arr[right] - arr[left]) * (right - left);
        int midVal = arr[mid];
        if (value == midVal) {
            return mid;
        } else if (value < midVal) {
            return insertValueSearch(arr, left, mid - 1, value);
        } else {
            return insertValueSearch(arr, mid + 1, right, value);
        }
    }
}
```

### 6.4斐波那契查找

- 核心思想与二分查找类似，mid取值不同，可用非递归方法实现（while+手动改left与right的值）
- 由F[k]=F[k-1]+F[k-2]可得：（F[k]-1）=（F[k-1]-1）+（F[k-2]-1）+1，只要顺序表的长度为**F[k]-1**，则可以将该表分成长度为**F[k-1]-1**和**F[k-2]-1**的两段，**mid=low+F(k-1)-1**      
- 顺序表长度n不一定刚好等于F[k]-1（F[k]-1恰好大于或等于n即可），所以需要将原来的顺序表长度n增加至F[k]-1，用顺序表最后一位的数值进行填充

```java
public class FibonacciSearch {
    static int maxSize = 20;
    public static void main(String[] args) {
        int[] arr = {1, 6, 7, 9, 12, 16, 19, 23, 24, 25, 28, 36, 39, 42};
        int index = fibSearch(arr, 19);
        if (index == -1) {
            System.out.println("NotFound！");
        } else {
            System.out.println("index = " + index);
        }
    }

    //非递归方法得到一个斐波那契数列
    public static int[] fib() {
        int[] f = new int[maxSize];
        f[0] = 1;
        f[1] = 1;
        for (int i = 2; i < maxSize; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        return f;
    }

    public static int fibSearch(int[] arr, int value) {
        int left = 0;
        int right = arr.length - 1;
        int k = 0;  //斐波那契数列分割数值的下标
        int mid;
        int[] fib = fib();  //获取斐波那契数列
        //获取到斐波那契数列分割数值的下标,该数值要刚好大于或等于数组长度
        while (right > fib[k] - 1) {
            k++;
        }
        //f[k]-1的值可能大于arr的长度，构造新的数组，不足的由arr数组最后一位填充
        int[] temp = Arrays.copyOf(arr, fib[k]);
        for (int i = right + 1; i < temp.length; i++) {
            temp[i] = arr[right];
        }
        //使用while循环找到value值
        //手动改left与right的值，加while循环来替代递归
        while (left <= right) {
            //mid将数组分成两部分
            //fib[k] - 1 = (fib[k - 1] - 1) + (fib[k - 2] - 1) + 1;
            mid = left + fib[k - 1] - 1;
            if (value < temp[mid]) {    //向左查找
                right = mid - 1;
                //fib[k-1]-1 = (fib[k-2]-1)+(fib[k-3]-1)+1;
                k--;
            } else if (value > temp[mid]) { //向右查找
                left = mid + 1;
                //fib[k-2]-1 = (fib[k-3]-1)+(fib[k-4]-1)+1;
                k -= 2;
            } else {    //value == temp[mid]
                //扩充过的数组需要确定返回哪个
                if (mid <= right) {
                    return mid;
                } else {
                    return right;
                }
            }
        }
        return -1;
    }
}
```

### 6.5 二维数组中的查找

- 描述

  在一个二维数组array中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序，请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

  ```java
  [
  [1,2,8,9],
  [2,4,9,12],
  [4,7,10,13],
  [6,8,11,15]
  ]
  给定 target = 7，返回 true。
  给定 target = 3，返回 false。
  ```

  数据范围：矩阵的长宽满足  5000≤*n*,*m*≤500 ， 矩阵中的值满足0≤val≤109
  进阶：空间复杂度 O(1) ，时间复杂度 O(n+m)

- 思路（线性搜索）

  解题思路：利用二维数组行列递增特性
  主要思路：

  1. 由于行列递增，可以得出：
     a.在一列中的某个数字，其上的数字都比它小
     b.在一行中的某个数字，其右的数字都比它大

  2. 搜索流程：
     a.首先从数组左下角搜索.
     b.如果当前数字大于target,那么查找往上移一位,如果当前数字小于target,那么查找往右移一位。
     c.查找到target,返回true; 如果越界，返回false;

     ![图片说明](Datastructureandalgorithm.assets/CF34A84A75CE743E086BA50AB6363B9E.png)

     **复杂度分析:**
     时间复杂度:*O(M+N)*
     空间复杂度:O(1)

- 代码

  ```java
  public class Solution {
      public boolean Find(int target, int [][] array) {
          if(array.length == 0 ) return false;
          int left = 0, down = array.length-1;
          while(left<array[0].length && down >=0 ){
              if( array[down][left] == target)
                  return true;
              else if(array[down][left]> target)
                  down--;
              else
                  left++; 
                 
          }
          return false;
      }
  }
  ```

### 6.6 搜索二维矩阵

- 描述

  编写一个高效的算法来判断mxn矩阵中，是否存在一个目标值，该矩阵具有如下的特性：

  - 每行中的整数从左到右按升序排列
  - 每行的第一个整数大于前一行的最后一个整数

  ![img](Datastructureandalgorithm.assets/mat.jpg)

- 思路1：[搜索二维矩阵相同](搜索二维矩阵)

- 思路2：一次二分查找

  若将矩阵每一行拼接在上一行的末尾，则会得到一个升序数组，我们可以在该数组上二分找到目标元素。代码实现时，可以二分升序数组的下标，将其映射到原矩阵的行和列上。

  ​	

  ```java
  class Solution {
      public boolean searchMatrix(int[][] matrix, int target) {
          int m = matrix.length, n = matrix[0].length;
          int low = 0, high = m * n - 1;
          while (low <= high) {
              int mid = (high - low) / 2 + low;
              int x = matrix[mid / n][mid % n];
              if (x < target) {
                  low = mid + 1;
              } else if (x > target) {
                  high = mid - 1;
              } else {
                  return true;
              }
          }
          return false;
      }
  }
  ```

- 思路3：二次二分查找

  由于每行的第一个元素大于前一行的最后一个元素，且每行元素是升序的，所以每行的第一个元素大于前一行的第一个元素，因此矩阵第一列的元素是升序的。我们可以对矩阵的第一列的元素二分查找，找到最后一个不大于目标值的元素，然后在该元素所在行中二分查找目标值是否存在。

  ```java
  class Solution {
      public boolean searchMatrix(int[][] matrix, int target) {
          int rowIndex = binarySearchFirstColumn(matrix, target);
          if (rowIndex < 0) {
              return false;
          }
          return binarySearchRow(matrix[rowIndex], target);
      }
  
      public int binarySearchFirstColumn(int[][] matrix, int target) {
          int low = -1, high = matrix.length - 1;
          while (low < high) {
              int mid = (high - low + 1) / 2 + low;
              if (matrix[mid][0] <= target) {
                  low = mid;
              } else {
                  high = mid - 1;
              }
          }
          return low;
      }
  
      public boolean binarySearchRow(int[] row, int target) {
          int low = 0, high = row.length - 1;
          while (low <= high) {
              int mid = (high - low) / 2 + low;
              if (row[mid] == target) {
                  return true;
              } else if (row[mid] > target) {
                  high = mid - 1;
              } else {
                  low = mid + 1;
              }
          }
          return false;
      }
  }
  ```

### 6.7 寻找峰值

- 描述

  给定一个长度为n的数组nums，请你找到峰值并返回其索引。数组可能包含多个峰值，在这种情况下，返回任何一个所在位置即可。

  1.峰值元素是指其值严格大于左右相邻值的元素。严格大于即不能有等于

  2.假设 nums[-1] = nums[n] = -\infty−∞

  3.对于所有有效的 i 都有 nums[i] != nums[i + 1]

  4.你可以使用O(logN)的时间复杂度实现此问题吗？

  数据范围：

  1≤*nums*.length≤2×10^5^ 

  −2^31^<=nums[i]<=2^31^−1

  如输入[2,4,1,2,7,8,4]时，会形成两个山峰，一个是索引为1，峰值为4的山峰，另一个是索引为5，峰值为8的山峰，如下图所示：

![img](Datastructureandalgorithm.assets/9EB9CD58B9EA5E04C890326B5C1F471F.png)

- 思路

  因为二分查找的本质是`二段性`，二分查找的过程本质是对`可行区间的压缩`。只要满足二段性的问题都可以用二分查找解决。在这里二段性的体现是峰值的左边单调增，右边单调减。你可能会反驳给我们的数值不只有一个峰值，但是只要我们控制好条件，一定可以把范围压缩到只有一个峰值的情况，来看看该怎么处理：

  - nums[mid] < nums[mid + 1]说明在“上坡”，则可以使left = mid + 1（因为mid肯定不是峰值），向“峰”处压缩
  - nums[mid] > nums[mid + 1]说明在“下坡”，则应该使right = mid（mid可能是峰值），往“峰”处压缩

  虽然开始left和right之间可能有多个峰值，但是随着left和right不断逼近，最后两者之间一定会压缩到一个峰值上，因为两者都是向“峰”不断靠近的，但是不会超过`最终`的“峰”

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int findPeakElement (int[] nums) {
          int left = 0;
          int right = nums.length - 1;
          //二分法
          while(left < right){ 
              int mid = ((right - left) >> 1) + left;
              //右边是往下，不一定有坡峰
              if(nums[mid] < nums[mid + 1])
                  left = mid;
              //右边是往上，一定能找到波峰
              else
                  right = mid + 1;
          }
          //其中一个波峰
          return left; 
      }
  }
  ```

### 6.8 数组中的逆序对

- 描述

  在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对，输入一个数组，求出这个数组中的逆序对的总数P

  数据范围： 对于 50% 的数据, size≤10^4^
  对于 100% 的数据, size≤10^5^

  数组中所有数字的值满足 0≤val≤1000000

  要求：空间复杂度 O(n)，时间复杂度 O(nlogn)

  输入描述：题目保证输入的数组中没有的相同的数字

  ```java
  输入：[1,2,3,4,5,6,7,0]
  返回值：7
  ```

- 思路（归并排序）

  归并排序过程：

  如下图所示，为数组 [7, 3, 2, 6, 0, 1, 5, 4] 的归并排序过程：

  ![Picture1.png](Datastructureandalgorithm.assets/1614274007-nBQbZZ-Picture1.png)

合并阶段 本质上是 合并两个排序数组 的过程，而每当遇到 左子数组当前元素 > 右子数组当前元素 时，意味着 「左子数组当前元素 至 末尾元素」 与 「右子数组当前元素」 构成了若干 「逆序对」 。

如下图所示，为左子数组 [2, 3, 6, 7]与 右子数组 [0, 1, 4, 5]的合并与逆序对统计过程。

![GIF 2022-6-27 13-41-00](Datastructureandalgorithm.assets/GIF 2022-6-27 13-41-00.gif)

- 算法流程

  - 终止条件： 当 l≥r 时，代表子数组长度为 1 ，此时终止划分；

  - 递归划分： 计算数组中点 m ，递归划分左子数组 merge_sort(l, m) 和右子数组 merge_sort(m + 1, r) ；

  - 合并与逆序对统计：

    - 暂存数组 nums 闭区间 [i, r] 内的元素至辅助数组 tmp ；
    - 循环合并： 设置双指针i , j 分别指向左 / 右子数组的首元素；
      - 当 i = m + 1 时： 代表左子数组已合并完，因此添加右子数组当前元素 tmp[j] ，并执行 j = j + 1 ；
      - 否则，当 j = r + 1 时： 代表右子数组已合并完，因此添加左子数组当前元素 tmp[i]，并执行 i = i + 1；
      - 否则，当 tmp[i] ≤tmp[j] 时： 添加左子数组当前元素 ttmp[i] ，并执行i=i+1；
      - 否则（ tmp[i]>tmp[j]）时： 添加右子数组当前元素 tmp[j] ，并执行 j=j+1 ；此时构成m−i+1 个「逆序对」，统计添加至 res ；
      - 返回值： 返回直至目前的逆序对总数 res ；

    ![Picture2.png](Datastructureandalgorithm.assets/1614274007-rtFHbG-Picture2.png)

- 代码（在归并排序上面加了一句count += (mid - i + 1)）

  ```java
  class Solution {
  
      int count ;
      public int reversePairs(int[] nums) {
          int[] temp = new int[nums.length];
          mergeSort(nums,0,nums.length-1,temp);
          return count;
      }
  
  
      public  void mergeSort(int[] arr, int left, int right, int[] temp) {
          if (left < right) { //（终止条件）直至全部分成只包含一个数据的有序序列
              int mid = (left + right) / 2;   //中间索引
              //向左递归分解
              mergeSort(arr, left, mid, temp);
              //向右递归分解
              mergeSort(arr, mid+1, right, temp);
              //最后一次将两个元素向左向右分解开，无法再递归分解，开始从栈顶开始回溯合并
              //merge()的参数即为当前调用mergeSort()的参数
              merge(arr, left, mid, right, temp);
          }
      }
  
  
      /**
       * @param arr: 排序的原始数组
       * @param left: 左边有序序列的初始索引
       * @param mid: 中间索引(左边有序序列的末尾)
       * @param right: 右边索引
       * @param temp: 做中转的数组
       * @return int
       * @Description: 合并的方法
       */
      public  void merge(int[] arr, int left, int mid, int right, int[] temp) {
          int i = left;   //左边有序序列的初始索引
          int j = mid + 1;    //右边有序序列的初始索引
          int t = left;      //temp数组的当前索引
          //（一）先把左右两边的数据按大小顺序填充到temp数组
          //直到左右两边有序序列有一边处理完毕为止
          //极限情况，一个数据也是有序序列
          while (i <= mid && j <= right) {
              //合并两个数组
              if (arr[i] <= arr[j]) {
                  temp[t] = arr[i];
                  t++;
                  i++;
              } else {
                  //用来统计逆序对的个数，关键步骤
                  count += (mid - i + 1);
                  temp[t] = arr[j];
                  t++;
                  j++;
              }
          }
          //（二）把有剩余数据的一边依次填充到temp数组
          while (i <= mid) {  //左边有序序列还有剩余元素
              temp[t] = arr[i];
              t++;
              i++;
          }
          while (j <= right) { //右边有序序列还有剩余元素
              temp[t] = arr[j];
              t++;
              j++;
          }
          //（三）将temp元素拷贝到arr(并不是每次拷贝所有)
          t = left;
          while (t <= right) {
              arr[t] = temp[t];
              t++;
          }
      }
  
  }
  ```

### 6.9 旋转数组的最小数字

- 描述

  有一个长度为n的非降序数组，比如[1,2,3,4,5],将它进行旋转，即把一个数组最开始的若干个元素搬到数组的末尾，变成一个旋转数组，比如变成了[3,4,5,1,2],或者[4,5,1,2,3]，请问，给定这样一个旋转数组，求数组中的最小值。

  数据范围：1≤*n*≤10000，数组中任意元素的值: 0 ≤val≤10000

  要求：空间复杂度：O(1) ，时间复杂度：O(logn)

- 思路

  **算法流程：**

  1、初始化： 声明 i, j 双指针分别指向 array 数组左右两端

  2、循环二分： 设 m = (i + j) / 2 为每次二分的中点（ "/" 代表向下取整除法，因此恒有 i≤m1、当 array[m] > array[j] 时： m 一定在 左排序数组 中，即旋转点 x 一定在 [m + 1, j] 闭区间内，因此执行 i = m + 1
  2、当 array[m] < array[j] 时： m 一定在 右排序数组 中，即旋转点 x 一定在[i, m]闭区间内，因此执行 j = m
  3、当 array[m] = array[j] 时： 无法判断 mm 在哪个排序数组中，即无法判断旋转点 x 在 [i, m] 还是 [m + 1, j] 区间中。解决方案： 执行 j = j - 1 缩小判断范围
  3、返回值： 当 i = j 时跳出二分循环，并返回 旋转点的值 array[i] 即可。

  ![img](Datastructureandalgorithm.assets/3C28F80DBB0E1E084CB71A32958F04F9.png)

- 代码

  ```java
  import java.util.*;
  import java.util.ArrayList;
  public class Solution {
      public int minNumberInRotateArray(int [] array) {
          int left = 0 ; 
          int right = array.length -1;
          while(left < right){
              int  mid = left + (right - left)/2;
              if(array[mid] < array[right]){
                  right = mid  ;
              }else if(array[mid] > array[right]){
                   left = mid + 1;
              }else{
                  right--;
              }
             
          }
          return array[left];
      }
  }
  ```

##

## 7.哈希表

### 7.1 哈希表(数组加链表)实现雇员系统

散列表（Hash table，也叫哈希表），是根据关键码值(Key value)而直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。这个映射函数叫做**散列函数**，存放记录的数组叫做散列表。

```java
* @description: 哈希表(数组加链表)实现雇员系统
 */
public class HashTableDemo {
    public static void main(String[] args) {
        //创建哈希表
        HashTable hashTable = new HashTable(7);
        //简单菜单
        int key;
        Scanner scanner = new Scanner(System.in);
        Boolean flag = true;
        while (flag) {
            System.out.println("1:添加雇员");
            System.out.println("2.显示雇员");
            System.out.println("3.显示雇员");
            System.out.println("4.退出");
            key = scanner.nextInt();
            switch (key) {
                case 1:
                    System.out.println("输入id");
                    int id = scanner.nextInt();
                    System.out.println("输入名字");
                    String name = scanner.next();
                    hashTable.add(new Emp(id, name));
                    break;
                case 2:
                    hashTable.list();
                    break;
                case 3:
                    System.out.println("输入id");
                    int id1 = scanner.nextInt();
                    hashTable.find(id1);
                    break;
                case 4:
                    flag = false;
                    scanner.close();
                    break;
            }
        }
    }
}

//创建哈希表，管理多条链表
class HashTable {
    private EmpLinkedList[] empLinkedLists;


    public HashTable(int size) {
        this.empLinkedLists = new EmpLinkedList[size];
        //分别初始化各条链表
        for (int i = 0; i < size; i++) {
            empLinkedLists[i] = new EmpLinkedList();
        }
    }

    //添加雇员
    public void add(Emp emp) {
        //根据id和散列函数决定其放入哪条链表
        int NO = hashFun(emp.id);
        empLinkedLists[NO].add(emp);
    }

    //遍历
    public void list() {
        for (int i = 0; i < empLinkedLists.length; i++) {
            empLinkedLists[i].list();
        }
    }

    //查找
    public Emp find(int id) {
        int NO = hashFun(id);
        Emp emp = empLinkedLists[NO].find(id);
        if (emp == null) {
            System.out.println("没有找到");
        } else {
            System.out.printf("在第%d条链表中找到id=%d的职员", NO, id);
        }
        return emp;
    }

    //散列函数
    public int hashFun(int id) {
        return id % empLinkedLists.length;
    }
}

//一个雇员
class Emp {
    public int id;
    public String name;
    public Emp next; //默认为空

    public Emp(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

//一条链表
class EmpLinkedList {
    private Emp head;   //表示一个雇员

    public void add(Emp emp) {
        if (head == null) {
            head = emp;
            return;
        }
        Emp curEmp = head;
        while (true) {
            if (curEmp.next == null) {
                break;
            }
            curEmp = curEmp.next;
        }
        curEmp.next = emp;
    }

    public void list() {
        if (head == null) {
            System.out.println("空");
            return;
        }
        Emp curEmp = head;
        while (true) {
            if (curEmp.next == null) {
                System.out.printf("id=%d name=%s\t", curEmp.id, curEmp.name);
                break;
            }
            curEmp = curEmp.next;
            System.out.println();
        }
    }

    public Emp find(int id) {
        if (head == null) {
            System.out.println("空");
            return null;
        }
        Emp curEmp = head;
        while (true) {
            if (curEmp.id == id) {
                break;
            }
            if (curEmp.next == null) {
                return null;
            }
            curEmp = curEmp.next;
        }
        return curEmp;
    }
}
```



### 7.2 两数之和

- 描述

  给出一个整型数组 numbers 和一个目标值 target，请在数组中找出两个加起来等于目标值的数的下标，返回的下标按升序排列。

  （注：返回的**数组下标从1开始**算起，保证target一定可以由数组里面2个数字相加得到）

  数据范围：2≤len(numbers)≤10^5^，−10≤numbersi≤10^9^，0≤target≤109

  要求：空间复杂度 O*(*n)，时间复杂度 O(nlogn)

  ```java
  输入：[3,2,4],6
  返回值：[2,3]
  说明：因为 2+4=6 ，而 2的下标为2 ， 4的下标为3 ，又因为 下标2 < 下标3 ，所以返回[2,3]    
  ```

  

- 思路

  ![图片说明](Datastructureandalgorithm.assets/89BD3BA90925FBF5408062AFC8863203.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      
      public int[] twoSum (int[] numbers, int target) {
          HashMap<Integer, Integer> map = new HashMap<>();
          //遍历数组
          for (int i = 0; i < numbers.length; i++) {
              //将不包含target - numbers[i]，装入map中，包含的话直接返回下标
              if(map.containsKey(target - numbers[i])) 
                  return new int[]{map.get(target - numbers[i])+1, i+1};
              else 
                  map.put(numbers[i], i);
          }
          throw new IllegalArgumentException("No solution");
      }
  }
  ```

### 7.3 三数之和

- 描述

  给出一个有n个元素的数组s，s中是否有元素abc满足a+b+c=0？找到数组s中所有满足条件的三元组

  数据范围：0≤*n*≤3000，数组中各个元素值满足val∣≤100

  空间复杂度：O(n^2)，时间复杂度 O(n^2)

  注意：

  1. 三元组（a、b、c）中的元素可以按任意顺序排列。
  2. 解集中不能包含重复的三元组。

  ```java
  输入：[-10,0,10,20,-10,-40]
  返回值：[[-10,-10,20],[-10,0,10]]
  ```

- 思路（双指针）

  双指针法思路： 固定 3 个指针中最左（最小）数字的指针 k，双指针 i，j 分设在数组索引 (k, len(nums)) 两端，通过双指针交替向中间移动，记录对于每个固定指针 k 的所有满足 nums[k] + nums[i] + nums[j] == 0 的 i,j 组合：

  - 当 nums[k] > 0 时直接break跳出：因为 nums[j] >= nums[i] >= nums[k] > 0，即 3 个数字都大于 0 ，在此固定指针 k 之后不可能再找到结果了。
  - 当 k > 0且nums[k] == nums[k - 1]时即跳过此元素nums[k]：因为已经将 nums[k - 1] 的所有组合加入到结果中，本次双指针搜索只会得到重复组合。
  - i，j 分设在数组索引 (k, len(nums))两端，当i < j时循环计算s = nums[k] + nums[i] + nums[j]，并按照以下规则执行双指针移动：
    - 当s < 0时，i += 1并跳过所有重复的nums[i]；
    - 当s > 0时，j -= 1并跳过所有重复的nums[j]；
    - 当s == 0时，记录组合[k, i, j]至res，执行i += 1和j -= 1并跳过所有重复的nums[i]和nums[j]，防止记录到重复组合。

- 代码

  ```java
  class Solution {
      public List<List<Integer>> threeSum(int[] nums) {
          Arrays.sort(nums);//排序，nums变成递增数组
          List<List<Integer>> res = new ArrayList<>();
          //k < nums.length - 2是为了保证后面还能存在两个数字
          for(int k = 0; k < nums.length - 2; k++){
              if(nums[k] > 0) break;//若nums[k]大于0，则后面的数字也是大于零（排序后是递增的）
              if(k > 0 && nums[k] == nums[k - 1]) continue;//nums[k]值重复了，去重
              int i = k + 1, j = nums.length - 1;//定义左右指针
              while(i < j){
                  int sum = nums[k] + nums[i] + nums[j];
                  if(sum < 0){
                      while(i < j && nums[i] == nums[++i]);//左指针前进并去重
                  } else if (sum > 0) {
                      while(i < j && nums[j] == nums[--j]);//右指针后退并去重
                  } else {
                      res.add(new ArrayList<Integer>(Arrays.asList(nums[k], nums[i], nums[j])));
                      while(i < j && nums[i] == nums[++i]);//左指针前进并去重
                      while(i < j && nums[j] == nums[--j]);//右指针后退并去重
                  }
              }
          }
          return res;
      }
  }
  ```

  

### 7.4 数组中出现次数超过一半的数字

- 描述

  给一个长度为 n 的数组，数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

  例如输入一个长度为9的数组[1,2,3,2,2,2,5,4,2]。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。

  数据范围：n≤50000，数组中元素的值0≤val≤10000

  要求：空间复杂度：O(1)，时间复杂度 O(n)

  输入描述：保证数组输入非空，且保证有解

- 思路

  先遍历一遍数组，在map中存每个元素出现的次数，然后再遍历一次数组，找到出现次数大于数组长度一半的数字。

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int MoreThanHalfNum_Solution(int [] array) {
          int res = 0;
          Map<Integer, Integer> map = new HashMap();
          for (int num : array) {
              map.put(num, map.getOrDefault(num, 0) + 1);
          }
          for (int num : array) {
              if (map.get(num) > array.length/2) {
                  return num;
              }
  
          }
          return 0;
      }
  }
  ```

### 7.5 数组中只出现一次的两个数字

- 描述

  一个整型数组里除了两个数字只出现一次，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

  数据范围：数组长度 2≤*n*≤1000，数组中每个数的大小 0<val≤1000000
  要求：空间复杂度 O(1)，时间复杂度 O(n)

  提示：输出时按非降序排列。

- 思路

  先遍历一遍数组，在map中存放每一个元素出现的次数，然后在遍历一遍数组，找到出现次数等于1的数字，并将些数字存放入res[]中，最后将res数组元素升序输出

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int[] FindNumsAppearOnce (int[] array) {
          int[] res = new int[2];
          Map<Integer, Integer> map = new HashMap();
          for (int num : array) {
              map.put(num, map.getOrDefault(num, 0) + 1);
          }
          int index = 0;
          for (int num : array) {
              if (map.get(num) == 1) {
                  if(index < 2){
                      res[index] = num;
                      index++;
                  }            
              }
          }
          if(res[0]>res[1]){
              int temp = res[1];
              res[1] = res[0];
              res[0] =temp;
          }
  
          return res;
      }
  }
  ```

### 7.6 缺失的第一个正整数

- 描述

  给定一个未排序的整数数组nums，请你找出其中没有出现的最小的正整数

  进阶:空间复杂度O(1)，时间复杂度O(n)

  数据范围:

  -2^31^<=nums[i]<=2^31^-1

  0<=len(nums)<=5*10^5^

- 思路（HashMap）

  *n*个长度的数组，没有重复，则如果数组填满了1～n，那么缺失n+1，如果数组填不满1～n，那么缺失的就是1～n中的数字。对于这种快速查询某个元素是否出现过的问题，还是可以使用哈希表快速判断某个数字是否出现过。

  具体做法：

  - step 1：构建一个哈希表，用于记录数组中出现的数字。
  - step 2：从1开始，遍历到n，查询哈希表中是否有这个数字，如果没有，说明它就是数组缺失的第一个正整数，即找到。
  - step 3：如果遍历到最后都在哈希表中出现过了，那缺失的就是n+1.

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int minNumberDisappeared (int[] nums) {
          int n = nums.length;
          HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>(); 
          //哈希表记录数组中出现的每个数字
          for(int i = 0; i < n; i++) 
              mp.put(nums[i], 1);
          int res = 1;
          //从1开始找到哈希表中第一个没有出现的正整数
          while(mp.containsKey(res)) 
              res++;
          return res;
      }
  }
  
  ```

  

## 8.树

### 8.1 二叉树介绍

- 树相较于顺序存储和链式存储能提高数据**存储，读取**的效率

  - 顺序存储如数组：
    - 优点：通过下标方式访问元素，速度快。**对于有序数组**，还可使用二分查找提高检索速度。
    - 缺点：如果要检索具体某个值，或者插入值(按一定顺序)**会整体移动**，效率较低
  - 链式存储：
    - 优点：在一定程度上对数组存储方式有优化(比如：插入一个数值结点，只需要将插入结点，链接到链表中即可， 删除效率也很好)。
    - 缺点：在进行检索时，效率仍然较低，比如(检索某个值，需要从头结点开始遍历) 

  ![image-20210525190112848](Datastructureandalgorithm.assets/image-20210525190112848.png)

- 树的常用术语(结合示意图理解):

  1)结点	2)根结点	3)父结点	4)子结点	5)叶子结点 (没有子结点的结点)	6)结点的权(结点值)	7)路径(从root结点找到该结点的路线)	8)层	9)子树	10)树的高度(最大层数)	11)森林 :多颗子树构成森林

- 树有很多种，每个结点**最多只能有两个子结点**的一种形式称为二叉树。

- 如果该二叉树的**所有叶子结点都在最后一层**，并且结点总数= 2^n -1 , n 为层数，则我们称为满二叉树。

- 如果该二叉树的所有叶子结点都在最后一层或者倒数第二层，而且最后一层的叶子结点在左边连续，倒数第二层的叶子结点在右边连续，我们称为完全二叉树。

- ![image-20210728144043481](Datastructureandalgorithm.assets/image-20210728144043481.png)


### 8.2 前序遍历

- 描述

  给你二叉树的根节点 root ，返回它节点值的 前序 遍历。

  数据范围：二叉树的节点数量满足0≤*n*≤100 ，二叉树节点的值满足 1≤val≤100 ，树的各节点的值各不相同

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
  
      ArrayList<Integer> resArray = new ArrayList();
      public int[] preorderTraversal (TreeNode root) {
          if(root==null){
              return new int[0];
          }
          preOrder(root);
          int[] res = new int[resArray.size()];
          for(int i = 0 ; i < resArray.size() ; i++){
              res[i] = resArray.get(i);
          }
          return res;
  
      }
      
      public void preOrder(TreeNode root){
          resArray.add(root.val);
          if(root.left != null){
              preOrder(root.left);
          }
          if(root.right != null){
              preOrder(root.right);
          } 
      }
  
  
  }
  ```

### 8.3 中序遍历

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
  
      ArrayList<Integer> resArray = new ArrayList();
      public int[] preorderTraversal (TreeNode root) {
          if(root==null){
              return new int[0];
          }
          preOrder(root);
          int[] res = new int[resArray.size()];
          for(int i = 0 ; i < resArray.size() ; i++){
              res[i] = resArray.get(i);
          }
          return res;
  
      }
      
      public void preOrder(TreeNode root){
         
          if(root.left != null){
              preOrder(root.left);
          }
           resArray.add(root.val);
          if(root.right != null){
              preOrder(root.right);
          } 
      }
  
  
  }
  ```

### 8.4 后序遍历

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
  
      ArrayList<Integer> resArray = new ArrayList();
      public int[] preorderTraversal (TreeNode root) {
          if(root==null){
              return new int[0];
          }
          preOrder(root);
          int[] res = new int[resArray.size()];
          for(int i = 0 ; i < resArray.size() ; i++){
              res[i] = resArray.get(i);
          }
          return res;
  
      }
      
      public void preOrder(TreeNode root){
         
          if(root.left != null){
              preOrder(root.left);
          }
          if(root.right != null){
              preOrder(root.right);
          } 
           resArray.add(root.val);
      }
  
  
  }
  ```

### 8.5 求二叉树的层序遍历

- 描述

  给定一个二叉树，返回该二叉树层序遍历的结果（从左到右，一层一层地遍历），例如：给定的二叉树是{3,9,20，#，#，15,7}

  ![img](Datastructureandalgorithm.assets/036DC34FF19FB24652AFFEB00A119A76.png)

  ```java
  该二叉树层序遍历的结果是
  [[3],[9,20],[15,7]]
  ```

- 数据范围：二叉树的节点数满足1≤n≤10^5^

- 自己的代码

  ```java
  import java.util.*;
  public class Solution {
      
      public ArrayList<ArrayList<Integer>> levelOrder (TreeNode root) {
          ArrayList<ArrayList<Integer>> res = new ArrayList();
          ArrayList<Integer> valPath = new ArrayList();
          ArrayList<TreeNode> path = new ArrayList();
          ArrayList<TreeNode> temp = new ArrayList();
          temp.add(root);
          valPath.add(root.val);
          res.add(new ArrayList<Integer>(valPath));//不可直接res.add(valPath),之后改变valPath的值，res也会随之改变
          valPath.clear();
          while (temp.size() != 0) {
  
              for (int i = 0 ; i < temp.size() ; i++) {
                  if (temp.get(i).left != null) {
                      path.add(temp.get(i).left);
                      valPath.add(temp.get(i).left.val);
                  }
                  if (temp.get(i).right != null) {
                      path.add(temp.get(i).right);
                      valPath.add(temp.get(i).right.val);
                  }
              }
              if(valPath.size() == 0) break;
              res.add(new ArrayList<Integer>(valPath));
              valPath.clear();
              temp.clear();
              for (int i = 0 ; i < path.size() ; i++) {
                  temp.add(path.get(i));
              }
              path.clear();
  
          }
          return res;
  
      }
  }
  ```

- 别人的代码（队列的方法）

  - 维护一个队列，队列保存每一层所有结点

  - list集合收集当前层的所有结点的值

  - 遍历所有每一层，从队列中取出当前层所有结点，并收集结果到集合

  - 左右节点按顺序加到队尾

    ![image-20210715214359892](Datastructureandalgorithm.assets/image-20210715214359892.png)

  ```java
  import java.util.*;
  
  public class Solution {
      public ArrayList<ArrayList<Integer>> levelOrder (TreeNode root) {
          ArrayList<ArrayList<Integer>> res = new ArrayList<>();        
          if(root == null) {
              return res;
          }        
          // 队列保存每一层所有结点
          Queue<TreeNode> queue = new LinkedList<>();
          // 先放入根节点
          queue.offer(root);
          while(!queue.isEmpty()) {
              // 收集当前层的所有结点的值
              ArrayList<Integer> list = new ArrayList<>();
              // ·当前层的节点数量
              int count = queue.size();
              // 遍历每一层
              while(count-- > 0) {
                  // 从对头取出节点
                  TreeNode node = queue.poll();
                  // 收集结果
                  list.add(node.val);
                  // 左右节点按顺序加到队尾
                  if(node.left != null) {
                      queue.offer(node.left);
                  }
                  if(node.right != null) {
                      queue.offer(node.right);
                  }
              }
              res.add(list);
          }
          return res;
      }
  }
  ```

  

### 8.6 按照之字顺序打印二叉树

- 描述

  给定一个二叉树，返回该二叉树的之字形层序遍历，（第一层从左向右，下一层从右向左，一直这样交替）

- 代码（[在层序遍历的基础上修改](#按照之字顺序打印二叉树)）

  ```java
  import java.util.*;
  import java.util.ArrayList;
  public class Solution {
      public ArrayList<ArrayList<Integer> > Print(TreeNode pRoot) {
          
          ArrayList<ArrayList<Integer>> res = new ArrayList();
          ArrayList<Integer> valPath = new ArrayList();
          ArrayList<TreeNode> path = new ArrayList();
          ArrayList<TreeNode> temp = new ArrayList();
          boolean flag = true;
          if(pRoot == null) return res;
          temp.add(pRoot);
          valPath.add(pRoot.val);
          res.add(new ArrayList<Integer>(valPath));//不可直接res.add(valPath),之后改变valPath的值，res也会随之改变
          valPath.clear();
          while (temp.size() != 0) {
  
              for (int i = 0 ; i < temp.size() ; i++) {
                  if (temp.get(i).left != null) {
                      path.add(temp.get(i).left);
                      valPath.add(temp.get(i).left.val);
                  }
                  if (temp.get(i).right != null) {
                      path.add(temp.get(i).right);
                      valPath.add(temp.get(i).right.val);
                  }
              }
              if(valPath.size() == 0) break;
              //用flag来判断打印的顺序
              if(flag){
                   Collections.reverse(valPath);
                  flag = !flag;
              }else{
                  flag = !flag;
              }
              res.add(new ArrayList<Integer>(valPath));
              valPath.clear();
              temp.clear();
              for (int i = 0 ; i < path.size() ; i++) {
                  temp.add(path.get(i));
              }
              path.clear();
  
          }
          return res;   
      }
  }
  ```

### 8.7 二叉树的最大深度

- 描述

  求给定二叉树的最大深度，深度是指树的根节点到任一叶子节点路径上节点的数量。

  数据范围：0≤n≤100000，树上每个节点的val满足|val|≤100

  时间复杂度O(n)

- 代码

  - (自己写的)

    ```java
    import java.util.*;
    public class Solution {
       
        public int maxDepth (TreeNode root) {
            if(root == null) return 0;
            return dfs(root);
        } 
        public int  dfs(TreeNode root){
            if(root.left != null && root.right != null){
                 return Math.max(dfs(root.left),dfs(root.right)) + 1 ;
            }else if(root.left == null && root.right != null){
                return  dfs(root.right) + 1;
            }else if(root.right == null && root.left != null){
                 return  dfs(root.left) + 1;
            }
               return 1;
        }
    }
    ```

    

  - 别人的

    ```java
    public int maxDepth(TreeNode root) {
            if(root==null)
                return 0;
            return 1+Math.max(maxDepth(root.left), maxDepth(root.right));
        }
    ```

### 8.8二叉树中和为某一值的路径（一）

- 描述

  给定一个二叉树root和一个值sum，判断是否有从根节点到叶子节点的节点值之和等于sum的路径。

  - 该题路径定义为从树的根节点开一直到叶子节点所经过的节点
  - 叶子节点是指没有字节点的节点
  - 路径只能从父节点到子节点，不能从子节点到父节点
  - 总结点数目为n

  例如：

  给出如下的为二叉树，sum = 22

  ![img](Datastructureandalgorithm.assets/999991351_1596786493913_8BFB3E9513755565DC67D86744BB6159.png)

  返回true，因为存在一条路径 5→4→11→2的节点值之和为 22

  数据范围：

  1.树上的节点数满足0≤*n*≤10000

  2.每个节点的值都满足∣val∣≤1000

  要求：空间复杂度 O(n)，时间复杂度 O(n)

  进阶：空间复杂度 O(树的高度)，时间复杂度 O(n)

- 思路（dfs）

  1、首先，深度优点遍历来说，先写上一个回溯 if (curNode == null) { return false; }，这表示递归至最深层开始回溯，至于为什么 return false 后面再讲
  2、每次进入函数时，将 sum 减去当前节点的权重(curNode.val)，当 sum 减到零时，说明目标路径存在，另外我们的目标是到叶子节点停止，叶子节点的条件是 curNode.left == null && curNode.right == null，所以说当 if (curNode.left == null && curNode.right == null && target == 0) ，我们返回 true 表示找到目标路径
  3、深度遍历的分支：对于当前节点 curNode 有两个分支，这两个分支都有可能成为目标路径，所以深度优先遍历的写法为 return dfs(curNode.left, target) || dfs(curNode.right, target);
  4、现在来谈谈为什么回溯时需要返回 false，因为当 curNode 为叶子节点时，并且 sum == 0 时，我们已经返回了 true，剩下的情况就是 curNode 不是叶子节点或者路径值不为 target，所应该返回 false

  ![img](Datastructureandalgorithm.assets/F12FF710F27F938492D6965EA63ADF43.png)

- 代码

  ```java
  public class Solution {
      /**
       * 
       * @param root TreeNode类 
       * @param sum int整型 
       * @return bool布尔型
       */
      public boolean hasPathSum (TreeNode root, int sum) {
          // write code here
          if (root == null) {
              return false;
          }
          // 深度优先遍历
          return dfs(root, sum);
      }
      
      private boolean dfs(TreeNode curNode, int target) {
          // 目标路径不存在，开始回溯
          if (curNode == null) {
              return false;
          }
          // 更新目标值
          target -= curNode.val;
          // 当当前节点为叶子节点并且目标路径存在时，返回 true
          if (curNode.left == null && curNode.right == null && target == 0) {
              return true;
          }
          // 对左右分支进行 dfs
          return dfs(curNode.left, target) || dfs(curNode.right, target);
      }
  }
  ```

### 8.9 二叉搜索树与双向链表

- 描述

  输入一棵二叉搜索树，将该二叉树转换成一个排序的双向链表。如下图所示：

  ![img](Datastructureandalgorithm.assets/E1F1270919D292C9F48F51975FD07CE2.png)

  数据范围：输入二叉树的节点数0≤*n*≤1000，二叉树中每个节点的值 0≤val≤1000
  要求：空间复杂度O(1)（即在原树上操作），时间复杂度 O(n)

  注意:

  1.要求不能创建任何新的结点，只能调整树中结点指针的指向。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继
  2.返回链表中的第一个节点的指针
  3.函数返回的TreeNode，有左右指针，其实可以看成一个双向链表的数据结构

  4.你不用输出双向链表，程序会根据你的返回值自动打印输出

- 思路（二叉排序树又叫二叉搜索树的中序遍历是递增的）
  - 中序遍历的节点存放在ArrayList中
  - 处理拼接集合中存放的节点

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
      ArrayList<TreeNode> res = new ArrayList();
      public TreeNode Convert(TreeNode pRootOfTree) {
          if(pRootOfTree == null || pRootOfTree.left == null && pRootOfTree.right == null ) return pRootOfTree;
          preOrder(pRootOfTree);
          res.get(0).left = null;
          res.get(0).right = res.get(1);
          for(int i = 1 ; i < res.size() ; i++){
              res.get(i).left = res.get(i-1);
              if(i != res.size() - 1){
                  res.get(i).right = res.get(i+1);
              } 
          }
          return res.get(0);
          
      }
      
      public void preOrder(TreeNode root){
          
          if(root.left != null){
              preOrder(root.left);
          }
                 res.add(root);
          if(root.right != null){
              preOrder(root.right);
          }
   
      }
  }
  ```

### 8.10 对称的二叉树

- 描述

  给定一棵二叉树，判断其是否是自身的镜像（即：是否对称）

  数据范围：节点数满足 0≤*n*≤1000，节点上的值满足∣val∣≤1000

  要求：空间复杂度 O(n)，时间复杂度 O(n)

- 自己的代码

  ```java
  import java.util.*;
  public class Solution {
      boolean isSymmetrical(TreeNode pRoot) {
          if(pRoot == null) return true;
          return dfs(pRoot.left,pRoot.right);
      }
      
      public boolean dfs(TreeNode left , TreeNode right){
          if(left == null && right ==null) return true;//递归到叶子节点，开始返回状态
          if(left == null && right != null || right == null && left != null ) return false;
          if(left.val == right.val){
             return dfs(left.left , right.right)&&dfs(left.right , right.left);
         }else{
              return false;
          }
          
      }
  }
  ```

### 8.11 合并二叉树

- 描述

  已知两棵二叉树，将他们合并一棵二叉树，合并规则是：都存在的节点，就将节点值加起来，否则空的位置就由另一个树的节点来代替

  数据范围：树上节点数量满足0≤*n*≤500，树上节点的值一定在32位整型范围内。

  进阶：空间复杂度 O(1) ，时间复杂度 O(n)

- 代码

  ```java
     import java.util.*;
  public class Solution {
         public TreeNode mergeTrees (TreeNode t1, TreeNode t2) {
          if(t1 == null) return t2;
          if(t2 == null) return t1;
          t1.val += t2.val;
          t1.left = mergeTrees(t1.left, t2.left);
          t1.right = mergeTrees(t1.right, t2.right);
          return t1;
      }
  }
  ```

### 8.12 二叉树的镜像

- 描述

  操作给定的二叉树，将其变换为源二叉树的镜像。

  数据范围：二叉树的节点数 0≤*n*≤1000 ， 二叉树每个节点的值0≤val≤1000

  要求： 空间复杂度 O(n)。本题也有原地操作，即空间复杂度 O(1) 的解法，时间复杂度 O(n)

  ![img](Datastructureandalgorithm.assets/420B82546CFC9760B45DD65BA9244888.png)

  ![img](Datastructureandalgorithm.assets/AD8C4CC119B15070FA1DBAA1EBE8FC2A.png)

- 自己的代码

  ```java
  import java.util.*;
  
  public class Solution {
      
       TreeNode temp = null;
      public TreeNode Mirror (TreeNode pRoot) {
         
          if(pRoot==null || pRoot.left == null&& pRoot.right == null) return pRoot;
          mirror(pRoot);
          return pRoot;
      }
      
      public void mirror(TreeNode root){
         if(root == null) return;//镜像到子节点就return
          temp = root.left;
          root.left = root.right;
          root.right = temp;
          mirror(root.left);
          mirror(root.right);
      
      }
      
  }
  ```

### 8.13 判断是不是二叉搜索树

- 描述

  给定一个二叉树的根节点，请你判断这棵树是不是二叉搜索树。

  数据范围：节点数量满足1≤n＜10^4^,节点上的值满足-2^31^≤val≤2^31^-1

- 思路

  - step 1：首先递归到最左，初始化maxLeft与pre。
  - step 2：然后往后遍历整棵树，依次连接pre与当前节点，并更新pre。
  - step 3：左子树如果不是二叉搜索树返回false。
  - step 4：判断当前节点是不是小于前置节点，更新前置节点。
  - step 5：最后由右子树的后面节点决定。

- 代码

  ```java
  import java.util.*;
  public class Solution {
      int pre = Integer.MIN_VALUE;
      //中序遍历
      public boolean isValidBST (TreeNode root) { 
          if (root == null)
              return true;
          //先进入左子树
          if(!isValidBST(root.left)) 
              return false;
          if(root.val < pre)
              return false;
          //更新最值
          pre = root.val;
          //再进入右子树
          return isValidBST(root.right); 
      }
  }
  ```

### 8.14 判断是不是完全二叉树

- 描述

  给定一个二叉树，确定他是否是一个完全二叉树。

  完全二叉树的定义：若二叉树的深度为h，除第h层外，其他各层的节点数都达到最大个数，第h层所有的**叶子节点都连续集中在最左边**，这就是完全二叉树。数据范围：节点数满足1≤n≤100

- 思路

  - step 1：先判断空树一定是完全二叉树。

  - step 2：初始化一个队列辅助层次遍历，将根节点加入。

  - step 3：逐渐从队列中弹出元素访问节点，如果遇到某个节点为空，进行标记，代表到了完全二叉树的最下层，若是后续还有访问，则说明提前出现了叶子节点，不符合完全二叉树的性质。

  - step 4：否则，继续加入左右子节点进入队列排队，等待访问。

    ![alt](Datastructureandalgorithm.assets/07986E476EB2CECD3C5F81D0BCADBE12.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public boolean isCompleteTree (TreeNode root) {
          //空树一定是完全二叉树
          if(root == null) 
              return true;
          //辅助队列
          Queue<TreeNode> queue = new LinkedList<>(); 
          queue.offer(root);
          TreeNode cur;
          //定义一个首次出现的标记位
          boolean notComplete = false;
          while(!queue.isEmpty()){
              cur = queue.poll();
              //标记第一次遇到空节点
              if(cur == null){ 
                  notComplete = true;
                  continue;
              }
              //后续访问已经遇到空节点了，说明经过了叶子
              if(notComplete) 
                  return false;
              queue.offer(cur.left);
              queue.offer(cur.right);
          }
          return true;
      }
  }
  ```

### 8.15 判断是不是平衡二叉树

- 描述

  输入一棵节点数为n的二叉树，判断该二叉树是否是平衡二叉树，在这里，我们只需要考虑其平衡性，不需要考虑是不是排序二叉树。

  平衡二叉树：它是一棵空树，或者它的左右两个字数的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

  数据范围：n≤100，树上的节点的val值满足0≤n≤1000

  空间复杂度O(1),时间复杂度O(n)

- 思路

  这道题目其实跟[二叉树的深度](https://www.nowcoder.com/practice/435fb86331474282a3499955f0a41e8b?tpId=13&&tqId=11191&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)这道题用到的方法是一样的，为什么说是一样的呢？因为我们求二叉树的深度，其实就是求了左右子树的深度的最大值，但是这道题目是要让我们判断二叉树是不是平衡树。

  我们都知道如何判断一棵二叉树是不是平衡二叉树，就是它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。所以，这个时候我们只需要判断左右子树的深度之差有没有超过1，若超过了则不是平衡的，反之则为平衡二叉树。

  我们只需要在上面的代码加上判断左右子树的深度之差即可。

  ```java
  (左子树深度-右子树深度) > 1，不是平衡树
  ```

  ![39](Datastructureandalgorithm.assets/39.gif)

- 代码

  ```java
  public class Solution {
      boolean isBalanced = true;
      public boolean IsBalanced_Solution(TreeNode root) {
          TreeDepth(root);
          return isBalanced;
      }
  
      public int TreeDepth(TreeNode root) {
          if(root == null)
              return 0;
          int l = TreeDepth(root.left);
          if(l == -1)  return -1;  // 提前返回
          int r = TreeDepth(root.right);
          if(r == -1)  return -1;  // 提前返回
          if(Math.abs(l-r) > 1){
              isBalanced = false;  // 不是平衡树
              return -1;  // 加一个标记-1，已经不可能是平衡树了
          }
  
          return Math.max(l,r)+1;
      }
  }
  ```

### 8.16 二叉搜索树的最近公共祖先

- 给定一个二叉搜索树，找到该树中两个指定节点的最近公共祖先

  1.对于该题的最近的公共祖先定义:对于有根树T的两个节点p、q，最近公共祖先LCA(T,p,q)表示一个节点x，满足x是p和q的祖先且x的深度尽可能大。在这里，一个节点也可以是它自己的祖先.

  2.二叉搜索树是若它的左子树不空，则左子树上所有节点的值均小于它的根节点的值； 若它的右子树不空，则右子树上所有节点的值均大于它的根节点的值

  3.所有节点的值都是唯一的。

  4.p、q 为不同节点且均存在于给定的二叉搜索树中。

  数据范围:3<=节点总数<=10000，0<=节点值<=10000

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public TreeNode commonAncestor (TreeNode root, int p, int q) {
          if (null == root) return null;
          if (root.val == p || root.val == q) return root;
          // 通过递归假设我们知道了运算结果 题目含义是不会出现重复节点
          if (p < root.val && q < root.val) return commonAncestor(root.left, p, q);
          else if (p > root.val && q > root.val) return commonAncestor(root.right, p, q);
          else return root;
      } 
      public int lowestCommonAncestor (TreeNode root, int p, int q) {
          // write code here
          return commonAncestor(root, p, q).val;
      }
  }
  ```

### 8.17 在二叉树中找到两个节点的最近公共祖先

- 描述

  给定一棵二叉树，（保证非空）以及这棵树上的 两个节点对应的val值O1和O2,请找到O1和O2的最近公共祖先节点。

  注：本题保证二叉树中每个节点的val值均不相同。

  数据范围：树上节点满足1≤n≤10^5^,节点值val满足区间[0,n]

  时间复杂度O(n)

  ```java
  import java.util.*;
  public class Solution {
       public TreeNode commonAncestor (TreeNode root, int p, int q) {
          if (null == root) return null;
          if (root.val == p || root.val == q) return root;
          // 通过递归假设我们知道了运算结果 题目含义是不会出现重复节点
          TreeNode left = commonAncestor(root.left, p, q);
          TreeNode right = commonAncestor(root.right, p, q);
          //如果左找不到p和q，就返回右边递归的结果
           if (left == null) return right;
          else if (right == null) return left;
           //如果p和q分布在root的左右两边，那么久返回root
          else return root;
      } 
      public int lowestCommonAncestor (TreeNode root, int p, int q) {
          // write code here
          return commonAncestor(root, p, q).val;
      }
  }
  ```

### 8.18 重建二叉树

- 描述

  给定节点数为n的二叉树的前序遍历和中序遍历结果，请重建出该二叉树并返回它的头结点。

  数据范围：n*≤2000，节点的值 −10000≤*val≤10000

  要求：空间复杂度 O(n)，时间复杂度 O(n)

  例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建出如下图所示。

  ![img](Datastructureandalgorithm.assets/776B0E5E0FAD11A6F15004B29DA5E628.png)

- 思路

  二叉树的前序遍历：根左右；中序遍历：左根右
  由前序遍历知道根节点之后，能在中序遍历上划分出左子树和右子树。分别对中序遍历的左右子树递归进行这一过程即可建树。

  - step 1：先根据前序遍历第一个点建立根节点。
  - step 2：然后遍历中序遍历找到根节点在数组中的位置。
  - step 3：再按照子树的节点数将两个遍历的序列分割成子数组，将子数组送入函数建立子树。
  - step 4：直到子树的序列长度为0，结束递归。

  ![img](Datastructureandalgorithm.assets/6A2A5DE961CF71A6B05079D595EBD1B6.png)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public TreeNode reConstructBinaryTree(int [] pre,int [] vin) {
          int n = pre.length;
          int m = vin.length;
          //每个遍历都不能为0
          if(n == 0 || m == 0) 
              return null;
          //构建根节点
          TreeNode root = new TreeNode(pre[0]);
          for(int i = 0; i < vin.length; i++){
              //找到中序遍历中的前序第一个元素
              if(pre[0] == vin[i]){ 
                  //构建左子树
                  root.left = reConstructBinaryTree(Arrays.copyOfRange(pre, 1, i + 1), Arrays.copyOfRange(vin, 0, i)); 
                  //构建右子树
                  root.right = reConstructBinaryTree(Arrays.copyOfRange(pre, i + 1, pre.length), Arrays.copyOfRange(vin, i + 1, vin.length));
                  break;
              }
          }
          return root;
      }
  }
  
  ```

### 8.19 输出二叉树的右视图

- 描述

  请根据二叉树的前序遍历，中序遍历恢复二叉树，并打印出二叉树的右视图

  数据范围：0≤n≤10000

  要求：时间复杂度O(n)，空间复杂度O(n)

  如输入[1,2,4,5,3],[4,2,5,1,3]时，通过前序遍历的结果[1,2,4,5,3]和中序遍历的结果[4,2,5,1,3]可重建出以下二叉树：

  ![img](Datastructureandalgorithm.assets/10FB15C77258A991B0028080A64FB42D.png)

​	所以对应的输出为[1,3,5]

```java
import java.util.*;
public class Solution {
    public int[] solve (int[] xianxu, int[] zhongxu) {
        List<Integer> resList =  rightSideView(reConstructBinaryTree(xianxu,zhongxu));
        int[] res = new int[resList.size()];
        for(int i = 0 ; i < resList.size() ; i++){
            res[i] = resList.get(i);
        }
        return res;


    }
	//构建二叉树
    public TreeNode reConstructBinaryTree(int [] pre,int [] vin) {
        int n = pre.length;
        int m = vin.length;
        //每个遍历都不能为0
        if(n == 0 || m == 0) 
            return null;
        //构建根节点
        TreeNode root = new TreeNode(pre[0]);
        for(int i = 0; i < vin.length; i++){
            //找到中序遍历中的前序第一个元素
            if(pre[0] == vin[i]){ 
                //构建左子树
                root.left = reConstructBinaryTree(Arrays.copyOfRange(pre, 1, i + 1), Arrays.copyOfRange(vin, 0, i)); 
                //构建右子树
                root.right = reConstructBinaryTree(Arrays.copyOfRange(pre, i + 1, pre.length), Arrays.copyOfRange(vin, i + 1, vin.length));
                break;
            }
        }
        return root;
    }

		//层序遍历出二叉树每一层最后的值来构建右视图
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
                if (i == size - 1) {  //将当前层的最后一个节点放入结果列表
                    res.add(node.val);
                }
            }
        }
        return res;
    }


}
```



### 8.20 二叉树的遍历、查找与删除结点

- 遍历

  前序遍历: **先输出父结点**，再遍历左子树和右子树（判断左右子树是否存在）

  中序遍历: 先遍历左子树，**再输出父结点**，再遍历右子树

  后序遍历: 先遍历左子树，再遍历右子树，**最后输出父结点**

  **小结**: 看输出父结点的顺序，就确定是前序，中序还是后序

  ![image-20210728221811659](Datastructureandalgorithm.assets/image-20210728221811659.png)

  前序遍历A-B-D-F-G-H-I-E-C

  中序遍历F-D-H-G-I-B-E-A-C

  后序遍历F-H-I-G-D-E-B-C-A

- 查找

  与前、中、后序遍历类似，但在递归时需注意找到目的结点后再return

- 删除

  （如果删除的结点是叶子结点，则删除该结点，如果删除的结点是非叶子结点，则删除该子树）

  二叉树是单向的，所以是判断当前结点的子结点是否是需要删除的结点

  如果当前结点的左子结点不为空，是需要删除的结点，则将其置空，结束递归，否则向左子树递归

  如果当前结点的右子结点不为空，是需要删除的结点，则将其置空，结束递归，否则向右子树递归

  root结点没有父结点，需要单独判断

```java
* @description: 二叉树前中后序遍历与查找、删除
 */
public class BinaryTreeDemo {
    public static void main(String[] args) {
        //先创建一个二叉树
        BinaryTree binaryTree = new BinaryTree();
        HeroNode heroNode = new HeroNode(1,"sd");
        HeroNode heroNode1 = new HeroNode(2,"nc");
        HeroNode heroNode2 = new HeroNode(3,"kd");
        HeroNode heroNode3 = new HeroNode(4,"ac");
        HeroNode heroNode4 = new HeroNode(5,"ef");

        binaryTree.setRoot(heroNode);
        heroNode.setLeft(heroNode1);
        heroNode.setRight(heroNode2);
        heroNode2.setLeft(heroNode3);
        heroNode2.setRight(heroNode4);

        System.out.println("preOrder");
        binaryTree.preOrder();

        System.out.println("preOrderSearch");
        HeroNode heroNode5 = binaryTree.postOrderSearch(3);
        if (heroNode5 == null) {
            System.out.println("NotFound");
        } else {
            System.out.println(heroNode5);
        }

        System.out.println("delNode");
        binaryTree.delNode(3);
        binaryTree.preOrder();

    }
}

//定义二叉树
class BinaryTree {
    private HeroNode root;

    //定义根结点
    public void setRoot(HeroNode root) {
        this.root = root;
    }

    //前序遍历
    public void preOrder() {
        root.preOrder();
    }
    //中序遍历
    public void midOrder() {
        root.midOrder();
    }
    //后序遍历
    public void postOrder() {
        root.postOrder();
    }

    //前序遍历查找
    public HeroNode preOrderSearch(int no) {
        return root.preOrderSearch(no);
    }
    //中序遍历查找
    public HeroNode midOrderSearch(int no) {
        return root.midOrderSearch(no);
    }
    //后序遍历查找
    public HeroNode postOrderSearch(int no) {
        return root.postOrderSearch(no);
    }

    //删除结点
    public void delNode(int no) {
        if (root != null) {
            //需要对root结点单独判断，因为其无父结点
            if (root.getNo() == no) {
                root = null;
            } else {
                root.delNode(no);
            }
        } else {
            System.out.println("Empty tree!");
        }
    }
}

//树的一个结点
class HeroNode {
    private int no;
    private String name;
    private HeroNode left;
    private HeroNode right;

    public HeroNode(int no, String name) {
        this.no = no;
        this.name = name;
    }

    public int getNo() {
        return no;
    }

    public void setLeft(HeroNode left) {
        this.left = left;
    }

    public void setRight(HeroNode right) {
        this.right = right;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }

    //前序遍历方法
    public void preOrder() {
        System.out.println(this);
        //递归向左
        if (this.left != null) {
            this.left.preOrder();
        }
        //递归向右
        if (this.right != null) {
            this.right.preOrder();
        }
    }

    //中序遍历方法
    public void midOrder() {
        //递归向左
        if (this.left != null) {
            this.left.midOrder();
        }
        System.out.println(this);
        //递归向右
        if (this.right != null) {
            this.right.midOrder();
        }
    }

    //后序遍历方法
    public void postOrder() {
        //递归向左
        if (this.left != null) {
            this.left.postOrder();
        }
        //递归向右
        if (this.right != null) {
            this.right.postOrder();
        }
        System.out.println(this);
    }

    //前序遍历查找
    public HeroNode preOrderSearch(int no) {
        if (this.no == no) {
            return this;
        }
        if (this.left != null) {
            //找到了再return
            if (this.left.preOrderSearch(no) != null) {
                return this.left.preOrderSearch(no);
            }
        }
        if (this.right != null) {
            return this.right.preOrderSearch(no);
        }
        return null;
    }

    //中序遍历查找
    public HeroNode midOrderSearch(int no) {
        if (this.left != null) {
            //如果左边没找到
            if (this.left.midOrderSearch(no) != null) {
                return this.left.midOrderSearch(no);
            }
        }
        if (this.no == no) {
            return this;
        }
        if (this.right != null) {
            return this.right.midOrderSearch(no);
        }
        return null;
    }

    //后序遍历查找
    public HeroNode postOrderSearch(int no) {
        if (this.left != null) {
            if (this.left.postOrderSearch(no) != null) {
                return this.left.postOrderSearch(no);
            }
        }
        if (this.right != null) {
            if (this.right.postOrderSearch(no) != null) {
                return this.right.postOrderSearch(no);
            }
        }
        if (this.no == no) {
            return this;
        }
        return null;
    }

    //删除结点
    public void delNode(int no) {
        if (this.left != null && this.left.no == no) {
            this.left = null;
            return;
        }
        if (this.right != null && this.right.no == no) {
            this.right = null;
            return;
        }
        //向左、右子树递归
        if (this.left != null) {
            this.left.delNode(no);
        }
        if (this.right != null) {
            this.right.delNode(no);
        }

    }
}
```



### 8.21 顺序存储二叉树

![image-20210526202744674](Datastructureandalgorithm.assets/image-20210526202744674.png)

- **数组存储方式**和**树**的存储方式可以相互转换，在遍历时也可以按照**前序遍历**，**中序遍历**和**后序遍历**的方式

- 顺序存储二叉树的**特点**：

  顺序二叉树通常只考虑完全二叉树

  第n个元素的左子结点为 2 * n + 1(编号)

  第n个元素的右子结点为 2 * n + 2(编号)

  第n个元素的父结点为 (n-1) / 2(编号)

  n : 表示二叉树中的第几个元素(按0开始编号)

```java
public class ArrBinaryTreeDemo {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        ArrBinaryTree arrBinaryTree = new ArrBinaryTree(arr);
        arrBinaryTree.preOrder();
    }
}

class ArrBinaryTree {
    private int[] arr;

    public ArrBinaryTree(int[] arr) {
        this.arr = arr;
    }

    /**
     * @param index: 数组的下标
     * @return void:
     * @Description: 前序递归遍历
     */
    //前序遍历
    public void preOrder(int index) {
        if (arr == null && arr.length == 0) {
            System.out.println("数组为空");
        }
        System.out.println(arr[index]);
        //向左递归遍历
        if ((index * 2 + 1) < arr.length) {
            preOrder(index * 2 + 1);
        }
        //向右递归遍历
        if ((index * 2 + 2 < arr.length)) {
            preOrder(index * 2 + 2);
        }
    }

    //重载（arrBinaryTree.preOrder();即开始遍历）
    public void preOrder() {
        this.preOrder(0);
    }
}
```



### 8.22 线索化二叉树

- n个结点的二叉链表中含有n+1 【 2n-(n-1)=n+1】 个空指针域。利用二叉链表中的空指针域，存放指向该结点在**某种遍历次序**下的**前驱**和**后继**结点的指针（这种附加的指针称为"线索"），**线索二叉树**(Threaded  BinaryTree)

- 因为线索化后，各个结点指向有变化，因此**原来的遍历方式不能使用**，各个结点可以**通过线型方式遍历**，因此**无需使用递归**方式，这样也提高了遍历的效率

- 中序遍历的结果：{8, 3, 10, 1, 14, 6}

  前序遍历的结果：{1, 3, 8, 10, 6, 14}

  后序遍历的结果：{6, 14, 10, 8, 3, 1}

![image-20210526203151815](Datastructureandalgorithm.assets/image-20210526203151815.png)

![image-20210526203207137](Datastructureandalgorithm.assets/image-20210526203207137.png)

```java
public class ThreadedBinaryTreeDemo {
    public static void main(String[] args) {
        HeroNode heroNode = new HeroNode(1,"sd");
        HeroNode heroNode1 = new HeroNode(3,"nc");
        HeroNode heroNode2 = new HeroNode(6,"kd");
        HeroNode heroNode3 = new HeroNode(8,"ac");
        HeroNode heroNode4 = new HeroNode(11,"ef");
        HeroNode heroNode5 = new HeroNode(14,"jm");
        BinaryTree binaryTree = new BinaryTree();
        binaryTree.setRoot(heroNode);
        heroNode.setLeft(heroNode1);
        heroNode.setRight(heroNode2);
        heroNode1.setLeft(heroNode3);
        heroNode1.setRight(heroNode4);
        heroNode2.setLeft(heroNode5);

        //线索化二叉树
        binaryTree.threadedNodes(heroNode);
        //测试是否完成线索化(14的前驱结点是1)
        System.out.println(heroNode5.getLeft());
        //使用线索化方式遍历线索化二叉树
        System.out.println("使用线索化方式遍历线索化二叉树");
        binaryTree.threadedlist();
    }
}

//定义线索化二叉树
class BinaryTree {
    private HeroNode root;
    
    //为了实现线索化，需要创建给指向当前结点的前驱结点的指针
    //在递归进行线索化时，始终保存前驱结点
    private HeroNode pre = null;

    public void setRoot(HeroNode root) {
        this.root = root;
    }

    //编写对二叉树进行中序线索化的方法（递归）
    //先遍历左子树，再父结点，再遍历右子树
    public void threadedNodes(HeroNode node) {
        if (node == null) {
            return;
        }
        //(1)先线索化左子树
        threadedNodes(node.getLeft());
        //(2)再线索化当前结点的左指针和对应前驱结点的右指针
        if (node.getLeft() == null) {
            //左指针指向前驱结点
            node.setLeft(pre);
            node.setLeftType(1);
        }
        if (pre != null && pre.getRight() == null) {
            //让前驱结点的右指针指向当前结点
            pre.setRight(node);
            pre.setRightType(1);
        }
        //每处理一个结点后，移动前驱结点
        pre = node;
        //(3)再线索化右子树
        threadedNodes(node.getRight());
    }

    //中序遍历线索化二叉树的方法（非递归）
    public void threadedlist() {
        //定义一个变量，存储当前遍历的结点
        HeroNode node = root;
        
        //线索化后，第一个结点前驱结点为null，最后一个结点后继结点为null
        while (node != null) {
            //循环找到leftType == 1的结点，第一个找到的就是8结点
            //(被线索化处理后但没有前驱结点的点)

            while (node.getLeftType() == 0) {
                node = node.getLeft();
            }
            //打印当前这个结点
            System.out.println(node);
            //如果当前结点的右指针指的是后继结点，就一直输出
            while (node.getRightType() == 1) {
                node = node.getRight();
                System.out.println(node);
            }
            /// 若已经没有后继结点，将当前结点转换为其右结点。
            node = node.getRight();
        }
    }
}

//树的一个结点
class HeroNode {
    private int no;
    private String name;
    private HeroNode left;
    private HeroNode right;
    //0--left是左子树  1--left是前驱结点
    private int leftType;
    //0--right是右子树  1--right是后驱结点
    private int rightType;

    public HeroNode(int no, String name) {
        this.no = no;
        this.name = name;
    }

    public void setLeft(HeroNode left) {
        this.left = left;
    }

    public void setRight(HeroNode right) {
        this.right = right;
    }

    public void setLeftType(int leftType) {
        this.leftType = leftType;
    }

    public void setRightType(int rightType) {
        this.rightType = rightType;
    }

    public int getLeftType() {
        return leftType;
    }

    public int getRightType() {
        return rightType;
    }

    public HeroNode getLeft() {
        return left;
    }

    public HeroNode getRight() {
        return right;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }
}
```



### 8.23 堆排序

- 堆是具有以下性质的**完全二叉树**：每个结点的值都大于或等于其左右孩子结点的值，称为大顶堆, 每个结点的值都小于或等于其左右孩子结点的值，称为小顶堆

- 大顶堆举例说明：

  ![image-20210729151251530](Datastructureandalgorithm.assets/image-20210729151251530.png)

- 堆排序是一种**选择排序，**它的最坏，最好，平均时间复杂度均为O(nlogn)，它也是不稳定排序。

- 一般升序采用大顶堆，降序采用小顶堆。

- 堆排序基本思想（以升序为例）：
  - 首先将一个排序序列构造成一个大顶堆：
    - 从最后一个非叶子结点开始下沉，循环向前（相当于每次在堆顶加入一个新元素）
    - 每个非叶子结点的下沉是与其左右子结点比较并交换，非叶子结点的值不再交换时结束下沉
  - 此时大顶堆的堆顶元素为最大值，将其与末尾元素交换，此时待排序序列的长度-1
  - 末尾元素也是此大顶堆的一个新元素，继续向下沉得到新的大顶堆，重复这两个操作直至待排序序列的长度为1

```java
public class HeapSort {
    public static void main(String[] args) {
        int arr[] = {4, 6, 8, 5, 9};
        heapSort(arr);
    }

    /**
     * Description: 堆排序方法
     * @param arr:
     * @return void:
     */
    public static void heapSort(int arr[]) {
        int temp;
        //构造初始堆（升序采用大顶堆，降序采用小顶堆），从左到右，从下到上
        //i = arr.length / 2 - 1为最后一个非叶子结点
        for (int i = arr.length / 2 - 1; i >= 0; i--) {
            adjustHeap(arr,i, arr.length);
        }
        //将堆顶元素与末尾元素交换，此时只改变了堆顶元素的值，
        //所以从堆顶开始继续调整使其满足大顶堆的定义
        for (int j = arr.length - 1; j > 0; j--) {
            temp = arr[j];
            arr[j] = arr[0];
            arr[0] = temp;
            adjustHeap(arr, 0, j);
        }
        System.out.println(Arrays.toString(arr));

    }

    /**
     * Description: 将【i对应的非叶子结点】下沉到合适位置
     *              (与其左右子结点比较，交换后指向其左右子结点再重复直至不交换break)
     *      若从最后一个非叶子结点向前进行此操作，即可构建大顶堆或小顶堆
     * {4, 6, 8, 5, 9}  i = 1 ->  {4, 9, 8, 5, 6}
     * @param arr:
     * @param i: 非叶子结点在数组的索引
     * @param length: 表示对数组前多少元素进行调整
     * @return void:
     */
    public static void adjustHeap(int arr[], int i, int length) {

        int temp = arr[i];
        //k = i * 2 + 1是i结点的左子结点，k = i * 2 + 2是i结点的右子结点
        for (int k = i * 2 + 1; k < length; k = k * 2 + 1) {
            if (k + 1 < length && arr[k] < arr[k + 1]) {  //左子结点的值小于右子结点
                //k指向右子结点
                k++;
            }
            if (arr[k] > temp) {    //如果子结点大于父结点
                arr[i] = arr[k];
                //将i指向k(k的值已经交换给了i)继续循环比较
                i = k;
            } else {
                break;
            }
        }
        //for循环结束后，已经将i为root的子树的最大值放在了最顶上
        arr[i] = temp;  //将temp值放到调整后的位置
    }
}
```



### 8.24 赫夫曼树

- 一些概念：

  - 路径：在一棵树中，从一个结点往下可以达到的孩子或孙子结点之间的通路
  - 路径长度：若规定根结点的层数为1，则从根结点到第L层结点的路径长度为L-1
  - 结点的权：将树中结点赋给一个有着某种含义的数值，则这个数值称为该结点的权
  - 带权路径长度：从**根结点**到该结点之间的**路径长度**与**该结点的权**的乘积
  - 树的带权路径长度：树的带权路径长度规定为**所有叶子结点的带权路径长度之和**，记为WPL(weighted path length) 

- **赫夫曼树(Huffman Tree)**：树的带权路径长度(WPL)最小，权值越大的结点离根结点越近的二叉树才是最优二叉树

- 创建赫夫曼树思路：

  - 将每一个数据构成一个结点（最简单的二叉树）加入List集合，按根结点权值从小到大进行排序
  - 取出根结点权值最小的两个二叉树，组成新的二叉树加入List集合，二叉树的根结点权值为两者之和，从List集合删除这两个二叉树
  - 再次按照根结点权值从小到大进行排序，重复这两个步骤，直至List集合只剩下一个元素，就是赫夫曼树的根结点
  - 由数列 {13, 7, 8, 3, 29, 6, 1}构成的赫夫曼树

  ![image-20210729223216180](Datastructureandalgorithm.assets/image-20210729223216180.png)

```java
public class HuffmanTree {
    public static void main(String[] args) {
        int[] arr = {13, 7, 8, 3, 29, 6, 1};
        Node root = createHuffmanTree(arr);
        root.preOrder();
    }

    //编写一个前序遍历的方法
    public static void preOrder(Node root) {
        if (root != null) {
            root.preOrder();
        } else {
            System.out.println("空树");
        }
    }

    //创建Huffman树的方法
    public static Node createHuffmanTree(int[] arr) {
        //遍历数组，将每个元素构成一个Node，将Node放入List
        List<Node> nodes = new ArrayList<>();
        for (int value : arr) {
            nodes.add(new Node(value));
        }

        while (nodes.size() > 1) {
            //排序从小到大(底层是快排)
            Collections.sort(nodes);
            //取出根结点最小的两颗二叉树(结点)
            Node leftNode = nodes.get(0);
            Node rightNode = nodes.get(1);
            //构建一个新的二叉树(两颗二叉树根结点值相加成为新结点、父结点)
            Node parent = new Node(leftNode.value + rightNode.value);
            parent.left = leftNode;
            parent.right = rightNode;
            //从ArrayList删除已经处理过的二叉树
            nodes.remove(leftNode);
            nodes.remove(rightNode);
            //将parent加入nodes
            nodes.add(parent);
        }
        //返回Huffman树的root结点
        return nodes.get(0);
    }

    //创建结点类
    //为了让Node对象支持排序，实现Comparable接口
    static class Node implements Comparable<Node>{
        int value;  //结点权值
        Node left;
        Node right;

        //前序遍历
        public void preOrder() {
            System.out.println(this);
            if (this.left != null) {
                this.left.preOrder();
            }
            if (this.right != null) {
                this.right.preOrder();
            }
        }

        public Node(int value) {
            this.value = value;
        }

        @Override
        public String toString() {
            return "Node{" +
                    "value=" + value +
                    '}';
        }

        @Override
        public int compareTo(Node o) {
            //从小到大排序
            return this.value - o.value;
        }
    }
}
```



### 8.25 赫夫曼编码

a）通信领域中信息的处理方式：

- 定长编码：每个字符对应的AscII码对应的8位的二进制
- 变长编码：各个字符出现的次数进行编码（0= , 1=a, 10=i, 11=e, 100=k, 101=l, 110=o, 111=v, 1000=j, 1001=u, 1010=y, 1011=d），原则是出现次数越多的，则编码越小，但不符合前缀编码
- 赫夫曼编码：按照字符出现的次数构建一颗赫夫曼树, 次数作为权值
  - 符合前缀编码：字符的编码都不能是其他字符编码的前缀
  - 如果文件本身就是经过压缩处理的，那么使用赫夫曼编码再压缩效率不会有明显变化, 比如视频,ppt 等等
  - 赫夫曼编码是按字节来处理的，因此可以处理所有的文件(二进制文件、文本文件)
  - 如果一个文件中的内容，重复的数据不多，压缩效果也不会很明显

 b）生成赫夫曼编码：

- 构建赫夫曼树结点类Node(属性Byte data；int weight；Node left；Node right；)

```java
//创建Node
class Node implements Comparable<Node>{

    Byte data;  //存放数据'a'->97 ' '->32
    int weight; //权值，字符数据出现的次数
    Node left;
    Node right;

    public Node(Byte data, int weight) {
        this.data = data;
        this.weight = weight;
    }

    //前序遍历
    public void preOrder() {
        System.out.println(this);
        if (this.left != null) {
            this.left.preOrder();
        }
        if (this.right != null) {
            this.right.preOrder();
        }
    }

    @Override
    public String toString() {
        return "Node{" +
                "data=" + data +
                ", weight=" + weight +
                '}';
    }

    @Override
    public int compareTo(Node o) {
        //从小到大排序
        return this.weight - o.weight;
    }
}
```

- 通过原始数据的字节数组，统计每个字符的权值（用Map统计），返回List\<Node>

```java
/**
 * Description: 接受一个字节数组，返回List
 * @param bytes:
 * @return java.util.List<huffmancode.Node>:
 */
private static List<Node> getNodes(byte[] bytes) {
    ArrayList<Node> nodes = new ArrayList<>();

    //存储每一个byte出现的次数（Map）
    HashMap<Byte, Integer> counts = new HashMap<>();
    for (byte b : bytes) {
        Integer count = counts.get(b);
        if (count == null) {
            counts.put(b, 1);
        } else {
            counts.put(b, count + 1);
        }
    }

    //把每个键值对转成一个Node对象并加入List集合
    for (Map.Entry<Byte, Integer> entry : counts.entrySet()) {
        nodes.add(new Node(entry.getKey(), entry.getValue()));
    }

    return nodes;
}
```

- 通过List\<Node>生成创建对应的Huffman树，返回代表Huffman树的根结点HuffmanRoot

```java
/**
 * Description: 通过List创建对应的Huffman树
 * @param nodes:
 * @return huffmancode.Node:
 */
private static Node createHuffmanTree(List<Node> nodes) {
    while (nodes.size() > 1) {
        //排序
        Collections.sort(nodes);
        //取出最小的两个二叉树,并创建一颗新的二叉树(只有权值，没有data)
        Node leftNode = nodes.get(0);
        Node rightNode = nodes.get(1);
        Node parent = new Node(null, leftNode.weight + rightNode.weight);
        parent.left = leftNode;
        parent.right = rightNode;
        //将新的二叉树加入List，从List删除使用过的两颗二叉树
        nodes.remove(leftNode);
        nodes.remove(rightNode);
        nodes.add(parent);
    }
    return nodes.get(0);
}
```

- 将传入Huffman树的所有叶子结点的赫夫曼编码得到，放入huffmanCodes集合Map<Byte, String>

```java
//生成赫夫曼树对应的赫夫曼编码表
//1.将赫夫曼编码表存放在Map<Byte,String>中
static Map<Byte, String> huffmanCodes = new HashMap<>();
//2.定义一个StringBuilder，存储某个叶子结点的路径
static StringBuilder stringBuilder = new StringBuilder();
//重载
private static Map<Byte, String> getCodes(Node root) {
    if (root == null) {
        return null;
    }
    getCodes(root,"",stringBuilder);
    return huffmanCodes;
}

/**
 * Description: 将传入node的所有叶子结点的赫夫曼编码得到，放入huffmanCodes集合
 * @param node: 传入结点
 * @param code: 路径：结点为左子结点：0，结点为右子结点：1
 * @param stringBuilder: 用于拼接路径
 * @return void:
 */
private static void getCodes(Node node, String code, StringBuilder stringBuilder) {
    StringBuilder stringBuilder1 = new StringBuilder(stringBuilder);
    stringBuilder1.append(code);
    if (node != null) { //如果node == null不处理
        //判断当前node是叶子结点还是非叶子结点
        if (node.data == null) {    //非叶子结点
            //递归处理
            //向左
            getCodes(node.left, "0", stringBuilder1);
            //向右
            getCodes(node.right, "1", stringBuilder1);
        } else {    //叶子结点
            huffmanCodes.put(node.data, stringBuilder1.toString());
        }
    }
}
```

 c）使用赫夫曼编码压缩数据：

```java
/**
 * Description: 把所有方法进行封装
 * @param bytes: 原始字符串对应的字节数组
 * @return byte[]: 经过赫夫曼编码处理过的字节数组（压缩过的数组）
 */
private static byte[] huffmanZip(byte[] bytes) {
    //将字符数组的转化成一个Node对象类型(字符数据与权值)的List集合
    List<Node> nodes = getNodes(bytes);
    //创建对应的赫夫曼树
    Node huffmanTreeRoot = createHuffmanTree(nodes);
    //根据赫夫曼树创建创建赫夫曼编码
    Map<Byte, String> huffmanCodes = getCodes(huffmanTreeRoot);
    //根据赫夫曼编码压缩得到赫夫曼编码处理过的字节数组（压缩过的数组）
    byte[] huffmanCodeBytes = zip(bytes, huffmanCodes);

    return huffmanCodeBytes;
}


/**
 * Description: 将字符串对应的byte[]数组，通过生成的赫夫曼编码表,返回赫夫曼编码压缩过的byte[]
 * @param bytes: 原始字符串对应的byte[]数组
 * @param huffmanCodes: 生成的赫夫曼编码Map
 * @return byte[]: 赫夫曼编码压缩过的byte[]，如byte[0]="10101000"(补码)补码等于反码+1
 */
private static byte[] zip(byte[] bytes, Map<Byte, String> huffmanCodes) {
    //1.利用 huffmanCodes 将 bytes 转成赫夫曼编码对应的字符串
    StringBuilder stringBuilder = new StringBuilder();

    for (byte b : bytes) {
        stringBuilder.append(huffmanCodes.get(b));
    }
    //System.out.println("strstringBuilder=" + stringBuilder);

    //2.将stringBuilder="1010100010111111110..."转化为byte[]
    //每8位对应一个byte
    int len = (stringBuilder.length() + 7) / 8;
    int index = 0;  //记录是第几个byte
    byte[] huffmanCodeBytes = new byte[len];

    for (int i = 0; i < stringBuilder.length(); i += 8) {
        String strByte;
        if (i + 8 >= stringBuilder.length()) {   //处理最后的一段
            //如"0010"转化为byte会丢失前面两个00，用zeroCount记录下来
            //存储到huffmanCodeBytes最后一项
            strByte = stringBuilder.substring(i);
        } else {
            strByte = stringBuilder.substring(i, i + 8);
        }
        //将strByte转成一个Byte,放入huffmanCodeBytes
        //由于计算机存储数据时，都是以补码的形式进行存储。
        //通常看到的数却是计算机存储的补码先转换成反码，后转换成原码，再转换成十进制呈现的。
        //正数和0的补码是其本身，负数补码是最高位不变，其他位按位取反再加1
        //当int32位类型强转为byte8位类型时, 存储的是10100111(补码)而不是原码
        //补码存储："(省略24位)10101000"-> 168 ->(byte)截取后8位 -> 11011000 -> -88
        huffmanCodeBytes[index] = (byte) Integer.parseInt(strByte, 2);
        index++;
    }
    return huffmanCodeBytes;
}
```

 d）使用赫夫曼编码解压数据：

```java
/**
 * Description: 解压
 * @param huffmanCodes: 赫夫曼编码表
 * @param huffmanBytes: 赫夫曼编码后的字节数组
 * @return byte[]: 原来字符串对应的字节数组
 */
private static byte[] deCode(Map<Byte, String> huffmanCodes, byte[] huffmanBytes) {
    //得到huffmanBytes对应的二进制字符串，形式如"1010100010111111110..."
    StringBuilder stringBuilder = new StringBuilder();
    for (int i = 0; i < huffmanBytes.length; i++) {
        //最后一个字节需要单独考虑
        if (i == huffmanBytes.length - 1) {
            stringBuilder.append(byteToBitString(false, huffmanBytes[i]));
        } else {
            stringBuilder.append(byteToBitString(true, huffmanBytes[i]));
        }
    }

    //把字符串按照赫夫曼编码解码
    //把赫夫曼编码调换，进行反向查询
    Map<String, Byte> map = new HashMap<>();
    for (Map.Entry<Byte, String> entry : huffmanCodes.entrySet()) {
        map.put(entry.getValue(), entry.getKey());
    }

    //创建集合，存放byte,再转化成数组（List长度可变）
    List<Byte> list = new ArrayList<>();
    int i = 0;  //赫夫曼编码后的字节数组索引
    while (i < stringBuilder.length()){
        int count = 1;
        boolean flag = true;
        Byte b = null;  //包装类可以存储null值
        while (flag) {
            //i不动，count++直到匹配到一个字符   [i, i + count)
            String key = stringBuilder.substring(i, i + count);
            b = map.get(key);
            if (b == null) {
                count++;
            } else {
                flag = false;
            }
        }
        list.add(b);
        i += count;
    }
    byte contentBytes[] = new byte[list.size()];
    for (int j = 0; j < contentBytes.length; j++) {
        contentBytes[j] = list.get(j);
    }
    return contentBytes;
}

/**
 * Description: 将一个byte转化为二进制字符串
 * @param flag: flase-表示不补高位（最后一个字节不补高位）
 * @param b: 传入的byte
 * @return java.lang.String: 对应的二进制的字符串（补码）
 */
private static String byteToBitString(boolean flag, byte b) {
    //将byte转化为int
    int temp = b;
    //非最后一个字节，如果是正数，不足8位，需要补高位
    if (flag) {
        temp |= 256;    //按位与 1 0000 0000
    }
    //返回的temp对应的二进制的**补码**字符串，与前面的补码相抵消
    String str = Integer.toBinaryString(temp);
    if (flag || temp < 0) { //非最后一个字节，或最后一个字节为负数
        //负数有32位，补位正数有9位，需要截取后8位
        return str.substring(str.length() - 8);
    } else {        //最后一个字节
        return str;
    }
}
```

 e）使用赫夫曼编码压缩文件：

```java
/**
 * Description: 使用赫夫曼编码压缩文件
 * @param srcFile: 待压缩文件位置
 * @param dstFile: 成功压缩后的文件位置
 * @return void:
 */
public static void zipFile(String srcFile, String dstFile) {
    FileInputStream fis = null;
    FileOutputStream fos = null;
    ObjectOutputStream oos = null;
    try {
        //创建文件输入流
        fis = new FileInputStream(srcFile);
        //创建一个与源文件大小一样的byte[]
        byte[] bytes = new byte[fis.available()];
        //读取文件
        fis.read(bytes);
        //直接对bytes压缩
        byte[] huffmanBytes = huffmanZip(bytes);
        //创建文件输出流
        fos = new FileOutputStream(dstFile);
        //创建一个与文件输出流相关联的ObjectOutputStream
        oos = new ObjectOutputStream(fos);
        //以对象流的方式写入文件（编码表和数据）
        //目的是恢复源文件时区分编码表和数据
        oos.writeObject(huffmanBytes);
        oos.writeObject(huffmanCodes);
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            if (oos != null) {
                oos.close();
            }
            if (fos != null) {
                fos.close();
            }
            if (fis != null) {
                fis.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

 f） 使用赫夫曼编码压缩文件：

```java
/**
 * Description: 解压文件
 * @param zipFile: 待解压文件位置
 * @param dstFile: 成功解压的文件位置
 * @return void:
 */
public static void unZipFile(String zipFile, String dstFile) {
    FileInputStream fis = null;
    ObjectInputStream ois = null;
    FileOutputStream fos = null;
    try {
        //文件输入流
        fis = new FileInputStream(zipFile);
        //与文件输入流相关联的对象输入流
        ois = new ObjectInputStream(fis);
        //读取byte[]数组(读取顺序与写入顺序一致)
        byte[] huffmanBytes = (byte[])ois.readObject();
        Map<Byte,String> huffmanCodes = (Map<Byte,String>)ois.readObject();
        //解码
        byte[] bytes = deCode(huffmanCodes, huffmanBytes);
        //将bytes写入目标文件
        fos = new FileOutputStream(dstFile);
        fos.write(bytes);
    } catch (IOException e) {
        e.printStackTrace();
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    } finally {
        try {
            if (fos != null) {
                fos.close();
            }
            if (ois != null) {
                ois.close();
            }
            if (fis != null) {
                fis.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



### 8.26 二叉排序树BST

- 介绍：
  - Binary Sort(Search) Tree，对于二叉排序树的任何一个非叶子结点，要求左子结点的值比当前结点的值小，右子结点的值比当前结点的值大。

  - 在二叉排序树的构建过程中，会造成对于任何一个非叶子结点，左子树的所有结点的值比当前结点的值小，右子树的所有结点的值比当前结点的值大，相同的值一般放在右子结点。

    ![image-20210802141308608](Datastructureandalgorithm.assets/image-20210802141308608.png)

  - 二叉排序树相较于顺序存储和链式存储能提高数据**存储，读取**的效率

    - 顺序存储如数组：
      - 优点：通过下标方式访问元素，速度快。**对于有序数组**，还可使用二分查找提高检索速度。
      - 缺点：如果要检索具体某个值，或者插入值(按一定顺序)**会整体移动**，效率较低
    - 链式存储：
      - 优点：在一定程度上对数组存储方式有优化(比如：插入一个数值结点，只需要将插入结点，链接到链表中即可， 删除效率也很好)。
      - 缺点：在进行检索时，效率仍然较低，比如(检索某个值，需要从头结点开始遍历) 

- 二叉排序树的创建与遍历：

```java
//测试
public class BinarySortTreeDemo {
    public static void main(String[] args) {
        int[] arr = {7, 3, 10, 12, 5, 1, 9};
        BinarySortTree binarySortTree = new BinarySortTree();
        for (int i = 0; i < arr.length; i++) {
            binarySortTree.add(new Node(arr[i]));
        }

        //中序遍历二叉排序树
        System.out.println("中序遍历二叉排序树");
        binarySortTree.midOrder();
    }
}

//二叉排序树
class BinarySortTree {
    private Node root;

    //添加结点
    public void add(Node node) {
        if (root == null) {
            root = node;
        } else {
            root.add(node);
        }
    }

    //中序遍历(c)
    public void midOrder() {
        if (root != null) {
            root.midOrder();
        } else {
            System.out.println("树空");
        }
    }
}

//结点
class Node {
    int value;
    Node left;
    Node right;

    public Node(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "Node{" +
                "value=" + value +
                '}';
    }
    
    //添加结点的方法
    //递归的方法，满足二叉排序树的要求
    public void add(Node node) {
        if (node == null) {
            return;
        }
        //判断传入的结点与当前子树根结点值的关系
        if (node.value < this.value) {
            if (this.left == null) {    //左子结点为空
                this.left = node;
            } else {
                //递归向左子树添加
                this.left.add(node);
            }
        } else {
            if (this.right == null) {
                this.right = node;
            } else {
                //递归向右子树添加
                this.right.add(node);
            }
        }
    }

    //中序遍历
    public void midOrder() {
        if (this.left != null) {
            this.left.midOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.midOrder();
        }
    }
}
```

- 二叉排序树的结点删除：
  - ![image-20210802141912503](Datastructureandalgorithm.assets/image-20210802141912503.png)
  - 删除叶子结点 (比如：2, 5, 9, 12)：
    - 若待删除结点是无父节点的叶子结点，即为根结点，直接将根结点置空
    - 找到待删除结点的父结点，将父结点的left或right属性置为空，
  - 删除只有一颗子树的结点 (比如：1)：
    - 若待删除结点无父结点，则root = 待删除结点.left(right)
    - 若待删除结点有父结点，判断待删除结点是父结点的左或右子结点，判断待删除结点的子结点是左或右子结点，则parent.left(right) = targetNode.left(right)
  - 删除有两颗子树的结点. (比如：7, 3，10 )：
    - 方法一：找到以待删除结点为根结点的右子树的值最小的结点，保存这个结点的值，删除这个结点，再将**这个值赋给待删除结点**。
    - 方法二：找到以待删除结点为根结点的左子树的值最大的结点，保存这个结点的值，删除这个结点，再将***这个值赋给待删除结点**。

```java
//测试
public class BinarySortTreeDemo {
    public static void main(String[] args) {
        int[] arr = {7, 3, 10, 12, 5, 1, 9};
        BinarySortTree binarySortTree = new BinarySortTree();
        for (int i = 0; i < arr.length; i++) {
            binarySortTree.add(new Node(arr[i]));
        }

        //中序遍历二叉排序树
        System.out.println("中序遍历二叉排序树");
        binarySortTree.midOrder();

        //删除叶子结点
        //System.out.println("删除结点后");
        //binarySortTree.delNode(5);
        //binarySortTree.midOrder();

        //删除只有一颗子树的结点
        //System.out.println("删除结点后");
        //binarySortTree.delNode(1);
        //binarySortTree.midOrder();

        //删除有两颗子树的结点
        System.out.println("删除结点后");
        binarySortTree.delNode(7);
        binarySortTree.midOrder();
    }
}

//二叉排序树
class BinarySortTree {
    private Node root;

    /**
     * Description: 删除以node为根节点的子树的最小结点并返回他的值
     * @param node: 当作以node为根节点的子树
     * @return int: 返回以node为根节点的子树最小结点的值
     */
    public int delRightTreeMin(Node node) {
        Node target = node;
        //找到以node为根节点的子树的最小值
        while (target.left != null) {
            target = target.left;
        }
        //删除最小结点（只是删除在树中的结构，没有删除这个类，有指针指向不会被回收）
        delNode(target.value);
        return target.value;
    }

    //删除结点
    public void delNode(int value) {
        if (root == null) {
            return;
        } else {
            Node targetNode = search(value);
            //如果没有找到要删除的结点
            if (targetNode == null) {
                return;
            }
            //如果有要删除的结点而二叉树只有根节点一个结点
            //不包括要删除的结点没有父结点而有子结点的情况
            if (root.left == null && root.right == null) {
                root = null;
                return;
            }
            //找到targetNode的父结点
            Node parent = searchParent(value);

            //1.删除的结点是叶子结点
            if (targetNode.left == null && targetNode.right == null) {
                //判断targetNode是父结点的左子结点还是右子结点
                if (parent.left != null && parent.left.value == value) {
                    parent.left = null;
                } else if (parent.right != null && parent.right.value == value) {
                    parent.right = null;
                }
            } else if (targetNode.left != null && targetNode.right != null) {
                //2.删除的结点有两颗子树
                int minVal = delRightTreeMin(targetNode.right);
                targetNode.value = minVal;
            } else {
                //3.剩余的就是删除的结点只有一颗子树
                //3.1如果要删除的结点有左子结点
                if (targetNode.left != null) {
                    //3.1.1如果targetNode是parent的左子结点
                    if (parent != null) {
                        if (parent.left.value == value) {
                            parent.left = targetNode.left;
                        } else {    //3.1.2如果targetNode是parent的右子结点
                            parent.right = targetNode.left;
                        }
                    } else {
                        root = targetNode.left;
                    }
                } else {    //3.1如果要删除的结点有右子结点
                    //3.2.1如果targetNode是parent的左子结点
                    if (parent != null) {
                        if (parent.left.value == value) {
                            parent.left = targetNode.right;
                        } else {    //3.2.2如果targetNode是parent的右子结点
                            parent.right = targetNode.right;
                        }
                    } else {
                        root = targetNode.right;
                    }
                }
            }

        }
    }

    //查找要删除结点的父结点
    public Node searchParent(int value) {
        if (root == null) {
            return null;
        } else {
            return root.searchParent(value);
        }
    }

    //查找删除结点
    public Node search(int value) {
        if (root == null) {
            return null;
        } else {
            return root.search(value);
        }
    }

    //添加结点
    public void add(Node node) {
        if (root == null) {
            root = node;
        } else {
            root.add(node);
        }
    }

    //中序遍历
    public void midOrder() {
        if (root != null) {
            root.midOrder();
        } else {
            System.out.println("树空");
        }
    }
}

//结点
class Node {
    int value;
    Node left;
    Node right;

    public Node(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "Node{" +
                "value=" + value +
                '}';
    }

    //查找要删除节点的父节点
    public Node searchParent(int value) {
        //如果当前结点就是要删除结点的父结点，返回
        if ((this.left != null && this.left.value == value) || (this.right != null && this.right.value == value)) {
            return this;
        } else {
            //当前查找的值小于当前结点的值，且当前左子结点不为空
            if (value < this.value && this.left != null) {
                return this.left.searchParent(value);   //向左子树递归查找
            } else if (value >= this.value && this.right != null) {
                return this.right.searchParent(value);  //向右子树递归查找
            } else {
                return null;    //没有找到父结点
            }
        }
    }


    //(前序遍历)查找要删除的结点
    public Node search(int value) {
        if (value == this.value) {
            return this;
        } else if (value < this.value) {    //向左子树递归查找
            if (this.left == null) {
                return null;
            }
            return this.left.search(value);
        } else {
            if (this.right == null) {   //向右子树递归查找
                return null;
            }
            return this.right.search(value);
        }
    }

    //添加结点的方法
    //递归的方法，满足二叉排序树的要求
    public void add(Node node) {
        if (node == null) {
            return;
        }
        //判断传入的结点与当前子树根结点值的关系
        if (node.value < this.value) {
            if (this.left == null) {    //左子结点为空
                this.left = node;
            } else {
                //递归向左子树添加
                this.left.add(node);
            }
        } else {
            if (this.right == null) {
                this.right = node;
            } else {
                //递归向右子树添加
                this.right.add(node);
            }
        }
    }

    //中序遍历
    public void midOrder() {
        if (this.left != null) {
            this.left.midOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.midOrder();
        }
    }
}
```



### 8.27 平衡二叉树AVL

- 介绍：

  - 数列{1,2,3,4,5,6}，创建一颗二叉排序树(BST)，左子树全部为空，从形式上看，更像一个单链表，插入速度没有影响查询速度明显降低(因为需要依次比较)， 不能发挥BST的优势，因为每次还需要比较左子树，其查询速度比单链表还慢

    ![image-20210802193440057](Datastructureandalgorithm.assets/image-20210802193440057.png)

  - 平衡二叉搜索树（Self-balancing binary search tree）又被称为AVL树，**是对二叉排序树功能的扩充**，可以**保证查询效率较高**。

  - 平衡二叉搜索树：它是一 棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树

- AVL树高度求解：

```java
//Node类的方法

//返回左子树的高度
public int leftHeight() {
    if (left == null) {
        return 0;
    } else {
        return left.height();
    }
}

//返回右子树的高度
public int rightHeight() {
    if (right == null) {
        return 0;
    } else {
        return right.height();
    }
}

//返回以当前结点为根结点的子树的高度
public int height() {
    return Math.max(left == null ? 0 : left.height(), right == null ? 0 : right.height()) + 1;
}
```

- AVL树左旋转：

  ![image-20210802194040450](Datastructureandalgorithm.assets/image-20210802194040450.png)

```java
//Node类的方法

//左旋转
public void leftRotate() {
    //1.以当前结点的值创建新的结点
    Node newNode = new Node(value);
    //2.把新结点的左子树设置为当前结点的左子树
    newNode.left = this.left;
    //3.把新结点的右子树设置为当前结点的右子树的左子树
    newNode.right = this.right.left;
    //4.把当前结点的值替换为右子结点的值
    this.value = this.right.value;
    //5.把当前结点的右子树设置为右子树的右子树
    this.right = this.right.right;
    //6.把当前结点的左子树设置为新结点
    this.left = newNode;
}
```

- AVL树右旋转：

![image-20210802194427681](Datastructureandalgorithm.assets/image-20210802194427681.png)

```java
//Node类的方法

//右旋转
public void rightRotate() {
    //1.以当前结点的值创建新的结点
    Node newNode = new Node(value);
    //2.把新结点的右子树设置为当前结点的右子树
    newNode.right = this.right;
    //3.把新结点的左子树设置为当前结点的左子树的右子树
    newNode.left = this.left.right;
    //4.把当前结点的值替换为左子结点的值
    this.value = this.left.value;
    //5.把当前结点的左子树设置为左子树的左子树
    this.left = this.left.left;
    //6.把当前结点的右子树设置为新结点
    this.right = newNode;
}
```

- AVL树双旋转：

![image-20210802194619951](Datastructureandalgorithm.assets/image-20210802194619951.png)

- 单独的进行左旋转或右旋转并不能使所有二叉树变成平衡二叉树

- 当对结点进行右旋转时，如果它的左子树的右子树高度大于它的左子树的左子树高度时，需要先将它的左子节点进行左旋转，再对当前结点进行右旋转
- 当对结点进行左旋转时，如果它的右子树的左子树高度大于它的右子树的右子树高度时，需要先将它的右子节点进行右旋转，再对当前结点进行左旋转
- 两个方向的双旋转并不同时进行

```java
//添加结点的方法
//递归的方法，满足二叉排序树的要求
public void add(Node node) {
    if (node == null) {
        return;
    }
    //判断传入的结点与当前子树根结点值的关系
    if (node.value < this.value) {
        if (this.left == null) {    //左子结点为空
            this.left = node;
        } else {
            //递归向左子树添加
            this.left.add(node);
        }
    } else {
        if (this.right == null) {
            this.right = node;
        } else {
            //递归向右子树添加
            this.right.add(node);
        }
    }

    //当添加完一个结点后，如果右子树高度-左子树高度 > 1
    if (rightHeight() - leftHeight() > 1) {
        //如果它的右子树的左子树高度大于它的右子树的右子树高度
        if (right != null && right.leftHeight() > left.rightHeight()) {
            //先对当前结点的右结点（右子树）进行右旋转
            right.rightRotate();
        }
        //再进行左旋转
        leftRotate();
        //不再进行下面右旋的操作
        return;
    }

    //当添加完一个结点后，如果左子树高度-右子树高度 > 1
    if (leftHeight() - rightHeight() > 1) {
        //如果它的左子树的右子树高度大于它的左子树的左子树高度
        if (left != null && left.rightHeight() > left.leftHeight()) {
            //先对当前结点的左结点（左子树）进行左旋转
            left.leftRotate();
        }
        //再进行右旋转
        rightRotate();
    }
}
```



### 8.28 多路查找树

#### 1 二叉树与多叉树

- 二叉树的问题分析：
  - 二叉树需要加载到内存的，如果二叉树的节点很多，在构建二叉树时，需要多次进行i/o操作(海量数据存在数据库或文件中)，节点海量，构建二叉树时，速度有影响
  - 节点海量，也会造成二叉树的高度很大，会降低操作速度
- 多叉树：
  - 允许每个节点可以有更多的数据项和更多的子节点，就是多叉树（multiway tree）
  - 多叉树通过重新组织节点，减少树的高度，能对二叉树进行优化
  - ![image-20210802214332593](Datastructureandalgorithm.assets/image-20210802214332593.png)

#### 2 2-3树

- 2-3树是最简单的B树结构，具有以下特点：
  - 2-3树的所有叶子节点都在同一层(只要是B树都满足这个条件)
  - 有两个子节点的节点（含一个关键字）叫二节点，二节点要么没有子节点，要么有两个子节点
  - 有三个子节点的节点（含两个关键字）叫三节点，三节点要么没有子节点，要么有三个子节点
  - 2-3树是由二节点和三节点构成的树。
- 2-3树构建举例{16, 24, 12, 32, 14, 26, 34, 10, 8, 28, 38, 20} **符合二叉排序树的规则**：
  - ![image-20210802214730847](Datastructureandalgorithm.assets/image-20210802214730847.png)
  - 当按照规则插入一个数到某个节点时，不能满足上面2-3树的三个特点，就需要拆，先向上拆，如果上层满，则拆本层，拆后仍然需要满足上面3个特点
  - 对于三节点的子树的值大小仍然遵守(BST 二叉排序树)的规则

#### 3 B树

- B-tree树即B树，B即Balanced，平衡的二叉树，2-3树和2-3-4树都是B树

- B树通过**重新组织节点，降低树的高度**，并且减少i/o读写次数来提升效率

![image-20210802214917153](Datastructureandalgorithm.assets/image-20210802214917153.png)

- 文件系统及数据库系统的设计者利用了磁盘预读原理，将一个节点的大小设为等于一个页(页得大小通常为4k)，这样每个节点只需要一次I/O就可以完全载入

- 将树的度M（结点的度是指子结点的个数，树的度是指最大的结点的度）设置为1024，在600亿个元素中最多只需要4次I/O操作就可以读取到想要的元素，B树(B+)广泛应用于文件存储系统以及数据库系统中

- B树的说明：

  - B树的阶：节点的最多子节点个数。比如2-3树的阶是3，2-3-4树的阶是4
  - B-树的搜索，从根结点开始，对结点内的关键字（有序）序列进行二分查找，如果命中则结束，否则进入查询关键字所属范围的儿子结点；重复，直到所对应的儿子指针为空，或已经是叶子结点
  - 关键字集合分布在整颗树中, 即叶子节点和非叶子节点都存放数据.
  - 搜索有可能在非叶子结点结束
  - 其搜索性能等价于在关键字全集内做一次二分查找

  ![image-20210802215328730](Datastructureandalgorithm.assets/image-20210802215328730.png)

#### 4 B+树

- B+树是B树的变体，也是一种多路搜索树，是MySql一些索引的底层原理

- B+树的说明：

  - B+树的搜索与B树也基本相同，区别是B+树只有达到叶子结点才命中（B树可以在非叶子结点命中），其性能也等价于在关键字全集做一次二分查找
  - 所有关键字都出现在叶子结点的链表中（即数据只能在叶子节点【也叫稠密索引】），且链表中的关键字(数据)恰好是有序的
  - 不可能在非叶子结点命中
  - 非叶子结点相当于是叶子结点的索引（稀疏索引），叶子结点相当于是存储（关键字）数据的数据层
    更适合文件索引系统
  - B树和B+树各有自己的应用场景，不能说B+树完全比B树好，反之亦然

  ![image-20210802215452159](Datastructureandalgorithm.assets/image-20210802215452159.png)

#### 5 B*树

- B*树是B+树的变体，在B+树的非根和非叶子结点再增加指向兄弟的指针

- B*树的说明：

  - B树定义了非叶子结点关键字个数至少为(2/3)*M，即块的最低使用率为2/3，而B+树的块的最低使用率为B+树的1/2*
  - 可以看出，B*树分配新结点的概率比B+树要低，空间使用率更高

  

![image-20210802215615450](Datastructureandalgorithm.assets/image-20210802215615450.png)



## 9.图

### 9.1 图的基本介绍

- 图（Graph）是一种数据结构，其中结点可以具有零个或多个相邻元素。两个结点之间的连接称为边。 结点也可以称为顶点。图可以表示多对多的关系。

- 图的常用术语：

  - 顶点(vertex)
  - 边(edge)
  - 路径
  - 无向图(右图)
  - 有向图
  - 带权图

  ![image-20210803165148688](Datastructureandalgorithm.assets/image-20210803165148688.png)

  ![image-20210803165214467](Datastructureandalgorithm.assets/image-20210803165214467.png)

  

### 9.2 图的表示方式

图的表示方式有两种：二维数组表示（邻接矩阵）与链表表示（邻接表）。

- 邻接矩阵

  邻接矩阵是表示图形中顶点之间相邻关系的矩阵，对于n个顶点的图而言，矩阵是的row和col表示的是1....n个点。0-未连通，1-连通（路径的权值）

  ![image-20210803165434134](Datastructureandalgorithm.assets/image-20210803165434134.png)

- 邻接表

  邻接矩阵需要为每个顶点都分配n个边的空间，其实有很多边都是不存在,会造成空间的一定损失.

  邻接表的实现只关心存在的边，不关心不存在的边。因此没有空间浪费，邻接表由数组+链表组成

  ![image-20210803165935507](Datastructureandalgorithm.assets/image-20210803165935507.png) 



### 9.3 图的深度优先遍历

- 图的深度优先搜索(Depth First Search) ：

  从初始访问结点出发，首先访问第一个邻接结点，然后再以这个被访问的邻接结点作为初始结点，访问它的第一个邻接结点。这样的访问策略是**优先往纵向挖掘深入**，而不是对一个结点的所有邻接结点进行横向访问。深度优先搜索是一个**递归**的过程。

- 深度优先遍历算法步骤：

  1.访问初始结点v，并标记结点v为已访问。

  2.查找结点v的第一个邻接结点w。

  3.若w存在，则继续执行4，如果w不存在，则回到第1步，将从v的下一个结点继续。

  4.若w未被访问，对w进行深度优先遍历递归（即把w当做另一个v，然后进行步骤123）。

  5.查找结点v的w邻接结点的下一个邻接结点，转到步骤3。

![image-20210803170432781](Datastructureandalgorithm.assets/image-20210803170432781.png)



### 9.4 图的广度优先遍历

- 图的广度优先搜索(Broad First Search) :

  类似于一个**分层搜索**的过程，广度优先遍历需要使用一个队列以保持访问过的结点的顺序，以便按这个顺序来访问这些结点的邻接结点。（如先输出A，再将与A邻接的B、C输出，再从B开始，将与B邻接的全部输出...）

- 广度优先遍历算法步骤：

  1.访问初始结点v并标记结点v为已访问。

  2.结点v入队列。

  3.当队列非空时，继续执行，否则算法结束。

  4.出队列，取得队头结点u。

  5.查找结点u的第一个邻接结点w。

  6.若结点u的邻接结点w不存在，则转到步骤3；否则循环执行以下三个步骤：

  ​	6.1 若结点w尚未被访问，则访问结点w并标记为已访问。 

  ​	6.2 结点w入队列。

  ​	6.3 查找结点u的继w邻接结点后的下一个邻接结点w，转到步骤6。

**深度优先和广度优先的代码实现：**

```java
public class Graph {

    public static void main(String[] args) {
        int n = 5;
        String[] vertexValue = {"A", "B", "C", "D", "E"};
        //创建图对象
        Graph graph = new Graph(5);
        //循环添加顶点
        for (String vertex : vertexValue) {
            graph.insertVertex(vertex);
        }
        //添加边
        graph.insertEdge(0,1,1);
        graph.insertEdge(0,2,1);
        graph.insertEdge(1,2,1);
        graph.insertEdge(1,3,1);
        graph.insertEdge(1,4,1);

        //显示邻接矩阵
        graph.showGraph();

        //测试dfs遍历
        //System.out.println("dfs");
        //graph.dfs(graph.isVisited, 0);
        //System.out.println();


        //测试bfs遍历
        System.out.println("bfs");
        graph.bfs(graph.isVisited, 0);
    }

    //存储顶点集合
    private ArrayList<String> vertexList;
    //存储图对应的邻接矩阵
    private int[][] edges;
    //表示边的数目
    private int numOfEdges;
    //记录某个顶点是否被访问
    private boolean[] isVisited;

    //构造器
    public Graph(int n) {
        //初始化矩阵和vertexList
        edges = new int[n][n];
        vertexList = new ArrayList<String>(n);
        numOfEdges = 0;
        isVisited = new boolean[n];
    }

    //对dfs进行重载，遍历所有结点，并进行bfs
    //目的是避免空顶点（结点孤立）遍历不到
    public void bfs() {
        for (int i = 0; i < getNumOfVertex(); i++) {
            if (!isVisited[i]) {
                bfs(isVisited, i);
            }
        }
    }

    //广度优先遍历算法
    private void bfs(boolean[] isVisited, int i) {
        int u;  //表示队列头结点的下标
        int w;  //表示邻接结点的下标
        //队列，记录结点访问的顺序
        LinkedList queue = new LinkedList();
        System.out.print(getValueByIndex(i) + "->");
        //将该结点设置为访问
        isVisited[i] = true;
        //将这个结点加入队列（先进先出）
        queue.addLast(i);
        //队列非空
        while (!queue.isEmpty()) {
            u = (Integer) queue.removeFirst();
            //得到u的第一个邻接结点的下标w
            w = getFirstNeighbor(u);
            while (w != -1) {   //说明有邻接结点
                if (!isVisited[w]) {    //如果w结点没被访问
                    System.out.print(getValueByIndex(w) + "->");
                    isVisited[w] = true;
                    queue.addLast(w);
                }
                //如果w结点已经被访问过，查找属于u的下一个邻接结点
                w = getNextNeighbor(u, w);
            }
        }
    }

    //对dfs进行重载，遍历所有结点，并进行dfs
    //目的是避免空顶点（结点孤立）遍历不到
    public void dfs() {
        for (int i = 0; i < getNumOfVertex(); i++) {
            if (!isVisited[i]) {
                dfs(isVisited, i);
            }
        }
    }

    //深度优先遍历算法
    public void dfs(boolean[] isVisited, int i) {
        //首先访问该结点，输出
        System.out.print(getValueByIndex(i) + "->");
        //将该结点设置为访问
        isVisited[i] = true;
        //查找结点i的第一个邻接结点
        int w = getFirstNeighbor(i);
        while (w != -1) {   //说明有邻接结点
            if (!isVisited[w]) {    //如果w结点没被访问
                dfs(isVisited, w);
            }
            //如果w结点已被访问,查找属于i的下一个邻接结点
            w = getNextNeighbor(i, w);
        }
    }

    /**
     * Description: 根据前一个邻接结点的下标来获取下一个邻接结点
     * @param v1: 本结点的下标
     * @param v2: 前一个邻接结点的下标
     * @return int:
     */
    public int getNextNeighbor(int v1, int v2) {
        for (int i = v2 + 1; i < vertexList.size(); i++) {
            if (edges[v1][i] > 0) {
                return i;
            }
        }
        return -1;
    }

    //得到以index为下标的结点的第一个领接结点的下标
    public int getFirstNeighbor(int index) {
        for (int i = 0; i < vertexList.size(); i++) {
            if (edges[index][i] > 0) {
                return i;
            }
        }
        return -1;
    }

    //显示图对应的矩阵
    public void showGraph() {
        for (int[] link : edges) {
            System.out.println(Arrays.toString(link));
        }
    }

    //返回顶点的个数
    public int getNumOfVertex() {
        return vertexList.size();
    }

    //返回边的个数
    public int getNumOfEdges() {
        return numOfEdges;
    }

    //返回顶点i(下标)对应的数据如0->"A"  1->"B"
    public String getValueByIndex(int i) {
        return vertexList.get(i);
    }

    //返回v1，v2的边的权值
    public int getWeight(int v1, int v2) {
        return edges[v1][v2];
    }

    //插入顶点
    public void insertVertex(String vertex) {
        vertexList.add(vertex);
    }

    /**
     * Description: 添加边
     * @param v1: 表示第v1个顶点的下标
     * @param v2: 表示第v2个顶点的下标
     * @param weight: v1，v2的边的权值
     * @return void:
     */
    public void insertEdge(int v1, int v2, int weight) {
        //无向表
        edges[v1][v2] = weight;
        edges[v2][v1] = weight;
        numOfEdges++;
    }
}
```



## 10.十大算法

### 10.1 二分查找算法（非递归）

用while循环来替代递归，算法的时间复杂度不变。

```java
public class BinarySearchNoRecur {
    public static void main(String[] args) {
        int[] arr = {1, 3, 8, 10, 11, 67, 100};
        int index = binarySearch(arr, 1);
        System.out.println("index = " + 10);
    }

    /**
     * Description:
     * @param arr: 待查数组，升序排列
     * @param target: 目标值
     * @return int: 返回对应下标，没有找到返回-1
     */
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        while (left <= right) { //继续查找
            int mid = (left + right) / 2;
            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] > target) {
                right = mid - 1;    //向左边查找
            } else {
                left = mid + 1; //向右边查找
            }
        }
        return -1;
    }
}
```



### 10.2 分治算法

- 分治法Divide and conquer algorithm在每一层递归上都有三个步骤：

  1)分解：将原问题分解为若干个规模较小，相互独立，与原问题形式相同的子问题

  2)解决：若子问题规模较小而容易被解决则直接解，否则递归地解各个子问题

  3)合并：将各个子问题的解合并为原问题的解。

- 分治算法可以求解的一些经典问题：二分搜索、大整数乘法、棋盘覆盖、**归并排序**、**快速排序**、线性时间选择、最接近点对问题、循环赛日程表、汉诺塔

- 汉诺塔问题分析：

  - 1)如果是有一个盘， A->C
  - 2)如果我们有 n >= 2 情况，我们总是可以看做是两个盘 1.最下边的盘(第n个) 2. 上面的盘(第1到n-1个)
    - 先把最上面的盘 A->B
    - 把最下边的盘 A->C
    - 把B塔的所有盘 从 B->C 
    - ![image-20210804102911540](Datastructureandalgorithm.assets/image-20210804102911540.png)

```java
public class DAQ {
    public static void main(String[] args) {
        hanoiTower(5,'A','B','C');
    }

    /**
     * Description: 第1到num个盘从a移动到c中间借助b
     * @param num: 要移动的汉诺塔数量
     * @param a:
     * @param b:
     * @param c:
     * @return void:
     */
    public static void hanoiTower(int num, char a, char b, char c) {
        //如果只有一盘
        if (num == 1) {
            System.out.println("第1个盘从" + a + "->" + c);
        } else {
            //1.把上面的所有盘A->B，移动过程中借助C
            hanoiTower(num - 1, a, c, b);
            //2.把最下面的盘A->C
            System.out.println("第" + num + "个盘从" + a + "->" + c);
            //3.把B上面的所有全部B->C
            hanoiTower(num - 1, b, a, c);
        }
    }
}
```



### 10.3 动态规划算法

- 动态规划算法介绍：

  - 动态规划(Dynamic Programming)算法的核心思想是：**将大问题划分为小问题**进行解决，从而一步步获取最优解的处理算法
  - 动态规划算法与分治算法类似，其基本思想也是将待求解问题分解成若干个子问题，先求解子问题，然后从这些子问题的解得到原问题的解。
  - 与分治法不同的是，适合于用动态规划求解的问题，经分解得到**子问题往往不是互相独立的**。 ( 即下一个子阶段的求解是建立在上一个子阶段的解的基础上，进行进一步的求解 )
  - 动态规划可以通过**填表**的方式来逐步推进，得到最优解.

- 01背包问题：

  - 背包问题主要是指一个给定容量的背包、若干具有一定价值和体积的物品，如何选择物品放入背包使物品的价值最大。其中又分**01背包(每个物品最多放一个)**和完全背包(完全背包指的是：每种物品都有无限件可用，可以转化为01背包问题)等

  - 问题描述：

    ![image-20210804145154514](Datastructureandalgorithm.assets/image-20210804145154514.png)

  - 解题思路：每次遍历到的第i个物品，根据w[i]和val[i]来确定是否需要将该物品放入背包中。即对于给定的n个物品，设val[i]、w[i]分别为第i+1(从0开始)个物品的价值和体积，C为背包的容量。再令v[i] [j]表示在前 i 个物品中能够装入容量为 j 的背包中的最大价值。

    - (1)  v[i] [0]=v[0] [j]=0; //表示填入表第一行和第一列是0

      ![image-20210804183103594](Datastructureandalgorithm.assets/image-20210804183103594.png)

    - (2) 当w[i-1]> j 时：令v[i] [j]=v[i-1] [j]   // 当准备加入新增的商品的容量大于当前背包的容量时，就直接使用上一个单元格的装入策略

    - (3) 当j>=w[i-1]时：// 当准备加入新增的商品的容量小于或等于当前背包的容量时

      令v[i] [j]=max{v[i-1] [j], val[i-1]+v[i-1] [j-w[i-1]]}  //新的单元格的装入策略由  1）上一个单元格的装入策略  2）当前商品加入背包与上一层商品&&背包容量减去当前商品体积的装入策略  **两者间的价值更大者**决定

      ![image-20210804183124961](Datastructureandalgorithm.assets/image-20210804183124961.png)

    - 背包问题最优解回溯（从最后一个解v[i] [j]开始）：

      - v[i] [j]=v[i-1] [j] 时，说明没有选择第 i 个商品，则回到v[i-1] [j]；
      - v[i] [j]=val[i-1]+v[i-1] [j-w[i-1]]时，说明装了第 i 个商品，该商品是最优解组成的一部分，随后我们得回到装该商品之前，即回到v[i-1] [j-w[i-1]]；
      - 一直遍历到i＝0结束为止，所有解的组成都会找到。

      ![image-20210804183744802](Datastructureandalgorithm.assets/image-20210804183744802.png)

```java
public class KnapsackProblem {
    public static void main(String[] args) {
        int[] w = {2, 3, 4, 5};  //物品的体积
        int[] val = {3, 4, 5, 6}; //物品的价值
        int n = val.length; //物品的个数
        int m = 8;  //背包的容量

        //创建二维数组，物品和背包容量的交叉表
        //v[i][j]表示在前i个物品中能放下装入容量j的背包的最大价值
        //初始化第一列第一行（默认为0）
        int[][] v = new int[n + 1][m + 1];

        //动态规划处理
        for (int i = 1; i < v.length; i++) {    //遍历所有商品
            for (int j = 1; j < v[0].length; j++) { //遍历所有背包容量
                //v[][]数组的i和j是从1开始遍历，val[]和w[]数组的i是从0开始遍历
                if (w[i - 1] > j) {
                    // 当准备加入新增的商品的容量大于当前背包的容量时，
                    // 就直接使用上一个单元格的装入策略
                    v[i][j] = v[i - 1][j];
                } else {
                    // 当准备加入新增的商品的容量小于或等于当前背包的容量时
                    // 新的单元格的装入策略由
                    // 1）上一个单元格的装入策略
                    // 2）当前商品加入背包与上一层商品&&背包容量减去当前商品体积的装入策略
                    // **两者间的价值更大者**决定
                    v[i][j] = Math.max(v[i - 1][j], val[i - 1] + v[i - 1][j - w[i - 1]]);
                }
            }
        }

        //输出v[][]物品和背包容量的交叉表
        for (int i = 0; i < v.length; i++) {
            for (int j = 0; j < v[i].length; j++) {
                System.out.print(v[i][j] + "\t");
            }
            System.out.println();
        }

        //输出最后背包内的商品
        int i = v.length - 1;    //行的最大下标
        int j = v[0].length - 1; //列的最大下标
        //从最后一项开始输出
        while (i > 0 && j > 0) {
            if (v[i][j] == v[i - 1][j]) {
                //说明没有选择第i个商品
            } else {
                //说明选择了第i个商品
                System.out.printf("第%d个商品放到背包中\n", i);
                j -= w[i - 1];
            }
            //朝上一个商品遍历
            i--;
        }
    }
}
```



### 10.4 KMP算法

- 字符串匹配问题：判断文本串"BBC ABCDAB ABCDABCDABDE"是否存在模式串"ABCDABD"，如果存在，就返回第一次出现的位置, 如果没有，则返回-1

- 暴力匹配算法：

  - 遍历文本串，i 为文本串的指针，j 为模式串的指针；

  - 如果当前字符匹配成功（即s1[i] == s2[j]），则i++，j++，继续匹配下一个字符；

  - 如果失配（即s1[i] != s2[j]），令i = i - (j - 1)，j = 0。**相当于每次失配时，i 回溯最初位置，j 被置为0**。

  - ![image-20210805145442763](Datastructureandalgorithm.assets/image-20210805145442763.png)

    ![image-20210805145500145](Datastructureandalgorithm.assets/image-20210805145500145.png)

```java
public class ViolenceMatch {
    public static void main(String[] args) {
        String str1 = "BBC ABCDAB ABCDABCDABDE";
        String str2 = "ABCDABD";
        System.out.println(violenceMatch(str1, str2));
    }

    //暴力匹配算法
    public static int violenceMatch(String str1, String str2) {
        char[] s1 = str1.toCharArray();
        char[] s2 = str2.toCharArray();

        int i = 0;  //i索引指向s1
        int j = 0;  //j索引指向s2
        //i < s1.length保证长字符串全部遍历
        //j < s2.length保证s1含有s2时就退出
        while (i < s1.length && j < s2.length) {
            if (s1[i] == s2[j]) {   //开始匹配
                i++;
                j++;
            } else {    //没有匹配成功
                i = i - (j - 1);
                j = 0;
            }
        }

        //判断是否匹配成功
        if (j == s2.length) {
            return i - j;
        }
        return -1;
    }
}
```

- KMP算法介绍：

  - Knuth-Morris-Pratt 字符串查找算法，由三个人的姓氏取名，利用之前判断过信息，通过一个next数组，保存模式串中前后最长公共子序列的长度，每次回溯时，通过next数组找到，前面匹配过的位置，省去了大量的计算时间
  - 参考：https://www.cnblogs.com/ZuoAndFutureGirl/p/9028287.html

- KMP算法：

  - 获取模式串的部分匹配表（**使用了KMP后续算法的原理**）：

    - next 数组各值的含义：代表包括当前字符在内的字符串中，有多大长度的相同前缀后缀。例如如果next [j] = k，代表包括 j 在内的字符串中有最大长度为*k* 的相同前缀后缀。
    - ![image-20210805150109856](Datastructureandalgorithm.assets/image-20210805150109856.png)

  - 遍历文本串，i 为文本串的指针，j 为模式串的指针；

  - 如果当前字符匹配成功（即s1[i] == s2[j]），则i++，j++，继续匹配下一个字符；

  - 如果失配（即s1[i] != s2[j]），令i 不变，j = next[j - 1]，**相当于每次失配时，i 不动，j 回溯到 前 j-1 个元素子串的相同前缀的后一个位置**。

  - ![image-20210805150738117](Datastructureandalgorithm.assets/image-20210805150738117.png)

    ![image-20210805150752631](Datastructureandalgorithm.assets/image-20210805150752631.png)



```java
public class KMP {
    public static void main(String[] args) {
        String str1 = "BBC ABCDAB ABCDABCDABDE";
        String str2 = "ABCDABD";
        //str2的部分匹配表
        System.out.println(Arrays.toString(kmpNext(str2)));
        //str2在str1中的位置
        System.out.println(kmpSearch(str1, str2));
    }

    /**
     * Description: KMP算法匹配模式串在文本串中的位置
     * @param text: 待匹配的文本串
     * @param pattern: 模式串
     * @return int: 模式串在文本串中的位置，不匹配返回-1
     */
    public static int kmpSearch(String text, String pattern) {
        //获取模式串的部分匹配表
        int[] next = kmpNext(pattern);
        //遍历待匹配的文本串
        //i-待匹配的文本串的索引   j-模式串的索引
        for (int i = 0, j = 0; i < text.length(); i++) {
            //不匹配，j回溯
            if (j > 0 && text.charAt(i) != pattern.charAt(j)) {
                j = next[j - 1];
            }
            //匹配，j++
            if (text.charAt(i) == pattern.charAt(j)) {
                j++;
            }
            if (j == pattern.length()) {    //找到位置
                return i - j + 1;
            }
        }
        //遍历后没有找到
        return -1;
    }
    /**
     * Description: 获取一个字符串的部分匹配表
     * @param pattern: 模式串
     * @return int[]: int[i]代表包括当前字符在内的字符串中，相同前缀后缀的长度
     */
    public static int[] kmpNext(String pattern) {
        int[] next = new int[pattern.length()];
        //子串长度为1，部分匹配值为0
        next[0] = 0;
        //i为遍历整个字符串的索引，j是前缀索引
        for (int i = 1, j = 0; i < pattern.length(); i++) {
            //j > 0 使 j = 0时 在不满足条件时保持索引0，而不是 j = next[-1]
            //pattern.charAt(i) != pattern.charAt(j)时，过程和模式串与文本串匹配类似
            //如模式串="ABABCABABA"
            //匹配表为="0012012343"
            //在j=4(ABABC),i=9(ABABA)时不满足条件，但前面已经满足"ABAB"相同了，
            //即 j 对应的前面的一个"AB"ABC和 i 对应的后面的一个AB"AB"A已经匹配上了
            //所以j = next[j - 1];指向前面的一个"AB"的后一位继续与i比较
            while (j > 0 && pattern.charAt(i) != pattern.charAt(j)) {
                j = next[j - 1];
            }
            //
            if (pattern.charAt(i) == pattern.charAt(j)) {
                j++;
            }
            next[i] = j;
        }
        return next;
    }
}
```



### 10.5 贪心算法

- 贪心算法介绍：Greedy Algorithm，是指在对问题进行求解时，在每一步选择中都采取最好或者最优(即最有利)的选择，从而希望能够导致结果是最好或者最优的算法，所得到的结果**不一定是最优的结果**(有时候会是最优解)，但是都是相对近似(接近)最优解的结果

- 应用-集合覆盖：存在如下表的需要付费的广播台，以及广播台信号可以覆盖的地区。 **如何选择最少的广播台**，让所有的地区都可以接收到信号

  - ![image-20210805193444352](Datastructureandalgorithm.assets/image-20210805193444352.png)

  - 思路分析：

    - 1)遍历所有的广播电台, 找到一个**覆盖了最多未覆盖的地区**（交集）的电台(此电台可能包含一些已覆盖的地区，但没有关系）

      2)将这个电台加入到一个选择集合中，从未覆盖地区中删除已经被这个电台覆盖的地区

      3)重复第1步直到覆盖了全部的地区，选择集合就是最后结果

```java
public class GreedyAlgorithm {
    public static void main(String[] args) {
        //创建广播电台
        HashMap<String, HashSet<String>> broadcasts = new HashMap<>();

        HashSet<String> hashSet1 = new HashSet<String>();
        hashSet1.add("北京");
        hashSet1.add("上海");
        hashSet1.add("天津");

        HashSet<String> hashSet2 = new HashSet<String>();
        hashSet2.add("广州");
        hashSet2.add("北京");
        hashSet2.add("深圳");

        HashSet<String> hashSet3 = new HashSet<String>();
        hashSet3.add("成都");
        hashSet3.add("上海");
        hashSet3.add("杭州");


        HashSet<String> hashSet4 = new HashSet<String>();
        hashSet4.add("上海");
        hashSet4.add("天津");

        HashSet<String> hashSet5 = new HashSet<String>();
        hashSet5.add("杭州");
        hashSet5.add("大连");

        //加入到broadcasts的map
        broadcasts.put("K1", hashSet1);
        broadcasts.put("K2", hashSet2);
        broadcasts.put("K3", hashSet3);
        broadcasts.put("K4", hashSet4);
        broadcasts.put("K5", hashSet5);

        //allAreas 存放所有需要覆盖的地区，选择电台后，去掉交集地区
        HashSet<String> allAreas = new HashSet<String>();
        allAreas.add("北京");
        allAreas.add("上海");
        allAreas.add("天津");
        allAreas.add("广州");
        allAreas.add("深圳");
        allAreas.add("成都");
        allAreas.add("杭州");
        allAreas.add("大连");

        //创建ArrayList，存放选择的电台集合selects
        ArrayList<String> selects = new ArrayList<>();

        //定义临时的集合，在遍历过程中，存放某个电台覆盖地区与还未覆盖地区的交集地区
        HashSet<String> tempSet = new HashSet<>();

        //maxKey保存在一次遍历过程中，上述交集地区最大的电台key
        //以及上一个电台maxkey与还未覆盖地区的交集地区数量
        String maxKey = null;
        int preMaxKeyNum = 0;


        //选择的电台还没有覆盖到所有地区
        while (allAreas.size() != 0) {
            maxKey = null;
            preMaxKeyNum = 0;
            //遍历所有电台key
            for (String key : broadcasts.keySet()) {
                //每次循环清空tempSet
                tempSet.clear();
                //当前电台key能覆盖的地区加入tempSet
                HashSet<String> areas = broadcasts.get(key);
                tempSet.addAll(areas);
                //求出tempSet（当前电台key能覆盖的地区）
                //和allAreas（还未覆盖的地区）的交集赋给tempSet
                tempSet.retainAll(allAreas);
                //如果当前电台key含有的未覆盖地区的数量，比本次循环中的maxKey还多
                //体现出贪心算法的特点
                if (tempSet.size() > 0 &&
                        (maxKey == null || tempSet.size() > preMaxKeyNum)) {
                    maxKey = key;
                    preMaxKeyNum = tempSet.size();
                }
            }
            //将电台maxKey加入选择selects
            if (maxKey != null) {
                selects.add(maxKey);
                //去除allAreas中已经覆盖的地区
                allAreas.removeAll(broadcasts.get(maxKey));
            }
        }

        System.out.println(selects);

    }
}
```



### 10.6 Prim算法

- 普里姆算法是求**带权的无向连通图**的**最小生成树**(Minimum Cost Spanning Tree/MST)的算法（**最短连通**）。
- 给定一个带权的无向连通图，如何选取一棵生成树（N个顶点，一定有N-1条边），使树上所有边上权的总和为最小，这叫最小生成树 。

![image-20210807232021381](Datastructureandalgorithm.assets/image-20210807232021381.png)

- 应用场景-修路问题：
  - ![image-20210807233107547](Datastructureandalgorithm.assets/image-20210807233107547.png)
  - 各个站点的距离用边线表示(权) ，如何修路保证各个村庄都能连通，并且总的修建公路总里程最短?
- Prim算法思路分析与图解：
  - 在包含n个顶点的连通图中，找出只有(n-1)条边包含所有n个顶点的连通子图，也就是所谓的**极小连通子图**
  - 设G=(V,E)是连通网，T=(U,D)是最小生成树，V,U是顶点集合，E,D是边的集合，visited[]标记该节点是否访问过
  - 若从顶点 u 开始构造最小生成树，则从集合 V 中取出顶点 u 放入集合U中，标记顶点 u 的 visited[u]=1
  - 若集合 U 中顶点 ui 与集合 (V-U) 中的顶点 vj 之间存在边，则寻找这些边中权值最小的边，将顶点 vj 加入集合U中，将边（ui,vj）加入集合D中，标记visited[vj]=1，**这种构造方法已经保证不会构成回路**
  - 重复步骤上一个步骤，直到U与V相等，即所有顶点都被标记为访问过，此时D中有n-1条边

![image-20210807233014282](Datastructureandalgorithm.assets/image-20210807233014282.png)

```java
public class PrimAlgorithm {

    public static void main(String[] args) {
        //测试看看图是否创建ok
        char[] data = new char[]{'A','B','C','D','E','F','G'};
        int verxs = data.length;
        //邻接矩阵的关系使用二维数组表示,10000这个大数，表示两个点不联通
        int [][] weight=new int[][]{
                //ABCDEFG
                {10000,5,7,10000,10000,10000,2},        //A
                {5,10000,10000,9,10000,10000,3},        //B
                {7,10000,10000,10000,8,10000,10000},    //C
                {10000,9,10000,10000,10000,4,10000},
                {10000,10000,8,10000,10000,5,4},
                {10000,10000,10000,4,5,10000,6},
                {2,3,10000,10000,4,6,10000},
        };

        //创建MGraph对象和MiniTree对象
        MGraph graph = new MGraph(verxs);
        MinTree minTree = new MinTree();
        minTree.createGraph(graph, verxs, data, weight);
        //显示图的邻接矩阵
        minTree.showGraph(graph);

        //测试prim算法
        minTree.prime(graph, 0);
    }
}

//最小生成树--村庄的图
class MinTree {

    /**
     * Description: 编写prim算法，得到最小生成树
     * @param graph: 图
     * @param v: 表示从第几个顶点开始生成
     * @return void:
     */
    public void prime(MGraph graph, int v) {
        //标记顶点是否被访问过 0-为被访问过
        int[] visited = new int[graph.verxs];
        //把当前结点已访问
        visited[v] = 1;
        //用俩个数据记录两个顶点的下标
        int v1 = -1;
        int v2 = -1;
        //minWeight初始化
        int minWeight = 10000;
        //遍历后产生n-1条边
        for (int k = 1; k < graph.verxs; k++) {

            for (int i = 0; i < graph.verxs; i++) { //遍历已经访问过的结点
                for (int j = 0; j < graph.verxs; j++) { //遍历还没有访问的结点
                    //已经访问过的结点与还没有访问的结点的权值小于minWeight
                    if (visited[i] == 1 && visited[j] == 0 && graph.weight[i][j] < minWeight) {
                        //替换miniWeight，并记录i和j的通路(寻找权值最小的边)
                        minWeight = graph.weight[i][j];
                        v1 = i;
                        v2 = j;
                    }
                }
            }
            //找到一条边是当前权值最小的(v1-v2)
            System.out.println("边<" + graph.data[v1] + "," + graph.data[v2] + ">:权值" + minWeight);
            //将当前这个结点标记为已经访问
            visited[v2] = 1;
            //重新设置miniWeight
            minWeight = 10000;
        }


    }

    //根据数据创建图的邻接矩阵
    public void createGraph(MGraph graph, int verxs, char data[], int[][] weight) {
        int i, j;
        for(i = 0; i < verxs; i++) {//顶点
            graph.data[i] = data[i];
            for(j = 0; j < verxs; j++) {
                graph.weight[i][j] = weight[i][j];
            }
        }
    }

    //显示图的邻接矩阵
    public void showGraph(MGraph graph) {
        for(int[] link: graph.weight) {
            System.out.println(Arrays.toString(link));
        }
    }
}

//原始图
class MGraph {
    int verxs;   //图结点的个数
    char[] data;    //结点数据
    int[][] weight; //边，邻接矩阵

    public MGraph(int verxs) {
        this.verxs = verxs;
        data = new char[verxs];
        weight = new int[verxs][verxs];
    }
}
```



### 10.7 Kruskal算法

- 克鲁斯卡尔(Kruskal)算法，同Prim算法一样是用来求加权连通图的最小生成树的算法

- 应用场景-修路问题：

  - 各个站点的距离用边线表示(权) ，如何修路保证各个村庄都能连通，并且总的修建公路总里程最短?
  - ![image-20210808203743814](Datastructureandalgorithm.assets/image-20210808203743814.png)

- 基本思想：按照权值从小到大的顺序选择n-1条边，并保证在选择边时不构成回路

- 图解：

  ![微信截图_20210807233707](Datastructureandalgorithm.assets/微信截图_20210807233707.png)

- 保证在选择边时不构成回路：
  - 即在添加边时边的两个顶点不能指向同一个终点
  - 顶点的终点是指在**当前最小生成树中与其连通的最大顶点**，将顶点数组映射到【0,1,2...数组】，**在添加边时要存储ends[start]=end**（start>end），以便查找顶点的终点
  - ![image-20210807234900478](Datastructureandalgorithm.assets/image-20210807234900478.png)

```java
public class KruskalDemo {
    private int KedgeNum;   //图边的个数
    private char[] data;    //图的结点数据（包含结点个数信息）
    private int[][] weight; //图的邻接矩阵
    private Kedge[] Kedges;   //图的边数据
    private static final int INF = Integer.MAX_VALUE;

    public static void main(String[] args) {
        char[] data = new char[]{'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        int weight[][] = {
                /*A*//*B*//*C*//*D*//*E*//*F*//*G*/
                /*A*/ {0, 12, INF, INF, INF, 16, 14},
                /*B*/ {12, 0, 10, INF, INF, 7, INF},
                /*C*/ {INF, 10, 0, 3, 5, 6, INF},
                /*D*/ {INF, INF, 3, 0, 4, INF, INF},
                /*E*/ {INF, INF, 5, 4, 0, 2, 8},
                /*F*/ {16, 7, 6, INF, 2, 0, 9},
                /*G*/ {14, INF, INF, INF, 8, 9, 0}
        };

        //根据上面的数据构建一个图
        KruskalDemo kruskalDemo = new KruskalDemo(data, weight);
        //打印图的邻接矩阵
        kruskalDemo.print();
        //输出图的所有边
        Kedge[] Kedges = kruskalDemo.getKedges();
        System.out.println(Arrays.toString(Kedges));

        //Kruskal算法得到最小生成树
        kruskalDemo.kruskal();
    }

    public void kruskal() {
        int index = 0;  //最后结果数组的索引
        int[] ends = new int[data.length];  //用于保存各顶点在已有最小生成树的终点
        //创建结果数组，保存最后的最小生成树
        Kedge[] result = new Kedge[data.length - 1];
        //获取当前的所有边的集合
        Kedge[] Kedges = getKedges();
        //遍历所有边，判断准备加入的边的两顶点是否形成了回路，没有则将边添加到最小生成树
        for (int i = 0; i < KedgeNum; i++) {
            //获取两顶点
            int p1 = getPosition(Kedges[i].start);
            int p2 = getPosition(Kedges[i].end);
            //获取两顶点的终点
            int m = getEnd(ends, p1);
            int n = getEnd(ends, p2);
            //是否构成回路
            if (m != n) {
                ends[m] = n;    //设置在“已有最小生成树”中的终点
                result[index++] = Kedges[i];  //加入最小生成树的结果数组
            }
        }
        //输出最小生成树
        System.out.println(Arrays.toString(result));
    }

    /**
     * Description: 返回ch顶点对应的下标，如果找不到，返回-1
     * @param ch: 顶点的值，比如'A','B'
     * @return int:
     */
    private int getPosition(char ch) {
        for(int i = 0; i < data.length; i++) {
            if(data[i] == ch) {//找到
                return i;
            }
        }
        //找不到,返回-1
        return -1;
    }

    /**
     * Description: 获取下标为i的顶点的终点，用于判断两个顶点的终点是否相同
     * @param ends: 在遍历过程中逐渐形成的
     * @param i: 该顶点在data[]中的下标
     * @return int:
     */
    public int getEnd(int[] ends, int i) {
        while (ends[i] != 0) {
            i = ends[i];
        }
        return i;
    }

    //图的构造器
    public KruskalDemo(char[] data, int[][] weight) {

        int vlen = data.length;
        //构建图的结点数据
        this.data = new char[vlen];
        for (int i = 0; i < vlen; i++) {
            this.data[i] = data[i];
        }
        //构建图的邻接矩阵
        this.weight = new int[vlen][vlen];
        ArrayList<Kedge> temp = new ArrayList<>();
        for (int i = 0; i < vlen; i++) {
            for (int j = 0; j < vlen; j++) {
                this.weight[i][j] = weight[i][j];
                //统计边的个数
                if (this.weight[i][j] != INF && this.weight[i][j] != 0) {
                    this.KedgeNum++;
                    temp.add(new Kedge(data[i], data[j], this.weight[i][j]));
                }
            }
        }
        //构建图的边的数据(并且按从小到大排序)
        Kedges = new Kedge[KedgeNum];
        for (int i = 0; i < temp.size(); i++) {
            Kedges[i] = temp.get(i);
        }
        Arrays.sort(Kedges);
    }

    //打印图的邻接矩阵
    public void print() {
        System.out.println("邻接矩阵为: \n");
        for (int i = 0; i < weight.length; i++) {
            for (int j = 0; j < weight.length; j++) {
                System.out.printf("%12d", weight[i][j]);
            }
            System.out.println();//换行
        }
    }

    public Kedge[] getKedges() {
        return Kedges;
    }
}

//创建一个类EData ，它的对象实例就表示一条边
class Kedge implements Comparable<Kedge> {

    @Override
    public int compareTo(Kedge o) {
        if (this.weight > o.weight) {
            return 1;
        } else if (this.weight < o.weight) {
            return -1;
        } else {
            return 0;
        }
    }

    char start; //边的一个点
    char end; //边的另外一个点
    int weight; //边的权值

    //构造器
    public Kedge(char start, char end, int weight) {
        this.start = start;
        this.end = end;
        this.weight = weight;
    }

    //重写toString, 便于输出边信息
    @Override
    public String toString() {
        return "Kedge [<" + start + ", " + end + ">= " + weight + "]";
    }
}
```



### 10.8 Dijkstra算法

- 迪杰斯特拉(Dijkstra)算法是**典型最短路径算法**，用于计算一个结点到其他结点的最短路径。 它的主要特点是以起始点为中心向外层层扩展(**广度优先**搜索思想+**贪心**思想)，直到扩展到终点为止。

- 应用场景-最短路径问题：
  - ![image-20210808154049427](Datastructureandalgorithm.assets/image-20210808154049427.png)
  - 各个村庄的距离用边线表示(权)，计算出D村庄到其它各个村庄的最短距离? 
- 算法思路：
  - 通过Dijkstra计算图G中的最短路径时，需要指定一个起点D(即从顶点D开始计算)。
  - 此外，引进三个数组already_arr、dis和pre_visited。already_arr的作用是记录顶点是否已遍历过（0-未遍历；1-已遍历），而dis则是记录顶点到起点D的距离（初始值为无穷大）， pre_visited[i] = j表示初始起点 D 到达顶点 i 要最后经过顶点 j
  - 初始时，数组already_arr中只有起点D = 1；遍历与起点D相邻的点，获取距离并更新dis数组
  - 然后，从数组already_arr中找出**目前路径最短（dis最小）**且**already_arr[K] = 0**的顶点K，遍历与顶点K相邻的点且还未遍历过的点，获取距离并更新dis数组【条件是(出发顶点->index + index->i) < 目前出发顶点到 i 结点的距离】，全驱结点数组 pre_visited[i] = index，并且使already_arr[K] = 1
  - 重复第4步操作，直到遍历完所有顶点。
- 算法思路图解：

![无标题](Datastructureandalgorithm.assets/无标题.png)

```java
public class DijkstraDemo {
    public static void main(String[] args) {
        char[] vertex = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        int[][] weight = new int[vertex.length][vertex.length];
        final int N = 65536;
        weight[0] = new int[]{N, 12, N, N, N, 16, 14};
        weight[1] = new int[]{12, N, 10, N, N, 7, N};
        weight[2] = new int[]{N, N, 10, 3, 5, 6, N};
        weight[3] = new int[]{N, N, 3, N, 4, N, N};
        weight[4] = new int[]{N, N, 5, 4, N, 2, 8};
        weight[5] = new int[]{16, 7, 6, N, 2, N, 9};
        weight[6] = new int[]{14, N, N, N, 8, 9, N};

        //创建图对象并显示
        KGraph kGraph = new KGraph(vertex, weight);
        kGraph.showKGraph();
        //dijkstra算法求D点到其他点的最小距离
        kGraph.dijkstra(3);
        kGraph.show();
    }
}


class KGraph {
    private char[] vertex;  //顶点数组
    private int[][] weight; //邻接矩阵
    // 记录各个顶点是否访问过 1表示访问过,0未访问,会动态更新
    public int[] already_arr;
    // 每个下标对应的值为前一个顶点下标, 会动态更新
    public int[] pre_visited;
    // 记录出发顶点到其他所有顶点的距离,比如G为出发顶点，就会记录G到其它顶点的距离，会动态更新，求的最短距离就会存放到dis
    public int[] dis;

    //迪杰斯特拉算法实现
    public void dijkstra(int index) {
        //初始化dis数组
        Arrays.fill(dis, 65536);
        this.dis[index] = 0;    //设置出发顶点的访问距离为0
        //初始化前驱结点
        Arrays.fill(pre_visited, -1);
        //设置出发顶点已经被访问
        this.already_arr[index] = 1;
        update(index);

        for (int j = 1; j < vertex.length; j++) {
            int min = 65536;
            //更新新的访问顶点(注意不是出发顶点)
            for(int i = 0; i < already_arr.length; i++) {
                if(already_arr[i] == 0 && dis[i] < min ) {
                    min = dis[i];
                    index = i;
                }
            }
            //更新 index 顶点被访问过
            already_arr[index] = 1;
            update(index);     //更新出发顶点到index下标周围顶点的距离和周围顶点的前驱顶点
        }
    }

    //更新出发顶点到index下标周围顶点的距离和周围顶点的前驱顶点
    public void update(int index) {
        int len;
        for (int i = 0; i < vertex.length; i++) {
            // 出发顶点到 index 顶点的距离+从 index 顶点到 i 顶点的距离
            len = dis[index] + weight[index][i];
            // 如果 i 结点没有被访问过，并且上述距离(出发顶点->index + index->i) < 目前出发顶点到 i 结点的距离
            if (already_arr[i] == 0 && len < dis[i]) {
                //更新 i 结点的前驱结点为index，并且更新出发顶点到 i 结点的距离
                pre_visited[i] = index;
                dis[i] = len;
            }
        }
    }

    //显示最后的结果
    public void show() {
        System.out.println(Arrays.toString(dis));
    }

    //显示图
    public void showKGraph() {
        for (int[] link : weight) {
            System.out.println(Arrays.toString(link));
        }
    }

    //构造器
    public KGraph(char[] vertex, int[][] weight) {
        this.vertex = vertex;
        this.weight = weight;
        this.already_arr = new int[vertex.length];
        this.pre_visited = new int[vertex.length];
        this.dis = new int[vertex.length];
    }
}
```



### 10.9 Floyd算法

- 迪杰斯特拉算法通过选定的被访问顶点，求出从出发访问顶点到其他顶点的最短路径；而**弗洛伊德算法**中每一个顶点都是出发访问点，所以需要将每一个顶点看做被访问顶点，**求出从每一个顶点到其他顶点的最短路径**。
- 应用场景-最短路径问题：
  - ![image-20210808204020088](Datastructureandalgorithm.assets/image-20210808204020088.png)
  - 各个村庄的距离用边线表示(权)，计算每个村庄到其它各个村庄的最短距离? 
- 算法思路和图解：
  - 顶点 vi 到顶点 vk 的最短路径已知为 Lik，顶点 vk 到 vj 的最短路径已知为 Lkj，顶点 vi 到 vj 的路径为 Lij，则 vi 到 vj 的最短路径为：min((Lik+Lkj),Lij)
  - **三层分别遍历**中间顶点，出发顶点和终点顶点{'A', 'B', 'C', 'D', 'E', 'F', 'G'...}，注意**出发顶点与中间顶点、中间顶点与终点顶点并不要求直连**
  - ![image-20210808204701749](Datastructureandalgorithm.assets/image-20210808204701749.png)
  - 把A作为中间顶点的所有情况都进行遍历后得到
  - ![image-20210808204754758](Datastructureandalgorithm.assets/image-20210808204754758.png)

```java
public class FloydDemo {
    public static void main(String[] args) {
        char[] vertex = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        int[][] weight = new int[vertex.length][vertex.length];
        final int N = 65536;
        weight[0]=new int[]{0,5,7,N,N,N,2};
        weight[1]=new int[]{5,0,N,9,N,N,3};
        weight[2]=new int[]{7,N,0,N,8,N,N};
        weight[3]=new int[]{N,9,N,0,N,4,N};
        weight[4]=new int[]{N,N,8,N,0,5,4};
        weight[5]=new int[]{N,N,N,4,5,0,6};
        weight[6]=new int[]{2,3,N,N,4,6,0};

        //创建图对象
        FGraph fGraph = new FGraph(vertex, weight);
        //floyd算法处理并显示结果
        fGraph.floyd();
        fGraph.showFGraph();
    }
    
}

class FGraph {
    private char[] vertex;  //顶点数组
    //初始的邻接矩阵
    //同时记录出发顶点到其他所有顶点的距离,比如G为出发顶点，就会记录G到其它顶点的距离，会动态更新，求的最短距离就会存放到dis
    private int[][] dis;
    // 到达目顶点的前驱结点
    public int[][] pre;

    public void floyd() {
        int len;
        //遍历中间顶点
        for (int k = 0; k < vertex.length; k++) {
            //遍历出发顶点
            for (int i = 0; i < vertex.length; i++) {
                //遍历终点顶点
                for (int j = 0; j < vertex.length; j++) {
                    // 从i出发，经过k，最后到达j，i与k，k与j并不一定直连
                    len = dis[i][k] + dis[k][j];
                    if (len < dis[i][j]) {
                        // 满足条件更新距离和前驱结点
                        dis[i][j] = len;
                        // i与k，k与j并不一定直连，所以更新前驱结点也是pre[k][j](直连时=k)而不是k
                        pre[i][j] = pre[k][j];
                    }
                }
            }
        }
    }

    //显示dis数组和pre数组
    public void showFGraph() {
        System.out.println("dis");
        for (int[] link : dis) {
            System.out.println(Arrays.toString(link));
        }
        System.out.println("pre");
        for (int[] link : pre) {
            System.out.println(Arrays.toString(link));
        }
    }

    //构造器
    public FGraph(char[] vertex, int[][] dis) {
        this.vertex = vertex;
        this.dis = dis;
        this.pre = new int[vertex.length][vertex.length];
        //对pre进行初始化，前驱顶点的下标是自身的下标
        for (int i = 0; i < vertex.length; i++) {
            Arrays.fill(pre[i], i);
        }
    }
}
```



### 10.10 马踏棋盘算法

- 马踏棋盘：将马随机放在国际象棋的8×8棋盘Board[0～7][0～7]的某个方格中，马按走棋规则(马走日字)进行移动。要求每个方格只进入一次，走遍棋盘上全部64个方格

![image-20210808232049122](Datastructureandalgorithm.assets/image-20210808232049122.png)

- 马踏棋盘问题(骑士周游问题)实际上是图的深度优先搜索(DFS)的应用，可以用**回溯**（循环加递归，实质就是深度优先搜索）来解决，用**贪心算法**来进行优化

- 算法思路：

  1. 创建棋盘 chessBoard , 是一个二维数组

  2. 将当前位置设置为已经访问，然后根据当前位置，计算马儿还能走哪些位置，并放入到一个集合中(ArrayList), 最多有8个位置， 每走一步，就使用step+1

  3. 遍历ArrayList中存放的所有位置，看看哪个可以走通 , 如果走通，就继续，走不通，就**回溯**.

  4. 判断马儿是否完成了任务，使用  step 和**应该走的步数**比较 ， 如果没有达到数量，则表示没有完成任务，将整个棋盘置0
  5. 优化思路：在选择马儿下一步走的位置时，优先选择这些位置中的下一步可选择位置数少的位置

```java
public class HouseChessboard {
    private static int X = 8;   //棋盘列数
    private static int Y = 8;   //棋盘行数
    //创建一个数组，标记棋盘的各个位置是否被访问过
    private static boolean visited[][];
    //创建棋盘，记录step
    private static int chessboard[][];
    //所有位置被访问的标记
    private static boolean finished;

    public static void main(String[] args) {
        visited = new boolean[X][Y];
        chessboard = new int[X][Y];
        //测试耗时
        long start = System.currentTimeMillis();
        traverlChessboard(0, 0, 1);
        long end = System.currentTimeMillis();
        System.out.println("耗时：" + (end - start) + "ms");
        //输出棋盘最后情况
        for (int[] link : chessboard) {
            System.out.println(Arrays.toString(link));
        }

    }

    /**
     * Description: 完成马踏棋盘的算法
     * @param x: 马儿当前x坐标
     * @param y: 马儿当前y坐标
     * @param step: 马儿走的第几步，初始位置为第一步
     * @return void:
     */
    public static void traverlChessboard(int x, int y, int step) {
        chessboard[x][y] = step;
        //标记已访问
        visited[x][y] = true;
        //获取当前位置可以走的下一个位置的集合(行列与next方法内对应)
        ArrayList<Point> points = next(new Point(x, y));
        //对points进行排序
        sort(points);
        //遍历points
        while (!points.isEmpty()) {
            Point point = points.remove(0); //取出下一个可以走的位置
            if (!visited[point.x][point.y]) {   //说明还未被j
                traverlChessboard(point.x, point.y, step + 1);
            }
        }
        //回溯
        //判断马儿是否完成了任务，没有完成任务将整个棋盘置为0
        //step < X * Y:  1  棋盘还没有走完   2  棋盘处于一个回溯过程
        if (step < X * Y && !finished) {
            chessboard[x][y] = 0;
            visited[x][y] = false;
        } else {
            finished = true;
        }
    }

    /**
     * Description: 根据当前的位置（Point），计算马儿还能走哪些位置
     * @param curPoint: 当前的位置（Point）
     * @return java.util.ArrayList<java.awt.Point>: 可走位置的集合
     */
    public static ArrayList<Point> next(Point curPoint) {
        ArrayList<Point> points = new ArrayList<>();
        //创建一个Point
        Point p1 = new Point();
        //表示马儿可以走4这个位置
        if((p1.x = curPoint.x - 2) >= 0 && (p1.y = curPoint.y -1) >= 0) {
            points.add(new Point(p1));
        }
        //判断马儿可以走3这个位置
        if((p1.x = curPoint.x - 1) >=0 && (p1.y=curPoint.y-2)>=0) {
            points.add(new Point(p1));
        }
        //判断马儿可以走2这个位置
        if ((p1.x = curPoint.x + 1) < X && (p1.y = curPoint.y - 2) >= 0) {
            points.add(new Point(p1));
        }
        //判断马儿可以走1这个位置
        if ((p1.x = curPoint.x + 2) < X && (p1.y = curPoint.y - 1) >= 0) {
            points.add(new Point(p1));
        }
        //判断马儿可以走0这个位置
        if ((p1.x = curPoint.x + 2) < X && (p1.y = curPoint.y + 1) < Y) {
            points.add(new Point(p1));
        }
        //判断马儿可以走7这个位置
        if ((p1.x = curPoint.x + 1) < X && (p1.y = curPoint.y + 2) < Y) {
            points.add(new Point(p1));
        }
        //判断马儿可以走6这个位置
        if ((p1.x = curPoint.x - 1) >= 0 && (p1.y = curPoint.y + 2) < Y) {
            points.add(new Point(p1));
        }
        //判断马儿可以走5这个位置
        if ((p1.x = curPoint.x - 2) >= 0 && (p1.y = curPoint.y + 1) < Y) {
            points.add(new Point(p1));
        }

        return points;
    }

    //根据ArrayList<Point>的所有位置再求各位置的下一步位置个数，进行非递减排序
    public static void sort(ArrayList<Point> points) {
        points.sort(new Comparator<Point>() {
            @Override
            public int compare(Point o1, Point o2) {
                //先获取o1的下一步的所有位置个数
                int count1 = next(o1).size();
                int count2 = next(o2).size();
                if (count1 < count2) {
                    return -1;
                } else if (count1 == count2) {
                    return 0;
                } else {
                    return 1;
                }
            }
        });
    }
}
```

## 11. 回溯算法

- **解题思路：**

- **DFS 和回溯算法区别**
   DFS 是一个劲的往某一个方向搜索，而回溯算法建立在 DFS 基础之上的，但不同的是在搜索过程中，达到结束条件后，恢复状态，回溯上一层，再次搜索。因此回溯算法与 DFS 的区别就是有无状态重置

- **何时使用回溯算法**
   当问题需要 "回头"，以此来查找出所有的解的时候，使用回溯算法。即满足结束条件或者发现不是正确路径的时候(走不通)，要撤销选择，回退到上一个状态，继续尝试，直到找出所有解为止

- **怎么样写回溯算法(从上而下，※代表难点，根据题目而变化)**

   1. 画出递归树，找到状态变量(回溯函数的参数)，这一步非常重要※
   2. 根据题意，确立结束条件
   3. 找准选择列表(与函数参数相关),与第一步紧密关联※
   4. 判断是否需要剪枝
   5. 作出选择，递归调用，进入下一层
   6. 撤销选择

- **回溯问题的类型**

   | 类型       | 题目链接                                                     |
   | ---------- | ------------------------------------------------------------ |
   | 子集、组合 | [子集](https://leetcode-cn.com/problems/subsets/)、[子集\|\|](https://leetcode-cn.com/problems/subsets-ii/)、[组合](https://leetcode-cn.com/problems/combinations/)、[组合总和](https://leetcode-cn.com/problems/combination-sum/)、[组合总数\|\|](https://leetcode-cn.com/problems/combination-sum-ii/) |
   | 全排列     | [全排列](https://leetcode-cn.com/problems/permutations/)、[全排列 II](https://leetcode-cn.com/problems/permutations-ii/)、[字符串的全排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)、[字母大小写全排列](https://leetcode-cn.com/problems/letter-case-permutation/) |
   | 搜索       | [解数独](https://leetcode-cn.com/problems/sudoku-solver/)、[单词搜索](https://leetcode-cn.com/problems/word-search/)、[N皇后](https://leetcode-cn.com/problems/eight-queens-lcci/)、[分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)、[二进制手表](https://leetcode-cn.com/problems/binary-watch/) |

- **回到子集、组合类型问题上来**

### [11.1 子集](https://leetcode-cn.com/problems/subsets/)

   给你一个整数数组 `nums` ，数组中的元素**互不相同 **。返回该数组所有可能的**子集**（幂集）。

   解集不能包含重复的子集。你可以按任意顺序返回解集。

   ```java
   输入：nums = [1,2,3]
   输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
   ```

   

**解题步骤如下**

**①递归树**

![d8e07f0c876d9175df9f679fcb92505d20a81f09b1cb559afc59a20044cc3e8c-子集问题递归树](Datastructureandalgorithm.assets/d8e07f0c876d9175df9f679fcb92505d20a81f09b1cb559afc59a20044cc3e8c-子集问题递归树.png)

观察上图可得，选择列表里的数，都是选择路径(红色框)后面的数，比如[1]这条路径，他后面的选择列表只有"2、3"，[2]这条路径后面只有"3"这个选择，那么这个时候，就应该使用一个参数start，来标识当前的选择列表的起始位置。也就是标识每一层的状态，因此被形象的称为"状态变量",最终函数名如下：

```java
//nums为题目中的给的数组
//path为路径结果，要把每一条 path 加入结果集
void backtrack(int[] nums,List<Integer> path,int start)
```
**②找结束条件**
​此题所有路径都应该加入结果集，所以不存在结束条件。或者说当 start 参数越过数组边界的时候，程序就自己跳过下一层递归了，因此不需要手写结束条件,直接加入结果集:

```java
res为结果集，是全局变量List<List<Integer>> res,到时候要返回
res.add(path);//把每一条路径加入结果集
```

**③找选择列表**
在①中已经提到过了，子集问题的选择列表，是上一条选择路径之后的数

```java
for(int i=start;i<nums.size();i++)
```

**④判断是否需要剪枝**
从递归树中看到，路径没有重复的，也没有不符合条件的，所以不需要剪枝

**⑤做出选择(即for 循环里面的)**

```java
void backtrack(int[] nums,List<Integer> path, int start)
{
    for(int i=start;i<nums.length;i++)
    {
        path.add(nums[i]);//做出选择
        backtrack(nums,path,i+1);//递归进入下一层，注意i+1，标识下一个选择列表的开始位置，最重要的一步
    }
}
```

**⑤撤销选择**
整体的 backtrack 函数如下

```java
void backtrack(int[] nums,List<Integer> path, int start)
{
    res.add(path);
    for(int i=start;i<nums.size();i++)
    {
        path.add(nums[i]);//做出选择
        backtrack(nums,path,i+1);//递归进入下一层，注意i+1，标识下一个选择列表的开始位置，最重要的一步
        path.remove(path.size() - 1);//撤销选择
    }
}
```

**完整AC代码：**

```java
import java.util.*;
class Solution {
   public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(0, nums, res, new ArrayList<Integer>());
        return res;
    }

    private void backtrack(int i, int[] nums, List<List<Integer>> res, ArrayList<Integer> tmp) {
        res.add(new ArrayList<>(tmp));
        for (int j = i; j < nums.length; j++) {
            tmp.add(nums[j]);
            backtrack(j + 1, nums, res, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }

}
```



### [11.2 子集II(剪枝思想)](https://leetcode-cn.com/problems/subsets-ii/)

**B:子集 II(剪枝思想)--问题描述:给定一个可能包含重复元素的整数数组nums，返回该数组所有可能的子集（幂集**
输入: [1,2,2]
输出:
[
[2],
[1],
[1,2,2],
[2,2],
[1,2],
[]
]

**解题步骤**
①递归树

![1ccf07d0ab33b4b28c2bedb316e262f1d344dffefb4debde33fda98da1e8429e](Datastructureandalgorithm.assets/1ccf07d0ab33b4b28c2bedb316e262f1d344dffefb4debde33fda98da1e8429e.png)

可以发现，树中出现了大量重复的集合，②和③和第一个问题一样，不再赘述，我们直接看第四步

④判断是否需要剪枝，需要先对数组排序，使用排序函数 sort(nums.begin(),nums.end())
显然我们需要去除重复的集合，即需要剪枝，把递归树上的某些分支剪掉。那么应去除哪些分支呢？又该如何编码呢？

![7dd0461942d17bc38860b05a2b6a6461feae54ad141c64bfaace9127e1a29651](Datastructureandalgorithm.assets/7dd0461942d17bc38860b05a2b6a6461feae54ad141c64bfaace9127e1a29651.png)

观察上图不难发现，应该去除当前选择列表中，与上一个数重复的那个数，引出的分支，如 “2，2” 这个选择列表，第二个 “2” 是最后重复的，应该去除这个 “2” 引出的分支(去除图中红色大框中的分支)编码呢，刚刚说到是 “去除当前选择列表中，与上一个数重复的那个数，引出的分支”，说明当前列表最少有两个数，当i>start时，做选择的之前，比较一下当前数，与上一个数 (i-1) 是不是相同，相同则 continue:

```java
void backtrack(int[] nums , List<Integer> path , int start)
    {
        res.add(path);
        for(int i=start;i<nums.length;i++)
        {
            if(i>start&&nums[i]==nums[i-1])//剪枝去重
                continue;
        }
    }
```

⑤做出选择

```java
void backtrack(int[] nums , List<Integer> path , int start)
    {
        res.add(path);
        for(int i=start;i<nums.length;i++)
        {
            if(i>start&&nums[i]==nums[i-1])//剪枝去重
                continue;
            path.add(nums[i]);
            backtrack(nums,path,i+1);
        }
    }
```

⑥撤销选择
整体的backtrack函数如下

```java
Arrays.sort(nums);
void backtrack(int[] nums , List<Integer> path , int start)
    {
        res.add(path);
        for(int i=start;i<nums.length;i++)
        {
            if(i>start&&nums[i]==nums[i-1])//剪枝去重
                continue;
            path.add(nums[i]);
            backtrack(nums,path,i+1);
            path.remove(path.size() - 1);
        }
    }
```

**完整AC代码：**

```java
import java.util.*;
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums){
         Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        backTrack(nums,0,res,new ArrayList<>());
        return res;
    }

    public void backTrack(int[] nums , int start , List<List<Integer>> res ,  List<Integer> path ){
        res.add(new ArrayList<>(path));

        for(int i = start ; i < nums.length ; ++i){
            if(i>start && nums[i]==nums[i-1]) continue;//剪枝去重
            path.add(nums[i]);
            backTrack(nums,i+1,res,path);
            path.remove(path.size()-1);
        }

    }
}
```

### [11.3 组合](https://leetcode.cn/problems/combinations/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-ma-/)

根据搜索起点画出二叉树
既然是树形问题上的 深度优先遍历，因此首先画出树形结构。例如输入：n = 4, k = 2，我们可以发现如下递归结构：

- 如果组合里有 1 ，那么需要在 [2, 3, 4] 里再找 11 个数；
- 如果组合里有 2 ，那么需要在 [3, 4] 里再找 11数。注意：这里不能再考虑 11，因为包含 11 的组合，在第 1 种情况中已经包含。
- 依次类推（后面部分省略），以上描述体现的 递归 结构是：在以 nn 结尾的候选数组里，选出若干个元素。画出递归结构如下图：

![1599488203-TzmCXb-image](Datastructureandalgorithm.assets/1599488203-TzmCXb-image.png)

说明：叶子结点的信息体现在从根结点到叶子结点的路径上，因此需要一个表示路径的变量 `path`，它是一个列表，特别地，`path` 是一个栈；
每一个结点递归地在做同样的事情，区别在于搜索起点，因此需要一个变量 `start` ，表示在区间 `[start , n]` 里选出若干个数的组合；
可能有一些分支没有必要执行，我们放在优化中介绍。==友情提示：对于这一类问题，画图帮助分析是非常重要的解题方法==。

完整代码：

```java
import java.util.*;
public class Solution {
     public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (k <= 0 || n < k) {
            return res;
        }
        // 从 1 开始是题目的设定
        List<Integer> path = new ArrayList<>();
        backTrack(n, k, 1, res , path);
        return res;
    }

    private void backTrack(int n, int k, int start, List<List<Integer>> res ,List<Integer> path ) {
        // 递归终止条件是：path 的长度等于 k
        if (path.size() == k) {
            res.add(new ArrayList<>(path));
            return;
        }
        // 遍历可能的搜索起点
        for (int i = start; i <= n; i++) {
            // 向路径变量里添加一个数
            path.add(i);
            // 下一轮搜索，设置的搜索起点要加 1，因为组合数理不允许出现重复的元素
            backTrack(n, k, i + 1, res,path);
            // 重点理解这里：深度优先遍历有回头的过程，因此递归之前做了什么，递归之后需要做相同操作的逆向操作
            path.remove(path.size() - 1);
        }
    }
}
```



### [11.4 组合总和](https://leetcode.cn/problems/combination-sum/)

**给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。candidates 中的数字可以无限制重复被选取。**
**输入: candidates = [1,2,3], target = 3,**
**所求解集为:**
**[**
**[1,1,1],**
**[1,2],**
**[3]**
**]**

**解题步骤**
①递归树

![95513b4b31c8570d7c3b4b29cb09169e1ae981800602ec44ff3cfa20d662b72a](Datastructureandalgorithm.assets/95513b4b31c8570d7c3b4b29cb09169e1ae981800602ec44ff3cfa20d662b72a.png)

(绿色箭头上面的是路径，红色框[]则为结果，黄色框为选择列表)从上图看出，组合问题和子集问题一样，1,2 和 2,1 是同一个组合，因此 需要引入start参数标识，每个状态中选择列表的起始位置。另外，每个状态还需要一个 sum 变量，来记录当前路径的和，函数名如下：

```java
void backtrack(int[] nums,List<List<Integer>>res,List<Integer>path,int start,int sum,int target,int len)
```

②找结束条件
由题意可得，当路径总和等于 target 时候，就应该把路径加入结果集，并 return

```java
 if(target==sum)
        {
            res.add(new ArrayList<>(path));
            return;
        }
```

③找选择列表

```java
for(int i=start;i<nums.length;i++)
```

④判断是否需要剪枝
从①中的递归树中发现，当前状态的sum大于target的时候就应该剪枝，不用再递归下去了

```java
for(int i=start;i<nums.length;i++)
        {
            if(sum>target)//剪枝
                continue;
        }
```

⑤做出选择
题中说数可以无限次被选择，那么 i 就不用 +1 。即下一层的选择列表，从自身开始。并且要更新当前状态的sum

```java
for(int i=start;i<nums.length;i++)
        {
            if(sum>target)
                continue;
            path.add(nums[i]);
            backtrack(nums,res,path,i,sum+nums[i],target,len);//i不用+1(重复利用)，并更新当前状态的sum
        }
```

⑤撤销选择

```java
void backtrack(int[] nums,List<List<Integer>> res,List<Integer> path,int start,int sum,int target,int len){
        if(sum == target){
            res.add(new ArrayList(path));
            return;
        }
        for(int i=start;i<len;i++){
            //判断剪枝
            if(sum+nums[i]>target){
                continue;
            }
            path.add(nums[i]);
            backtrack(nums,res,path,i,sum+nums[i],target,len);
            path.remove(path.size()-1);
        }
    }
```

**完整AC代码：**

```java
class Solution {
   public List<List<Integer>> combinationSum(int[] candidates, int target) {
        int len = candidates.length;
        List<List<Integer>> res = new ArrayList<>();
        if (len == 0) {
            return res;
        }
        List<Integer> path = new ArrayList<>();
        backtrack(candidates, res, path , 0 , 0 , target , len);
        return res;
    }
    /**
     * @param candidates 候选数组
     * @param res        结果集列表
     * @param path       从根结点到叶子结点的路径
     * @param start      搜索起点
     * @param sum        路径和
     * @param target     目标值不变
     * @param len		候选数组的长度
     */
    public void backtrack(int[] candidates,List<List<Integer>> res,List<Integer> path,int start,int sum,int target,int len){
        if(sum == target){
            res.add(new ArrayList(path));
            return;
        }
        for(int i=start;i<len;i++){
            //判断剪枝
            if(sum+candidates[i]>target){
                continue;
            }
            path.add(candidates[i]);
            backtrack(candidates,res,path,i,sum+candidates[i],target,len);
            path.remove(path.size()-1);
        }
    }
    
    
}
```

### [11.5 组合总和II](https://leetcode.cn/problems/combination-sum-ii/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-3/)

与组合之和的区别在于：

- 组合之和的数字可以被无限制重复选取
- 本题中的数字，每一个组合中只能使用一次

相同点是：相同数字列表的不同排列视为一个结果。

这里我们使用和第 39 题和第 15 题（三数之和）类似的思路：不重复就需要按 顺序 搜索， 在搜索的过程中检测分支是否会出现重复结果 。注意：这里的顺序不仅仅指数组 candidates 有序，还指按照一定顺序搜索结果。

![1599718525-iXEiiy-image](Datastructureandalgorithm.assets/1599718525-iXEiiy-image.png)

![1599716342-gGiISM-image](Datastructureandalgorithm.assets/1599716342-gGiISM-image.png)

由第 39 题我们知道，数组 candidates 有序，也是 深度优先遍历 过程中实现「剪枝」的前提。
将数组先排序的思路来自于这个问题：去掉一个数组中重复的元素。很容易想到的方案是：先对数组 升序 排序，重复的元素一定不是排好序以后相同的连续数组区域的第 11 个元素。也就是说，剪枝发生在：同一层数值相同的结点第 22、33 ... 个结点，因为数值相同的第 11 个结点已经搜索出了包含了这个数值的全部结果，同一层的其它结点，候选数的个数更少，搜索出的结果一定不会比第 11 个结点更多，并且是第 11 个结点的子集。（说明：这段文字很拗口，大家可以结合具体例子，在纸上写写画画进行理解。）
说明：
解决这个问题可能需要解决 第 15 题（[三数之和](https://leetcode-cn.com/problems/3sum/)）、 第 47 题（[全排列 II](https://leetcode-cn.com/problems/permutations-ii/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liwe-2/)）、 第 39 题（[组合之和](https://leetcode-cn.com/problems/combination-sum/)）的经验；
对于如何去重还不太清楚的朋友，可以参考当前题解的 高赞置顶评论 。

完整代码：

```java
import java.util.*;

public class Solution {

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        int len = candidates.length;
        List<List<Integer>> res = new ArrayList<>();
        if (len == 0) {
            return res;
        }

        // 关键步骤
        Arrays.sort(candidates);
        
        List<Integer> path = new ArrayList<>();
        backtrack(candidates, target,len, 0, res, path);
        return res;
    }

    /**
     * @param candidates 候选数组
     * @param len        冗余变量
     * @param begin      从候选数组的 begin 位置开始搜索
     * @param target     表示剩余，这个值一开始等于 target，基于题目中说明的"所有数字（包括目标数）都是正整数"这个条件
     * @param path       从根结点到叶子结点的路径
     * @param res
     */
    private void backtrack(int[] candidates, int target , int len, int begin, List<List<Integer>> res , List<Integer> path) {
        if (target == 0) {
            res.add(new ArrayList<>(path));
            return;
        }
        for (int i = begin; i < len; i++) {
            // 大剪枝：减去 candidates[i] 小于 0，减去后面的 candidates[i + 1]、candidates[i + 2] 肯定也小于 0，因此用 break
            if (target - candidates[i] < 0) {
                break;
            }

            // 小剪枝：同一层相同数值的结点，从第 2 个开始，候选数更少，结果一定发生重复，因此跳过，用 continue
            if (i > begin && candidates[i] == candidates[i - 1]) {
                continue;
            }

            path.add(candidates[i]);
            // 调试语句 ①
            // System.out.println("递归之前 => " + path + "，剩余 = " + (target - candidates[i]));

            // 因为元素不可以重复使用，这里递归传递下去的是 i + 1 而不是 i
            backtrack(candidates, target - candidates[i] , len , i + 1 , res , path );

            path.remove(path.size() - 1);
            // 调试语句 ②
            // System.out.println("递归之后 => " + path + "，剩余 = " + (target - candidates[i]));
        }
    }

    public static void main(String[] args) {
        int[] candidates = new int[]{10, 1, 2, 7, 6, 1, 5};
        int target = 8;
        Solution solution = new Solution();
        List<List<Integer>> res = solution.combinationSum2(candidates, target);
        System.out.println("输出 => " + res);
    }
}
```



### 总结1

子集、组合类问题，关键是用一个 start 参数来控制选择列表！！最后回溯六步走：
①画出递归树，找到状态变量(回溯函数的参数)，这一步非常重要
②根据题意，确立结束条件
③找准选择列表(与函数参数相关),与第一步紧密关联※
④判断是否需要剪枝
⑤作出选择，递归调用，进入下一层
⑥撤销选择



###  [11.6 全排列](https://leetcode.cn/problems/permutations/)

给定一个 没有重复 数字的序列，返回其所有可能的全排列
输入: [1,2,3]
输出:
[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
<font color=red>解题步骤</font>
①递归树

![60930c71aa60549ff5c78700a4fc211a7f4304d6548352b7738173eab8d6d7d8](Datastructureandalgorithm.assets/60930c71aa60549ff5c78700a4fc211a7f4304d6548352b7738173eab8d6d7d8.png)

最下面的叶子节点，红色【】中的就是要求的结果)
然后我们来回想一下，整个问题的思考过程，这棵树是如何画出来的。首先，我们固定1，然后只有2、3可选：如果选2，那就只剩3可选，得出结果[1,2,3]；如果选3，那就只剩2可选，得出结果[1,3,2]。再来，如果固定2，那么只有1,3可选：如果选1，那就只剩3，得出结果[2,1,3].....
有没有发现一个规律：如果我们固定了(选择了)某个数，那么他的下一层的选择列表就是——除去这个数以外的其他数！！比如，第一次选择了2，那么他的下一层的选择列表只有1和3；如果选择了3，那么他的下一层的选择列表只有1和2,那么这个时候就要引入一个used数组来记录使用过的数字，算法函数如下：

```java
void backtrack(int[] nums , boolean[] used , List<List<Integer>> res ; List<Integer> path )//你也可以把used设置为全局变量
```

②找结束条件

```java
 if(path.size()==nums.length)
        {
            res.add(new ArrayList<>(path));
            return;
        }
```

③找准选择列表

```java
for(int i=0;i<nums.length;i++)
{
    if(!used[i])//从给定的数中除去用过的，就是当前的选择列表
    {
    }
}
```

④判断是否需要剪枝
不需要剪枝，或者你可以认为，!used[i]已经是剪枝

⑤做出选择

```java
for(int i=0;i<nums.length;i++)
{
    if(!used[i])//从给定的数中除去用过的，就是当前的选择列表
    {
        path.add(nums[i]);//做选择
        used[i]=true;//设置当前数已用
        backtrack(nums,used,res,path);//进入下一层
    }
}
```

⑥撤销选择
整体代码如下:

```java
 public void backtrack(int[] nums , boolean[] used , List<List<Integer>> res , List<Integer> path )//used初始化为false
    {
        if(path.size()==nums.length)
        {
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i=0;i<nums.length;i++)//从给定的数中除去，用过的数，就是当前的选择列表
        {
            if(!used[i])//如果没用过
            {
                path.add(nums[i]);//做选择
                used[i]=true;//设置当前数已用
                backtrack(nums,used,res,path);//进入下一层
                used[i]=false;//撤销选择
                path.remove(path.size() - 1);//撤销选择
            }
        }

    }
```

完整代码：

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
		
        boolean[] used = new boolean[nums.length];
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        backtrack(nums,used,res,path);
        return res;
        
    }
    
      public void backtrack(int[] nums , boolean[] used , List<List<Integer>> res , List<Integer> path )//used初始化为false
    {
        if(path.size()==nums.length)
        {
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i=0;i<nums.length;i++)//从给定的数中除去，用过的数，就是当前的选择列表
        {
            if(!used[i])//如果没用过
            {
                path.add(nums[i]);//做选择
                used[i]=true;//设置当前数已用
                backtrack(nums,used,res,path);//进入下一层
                used[i]=false;//撤销选择
                path.remove(path.size() - 1);//撤销选择
            }
        }

    }
    
    
    
}
```

### [11.7 全排列 II(剪枝思想)](https://leetcode-cn.com/problems/permutations-ii/)

给定一个可包含重复数字的序列，返回所有不重复的全排列。
输入: [1,2,2]
输出: [[1,2,2],[2,1,2],[2,2,1]]
很明显又是一个“重复”问题，在[子集II](https://leetcode-cn.com/problems/subsets-ii/)中，当遇到有重复元素求子集时，先对nums数组的元素**排序**，再用if(i>start&&nums[i]==nums[i-1])来判断是否剪枝，那么在排列问题中又该怎么做呢？

①递归树
依旧要画递归树，判断在哪里剪枝。这个判断不是凭空想出来，而是看树上的重复部分，而归纳出来的

![cc2e874824b271c5858d71d697497f6d7bab56fcf1600021d015e67c50ce4815](Datastructureandalgorithm.assets/cc2e874824b271c5858d71d697497f6d7bab56fcf1600021d015e67c50ce4815.png)

可以看到，有两组是各自重复的，那么应该剪去哪条分支？首先要弄懂，重复结果是怎么来的，比如最后边的分支，选了第二个2后，,竟然还能选第一个2，从而导致最右边整条分支都是重复的

![424c5bd8222eb40364adec57e5f9be5b5ab60642676d91d374b1fe004391b5cb](Datastructureandalgorithm.assets/424c5bd8222eb40364adec57e5f9be5b5ab60642676d91d374b1fe004391b5cb.png)

②③不再赘述，直接看④
④判断是否需要剪枝，如何编码
有了前面“子集、组合”问题的判重经验，同样首先要对题目中给出的nums数组排序，让重复的元素并列排在一起，在if(i>start&&nums[i]==nums[i-1])，基础上修改为if(i>0&&nums[i]==nums[i-1]&&!used[i-1])，语义为：当i可以选第一个元素之后的元素时(因为如果i=0，即只有一个元素，哪来的重复？有重复即说明起码有两个元素或以上,i>0)，然后判断当前元素是否和上一个元素相同？如果相同，再判断上一个元素是否能用？如果三个条件都满足，那么该分支一定是重复的，应该剪去，给出最终代码:

```java
void backtrack(int[] nums , boolean[] used , List<List<Integer>> res , List<Integer> path)//used初始化全为false
{
    if(path.size()==nums.length())
    {
        res.add(new ArrayList<>(path));
        return;
    }
    
    for(int i=0 ; i<nums.length ; i++)//从给定的数中除去，用过的数，就是当前的选择列表
    {
        if(!used[i])
        {
            if(i>0&&nums[i]==nums[i-1]&&!used[i-1])//剪枝，三个条件
                continue;
            path.add(nums[i]);//做选择
            used[i]=true;//设置当前数已用
            backtrack(nums,used,res,path);//进入下一层
            used[i]=false;//撤销选择
            path.remove(path.size() - 1);//撤销选择
        }
    }
}
```

完整代码：

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
	    Arrays.sort(nums);
        boolean[] used = new boolean[nums.length];
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        backtrack(nums,used,res,path);
        return res;
    }
    
    public void backtrack(int[] nums , boolean[] used , List<List<Integer>> res , List<Integer> path)//used初始化全为false
	{
        if(path.size()==nums.length())
        {
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i=0 ; i<nums.length ; i++)//从给定的数中除去，用过的数，就是当前的选择列表
        {
            if(!used[i])
            {
                if(i>0&&nums[i]==nums[i-1]&&!used[i-1])//剪枝，三个条件
                    continue;
                path.add(nums[i]);//做选择
                used[i]=true;//设置当前数已用
                backtrack(nums,used,res,path);//进入下一层
                used[i]=false;//撤销选择
                path.remove(path.size() - 1);//撤销选择
            }
        }
	}  
    
}
```

### [11.8 字符串的全排列(剪枝思想)](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。
示例:
		输入：s = "abc"
		输出：["abc","acb","bac","bca","cab","cba"]
解题步骤：
其实这题跟例题B一模一样，换汤不换药，把nums数组换成了字符串，直接上最终代码，记得先用sort对字符串s进行排序，再传进来！

```java
class Solution {
    public String[] permutation(String s)  {
	    char[] nums = s.toCharArray();
        Arrays.sort(nums);
        boolean[] used = new boolean[nums.length];
        List<String> res = new ArrayList<>();
        List<Character> path = new ArrayList<>();
        backtrack(nums,used,res,path);
        return res.toArray(new String[res.size()]);
    }
    
    public void backtrack(char[] nums , boolean[] used , List<String> res , List<Character> path)//used初始化全为false
	{
        if(path.size()==nums.length)
        {
            //字符集合转为字符串对象
            StringBuilder str = new StringBuilder();
        for (Character character : path) {// 对ArrayList进行遍历，将字符放入StringBuilder中
            str.append(character);
        }
            res.add(str.toString());
            return;
        }
        
        for(int i=0 ; i < nums.length ; i++)//从给定的数中除去，用过的数，就是当前的选择列表
        {
            if(!used[i])
            {
                if(i>0&&nums[i]==nums[i-1]&&!used[i-1])//剪枝，三个条件
                    continue;
                path.add(nums[i]);//做选择
                used[i]=true;//设置当前数已用
                backtrack(nums,used,res,path);//进入下一层
                used[i]=false;//撤销选择
                path.remove(path.size() - 1);//撤销选择
            }
        }
	}  
    
}
```

### [11.9 字母大小写全排列](https://leetcode-cn.com/problems/letter-case-permutation/)

完整AC代码：

**大小写字母的二进制ASCII码只有第6位有所不同**则我们可以利用异或位运算（XOR）来实现相互转换。则易证 ***一个字母 XOR （32 or（1 << 5））***即可以轻松地转换大小写。这边转换是异或了一个空格。因为空格的ASCII码即为32！！！！！！

```java
if(ch >= 'a' && ch <= 'z' || ch >= 'A' && ch <= 'Z') ch ^= ' ';
if(ch >= 'a' && ch <= 'z' || ch >= 'A' && ch <= 'Z') ch ^= 32;
```



```java
class Solution {
    public List<String> letterCasePermutation(String s) {
        List<String> res = new ArrayList<>();
        char[] ch = s.toCharArray();
        int n = ch.length;
        backTracking(ch, 0, n ,res);
        return res;
    }

    private void backTracking(char[] ch, int index, int n , List<String> res) {
        res.add(new String(ch)); 
        for (int i = index; i < n; i++) {
            if (isDigit(ch[i])) {
                continue;
            }
            ch[i] ^= ' ';
            backTracking(ch, i + 1, n ,res);
            ch[i] ^= ' ';
        }
    }

    private boolean isDigit(char c) {
        if (c >= '0' && c <= '9') {
            return true;
        }
        return false;
    }
}
```

### [11.10 解数独](https://leetcode.cn/problems/sudoku-solver/solution/hui-su-fa-jie-shu-du-by-i_use_python/)

![img](Datastructureandalgorithm.assets/250px-sudoku-by-l2g-20050714svg.png)

```java
输入：board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
输出：[["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
```

解数独思路：
类似人的思考方式去尝试，行，列，还有 3*3 的方格内数字是 1~9 不能重复。我们尝试填充，如果发现重复了，那么擦除重新进行新一轮的尝试，直到把整个数组填充完成。

算法步骤:

- 数独首先行，列，还有 3*3 的方格内数字是 1~9 不能重复。*
- 声明布尔数组，表明行列中某个数字是否被使用了， 被用过视为 true，没用过为 false。
- 初始化布尔数组，表明哪些数字已经被使用过了。
- 尝试去填充数组，只要行，列， 还有 3*3 的方格内 出现已经被使用过的数字，我们就不填充，否则尝试填充。
- 如果填充失败，那么我们需要回溯。将原来尝试填充的地方改回来。
- 递归直到数独被填充完成。

完整代码:

```java
class Solution {
    public void solveSudoku(char[][] board) {
        // 三个布尔数组 表明 行, 列, 还有 3*3 的方格的数字是否被使用过
        boolean[][] rowUsed = new boolean[9][10];
        boolean[][] colUsed = new boolean[9][10];
        boolean[][][] boxUsed = new boolean[3][3][10];
        // 初始化
        for(int row = 0; row < board.length; row++){
            for(int col = 0; col < board[0].length; col++) {
                int num = board[row][col] - '0';
                if(1 <= num && num <= 9){
                    rowUsed[row][num] = true;
                    colUsed[col][num] = true;
                    boxUsed[row/3][col/3][num] = true;
                }
            }
        }
        // 递归尝试填充数组 
        recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, 0, 0);
    }
    
    private boolean recusiveSolveSudoku(char[][]board, boolean[][]rowUsed, boolean[][]colUsed, boolean[][][]boxUsed, int row, int col){
        // 边界校验, 如果已经填充完成, 返回true, 表示一切结束
        if(col == board[0].length){
            col = 0;
            row++;
            if(row == board.length){
                return true;
            }
        }
        // 是空则尝试填充, 否则跳过继续尝试填充下一个位置
        if(board[row][col] == '.') {
            // 尝试填充1~9
            for(int num = 1; num <= 9; num++){
                boolean canUsed = !(rowUsed[row][num] || colUsed[col][num] || boxUsed[row/3][col/3][num]);
                if(canUsed){
                    rowUsed[row][num] = true;
                    colUsed[col][num] = true;
                    boxUsed[row/3][col/3][num] = true;
                    
                    board[row][col] = (char)('0' + num);
                    if(recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, row, col + 1)){
                        return true;
                    }
                    board[row][col] = '.';
                    
                    rowUsed[row][num] = false;
                    colUsed[col][num] = false;
                    boxUsed[row/3][col/3][num] = false;
                }
            }
        } else {
            return recusiveSolveSudoku(board, rowUsed, colUsed, boxUsed, row, col + 1);
        }
        return false;
    }
}

```

###  [11.11 单词搜索](https://leetcode.cn/problems/word-search/comments/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

![img](Datastructureandalgorithm.assets/word2.jpg)

```java
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

![img](Datastructureandalgorithm.assets/word3.jpg)

```java
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
输出：false
```

完整代码(可理解)：

```java
/**
* 回溯法：相比于DFS，多了一步『撤销修改节点状态』
*/
class Solution {
    private boolean find;  // 定义为成员变量，方便以下两个成员方法使用和修改

    public boolean exist(char[][] board, String word) {
        if (board == null) return false;
        int m = board.length, n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        find = false;

        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                backtracking(i, j, board, word, visited, 0);  // 从左上角开始遍历棋盘每个格子
            }
        }
        return find;
    }

    /**
    * i,j,board：棋盘格及当前元素的坐标
    * word: 要搜索的目标单词
    * visited：记录当前格子是否已被访问过
    * pos: 记录目标单词的字符索引，只有棋盘格字符和pos指向的字符一致时，才有机会继续搜索接下来的字符；如果pos已经过了目标单词的尾部了，那么便说明找到目标单词了
    */
    public void backtracking(int i, int j, char[][] board, String word, boolean[][] visited, int pos){
        // 超出边界、已经访问过、已找到目标单词、棋盘格中当前字符已经和目标字符不一致了
        if(i<0 || i>= board.length || j<0 || j >= board[0].length || visited[i][j] || find
           || board[i][j]!=word.charAt(pos))  return;

        if(pos == word.length()-1){
            find = true;
            return;
        }

        visited[i][j] = true;  // 修改当前节点状态
        backtracking(i+1, j, board, word, visited, pos+1);  // 遍历子节点
        backtracking(i-1, j, board, word, visited, pos+1);
        backtracking(i, j+1, board, word, visited, pos+1);
        backtracking(i, j-1, board, word, visited, pos+1);
        visited[i][j] = false; // 撤销修改
    }

}
```

### [11.12 N皇后问题](https://leetcode.cn/problems/eight-queens-lcci/solution/ba-huang-hou-hui-su-suan-fa-jing-dian-ti-mu-xiang-/)

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

![img](Datastructureandalgorithm.assets/20211020232201.png)

- 输入：n = 4
- 输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
- 解释：如上图所示，4 皇后问题存在两个不同的解法。

示例 2：

- 输入：n = 1
- 输出：[["Q"]]

![51.N皇后](Datastructureandalgorithm.assets/20210130182532303.jpg)

从图中，可以看出，二维矩阵中矩阵的高就是这棵树的高度，矩阵的宽就是树形结构中每一个节点的宽度。那么我们用皇后们的约束条件，来回溯搜索这棵树，**只要搜索到了树的叶子节点，说明就找到了皇后们的合理位置了**。

 回溯三部曲

按照我总结的如下回溯模板，我们来依次分析：

```text
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }
    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

- 递归函数参数

我依然是定义全局变量二维数组result来记录最终结果。

参数n是棋盘的大小，然后用row来记录当前遍历到棋盘的第几层了。

代码如下：

```java
List<List<string>> result;
public void backTrack(int n, int row, char[][] chessboard)
```

- 递归终止条件

在如下树形结构中： ![51.N皇后](Datastructureandalgorithm.assets/20210130182532303-16542559884329.jpg)

可以看出，当递归到棋盘最底层（也就是叶子节点）的时候，就可以收集结果并返回了。

代码如下：

```java
if (row == n) {
    result.add(Array2List(chessboard));
    return;
}
```

- 单层搜索的逻辑

递归深度就是row控制棋盘的行，每一层里for循环的col控制棋盘的列，一行一列，确定了放置皇后的位置。

每次都是要从新的一行的起始位置开始搜，所以都是从0开始。

代码如下：

```cpp
for (int col = 0; col < n; col++) {
    if (isValid(row, col, chessboard, n)) { // 验证合法就可以放
        chessboard[row][col] = 'Q'; // 放置皇后
        backtracking(n, row + 1, chessboard);
        chessboard[row][col] = '.'; // 回溯，撤销皇后
    }
}
```

- 验证棋盘是否合法

按照如下标准去重：

1. 不能同行
2. 不能同列
3. 不能同斜线 （45度和135度角）

代码如下：

```cpp
public boolean isValid(int row, int col, int n, char[][] chessboard) {
        // 检查列
        for (int i=0; i<row; ++i) { // 相当于剪枝
            if (chessboard[i][col] == 'Q') {
                return false;
            }
        }
        // 检查45度对角线
        for (int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) {
            if (chessboard[i][j] == 'Q') {
                return false;
            }
        }
        // 检查135度对角线
        for (int i=row-1, j=col+1; i>=0 && j<=n-1; i--, j++) {
            if (chessboard[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }
```

在这份代码中，细心的同学可以发现为什么没有在同行进行检查呢？因为在单层搜索的过程中，每一层递归，只会选for循环（也就是同一行）里的一个元素，所以不用去重了。

完整代码：

```java
class Solution {
    List<List<String>> res = new ArrayList<>();
    public List<List<String>> solveNQueens(int n) {
        char[][] chessboard = new char[n][n];
        for (char[] c : chessboard) {
            Arrays.fill(c, '.');
        }
        backTrack(n, 0, chessboard);
        return res;
    }


    public void backTrack(int n, int row, char[][] chessboard) {
        if (row == n) {
            res.add(Array2List(chessboard));
            return;
        }

        for (int col = 0;col < n; ++col) {
            if (isValid (row, col, n, chessboard)) {
                chessboard[row][col] = 'Q';
                backTrack(n, row+1, chessboard);
                chessboard[row][col] = '.';
            }
        }

    }


    public List Array2List(char[][] chessboard) {
        List<String> list = new ArrayList<>();
        for (char[] c : chessboard) {
            list.add(String.copyValueOf(c));
        }
        return list;
    }


    public boolean isValid(int row, int col, int n, char[][] chessboard) {
        // 检查列
        for (int i=0; i<row; ++i) { // 相当于剪枝
            if (chessboard[i][col] == 'Q') {
                return false;
            }
        }
        // 检查45度对角线
        for (int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) {
            if (chessboard[i][j] == 'Q') {
                return false;
            }
        }
        // 检查135度对角线
        for (int i=row-1, j=col+1; i>=0 && j<=n-1; i--, j++) {
            if (chessboard[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }
}
```

### [11.13 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/solution/131-fen-ge-hui-wen-chuan-hui-su-sou-suo-yp2jq/)

本题这涉及到两个关键问题：

- 切割问题，有不同的切割方式
- 判断回文

相信这里不同的切割方式可以搞懵很多同学了。这种题目，想用for循环暴力解法，可能都不那么容易写出来，所以要换一种暴力的方式，就是回溯。一些同学可能想不清楚 回溯究竟是如何切割字符串呢？我们来分析一下切割，其实切割问题类似组合问题。

- 例如对于字符串abcdef：
  - 组合问题：选取一个a之后，在bcdef中再去选取第二个，选取b之后在cdef中在选组第三个.....。
  - 切割问题：切割一个a之后，在bcdef中再去切割第二段，切割b之后在cdef中在切割第三段.....。

感受出来了不？所以切割问题，也可以抽象为一颗树形结构，如图：

![image.png](Datastructureandalgorithm.assets/1631605968-vKKScH-image.png)

递归用来纵向遍历，for循环用来横向遍历，切割线（就是图中的红线）切割到字符串的结尾位置，说明找到了一个切割方法。此时可以发现，切割问题的回溯搜索的过程和组合问题的回溯搜索的过程是差不多的。

- 回溯三部曲

递归函数参数
全局变量数组path存放切割后回文的子串，二维数组result存放结果集。 （这两个参数可以放到函数参数里）本题递归函数参数还需要startIndex，因为切割过的地方，不能重复切割，和组合问题也是保持一致的。在回溯算法：[求组合总和（二）](https://leetcode.cn/link/?target=https%3A%2F%2Fprogrammercarl.com%2F0039.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.html)中我们深入探讨了组合问题什么时候需要startIndex，什么时候不需startIndex。

代码如下：

```java
private void backTracking(String s, int startIndex)
```

- 递归函数终止条件

  ![image.png](Datastructureandalgorithm.assets/1631606009-OMGnoi-image.png)

  

  从树形结构的图中可以看出：切割线切到了字符串最后面，说明找到了一种切割方法，此时就是本层递归的终止终止条件。那么在代码里什么是切割线呢？在处理组合问题的时候，递归参数需要传入startIndex，表示下一轮递归遍历的起始位置，这个startIndex就是切割线。

  终止条件代码如下：

  ```java
  //如果起始位置大于s的大小，说明找到了一组分割方案
          if (startIndex >= s.length()) {
              lists.add(new ArrayList(deque));
              return;
          }
  ```

  - 单层搜索的逻辑

  来看看在递归循环，中如何截取子串呢？在`for (int i = startIndex; i < s.size(); i++)`循环中，我们定义了起始位置`startIndex`，那么 `[startIndex, i]` 就是要截取的子串。首先判断这个子串是不是回文，如果是回文，就加入在`Deque<String> deque`中，deque用来记录切割过的回文子串

  代码如下：

  ```java
  for (int i = startIndex; i < s.length(); i++) {
              //如果是回文子串，则记录
              if (isPalindrome(s, startIndex, i)) {
                  String str = s.substring(startIndex, i + 1);
                  deque.addLast(str);
              } else {
                  continue;
              }
              //起始位置后移，保证不重复
              backTracking(s, i + 1);
              deque.removeLast();
          }
  ```

  - 判断回文子串

  可以使用双指针法，一个指针从前向后，一个指针从后先前，如果前后指针所指向的元素是相等的，就是回文字符串了。

  ```java
  //判断是否是回文串
      private boolean isPalindrome(String s, int startIndex, int end) {
          for (int i = startIndex, j = end; i < j; i++, j--) {
              if (s.charAt(i) != s.charAt(j)) {
                  return false;
              }
          }
          return true;
      }
  ```

  - 完整代码

  ```java
  class Solution {
      List<List<String>> lists = new ArrayList<>();
      Deque<String> deque = new LinkedList<>();
  
      public List<List<String>> partition(String s) {
          backTracking(s, 0);
          return lists;
      }
  
      private void backTracking(String s, int startIndex) {
          //如果起始位置大于s的大小，说明找到了一组分割方案
          if (startIndex >= s.length()) {
              lists.add(new ArrayList(deque));
              return;
          }
          for (int i = startIndex; i < s.length(); i++) {
              //如果是回文子串，则记录
              if (isPalindrome(s, startIndex, i)) {
                  String str = s.substring(startIndex, i + 1);
                  deque.addLast(str);
              } else {
                  continue;
              }
              //起始位置后移，保证不重复
              backTracking(s, i + 1);
              deque.removeLast();
          }
      }
      //判断是否是回文串
      private boolean isPalindrome(String s, int startIndex, int end) {
          for (int i = startIndex, j = end; i < j; i++, j--) {
              if (s.charAt(i) != s.charAt(j)) {
                  return false;
              }
          }
          return true;
      }
  }
  ```

### 11.14 二进制手表

- 解题步骤：

  1.读懂题意，把题目尽可能抽象成“子集、排列、组合”类型问题本题的题目总结而言就是：有十盏灯，我分别给他编号0-9，号码0-3代表小时，号码4-9代表分钟，然后每盏灯又代表着不同数字，如下图：

  ![image.png](Datastructureandalgorithm.assets/b3f1697294a9d60841bc4a9f705d346fe2bc66ee0a14763774a3320cf2fb1d0d-image.png)

(灯泡中的红色数字,其实就是二进制转换，题目中的图也有标)然后从10盏灯中挑选n盏打开，问你有多少种组合，返回这些组合代表的时间。这样一翻译，是不是有点“组合”类型问题的味道了？说白了就是：**==从n个数里面挑选k个，返回组合==**。如果你能形成这种抽象思想，那么你就成功一大半了

2.回溯六步走

①画出递归树，找到状态变量(回溯函数的参数)，这一步非常重要
②根据题意，确立结束条件
③找准选择列表(与函数参数相关),与第一步紧密关联
④判断是否需要剪枝
⑤作出选择，递归调用，进入下一层
⑥撤销选择

![1.png](Datastructureandalgorithm.assets/4cb75ced126e1d788ed9a0c0e91b61d9a9cb9303c576940a0b02323b9cc7f666-1.png)

![2.png](Datastructureandalgorithm.assets/474f3d527c3e94d57e673bf4bd92cfb3eaea8d579e091c1bdfa6a7477270e020-2.png)

我们接下来思考，回溯函数需要什么哪些参数，来表示当前状态。首先灯是越来越少的，所以需要一个参数num,表示剩余可亮的灯数，直到num等于0就应该结束；然后还需要参数start，来指示当前可选择的灯的开始位置，比如n=2我选了7号灯,然后剩下的一盏灯，只能选8号或9号，你不可能回去选0-6号，因为会导致重复，这个问题在“子集、组合”类型问题中说过，详细请看顶部的文章；最后还需要一个time参数，来表示当前状态的时间。算法签名如下：

```java
int[] hash = {1,2,4,8,16,32};//数组映射灯对应的数字
private void backtrack(int num , int start , int[] time , List<String> res , int[] hash )
```

②根据题意，确立结束条件
这个上面提到过了，当num=0就是没有灯可以点亮了，就应该return，加入结果集

```java
if(num == 0 ){
    if(time[0] > 11 || time[1] > 59) return;
    String tempHour = String.valueOf(time[0]);
    String tempMinue = String.valueOf(time[1]);
    if(tempMinue.length() == 1) tempMinue = "0" + tempMinue; //如果分钟数是个位数，需要补零
    res.add(tempHour + ":" + tempMinue);
    return;
}
```

③找准选择列表
从参数start标识的位置开始，到最后一盏灯，都是可选的

```java
for(int i=start;i<10;i++) {}
```

④判断是否需要剪枝
当hour>11或minute>59的时候，无论还有没有灯可以点亮，都不用再继续递归下去，因为后面只会越增越多，应该剪枝

```java
if(time[0] > 11 || time[1] > 59) continue;
```

⑥撤销选择

```java
for(int i = start ; i < 10 ; i++ ){
    if(time[0] > 11 || time[1] > 59) continue;
    int[] store = Arrays.copyOf(time , 2);//数组拷贝，临时存放
    if(i < 4){
        time[0] += hash[i];
    }else{
        time[1] += hash[i-4];
    }
    backtrack(num - 1 , i + 1 , time , res , hash);
    time = store;//撤销选择

}
```

完整AC代码：

```java
class Solution {
    public List<String> readBinaryWatch(int turnedOn) {
        int[] hash = {1,2,4,8,16,32};
        List<String> res = new ArrayList<>();
        backtrack(turnedOn , 0 , new int[2] , res , hash);
        return  res;
    }

    private void backtrack(int num , int start , int[] time , List<String> res , int[] hash ){
        if(num == 0 ){
            if(time[0] > 11 || time[1] > 59) return;
            String tempHour = String.valueOf(time[0]);
            String tempMinue = String.valueOf(time[1]);
            if(tempMinue.length() == 1) tempMinue = "0" + tempMinue;
            res.add(tempHour + ":" + tempMinue);
            return;
        }
        
        for(int i = start ; i < 10 ; i++ ){
            if(time[0] > 11 || time[1] > 59) continue;
            int[] store = Arrays.copyOf(time , 2);
            if(i < 4){
                time[0] += hash[i];
            }else{
                time[1] += hash[i-4];
            }
            backtrack(num - 1 , i + 1 , time , res , hash);
            time = store;
            
        }
        
    }

    
}
```

### 11.15 岛屿问题总结

- DFS的基本结构

  二叉树遍历:

  ```java
  void traverse(TreeNode root) {
      // 判断 base case
      if (root == null) {
          return;
      }
      // 访问两个相邻结点：左子结点、右子结点
      traverse(root.left);
      traverse(root.right);
  }
  ```

  可以看到，二叉树的 DFS 有两个要素：「访问相邻结点」和「判断 base case」。

  第一个要素是访问相邻结点。二叉树的相邻结点非常简单，只有左子结点和右子结点两个。二叉树本身就是一个递归定义的结构：一棵二叉树，它的左子树和右子树也是一棵二叉树。那么我们的 DFS 遍历只需要递归调用左子树和右子树即可。

  第二个要素是 判断 base case。一般来说，二叉树遍历的 base case 是 root == null。这样一个条件判断其实有两个含义：一方面，这表示 root 指向的子树为空，不需要再往下遍历了。另一方面，在 root == null 的时候及时返回，可以让后面的 root.left 和 root.right 操作不会出现空指针异常。

  对于网格上的 DFS，我们完全可以参考二叉树的 DFS，写出网格 DFS 的两个要素。

- 网格类问题的DFS遍历方法

  岛屿问题是一类典型的网格问题。每个格子中的数字可能是 0 或者 1。我们把数字为 0 的格子看成海洋格子，数字为 1 的格子看成陆地格子，这样相邻的陆地格子就连接成一个岛屿。

  ![岛屿问题示例](Datastructureandalgorithm.assets/c36f9ee4aa60007f02ff4298bc355fd6160aa2b0d628c3607c9281ce864b75a2.jpg)

  网格结构中的格子有多少相邻结点？答案是上下左右四个。对于格子 (r, c) 来说（r 和 c 分别代表行坐标和列坐标），四个相邻的格子分别是 (r-1, c)、(r+1, c)、(r, c-1)、(r, c+1)。换句话说，网格结构是「四叉」的。

  ![网格结构中四个相邻的格子](Datastructureandalgorithm.assets/63f5803e9452ccecf92fa64f54c887ed0e4e4c3434b9fb246bf2b410e4424555.jpg)

  其次，网格 DFS 中的 base case 是什么？从二叉树的 base case 对应过来，应该是网格中不需要继续遍历、grid[r][c] 会出现数组下标越界异常的格子，也就是那些超出网格范围的格子。

  ![网格 DFS 的 base case](Datastructureandalgorithm.assets/5a91ec351bcbe8e631e7e3e44e062794d6e53af95f6a5c778de369365b9d994e.jpg)

  这一点稍微有些反直觉，坐标竟然可以临时超出网格的范围？这种方法我称为「**先污染后治理**」—— 甭管当前是在哪个格子，先往四个方向走一步再说，如果发现走出了网格范围再赶紧返回。这跟二叉树的遍历方法是一样的，先递归调用，发现 root == null 再返回。

  这样，我们得到了网格 DFS 遍历的框架代码：

  ```java
  void dfs(int[][] grid, int r, int c) {
      // 判断 base case
      // 如果坐标 (r, c) 超出了网格范围，直接返回
      if (!inArea(grid, r, c)) {
          return;
      }
      // 访问上、下、左、右四个相邻结点
      dfs(grid, r - 1, c);
      dfs(grid, r + 1, c);
      dfs(grid, r, c - 1);
      dfs(grid, r, c + 1);
  }
  
  // 判断坐标 (r, c) 是否在网格中
  boolean inArea(int[][] grid, int r, int c) {
      return 0 <= r && r < grid.length 
          	&& 0 <= c && c < grid[0].length;
  }
  ```

- 如何避免重复遍历

  网格结构的 DFS 与二叉树的 DFS 最大的不同之处在于，遍历中可能遇到遍历过的结点。这是因为，网格结构本质上是一个「图」，我们可以把每个格子看成图中的结点，每个结点有向上下左右的四条边。在图中遍历时，自然可能遇到重复遍历结点。这时候，DFS 可能会不停地「兜圈子」，永远停不下来，如下图所示：

  ![DFS 遍历可能会兜圈子（动图）](Datastructureandalgorithm.assets/7fec64afe8ab72c5df17d6a41a9cc9ba3879f58beec54a8791cbf108b9fd0685.gif)

  如何避免这样的重复遍历呢？答案是标记已经遍历过的格子。以岛屿问题为例，我们需要在所有值为 1 的陆地格子上做 DFS 遍历。每走过一个陆地格子，就把格子的值改为 2，这样当我们遇到 2 的时候，就知道这是遍历过的格子了。也就是说，每个格子可能取三个值：

  - 0 —— 海洋格子
  - 1 —— 陆地格子（未遍历过）
  - 2 —— 陆地格子（已遍历过）

  我们在框架代码中加入避免重复遍历的语句：

  ```java
  void dfs(int[][] grid, int r, int c) {
      // 判断 base case
      if (!inArea(grid, r, c)) {
          return;
      }
      // 如果这个格子不是岛屿，直接返回
      if (grid[r][c] != 1) {
          return;
      }
      grid[r][c] = 2; // 将格子标记为「已遍历过」
      // 访问上、下、左、右四个相邻结点
      dfs(grid, r - 1, c);
      dfs(grid, r + 1, c);
      dfs(grid, r, c - 1);
      dfs(grid, r, c + 1);
  }
  // 判断坐标 (r, c) 是否在网格中
  boolean inArea(int[][] grid, int r, int c) {
      return 0 <= r && r < grid.length 
          	&& 0 <= c && c < grid[0].length;
  }
  ```

  ![标记已遍历的格子](Datastructureandalgorithm.assets/20fe202fb5e5fc5048e140c29310c1bcbb17661860d2441e8a3feb1236a2e44d.gif)

  这样，我们就得到了一个岛屿问题、乃至各种网格问题的通用 DFS 遍历方法。以下所讲的几个例题，其实都只需要在 DFS 遍历框架上稍加修改而已。

  小贴士：在一些题解中，可能会把「已遍历过的陆地格子」标记为和海洋格子一样的 0，美其名曰「陆地沉没方法」，即遍历完一个陆地格子就让陆地「沉没」为海洋。这种方法看似很巧妙，但实际上有很大隐患，因为这样我们就无法区分「海洋格子」和「已遍历过的陆地格子」了。如果题目更复杂一点，这很容易出 bug。

### 11.16 岛屿数量

- 问题描述

  给一个01矩阵，1代表是陆地，0代表海洋， 如果两个1相邻，那么这两个1属于同一个岛。我们只考虑上下左右为相邻。
  岛屿: 相邻陆地可以组成一个岛屿（相邻:上下左右） 判断岛屿个数。
  例如：
  输入
  [[1,1,0,0,0],
  [0,1,0,1,1],
  [0,0,0,1,1],
  [0,0,0,0,0],
  [0,0,1,1,1]]
  对应的输出为3

```java
输入：
[[1,1,0,0,0],[0,1,0,1,1],[0,0,0,1,1],[0,0,0,0,0],[0,0,1,1,1]]
返回值：3
```

- 完整代码

```java
class Solution {
    private int res;
    public int numIslands(char[][] grid) {
        res = 0;
        //从网格的每一个格子为入口遍历
        for (int i = 0; i < grid.length; i ++) {
            for (int j = 0; j < grid[0].length; j ++) {
               	//如果遇到'1'的岛屿，一定有一个岛屿res+1  
                if (grid[i][j] == '1') {
                    dfsGrid(grid, i, j);
                    res ++;
                }
            }
        }
        return res;
    }

    private void dfsGrid(char[][] grid, int row, int col) {
        if (row >= grid.length || col >= grid[0].length || row < 0 || col < 0) {
            return;
        }
        //如果发现不是'1' ， 直接return返回
        if (grid[row][col] != '1') {
            return;
        }
        grid[row][col] = '2';//将搜索完的岛屿标记为2，下次如果深度递归到这个格子，直接return返回
        //依次上下左右递归寻找'1'，并标记为'2',
        dfsGrid(grid, row - 1, col);
        dfsGrid(grid, row + 1, col);
        dfsGrid(grid, row, col - 1);
        dfsGrid(grid, row, col + 1);
    }
}
```

### 11.17 岛屿的最大面积

- 问题描述

  给你一个大小为 m x n 的二进制矩阵 grid 。

  岛屿 是由一些相邻的 1 (代表土地) 构成的组合，这里的「相邻」要求两个 1 必须在 水平或者竖直的四个方向上 相邻。你可以假设 grid 的四个边缘都被 0（代表水）包围着。岛屿的面积是岛上值为 1 的单元格的数目。计算并返回 grid 中最大的岛屿面积。如果没有岛屿，则返回面积为 0 。

  ![img](Datastructureandalgorithm.assets/maxarea1-grid.jpg)

```java
输入：grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
输出：6
解释：答案不应该是 11 ，因为岛屿只能包含水平或垂直这四个方向上的 1 。
```

- 代码

  ```java
  public class Solution {
  
      private int res = 0;//成员变量存储每一个节点对应的岛屿数量，在计算下一个节点的时候，记得归零
      public int maxAreaOfIsland(int[][] grid) {
          int result = 0 ;//存储最大的岛屿数量
          for (int i = 0; i < grid.length; i ++) {
              for (int j = 0; j < grid[0].length; j ++) {
                      res = 0;//计算每一个节点之前，需要归0
                  if (grid[i][j] == 1) {
                      dfsGrid(grid, i, j );
                      result = Math.max(result,res);
                  }
              }
          }
          return result;
      }
  
      private void dfsGrid(int[][] grid, int row, int col ) {
          if (row >= grid.length || col >= grid[0].length || row < 0 || col < 0) {
              return;
          }
  
          if (grid[row][col] != 1) {
              return;
          }
          res++;//如果发现grid[row][col] == 1 ， 表示当前为岛屿，岛屿数量加1
          grid[row][col] = 2;
          dfsGrid(grid, row - 1, col );
          dfsGrid(grid, row + 1, col );
          dfsGrid(grid, row, col - 1 );
          dfsGrid(grid, row, col + 1);
  
      }
      
  }
  ```

### 11.18 岛屿的周长

- 描述
  给定一个 `row x col` 的二维网格地图 grid ，其中：`grid[i][j] = 1` 表示陆地， `grid[i][j] = 0` 表示水域。网格中的格子 水平和垂直 方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。
  岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

![img](Datastructureandalgorithm.assets/island.png)

- 思路

  那么这些和我们岛屿的周长有什么关系呢？实际上，岛屿的周长是计算岛屿全部的「边缘」，而这些边缘就是我们在 DFS 遍历中，dfs 函数返回的位置。观察题目示例，我们可以将岛屿的周长中的边分为两类，如下图所示。黄色的边是与网格边界相邻的周长，而蓝色的边是与海洋格子相邻的周长。

  ![将岛屿周长中的边分为两类](Datastructureandalgorithm.assets/66d817362c1037ebe7705aacfbc6546e321c2b6a2e4fec96791f47604f546638.jpg)

  当我们的 dfs 函数因为「坐标 (r, c) 超出网格范围」返回的时候，实际上就经过了一条黄色的边；而当函数因为「当前格子是海洋格子」返回的时候，实际上就经过了一条蓝色的边。这样，我们就把岛屿的周长跟 DFS 遍历联系起来了，我们的题解代码也呼之欲出。

- 代码

  ```java
  class Solution {
     
      private int res = 0;
      public int islandPerimeter(int[][] grid) {
          res = 0;
          //这个for循环只需要找到其中一个岛，因为题目限制矩阵中只有一个岛屿
          for (int i = 0; i < grid.length; i ++) {
              for (int j = 0; j < grid[0].length; j ++) {
                  //如果要求岛屿的最大周长，就需要res=0,并且result = Math.max(result,res)存储岛屿周长的最大值
                  if (grid[i][j] == 1) {
                      dfsGrid(grid, i, j );
                     return res;//如果矩阵中有多个岛屿，就去掉这一行，去遍历整个矩阵
                      
                  }
              }
          }
          return res;
  
      }
  
       private void dfsGrid(int[][] grid, int row, int col ) {
          if (row >= grid.length || col >= grid[0].length || row < 0 || col < 0) {
              res++;//遇到边界，边长加一
              return;
          }
  
          if (grid[row][col] != 1) {
              if(grid[row][col] != 2) res++;//遇到水域，边长加一
              return;
          }
         
          grid[row][col] = 2;//已经遍历过的置为2
          dfsGrid(grid, row - 1, col );
          dfsGrid(grid, row + 1, col );
          dfsGrid(grid, row, col - 1 );
          dfsGrid(grid, row, col + 1);
  
      }
  
  }
  ```

### 11.19 最大人工岛

- 问题描述

  在二维地图上， 0 代表海洋，1代表陆地，我们最多只能将一格 0 （海洋）变成 1 （陆地）。进行填海之后，地图上最大的岛屿面积是多少？

- 思路

  大致的思路我们不难想到，我们先计算出所有岛屿的面积，在所有的格子上标记出岛屿的面积。然后搜索哪个海洋格子相邻的两个岛屿面积最大。例如下图中红色方框内的海洋格子，上边、左边都与岛屿相邻，我们可以计算出它变成陆地之后可以连接成的岛屿面积为 7+1+2=10

  ![一个海洋格子连接起两个岛屿](Datastructureandalgorithm.assets/3a993272977112d82a37676380bf723f3f6b919a20da322e9a5c5afda07fa397.jpg)

  然而，这种做法可能遇到一个问题。如下图中红色方框内的海洋格子，它的上边、左边都与岛屿相邻，这时候连接成的岛屿面积难道是 7+1+7？显然不是。这两个 7 来自同一个岛屿，所以填海造陆之后得到的岛屿面积应该只有 7+1 = 8。

![一个海洋格子与同一个岛屿有两个边相邻](Datastructureandalgorithm.assets/f519da076eb48fc993c7c71a0fa091b53bc6a1661163549eab60010606ee0e1c.jpg)

可以看到，要让算法正确，我们得能区分一个海洋格子相邻的两个 7 是不是来自同一个岛屿。那么，我们不能在方格中标记岛屿的面积，而应该标记岛屿的索引（下标），另外用一个数组记录每个岛屿的面积，如下图所示。这样我们就可以发现红色方框内的海洋格子，它的「两个」相邻的岛屿实际上是同一个。

![标记每个岛屿的索引（下标）](Datastructureandalgorithm.assets/56ec808215d4ff3014476ef22297522b3731602266f9a069a82daf41001f904c.jpg)

可以看到，这道题实际上是对网格做了两遍 DFS：第一遍 DFS 遍历陆地格子，计算每个岛屿的面积并标记岛屿；第二遍 DFS 遍历海洋格子，观察每个海洋格子相邻的陆地格子。

- 代码

```java
import java.util.HashMap;
import java.util.HashSet;

class Solution {
    public int largestIsland(int[][] grid) {
        if (grid==null || grid.length == 0){
            return 1;
        }

        int res = 0;
        int index = 2;//index表示岛屿的编号，0是海洋1是陆地，从2开始遍历
        HashMap<Integer,Integer> indexAndAreas = new HashMap<>();//岛屿编号：岛屿面积

        /**
         * 计算每个岛屿的面积，并标记是第几个岛屿
         */
        for (int r=0;r<grid.length;r++){
            for (int c=0;c<grid[0].length;c++){
                if (grid[r][c] == 1){//遍历没有访问过的岛屿格子
                    int area = area(grid,r,c,index);//返回每个岛屿的面积，dfs
                    indexAndAreas.put(index,area);//存入岛屿编号、岛屿面积
                    index++;//岛屿编号增加
                    res = Math.max(res,area);//记录最大的岛屿面积
                }
            }
        }

        if (res == 0) return 1;//res=0表示没有陆地，那么造一块，则返回1即可

        /**
         * 遍历海洋格子，假设这个格子填充，那么就把上下左右是陆地的格子所在的岛屿连接起来
         */
        for (int r=0;r<grid.length;r++){
            for (int c=0;c<grid[0].length;c++){
                if (grid[r][c] == 0){ //遍历海洋格子
                    HashSet<Integer> hashSet = findNeighbour(grid,r,c);//把上下左右邻居放入set去重
                    if (hashSet.size() < 1)continue;//如果海洋格子周围没有格子不必计算
                    int twoIsland = 1;//填充这个格子，初始为1，这个变量记录合并岛屿后的面积
                    for (Integer i: hashSet){
                        twoIsland += indexAndAreas.get(i);//该格子填充，则上下左右的陆地的都连接了，通过序号获得面积，加上面积
                    }
                    res = Math.max(res,twoIsland);//比较得到最大的面积
                }
            }
        }
        return res;
    }


    /**
     * 对于海洋格子，找到上下左右
     * 每个方向，都要确保有效inArea以及是陆地格子，则表示是该海洋格子的陆地邻居
     * @param grid
     * @param r
     * @param c
     * @return
     */
    private HashSet<Integer> findNeighbour(int[][] grid,int r,int c){
        HashSet<Integer> hashSet = new HashSet<>();
        if (inArea(grid,r-1,c)&&grid[r-1][c] != 0){
            hashSet.add(grid[r-1][c]);
        }
        if (inArea(grid,r+1,c) && grid[r+1][c] != 0){
            hashSet.add(grid[r+1][c]);
        }
        if (inArea(grid,r,c-1) && grid[r][c-1] != 0){
            hashSet.add(grid[r][c-1]);
        }
        if (inArea(grid,r,c+1) && grid[r][c+1] != 0){
            hashSet.add(grid[r][c+1]);
        }
        return hashSet;
    }

    /**
     * dfs方法，将格子填充为index，即表示这个格子属于哪个岛的
     * 计算岛屿面积，上下左右，当然这个可以优化的，因为不需要计算上面的，会有重复
     * @param grid
     * @param r
     * @param c
     * @param index
     * @return
     */
    private int area(int[][] grid, int r, int c,int index){
        if (!inArea(grid,r,c)){
            return 0;
        }
        //不为1，表示为海洋格子或者已经遍历过了
        if (grid[r][c] != 1){
            return 0;
        }
        grid[r][c] = index;//设置当前格子为某个岛屿编号
        return 1 + area(grid,r-1,c,index) + area(grid,r+1,c,index) + area(grid,r,c-1,index) + area(grid,r,c+1,index);
    }

    /**
     * 判断grid[r][c]是否大小合适
     * @param grid
     * @param r
     * @param c
     * @return
     */
    private boolean inArea(int[][] grid,int r,int c){
        return r>=0 && r<grid.length&&c>=0 && c<grid[0].length;
    }
}
```

### 11.20 括号生成

- 描述

  数字 `n` 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

  ```java
  输入：n = 3
  输出：["((()))","(()())","(())()","()(())","()()()"]
  ```

- 思路

  我们以 `n = 2` 为例，画树形结构图。方法是 「做减法」

  ![LeetCode 第 22 题：“括号生出”题解配图.png](Datastructureandalgorithm.assets/7ec04f84e936e95782aba26c4663c5fe7aaf94a2a80986a97d81574467b0c513-LeetCode 第 22 题：“括号生出”题解配图.png)

  画图以后，可以分析出的结论：

  - 当前左右括号都有大于 00 个可以使用的时候，才产生分支；
  - 产生左分支的时候，只看当前是否还有左括号可以使用；
  - 产生右分支的时候，还受到左分支的限制，右边剩余可以使用的括号数量一定得在严格大于左边剩余的数量的时候，才可以产生分支；
  - 在左边和右边剩余的括号数都等于 00 的时候结算。

- 代码

  ```java
  import java.util.ArrayList;
  import java.util.List;
  
  public class Solution {
  
      // 做减法
  
      public List<String> generateParenthesis(int n) {
          List<String> res = new ArrayList<>();
          // 特判
          if (n == 0) {
              return res;
          }
  
          // 执行深度优先遍历，搜索可能的结果
          dfs("", n, n, res);
          return res;
      }
  
      /**
       * @param curStr 当前递归得到的结果
       * @param left   左括号还有几个可以使用
       * @param right  右括号还有几个可以使用
       * @param res    结果集
       */
      private void dfs(String curStr, int left, int right, List<String> res) {
          // 因为每一次尝试，都使用新的字符串变量，所以无需回溯
          // 在递归终止的时候，直接把它添加到结果集即可，注意与「力扣」第 46 题、第 39 题区分
          if (left == 0 && right == 0) {
              res.add(curStr);
              return;
          }
          // 剪枝（如图，左括号可以使用的个数严格大于右括号可以使用的个数，才剪枝，注意这个细节）
          if (left > right) {
              return;
          }
  
          if (left > 0) {
              dfs(curStr + "(", left - 1, right, res);
          }
  
          if (right > 0) {
              dfs(curStr + ")", left, right - 1, res);
          }
      }
  }
  ```

### 11.21 矩阵中的最长递增路径

- 描述

  给定一个 m x n 整数矩阵 matrix ，找出其中 最长递增路径 的长度。对于每个单元格，你可以往上，下，左，右四个方向移动。 你 不能 在 对角线 方向上移动或移动到 边界外（即不允许环绕）。

  ![img](Datastructureandalgorithm.assets/grid1.jpg)

  ```java
  输入：matrix = [[9,9,4],[6,6,8],[2,1,1]]
  输出：4 
  解释：最长递增路径为 [1, 2, 6, 9]。
  ```

  ![img](Datastructureandalgorithm.assets/tmp-grid.jpg)

  ```java
  输入：matrix = [[3,4,5],[3,2,6],[2,2,1]]
  输出：4 
  解释：最长递增路径是 [3, 4, 5, 6]。注意不允许在对角线方向上移动。
  ```

  

- 思路（记忆化思路）

  记忆化的思想明确了，回到本题上来看看怎么应用这个思想。首先明确我们记忆化矩阵每一点存的值意味着什么。从深搜的角度入手，我们从i，j这个点出发，返回值为int意味着我们得到从该点出发能够经过的最长递增路径的值。举个一维数组的例子，现在是[1, 2, 3, 4]，我们从3这个点出发，找递增路径，然后求得从3出发的最大递增路径长度为2，现在从2出发，我们会深搜进3，再从3出发，到4，最后回到最开始的层，我们计算出的结果是3。这里就可以利用记忆化去减少时间，当我们从2出发时，到位置3，既然第一遍我们已经算过从3出发的路径长度，那么我们可以直接返回从3出发的路径长度，这样相当于直接是 1 + 从3出发的路径长度 = 3，现在将从2出发的路径长度记录下来存入memo[2]中，我们再从1出发，当1碰到2时，我们看看memo，发现从2出发的长度我们已经计算过了，那么我们不必要再去从2深搜，直接返回memo[2]的值即可。这便是记忆化的应用。

  回到这个题上来，我们是不是也可以类比上面一维数组的例子来进行记忆化呢？
  我们建立一个memo[][]二维数组，其中`memo[i][j]`意味着，从(i, j)这个点出发最长的递增路径长度。因为`memo[i][j]`最小为1，意味着此时这个点上下左右都没法走，它是上下左右最大的，那么最长也就是1了，这就是为什么代码中我每进入一层首先要给我的`memo[i][j]++`(我初始化将其全部为0了)。现在又有这样一个问题，每当你达到(i, j)这个位置的时候，你都要计算上下左右四个方向，你需要选四个方向中最长的路径长度将其记录进`memo[i][j]`，因此我在每个if里都进行了`max(memo[i][j], dfs(...) + 1)`进行比较，比如我先计算了上方存入memo，再计算左边，发现左边小于上面的memo，因此此时还保留上方的memo的值。当你读到这里时，你应该对记忆化有了一个基本的认知，并且明白这道题该怎么利用记忆化去做了。

- 代码

  ```java
  class Solution {
      int m, n;
      int[][] matrix, memo;   
      public int longestIncreasingPath(int[][] _matrix) {
          /*
          方法2:记忆化搜索
          利用dfs将深度优先搜索过程中得到matrix[i][j]的最长路径长度存储到memo[i][j]中
          然后如果memo[i][j]没有计算才需要dfs,否则说明已经计算过了就不用进一步计算
          */
          matrix = _matrix;
          m = matrix.length;
          n = matrix[0].length;
          // 存储matrix的最长递增路经
          int res = 1;
          // 记忆载体
          memo = new int[m][n];        
          // 遍历每个节点
          for(int i = 0; i < m; i++) {
              for(int j = 0; j < n; j++) {
                  // 若没有搜索过才需要进行搜索
                  if(memo[i][j] == 0) {
                      res = Math.max(res, dfs(i, j));   
                  }
                  // 这里为什么没有比较memo[i][j]!=0的情况?
                  // 因为后面matrix[nextI][nextJ]为起点的路径总比matrix[i][j]为起点的短
                  // 满足matrix[nextI][nextJ]>matrix[i][j]才会进行dfs的
              }
          }
          return res;
      }
      /*
      返回以matrix[i][j]为起点的最长递增路径
      */
      private int dfs(int i, int j) {
          // 若之前搜索过了直接返回之前存储的最大长度
          if(memo[i][j] != 0) {
              return memo[i][j];
          }
          int[][] dirs = new int[][]{{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
          // 以matrix[i][j]为起点的最长递增路径
          int maxLen = 1;
          for(int[] dir : dirs) {
              int nextI = i + dir[0];
              int nextJ = j + dir[1];
              if(nextI >= 0 && nextI < m && nextJ >= 0 && nextJ < n 
              && matrix[nextI][nextJ] > matrix[i][j]) {
                  // 选择4个方向的最大路径的最大值作为maxLen
                  maxLen = Math.max(maxLen, dfs(nextI, nextJ) + 1);
              }
          }
          // 将以matrix[i][j]为起点的最长递增路径存储在memo[i][j]中
          // 注意:在递归过程中将matrix[nextI,nextJ]为起点的最长路径都存储在memo了
          memo[i][j] = maxLen;
          // 返回该最长路径长度
          return maxLen;
      }
  }
  ```

### 11.21 矩阵中的最长递增路径

- 描述

  给定一个 m x n 整数矩阵 matrix ，找出其中 最长递增路径 的长度。对于每个单元格，你可以往上，下，左，右四个方向移动。 你 不能 在 对角线 方向上移动或移动到 边界外（即不允许环绕）。

  ![img](Datastructureandalgorithm.assets/grid1.jpg)

  ```java
  输入：matrix = [[9,9,4],[6,6,8],[2,1,1]]
  输出：4 
  解释：最长递增路径为 [1, 2, 6, 9]。
  ```

  ![img](Datastructureandalgorithm.assets/tmp-grid.jpg)

  ```java
  输入：matrix = [[3,4,5],[3,2,6],[2,2,1]]
  输出：4 
  解释：最长递增路径是 [3, 4, 5, 6]。注意不允许在对角线方向上移动。
  ```

  

- 思路（记忆化思路）

  记忆化的思想明确了，回到本题上来看看怎么应用这个思想。首先明确我们记忆化矩阵每一点存的值意味着什么。从深搜的角度入手，我们从i，j这个点出发，返回值为int意味着我们得到从该点出发能够经过的最长递增路径的值。举个一维数组的例子，现在是[1, 2, 3, 4]，我们从3这个点出发，找递增路径，然后求得从3出发的最大递增路径长度为2，现在从2出发，我们会深搜进3，再从3出发，到4，最后回到最开始的层，我们计算出的结果是3。这里就可以利用记忆化去减少时间，当我们从2出发时，到位置3，既然第一遍我们已经算过从3出发的路径长度，那么我们可以直接返回从3出发的路径长度，这样相当于直接是 1 + 从3出发的路径长度 = 3，现在将从2出发的路径长度记录下来存入memo[2]中，我们再从1出发，当1碰到2时，我们看看memo，发现从2出发的长度我们已经计算过了，那么我们不必要再去从2深搜，直接返回memo[2]的值即可。这便是记忆化的应用。

  回到这个题上来，我们是不是也可以类比上面一维数组的例子来进行记忆化呢？
  我们建立一个memo[][]二维数组，其中`memo[i][j]`意味着，从(i, j)这个点出发最长的递增路径长度。因为`memo[i][j]`最小为1，意味着此时这个点上下左右都没法走，它是上下左右最大的，那么最长也就是1了，这就是为什么代码中我每进入一层首先要给我的`memo[i][j]++`(我初始化将其全部为0了)。现在又有这样一个问题，每当你达到(i, j)这个位置的时候，你都要计算上下左右四个方向，你需要选四个方向中最长的路径长度将其记录进`memo[i][j]`，因此我在每个if里都进行了`max(memo[i][j], dfs(...) + 1)`进行比较，比如我先计算了上方存入memo，再计算左边，发现左边小于上面的memo，因此此时还保留上方的memo的值。当你读到这里时，你应该对记忆化有了一个基本的认知，并且明白这道题该怎么利用记忆化去做了。

- 代码

  ```java
  class Solution {
      int m, n;
      int[][] matrix, memo;   
      public int longestIncreasingPath(int[][] _matrix) {
          /*
          方法2:记忆化搜索
          利用dfs将深度优先搜索过程中得到matrix[i][j]的最长路径长度存储到memo[i][j]中
          然后如果memo[i][j]没有计算才需要dfs,否则说明已经计算过了就不用进一步计算
          */
          matrix = _matrix;
          m = matrix.length;
          n = matrix[0].length;
          // 存储matrix的最长递增路经
          int res = 1;
          // 记忆载体
          memo = new int[m][n];        
          // 遍历每个节点
          for(int i = 0; i < m; i++) {
              for(int j = 0; j < n; j++) {
                  // 若没有搜索过才需要进行搜索
                  if(memo[i][j] == 0) {
                      res = Math.max(res, dfs(i, j));   
                  }
                  // 这里为什么没有比较memo[i][j]!=0的情况?
                  // 因为后面matrix[nextI][nextJ]为起点的路径总比matrix[i][j]为起点的短
                  // 满足matrix[nextI][nextJ]>matrix[i][j]才会进行dfs的
              }
          }
          return res;
      }
      /*
      返回以matrix[i][j]为起点的最长递增路径
      */
      private int dfs(int i, int j) {
          // 若之前搜索过了直接返回之前存储的最大长度
          if(memo[i][j] != 0) {
              return memo[i][j];
          }
          int[][] dirs = new int[][]{{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
          // 以matrix[i][j]为起点的最长递增路径
          int maxLen = 1;
          for(int[] dir : dirs) {
              int nextI = i + dir[0];
              int nextJ = j + dir[1];
              if(nextI >= 0 && nextI < m && nextJ >= 0 && nextJ < n 
              && matrix[nextI][nextJ] > matrix[i][j]) {
                  // 选择4个方向的最大路径的最大值作为maxLen
                  maxLen = Math.max(maxLen, dfs(nextI, nextJ) + 1);
              }
          }
          // 将以matrix[i][j]为起点的最长递增路径存储在memo[i][j]中
          // 注意:在递归过程中将matrix[nextI,nextJ]为起点的最长路径都存储在memo了
          memo[i][j] = maxLen;
          // 返回该最长路径长度
          return maxLen;
      }
  }
  ```


## 12.双指针

### 12.1 盛最多水的容器

- 描述

  给定一个长度为n的整数数组height，有n条垂线，第i条线的两个端点是（i,0）和（i,height[i]）。找出其中的两条线，使得它们与x轴共同构成的容器可以容纳最多的水。

  ![img](Datastructureandalgorithm.assets/question_11.jpg)

```java
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

- 思路（双指针）

  设两指针 i , j ，指向的水槽板高度分别为 h[i] , h[j] ，此状态下水槽面积为 S(i,j) 。由于可容纳水的高度由两板中的短板决定，因此可得如下面积公式 ：

![Picture0.png](Datastructureandalgorithm.assets/1628780627-VtSmcP-Picture0.png)

在每个状态下，无论长板或短板向中间收窄一格，都会导致水槽 底边宽度 -1−1 变短：

- 若向内 移动短板 ，水槽的短板 min(h[i], h[j])min(h[i],h[j]) 可能变大，因此下个水槽的面积 可能增大 。

- 若向内 移动长板 ，水槽的短板 min(h[i], h[j])min(h[i],h[j]) 不变或变小，因此下个水槽的面积 一定变小 。因此，初始化双指针分列水槽左右两端，循环每轮将**短板向内移动一格**，并更新面积最大值，直到两指针相遇时跳出；即可获得最大面积。

- 代码

  ```java
  class Solution {
      public int maxArea(int[] height) {
          int i = 0, j = height.length - 1, res = 0;
          while(i < j) {
              res = height[i] < height[j] ? 
                  Math.max(res, (j - i) * height[i++]): 
                  Math.max(res, (j - i) * height[j--]); 
          }
          return res;
      }
  }
  ```

### 12.2 合并两个有序的数组

- 描述

  给出一个有序的整数数组 A 和有序的整数数组 B ，请将数组 B 合并到数组 A 中，变成一个有序的升序数组数据范围：1000≤*n*,*m*≤100，|A_i| <=100， |B_i| <= 100

  - 注意：
    保证 A 数组有足够的空间存放 B 数组的元素， A 和 B 中初始的元素数目分别为 m 和 n，A的数组空间大小为 m+n

    不要返回合并的数组，将数组 B 的数据合并到 A 里面就好了，且后台会自动将合并后的数组 A 的内容打印出来，所以也不需要自己打印

    A 数组在[0,m-1]的范围也是有序的

  ```java
  输入：[4,5,6],[1,2,3]
  返回值：[1,2,3,4,5,6]
  说明：
  A数组为[4,5,6]，B数组为[1,2,3]，后台程序会预先将A扩容为[4,5,6,0,0,0]，B还是为[1,2,3]，m=3，n=3，传入到函数merge里面，然后请同学完成merge函数，将B的数据合并A里面，最后后台程序输出A数组    
  ```

  

- 思路

  ![alt](Datastructureandalgorithm.assets/262712F1AAAB9043384442160A7FA6E8.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public void merge(int A[], int m, int B[], int n) {
          //指向数组A的结尾
          int i = m - 1; 
          //指向数组B的结尾
          int j = n - 1; 
          //指向数组A空间的结尾处
          int k = m + n - 1; 
          //从两个数组最大的元素开始，直到某一个数组遍历完
          while(i >= 0 && j >= 0){ 
              //将较大的元素放到最后
              if(A[i] > B[j]) 
                  A[k--] = A[i--];
              else
                  A[k--] = B[j--];
          }
          //数组A遍历完了，数组B还有，则还需要添加到数组A前面
          if(i < 0){ 
              while(j >= 0)
                  A[k--] = B[j--];
          } 
          //数组B遍历完了，数组A前面正好有，不用再添加
      }
  }
  
  ```

### 12.3 合并区间

- 描述

  给出一组区间，请合并所有重叠的区间。

  请保证合并后的区间按区间起点升序排列。

  数据范围：区间组数 0≤*n*≤2×10^5^，区间内的值都满足0≤val≤2×10^5^

  要求：空间复杂度 O*(*n*)，时间复杂度 O(nlogn)

  进阶：空间复杂度 O(val)，时间复杂度O(val)

  ```java
  输入：[[10,30],[20,60],[80,100],[150,180]]
  返回值：[[10,60],[80,100],[150,180]]
  ```

- 思路

  - 对左边界排序，

  - 如果下一个区间的左边界在前一个的有边界内，考虑是否要更新边界，

  - 如果下一个区间的左边界在前一个的有边界外，说明区间无法合并，开始计算下一个区间

- 代码

  ```java
      public ArrayList<Interval> merge(ArrayList<Interval> intervals) {
          ArrayList<Interval> res = new ArrayList<>();
          Collections.sort(intervals,(a,b)->a.start-b.start);
          int len = intervals.size();
          int i = 0;
          while (i < len) {
              //初始化小区间
              int left = intervals.get(i).start;
              int right = intervals.get(i).end;
              //不断找到，后面区间的start位置与当前区间交叉，考虑更新最大end
              while (i < len-1 && intervals.get(i+1).start <= right) {
                  right = Math.max(right,intervals.get(i+1).end);
                  i++;
              }
              //更新完后,加入res，继续循环找到下一个区间
              res.add(new Interval(left,right));
              i++;
          }
          return res;
      }
  ```

### 12.4 判断回文字符串

- 描述

  给定一个长度为 n 的字符串，请编写一个函数判断该字符串是否回文。如果是回文请返回true，否则返回false。字符串回文指该字符串正序与其逆序逐字符一致。

  数据范围：0<*n*≤1000000

  要求：空间复杂度 O(1)，时间复杂度 O*(*n)

- 代码

  ```java
  public boolean judge(String str) {
      if (str.length() == 0)
          return true;
      //两个指针，一个从左边开始，一个从右边开始，每次两个
      //指针都同时往中间挪，只要两个指针指向的字符不一样就返回false
      int left = 0;
      int right = str.length() - 1;
      while (left < right) {
          if (str.charAt(left++) != str.charAt(right--))
              return false;
      }
      return true;
  }
  ```

### 12.5 反转字符串

- 描述

  写出一个程序，接受一个字符串，然后输出该字符串反转后的字符串。（字符串长度不超过1000）

  数据范围： 0≤*n*≤1000

  要求：空间复杂度 O(n)，时间复杂度 O(n)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public String solve (String str) {
          //左右双指针
          char[] s = str.toCharArray();
          int left = 0;
          int right = str.length() - 1;
          //两指针往中间靠
          while(left < right){  
              char c = s[left];
              //交换位置
              s[left] = s[right];
              s[right] = c;
              left++;
              right--;
          }
          return new String(s);
      }
  }
  
  ```

### 12.6 最长无重复子数组

- 描述

  给定一个长度为n的数组arr，返回arr的最长**无重复元素子数组**的长度，无重复指的是所有数字都不相同，子数组是连续的，比如[1,3,5,7,9]的子数组有[1,3],[3,5,7]等等，但是[1,3,7]不是子数组

  数据范围：0≤arr.length≤10^5^，0<arr[i]≤10^5^

  ```java
  输入：[2,3,4,5]
  返回值：4
  说明：[2,3,4,5]是最长子数组     
  输入：[2,2,3,4,3]
  返回值：3
  说明：[2,3,4]是最长子数组     
  ```

- 思路

  我们使用两个指针，一个i一个j，最开始的时候i和j指向第一个元素，然后i往后移，把扫描过的元素都放到map中，如果i扫描过的元素没有重复的就一直往后移，顺便记录一下最大值`max`，如果i扫描过的元素有重复的，就改变j的位置

- 代码

  ```java
  import java.util.*;
  public class Solution {
          public int maxLength(int[] arr) {
          if (arr.length == 0)
              return 0;
          HashMap<Integer, Integer> map = new HashMap<>();
          int max = 0;
          for (int i = 0, j = 0; i < arr.length; ++i) {
              if (map.containsKey(arr[i])) {
                   //因为有可能遇到的重复数字的位置 比j还要前
                   //所以不能把j置于该位置前一位， 而是比较哪个最大{3,3,2,1,3,3,3,1}
                   //j只能往右边滑动，不能回左边
                   //比如最后一个1，map.get(arr[i]) + 1 = 3（这里是找到了j=7左边的1的下标再加一）
                  j = Math.max(j, map.get(arr[i]) + 1);
              }
              map.put(arr[i], i);
              max = Math.max(max, i - j + 1);
          }
          return max;
      }
  }
  ```

### 12.7 接雨水问题

- 描述

  给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

  ![img](Datastructureandalgorithm.assets/rainwatertrap.png)

**提示：**

`n == height.length`

``1 <= n <= 2 * 104`

`0 <= height[i] <= 105`

- 思路1(单调栈)

  - 使用单调栈，【单调栈入门】

  - 单调递减栈

    理解题目，参考图解，注意题目的性质，当后面的柱子高度比前面的低时，是无法接雨水的
    当找到一根比前面高的柱子，就可以计算接到的雨水
    所以使用单调递减栈

  - 对更低的柱子入栈

    更低的柱子以为这后面如果能找到高柱子，这里就能接到雨水，所以入栈把它保存起来
    平地相当于高度 0 的柱子，没有什么特别影响

  - 当出现高于栈顶的柱子时

    说明可以对前面的柱子结算了

    计算已经到手的雨水，然后出栈前面更低的柱子

  - 计算雨水的时候需要注意的是

    雨水区域的右边 r 指的自然是当前索引 i
    底部是栈顶 st.top() ，因为遇到了更高的右边，所以它即将出栈，使用 cur 来记录它，并让它出栈
    左边 l 就是新的栈顶 st.top()
    雨水的区域全部确定了，水坑的高度就是左右两边更低的一边减去底部，宽度是在左右中间
    使用乘法即可计算面积

  ![GIF 2022-6-25 14-57-12](Datastructureandalgorithm.assets/GIF 2022-6-25 14-57-12.gif)

- 代码

  ```java
  class Solution {
      public int trap(int[] walls) {
          if (walls == null || walls.length <= 2) {
              return 0;
          }
          // 思路：
          // 单调不增栈，walls元素作为右墙依次入栈
          // 出现入栈元素（右墙）比栈顶大时，说明在右墙左侧形成了低洼处，低洼处出栈并结算该低洼处能接的雨水
          int water = 0;
          Stack<Integer> stack = new Stack<>();
          for (int right=0; right<walls.length; right++) {
              // 栈不为空，且当前元素（右墙）比栈顶（右墙的左侧）大：说明形成低洼处了
              while (!stack.isEmpty() && walls[right]>walls[stack.peek()]) {
                  // 低洼处弹出，尝试结算此低洼处能积攒的雨水
                  int bottom = stack.pop();
                  // 看看栈里还有没有东西（左墙是否存在）
                  // 有右墙+有低洼+没有左墙=白搭
                  if (stack.isEmpty()) {
                      break;
                  }
                  // 左墙位置以及左墙、右墙、低洼处的高度
                  int left = stack.peek();
                  int leftHeight = walls[left];
                  int rightHeight = walls[right];
                  int bottomHeight = walls[bottom];
  
                  // 能积攒的水=(右墙位置-左墙位置-1) * (min(右墙高度, 左墙高度)-低洼处高度)
                  water += (right-left-1) * (Math.min(leftHeight, rightHeight)-bottomHeight);
              }
  
              // 上面的pop循环结束后再push，保证stack是单调不增
              stack.push(right);
          }
  
          return water;
      }
  }
  ```

- 思路（双指针）（另外的条件限制是数组中的值都是大于0的，也就是底部最小高度是1）

  具体做法：

  - step 1：检查数组是否为空的特殊情况
  - step 2：准备双指针，分别指向数组首尾元素，代表最初的两个边界
  - step 3：指针往中间遍历，遇到更低柱子就是底，用较短的边界减去底就是这一列的接水量，遇到更高的柱子就是新的边界，更新边界大小。

  ![alt](Datastructureandalgorithm.assets/1E66C1358EA2CEEA33028656F0568955.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public long maxWater (int[] arr) {
          //排除空数组
          if(arr.length == 0) 
              return 0;
          long res = 0;
          //左右双指针
          int left = 0; 
          int right = arr.length - 1; 
          //中间区域的边界高度
          int maxL = 0; 
          int maxR = 0;
          //直到左右指针相遇
          while(left < right){ 
              //每次维护往中间的最大边界
              maxL = Math.max(maxL, arr[left]); 
              maxR = Math.max(maxR, arr[right]);
              //较短的边界确定该格子的水量
              if(maxR > maxL) 
                  res += maxL - arr[left++]; 
              else
                  res += maxR - arr[right--];
          }
          return res;
      }
  }
  
  ```


### 12.8 比较版本号

- 描述

  牛客项目发布项目版本时会有版本号，比如1.02.11，2.14.4等等，现在给你2个版本号version1和version2，请你比较他们的大小，版本号是由修订号组成，修订号与修订号之间由一个"."连接。1个修订号可能有多位数字组成，修订号可能包含前导0，且是合法的。例如，1.02.11，0.1，0.2都是合法的版本号，每个版本号至少包含1个修订号。修订号从左到右编号，下标从0开始，最左边的修订号下标为0，下一个修订号下标为1，以此类推。

  比较规则：

  - 一. 比较版本号时，请按从左到右的顺序依次比较它们的修订号。比较修订号时，只需比较忽略任何前导零后的整数值。比如"0.1"和"0.01"的版本号是相等的
  - 二. 如果版本号没有指定某个下标处的修订号，则该修订号视为0。例如，"1.1"的版本号小于"1.1.1"。因为"1.1"的版本号相当于"1.1.0"，第3位修订号的下标为0，小于1
  - 三. version1 > version2 返回1，如果 version1 < version2 返回-1，不然返回0.

  数据范围：

  - 1 <= version1.length, version2.length <= 1000
  - version1 和 version2 的修订号不会超过int的表达范围，即不超过 **32 位整数** 的范围

- 思路（双指针遍历截取）

  - step 1：利用两个指针表示字符串的下标，分别遍历两个字符串。

  - step 2：每次截取点之前的数字字符组成数字，即在遇到一个点之前，直接取数字，加在前面数字乘10的后面。（因为int会溢出，这里采用long记录数字）

  - step 3：然后比较两个数字大小，根据大小关系返回1或者-1，如果全部比较完都无法比较出大小关系，则返回0.

    ![alt](Datastructureandalgorithm.assets/34EC0DBACF8E56532AF5EE41BC84C258.gif)

- 代码

  ```java
  import java.util.*;
  public class Solution {
      public int compare (String version1, String version2) {
          int n1 = version1.length();
          int n2 = version2.length();
          int i = 0, j = 0;
          //直到两个字符串全部结束
          while(i < n1 || j < n2){
              long num1 = 0;
              //从下一个点前截取数字
              while(i < n1 && version1.charAt(i) != '.'){ 
                  num1 = num1 * 10 + (version1.charAt(i) - '0');
                  i++;
              }
              //跳过点
              i++; 
              long num2 = 0;
              //从下一个点前截取数字
              while(j < n2 && version2.charAt(j) != '.'){ 
                  num2 = num2 * 10 + (version2.charAt(j) - '0');
                  j++;
              }
              //跳过点
              j++; 
              //比较数字大小
              if(num1 > num2) 
                  return 1;
              if(num1 < num2)
                  return -1;
          }
          //版本号相同
          return 0; 
      }
  }
  
  ```


## 13.字符串

### 13.1 字符串变形

- 描述

  对于一个长度为n的字符串，我们需要对它做一些变形。首先这个字符串中包含着一些空格，就像“Hello world”一样，然后我们要做的就是把这个字符串中由空格隔开的单词反序，同时反转每个字符的大小写。

  比如“Hello World”变形后就变成了“wORLD hELLO”

  数据范围：1≤n≤10^6^,字符串中包含大写英文字母、小写英文字母、空格

  空间复杂度O(n),时间复杂度O(n)

- 思路

  使用split进行字符串切分的时候需要注意

  - 空格分隔成字符串
  - 对字符串数组反转大小写
  - StringBuilder对字符串数组反向拼接，并且加上空格，最后stringBuilder.toString()，返回字符串结果

- 代码

  ```java
  import java.util.*;
  
  public class Solution {
      
      // 反转字符串大小写
      public String reverse(String str){
          StringBuilder stringBuilder = new StringBuilder();
          for(int i = 0; i < str.length(); i++){
              if(Character.isUpperCase(str.charAt(i))){
                  stringBuilder.append(Character.toLowerCase(str.charAt(i)));
              }else{
                  stringBuilder.append(Character.toUpperCase(str.charAt(i)));
              }
          }
          return stringBuilder.toString();
      }
      
      public String trans(String s, int n) {
          // write code here
          String[] tmp = s.split(" ", -1);// 这里，limit设置为-1，模式可以应用无数次
          StringBuilder stringBuilder = new StringBuilder();
          for(int i = tmp.length - 1; i >= 0; i--){
              stringBuilder.append(reverse(tmp[i]));
              if(i != 0){
                  stringBuilder.append(" ");
              }
          }
          return stringBuilder.toString();
      }
  }
  ```

### 13.2 最长公共前缀

- 描述

  给你一个大小为 n 的字符串数组 strs ，其中包含n个字符串 , 编写一个函数来查找字符串数组中的最长公共前缀，返回这个公共前缀。

  数据范围： 0≤*n*≤5000，0≤len(strs~i~)≤5000

  进阶：空间复杂度 O(n)，时间复杂度 O(n)

  ```java
  输入：["abca","abc","abca","abc","abcc"]
  返回值："abc"
  ```

- 思路

  - 将字符串数组看作一个二维空间，每一次从第一列开始。

  - 确定所有字符子串中第一列字符。

  - 逐层扫描后面每一列，遇到不同字符停止扫描。

  - 图解：

    ![图片说明](Datastructureandalgorithm.assets/3E866D7DC0F594B37D675D8164116AB5.png)

  

- 代码

  ```java
  import java.util.*;
  
  
  public class Solution {
      /**
       * 
       * @param strs string字符串一维数组 
       * @return string字符串
       */
      public String longestCommonPrefix (String[] strs) {
          // //纵向扫描
          if(strs.length==0 || strs==null){
              return "";
          }
  
          int rows = strs.length;
          int cols = strs[0].length();
          //开始扫描
          for(int i=0;i<cols;i++){
              char firstChar = strs[0].charAt(i);
              for(int j=1;j<rows;j++){
                  if(strs[j].length()==i || strs[j].charAt(i)!=firstChar){
                      return strs[0].substring(0,i);
                  }
              }
          }
          return strs[0];
      }
  }
  ```

### 13.3 验证IP地址

- 描述

  编写一个函数来验证输入的字符串是否是有效的 IPv4 或 IPv6 地址

  IPv4 地址由十进制数和点来表示，每个地址包含4个十进制数，其范围为 0 - 255， 用(".")分割。比如，172.16.254.1；
  同时，IPv4 地址内的数不会以 0 开头。比如，地址 172.16.254.01 是不合法的。

  IPv6 地址由8组16进制的数字来表示，每组表示 16 比特。这些组数字通过 (":")分割。比如, 2001:0db8:85a3:0000:0000:8a2e:0370:7334 是一个有效的地址。而且，我们可以加入一些以 0 开头的数字，字母可以使用大写，也可以是小写。所以， 2001:db8:85a3:0:0:8A2E:0370:7334 也是一个有效的 IPv6 address地址 (即，忽略 0 开头，忽略大小写)。

  然而，我们不能因为某个组的值为 0，而使用一个空的组，以至于出现 (::) 的情况。 比如， 2001:0db8:85a3::8A2E:0370:7334 是无效的 IPv6 地址。
  同时，在 IPv6 地址中，多余的 0 也是不被允许的。比如， 02001:0db8:85a3:0000:0000:8a2e:0370:7334 是无效的。

  说明: 你可以认为给定的字符串里没有空格或者其他特殊字符。

  数据范围：字符串长度满足5≤*n*≤50

  进阶：空间复杂度 O(n)，时间复杂度 O(n)

  ```java
  输入："172.16.254.1"
  返回值："IPv4"
  说明：这是一个有效的 IPv4 地址, 所以返回 "IPv4"  
  
  输入："172.16.254.1"
  返回值："IPv4"
  说明：这是一个有效的 IPv4 地址, 所以返回 "IPv4"  
  
  输入："256.256.256.256"
  返回值："Neither"
  说明：这个地址既不是 IPv4 也不是 IPv6 地址   
  ```

- 思路

  - 1.分别验证IPv4和IPv6
  - 2.注意事项
    - 2.1 分割字符串时，使用limit = -1的split函数，使得字符串末尾或开头有一个'.'或':'也能分割出空的字符串
    - 2.2 使用Integer.parseInt()函数检查异常

- 代码1

  ```java
      public String validIPAddress(String queryIP) {
          if (queryIP.indexOf('.') >= 0) {
              return isIpV4(queryIP) ? "IPv4" : "Neither";
          } else {
              return isIpV6(queryIP) ? "IPv6" : "Neither";
          }
      }
  
      public boolean isIpV4(String queryIP) {
          //加-1是防止出现空字符串无法计数 比如192.168.1.1. 后边多了一个点，不加-1会被忽略后边的空串
          String[] split = queryIP.split("\\.",-1);
          //个数不是4个
          if (split.length != 4) {
              return false;
          }
          for (String s : split) {
              //每个长度不在 1-3之间
              if (s.length() > 3 || s.length() == 0) {
                  return false;
              }
              //有前导0 并且长度不为1
              if (s.charAt(0) == '0' && s.length() != 1) {
                  return false;
              }
              //计算数字
              int ans = 0;
              for (int j = 0; j < s.length(); j++) {
                  char c = s.charAt(j);
                  //不是数字
                  if (!Character.isDigit(c)) {
                      return false;
                  }
                  ans = ans * 10 + (c - '0');
              }
              //数字超过255
              if (ans > 255) {
                  return false;
              }
          }
          return true;
      }
  
      public boolean isIpV6(String queryIP) {
          String[] split = queryIP.split(":",-1);
          //数量不是8个
          if (split.length != 8) {
              return false;
          }
          for (String s : split) {
              //每个串 长度不在1-4之间
              if (s.length() > 4 || s.length() == 0) {
                  return false;
              }
              for (int i = 0; i < s.length(); i++) {
                  char c = s.charAt(i);
                  //不是数字并且字母不在 a-f之间
                  if (!Character.isDigit(c) && !(Character.toLowerCase(c) >= 'a') || !(Character.toLowerCase(c) <= 'f')) {
                      return false;
                  }
              }
          }
          return true;
      }
  ```

- 代码2(优雅)

  ```java
  public String validIPAddress(String IP) {
      return validIPv4(IP) ? "IPv4" : (validIPv6(IP) ? "IPv6" : "Neither");
  }
  
  private boolean validIPv4(String IP) {
      String[] strs = IP.split("\\.", -1);
      if (strs.length != 4) {
          return false;
      }
  
      for (String str : strs) {
          if (str.length() > 1 && str.startsWith("0")) {
              return false;
          }
          try {
              int val = Integer.parseInt(str);
              if (!(val >= 0 && val <= 255)) {
                  return false;
              }
          } catch (NumberFormatException numberFormatException) {
              return false;
          }
      }
      return true;
  }
  
  private boolean validIPv6(String IP) {
      String[] strs = IP.split(":", -1);
      if (strs.length != 8) {
          return false;
      }
  
      for (String str : strs) {
          if (str.length() > 4 || str.length() == 0) {
              return false;
          }
          try {
              int val = Integer.parseInt(str, 16);
          } catch (NumberFormatException numberFormatException) {
              return false;
          }
      }
      return true;
  }
  ```

### 13.4 大数加法

- 描述

  以字符串的形式读入两个数字，编写一个函数计算它们的和，以字符串的形式返回。

  数据范围：s.length,t.length ≤100000，字符串仅由0-9构成

  时间复杂度：O(n)

- 思路

  - 两个字符串末尾依次转为Integer数据相加，设置进位项top，结果大于10，将个位数入栈，top置1
  - 依次加到末尾，对未加完的字符串，继续入栈操作，同时注意对进位项top的处理

- 代码（自己的）

  ```java
  import java.util.*;
  public class Solution {
      public String solve (String s, String t) {
          Stack<Integer> temp = new Stack();
          int i = s.length() - 1;
          int j =  t.length() - 1;
          int top = 0;
          int add = 0;
          while(i>=0&&j>=0){
               add = s.charAt(i) - '0' + t.charAt(j) - '0' + top;
              if(add<10){
                  temp.push(add);
                  top = 0;
              }else{
                  temp.push(add-10);
                  top = 1;
              }
              i--;
              j--;
              
          }
          
          if(i<0&&j>=0){
              while(j>=0){
                   add = t.charAt(j) - '0' + top;
                  if(add<10){
                  temp.push(add);
                  top = 0;
              }else{
                  temp.push(add-10);
                  top = 1;
              }
                  j--;
              }
          }else if(j<0&&i>=0){
              while(i>=0){
                   add = s.charAt(i) - '0' + top;
                  if(add<10){
                  temp.push(add);
                  top = 0;
              }else{
                  temp.push(add-10);
                  top = 1;
              }
                  i--;
              }
          }
          if(top==1){
              temp.push(top);
          }
          StringBuilder s1 = new StringBuilder();
          while(!temp.empty()){
              s1.append(temp.pop());
          }
          return s1.toString();
      }
  }
  ```


## 14.模拟

### 14.1 旋转数组

- 描述

  一个数组A中存有n个整数，在不允许使用另外数组的前提下，将每个整数循环向右移M≥0个位置，如果需要考虑程序移动数据的次数尽量少，要如何设计移动的方法？

  数据范围：0<n≤100,0≤m≤1000

  空间复杂度O(1),时间复杂度O(n)

- 思路

  该方法基于如下的事实：将数组的元素向右移动 k 次后，尾部 m mod n 个元素会移动至数组头部，其余元素向后移动 m mod n 个位置。
  该方法为数组的翻转：翻转算法参考 反转链表中的双指针方法 https://blog.nowcoder.net/n/d259b250747b4085bc7975f102d248c4

  1、可以先将所有元素翻转，这样尾部的 m mod n 个元素就被移至数组头部，

  2、然后再翻转 [0,m mod n−1] 区间的元素

  3、 最后翻转[m mod n,n−1] 区间的元素即能得到最后的答案。

  **实例：**
  以 n=7，m=3 为例进行如下展示：

  | 操作                            | 结果                    |
  | ------------------------------- | ----------------------- |
  | 原始数据                        | 【1，2，3，4，5，6，7】 |
  | 翻转所有元素                    | 【7，6，5，4，3，2，1】 |
  | 翻转 [0,m mod n −1] 区间的元素  | 【5，6，7，4，3，2，1】 |
  | 翻转 [m mod n, n −1] 区间的元素 | 【5，6，7，1，2，3，4】 |

  ![alt](Datastructureandalgorithm.assets/3E6A48137367D997F49AB13EF302653A.gif)

  最后返回：【5，6，7，1，2，3，4】

- 代码(优雅)

  ```java
  public class Solution {
      public int[] solve (int n, int m, int[] a) {
          //取余，因为每次长度为n的旋转数组相当于没有变化
          m = m % n; 
          //第一次逆转全部数组元素
          reverse(a, 0, n - 1); 
          //第二次只逆转开头m个
          reverse(a, 0, m - 1); 
          //第三次只逆转结尾m个
          reverse(a, m, n - 1); 
          return a;
      }
      //反转函数
      public void reverse(int[] nums, int start, int end){ 
          while(start < end){
              swap(nums, start++, end--);
          }
      }
      //交换函数
      public void swap(int[] nums, int a, int b){ 
          int temp = nums[a];
          nums[a] = nums[b];
          nums[b] = temp;
      }
  }
  
  ```

### 14.2 螺旋矩阵

- 描述

  给定一个mxn大小的矩阵，按照螺旋的顺序返回矩阵中的所有元素

  数据范围：0≤n，m≤10，矩阵中任意元素都满足|val|≤100

  空间复杂度：O(nm),时间复杂度O(nm)

- 思路

  - step 1：首先排除特殊情况，即矩阵为空的情况。

  - step 2：设置矩阵的四个边界值，开始准备螺旋遍历矩阵，遍历的截止点是左右边界或者上下边界重合。

  - step 3：首先对最上面一排从左到右进行遍历输出，到达最右边后第一排就输出完了，上边界相应就往下一行，要判断上下边界是否相遇相交。

  - step 4：然后输出到了右边，正好就对最右边一列从上到下输出，到底后最右边一列已经输出完了，右边界就相应往左一列，要判断左右边界是否相遇相交。

  - step 5：然后对最下面一排从右到左进行遍历输出，到达最左边后最下一排就输出完了，下边界相应就往上一行，要判断上下边界是否相遇相交。

  - step 6：然后输出到了左边，正好就对最左边一列从下到上输出，到顶后最左边一列已经输出完了，左边界就相应往右一列，要判断左右边界是否相遇相交。

  - step 7：重复上述3-6步骤直到循环结束。

    ![alt](Datastructureandalgorithm.assets/34EC0DBACF8E56532AF5EE41BC84C258-165760662136933.gif)

- 代码

  ```java
  import java.util.ArrayList;
  
  public class Solution {
      public ArrayList<Integer> spiralOrder(int[][] matrix) {
          ArrayList<Integer> res = new ArrayList<>();
           //先排除特殊情况
          if(matrix.length == 0) {
              return res;
          }
          //左边界
          int left = 0; 
          //右边界
          int right = matrix[0].length - 1; 
          //上边界
          int up = 0; 
          //下边界
          int down = matrix.length - 1; 
          //直到边界重合
          while(left <= right && up <= down){ 
              //上边界的从左到右
              for(int i = left; i <= right; i++) 
                  res.add(matrix[up][i]); 
              //上边界向下
              up++; 
              if(up > down)
                  break;
              //右边界的从上到下
              for(int i = up; i <= down; i++) 
                  res.add(matrix[i][right]);
              //右边界向左
              right--; 
              if(left > right)
                  break;
              //下边界的从右到左
              for(int i = right; i >= left; i--) 
                  res.add(matrix[down][i]);
              //下边界向上
              down--; 
              if(up > down)
                  break; 
              //左边界的从下到上
              for(int i = down; i >= up; i--) 
                  res.add(matrix[i][left]);
              //左边界向右
              left++; 
              if(left > right)
                  break;
          }
          return res;
      }
  }
  
  ```

### 14.3 顺时针旋转矩阵

- 描述

  有一个nxn整数矩阵，请编写一个算法，将矩阵顺时针旋转90°，给定一个nxn的矩阵，和矩阵的阶数n，请返回旋转后的nxn矩阵。

  数据范围：0＜n＜300，矩阵中的值满足0≤val≤1000

  空间复杂度O(n^2^),时间复杂度O(n^2^) , 进阶：空间复杂度O(1),时间复杂度O(n^2^)

- 思路1（找出原矩阵和返回矩阵的位置关系）

  ![图片说明](Datastructureandalgorithm.assets/D41A5BF71032A625E80110D9E5546216.jpeg)

  从上图中的矩阵旋转来看：原矩阵元素的列数变成新矩阵元素的行数；原矩阵元素的行数是第2行，旋转后元素的列数是从右往左倒数第2列。因此对于原矩阵mat[i] [j]，旋转后该值应该在新矩阵ans[j] [n-i-1]的位置。

  - 代码(空间：O(n^2^),时间O(n^2^))

    ```java
    import java.util.*;
    
    public class Rotate {
        public int[][] rotateMatrix(int[][] mat, int n) {
            // write code here
            int[][] temp = new int[n][n];//新建temp对象，作为最终返回的对象
            for(int i = 0;i < n;i++){
                for(int j = 0;j < n;j++){
                    temp[j][n-1-i] = mat[i][j];//直接交换
                }
            }
            return temp;
        }
    }
    ```

- 思路2(主对角线翻转，再左右翻转)

  - 代码(空间：O(1),时间O(n^2^))

    ```java
    public int[][] rotateMatrix(int[][] mat, int n) {
            //先按主对角线翻转，再左右翻转
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < i; j++) {
                    int tmp = mat[i][j];
                    mat[i][j] = mat[j][i];
                    mat[j][i] = tmp;
                }
            }
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n/2; j++) {
                    int tmp = mat[i][(n-1) - j];
                    mat[i][(n-1) - j] = mat[i][j];
                    mat[i][j] = tmp;
                }
            }
            return mat;
        }
    ```

- 举一反三

  如果是逆时针旋转矩阵

  - 思路2(主对角线翻转，再上下翻转)

### 14.4 设计LRU缓存结构(最近最少使用)

- 描述

  设计LRU(最近最少使用)缓存结构，该结构在构造时确定大小，假设大小为 capacity ，操作次数是 n ，并有如下功能:

  1. Solution(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存
  2. get(key)：如果关键字 key 存在于缓存中，则返回key对应的value值，否则返回 -1 。
  3. set(key, value)：将记录(key, value)插入该结构，如果关键字 key 已经存在，则变更其数据值 value，如果不存在，则向缓存中插入该组 key-value ，如果key-value的数量超过capacity，弹出最久未使用的key-value

  关键点：

  1、一个最大容量、两个API

  2、保证都是O(1)的时间复杂度

  3、上一次访问的元素在第一个

  查找快、插入快、删除快、有顺序之分

- 思路

  1、显然 cache 中的元素必须有时序，以区分最近使用的和久未使用的数据，当容量满了之后要删除最久未使用的那个元素腾位置。

  2、我们要在 cache 中快速找某个 key 是否已存在并得到对应的 val；

  3、每次访问 cache 中的某个 key，需要将这个元素变为最近使用的，也就是说 cache 要支持在任意位置快速插入和删除元素。

  那么，什么数据结构同时符合上述条件呢？哈希表查找快，但是数据无固定顺序；链表有顺序之分，插入删除快，但是查找慢。所以结合一下，形成一种新的数据结构：哈希链表 LinkedHashMap。

  LRU 缓存算法的核心数据结构就是哈希链表，双向链表和哈希表的结合体。这个数据结构长这样：

  ![img](Datastructureandalgorithm.assets/1647580694-NAtygG-4.jpg)

  

- 代码

  ```java
  public class LRUCache {
      //自定义双向链表
      class DLinkedNode {
          int key;
          int value;
          DLinkedNode prev;
          DLinkedNode next;
          public DLinkedNode() {}
          public DLinkedNode(int _key, int _value) {key = _key; value = _value;}
      }
  
      //定义哈希表，映射key-node，方便在双向链表中快速找到对应节点
      private Map<Integer, DLinkedNode> cache = new HashMap<Integer, DLinkedNode>();
      private int size;
      private int capacity;
      private DLinkedNode head, tail;
  
      public LRUCache(int capacity) {
          this.size = 0;
          this.capacity = capacity;
          // 使用伪头部和伪尾部节点
          head = new DLinkedNode();
          tail = new DLinkedNode();
          head.next = tail;
          tail.prev = head;
      }
  
      public int get(int key) {
          DLinkedNode node = cache.get(key);
          if (node == null) {
              return -1;
          }
          // 如果 key 存在，先通过哈希表定位，再移到头部
          moveToHead(node);
          return node.value;
      }
  
      public void put(int key, int value) {
          DLinkedNode node = cache.get(key);
          if (node == null) {
              // 如果 key 不存在，创建一个新的节点
              DLinkedNode newNode = new DLinkedNode(key, value);
              // 添加进哈希表
              cache.put(key, newNode);
              // 添加至双向链表的头部
              addToHead(newNode);
              ++size;
              if (size > capacity) {
                  // 如果超出容量，删除双向链表的尾部节点
                  DLinkedNode tail = removeTail();
                  // 删除哈希表中对应的项
                  cache.remove(tail.key);
                  --size;
              }
          }
          else {
              // 如果 key 存在，先通过哈希表定位，再修改 value，并移到头部
              node.value = value;
              moveToHead(node);
          }
      }
  
      private void addToHead(DLinkedNode node) {
          node.prev = head;
          node.next = head.next;
          head.next.prev = node;
          head.next = node;
      }
  
      private void removeNode(DLinkedNode node) {
          node.prev.next = node.next;
          node.next.prev = node.prev;
      }
  
      private void moveToHead(DLinkedNode node) {
          removeNode(node);
          addToHead(node);
      }
  
      private DLinkedNode removeTail() {
          DLinkedNode res = tail.prev;
          removeNode(res);
          return res;
      }
  }
  
  ```

### 14.5 设计LFU缓存结构(最近最不经常使用)

- 描述

  一个缓存结构需要实现如下功能。

  - set(key, value)：将记录(key, value)插入该结构
  - get(key)：返回key对应的value值

  但是缓存结构中最多放K条记录，如果新的第K+1条记录要加入，就需要根据策略删掉一条记录，然后才能把新记录加入。这个策略为：在缓存结构的K条记录中，哪一个key从进入缓存结构的时刻开始，被调用set或者get的次数最少，就删掉这个key的记录；

  如果调用次数最少的key有多个，上次调用发生最早的key被删除

  这就是LFU缓存替换算法。实现这个结构，K作为参数给出

  数据范围：0<*k*≤10^5^，∣val∣≤2×10^9^

  要求：get和set的时间复杂度都是 O(logn)，空间复杂度是 O(n)

- 代码

  ```java
  class LFUCache {
  
      Map<Integer, Node> cache;  // 存储缓存的内容，Node中除了value值外，还有key、freq、所在doublyLinkedList、所在doublyLinkedList中的postNode、所在doublyLinkedList中的preNode，具体定义在下方。
  
      DoublyLinkedList firstLinkedList; // firstLinkedList.post 是频次最大的双向链表
  
      DoublyLinkedList lastLinkedList;  // lastLinkedList.pre 是频次最小的双向链表，满了之后删除 lastLinkedList.pre.tail.pre 这个Node即为频次最小且访问最早的Node
  
      int size;
  
      int capacity;
  
  
  
      public LFUCache(int capacity) {
  
          cache = new HashMap<> (capacity);
  
          firstLinkedList = new DoublyLinkedList();
  
          lastLinkedList = new DoublyLinkedList();
  
          firstLinkedList.post = lastLinkedList;
  
          lastLinkedList.pre = firstLinkedList;
  
          this.capacity = capacity;
  
      }
  
  
  
      public int get(int key) {
  
          Node node = cache.get(key);
  
          if (node == null) {
  
              return -1;
  
          }
  
          // 该key访问频次+1
  
          freqInc(node);
  
          return node.value;
  
      }
  
  
  
      public void put(int key, int value) {
  
          if (capacity == 0) {
  
              return;
  
          }
  
          Node node = cache.get(key);
  
          // 若key存在，则更新value，访问频次+1
  
          if (node != null) {
  
              node.value = value;
  
              freqInc(node);
  
          } else {
  
              // 若key不存在
  
              if (size == capacity) {
  
                  // 如果缓存满了，删除lastLinkedList.pre这个链表（即表示最小频次的链表）中的tail.pre这个Node（即最小频次链表中最先访问的Node），如果该链表中的元素删空了，则删掉该链表。
  
                  cache.remove(lastLinkedList.pre.tail.pre.key);
  
                  lastLinkedList.removeNode(lastLinkedList.pre.tail.pre);
  
                  size--;
  
                  if (lastLinkedList.pre.head.post == lastLinkedList.pre.tail) {
  
                      removeDoublyLinkedList(lastLinkedList.pre);
  
                  } 
  
              }
  
              // cache中put新Key-Node对儿，并将新node加入表示freq为1的DoublyLinkedList中，若不存在freq为1的DoublyLinkedList则新建。
  
              Node newNode = new Node(key, value);
  
              cache.put(key, newNode);
  
              if (lastLinkedList.pre.freq != 1) {
  
                  DoublyLinkedList newDoublyLinedList = new DoublyLinkedList(1);
  
                  addDoublyLinkedList(newDoublyLinedList, lastLinkedList.pre);
  
                  newDoublyLinedList.addNode(newNode);
  
              } else {
  
                  lastLinkedList.pre.addNode(newNode);
  
              }
  
              size++;
  
          }
  
      }
  
  
      /**
     * node的访问频次 + 1
     */
      void freqInc(Node node) {
  
          // 将node从原freq对应的双向链表里移除, 如果链表空了则删除链表。
  
          DoublyLinkedList linkedList = node.doublyLinkedList;
  
          DoublyLinkedList preLinkedList = linkedList.pre;
  
          linkedList.removeNode(node);
  
          if (linkedList.head.post == linkedList.tail) { 
  
              removeDoublyLinkedList(linkedList);
  
          }
  
  
          // 将node加入新freq对应的双向链表，若该链表不存在，则先创建该链表。
  
          node.freq++;
  
          if (preLinkedList.freq != node.freq) {
  
              DoublyLinkedList newDoublyLinedList = new DoublyLinkedList(node.freq);
  
              addDoublyLinkedList(newDoublyLinedList, preLinkedList);
  
              newDoublyLinedList.addNode(node);
  
          } else {
  
              preLinkedList.addNode(node);
  
          }
  
      }
  
  
      /**
     * 增加代表某1频次的双向链表
     */
      void addDoublyLinkedList(DoublyLinkedList newDoublyLinedList, DoublyLinkedList preLinkedList) {
  
          newDoublyLinedList.post = preLinkedList.post;
  
          newDoublyLinedList.post.pre = newDoublyLinedList;
  
          newDoublyLinedList.pre = preLinkedList;
  
          preLinkedList.post = newDoublyLinedList; 
  
      }
  
  
      /**
     * 删除代表某1频次的双向链表
     */
      void removeDoublyLinkedList(DoublyLinkedList doublyLinkedList) {
  
          doublyLinkedList.pre.post = doublyLinkedList.post;
  
          doublyLinkedList.post.pre = doublyLinkedList.pre;
  
      }
  
  }
  
  
  
  class Node {
  
      int key;
  
      int value;
  
      int freq = 1;
  
      Node pre; // Node所在频次的双向链表的前继Node 
  
      Node post; // Node所在频次的双向链表的后继Node
  
      DoublyLinkedList doublyLinkedList;  // Node所在频次的双向链表
  
  
  
      public Node() {}
  
  
  
      public Node(int key, int value) {
  
          this.key = key;
  
          this.value = value;
  
      }
  
  }
  
  
  
  class DoublyLinkedList {
  
      int freq; // 该双向链表表示的频次
  
      DoublyLinkedList pre;  // 该双向链表的前继链表（pre.freq < this.freq）
  
      DoublyLinkedList post; // 该双向链表的后继链表 (post.freq > this.freq)
  
      Node head; // 该双向链表的头节点，新节点从头部加入，表示最近访问
  
      Node tail; // 该双向链表的尾节点，删除节点从尾部删除，表示最久访问
  
  
  
      public DoublyLinkedList() {
  
          head = new Node();
  
          tail = new Node();
  
          head.post = tail;
  
          tail.pre = head;
  
      }
  
  
  
      public DoublyLinkedList(int freq) {
  
          head = new Node();
  
          tail = new Node();
  
          head.post = tail;
  
          tail.pre = head;
  
          this.freq = freq;
  
      }
  
  
  
      void removeNode(Node node) {
  
          node.pre.post = node.post;
  
          node.post.pre = node.pre;
  
      }
  
  
  
      void addNode(Node node) {
  
          node.post = head.post;
  
          head.post.pre = node;
  
          head.post = node;
  
          node.pre = head;
  
          node.doublyLinkedList = this;
  
      }
  
  
  
  }
  
  ```

  

