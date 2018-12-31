+++
author = "Bowen She"
categories = ["面经"]
tags = ["狗家", "onsite"]
date = "2018-12-17"
description = "一亩三分地Google onsite整理 P1"
featured = "google-02.jpg"
featuredalt = "Google 2"
featuredpath = "/img/面经/Google"
linktitle = ""
title = "狗家 oniste Part 01"
type = "post"

+++
***Disclaimer: The following resources are from 1point3acre.com(以下资源来自一亩三分地)***

# LeetCode 380
medium
https://leetcode.com/problems/insert-delete-getrandom-o1/
# LeetCode 381
hard
https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/

---
# Fraction to Recurring Decimal

🔗 [LeetCode 166](https://leetcode.com/problems/fraction-to-recurring-decimal/description/)

---
设计一个系统， 客户端发一些userid, key, value过来， 然后在一个dashboard上实时显示过去某个时间段内发消息最多的10个userid， 和对应的key/value
这里后面的时间也让白板写代码， 问如果是单机代码题这个怎么做.
🔗 [LeetCode 460]https://leetcode.com/problems/lfu-cache/

---

第一轮
2D grid，从起点左上角到右下角一共多少种走法。
Followup:
如果grid中有一个障碍物，如何计算
Followup2:
如果grid中有不止一个障碍物，如何计算


第二轮
在一个非常长的一维坐标系中，给一个List的线段（均平行于x轴，线段给出两端点坐标），这些线段有可能有重叠。请问所有给出的线段的总长度是多少（重叠部分只可计入一次）
Followup:
请实现一个添加线段的方法，每次输入一个添加的线段，返回当前所有线段的总长度（重叠部分只可计入一次）

第三轮
假设云虚拟机的使用会产生一系列日志，格式如下
{  int vmId, int numCourse,  int startTime, int endTime}
请在输入的一个list的日志中，找到并发使用量最多course的并发量数值返回。
Followup1:
如果日志中的time从second变成粒度非常小的microsecond怎么办
Followup2:
如果日志记录的输入量非常巨大怎么办

第四轮
给一个字典，里面是不重复的字符。再给一个输入的字符串。
请在这个字符串中找到所有不完全包含字典内字符的子字符串的个数并返回。

第五轮
假设用户交给你一个Binary Tree结构的数据，请设计一个API程序，实现以下方法
getRandomNodeVal()
Followup:
在此基础上实现如下两个方法
addNewNode(val)
removeNode(val)

---
[000](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465735&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%255B3046%255D%255Bvalue%255D%3D1%26searchoption%255B3046%255D%255Btype%255D%3Dradio%26searchoption%255B3109%255D%255Bvalue%255D%3D2%26searchoption%255B3109%255D%255Btype%255D%3Dradio%26orderby%3Ddateline&page=1)

1) Implement iterator of binary tree, two functions: next() and hasNext().
Follow up question: implement prev() function.

Given a stream of requests, keep the top 100 requests with largest value. Design a heap to keep the requests.

2) Given a matrix with white and black elments. Check if the white elments are all connected.

3) Given a list of integer interval, and a number, return the list of interval contains this number.  Follow up question: the number is float

4) System design: design an ID generator. Requirement: 1) unique 2) consecutive (roughly) 3) low latency-baidu 1point3acres

5) Serialize and Deserialize a binary tree

