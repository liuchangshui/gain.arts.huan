# ARTS WEEK01 (0422-0428)
## Algorithm 
### 题目
```
7. Reverse Integer

	Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

	Input: 123
	Output: 321
	Example 2:

	Input: -123
	Output: -321
	Example 3:

	Input: 120
	Output: 21
	
Note:

	Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
	
```

### 解法 1
```java

class Solution {
    public int reverse(int x) {
        
        int newNumber = 0;
        
        while(x != 0)
        {
            // 获取一个int类型的数值，首先就数值用10进行取余。获得的这个数值个位数的具体数字
            int lastNumber = x % 10;
            
            // 将完成上一步使命的 x 数值，除以10，从而去除掉最后一位数字
            x = x / 10;
            
            // 如果新的数字 大于integer类型的最大值除以10 或者 新的数字等于最大值除以10 并且 附加在其后面的值大于7，就说明这个值将会在integer中报overflow          
            if(newNumber > Integer.MAX_VALUE / 10 || (newNumber == Integer.MAX_VALUE / 10 && lastNumber > 7)){
                return 0;
            }
            
            // 如果新的数字 小于integer类型的最小值除以10 或者 新的数字等于最小值除以10 并且 附加在其后面的值小于-8，就说明这个值将会在integer中报overflow          
            if(newNumber < Integer.MIN_VALUE / 10 || (newNumber == Integer.MIN_VALUE / 10 && lastNumber < -8)){
                return 0;
            }
            
            // 经过上一步骤，lastNumber是当前状态下的第一位数字。新的数字按照规则就变成了。
            newNumber = newNumber * 10 + lastNumber;
        }
        return newNumber;
        
    }
}

```

## Review
### [Teach Yourself Programming in Ten Years](http://norvig.com/21-days.html)

### 阅读笔记

	这篇文章确切来说是一篇读书笔记，是左耳朵耗子分享出来的，分享这篇文章的主要目的是能够通过这种方式对文章内容深入理解，另外一个目的是英文原版阅读从而提升英文阅读能力
	
**用十年的时间学会Java**<br>

**为什么大家都这么急躁**<br>
	走进书店，你会发现《24小时学会Java》的旁边有无数本各种各样，教你在几小时或者几天内让你学会C、SQL、Ruby以及算法的书籍。在亚马逊用teach、yourself、hours等关键字进行搜索，你会找出来512本这样的书籍。排名前十的其中有九本是关于编程的，另外一本是关于手账的。换一个“teach yourself” 作为关键词也会搜索到类似的结果。<br>
	上面的情景我们可以得出结论，人类学习编程是非常急躁的或者认为编程是极其容易的。Felleisen在他的《怎样设计程序》的书中有这样一句名言，“烂程序写起来很容易，傻子也可以在21天内学会，甚至人体模型可以”。<br>
	我们分析下《24小时教会你C++编程》意味着什么<br>
	自学：24小时内，根本就没有时间写几个重要的程序，同时从中学习一些成功和失败的经验。也没有时间和经验丰富的程序员一起工作并且明白C++环境意味着什么。简而言之，就是你没有时间在24小时内学到很多。所以这类书籍只能告诉你一些皮毛而不会让你深入理解。Alexander Pope说过，不求甚解，很是危险。<br>
	C++：24小时之内你可能会学会一些C++的语法（如果你已经了解过别的语言的情况下），但是无法掌握如何应用这门语言的能力。直白点说，就是你可能会用C++写一个简单的程序，但是无法领略C++这门语言的魅力，无论是好的还是不好的方方面面。上面的关键点是什么呢？Alan Perlis说过，“一门编程语言如果不能影响程序员的编程思维方式，那么就不值得去学习和了解”，有一种可能的情况是你必须去学习一点C++，那就是需要完成一个任务，然后就不再学习了，因为你已经完成任务了。<br>
	24小时内：不幸的是，这完全不够，我们将在下一小节中来展示<br>
	
**让自己在十年内学会编程**<br>
	在神经学和生物学领域，研究表明，人类需要花费大约十年的时间去掌握一个领域的技能，包括围棋、音乐、绘画、钢琴、游泳、网球等。其中的关键点是：不是一遍一遍的重复工作，而是用刚好超过自己当前能力的一点的任务来挑战自己，做完后尝试去分析自己的表现，并修正这个过程中可能存在的错误，周而复始这个过程（一个螺旋上升的过程）。这个过程是没有捷径的，厉害如莫扎特，这个音乐奇才，从四岁开始花了13年的时间才向时间发布名曲，另外一个例子，Beatles在1964年就爆红，但是他们从1957年开始就已经在小酒吧开始演出了，当他们出名的时候，他们已经获得了很多成功了。<br>
	Malcolm Gladwell 有一个很流行的观点，尽管他说的是专注10000小时而不是十年。Henri Cartier-Bresson（1908-2004）有另外一个名言：“你的前10000张照片，是你最差的照片”（他没有预料到数码相机的到来，有些人可能一个星期就能拍摄出10000张照片），真正的专长是需要花费一声的时间去打磨。samuel Johnson(1709-1784)说过“在任何一个领域取得优秀的成绩，都需要花费一生的时间去努力，他不会被低价购买的”，并且 Chaucer 感叹说：“生命如此短暂，要学习的东西还那么多”，Hippocrates的一段摘录“ars longa, vita brevis”，这个是一个引文的一部分。翻译成英语的意思是，“生命短暂，艺术无止境，实验遭到反噬，下决定很难。”，当然没有一个确切的时间作为答案，掌握所有通向大师的技能，对所有人来说，所花费的时间是相同的也不合适啊（比如编程、围棋、音乐等），值得注意的时，在大多数领域，即使你是个天才，要达到专家级水平仍然需要时间，10000个小时只是给你一个概念，一个天才如果每周练习10到20个小时的时间，仍然需要数年时间才能达到专家级水平。<br>
	----下一次我们来分享如果你想成为一个程序员需要在思想上做些什么改变。

