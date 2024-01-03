---
aliases:
  - 盘点一下最近使用的AI工具
date: 2023-06-15 10:06
tags:
  - Midjourney
  - StableDiffusion
shanghai: ⛅️  🌡️+17°C 🌬️↘19km/h
number headings: auto, first-level 1, max 6, _.1.1
---
# 盘点一下最近折腾过的AI服务&工具

- 绘画类
	- Midjourney
		- 先说结论，V5版本的效果确实不错。不过我不是很喜欢在Discord上使用，总感觉像是一个玩具，拿来做生产力工具还是有点太麻烦了。
		- 我最近比较常用的是用niji这个模型来生成插图，配合最近推出的describes   image 功能还是很方便的。Midjourney生成的插图放在illustrator里转换矢量图片，之后就可以随意修改了。
		- Midjourney V5 生成的写实图片效果很惊人。
		- 根据Twitter上的网友分享一个prompt程序[^1]，可以非常轻松的生成各种高质量的真实照片。现在这个prompt配合describes image 可以说非常👍了。
		- Midjourney缺点：
			- 生成结果随机不可控
				- prompt这种像咒语一样的控制力实在是让人很沮丧。
				- 生成之后图片很难调整细节，只能像扔骰子一样再生成几个变量。我相信任何想把它做为生产力的设计师都不能忍受这种失控感。
			- Discord机器人的交互体验很糟糕。现在的输入体验类似于手抄本的时代。用户需要去其他工具里管理prompt，生成好了之后，再复制黏贴回discard。我只是希望有一个类似于SD的webui操作页面即可。
				- 不过这也恰好证明了那些说未来的UI只需要一个输入框就行了的这种妄想。
				- 似乎在下一个版本Midjourney也计划推出一个WebUI了。
			- 还有就是使用文本来描述图片。这有点削足适履。更自然的方式还是直接用图片来交互。
			- 价格高，相比开源的SD来说还是太贵了。
	- Stable Diffusion
		- 我最先使用的是Stable Diffusion，它相比Midjourney就更像是一个生产力工具，有多个webUI界面[AUTOMATIC1111 ](https://github.com/AUTOMATIC1111/stable-diffusion-webui)和[ComfyUI](https://github.com/comfyanonymous/ComfyUI)、支持多种部署方式、社区开源的模型很多，超多的社区插件尤其是[ControlNet](https://github.com/lllyasviel/ControlNet)插件把这种生成的随机性大幅度降低后，Stable Diffusion才越来越朝着专业工具软件的方向发展了。
		- 我主要是根据社区提供的colab脚本把Stable Diffusion安装在Google driven上，用起来也还是挺方便的，在colab上运行大概是一小时2块钱。
			- 在Stable Diffusion上试着训练了两个人像的lora模型后，感觉很神奇。Stable Diffusion训练loro模型不需要太多的图片，大概20多张就差不多了，训练时间也很快。配合设定好的关键词，最后生成的图片效果已经很接近真实了。
			- Stable Diffusion非常适合在某一个领域内集中训练一个模型来使用，因此想用好Stable Diffusion第一步应该去社区选一个适合的模型。
			- Stable Diffusion里还有一个非常棒的脚本功能，可以根据设定的参数大批量的生成效果图。非常适合需要反复调整参数来研究模型。
		- Stable Diffusion现在的问题主要是下限很低、上限很高。使用门槛也比Midjourney要麻烦不少。
			- 听说新版的Stable Diffusion已经没办法在消费级显卡上部署了。这对开源社区来说打击比较大。
			- 我一直相信这种AIGC的软件最好要能支持个人用户本地部署，完全的在线服务实在有点不让人放心，其实是我们生处的这个网络环境。
- GPT
	- Bing
	- ChatGPT
- 语音转文本
	- 

# Reference
up:: [[Stable Diffusion与Midjourney]]
same:: 

[^1]: https://github.com/jesselau76/GPT-Prompts/tree/main/midjourney-prompt-generator