---
[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465719&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
1轮：
亚裔小哥
类似lc 486
但是guess那个api需要你自己设计，return black num/white num 分别代表位置和字符都正确的数量 和剩余位置不正确但是正确出现的数量
follow up是给一堆guess words和api return的 [black,white] list,
问怎么确认 一个新的newGuess 是否有可能正确

2轮：
被晃点的一轮

3轮：
英语很好的国人小姐姐
面完搜了一下原来是拿棋子的面经题目，但是没有准备到这一个
加上刚吃完饭有点犯困，也没太好思路
开始说了dfs的暴力解法，面试官问了下大概logic 说ok没太大问题 没让写码说直接开始考虑怎么optimize
我当时想的是不然先把码写出来吧 但面试官说不用
当时没什么思路 也只有一个简单的例子
我个人感觉这种step by step的题就往greedy想了，但是想得一些current best option都被提示有反例
开始闲聊了下有个面试官没来的情况怎么处理 最后时间不够了也没搞出来，她做了note 又说了good luck 而且白板上没有让写码跟拍照，估计血崩了
没见过这题是真心很难想到怎么做啊，看面经里说的办法感觉真是很独特，一口气凭空想到正确办法那一步感觉挺不容易的。
毕竟得首先往graph上去想，我根本就没太往那个方向想，还得自己定义neighbor

4轮：
中东大哥
先问了个怎么找direct graph 的connected component,并且尽可能节约空
聊了聊union find跟怎么path compression 跟 weighted的implementation，没让写码
然后问了个类似64的path sum，写了一黑板，但面试官

5轮：
美国老哥
类似lc 803
具体到写码真是肥肠难。。。。
---
[11](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465513&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
一共五轮
四轮纯coding
一轮半简单设计半coding
第一轮 美国大叔
1.求一个长方形和圆形是否相交，自己设计input
2.两个string，一个是另外一个插入一个字符得到的，找到这个字符
第二轮
国人漂亮小妹
刷题网站原题 记不清题号了
插入，删除，找random 一个数，要O（1）
followup
有重复的数字
第三轮
国人帅帅小弟
两个string，判断一个是另一的转换？就是每次替换一个字母，能最终得到另一个；followup 是需要中间字母的情况
比如“ab”到“ba” 不能直接“ab” -》“aa” 这样就转不成了，需要“ab” “cb” "ca" "ba"
第四轮
米国人
产生trillions ID，给一个forbiddeng dict，不能重复，不能有forbid word
怎么产生？怎么最优解？
第五轮
三角形，给个integer 是周长，给个float是面积，三个边是int，输出所有三个边的可能

----

[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465437&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)


三角Array（先增后减）找peek number， 如何搜索target？
   2.  AStream 和 BStream 两个代表整数的流比大小，流很长所以只允许常数空间， followup 假设里面有小数点， 有e
n m的方框里面有若干个球，如果每行或者每列有2个或者以上的球，我们可以拿掉一个，问最后最少剩下多少球？
给A和B两个字符串，每次操作可以将一个B串的子串（不用连续）放到当前串（初始为空串）后面，问最少要几次操作才能得到A？
想实现一个RateLimiter，给定Qps，对请求返回该请求是否可接受。 要从多个方面考虑， 比如要求很精准，允许使用一些空间。 或者不需要精准，只允许常数空间。
---
[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465305&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
1. 一个十位数字的ID, 设计一个rule-base的规则, 可以在不用查看数据库的情况下, 就知道你输入的ID存在某两位出现swap的情况 根据你设计的rule 实现一个ID递增的函数
2. [系统设计] - typeahead
3. [系统设计] - 设计一个service可以接受动态schema数据的ingestion和query-baidu 1point3acres
    e.g. upload: 用户可以自行upload任何schema的数据 {A:1, B:2, C:{D:3}}, {X:2, A:2, D:4}
           query:  可以按照任何column对该用户upload过的所有的数据 进行query
4. 输入法组的台湾小哥 全程中文 给字典返回所有可能match的结果 ab->”哈” c->”楼” abc->”电脑”

-input “abc”; output “[哈楼,电脑]”
5. 找出所有的ambiguous的数字 拍卖的时候举牌子 有时候举反了容易歧义  6->9 169->691 找出所有这样的数字  
6. 在给出的数组里, 可以组合成连续五个数字(出现顺序不一定有序)的组合的个数 1,4,3,6,2,1,3,4,5
        follow-up: 出现顺序有序呢
-baidu 1point3acres
7.散妖骑
---
[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=464873&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
[Image Overlap](https://leetcode.com/problems/image-overlap/)

----
[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=464595&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
1）用“.”和“-”的组合给a-z进行Morse code加密，要求是最长的code要尽可能短，比如a是dot，b可以是dotdash，etc，加密方法有多种，要求返回一种就可以。解法应该构造一个binary tree, 然后BFS，每一个node （. or -）都有同样的两个children (. and -)。
2）一个binary search tree，每个node有parent link，tree里可以有duplicate，给定任何一个node （不一定是root），求这个node的in-order successor。
3）给一个命令 ls abc_{x, y}_c{d, e}.txt，这个命令会执行ls abc_x_cd.txt， ls abc_x_ce.txt, ls abc_y_cd.txt, ls abc_y_ce.txt，implement一个method将一个String （比如abc_{x, y}_c{d, e}.txt）解析成a list of Strings （比如abc_x_cd.txt， abc_x_ce.txt, abc_y_cd.txt, abc_y_ce.txt)。{}可以有嵌套。
4）假定一个code repository，很多class name，比如MyClass, AnotherClass, YourNewClass, 然后给一个CamelCase的object的名字，check这个object是不是valid，比如AC, AnC, AnoC等都是valid （match AnotherClass), M也是valid (match MyClass) 但是AoC，YC就不valid。follow-up是如果这个repository的所有class都给定，然后会有频繁的request，应该怎么处理。
5）第五题记不清了，等我想起来在update哈

---
[1](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=464485&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)
第一轮，给骨骼doc加annotation，题不难，就是记不清了，followup没怎么答上来，但是小哥非常好，引导和交流的很愉快。第二轮是高频remove最多的石子那道，很多石子在同行同列就可以remove掉那个，followup两个问题记不太清但是也不难都答上来了，小哥其实还有followup但是好像自己觉得很难就直接告诉我了一个想法。第三轮是血崩，高频汇率，小哥一上来和我一直讨论一步一步的优化，优化到一个他觉得满意的复杂度然后开始写code，结果才写完前面部分code，后面主要的dfs代码都没时间写，太惨了，而且小哥面之前就告诉我一定要写real code，as close as possible，我就欲哭无泪，真的不是不会写啊，用java真的写的慢啊TUT，而且小哥没提示我时间所以我也没注意，没想到就不够了啊啊啊啊啊后悔不快点写，只求面试官高抬贵手，这轮真的交流的太多了耽误了好多时间。第四轮是高频左上到右上followup三连，都答上来了，followup写了code，小姐姐还安慰我。。第五轮也有点炸，但是印度小哥特别好，用n个骰子投出长度为n的string，一开始觉得特别简单，用dfs说了思路，然后小哥问可不可以优化，我就优化了一下，小哥继续问，，你还可不可以再优化，我？？？真的一脸蒙蔽，我眼看就没有时间写code了是不是在黑我，但是小哥突然让我写了我一开始说的第二种优化后的方法，小哥给了我extra大概有十分钟的时间，而且小哥还说这轮主要看explore不看code，而且说这个题很难，他也很犹豫要不要拿出来考我，虽然是安慰我，但是我也隐约感觉不会很好了这轮的评价，求印度小哥高抬贵手啊TUT
