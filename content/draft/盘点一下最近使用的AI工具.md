---
draft: true
aliases:
  - 盘点一下最近折腾过的 AI 服务&工具
  - 盘点一下最近折腾过的AI服务&工具
date: 2023-06-15 10:06:00
tags:
  - draft
shanghai: ⛅️  🌡️+17°C 🌬️↘19km/h
number headings: auto, first-level 1, max 6, _.1.1
title: 盘点一下最近使用的AI工具
date modified: 2024-01-04 10:53:35
---

# 盘点一下最近折腾过的 AI 服务&工具

- 绘画类
	- Midjourney
		- 先说结论，V5 版本的效果确实不错。不过我不是很喜欢在 Discord 上使用，总感觉像是一个玩具，拿来做生产力工具还是有点太麻烦了。
		- 我最近比较常用的是用 niji 这个模型来生成插图，配合最近推出的 describes   image 功能还是很方便的。Midjourney 生成的插图放在 illustrator 里转换矢量图片，之后就可以随意修改了。
		- Midjourney V5 生成的写实图片效果很惊人。
		- 根据 Twitter 上的网友分享一个 prompt 程序 [^1]，可以非常轻松的生成各种高质量的真实照片。现在这个 prompt 配合 describes image 可以说非常👍了。
		- Midjourney 缺点：
			- 生成结果随机不可控
				- prompt 这种像咒语一样的控制力实在是让人很沮丧。
				- 生成之后图片很难调整细节，只能像扔骰子一样再生成几个变量。我相信任何想把它做为生产力的设计师都不能忍受这种失控感。
			- Discord 机器人的交互体验很糟糕。现在的输入体验类似于手抄本的时代。用户需要去其他工具里管理 prompt，生成好了之后，再复制黏贴回 discard。我只是希望有一个类似于 SD 的 webui 操作页面即可。
				- 不过这也恰好证明了那些说未来的 UI 只需要一个输入框就行了的这种妄想。
				- 似乎在下一个版本 Midjourney 也计划推出一个 WebUI 了。
			- 还有就是使用文本来描述图片。这有点削足适履。更自然的方式还是直接用图片来交互。
			- 价格高，相比开源的 SD 来说还是太贵了。
	- Stable Diffusion
		- 我最先使用的是 Stable Diffusion，它相比 Midjourney 就更像是一个生产力工具，有多个 webUI 界面 [AUTOMATIC1111 ](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 和 [ComfyUI](https://github.com/comfyanonymous/ComfyUI)、支持多种部署方式、社区开源的模型很多，超多的社区插件尤其是 [ControlNet](https://github.com/lllyasviel/ControlNet) 插件把这种生成的随机性大幅度降低后，Stable Diffusion 才越来越朝着专业工具软件的方向发展了。
		- 我主要是根据社区提供的 colab 脚本把 Stable Diffusion 安装在 Google driven 上，用起来也还是挺方便的，在 colab 上运行大概是一小时 2 块钱。
			- 在 Stable Diffusion 上试着训练了两个人像的 lora 模型后，感觉很神奇。Stable Diffusion 训练 loro 模型不需要太多的图片，大概 20 多张就差不多了，训练时间也很快。配合设定好的关键词，最后生成的图片效果已经很接近真实了。
			- Stable Diffusion 非常适合在某一个领域内集中训练一个模型来使用，因此想用好 Stable Diffusion 第一步应该去社区选一个适合的模型。
			- Stable Diffusion 里还有一个非常棒的脚本功能，可以根据设定的参数大批量的生成效果图。非常适合需要反复调整参数来研究模型。
		- Stable Diffusion 现在的问题主要是下限很低、上限很高。使用门槛也比 Midjourney 要麻烦不少。
			- 听说新版的 Stable Diffusion 已经没办法在消费级显卡上部署了。这对开源社区来说打击比较大。
			- 我一直相信这种 AIGC 的软件最好要能支持个人用户本地部署，完全的在线服务实在有点不让人放心，其实是我们生处的这个网络环境。
- GPT
	- Bing
	- ChatGPT
- 语音转文本
	-

# Reference

up:: [[Stable Diffusion与Midjourney]]
same::

[^1]: https://github.com/jesselau76/GPT-Prompts/tree/main/midjourney-prompt-generator