# ARTS WEEK04 (0429-0505)
## Algorithm 
### 题目
```
9. Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

	Input: 121
	Output: true
	Example 2:

	Input: -121
	Output: false
	Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

	Input: 10
	Output: false
	Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
Follow up:

Coud you solve it without converting the integer to a string?
	
```

### 解法 1
```java
class Solution {
public:
    bool isPalindrome(int x) {
        //对于负数直接判定为不符合。
        if(x < 0){
            return false;
        }
        
        //对于小于10直接判定为符合
        if(x < 10){
            return true;
        }
        int x_temp = x;
        int resultNum = 0;
        //对输入的数字进行倒序排列，生成新的数字
        while(x_temp > 0){
            int lastNum = x_temp % 10;//获取当前数字中的最后一位数
            x_temp = x_temp / 10;//将当前数字去掉最后一位数字
            if(resultNum < 2147483647/10){
                resultNum = resultNum * 10 + lastNum;
            }else{
                resultNum = 0;
            }
        }

        //比较输入和输出的数字大小，若相等，则表示这两个数字是相等的
        if(x == resultNum){
            return true;
        }        
        return false;

    }
};

```

## Review
### [Teach Yourself Programming in Ten Years](http://norvig.com/21-days.html)

### 阅读笔记

	接上一周的翻译内容，开始翻译下一节，如果你想成为程序员应该怎么办呢？
	
**用十年的时间学会Java**<br>

**所以，你想成为程序员，应该这样做**<br>
	这是我认为如果想成功的编程所需要做的清单<br>
	* 对编程感兴趣，因为有趣所以才去干的，你得确认了，确实有足够的兴趣作为驱动力，保证你可以一直持续下去，让你能够做十年或者一万小时，以至于很久。<br>
	* 敲代码，最好的学习方式就是实践，更严格的说：“个体在特定领取的最优表现，不是作为长期经验的结果而自动获得的，但是经验丰富的个体，也可以通过刻意的努力，也能提高表现水准”并且“最有效的学习方法是需要为个体制定适合难度的任务，有效的信息反馈和持续纠正错误的机会。”这本“ Cognition in Practice: Mind, Mathematics, and Culture in Everyday Life”表达了这样一个有趣的观点。<br>
	* 和其他程序员探讨,阅读别人的程序代码，这将比任何书籍与培训课程都重要<br>
	* 如果你愿意的话，可以花四年的时间去读个大学（或者是研究生），这将给你带来获得工作的资质，也将帮助你对这个领域有更深的理解，但如果你不想去学校的话你也能够从工作中获取同样的经验（这需要更多的毅力），任何情况下，书本的学习永远是不够的。“光学习笔刷和像素无法使人成为画家，那么相较更加困难的是计算机教育无法使人变成变成编程专家”《新黑客字典》的作者Eric Raymond这样说。我曾经雇佣过最好的程序员是高中毕业，他开发了很多伟大的程序，他有自己的新闻组，他用自己的股票期权买了一个属于他的夜店。<br>
	* 和其他程序员一起工作，在某些团队中做最好的那一个，在另外一些团队中当比较差劲的那个，当你是最牛的那个的时候，训练的是领导项目，鼓励他人，当你比较差劲的时候，要学习团队master如何做，也要学习他们不愿意做什么（因为他们会让你来为他们干一些事情）。<br>
	* 接收别的程序员完成的项目，当最初的程序员不在时，了解别人写的程序并修复需要修改的内容，并思考如何设计，让自己的程序在别人接手后比较容易的进行维护。<br>
	* 学习至少半打数量的编程语言，包括一种类抽象语言（如java、C++），函数抽象语言（如Lisp、ML、Haskell），一门支持句法抽象语言（如，Lisp），一门说明性规约语言（如，Prolog、C++模板语言）和并发编程语言（如，clojure、Go）。<br>
	* 时刻铭记，计算机科学中，是包含计算的，要知道从内存中抽取一个word去执行，需要花费多长时间（包括未命中的情况），也要知道连续从磁盘中读取数据和重新在磁盘上定位数据需要多少时间。<br>
	* 努力加入到预研标准制定中去，可以是ANSI C++ 协会，后者决定你本地的代码格式是缩进两个或者四个空格，无论哪一条路，你都会学习到其他人喜欢一门语言的什么地方，有多喜欢这门语言，甚至了解到为什么他们会有这样的感觉。<br>
	* 拥有从语言标准化工作中撤退的优秀判断力。<br><br>
	拥有了这些想法，问题是仅从书本上你可以获得多少呢？从我的第一个孩子出生前，我阅读了所有该怎样做的书，但是我一直感觉自己是个菜鸟。30个月后，我的第二个孩子也出世了，难道我又去重新阅读一遍？才不呢，我依靠着我的个人经验，结果是相比于专家的几千页文字，这才让我觉得更有用也更加安心。<br><br>
	Fred Brooks在他的《 No Silver Bullet》定义了三步计划，来发掘伟大的软件设计师<br><br>
		--1.尽可能早的系统的识别顶级的设计人才。<br>
		--2.安排一个导师来负责这个开发新星并且小心的维护他的履历<br>
		--3.让设计师们有机会互相影响和激励<br><br>
	这假定了某些人具备成为伟大设计师的潜力，要做的只是引导他们前进 ，Alan Perlis说的更加简洁：“每个人都被教导如何成为一个雕塑家，但是米开朗基罗被教导为如何不成为一个雕塑家，伟大的程序员也同样如此”，Perlis说，伟大的人都有一些内在的特质，这些特质超过所接收的训练，但是这些特质来自哪里呢？天生的还是通过后天勤奋的开发，正如Auguste Gusteau（料理鼠王）所说，“任何人都可以烹饪，但是只有无畏的人才能成为大厨”，我更愿意说，把你人生中的大部分时间用在可以练习上，但是无所畏惧的精神才会让这些联系形成成果，或者如Anton Ego所说：“不是所有人都能成为伟大的艺术家，但是伟大的艺术家可以来自任何地方”。<br>
	所以尽管去买一些如php、java、ruby等书籍吧，你可能获取一些有用的只是，但是不会改变的你一生，也不会让你在24小时或者21天内有真的提高。尝试一下连续24个月去提升自己怎么样？好吧，现在你可以上路了。<br>
	
