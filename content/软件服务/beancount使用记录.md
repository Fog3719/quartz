---
draft: false
aliases:
  - Beancount 使用问题记录
  - beancount
number headings: auto, first-level 1, max 6, _.1.1
created: 2023-12-01 08:52
tags:
  - Software
shanghai: ☀️ 🌡️+4°C 🌬️↘22km/h
date: 2023-12-01 08:52:00
date modified: 2024-01-04 11:47:33
id: 20231201085304-64470873-0197-40b4-a223-85d062d72059
up: "[[🖥️ 数字生活 💽]]"
---

## 1 为什么使用 beancount 记账？

### 1.1 其他软件不能满足需求

一开始我也尝试了一些其他的软件比如 [MoneyManager Ex -](https://moneymanagerex.org/)，再尝试了几天之后，我发现他再记录账户之间的转账和支出时比较麻烦。一笔转账要分别去两个账户记录一次。

再后来我就看到了复式记账这个方式，感觉更符合我的需求。一开始选择的复式记账软件也不是 beancount，而是 [Free Accounting Software | GnuCash](https://www.gnucash.org/)。
![Screenshot2024001004011023028](https://pic.237484.xyz/uPic/Screenshot2024001004011023028.png)
他的软件 UI 让我有点时光穿梭的感觉，用了很短的时间我就放弃了。软件的 UI 交互逻辑都很难以理解。

### 1.2 数据格式不通用

每一个记账软件都用了不同的数据格式，在导入外部数据时，只有 [MoneyManager Ex -](https://moneymanagerex.org/) 还算比较好用。
尤其是在批量修改记录时非常不方便。

## 2 账户格式问题

beancount 账户格式要求二级账户必须大写英文字母开头，至于英文字母后面的字符其实是没有限制的。最末级的账户是没有限制的完全可以写中文账户。

我不建议用中文账户名称，因为在 VSCode 中中文字符无法自动填充。

## 3 Beancount 如何处理尾差

在权益账户中增加一个 Rounding 账户，在购买基金、股票时如果有尾差，就把尾差并入到这个科目中，以便保持账户之间的平衡。

## 4 如何处理显示精度？

不知道，在网上看到一种说法是在输入时保持需要的小数点精度，也有说法是直接使用 custom 指令来指定具体的商品精度。我感觉没啥用。在官方的文档中也没有找到特别靠谱的说法。
~~在某一次启动之后，显示了对应的账户的盈余数据，但也仅此一次。再次启动的时候就看不到了。又恢复到了 2 位小数。~~

> [!tip] 2023-12-04 11:07 更新
> 调整输入的小数位数是有效果的，但是也没有能把收益直接体现在资产负债表上。

> [!tip] 2024-01-03 12:26 更新
> 其实是我没有设置好，在 fava 的右上角的下拉选择中选为 `市价`，就可以显示收益值。

## 5 如何记录周期账单🧾？

~~有一个周期账单的插件，但是其实并不好用。~~因为他是一条规则，只会在 fava 中显示一批虚拟的交易记录，在实际的账户记录上是没有的。但也会立即计入资产负债表中。

对于这种记录，如果临时调整了账单的周期，之前的记录就会出现问题。比如分期付款了 12 期，最后 3 期一次性付完了。就需要去调整之前设置周期账单规则。

> [!tip] 2023-12-14 16:16
> 我发现这个插件用来计算利息和分期付款的账单还是很不错的。

他的语法示例是这样的。

```lisp
2023-12-29 # "借款利息 [DAILY UNTIL 2024-01-10]"
	Expenses:Interest:XXXX (10000 * 0.0003) CNY
	Liabilities:CreditCard:XXXX
```

## 6 如何设置预算？

fava 有一个预算设置命令，在帮助文档中有详细的说明。比较简单。

```lisp
2024-01-01 custom "budget" Expenses:HouseholdBills:Internet "yearly" 1200.00 CNY ;宽带预算1年1200元

2024-01-01 custom "budget" Expenses:Car:CommuteParking "monthly" 300.00 CNY ;通勤停车位 每个月300元

2024-01-01 custom "budget" Expenses:Car:Charging "monthly" 300.00 CNY ;每个月汽车充电费300元

2024-01-01 custom "budget" Expenses:Car:TemporaryParking "monthly" 100.00 CNY ; 每个月临时停车费 100

2024-01-01 custom "budget" Expenses:Personal:Clothing "monthly" 50.00 CNY ; 每个月服装费 50

2024-01-01 custom "budget" Expenses:Personal:Haircut "monthly" 50.00 CNY ;每个月理发 50

2024-01-01 custom "budget" Expenses:Personal:Coffice "quarterly" 400.00 CNY ;每3个月咖啡豆 

2024-01-01 custom "budget" Expenses:HouseholdBills:Property "yearly" 3124.00 CNY ;物业费
```

## 7 信封式预算插件

> [!tip] 2024-01-01 11:00
> 信封式预算，不太好用。我有点理解不了这个预算逻辑。

[polarmutex/fava-envelope: A beancount fava extension to add a envelope budgeting capability (github.com)](https://github.com/polarmutex/fava-envelope)

安装命令 `pip install fava-envelope`

## 8 如何记录购物退款？

原路退回即可。

## 9 如何关联其他文件

使用 include 命令可以关联其他文件，但是在表示相对路径时，需要注意要使用 `../子文件夹/XXX.beancount` 这种语法来表示。

如果要关联一个特定格式的账本文件，比如这样的

```
2023-01.beancount 
2023-02.beancount 
……
2023-12.beancount 
```

则可以使用更简洁的方法关联 `include "2023-*.beancount"`

## 10 如何同步数据？

我是用 GitHub 的私人仓库来同步数据，我觉得还是挺方便的。唯一的问题是在移动端不太好记录这些数据。

## 11 如何分类记录账单？

1. 可以使用单独的文件来记录，比如 `2023travel-beijing.beancount`
2. 也可以在日常的账本文件中使用 标签堆叠的方法来记录。[^1] 在 `pushtag` 和 `poptag` 之间的所有交易记录都会自动打上这样的标签。这样的方法用起来比较自由

```lisp
pushtag #berlin-trip-2014 

2014-04-23 * "Flight to Berlin" 
	Expenses:Flights -1230.27 USD 
	Liabilities:CreditCard 
	
poptag #berlin-trip-2014
```

## 12 如何添加购物凭证（发票🧾）？

1. 手动添加凭证的语法 `2013-11-03 document Liabilities:CreditCard "/home/joe/stmts/apr-2014.pdf"`
2. 自动关联，则需要用户按照文档里的规则，创建对应账户的结构和日期命名的规则。嗯 可以使用
3. 在 fava 中打开对应的账户，直接在把凭证文件拖入到 web 页面中，修改一下文件名称就可以自动创建对应的账户文件夹了。👍

## 13 如何记录分担费用 (AA)？

我现在应该是用不到这个插件了，不过如果需要的话，可以安装这个插件试一试。[Akuukis/beancount_share：一个 beancount 插件，用于在一个账本中与外部合作伙伴分担费用。 (github.com)](https://github.com/Akuukis/beancount_share)

## 14 如何抹除对账时的少量🤏差额？

使用 `pad` 命令把需要抹零的账户 直接转到 所有者权益账户。

## 15 如何使用 Fava 的统计页面的 Copy balance directives？

![Screenshot2024001004011007057](https://pic.237484.xyz/uPic/Screenshot2024001004011007057.png)
<center>Copy balance directives </center>

应该在账户开户的命令下增加一个元数据，`fava-uptodate-indication: "True"`，这样才能正常复制 blance 命令。[^2]。

关于这个元数据的使用方法其实在帮助文档中有写，但是当时我看的时候，完全没有意识到这个元数据跟 `Copy balance directives` 按钮有什么关系。

> [!help]+  Up-to-date indicators 最新指标
> Fava offers colored indicators that can help you keep your accounts up-to-date. They are shown next to accounts that have the metadata set on their Open directive. The colors have the following meaning: `fava-uptodate-indication: TRUE`
> Fava 提供了彩色指示器，可以帮助您保持账户的最新状态。它们显示在已设置了 Open 指令元数据的账户旁边。颜色的含义如下： `fava-uptodate-indication: TRUE`
> - green: The last entry for this account is a balance check that passed.
	> 绿色：此账户的最后一笔记录是一次通过的余额查询。
> - red: The last entry is a balance check that failed.
	> 红色：最后一条记录是一次失败的余额检查。
> - yellow: The last entry is not a balance check.
	> 黄色：最后一项不是余额查询。
In addition, a grey dot will be shown if the account has not been updated in a while, as configured by the option.`uptodate-indicator-grey-lookback-days`
此外，如果账户已经有一段时间没有更新，根据选项的配置，将显示一个灰色的点。

文档里这句 "In addition, a grey dot will be shown if the account has not been updated in a while, as configured by the option.`uptodate-indicator-grey-lookback-days` "
可以在主账本中添加一个这样的设置就好了。

> [!note]+
> `2023-12-22 custom "fava-option" "uptodate-indicator-grey-lookback-days" "10"

10 代表的天数。
这样设置完成之后，就可以在 fava 页面中看到每个账户右侧多了一个状态标识。

## 16 如何记录折旧？

我放弃研究折旧了，折旧对于日常生活记账似乎没有实际意义。

## 17 格式化账本

> [!tip] 2024-01-04
> 格式化了一个月的账本之后，感觉并不很好用，尤其是账本中有一些四则运算符的时候，格式化效果很糟糕。

[LaunchPlatform/beancount-black: Opinionated code formatter, just like Python's black code formatter but for Beancount (github.com)](https://github.com/LaunchPlatform/beancount-black)

## 18 其他插件

还没有尝试其他的插件。

[^1]: [Beancount 语言语法 - Beancount 文档](https://beancount.github.io/docs/beancount_language_syntax.html#the-tag-stack)
[^2]: https://github.com/beancount/fava/issues/908#issuecomment-489360641
