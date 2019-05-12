# ARTS WEEK05 (0506-0512)
## Algorithm 
### 题目
```
70. Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:

	Input: 2
	Output: 2
	Explanation: There are two ways to climb to the top.
	1. 1 step + 1 step
	2. 2 steps

Example 2:

	Input: 3
	Output: 3
	Explanation: There are three ways to climb to the top.
	1. 1 step + 1 step + 1 step
	2. 1 step + 2 steps
	3. 2 steps + 1 step
	
```

### 解法 1

强制递归求解，因为重复计算太多的原因，会导致时间和空间复杂度过高，时间复杂度达到n的平方，所以这个算法其实是不被leetcode收录的。
算法图解如图所示，被框选中的地方是需要重复计算的地方，会发现有大量的重复计算内容：<br>
![递归算法图解](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/%E9%80%92%E5%BD%92%E7%AE%97%E6%B3%95%E5%9B%BE%E7%A4%BA.png)

```java
class Solution {
    public int climbStairs(int n) {
        return climbEveryStairs(n);
    }
    
    
    private int climbEveryStairs(int n){        
        //set value is 1 when var[0] or var[1]
        if(n == 0 || n == 1){
            return 1;
        }

        return climbEveryStairs(n-1) + climbEveryStairs(n-2);
    }
}

```

### 解法 2

记忆搜索方法，这个算法是针对强制递归所做的优化，将重复计算部分的内容做了类似寄存器这样一个设置，临时对数值做保存，从而降低重复计算的内容，时间复杂度在可接受范围O(n)。

```java
class Solution {
    public int climbStairs(int n) {
        //using memory search approch to slove this problem
        //set var array that store processing data
        int[] climbArray = new int[n+1];
        return climbEveryStairs(n,climbArray);
    }
    
    private int climbEveryStairs(int n, int[] climbArray){
         //using looping statment to add every result
        
            //set value is 1 when var[0] or var[1]
            if(n==0 || n==1){
                return 1;
            }
            System.out.println(n+"===="+climbArray[n]);
            //set value is var[n] = var[n-1] + var[n-2] when var[n] is not -1
            if(climbArray[n] == 0){
                System.out.println(n+"===="+n+"-"+1+"+"+n+"-"+2);
                climbArray[n] = climbEveryStairs(n-1,climbArray) + climbEveryStairs(n-2,climbArray);
            }
        return climbArray[n];
    }
}
```


### 解法 3

动态规划算法，这个算法本质上也是递归，但是在这个题目中，递归的方式有别于我们传统意义上理解的递归，采用的是自下向上的递归方案，定义一个数组，根据题目将边界数值放入数组中，即array[0]=1以及array[1]=1，然后在此基础之上，设置一个循环，i=2，将2-->n范围内的数值采用 

```java
array[n] = array[n-1] + array[n-2];
```
来表现。这样就不是函数的直接调用，采用数组就可以来实现，而且可以进一步优化，不用数组，采用变量替换的方式，将空间复杂度降低到O(1)的水平

