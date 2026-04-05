---
title: "Claude Code + n8n = 工作流神器：一个搭得快，一个跑得稳"
source: "https://mp.weixin.qq.com/s/QlyfaMQEwxKZT7VlGGpaLA?scene=1&click_id=12"
author:
  - "[[富百]]"
published:
created: 2026-04-05
description: "前几天刷到一条推文，一个叫 Cody Schneider 的老外发了条长帖，说了一句让我停下来想了很久的"
tags:
  - "clippings"
---
原创 富百 *2026年3月3日 16:53*

---

前几天刷到一条推文，一个叫 Cody Schneider 的老外发了条长帖，说了一句让我停下来想了很久的话：

**一个人用 Claude Code + API + n8n 这套组合，一天干的活，顶500强公司一个团队干一年。**

然后他列了一下他当天做了什么：

> 40个 Facebook 广告、100个着陆页、3篇客座博客、4个播客预约（冷邮件自动发的）、5篇帮助文档、2个视频剪辑、25条推文排期、2个 LinkedIn 引流小工具。
> 
> 写到这儿他一天还剩4个小时。

这条推文 33 万人看了，3400 多人收藏。

我看到的第一反应不是"这也太夸张了"——因为我现在搭工作流，也是这么干的。不打开 n8n 界面拖节点，直接用自然语言告诉 AI 我要什么，AI 帮我把工作流建好。

回想一下你是怎么搭 n8n 工作流的？

打开浏览器 → 进入 n8n 界面 → 拖一个节点 → 配置参数 → 连线 → 测试 → 报错。

报错了怎么办？切到 ChatGPT 或者 DeepSeek，把报错信息贴过去问，拿到回答再复制回 n8n 改参数。改完再测，又报错，再去问，再复制回来……

**你的时间有一半花在了 n8n 和聊天窗口之间来回切换上。**

用 Claude Code + n8n MCP 完全不一样。AI 直接连着你的 n8n，它创建节点、配参数、测试、发现报错、自己改、再测试——整个过程不需要你复制粘贴任何东西，甚至不需要你打开 n8n 界面。

以前你用 ChatGPT，Gemini，豆包，AI 是 **顾问** ——你问它怎么配，它告诉你，但操作还是你自己来。

现在用 Claude Code + n8n MCP，AI 是 **操盘手** ——它直接上手帮你建工作流、改参数、跑测试。

