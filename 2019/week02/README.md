# ARTS WEEK02 (0415-0421)
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

## Tip
### git极其简单的教程？
	今天要分享的是git的简单教程，在刚刚成为程序员的时候，我使用的是cvs作为版本控制系统，后来接触公司使用的是harvest作为版本管理软件，这个软件真实印象深刻啊，非常的慢，再后来就是比较流行的svn了。其实作为程序员来说最应该掌握的是git，因为git是linux之父创造的版本控制软件，他的理念是通过远程数据库和本地数据库分别管理和同步的方式对我们的文件和代码进行版本管理。好的我们进入今天的正题，git教程一共分为四部分，第一部分是介绍git的基本个概念。第二部分是git基础，安装并创建本地数据库。第三部分是创建远程数据库，包括与本地数据库产生关联。第四部分是版本合并和冲突解决。

第一部分：git基本概念

	首先：git数据库分为远程数据库和本地数据库两种
	远程数据库：配备专用的服务器，为多人共享而建立的数据库
	本地数据库：为方便用户个人使用，在用户本地建立的数据库（这样就可以在本地管理自己的代码版本了）
	数据库的创建：因为分为远程数据库和本地数据库，所以数据库的创建也分为两种方式第一种方式是直接在本地创建，第二种方式是从远程数据库复制一份到本地
	
	修改记录提交：有了数据库后，数据库存在的意义是可以存放和记录我们放在数据库中的文件，因此就会涉及到文件修改记录的提交问题。对文件修改内容提交时最好遵循以下tips
		tip1：不同类别的修改（功能添加和bug修复）最好分开提交，这样便于以后定位
		tip2：内容提交信息是非常重要的提交说明资料，请遵循如下规则
			第一行：提交修改内容的摘要
			第二行：空行
			第三行：提交修改内容的理由
			
	工作树和索引：在这里引入几个概念，在git的管理之下，我们实际操作的目录是“工作树”，在“工作树”和“数据库”之间有“索引”，“索引”是为了向“数据库”提交做准备的区域。从“工作树”到“索引”采用的命令是git add “filename” 。没有添加到索引的文件是不能被提交的。索引区存在的意义：可以避免工作树中不必要的文件提交，也可以将文件修改内容的一部分加入到索引区并提交
	
第二部分：git基础，安装并创建本地数据库

	安装git：去搜索引擎中随便找一篇文章都可以很顺畅的安装下来，本篇文章关注点是使用教程
	安装验证：git --version   若能正常显示，则表示安装成功
	
	git初期设定：安装git之后需要对git进行一些设定，包括用户名设定、密码设定、显示设定、别名设定等
		git config --global user.name "<用户名>"
		git config --global user.email "<邮箱>"
		git config --global color.ui auto
		git config --global alias.co checkout (将checkout用co别名代替)
	
	创建数据库：我们在学习git的时候首先需要创建一个数据库，在git中数据的英文名是“repository”，创建步骤如下
		1、在任意一个地方创建一个目录，比如我在桌面创建了一个目录
			mkdri toturial
		2、进入目录中
			cd toturial
		3、将新创建的tutorial设置到git仓库
			git init
		
		ps：这里面有的读者会问一下，如何删除这个目录呢，很简单，在在torurial目录下执行rm命令就可以
			rm -rf .git
		
	提交文件：具体步骤是在工作树区域创建文件，然后将文件提交到索引区，最后通过索引区提交到本地数据库
		1、添加一个文件，比如sample.txt,里面写一句话“连猴子都懂的git命令”
		2、查看工作树和索引的状态,会看到未添加到索引的文件
			git status
		3、添加文件到索引区
			git add filename
		ps: git add . 可以吧所有文件添加到索引
	
		4、从索引区提交文件仓库
			git commit -m "fist commit"
		5、可以使用git status命令再次查看工作树和索引区的状态
		6、使用git log命令查看数据库提交记录，可以看到我们这次提交的内容
		ps：log是进入到记录视图，退出方式与vim是一样的，先按esc，然后 ： 再次q 可以退出了
		