```java
class Solution {
    public int climbStairs(int n) {
        return climbEveryStairs(n);
    }
    
    
    private int climbEveryStairs(int n){        
        int[] climbStairsArray = new int[n+1];
        climbStairsArray[0] = 1;
        climbStairsArray[1] = 1;
        
        for(int i=2; i <= n; i++){
            climbStairsArray[i] = climbStairsArray[i-1] + climbStairsArray[i-2];
        }
        
        return climbStairsArray[n];
    }
}
```
参考文献：<br>
[1][leetcode题解(动态规划)](https://juejin.im/post/5b3b562e5188251a9f247cd5#heading-8)<br>
[1][climbing-stairs/solution](https://leetcode.com/problems/climbing-stairs/solution/)

## Review
### [The Greatest Developer Fallacy Or The Wisest Words You’ll Ever Hear?](https://skorks.com/2011/02/the-greatest-developer-fallacy-or-the-wisest-words-youll-ever-hear/)

### 阅读笔记

“I will learn it when I need it”! I’ve heard that phrase a lot over the years; it seems like a highly pragmatic attitude to foster when you’re in an industry as fast-paced as software development. On some level it actually IS quite pragmatic, but on another level I am annoyed by the phrase. It has become a mantra for our whole industry which hasn’t changed said industry for the better. The problem is this, in the guise of sounding like a wise and practical developer, people use it as an excuse to coast. There is too much stuff to know, it is necessary to be able to pick certain things up as you go along – part of the job. But, there is a difference between having to “pick up” some knowledge as you go along and doing absolutely everything just-in-time.

“当我需要的时候，我会去学习它的”！这句话我已经听了很多年了；诚然，在像软件开发这样的快速发展的行业中，这句话听起来像是培养务实精神而提出的。在某种程度上面也确实如此，但是从另外一些层面来看的话，这句话有其令人困扰的一面，因为它反而成了阻碍我们整个行业前进的魔咒了。它听起来像是一个经验丰富的开发者所说，所以人们以此为借口能划水就划水。有太多的东西需要知道，我们也确实需要在工作中能够学习掌握这些知识。但是工作学习起头并进和遇到问题解决问题是有本质区别的。

The whole industry has become a bunch of generalists, maybe it has always been this way, I just wasn’t around to see it, either way I don’t like it. No one wants to invest the time to learn anything really deeply, not computer science fundamentals, not the latest tech you’re working with, not even the language you’ve been coding in every day, for the last few years. Why bother, it will be replaced, superseded, marginalised and out of fashion before you’re half way done. I’ve discussed this with various people many times, but no one seems to really see it as a problem. “Just being pragmatic dude”. In the meantime we’ve all become clones of each other. You want a Java developer, I am a Java developer, you’re a Java developer, my neighbour is a Java developer. What differentiates us from each other – not much! Well, I’ve got some jQuery experience. That’s great, so you know how to build accordion menu then? Sure, I Google it and steal the best code I find :). In the meantime, if you need to hire a REAL expert (in anything, maybe you’re writing a fancy parser or need to visualise some big data), I hope you’ve stocked up on beer and sandwiches cause you’re gonna be here a while.

整个行业到目前已经变成一个多面手的时代，可能一直是这个样子的，只是我没有发觉罢了。也可能是我不愿意看到这样。近年来，没有人愿意投入时间去深入学习任何事情，包括计算机基础、工作中用到的最新技术甚至每天使用的编程语言。大家都会说，别浪费时间了，这些东西总归是将被替换、淘汰、边缘化的，又为什么去做这样的事情呢？就这个现象我和很多人探讨过，但是没有人认为这样的现象是有问题的。大家都说“做一个实用主义者吧”。
与此同时，这也意味着我们互相模仿。你想找一个Java程序员，我是Java程序员，你是Java程序员，我的邻居是Java程序员，我们之间有什么不同吗？--没有！还有，你告诉我“我学习了一些jQuery的知识”，“这很棒，所以你知道了怎么样做一个可折叠的菜单？”，你回答我说，我可以从google上找到并剽窃我能找到的最好的一段代码来实现。
同样的，如果你需要招聘一个真正的专家（也许你想要一个神奇的解释器或将大量数据进行可视化），我希望你为长期作战而准备好了足够的啤酒喝三明治

Ok, there are ways to differentiate yourself, I have better communication skills, which is why I do better. That’s important too, but, developers differentiating themselves based on soft skills rather than developer skills – seems a bit twisted. We all communicate really well but the code is a mess :). Hell, I shouldn’t really talk, I am a bit of a generalist too. Of course I’d like to think of myself as a T-shaped individual, but if we’re completely honest, it’s more of a dash-shaped or underscore-shaped with maybe a few bumps :). To the uninitiated those bumps might look like big giant stalactites – T-shaped indeed. You seem like an expert without ever being an expert, just one advantage of being in a sea of generalists.

正是这样，有很多方法来区分你我之间的差别，我拥有不错的沟通技巧，这让我做的比别人更好一点。这点同样很重要，但是对于开发人员来说，用软技能和开发技能来进行区分，多少是有些别扭的。就像是，我们都善于沟通，但是代码写的一团糟---该死的，我不应该说这样的真话。我也算是一个通才了，我想我是那种T型人才，但是如果我们扪心自问的话，大部分人都是破折号或者下划线一类的人，在这些破折号中，你就像一个巨大的钟乳石--你是T型的，你不是个专家也会被认为是个专家，这就是通才遍地都是的海洋中的优势。

