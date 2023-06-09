# 学生故事:用细条纹编程

> 原文：<https://blog.teclado.com/student-stories-chris-nyland-programming-with-pinstripes/>

> 在这篇博文中，Teclado 学生 [Chris Nyland](https://twitter.com/nylnd) 分享了他一边做全职工作，一边学习编程以开发有助于工作的工具的经历！

就像往常一样，它开始于一种绝望的行为。

我辞掉了在一家我热爱的公司做税务律师的工作，仅仅是因为有一项可怕的任务对我来说代价太大了:印花税土地税(“SDLT”)租赁计算。除了说当(在英国)承租人接受租约时，他们必须纳税之外，没有必要对它的变幻莫测进行太多研究。有一套远比真正与纳税义务成比例的更复杂的条件、计算规则和公式。

英国税务当局(HMRC)建立了自己的计算器，但他们自己承认，任何偏离(非常狭窄的)规范的事情都意味着从头开始建立基于时间的电子表格。这对学习 Excel 来说太棒了；但是在 Excel 上构建一个安全的、自动化的、可测试的和可授权的时间序列计算套件是很难的，更不用说实践了。我开始害怕一个计算进来。

所以我离开了法律行业，去了一家会计师事务所，在那里 SDLT 已经不在考虑范围之内了；我的一位同事使用数据分析工具对大量时间序列数据进行分析，寻找有助于客户发现增值税欺诈的异常模式。当我回到我原来的公司时，这种方法一直困扰着我，激励我再次尝试参加 SDLT“挑战赛”。

我希望我能指出某种好莱坞蒙太奇，在那里，一闪而过的洞察力之后是疯狂的创造力，并以令人兴奋的产品结束。但是我不能。因为我不会编码；在努力改正这个缺点的同时，我还要经营一家全职法律事务所，还要照顾一个年轻的家庭。此外，我只是想要一个漂亮的小应用程序，为我做算术。没什么改变世界的。

接下来，也是这篇文章所要讲述的，是在从事另一份工作的同时学习编码的缓慢而持续的道路。它的目的只是提供一些提示，并支持那些可能想做同样事情的忙碌的有抱负的程序员:这可能是一条孤独的路，我自己的经历可能会有所帮助。或许(如果不是太自负的话)我可以大胆地建议，这并不是最糟糕的做事方式。

# 开始:从“嗯？”敬泽德

我试了几本不同的书，但我发现大多数都很枯燥。最引人注目的是 Zed Shaw 写的(当时)免费的书《艰难地学习 Python》(T1)。我怎么推荐这本书都不为过。这本书的教学方法给我留下了极其深刻的印象，它的坦率、幽默，以及鼓励人们*甚至*“打破”你的代码。

我买了付费版，很快就看完了这本书。我发现 Zed 教授的*方法*和他教授的代码一样多，而且这种方法很有效。我会想出一个办法，给每一个小挑战添加一个“taxy”的旋转，即使它像打印字符串“tax liability is ...”一样强制，并附加一个固定的数字。

# 黑白回答:熊猫

在泽德的书读到一半的时候，我变得有点冲动，偷偷看完了。泽德推荐熊猫从事定量研究。因此，我找到了旅途中的第二本书:韦斯·麦金尼的[“用于数据分析的 Python”](http://wesmckinney.com/pages/book.html)。第一版在后面有一个关于 Python 的精彩摘要入门(在第二版的前面)。我开始偷偷把韦斯的书的例子放进泽德的书为我设置的挑战和附带项目中。我开始尝试复制我在 Excel 中构建的更基本的电子表格，但用的是熊猫。

非常缓慢地，一个非常笨拙的文件迭代出现了，它是 Zed 的“选择你自己的冒险”代码片段和熊猫数据帧的产物。但是当我在控制台中运行该文件时，它第一次返回了正确的数字，并显示了一些粗糙的工作方式。突然间，我觉得这可能只是一个可行的努力。

我从 Zed 的书中“毕业”,但是他没有其他的 Python 书籍，所以是时候自己动手了。此后，他写了一部优秀的续集。

下一步是继续我的 CYOA/数据帧弗兰肯文件。还有很多 Python 需要我去学习，但是在这一点上，我停下来学习了另外两个技能来帮助我:测试和版本控制。

当你试图兼职学习代码时，一个关键的问题是，你想“储存”你已经取得的成果，一点一点地试验(如果你迷路了，可以回到你原来的地方)，测试你的进度，从你停下来的地方快速地重新开始，而不必记住哪个不同名称的文件(`ex_24_1_a_experiment_b_dynamic.py`或`ex_21_1_a_final_experiment_c_static.py`)。)我最后一直在剪辑。这就是测试和版本控制变得重要的地方。

当 Zed 的书接近尾声时，它在我的剧目中增加了测试，我的进度开始加快，只是因为实验变得更加直接了。单位测试，鼻子，Pytest...事实是，你用什么并不重要——关键是你用了什么东西。

## 版本控制

添加到测试中的重要内容是对版本控制的初步掌握。当然，这是律师们普遍熟悉的东西(尽管我们几乎只使用集中式版本控制系统)。但是即使原理很容易掌握，转移到*事实上的*版本控制系统(Git)需要扎实的实践。在这方面，在我看来，领先的指南(遥遥领先)是 Travis Swicegood 的《T2 》,这本书构思巧妙，内容精彩。它有一个描述性和示例性页面的巧妙配对，有很好的插图。

掌握这一点给了我构建一个模块(“ORVILLE”)所需的效率，我可以将这个模块导入到 IPython(或者当时的 IPython Notebook)中，并进行计算。事情看起来很好。我甚至在 PyData 上谈到了这件事，受到了令人愉快的欢迎。这是从第一次点击 Zed 书中第一个练习的“保存”开始的第十二个月。

# 从项目到同事

然后事情在副业和工作项目之间的腹地陷入停顿。在工作和家庭之间的空闲时间里，我一直在努力研究奥维尔，以建立一个可以向我的公司展示的概念证明。尽管给他们留下了深刻的印象，但让它进入组织并在工作机器上运行，同时我试图证明我的编码能力，这是一种推销。在我等待和推动的同时，我通过阅读方便的 Python 风格或结构指南来巩固和润色我的知识，然后我将从这些指南中收集到奥维尔的信息，如[丹·巴德](https://dbader.org/products/python-tricks-book/)、[杰夫·克努普](https://jeffknupp.com/writing-idiomatic-python-ebook/)、[布雷特·斯拉特金](https://effectivepython.com/)和[马特·哈里森](https://leanpub.com/u/mharrison)的指南。

它采取了合并，一个了不起的 It 同事谁伴随着它，以帮助把 ORVILLE 的巩固阶段，并进入一个法律工作站。他力劝公司给我一台 Ubuntu 虚拟机，上面安装了新的 Anaconda Python，并告诉我去试试。

从那以后，我每天都用奥维尔来工作。我还为团队中的低年级学生设置了 Ubuntu box 的登录，鼓励他们通过 IPython 使用它。但是，可悲的是，他们甚至不愿写一点 Python(即使是用我给 ORVILLE 的易于理解的名称空间)。他们需要一个 UI——这基本上意味着把 ORVILLE 变成一个 webapp，或者添加一个 GUI。我选择了前者。

从 Lalith Polepeddi 令人愉快地直截了当的[“Python 的 Flask 框架介绍”](https://code.tutsplus.com/tutorials/an-introduction-to-pythons-flask-framework--net-28822?_ga=2.192818223.460443288.1541972064-1309881505.1541835603)，到 Miguel Grinberg 的优秀课程(其中当前最好的迭代[在这里](https://courses.miguelgrinberg.com/)，我构建了一个准系统，但功能完美的 Flask 和 jinja 2 ORVILLE 前端(ORVILLE web 层，或“OWL”)。我在[高灵 WLG](https://www.gowlingwlg.com) 的 IT 同事在上面撒了一些 CSS，做出了一个非常可爱的界面。代码现在是团队的重要成员。

# 从同事到可信赖的顾问

但是事情还没有完全结束。虽然法律中最重要的技巧是给出正确的答案，但真正的诀窍是只问*你需要的相关问题。我在 OWL 中将这些表格放在一起，它们有大约 20 个输入，并不是所有的都是相关或适用的。这使得向低年级学生传递计算变得更加困难，所以我决定尝试重写应用程序的前端，以便它只显示基于已经回答的问题的相关问题。这意味着学习足够的 React 来构建一个自包含的 web 应用程序(“Yaffle”)，该应用程序将汇编足够的 JSON 来发送到 Flask API，该 API 反过来会选择 ORVILLE 来完成该任务。*

## 烧瓶 API

第一步，也是两步中最重要的一步，是确保我有一个稳定的 Python 目标来瞄准我的第一个 React 应用程序。这使得 Teclado 自己的何塞·萨尔瓦蒂耶拉的[优秀的 API 构建指南](https://www.udemy.com/rest-api-flask-and-python)成为必不可少的看点。它清楚地分解了构建一个可靠的 RESTful API 所需要的东西。我目前正在享受他的[后续课程](https://www.udemy.com/advanced-rest-apis-flask-python/)，它增加了更多的铃声、哨声和稳定性。

API 完成后，是时候构建我的 React 应用程序了...

## 反应

首先，我必须了解 JavaScript——如果你有 Python 的工作知识，Stephen Grider 的[ES6 指南](https://www.udemy.com/javascript-es6-tutorial/)是一本很好的入门书(特别是当你和[以及类似于本文](https://sayazamurai.github.io/python-vs-javascript/)的许多文章中的任何一篇结合起来的时候)。

继续学习足够的 React 是一件非常痛苦的事情——尤其是因为它的持续变化使得许多课程很快就过时了，所以你需要一些保持最新的东西。在这方面，最终对我有用的是罗宾·维鲁奇精彩的[“学习 React 之路”](https://www.robinwieruch.de/the-road-to-learn-react/)，安德鲁·米德全面的 [React 网络开发课程](https://www.udemy.com/react-2nd-edition)，以及英国自己的[网络忍者](https://www.thenetninja.co.uk/)的 Youtube 视频。

# 有用的教训

所有这些把我们带到了今天。从我第一次愤怒地编码到现在已经五年了。我羡慕地看着那些在几个月内就获得全栈能力的人。但是，那时，我实际上并不想要一份编码工作——我很喜欢当律师:我只是想制造令人敬畏的电动工具，让我和我的同事的工作变得更容易忍受。

我也不后悔走这条路，因为我努力确保它也有自己的优势:我有更多的时间吸收和内化概念，以及探索困难的奢侈。我有一份日常工作，激发了我的早晚编码；以及一种业余爱好，这种爱好能让你从工作中暂时休息一下。也许我是在把一种需要变成一种美德——但这并不是世界上最糟糕的品质。

我不怀疑其他人可能会比我进步更快，甚至超越他们自己的道路，但是我能向那些既想从事代码工作又想从事与代码无关的全职工作的人传授什么经验呢？理想情况下，你可以更快地到达你需要的地方？

1.  当你学习一门课程时，要打字:不要欺骗自己——当你消耗信息时，你不能明智地点头——你也必须生产。
2.  从心中的目标开始(最好有点纠结于此):保持你的网状激活系统开启，这样当你阅读时，你可以筛选有用的信息。并且有一个你信任的仓库来存放这些金块(Evernote、Pocket、Moleskine，任何你喜欢的东西)。
3.  找到重叠部分:如果你打算过双重生活，那么你有责任确保这两种生活尽可能重叠。对我来说，每一秒钟的编码都是某种意义上的“工作”(不是每个雇主都像我一样支持)。
4.  让事情变小:如果你在业余时间做这件事，那么你需要给自己很多小的增量胜利。其中很大一部分是，在学习了基本的编码之后，进行版本控制和测试:这只是帮助你在适当的时候加入和退出。解决今天的问题——你可能会积累足够的洞察力来解决更大的问题。
5.  长话短说:在一个问题上很容易陷入困境。我自然被限制在(我的通勤)火车上一天两次 25 分钟的突发编码。这有助于你对所做的事情采取专注和注重结果的态度；
6.  ...但是不要害怕用大的解决方案来解决小问题:甚至布兰登·罗德斯也赞同这种方法。
7.  一旦你掌握了基础知识，掌握测试和版本控制——没有任何尝试或探索是真正浪费的(即使失败了)。
8.  带上你的技能。人们很容易忽略你已经能为奋进号带来的东西。律师:起草和编码是比你想象的更相似的技能；会计——你的优势——会让你倾向于很酷的自动化。
9.  有不同的学习方式。我有一系列的活动，我会根据自己所处的环境来参与。
    *   如果可以编码，那就编码；
    *   如果你不会编码，但是可以看一个 Udemy 或者 YouTube 的教程，那就看一个视频；
    *   如果你不能看视频，但可以阅读，那就阅读(无论是电子书还是硬拷贝)；
    *   如果这些你都不会，那就听播客，比如句法。如果你不在一个代码丰富的环境中，那么你就会错过听到术语流传的“潜移默化”。即使你不能完全欣赏技术播客的内容，它也可能只是给你一些背景，甚至是一些有用的内容。
10.  避免我犯过的错误(或者有时仍然会犯的错误):
    *   特别是，你很容易在 Twitter 上找到你的新兴技能的归属感。但这是一个充斥着不必要的政治和姿态的兔子窝，从中你将收获甚少。这些天，我试着去那里只是为了公开感谢好内容的创造者；
    *   跑向 StackOverflow 是非常容易的，但是不要打扰他们，直到你确定你有一个有效的问题，如果他们唐突地回来也不要担心——我偷看过，我潜伏过...但是我还没有在上面张贴任何东西。
    *   有许多伪装成捷径的分心事物——通常是你必须尝试的一个新的前沿图书馆的形式:不要把自己扣为最新和最棒的人质，同时你有相对奢侈的权利，没有人因为你使用了经过尝试和测试的东西而对你进行评判——尤其是因为周围很可能有更多既定的学习材料；和
    *   不要在网上到处寻找关于你所选择的技术的文章(黑客新闻、媒体等):如果你确实想了解你感兴趣的语言或技术的发展，那么就去找别人整理的每周电子邮件通知——有太多的可以列出来，但是任何看起来像 Pycoder 的每周的文章都是一个很好的起点，根本不需要花时间去阅读。