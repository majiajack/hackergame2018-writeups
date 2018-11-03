# USTC Hackergame 2018 Writeup

by [Ciel](https://ciel.pro)

View in my blog: <https://ciel.pro/hackergame-2018-writeup/>

## 绪言

科大第五届信安大赛举办的消息传到了我这个高三生的耳朵里，考虑良久还是参与了，于是就有了你在看的这篇 writeup 。两年前从学长的口中得知的第三届 Hackergame ，因为搞 Web 的原因所以对安全比较有兴趣，就以校外选手的身份参与了一下，当时还是闯关制，第五关就翻车了，但是也是我第一次接触 CTF 和认识 USTC 信安俱乐部的各位前辈。去年的 Hackergame 就取消了闯关的设定，但因为个人原因没能好好参与，人又菜，就都没有写 writeup 。虽然今年还是挺菜的，不过腾出了点时间参与，也算稍有进步，于是决定写篇 writeup 留给同道中人更是留给自己。

碎碎念就到这，下面进入正题。

## 签到题

到点了欢快地点进题目名就善良的第一题，第一眼以为是过关 flag 点击就送题，然后 Key 错误，发现粘进去的 Key 少了一位，手动补上失败，F12 发现 `<input>` 有 `maxlength` 限制，删除之，补全，提交，得到 flag “玩的开心”。

## 猫咪问答

~~题面梗玩的好（滑稽）~~前两年都有的~~搜索引擎~~信息搜集题，需要稍微耗时一点。

- 建校年份直接搜喂鸡百科
- 学号演变史直接搜出来一篇文章看懂了就好了，注意看博士生那一段
- 视频人数搜标题然后快进查一遍
- 索书号进入科大图书馆网站检索书名
- 教室编号在 LUG 站内检索聚会主题，LUG 链接首页有

flag 是“谷歌是你的好伙伴”，可以概括此题解法了。

## 游园会的集章卡片

可能是技术含量最低的一道题，但是略耗时，在 Pinta 里拼的好累，可以看一下文件数是 25 猜出来是 5\*5 （然而我没有）。据说还有打印了然后真·拼图的，那这题怕是打字复印社都会做。flag 是“图像处理快乐”，我。。（表情一阵抽搐）

## 猫咪和键盘

给出了一份被猫破坏的 C++ 代码，稍作观察（关闭自动换行）可发现是有部分字符列被移动到了错误位置，于是从语法角度观察，用 Sublime Text 的列编辑直接拉回原位，然而编译不过，看开头注释/编译信息发现需要开 `-std=c++17` ，看看好像没有恶意代码，于是直接运行得到 flag 。由于做了签到题后明智地跳过了 2 、3 题，顺利地拿到了这题的一血（然而并非校内选手），不料这时猫咪又突w13gcft4n kj87u6,/lp0o9--=l[

## Word 文档

拿过来怎么感觉都和前两年的 PDF 隐写很像，于是全选清除格式改字号看页眉页脚发现什么都没有，于是看了看文档看到“以ZIP格式压缩“这里恍然大悟，一瞬 `unzip` 得到 flag.txt 内容是 “docx/xlsx/pptx 都只是 zip 文件”，然后收拾一片狼藉的下载文件夹...

## 猫咪银行

~~猫咪居然要学习噶韭菜，主流币名字反向出题还行。。~~想起了第三届的校园书店，于是尝试买入负数个理财产品，然而发现都做了过滤，各种兑换也没有够大的汇率差可赚，理财产品即使算复利也不够数，两秒交易间隔和账号有效期背后的玄机也看不透……于是去做了别的题。后来别的题也懵比后回来，突然想起了整数溢出（希望后端不是 Python ... ），于是买入 $2^{32}$ 分钟，发现没溢出，重置，买入 $2^{64}$ 分钟，成功溢出！于是稍微调节分钟数使取出时间为过去，金额为正数，然后把 TSDU 兑换回 CTB 买 flag 即可，flag 是“邪恶的溢出啊”。

## 黑曜石浏览器

直接想把 UA 改为 `HEICORE` ，发现不行，把浏览器 UA 里的 `Chrome` 替换成 `HEICORE` 也无果。深知不能猜 UA 的我打开了好朋友谷哥，搜索黑曜石浏览器没想到还真有。，但是打开一看就发现不对，FLAG 自动机、船新国产内核，这原来玩的是红芯（REDCORE）的梗啊！！那这网站是出题人做的无误了~~（先来一个T~~，找到下载发现需要登录，于是随便打了个账号，发现需要用黑曜石浏览器登录才能下载黑曜石浏览器，注册也需要黑曜石浏览器！太毒了啊这是 Web 题？注入题？绝望地看了看源码然后发现一个

```javascript
var HEICORE_UA = "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) HEICORE/49.1.2623.213 Safari/537.36";
```

```shell
curl http://202.38.95.46:12001/ -H "User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) HEICORE/49.1.2623.213 Safari/537.36"
```

成功得到 flag “黑曜石赛高”。

P.S. 由于主页滑稽的描述和神奇的黑曜石登录设计，黑曜石浏览器成功成梗。

## 回到过去

大概看懂了题面，试着敲了一下发现完全看不懂输出，于是看 `info ed` 发现保存命令是 `w file` 。尝试在最后一个 `q` 前保存，保存的文件联成一行后，把那个 ESC 及其后的 c 删掉即为 flag 。然而我还是不会用 ed 甚至不知道 Lawrence 干了啥，感谢出题人介绍古代编辑器。

## 我是谁

~~我是谁？我在哪？~~

### 哲 学思考

随便打了点东西都不对，看看源代码没什么收获，于是打开了 F12 Network ，发现状态码居然是 `418 I'm a teapot.` 这个愚人节 RFC 定义的返回码，输入 “teapot” 得到 flag “我不能倒咖啡”，心疼小 T 一秒。然后被指引到第二问的链接，让你去给大佬倒一杯茶。

### Can I help me?

直接访问提示换一种方法，`POST` 提示此方法已废弃，于是

```shell
curl http://202.38.95.46:12005/the_super_great_hidden_url_for_brewing_tea/ -X OPTIONS -v
```

发现允许 `BREW` 方法和 `WHEN` 方法，如果执行 `WHEN` 方法则会告诉你 “Please, read RFC-7168, not RFC-2324.”，其中前者是 2014 年愚人节 RFC 后者是 1998 年愚人节 RFC，`BREW` 方法定义于前者，直接查阅的话也能得到。用 `BREW` 请求时提示 header 里缺东西，于是仔细看 RFC 发现需要指定 `Content-Type: message/teapot` 。于是

```shell
curl http://202.38.95.46:12005/the_super_great_hidden_url_for_brewing_tea/ -X BREW -H "Content-Type: message/teapot" -v
```

发现返回了 300 多重选择，header 里多了 `Alternates` （其实 RFC 里都写了），给出了新的链接，告诉你可以倒红茶，用新的链接再试一次

```shell
curl http://202.38.95.46:12005/the_super_great_hidden_url_for_brewing_tea/black_tea -X BREW -H "Content-Type: message/teapot" -v
```

得到 flag “给大佬递茶”。

P.S. 这道小题价值 300 分，是我这个菜做出来最值钱的题。

## 秘籍残篇 - 滑稽 Art

最开始查了下 Malbolge 语言，发现和 brainfuck 类似，头皮一阵发麻。因为忽略所有空格，于是直接扔上了解释器，结果提示 Key 错误，由于毫无读代码的意图于是暂时放弃。

后来看到“滑稽 Art"这个标题好像知道为啥有空格了，于是打开 Python

```python
import os
for i in range(500,2000): os.system('fold -w '+str(i)+' malbolge.txt > '+str(i)+'.txt')
```

全部打开进 Sublime Text （预先关闭自动换行）按住 Ctrl+Tab 到 1112 个字符/行所对应的文件左右，发现比例是较为适当的，图中读到 flag “滑稽大学”。

## 猫咪遥控器

没啥可说的，按给定的行进序列行进，路径在第四象限写出了 flag “喵喵”。我用 canvas 画的，用别的也行。

## 她的诗

想了一个问题，为何给出的是解码程序和密文，而不是给解码结果呢？结合题面提示「只纠结于字面意思是很费劲的，而且……你不会得到任何有用的结论。」，猜测解码出来的诗毫无意义，密文中一定隐藏了其他信息。阅读解码器代码得知编码是 `uuencode` ，就去喂鸡百科查了一下。每行第一个字符表示实际编码了多少字节，后面是编码后的字节，不难猜测到，可以把 flag 切碎了隐藏在每行末尾编码，然后把长度指示字符改小，这样正常解码只能解出她的诗。果然修改长度指示字符为最大后，行末出现了切碎的 flag "uuencode 隐写真好玩"。。。

## 猫咪克星

连上以后发现只有 30s ，手速是不够的，于是写 Python 自动计算 ...

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('202.38.95.46', 12009))
print(s.recv(1024))

while 1:
	data = s.recv(1024).decode()
	print(data)
	res = str(eval(data))+'\n' # data is dirty!!!
	s.send(res.encode())
	print(res)

s.close()
```

相信这么干了的同学一定和我一样被吓了一大跳，本来还准备 have a coffee 的时候突然清屏，然后自己家目录里的文件被刷了出来吓得赶紧狂按 Ctrl-C 。。。太恐怖了，我 hack 我 自 己，给出题人送上了自己的 shell ，感谢出题人没 `rm -rf *` 。。。

可以在如上代码中加手动判断是否执行，多轮连接仔细观察后发现只有四种非预期的指令：

```python
print('\x1b\x5b\x33\x3b\x4a\x1b\x5b\x48\x1b\x5b\x32\x4a')
__import__('time').sleep(100)
__import__('os').system('find ~')
exit()
```

分别是清屏、等待、遍历家目录和退出，都在 `eval` 之前直接替换成 `0` （此题 `None` 和 `0` 等效）就好了，一百个表达式之后，flag 是“人生短暂用 Python”（这个 flag 因为没法 `eval` 所以上述脚本正好会 crash ）。

## 猫咪电路

用 MC 出题丧心病狂。。。在同学帮助下成功在 Linux 下搞起了 MC ，然而我并不会红石逻辑，也记不住。观察一下整个装置，是一个树状的逻辑反馈，根结点是一个会变色的信标（期望状态为 1），中间有若干结点（逻辑分叉），叶结点是 40 个拉杆（状态未知）。这样就有方法了，对于从根（信标）开始深度优先遍历，在到每个子结点（逻辑分叉后）的红石路径上将一个红石替换成拉杆，测试子结点状态（反馈通/断）如何决定当前节点的状态，进而确定子结点期望的状态，然后选择一个子结点作为新的当前节点，将红石恢复，继续向末端进行，当判断了叶节点（拉杆）期望的状态时，就求出了 flag 的对应位，然后回溯继续遍历其他分支，直到整棵树遍历完成，40 个拉杆期望的状态就求出了。当子树足够小时，可以直接枚举叶子结点状态，我一般是 2 或 4 个就试一下，实际操作方便。~~不好是做 OI/ACM 题的感觉~~

## FLXG 的秘密 - 来自未来的漂流瓶

毒瘤六十四卦编码，参考维基百科替换解码后，得到损坏的 tar.gz 文件。解压得到可执行程序 `flag` 和 `passkey.txt` ，执行 `flag` 提示 Keyfile 不对，遂放弃。

没想到第一个 flag “卦的力量”就在二进制文件 `flag` 的末尾，我记得当时看文件尾了，怎么就没发现第一个 flag 呢，亏爆。

## C 语言作业

先 IDA 一下，发现 `__err` 函数内有 `execlp` 可以执行一个命令（过滤了 sh），再观察到 `__init` 函数内把几个 signal 挂到了 `__err` 上，于是我开始想怎么触发信号。直接 Ctrl-C 之类的只会弄坏 `nc` ，而信号似乎又不能通过网络远程打过去，这时我留意到了 `SIGFPE` 。然而除零被判掉了，这个计算器又不支持括号，就比较麻烦，我突然想起来（上网查也可得知）有一个 `-2147483648/-1` 会触发 `SIGFPE` ，试一试果然对了。

然后被要求输入一个命令，我想了一下，然后超时了。然后尝试直接 `cat flag` ，然后只输出了一个 “flag”？。？试了试 `less` / `head` 等都不正常，突然发现 `execlp` 没有传参。。于是使用 `vim` 然后 `:o flag` ，得到提示真的 flag 在文件“`-`”里，于是再 `:o -` ，得到 flag 。

## 加密算法和解密算法

首先 Get your brain fucked ，阅读一下这段程序，发现不难理解，可以在适当地方换行分组得到如下

```brainfuck
,[->>+++++++>>+++++>>+++>>++>>++++>++++++<<+++<<+++++++++<<++++++++<<++++++<<++++++++<]
>[->>+++++>>+++++++++>>+++++++++>>++>>++++<+++++++++<<++++<<++++<<++<<++<]<
中间省略九组类似的，+号个数有一些变化
,[->>+++++++++>>+++++++>>+++++>>++++>>++>+++++<<+++++<<++<<++<<+++++<<++++++++<]
>[->>++++++++>>++++++>>++>>+++++>>+++++++++<++++++++<<++++++++<<++++<<++++<<+++++++++<]

>++.>++++++.>++++++++.>++++++++.>+++.>+++++.>+++++.>+++++++.>++++.>+++++++++.
```

BF 的语法和标准不再赘述，可以看出是每组输入一个数（字符ASCII）到 $x\_0$，给 $x\_1～x\_{11}$ 加上一定值，加 $x\_0$ 次并同时清空 $x\_0$ ，然后给 $x\_2～x\_{11}$ 加上一定值，加 $x\_1$ 次并同时清空 $x\_1$ 。十个字符执行十次，最后给 $x\_2～x\_\{11\}$ 加上一定值输出。

根据 + 号个数和位置整理出两个矩阵 $A$ 和 $B$ ，行对应组，列对应内存位置，可以发现 $A\_{i,1}$ 都是 8 ，也就是说实际上 $B$ 中每行会执行 $8x\_0$ 次，根据此令 $A=A+8B$ ，忽略 $x\_0$ 和 $x\_1$ 两列得到一个方阵。容易想到这个方针转置后用密文做列向量增广一下，就可以高斯消元拿到原文了，然而整个过程是在 mod 64 意义下进行的，所以无法直接高消想了想后放弃。

看完 official writeup 后恍然大悟求逆，亏爆。

## 她的礼物

先说一句这次比赛是我第一次用 IDA 。

拿到后加那句诗做参数运行，发现有 `alarm` 定时退出了，拖进 IDA 找到 `main` 直接 F5 ，发现有一个 `233333` 次的循环，会不停地唱歌（雾）、做一些奇怪的运算和 `sleep` 两秒，循环结束后会有输出 flag 的过程，然而正常歌一次都唱不完更别提 `233333` 次了。于是在 IDA 中定位了 `sleep` 的两秒的位置，在 Sublime 里直接改成了 `0` ，然而还是跑不完。

由于没找到注册 `alarm` 的地方，如法炮制直接改了循环变量初值为 `233333` ，再运行发现直接吐出了 flag ？！欢天喜地交上去，愁眉苦脸滚回来，谁想到这样有意义的字符串还不对呢... 尝试改小初值（最后一字节为`00`）让他唱几次歌，发现果然 flag 有变化，尝试提交这个看起来还有错别字的 flag，过了？！（距离比赛结束不到半小时时，我的心情像过山车一样）

看了 official writeup 发现是直接搞掉了 `alarm` 、`sleep` 和 `system` ，然后跑出 flag ，那不知道我这个砍循环次数的做法算不算非预期？orz

## 后记

算是第一场认真打的趣味型 CTF ，花了一些时间，也认识到知识盲区很多有待覆盖，不盲区有待提高。第一次用 IDA 的萌新最后半小时做出来了她的礼物，冲到了 Rank 36 ，共计 2900 分，基本无憾了。

最后，感谢 Hackergame 2018 组委会各位的奉献，和全体参赛选手。

### 附：一些不会的题

#### 秘籍残篇 - 天书易解

上图中会发现很多零散在空白区域的字符，猜测连起来是 Key 然而失败了，可能只是生成的时候的噪音吧。真的没想到是真的要看 Malbolge 这么可怕。

#### FLXG 的秘密 - 难以参悟的秘密 & 王的特权 & 困惑的 flxg 小程序

逆不动，逆不动。

#### CWK的试炼 & 数理基础扎实的发烧友

猜测到和图片 LSB 隐写，音频隐写等有关，但是一没时间，二没工具，三不熟悉，就弃疗了。

#### 家里有矿 & Z 同学的 RSA & 一些宇宙真理 & 对抗深渊

根本就没有做的欲望，甚至看都不敢看。