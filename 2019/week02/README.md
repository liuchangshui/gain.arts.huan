# ARTS WEEK01 (0415-0421)
## Algorithm 
### 题目
```
2. Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
	Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
	Output: 7 -> 0 -> 8
	Explanation: 342 + 465 = 807.
	
```

### 解法 1
```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //设置初始节点对象
        ListNode listnode = new ListNode(0);
        //设置临时节点
        ListNode tempNode = listnode;
        int offsetNodeNum = 0;
        
        while (l1 != null || l2 != null){
            //取listNode对象中的第一个值
            int num1 = l1 == null ? 0 : l1.val;
            int num2 = l2 == null ? 0 : l2.val;
            //节点值+进位标识 求和
            int sum = num1 + num2 + offsetNodeNum;
            //判断和值是否大于等于10,若大于等于10,则进位标识设置为1
            offsetNodeNum = sum >= 10 ? 1 : 0;
            tempNode.next = new ListNode(sum % 10);
            tempNode = tempNode.next;
            if(l1 != null){l1 = l1.next;}
            if(l2 != null){l2 = l2.next;}
        }
        
        if(offsetNodeNum == 1){
            tempNode.next = new ListNode(1);
        }
        
        return listnode.next;
    }
}

```
## Review
### [Declaring Variables in Java](https://www.thoughtco.com/declaring-variables-2034319)

### 阅读笔记

	这是一篇关于Java变量定义的文章，文章通过什么是变量开始讲述，进而讲了怎样声明一个变量、初始化变量和如何为变量命名，通过这样三个步骤让读者明白Java中变量的一些基本知识，我们来看下作者是如何描述变量的吧
	开篇点题，首先变量是一个放置值的一个容器，所以在使用变量之前必须要声明变量
	
	怎么声明变量
	
	既然要声明变量必然要考虑，在Java中如何声明变量，声明的步骤和法则是什么。作者用了两端文字做了说明，第一段文字强调Java是一个强类型的编程语言，因此在变量声明时必须指定变量类型，基本的变量类型有八个，分别是 byte、short、int、long、float、double、char、boolean；第二段文字有了一个类比的方式，让读者更加便于理解声明变量时的类型指定，作者用了一个木桶的方式做了类比，首先木桶就是个容器，我们可以往木桶中放入物体和拿出物体，当我们给木桶贴了一个标签时，比如我们贴的是沙子，那么我们就只能往木桶中放入和取出沙子，如果放入其他东西就会被木桶警察所阻止，并判定为违法。同样的道理，贴标签就相当于类型指定、木桶警察就相当于Java编译器。
	
	初始化变量
	
	变量声明好了就能用了吗？作者告诉我们不可以，我们在使用变量之前还需要对变量进行初始化，就是为变量赋一个初始的值，否则如果我们直接使用变量做操作的时候就会抛出一个异常“variable numberOfDays might not have been initialized”，变量的初始化有好几种方式。
		int numberOfDays;
		numberOfDays = 7; //先声明后初始化
		---
		int numberOfDays = 7; //声明和初始化同步进行
	
	为变量起一个好名字
	
	为变量名字是为了标识出变量的唯一性，作者给出了为变量起名的几条规则
		保留关键字不可以用来起名字：比如 goto
		不能以数字开头，但是数字可以跟在第一个字母之后
		可以用字符开头，下划线 _ 和 美元符 $
		不能使用其他特殊字符或者空格
	同时建议为变量起名字的时候要起得有意义，比如一本书的价格，那么变量的名字可以是bookOfPrice，这样的好处是后面对于程序定位问题将会容易很多。当变量是多个单词组成的，请遵循首字母小写的驼峰命名法。
	
	总结
		变量是一个程序语言最基础的知识，作者用一个木桶和木桶警察的类比形象的让读者瞬间get到变量的点。
