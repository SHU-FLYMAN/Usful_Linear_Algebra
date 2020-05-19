[toc]

# 01 课程简介

## 1.1 为什么要学《线性代数》

从事三维重建和SLAM（以后统称SLAM，两者有些许区别，但区别不大）需要很好的数学基础，而《线性代数》是其中最重要的一门课，在SLAM各个环节都需要用到：

<img src="https://upload-images.jianshu.io/upload_images/10148170-01a57fa3bc00e1cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png" style="zoom: 50%;" />



SLAM的论文它是长这样的，比如说：[《ORB-SLAM2: an Open-Source SLAM System for Monocular, Stereo and RGB-D Cameras》](https://arxiv.org/abs/1610.06475v2)，它长这个样子，可以看到里面充斥着大量矩阵的东西：

<img src="https://upload-images.jianshu.io/upload_images/10148170-64fdd38001756a9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png" style="zoom:70%;" />

有人说，不不不，我会基本的矩阵运算就行，那个到时候用到查一下就行了，这个或许在深度学习领域可以，但在SLAM领域还真的不行，因为SLAM是建立在《李群》和《李代数》上面的，而《李群》和《李代数》的基础就是《线性代数》。《线性代数》不会你是真的要凉凉的：

> 为什么需要李群李代数：请看这个[链接](https://mp.weixin.qq.com/s/7gmSyF13UUMDOnxpHVx9lg)，看不懂没关系，简单说，相机的位姿不是转来转去的嘛，我们要这些点之间的旋转矩阵做些什么，比如说求导，相加等等一系列操作，而旋转矩阵必须是正交矩阵（什么是正交矩阵，反正就是一个特殊的矩阵），引入了额外的约束，反正这些常规的矩阵运算就不能操作了，引入李群和李代数来解决。

> 再简单说，SLAM中对相机不同位姿点的旋转矩阵做点什么，但是它比较特殊，你不能直接办了它，于是你耍了点手段，也就是用一堆看不懂的符号和特殊规则，李群和李代数来处理。

所以说，《线性代数》是一门SLAM的先修课（意思是，你要实现下面这个demo，一定要会），先给你们一个帅气的SLAM视频，这样东西酷才有人学嘛，点开下面这个链接：[波士顿动力 SpotMini 狗SLAM导航demo](https://www.bilibili.com/video/BV11p411o7By?from=search&seid=9550520077457032984)，你可以看到：

<img src="https://upload-images.jianshu.io/upload_images/10148170-a8d85dd492ac713e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" alt="image.png" style="zoom:50%;" />

既然这么重要，又很酷，那么就让我们来学习《线性代数》吧。

## 1.2 为什么我要更新这个系列

还有个问题，国内优秀的《线性代数》课程有很多，国外也有很多，那么为什么我要更新这门课呢？其实事情是这样的：

> 我小外甥不是不喜欢数学吗？小学六年级数学竟然及格都考不了，某一天，我问他你为什么不喜欢数学？他反问我，数学有什么用？除了日常买菜要用到数学，我还用到什么？呀，我去，把我给问住了。

可哥哥（舅舅）我还苦于做科研数学功底不够恨不能大学重念个数学系呢？对啊，生活中数学有什么用？我想跟他说：

1. 如果你数学不好，高考成绩就偏科，就考不上好大学，考不上好大学，就不好找好工作，找不到好工作，你就…为了你个人的幸福，也要好好学习呀。
2. 中国之所有有今天的成就和有一大批优秀的科研人员和工程师密切相关，而他们解决问题最重要的工具就是数学，为了祖国的四化建设你也得好好学习呀。

可小孩子哪懂这些啊？事实上这个问题，我认为在目前国内数学教育领域还是蛮严重的，“数学无用论”主要的表现有以下两点：

1. 初等教材，虽然讲了数学的应用，但是仅局限于一根香蕉，两个香蕉问题，或者游泳池这边开闸，那边放水，多久更新完一波水，这些应用不是幼稚就是莫名其妙，就不能先把水放光，把泳池洗干净了再进水进去？搞我吗？事实的场景是，夏天泳池日进斗金，它是不能歇业的，而且天天换水，一口气放光老板也没那么多钱，等等因素导致，所以要边放水边进水，给了这个条件，整个问题就变得合理多了。

   > 其实，泳池问题，这是一个非常复杂的控制问题，需要用到微积分和流体力学的知识。这个问题也有重要应用场景的，在化工领域，反应炉里这边要加反应的原材料，那边要产出反应物，而反应又需要每种反应物维持在特定的反应浓度。解决这个问题需要十年化工控制博士起步（关于控制为什么这么难，请参照下面给出的链接），国外也有家公司叫做Honeywell，霍尼韦尔，一套软件，几十个亿美元吧，每年还要付巨额维护费用，因为传感器会飘，怎么在传感器飘的情况下保证控制稳定？就这供应还是有价无市。
   >
   > [自动控制的故事](https://zhuanlan.zhihu.com/p/65339164)

2. 高等教材，没有讲数学的应用，比如说同济大学的《线性代数》教材，干脆不讲应用，一上来一大堆定义就干了个 **行列式**，就没讲行列式干嘛，事实上，四阶行列式计算，用一句流行的话说，小朋友，你是不是有很多问号，我算它干什么？它不是在玩我？

   > 行列式：它可以用来计算空间中点的体积，线性方程组是否有解，测度一个线性变换对图形面积的改变量，两极附近的地图的扩张比例问题用处。

这两个点导致的直接问题是我们的数学教育：

1. 小孩子不喜欢数学，因为这玩意“没用”啊（好学生不受影响，但目的也只是应付考试；差学生就觉得这门课没用，不想学了）；

   > 我们说，热爱数学，任何的爱和不爱都是有理由的，让小孩子爱上数学不是简简单单的一句话就可以解决的。相反，我们应该反思我们的数学教育。

2. 大人，一方面不会应用用数学，另一方面，数学自学能力的缺失（因为数学不有趣，没用，所以不会主动去学）；

   > 以我以及身边同学为例，比如说汽车消声器流体分析问题，用于求解的[有限元法](https://zhuanlan.zhihu.com/p/56326567?utm_source=wechat_session)的原理，因为它用到比较高级的线性代数知识，看着推导好的公式理解有时候都是问题。但也不会自己去找教材拓展自己的数学知识。

   ![img](https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1770626822,941989437&fm=26&gp=0.jpg)

国内讲《线性代数》，也不乏大量优秀的老师，但你遇到总归是小概率事件。还有，有会SLAM的《线性代数》老师吗？总结来说，更新这门课的意义就在于下面两部分：

1. 让《线性代数》有趣一点，为数学的推广做一点小小的贡献；
2. 教SLAM 入门的《线性代数》数学基础；

如果有讲错的地方，请及时指出，在issue里告诉我。

## 1.3 和其他线性代数课程的区别

大多内容可以看去看我推荐的视频和教材，里面讲的比我好不知道多少倍！而且，这也是一个研究生基本的自学能力。

但是如果你在其他地方看不懂线性代数的话，可以来看我的教程，本课程与其他课程相比主要有以下几点区别：

1. 以往的课程很多是由数学系的老师来上的，更多是理论上的推导，缺少实际的应用，比如我问下面几个问题：

   - 求行列式干什么？
   - 矩阵的迹有什么用？
   - 矩阵的特征值呢？

   回答不上来吧？本课程将从实际工程的角度，包括经济学、物理、图形学等角度给你一个高屋建瓴的概览，告诉你线性代数是有用的，现代生活没有它还真是不行的。

2. 这都21世纪了，光讲理论，不讲怎么用计算机实现，包括但不限于：

   - 现代科学中，线性代数是怎么被用到的？

   - 自己实现这些程序的时候，要注意什么？
   - 大型商业化数值计算库或者深度学习库是怎么去做优化的？

3. 讲课方式不同，每节课最长只有10分钟，原理我只会讲大致讲一遍。

总的来说，更多的是培养你的自学能力，实际应用数学能力，以及对数学的兴趣，理论的讲解请看给出的笔记和课外链接。

# 02 如何开始这个课程

## 2.1 课程大纲

- 第1章 线性代数中的线性方程
  - 1.1 线性代数有什么用？
    - 课程
    - [笔记]()
    - 作业

## 2.2 笔记方式

我们会给出整门课程的大纲，大家按部就班地学习记笔记、写代码就行，推荐以下要点：

1. 视频只看一遍，记大纲笔记，细节我们会有专门的笔记和推荐你去看的书本章节，数学是靠长期习的，别想着课上就学会。
2. 不论平时用什么软件做笔记，最后都要用Xmind理出自己的线性代数脉络，因为人真的很容易忘。
3. 题目/代码5分钟不会就看答案，别浪费时间，看完之后再补充知识，因为这是工程数学，会算就行。

代码和笔记都提供在仓库里面，视频在 bibi 里，请随意食用。

## 2.2 推荐教材

> 《线性代数及其应用（原书第5版）》：https://book.douban.com/subject/30310517/

![img](https://img1.doubanio.com/view/subject/s/public/s29854268.jpg)

这本书的作者是David C. Lay 教授，其在美国加利福尼亚大学获得硕士和博士学位，也是多所大学的教授，是目前市面上《线性代数》最好的教材没有之一，豆瓣评分9.3。这么优秀的教材，如果你不是特别特别差钱，请不要去下载盗版，因为以下理由：

1. 英文版原价1500多人民币，已经降到了50多块钱，500多页，差不多就剩纸张的价格了，里面还提供练习和代码，原作者很良心了。
2. 翻译质量很好，倾注了翻译人员大量心血，500多页，十几万字的教材，要翻整整一年，也没几个钱。寒了他们的心，以后这样良心的教材谁给你翻译？

----

推荐的课程，清华大学数学科学系的马辉教授和徐帆的国家级精品课：

> 《线性代数1》：https://next.xuetangx.com/course/THU07011000411/1516478
>
> 《线性代数2》：https://next.xuetangx.com/course/THU07011000412/1515599

其实也是用这本书做教材的，讲得非常好，就是讲得稍微有点快（大概因为人家面对清华学生的缘故）。

---

> 《矩阵分析与应用（第2版）》：https://book.douban.com/subject/25811213/

还有另外本书是西安电子科技大学（原名叫做中国人民解放军军事电信工程学院）的长江学者特聘教授，同时也在清华任教，著名的信息与信号处理专家张贤达教授的《矩阵分析与应用-第2版》，豆瓣评分也有8.9分。

这本书没有那么多证明，很多公理和结论都是直接给出，讲的内容更为深入全面，是一本进一步深入入门线性代数不可多得的教材（意思是，你如果上一本书没有学好的话，不推荐看）：

![矩阵分析与应用（第2版）](https://img9.doubanio.com/view/subject/s/public/s27201205.jpg)

> 张贤达老先生是信息与信号处理方向（就是中国预警机上那些雷达）师祖级的人物，一生发表了大量信号系统方面的论文，同时致力于我国的教育事业，出版了大量优秀的教材，为我国培养了大量信号系统方面尖端人才。
>
> 张老先生对我国科学事业做出来的贡献是不可估量，但很遗憾更新这个教程的时候，张老已经永远地离开我们了……
>
> 讣告：[清华信号处理著名学者张贤达去世，享年74岁](https://www.sohu.com/a/377599790_243614)

---

最后，关于吐槽《同济大学线性代数教材》，给个豆瓣链接：[《豆瓣：同济大学线性代数教材》](https://book.douban.com/subject/2197140/)，大家自己看完之后客观去点评一下！

## 2.3 课程要求

课程要求主要以下几点：

- 该课程没有任何数学先修知识要求，哪里不会自己去补哪里。
- 我不相信这些会成为阻碍你学习的因素，唯一困扰你的，就是你的懒惰，早上不肯起，晚上不肯睡，学一会就犯困。
- 你想要变得比别人优秀，如果没人家聪明，你就得多付出努力，趁人家偷懒时候多跑两步。

#  03 版权

关于版权，以下注意事项：

- 如果侵犯到您的权利，请立即联系，邮箱：fly_cjb@163.com
- 请不要使用我的课程、笔记卖钱，这有违我做这个教程的初衷
- 转发请引用这个仓库，其它的文件，如PPT、xmind请随意使用

