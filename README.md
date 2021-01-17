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

## Installing the web drivers

* The drivers for most browsers can be found on selenium's site [here](https://www.selenium.dev/documentation/en/getting_started_with_webdriver/browsers/), although at the moment, only Firefox and Chrome are supported

* NOTE: There are already webdrivers for Chrome and Firefox, for MacOS, Linux, and Windows, which will be loaded if no other webdriver is specified manually

# Usage

1. Make sure that you have done all the Pre-installation requirements in the `Getting Started` section above

1. Clone this repository's source code
   1. If you have git installed, this can be done as easily as `git clone https://github.com/alexschimpf/Snkrs-Bot`
   1. Otherwise, download the zipped source code and unzip it

1. Navigate to the project's code
   * `cd path/to/downloaded/project`

1. Install all the Python dependencies by running
  * `pip install -r requirements.txt`

1. Run the bot
   * Replace all the fields in the command below with the options that you want, and any of the configuration options listed below
   ```bash
   python3 main.py --username myemail@gmail.com --password abc123 --url <your-shoes-url> --shoe-size 6 --driver-type chrome
   ```

# Configuration options

Here is a list and description of the different arguments to use for the script:

<b>--username</b>
* Username for login

<b>--password</b>
* Password for login

<b>--url</b>
* URL for desired shoe
* Size parameter can also be passed in (for example: https://www.nike.com/launch/t/kobe-5-protro-bruce-lee?size=11). In this case, `--shoe-size` and `--shoe-type` will be ignored
* DO NOT pass in size parameter with url on releases with "Additional Size Ranges" (i.e. children's shoes on same page) as it can lead to unexpected results

<b>--shoe-size</b>
* Self-explanatory

<b>--shoe-type</b>
* Men's (M), Women's (W), Youth (Y) or Child (C)
* For special releases (i.e. Air Presto), can pass in XXS, XS, S, M, L or XL. You do not need to pass in shoe size

<b>--cvv</b>
* Card Verification Value for your stored credit card
* May not be needed in some cases (for example, if you have previously purchased a release with a stored credit card)

<b>--shipping-option</b>
* STANDARD, TWO_DAY or NEXT_DAY

<b>--shipping-address</b>
* If given, the bot will attempt to add a new shipping address in some scenarios
* In some cases, checkout will not proceed without adding a new shipping address. If you are unsure, include it
* Must be in this format: '{"first_name":"John", "last_name":"Doe", "address":"1313 Mockingbird Lane", "apt":"", "city":"Long Beach", "state":"CA", "zip_code":"90712", "phone_number":"9999999999"}'

<b>--login-time</b>
* If given, the bot will pause until a specific time before it logs in (can be any datetime format)

<b>--release-time</b>
* If given, the bot will pause until a specific time before it purchase the sneaker (can be any datetime format)

<b>--screenshot-path</b>
* If given, the bot will take a screenshot of the page after purchasing and save it at the given file path (may be useful for debugging)

<b>--html-path</b>
* If given, the bot will take the page source after purchasing and save it at the given file path (may be useful for debugging)

<b>--page-load-timeout</b>
* This is used to limit the page load time (in seconds), which can be useful when the page is still loading, but the UI is nevertheless useable. This is pretty much a necessity as I've noticed Nike's pages hang all the time. I'd recommend using 1-3 seconds for this.

<b>--driver-type</b>
* Should be 'firefox' or 'chrome' (the OS will be determined for you)
* Defaults to `Firefox` if nothing is specified

<b>--webdriver-path</b>
* If specified, will use the specified driver instead of the defaults
* NOTE: The driver should match the browser specified in the `--driver-type` option (defaults to Firefox)

<b>--headless</b>
* This will run the driver in headless mode, which should make the bot quicker

<b>--select-payment</b>
* If you already have your payment options pre-saved on your Nike account, DO NOT use this. If for some reason you don't have it pre-saved (even though it will cost the bot more time) the bot will select the first payment option it finds.

<b>--purchase</b>
* If this argument is given, the bot WILL attempt to purchase the shoe so USE WITH CAUTION!

<b>--num-retries</b>
* If the bot fails for some reason, it will retry any number of times or until successful

<b>--dont-quit</b>
* Prevent browser from closing. Please note, if you are passing the `--purchase` parameter, it may be necessary to pass this parameter in