第三部分：创建共享数据库，包括本地数据push到远程数据库，以及修改内容的pull、push等

	创建共享数据库：我采用的是github来创建的数据库，大家有其他的创建数据库的网站也可以，创建共享数据库很简单，只需要有个账号就行，然后在网站上创建repository就可以，我们在网站上创建一个叫“toturial”的数据吧
	
	添加本地数据库到共享数据库：向远程数据库推送本地数据库的改动记录，首先需要在本地添加远程数据库
		 git remote add <name> <url>
		 $ git remote add origin https://[your_space_id].backlogtool.com/git/[your_project_key]/tutorial.git
	在添加的时候需要给远程数据库起个名字，这样下次推送的时候就不用输入一长串的URL了。
	请使用remote指令添加远程数据库。在<name>处输入远程数据库名称，在<url>处指定远程数据库的URL。
	tip：执行推送或者拉取的时候，如果省略了远程数据库的名称，则默认使用名为”origin“的远程数据库。因此一般都会把远程数据库命名为origin。
	
	推送修改记录到远程数据库：使用push命令，将本地修改内容推送到远程数据库
		gti push <repository> <refspec>
	使用push命令向数据库推送更改内容。<repository>处输入目标地址，<refspec>处指定推送的分支。
	运行以下命令便可向远程数据库‘origin’进行推送。当执行命令时，如果您指定了-u选项，那么下一次推送时就可以省略分支名称了。但是，首次运行指令向空的远程数据库推送时，必须指定远程数据库名称和分支名称。
		$ git push -u origin master
		Username: <用户名>
		Password: <密码>
	
	克隆远程数据库：将远程数据库克隆到本地，我们可以换一个目录，模拟另外一个人克隆的行为
		$ git clone <repository> <directory>
	使用clone指令可以复制数据库，在<repository>指定远程数据库的URL，在<directory>指定新目录的名称。
	
	push到远程数据库：在克隆下来的数据库中修改完内容后，添加到索引，然后commit到本地数据库，就可以再次push到远程数据库了。
	
	pull到本地数据库：当我们切回到我们在第二部分创建的数据库目录时，就可以使用pull命令将新修改的内容拉到本地数据库，从而获得他人修改的最新内容。
		$ git pull <repository> <refspec>...
	使用pull指令可以拉取远程数据库内容到本地数据库，在<repository>指定远程数据库的URL，在<refspec>指定拉取的分支
	
第四部分：版本合并和冲突解决
	
	本部分讲解的是使用git做简单的版本合并和冲突问题的解决，我们首先在构建一个场景，有A、B两人，首先对同一个共享数据库做了pull操作，然后A、B分别在本地都做了修改。此时B先push到共享数据库，此时A提交修改内容到共享数据库时会报冲突错误。对于这样的场景git要求按照如下步骤解决
		1、当A，push内容到共享数据库时，共享数据库报冲突错误。
		2、此时提示，使用git pull命令将共享数据库的内容拉取到本次，git会自动合并有冲突的内容
		3、我们需要自行打开文件，将程序自动合并的内容进行手工调整。
		4、此时再从工作树区域添加到索引区从而执行提交和push时就不会冲突了。
	tip：我们可以用log命令来确认数据库的历史记录是否准确。指定--graph选项，能以文本形式显示更新记录的流程图。指定--oneline选项，能在一行中显示提交的信息
		$ git log --graph --oneline
		*   d845b81 合并
		|\
		| * 4c01823 添加pull的说明
		* | 95f15c9 添加commit的说明
		|/
		* 3da09c1 添加add的说明
		* ac56e47 first commit

