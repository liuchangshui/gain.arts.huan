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
