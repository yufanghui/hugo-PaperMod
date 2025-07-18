---
title: "ai制作书籍解读视频初体验"
date: "2025-07-18"
tags: ["ai生成视频"]
---

昨天一个友人发来一个视频，我点进去看了，似乎是ai生成的，统一的15分钟，统一的视频封面，ai口播，一致的图片制作的分镜，ai感觉非常浓厚。而且视频点赞居然还不错。我也想今天试试，来实现一个aidemo自动产出15分钟的讲书视频。

# ai的方案

当然还是询问ai了，最近听说kimi2性能爆表，使用kimi输入我的需求。以下是沟通完毕需求之后，kimi给出的基础版方案。

> 最小可行 MVP（零代码、30 分钟内跑通）
>
> 1. 讲稿 → 15 min 逐段文案
>    工具：直接让 Kimi / 豆包生成
>    Prompt：
>    “把《书名》做成 15 min 讲书视频，拆成 15 段 60 s 左右的口播文案，每段配一句画面描述，用表格输出：序号 | 口播文案 | 画面关键词”
> 2. 图片 → 16:9 插图
>    工具：智谱清言「绘画智能体」或 美图 WHEE 
>    动作：把上一步的“画面关键词”直接贴进去，统一尺寸 1024×576，下载 PNG。
> 3. 图片转动态（平移/缩放）
>    工具：DynamiCrafter（免费在线版）
>    动作：
>    - 上传一张 PNG → 选 “Camera Pan” 或 “Zoom” 模板 → 6-8 s MP4 直接出。
>    - 15 张图并行跑，3 分钟搞定。
> 4. 配音
>    工具：Speechify（网页版免注册）
>    动作：把 15 段文案一次性粘进去 → 选中文女声 → 调语速 1.1x → 一键下载整段 15 min MP3。
> 5. 自动剪辑成片
>    工具：剪映「脚本成片」
>    动作：
>    - 新建「脚本成片」→ 导入 MP3 + 15 段 DynamiCrafter MP4 → 按顺序排好 → 开「智能匹配」→ 自动对齐 → 导出 1080p，2 分钟渲染完成。
>
> 成本 & 时长
> • 0 元，全部用免费额度。
> • 人工操作 ≈ 5 min，AI 跑图+跑视频 ≈ 10 min，剪映导出 ≈ 3 min。
> → 20 分钟一条 15 min 讲书视频，换书名即可复制。

让我看看30分钟能否跑通哈，开始计时。

## 问题1:生成的文案很短

只有两三句，不够60s口播，我想着先不管，先能跑通为主，为文案短点就短点。

![image-20250718093134640](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718093136923.png)

执行第二步，把画面关键词一起输入到智谱清言到ai绘画智能体。

## 问题2:无法批量生成所有画面关键词对应的图片

![image-20250718093252273](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718093254361.png)

## 问题3:生成的图片太过于花里胡哨了

不过这也不重要，内容可以后续再优化。

# 使用现成的coze agent

此时，我突然想到一件事情，就是想到这个任务，应该优先看看有没有现成的。

昨天不是看到一个类似的产出心理学视频的吗？能否借鉴一二，正好人家做成了工作流，而且批量生成图片也好，大段文案也好，似乎工作流遍历操作更加合适。

开干。找到了。

https://pr94v95fnu.feishu.cn/docx/C93zddVNQol6xzxYI2TciRmcn6d

![image-20250718093902754](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718093904753.png)

好，接下来，就让我按照步骤操作一下。

本来打算按照教程尝试一下，结果打开coze就看到有现成的工作流

## 速推AIGC的书单爆款视频生成【高级版】体验

![image-20250718094136468](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718094139792.png)

尝试一下，我的乖乖，不到30s生成完毕

![image-20250718094216666](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718094219665.png)

打开之后发现只是一个任务链接，但是视频还在生成中。

![image-20250718094250613](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718094253782.png)

一两分钟就生成完毕了。不过视频有点短，只有46s

https://www.51aigc.cc/#/video-status/e7188019-4257-4eb9-8932-13ca4a08e23d

大家感受一下。看评论，说是模板基本上全都一样，非常单一。我看了下，确实模板不太行。

发现还有好多类似的agent，如下

![image-20250718095025263](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718095028638.png)

## CodeL的视频工作流｜爆款书单视频体验

再体验一个，codel家的，居然是官方的，提示我额度不足。看demo效果不错，充10块钱试试。

![image-20250718095745535](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718095748032.png)

兄弟们等我效果

不对，不是官方的，还是这个速推AIGC，应该只是接入了火山大模型，按量付费。

![image-20250718100127624](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718100129890.png)

妈的，骗人的，割韭菜的，只有声音没有画面。下载下来是好的，应该只是web端播放有问题

![image-20250718100322379](https://qingyinoteimgs.oss-cn-beijing.aliyuncs.com/20250718100324613.png)

https://video.aiyes.vip/api/get_video/61184b92-c5aa-43bc-8102-c72ab6d2a2ee

文案很好，视频也很好，至少比我这种不会做视频的人做得好，还结合现实痛点，很适合抖音微信短视频传播，一分半钟的视频。但是我觉得很sad，这不就是新时代的电子垃圾吗？

## agent的问题

时间有限，基本上一分钟上下，后续准备看看黄总的工作流的方案，看看能否自定义时长。

然后稍后再测试下先有的agent自定义文案，能否让视频更长一些。