总结：OK了，这个就是git的基础教程，下回我会再次分享其他的教程。<br>
参考文献：[1][猴子都能懂的git入门--基础篇](https://backlog.com/git-tutorial/cn/intro/intro1_1.html)

## Share
### 关于电商系统中商户数据模型的设计
通常意义上的电商系统，我们只需要考虑如订单、商品模型就可以，但是当一个电商系统涉及到第三方入驻或者有店铺的概念后，商户的数据模型就自然需要我们来思考，那么到底什么样的数据模型可以满足商户数据存储呢？而且还要思考后期的拓展，那好我们来看看一个典型的商户数据模型应该是什么样的。都是基于什么考虑来设计的。

#### 商户模型

* 商户表 ： 用来存放商铺的基本信息。


#### 数据表结构
```sql
---商户表
/*==============================================================*//* Table: COMPANY_SHOP_INFO                                  *//*==============================================================*/create table COMPANY_SHOP_INFO(   SHOP_ID              varchar(25) not null comment '商铺ID',   COMPANY_ID           varchar(25) not null comment '公司ID',   COMPANY_NAME         varchar(50) not null comment '公司名称',   SHOP_TYPE_ENUM       varchar(8) not null comment '商铺类型枚举：餐厅、酒店等',   SHOP_NAME            varchar(50) not null comment '商铺名称',   SHOP_SUB_NAME        varchar(255) comment '商铺副名称',   SHOP_CODE            varchar(50) comment '商铺code',   SHOP_POSITION        varchar(25) not null comment '商铺行政区域,关联行政区划表',   SHOP_LOCATION_LONG   varchar(255) comment '商铺经度',   SHOP_LOCATION_LAT    varchar(255) comment '商铺纬度',   SHOP_ADDRESS         varchar(255) not null comment '商铺地址',   SHOP_TEL             varchar(30) not null comment '商铺电话',   SHOP_PHONE           varchar(30) comment '商铺手机号',   SHOP_MAIL            varchar(30) comment '商铺邮箱',   SHOP_DESC            varchar(255) comment '商铺描述',   SHOP_LEVEL           int comment '商铺等级',   SHOP_STAR_ENUM       varchar(8) comment '商铺星级：服务于酒店类型的商铺',   SHOP_LOGO            varchar(255) comment '店铺logo',   SHOP_HOST_IMAGE      varchar(255) comment '商铺主图：体现在商铺列表图中',   SHOP_CONTENT_HOST_IMAGE text comment '商铺内容主图：体现在商铺内的介绍图信息中，目前业务约束放五张图',   SHOP_CONTENT_VALUE   text comment '商铺内容值，可以存放富文本信息',   SHOP_STATUS_ENUM     varchar(8) not null comment '商铺状态枚举',   SHOP_OWNER           varchar(25) not null comment '店铺owner',   SHOP_QUALIFICATION   varchar(255) comment '店铺资质',   SHOP_BUSINESS_HOURS  varchar(255) comment '店铺营业时段',   SHOP_CARD            varchar(255) comment '商铺名片',   SHOP_OPEN_TIME       datetime not null comment '开店时间',   SHOP_CLOSE_TIME      datetime comment '关店时间',   SHOP_CLOSE_DETAIL    varchar(255) comment '关店原因',   SHOP_SUSPEND_USER    varchar(25) comment '店铺挂起人',   SHOP_SUSPEND_TIME    datetime comment '店铺挂起时间',   SHOP_SUSPEND_DETAIL  varchar(255) comment '店铺挂起原因',   CORP_CODE            varchar(50) comment '租户编码',   CORP_NAME            varchar(50) comment '租户名称',   CREATE_USER          varchar(25) not null comment '创建用户',   CREATE_TIME          datetime not null comment '创建时间',   UPDATE_USER          varchar(25) comment '更新用户',   UPDATE_TIME          datetime comment '更新时间',   REMARK               varchar(255) comment '备注',   primary key (SHOP_ID));alter table COMPANY_SHOP_INFO comment '商铺表';

```

总结：读者可以看下商户表的数据结构。
	首先商户和公司之间，应该是商户从属公司，所以商户表中有公司作为主键。
	其次，商铺一定是可以卖各类商品的，因此商铺要区别出各种各样的类型
	最后，这样的信息表要具备租户和创建人、更新人、创建时间和更新时间的概念才可以说得上完善。