![image](https://mmbiz.qpic.cn/mmbiz_png/RxhYNXicIDHkqZSrBbFK354DawniapNOMk6ickeCNzWod2DXfKufy4gV1f3Hicxxx2Uos4rQ5jbUHic5yhIn0X2pEZxrqbtNgWys6aH2z1USRtLo/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

---

## 这套东西到底是什么

说清楚这三个角色：

**Claude Code** — Anthropic 出的命令行 AI 助手。你在终端里用自然语言跟它说话，它能写代码、操作文件、调 API。不是聊天机器人，是真的能干活的——创建文件、安装依赖、运行脚本、调用接口，全部通过终端完成。

**n8n MCP Server** — n8n 官方出的接口协议，让 Claude Code 能直接操作你的 n8n 实例。创建工作流、修改节点、运行测试，全部通过自然语言完成，不用打开 n8n 界面。

**Skills（.md 文件）** — 给 Claude Code 的"说明书"。你把业务逻辑、常用配置、API 信息写成 Markdown 文件，Claude Code 读完就知道你的环境和习惯。其中 **n8n Skills** 尤其关键——Claude Code 是通用 AI，对 n8n 的节点配置和 Expression 语法不完全熟悉，n8n Skills 写好了最佳实践和常见坑点，让 AI 搭出来的工作流质量高很多。

三个拼在一起，效果是这样的：

你说："帮我搭一个工作流，监控这 5 个 Twitter 账号，有新推文就翻译成中文，存到飞书多维表格里。"

它直接调用 n8n API 帮你创建工作流，配好节点、设好定时触发。你打开 n8n 看，工作流已经躺在那里了。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/RxhYNXicIDHkAYXXgDaSJm8iarf2GE4Ao4Nl3tTrvTtctLnUZQb7phfpWmc8emKdFfjrMicicHjlbNNeWNq3utOwpOR4iczmm8gobkoYyweqMnEk/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1) ![image](https://mmbiz.qpic.cn/sz_mmbiz_png/RxhYNXicIDHlibsfftCeTrdBPxicyPw5wmA56ib0X0onndiabIh3H7uPwT670iaKylFK1TPMpovUkLpvicIKPXTGLsNHY2Aib0icuzE1rLJiaHmCYSHY0/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

不只是我有这个感受。一个日本的 n8n 博主分享了类似的经历，他用日语给 Claude Code 下指令，30 分钟搭完了一个完整的工作流。他说自己编程经验为零，以前光查 Expression 语法就要几个小时，用了 Claude Code 之后生产力变了 10 倍以上。

---

## 两层自动化叠在一起，效率是指数级的

你可能想：我手动拖节点也挺快的，干嘛多搞一层。

这么想的人，跟当年觉得"我用 Excel 也挺快，干嘛学 Python"的人一样。

差别不在于单次效率差多少，在于 **天花板不一样了** 。

手动拖节点，你一天搭 3-5 个工作流，这基本是上限。

用 Claude Code + n8n MCP，一天可以搭几十个。因为 Skills 文件沉淀了你的经验，AI 搭出来的工作流会越来越懂你的业务，质量越来越高。

这背后是两层自动化叠在一起：

**第一层：n8n 帮你执行任务。** 你搭好工作流，它 7×24 小时跑，定时触发、自动重试、报错有日志。

**第二层：AI 帮你搭建 n8n。** Claude Code 理解你的需求，直接调 n8n API 创建工作流。

两层叠加，效率是指数级的。Cody Schneider 一天做那么多事，不是因为他手速快，是因为他把"搭建工作流"这件事本身也自动化了。

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/RxhYNXicIDHnIcicvpYic0FlAp9D1Tf0TbicD9h6fqhmN0krro9xfhQpbicZugYPCdC1qfCARFkkiaWV1ylZNLH11Ms9LfEs4RZPO1MdDr0PATDbQ/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

你可能会问：那我直接用 Claude Code 不就行了，为什么还要 n8n？

两个原因。

第一，脚本是黑盒，工作流是透明的。脚本也能定时跑，但出了问题你得翻代码排查。n8n 每个节点的输入输出一目了然，报错了打开界面就知道卡在哪里。对企业来说更重要的是：脚本只有写代码的人能维护，n8n 工作流任何人都能看懂，还支持权限管理、版本记录、多人协作。

第二，大量业务操作根本不需要 AI 动脑子。每天早上 8 点抓一次竞品价格、每小时同步一次库存、客户下单后自动发确认邮件——这些是固定流程，每次执行的逻辑一模一样。用 AI 来跑既贵又没必要，n8n 直接执行就好。

**需要动脑子的交给 AI，不需要动脑子的交给 n8n。** 各干各擅长的事。

---

## 落到跨境场景

说点实际的。做跨境的人每天大量时间花在重复性工作上：

- **竞品监控**
	盯几十个竞品店铺的新品、价格、广告变化。现在你可以跟 Claude Code 说"帮我搭一个工作流，每天抓取这 10 个 ASIN 的价格和评价，变动超过 5% 就发飞书通知"，它直接帮你建好。
- **Listing 文案**
	标题、五点描述、A+ 图文，填好关键词和卖点就能批量生成，不用一条一条手写。
- **客户开发**
	Cody 那条冷邮件工作流，放到跨境场景就是——抓取海外展会或行业论坛的参与者 → 查找邮箱 → 验证 → 自动发开发信。 **一条工作流，替代一个 BD 团队的日常。**
- **产品图**
	传统拍一套产品图要两千，AI 批量生图成本不到十分之一。搭一条工作流，填好产品信息就能批量出主图、场景图、白底图。

以前这些工作流你一个一个手动搭，每个折腾半天。现在跟 AI 说清楚需求，很快就能出一个能跑的版本。

---

## 我自己的真实体验

拿上面提到的产品图来说，我之前帮一个做跨境的朋友搭过这样一套工作流。他的痛点很典型：每个月上新 200 多个 SKU，每个品要出主图、场景图、白底图，还要针对不同站点做尺寸适配。以前找摄影师拍一套产品图要 2000 块左右，一个月光拍图就要小几十万。

我用 Claude Code 帮他搭了一套 n8n 工作流：从飞书表格读取产品信息和关键词 → 调 AI 生图接口批量出图 → 自动裁剪成各站点需要的尺寸 → 生成结果回写到飞书表格。

整个工作流的搭建过程，我就是跟 Claude Code 描述需求——要对接哪个生图 API、飞书表格的字段结构是什么、输出尺寸规格是多少。它自己去配 n8n 节点、写数据转换逻辑、调通 API。中间报了几次错，它自己看报错日志自己改，我基本不用动手。

**以前手动搭这种工作流至少要两三天，用 Claude Code 大半天就跑通了。**

![image](https://mmbiz.qpic.cn/mmbiz_png/RxhYNXicIDHnvI1NvBibjx5lA1skjibkJ3SBwqfwNpDxohzhYxtsF3Mtt29Qc8PLbtxeEP7Nmr5ic9Ca64Fvm6kd4zNdA5pGFIAoI7fiaGImwTys/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

关键是成本差距：传统拍摄一套 2000 元，AI 生图一张 5 毛钱不到，即使按 1 块钱算，20 个新品每个品 7-8 张图，一个月总共不到 200 块。成本从小几万直接降到两百以内。工作流搭好之后，运营自己在飞书表格里填好产品信息，点一下就出图，不需要懂任何技术。

而且这不是一次性的。后来我给自己搭公众号封面生成、朋友圈配图，每次都是同样的模式——我说需求，Claude Code 搭，我审核。因为 Skills 文件积累了我的业务上下文（飞书表 ID、API 配置、输出规格），它搭出来的东西越来越贴合实际环境，越搭越快。

**以前一个想法从冒出来到落地，可能折腾一两天。现在半小时就能看到原型。**

---

## 真正值钱的不是工具操作

说实话，这个趋势让我兴奋，同时也有点紧张。

兴奋的是：搭工作流的门槛在大幅降低。以前要懂节点逻辑、API 配置、数据格式转换，入门门槛不低。现在 Claude Code 能帮你处理大部分技术细节， **你只需要说清楚你要什么。**

紧张的是： **"会搭工作流"正在从稀缺能力变成标准配置。**

有个做 AI 自动化教程的博主说了一句话，我觉得很到位：

> "如果你不理解自己要自动化的流程，你只是在规模化混乱。"

同样用 Claude Code 搭工作流，懂业务的人和不懂业务的人，搭出来的东西差距巨大。

你跟 AI 说"帮我搭一个竞品监控"，它能搭出来。但监控哪些指标才有意义？价格变动的阈值设多少？触发通知后下一步该做什么？这些 AI 帮不了你—— **这是你的业务判断。**

工具操作 AI 能学会，业务洞察 AI 学不会。

这也是我一直在说的——工作流思维 > 单点工具。工具会变，今天手动拖节点，明天 AI 帮你搭，后天可能又是新的方式。但你对业务流程的理解，一直值钱。

![image](https://mmbiz.qpic.cn/sz_mmbiz_png/RxhYNXicIDHmicgmucVsmQm6f21edfYys0zTIqvGWvBDP9HlKLlDicPpPzyYdcHlibViaUqmkoTIx7YoFyo6CbT9P9vEXBoUT720SFPd8fOOT4Vc/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)

---

## 写在最后

n8n 没有过时，恰恰相反，它正在迎来第二春。

Claude Code 帮你快速搭建，n8n 帮你稳定运行。两个不是替代关系，是配合关系——一个解决"怎么搭得快"，一个解决"怎么跑得稳"。

以前大家说 n8n 的门槛是"要懂一点技术"。现在 AI 正在把这个门槛大幅拉低。但门槛降低意味着竞争也在变——当所有人都能搭工作流的时候，拼的是谁更懂业务、谁的工作流设计更聪明。

**搭工作流的能力正在被自动化，理解业务的能力不会。**

这才是真正的护城河。

3月中旬开始第五期AI工作流训练营，有兴趣的可以点关注联系我

[》》戳我，跟富百一起学习](https://mp.weixin.qq.com/s?__biz=MzYyNTYyNjk4MQ==&mid=2247483722&idx=1&sn=6cd78fe237064cd950fe4e84e704e5fc&scene=21#wechat_redirect)

我是富百，专注AI工作流，智能体agent搭建。

继续滑动看下一个

富百说

向上滑动看下一个