Investing In Your Future
I don’t want to preach about how we should all be investing in our professional future, everybody knows we should be. Most people probably think they are infact investing, they rock up to work, write a lot of code maybe even do some reading on the side, surely that must make them an expert in about 10 years, and a senior expert in 20 (I keep meaning to write more about this, one day I’ll get around to it :))? But, if that was the way, every old person would be an expert in a whole bunch of stuff and that is emphatically not the case. Maybe it is just that people don’t know how to build expertise (there is an element of truth to this), but I have a sneaking suspicion that it’s more about lack of desire rather than lack of knowledge. What was that saying about the will and the way – totally applicable in this case?

投资你的未来
我不想传道似的告诉大家，我们应该为我们的未来专业进行投资，因为每个人都知道应该这样做。大部分人觉得自己正在投资，他们努力工作，写大量的代码甚至是边学习边工作，诚然，这将使他们在未来的十年内成为专家并在且在20年内成为高级专家（我会一直写关于这件事情的，总有一天将实现）但是，如果是这样的话，每一个上了年纪的人都将在某个领域成为专家，但事情肯定不会是这样的。也许是因为人们不知道在某个方向上去发展或者建立他们的专长（这是实际存在的）但是我私以为缺乏热情甚于缺少知识，我们探讨的内容都可以和这个观点匹配上。

I’ve gone completely off-track. “Investing in professional future” is just one of those buzzword things, the mantra is “I will learn it when I need it”. It was good enough for my daddy and it has served me well so far. Let’s apply this thinking to finance, “I will invest my money when I think I need the money”. Somehow it doesn’t quite have the same kind of pragmatic ring to it.

我完全跑题了，“投资未来”只是我们讨论的问题之一，这句魔咒“在我需要的时候我会去学习它的”，这句话给我老爸足够合适，同样的这句话也被我信奉多年，让我们想象一下，应用这句话到金融领域，“当我需要钱的时候，我自然会去投资”，换一种方式后将发现，这句话将不同样适用了。

You Don’t Know What You Don’t Know
We’ve all had those moments where you’re going through major pain trying to solve a problem until someone comes along and tells you about algorithm X or technology Y and it makes everything fast and simple. It was lucky that person just happened to be there to show you the “easy” way, otherwise you would have spent days/weeks trying to figure it out and it would have been a mess. You can’t be blamed for this though, you don’t know what you don’t know. For me, this is where the “I will learn it when I need it” mentality falls over. You can’t learn something if you don’t know it exists. Google goes a long way towards mitigating this problem, but not all the way. There are plenty of problems you will encounter in the wild where you can beat your head against the wall ad infinitum unless you know what class of problem you’re looking at (_e.g. if you know a bit about searching and constraint propagation, solving sudoku is easy, otherwise it’s really quite hard_). You can’t learn about an algorithm if you’re not aware of it or its applicability. You can’t utilise a technology to solve a problem if you don’t even realise it has that capability. You’re not going to always have someone there to point you in the right direction. I am willing to bet there is a billion lines of code out there right now which can be replaced with a million lines of faster, cleaner, better code simply because whoever wrote it didn’t know what they didn’t know.

I seem to be making a case for the opposite side here, if knowing what you don’t know is the ticket then surely we should be focusing on breadth of knowledge. Superficial awareness of as much stuff as possible should see us through, we’ll be able to recognise the problems when we see them and then learn what we need more deeply. Except it doesn’t work like that, skimming subjects doesn’t allow you to retain anything, our brain doesn’t work that way. If we don’t reinforce and dig deeper into the concepts we quickly page that information out as unimportant, it is a waste of time (think back to cramming for exams, how much do you remember the next day?). However if you focus on building deeper understanding of a subject – in an interesting twist – you will gain broad knowledge as well (which you will actually be able to retain). My grandad is a nuclear physicist, several decades of working to gain deeper knowledge of the subject has made him an expert, but it has also made him an excellent mathematician, a decent chemist, a pretty good geologist, a fair biologist etc. Just some empirical evidence that seeking depth leads to breadth as a side-effect.

Can You Learn It Fast Enough
Learn fast

Some stuff just takes a long time to learn. I am confident I can pick up an ORM framework I haven’t seen before without even breaking stride, I’ve used them before, the concepts are the same. But what if you need to do some speech to text conversion, not quite as simple, not enough background. Hopefully Google will have something for us to copy/paste. That was a bad example, only research boffins at universities need to do that crap. How about building a website then, we all know how to do that, but what if you need to do it for 10 million users a day. We just need to learn everything about scaling, I am sure the users will wait a month or two for us to get up to speed :). Yeah, I am just being stupid, all we need to do is hire an expert and … errr … oh wait, we’re all out of beer and sandwiches.

