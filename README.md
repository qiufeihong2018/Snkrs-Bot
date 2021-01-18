# 请阅读！


这是一个Selenium机器人，可以在发布日从Nike Snkrs网站购买指定的运动鞋。
   它不适用于发布日之后（或发布日晚些时候）的运动鞋。
   “请注意，此脚本是在美国网站上编写的，因此其他国家的耐克网站可能会引起问题。”
    这是因为购买页面更改为“购买”按钮重定向到单独的结帐页面的位置（与发布期间的直接购买弹出窗口相对）。
这是一个仅用python编写的命令行脚本。`请在python 3.7上运行。
bin目录中有6个硒驱动程序，用于Linux，MacOS和Winows上的Chrome和Firefox。`需要按照以下说明安装其他操作系统的驱动程序。
我发现适用于MacOS的Firefox驱动程序效果最好。

理想情况下，可以用直接的Nike API请求而不是Selenium代替其中的某些（或全部？）。但是，我发现Nike API并不是很简单。

# 入门
运行机器人需要满足一些条件。首先，您需要安装Python 3.7或更高版本。以下说明向您展示了如何在多个操作系统中执行此操作

接下来，我们提供了适用于MacOS，Linux和Windows的Web驱动程序，但是如果它们不存在，或者您需要比随附的驱动程序更新的内容，则需要按照说明自行下载下面

最后，程序从终端（命令行）运行，所以你应该从终端上运行的Python程序熟悉[这里]((https://realpython.com/run-python-scripts/))

## 下载python

必须是Python版本 `3.7` 或更高版本

MacOS

   * 从Python的官方网站 [here](https://www.python.org/downloads/mac-osx/)
   * 如果您安装了 [brew](https://brew.sh) ，则可以运行 coommand `brew install python3`

Linux

   * 从Python的官方网站 [here](https://www.python.org/downloads/source/)
   * 在系统上使用软件包管理器。对于Ubuntu，此命令是sudo apt install python3-dev

Windows

   * 从Python的官方网站 [here](https://www.python.org/downloads/windows/)
   * 如果您已安装 [Chocolatey package manager](https://chocolatey.org/) ，则可以运行 `choco install python`

您选择的浏览器的Selenium Webdrivers

## 安装网络驱动程序

* 大多数浏览器的驱动器可以在selenium的网站上找到[here](https://www.selenium.dev/documentation/en/getting_started_with_webdriver/browsers/)，但在目前，只有Firefox和Chrome都支持

* 注意：已经存在适用于Chrome和Firefox，适用于MacOS，Linux和Windows的Web驱动程序，如果未手动指定其他Web驱动程序，则将加载这些驱动程序
# 用法

1. 确保已完成上述 `Getting Started` 部分中的所有预安装要求
1. 克隆此存储库的源代码
   1. 如果您已安装git，则可以像`git clone https://github.com/alexschimpf/Snkrs-Bot`
   1. 否则，请下载压缩的源代码并解压缩

1. 导航到项目的代码
   * `cd path/to/downloaded/project`

1. 通过运行安装所有Python依赖项
  * `pip install -r requirements.txt`

1. 运行 bot
   * 将下面命令中的所有字段替换为所需的选项以及下面列出的任何配置选项
   ```bash
   python3 main.py --username myemail@gmail.com --password abc123 --url <your-shoes-url> --shoe-size 6 --driver-type chrome
   ```

# 配置选项
以下是用于脚本的不同参数的列表和说明：

<b>--username</b>
* Username for login

<b>--password</b>
* Password for login

<b>--url</b>
* 所需鞋子的网址
* 还可以传入size参数 (for example: https://www.nike.com/launch/t/kobe-5-protro-bruce-lee?size=11). 在这种情况下， `--shoe-size` and `--shoe-type` 会被忽略
* 在带有“其他尺寸范围”的版本中（例如同一页面上的童鞋），请勿在URL中传递带有URL的尺寸参数，因为它可能导致意外结果

<b>--shoe-size</b>
* 不言自明

<b>--shoe-type</b>
* Men's (M), Women's (W), Youth (Y) or Child (C)
* 对于特殊版本 (i.e. Air Presto), can pass in XXS, XS, S, M, L or XL. 您不需要传递鞋码

<b>--cvv</b>
* 您存储的信用卡的卡验证值
* 在某些情况下可能不需要（例如，如果您以前使用存储的信用卡购买了发行版）

<b>--shipping-option</b>
* STANDARD, TWO_DAY or NEXT_DAY

<b>--送货地址</b>
* 如果给出的话，机器人会在某些情况下尝试添加新的收货地址
* 在某些情况下，如果不添加新的收货地址，则无法进行结帐。如果不确定，请包括在内
* 必须采用以下格式：'{"first_name":"John", "last_name":"Doe", "address":"1313 Mockingbird Lane", "apt":"", "city":"Long Beach", "state":"CA", "zip_code":"90712", "phone_number":"9999999999"}'

<b>--login-time</b>
* 如果给出，则机器人会暂停直到登录之前的特定时间（可以是任何日期时间格式）

<b>--release-time</b>
* 如果给出，则机器人会暂停直到购买运动鞋之前的特定时间（可以是任何日期时间格式）

<b>--screenshot-path</b>
* 如果提供，则漫游器将在购买后拍摄页面的屏幕截图并将其保存在给定的文件路径中（可能对调试有用）

<b>--html-path</b>
* 如果提供，则漫游器将在购买后获取页面源并将其保存在给定的文件路径中（可能对调试有用）

<b>--page-load-timeout</b>
* 这用于限制页面加载时间（以秒为单位），这在页面仍加载时很有用，但是UI仍然可用。因为我已经注意到耐克的页面一直挂着，所以这几乎是必须的。我建议为此使用1-3秒。

<b>--驱动程序类型</b>
* 应该是“ firefox”或“ chrome”（将为您确定操作系统）
* 默认为Firefox如果未指定任何内容

<b>--webdriver-path</b>
* 如果指定，将使用指定的驱动程序代替默认驱动程序
* 注意：驱动程序应与 `--driver-type` 选项中指定的浏览器匹配（默认为Firefox）

<b>--headless</b>
这将以headless模式运行驱动程序，这将使bot更快

<b>--select-payment</b>
* 如果您的耐克帐户中已经预先保存了付款方式，请不要使用此选项。如果由于某种原因您没有对其进行预先保存（即使这会花费更多时间给机器人，则机器人会选择找到的第一个付款方式）。

<b>--purchase</b>
* 如果给出此参数，机器人将尝试购买鞋子，因此请谨慎使用！

<b>--num-retries</b>
如果bot由于某种原因失败，它将重试任意次或直到成功

<b>--dont-quit</b>
防止浏览器关闭。请注意，如果您要传递 `--purchase` 参数，则可能有必要在
