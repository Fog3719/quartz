---
tags: 
draft: false
date: 2024-01-03 11:01:08
enableToc: true
published: "false"
up: "[[🖥️ Cyber Garden 🏝️]]"
updated: 2024-01-05 10:28:02
number headings: auto, first-level 1, max 6, _.1.1
---

## 1 如何在页面上增加最后修改时间？

首先需要保证在 frontmatter 中包含 `lastmod`、`updated`、`last-modified` 这些字段中的任意一个即可。日期格式似乎没有很严格，我常用的 `yyyy-mm-dd hh:mm:ss` 可以正常识别出来。

第二步很关键，需要在 `quartz/components/ContentMeta.tsx` 中增加一段代码。

```ts
      if (fileData.dates && fileData.dates.modified) {
        segments.push(`Last modified: ${formatDate(fileData.dates.modified)}`)
      }
```

```ts {11-13}
export default (() => {
  function ContentMetadata({ cfg, fileData, displayClass }: QuartzComponentProps) {
    const text = fileData.text
    if (text) {
      const segments: string[] = []
      const { text: timeTaken, words: _words } = readingTime(text)

      if (fileData.dates) {
        segments.push(formatDate(getDate(cfg, fileData)!))
      }
      if (fileData.dates && fileData.dates.modified) {
        segments.push(`Last modified: ${formatDate(fileData.dates.modified)}`)
      }

      segments.push(timeTaken)
      return <p class={`content-meta ${displayClass ?? ""}`}>{segments.join(", ")}</p>
    } else {
      return null
    }
  }
```

这样就可以在页面上把最后修改时间展示出来了。
![[Pasted image 20240105102653.png]]

## 2 如何修改页面默认的明暗 UI？

![[Screenshot2024001005009016054.png]]

## 3 无语的页面样式

我花了很长的时间在研究页面布局的问题。我按照官方文档的说明修改了 layout 文件的布局设置，但是无论我怎么刷新页面，对应的页面布局都没有发生变化。

这就让我困惑了很久都不明白为什么，直到我看到有用户是可以正常把资源管理器组件展示出来，我才想到是否可能是屏幕尺寸的问题。我把窗口放大之后，才看到了桌面下的正常设置。

之后我发现官方默认的 css 样式，实在是无语。<=1510 左右就会转换成移动端的样式。这个样式设置真的太无语了，在 MacBook 14（宽度正好是 1504） 看上去就很怪异。

![Screenshot2024001003014018052](https://pic.237484.xyz/uPic/Screenshot2024001003014018052.png)

![Screenshot2024001003014019002](https://pic.237484.xyz/uPic/Screenshot2024001003014019002.png)

期间我也发现这个问题不止困扰我一个人，有人已经提过解决方案了。但是一直还没有得到回复。

最后我还是直接去改样式表了，把页面宽度粗暴的改为 1200px 了。一切恢复正常了。

```scss
// styles/variables.scss
$fullPageWidth: 1200px; 
```

## 4 语焉不详的文件结构

官方文档对于文件结构的说明一直语焉不详，官方的 demo 里也没有对应的文件管理器。这对于普通用户来说实在太难用了。我一直不明白为什么官方需要在根目录下设置一个 `index.md` 文件。

文档里应该给一个对应的文件结构示例。要不然真的是看不懂啊。