Why Should I Care
Working with experts is freaking awesome. You may have experienced it before, everything they say is something new and interesting, you learn new tricks with every line of code, you can almost feel your brain expanding :). You want to learn from the experts, so it’s really sad when you can’t find any. Since everyone is only learning when they “need it”, noone can teach anything to anyone. The chunk of wisdom here is this, you want to work with experts, but the experts also want to work with experts, so what are you doing to make sure the experts want to work with you? Being able to learn something when you need it is a good skill to have, but you can not let it be your philosophy as a developer. Yes it is a big industry you can’t learn everything, so pick something and make sure you know it backwards, if you’re curious enough to follow up on the interesting bits, you’ll find you have a decent grasp of a lot of other stuff at the end. And if you do a good enough job, other super-awesome-smart people are going to want to come and hang around you cause they’ll be able to learn something from you and you’ll be able to learn much from them. Everybody will be a winner.

Image by SamueleGhilardi and SpecialKRB
	
参考文献：<br>
[1][The Greatest Developer Fallacy Or The Wisest Words You’ll Ever Hear?](https://skorks.com/2011/02/the-greatest-developer-fallacy-or-the-wisest-words-youll-ever-hear/)<br>
[2][这是开发者的弥天大谎还是至理名言？](https://qtlkw.iteye.com/blog/1003357)<br>
[3][程序员的谎谬之言还是至理名言?](https://coolshell.cn/articles/4235.html)<br>

	
## Tip
### 针对电商领域，未店铺设置规则的可扩展表的设计

表结构如下图所示，因为涉及到一些商业机密，我通常会将表的字段与名字进行修改，但主体结构不会变化的，这个表所要承载的信息是能够保障针对店铺设置的规则可以在这个表中进行存储，可以看到，里面包括了rule_name和rule_code这两个字段，这两个字段的意义在于可以通过名称和编码让规则做定位。
剩下的是company和shop,可以定位为那个店铺设置的规则，再往下是重要的字段也是核心的字段，rule_input_key rule_input_value rule_output_key rule_output_value这四个字段扮演的角色是可以支持各种类型的规则信息，比如佣金规则，可以针对输出字段进行设置。如打折规则可以利用输入和输出字段进行联合设置。
这样的表结构让表的可扩展性增强了，同时也不会有过多的额数据冗余。

```sql/*==============================================================*//* Table: COMPANY_SHOP_RULE_DICT                             *//*==============================================================*/create table COMPANY_SHOP_RULE_DICT(   SHOP_RULE_ID         varchar(25) not null comment '店铺规则ID',   SHOP_RULE_NAME       varchar(50) not null comment '店铺规则名称：如佣金设置、连续入住规则',   SHOP_RULE_CODE       varchar(50) not null comment '店铺规则编码：匹配规则名称的英文简称',   COMPANY_ID           varchar(25) comment '公司ID',   SHOP_ID              varchar(25) comment '店铺ID',   SHOP_RULE_INPUT_KEY  varchar(20) not null comment '店铺规则输入key：标记为什么类型的规则，无输入的时候默认设置为defaultkey',   SHOP_RULE_INPUT_VALUE varchar(20) not null comment '店铺规则输入值：对应输入key，标记为规则值,无输入的时候，默认输入为defaultvalue',   SHOP_RULE_OUTPUT_KEY varchar(20) not null comment '店铺规则输出key：标记为什么类型的规则',   SHOP_RULE_OUTPUT_VALUE varchar(20) not null comment '店铺规则输出值：对应输出key，标记为规则结果值',   SHOP_RULE_STATUS_ENUM char(8) not null comment '店铺规则状态枚举：如，是否启用',   CREATE_USER          varchar(25) not null comment '创建人',   CREATE_TIME          datetime not null comment '创建时间',   UPDATE_USER          varchar(25) comment '更新人',   UPDATE_TIME          datetime comment '更新时间',   REMARK               varchar(255) comment '备注',   primary key (SHOP_RULE_ID));alter table COMPANY_SHOP_RULE_DICT comment '店铺规则表';

```


## Share
### 编码技术成功的关键要点
这次分享的是英文，我将对这篇英文进行翻译，并分享给大家。
[The Key To Accelerating Your Coding Skills](http://blog.thefirehoseproject.com/posts/learn-to-code-and-be-self-reliant/)