参考文献：[1][Teach Yourself Programming in Ten Years](http://norvig.com/21-days.html)
	
## Tip
### git极其简单的教程-高级篇（分支管理）？
	接上一篇基础教程，本次篇章主要讲解的是git高级篇内容，因篇幅限制，将分几部分进行讲解，首先是关于分支的使用，我们从最基础的分支概念开始，逐步深入，包括分支的分类、分支的切换、分支合并以及基于分支之上的版本管理理念，我认为工具的使用归根结底是思想与方案的落地，所以这里面的重中之重是版本管理理念。

第一部分：什么是分支
			
		分支的概念
		分支是将修改记录的整体流程进行分叉保存，分叉后的分支与其他分支是相互独立的关系。
		
		分支可以拆分出来的同时，也意味着分支可以合并，这样就可以将自己修改的内容合并到主分支上了。
		
		在创建数据库的时候，默认会有一个分支，及时master分支，后面的分支管理都是基于此分支进行的分支管理。
	
第二部分：分支的运用

		分支可以自由的建立，但是自由创建的基础是要建立在使用规范上的，只有遵循了使用规范才会让git的版本管控效能发挥最大。我们先介绍两个分支的基本概念，merge和topic。merge是主分支的概念，

		merge的特点
			1、随时发布release
			2、作为topic分支的源分支而存在
			3、针对该分支可以使用CI工具（因为这个分支是被认为可发布版本所在的分支）
			4、通常采用master作为merge的分支
		topic的特点
			1、未开发新功能或修复bug而设立的分支
			2、多个任务建议创建多个分支（比如测试任务、开发任务、发布任务、修复bug任务等）
			3、最终目的还是回到merge分支中去
		
第三部分：分支的切换

		分支间是可以切换的。切换采用的命令是checkout，git会从工作树还原向目标分支提交的修改内容，checkout之后的提交记录，将会最追加到目标分支。
		
		HEAD概念
			HEAD是指当前在使用分支的最后一次更新，通常默认指向的master分支，可以通过切换分支改变HEAD的指向。有点指针的概念
			
		stash概念
			还没有提交的修改内容或者新添加的文件，留在索引区或者工作树的情况下，当切换分支的时候，修改的内容会从原来的分支移动到目标分支。（映射到分支切换的第一段描述）
			但是如果checkout的目标分支中有相同文件的存在修改，checkout就会失败，这种情况下要么先提交修改内容或者将修改内容暂存在stash中后，再做checkout。
			stash是临时保存文件的区域，stash可以暂时保存工作树或者索引中未提交的内容，作为后面从stash区域中取出来，应用到原先的分支或者其他分支中去

第四部分：分支的合并

			还记得我们在第二部分讲解的内容吗？分支是分为merge和topic两种的，完成topic的分支是要合并回merge分支的。在这一小结中我们主要讲解下合并的方法都有什么？分别产生的效果是什么？
			
			merge合并
				使用merge可以合并多个分支，例如当前有两个分支，一个是master分支另外一个是bugfix分支。当bugfix分支合并到master分支上时，master没有任何改动的情况，只需要将bugfix分支移动到bugfix最新分支上，这样就完成了分支合并。这种情况叫做fast-foward合并（快进合并--有点像看电影时快进一样，不需要修改能直接快进到一个节点）
				而master存在改动的情况时，就需要把两个分支修改的内容合并起来，并新生成一个提交，这时master的HEAD会移动到该提交上。
			
			rebase合并
				首先rebase合并，bugfix分支合并到master分支，会追加在master分支后面去，这个流程回避merge分支合并展现的更加简洁。
				rebase合并后master分支的HEAD位置不变，因此要合并master和bugfix分支，是将master分支的HEAD移动到bugfix的HEAD上去。
				
			总结
				merge：保持修改记录，但是会使得记录很复杂
				rebase：记录简单，是在原有提交的基础上将修改记录合并进去，有可能造成原有内容不可用。
				
				实例：想记录简洁的话可以采用如下方案
					1、从topic分支更新merge分支的内容，使用rebase方法
					2、向merge分支提交topic分支的更新，先使用rebase，然后使用merge移动HEAD
		
第四部分：topic和merge分支的运用实例
![git分支使用模型](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/git%E5%88%86%E6%94%AF%E4%BD%BF%E7%94%A8%E6%A8%A1%E5%9E%8B%E7%A4%BA%E6%84%8F%E5%9B%BE.png)	

### git极其简单的教程-高级篇（分支管理实操）？
接下来的内容是实践操作的内容，带命令行的方式来展示我们在上面看到的内容信息。分为几个小节分别是：
	
	1、事前准备
	2、建立分支
	3、切换分支
	4、合并分支
	5、删除分支
	6、并行操作
	7、解决合并的冲突
	8、用rebase合并

1、事前准备
	
	按照我们在week02中分享的内容，在本地新建一个仓库并初始化和提交。

2、建立分支
	
	建立分支的命令格式  git branch <branchname>
	
	例如：git branch issue1
	
	补充：git branch 是将当前仓库的所有分支都列出来，其中带“*”号的分支表示当前正在使用的分支。
	
3、切换分支

	切换分支的命令格式 git checkout <branchname>
	
	例如：git checkout issue1
	
	补充：git checkout -b <branchname> 创建并切换分支
	
4、合并分支
	
	合并分支的命令格式 git merge <commit>
	
	例如：
		git checkout master 首先切换到目标分支
		git merge issue1 将issue1分支的内容合并到master分支上，这步操作要在上一步的前提下来执行。

5、删除分支
	
	删除分支的命令格式 git checkout -d <branchname>
	
	例如：git checkout -d issue1

6、并行操作
	
	这一个步骤我们来模拟一下团队的并行操作，从而制造出一种内容冲突的场景
	git branch issue2
	git branch issue3
	git checkout issue2
	git add myfile.txt
	git commit -m "添加commit 说明"
	git checkout issue3
	git add myfile.txt
	git commit -m "添加pull 说明"

7、解决合并冲突的问题

	先合并issue2
	git checkout master
	git merge issue2
	
	再合并issue3
	git merge issue3
	
	此时会报错的，因为相同的文件被修改，无法自动合并了，因此要手动修改，并add到索引区紧接着提交

8、用rebase方法进行合并
	
	刚才采用的是merge方法进行的合并，先切换到要合并的目标分支，然后将修改分支的内容用merge的命令合并到目标分支。
	这次我们使用rebase的命令进行分支合并。
	先将刚才的合并动作放弃
	git reset --hard HEAD- 此时我们将神奇的看到分支回到了以前的位合并的情况了
	
	git checkout issue3
	git rebase master
	此时这个命令同样会报错，因为内容冲突了。
	所以对内容进行修改，然后add文件并提交（这里需要注意，这个提交和merge方法合并采用的提交时不一样的，rebase的提交采用的命令格式是  git rebase --continue）
	切换到master分支
	git checkout master
	
	将HEAD移动到当前分支
	git merge issue3


总结：OK了，这个就是git简单教程的高级篇关于分支的讲解和实操部分，下回我会再次分享其他的教程。<br>
参考文献：[1][猴子都能懂的git入门--高级篇](https://backlog.com/git-tutorial/cn/stepup/stepup2_8.html)

## Share
### 系统版本管理模型
这回我们来分享一下，系统版本管理的数据模型设计思路，按照惯例，我们来首先看数据模型的建表语句

```sql/*==============================================================*//* Table: SYS_VERSION_DICT                                   *//*==============================================================*/create table SYS_VERSION_DICT(   VERSION_ID           varchar(25) not null comment '系统版本流水',   VERSION_TYPE_ENUM    varchar(50) not null comment '版本类型枚举，如ios andorid等',   VERSION              varchar(50) not null comment '系统版本号，如1.0.1',   VERSION_TAG          varchar(255) comment '版本标签',   VERSION_UPDATE_USER  varchar(255) comment '版本更新用户,如，nsevent等',   VERSION_UPDATE_TIME  datetime comment '版本更新时间',   VERSION_DOWNLOAD_URL varchar(255) not null comment '版本下载地址',   VERSION_DESC         varchar(500) comment '版本描述',   VERSION_UPDATE_MODE_ENUM varchar(80) comment '版本更新模式枚举，如10：全量， 20：增量',   VERSION_STATUS_ENUM  varchar(8) not null comment '版本状态枚举：如 10：正常   20： 关闭',   CREATE_USER          varchar(25),   CREATE_TIME          datetime,   UPDATE_USER          varchar(25),   UPDATE_TIME          datetime,   REMARK               varchar(255) not null comment '备注',   primary key (VERSION_ID));alter table SYS_VERSION_DICT comment '系统版本配置表';

```
我们来看下，这个表的属性字段，首先是版本类型枚举，比如ios和安卓，其次是版本号，这个是用来表现版本号的，再有就是更新用户、版本更新时间（可以指定更新时间），最后是版本下载地址和描述等信息，这样一个表结构可以满足绝大部分的版本管控的诉求。