参考文献：[1][Teach Yourself Programming in Ten Years](http://norvig.com/21-days.html)
	
## Tip
### git极其简单的教程-高级篇（远端数据库、标签及改写提交）？
远端数据库

	pull命令：是从远端的共享数据库拉取最新版本合并到本地数据库，此时如果本地数据库没有做过修改，则会直接合并，如果做过修改则需要对冲突部分进行修复合并，然后在合并提交。

	fetch命令：有时候不想把远端数据库的内容直接合并，而仅仅是查看下远端数据库的内容，那么这时候就可以使用git fetch命令了，这个命令意味着会将远端数据库的内容同步到本地，获取到的内容被导入到一个没有名字的分支，这个分支可以从FETCH_HEAD中推出。
	如下图所示：
![git fetch命令执行后的效果示意图](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/git%20fetch%E5%91%BD%E4%BB%A4%E6%89%A7%E8%A1%8C%E5%90%8E%E7%9A%84%E6%95%88%E6%9E%9C%E7%A4%BA%E6%84%8F%E5%9B%BE.png)<br>
	
	接上图，当我们希望对这个分支进行合并的时候，可以执行git merge FETCH_HEAD命令或者重新执行git pull命令，效果图如下图所示:
![git pull 命令执行后的效果示意图](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/git%20pull%20%E5%91%BD%E4%BB%A4%E6%89%A7%E8%A1%8C%E5%90%8E%E7%9A%84%E6%95%88%E6%9E%9C%E7%A4%BA%E6%84%8F%E5%9B%BE.png)<br>
	
	从上面的两张图和说明中我们不难看出来，git pull = git fetch  +  git merge
	
	补充说明：git fetch 命令之后，如果想看一下远端数据库内容是什么，可以通过  git log -p FEATCH_HEAD 来查看变更记录。
	
	push命令：从本地数据库push到远程数据库时，要fast-forward合并push的分支。如果发生冲突，push会被拒绝的。
	若要共享在本地数据库创建的分支，需要明确的push。因此，没有执行push就不会给远程数据库带来影响，因而可以自由的创建自己的分支
	注意：基本上远程数据库共享的提交时不能修改的，因为如果一旦修改，那些以前依据远程数据库的特定提交就会出现很多不可预测的情况。
	
标签建立与管理
	
	git中的标签分为两种，一种是请标签（仅是包括了一个名字），另外一种是注解标签（包括：名称、注解、签名）
	添加轻标签：git tag <tagname>
				git tag master-liucs01
				显示标签列表：git tag
				显示包含标签资料的历史记录：git log --decorate
	添加注解标签：
				git tag -a <tagname>
				git tag -am "描写标签的注解" master-licus02
				显示标签列表和注解：git tag -n
	删除标签：	git tag -d <tagname>

改写提交
	
	修改最近的提交（commit --amend）
		
		使用场景：1、添加最近提交漏掉的档案；2、修改最近提交的注解
		
		操作实例：
				修改文件内容
				添加修改内容到索引区 git add filename
				修改最近的提交 git commit --amend
				
		检验步骤：
				通过git log命令查看
	=====================================			
	取消过去的提交(revert)
	
		使用场景：1、安全的取消过去发布的提交
				使用revert可以取消指定的提交内容，reset和rebase -i 也可以删除已经提交的内容，但是不能随便删除已经发布的提交内容，这时就需要使用revert创建否定的提交了。
		
		操作实例:
				git log查看日志
				git revert HEAD 取消最新的提交
				git log验证是否取消成功
	=====================================
	遗弃提交(reset)
		
		使用场景：1、复原修改过的索引状态（mixed-默认）；2、彻底取消最近的提交（hard）；只取消提交（soft）
				reset可以遗弃不想要的提交，在遗弃的时候，需要根据想影响的范围，指定上面的模式，从而决定是否复原索引区或者工作树区
		
		操作实例：
				用reset删除master分支最前面的两个提交
				git reset --hard HEAD~~ (注意，这里有两个“~”，表示往后退两个版本)
		
		补充信息：
				1、对于操作的记录，可以通过git reflog命令查看HEAD的变化，而且可以通过git reset --hard XXXXXX命令回到指定的提交节点。
				2、Reset错误的时候，在ORIG_HEAD上reset 就可以还原到reset前的状态（git reset --hard ORIG_HEAD）
	=====================================
	提取提交(cherry-pick)
	
		使用场景：1、把弄错分支的提交移动到正确的地方；2、把其他分支的提交添加到现在的分支
		
		操作实例：
				git checkout master
				git cherry-pick 99daed2
	=====================================
	改写提交的历史记录(rebase -i)
		
		使用场景：1、在push之前，重新输入正确的提交注解；2、清楚的汇合内容含义相同的提交；3、添加最近提交时漏掉的档案。
		
		操作实例：
				1、$ git rebase -i HEAD~~
				2、打开文本编辑器，将看到从HEAD到HEAD~~的提交记录。
				3、将显示的提交记录中的第二行，pick修改成squash，然后保存提交。
				4、这时因为合并后要提交，所以接着会出现编辑提交信息的界面，编辑后保存，两个提交就变成一个了
				------------------------
				和上面的操作一样，不同的地方是从第三步开始，需要将需要变更的内容的那一行，由pick修改成edit。
					将会有如下提示
					You can amend the commit now, with

        			git commit --amend

					Once you are satisfied with your changes, run

        			git rebase --continue
				
				git add filename   （添加修改的文件）
				git commit --amend （修改提交）
				现在已经commit，但是rebase操作还没结束。若要通知这个提交的操作已经结束，请指定 --continue选项执行rebase。
				git rebase --continue 
	
	汇合分支上的提交，然后一同合并到分支(merge --squash)
		
		使用场景：1、汇合主题分支的提交，然后合并到目标分支上去
		
		操作实例：
				git checkout master
				git merge --squash issue1
				如果发生了冲突，需要做如下操作
				git add sample.txt
				git commit

总结：OK了，这个就是git简单教程的高级篇所有部分的内容了<br>
参考文献：[1][猴子都能懂的git入门--高级篇](https://backlog.com/git-tutorial/cn/stepup/stepup2_8.html)

## Share
### 分享数据库的设计思路
![数据库设计思路@需求分析与逻辑设计](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%BE%E8%AE%A1%40%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90%E4%B8%8E%E9%80%BB%E8%BE%91%E8%AE%BE%E8%AE%A1.png)
