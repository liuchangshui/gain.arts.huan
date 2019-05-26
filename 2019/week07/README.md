# ARTS WEEK07 (0520-0526)
## Algorithm 
### 题目
```
279. Perfect Squares

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

	Input: n = 12
	Output: 3 
	Explanation: 12 = 4 + 4 + 4.

Example 2:

	Input: n = 13
	Output: 2
	Explanation: 13 = 4 + 9.

```

### 解法 1

```java

import java.util.Arrays;

class Solution {
    public int numSquares(int n) {
        //实例化一个n+1的数组，用来存储第i个数最少由多少个完全平方数组成的数量。
        int[] positiveIngeger = new int[n+1];
        //数组中的值进行初始化，赋最大的值
        Arrays.fill(positiveIngeger, Integer.MAX_VALUE);
        positiveIngeger[0] = 0;
        //理解规则，任何一个正整数，都可以由一个普通数+一个完全平方数构成
        //因此当输入的数为n时，概数可以分解为 i+j*j,以此为基础。
        //positiveIngeger[n] = positiveIngeger[i+j*j] = Math.min(positiveIngeger[i+j*j],positiveIngeger[i]+1);
        for(int i=0; i<=n; i++){
            for(int j=1; i+j*j<=n; j++){
                positiveIngeger[i+j*j] = Math.min(positiveIngeger[i+j*j],positiveIngeger[i]+1);
            }
        }
        return positiveIngeger[n];
    }
}

```

### 解法 2
![动态规划之完全平方数，状态转移方程推导](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92-%E5%AE%8C%E5%85%A8%E5%B9%B3%E6%96%B9%E6%95%B0.jpeg)

```java
import java.util.Arrays;

class Solution {
    public int numSquares(int n) {
        //实例化一个n+1的数组，用来存储第i个数最少由多少个完全平方数组成的数量。
        int[] positiveIngeger = new int[n+1];
        //数组中的值进行初始化，赋最大的值
        Arrays.fill(positiveIngeger, Integer.MAX_VALUE);
        
        for(int i=1; i<=n; i++){
            int nearCloseNumber = (int)Math.sqrt(i);
            if(nearCloseNumber*nearCloseNumber == i){
                positiveIngeger[i] = 1;
            }else{
                for(int j=nearCloseNumber; j>=1; j--){
                    positiveIngeger[i] = Math.min(positiveIngeger[i-j*j]+1,positiveIngeger[i]);
                }
            }
        }
        return positiveIngeger[n];
    }
}
```

参考文献：<br>
[1][leetcode题解(动态规划)](https://juejin.im/post/5b3b562e5188251a9f247cd5#heading-8)<br>
[2][记完全平方数的三种解法(BFS/动态规划/四方和定理)(Leetcode.279 完全平方数)](https://mp.weixin.qq.com/s/CrFETX5gD9m9Ej6WA_xslQ)

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

你不知道你所不知道的<br>
很多时候，当我们为解决某个问题而陷入长时间的痛苦时，某人如天使一样告诉我们某种算法或者技术后，问题就迎刃而解了，仿佛每件事都变的容易和简单。通常来说这种情况是幸运的，没有让我们花费巨量的时间和精力去寻找解决方案。如果没有发生这种情况，你也不会被责怪，因为你根本就不知道你所不了解的内容。对于我来说，我就掉进了“我需要的时候再去学习”。可是如果你连知道都不知道这些知识点存在，根本就无从谈起学习二字，谷歌等搜索引擎，会对这种情况有所缓解，但是不能彻底解决。在生活的世界中有大量的问题需要解决，每天冲击着我们的大脑，除非你知道某种问题的归类，再去寻找解决方案（比如，如果你知道一点关于搜索和限制繁殖，那么解决数独问题就很容易，否者将会很难）。如果你没有觉察或有适用的场景就没有办法学习相关的算法。如果你压根就不知道某门技术的存在，那么怎么能想到用这种技术去解决对应的问题呢？现实世界中，不会一直有人在旁边适时的告诉你应该这么做或者采用什么技术。我相信会存在百万行代码可以替换十亿行代码的功能，而且更快、更整洁也更简单，因为无论是谁写的，都存在他不知道的领域。

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
### 分享一些做算法的思考

	1、建立算法模型

## Share
### 编码技术成功的关键要点（本周继续分享这个内容）
这次分享的是英文，我将对这篇英文进行翻译，并分享给大家。
[The Key To Accelerating Your Coding Skills](http://blog.thefirehoseproject.com/posts/learn-to-code-and-be-self-reliant/)

