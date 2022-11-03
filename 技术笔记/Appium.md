# Appium

### 环境搭建

参考：https://blog.csdn.net/qq_37733396/article/details/120470092

- 环境变量M1电脑版本

  - > open ~/.zshrc
    > open .bash_profile
    >
    > source ~/.zshrc
    > source .bash_profile

 - 安装JDK并设置环境变量

   - https://www.oracle.com/java/technologies/downloads/#jdk19-mac

   - > export JAVA_HOME=/Library/Java/JavaVirtualMachines/{版本}/Contents/Home/
     > export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
     > export PATH=$JAVA_HOME/bin:$PATH:

 - 安装Android SDK并设置环境变量

   - https://developer.android.com/studio

     > export ANDROID_HOME=/Users/{用户名}/Library/Android/sdk
     > export PATH=${PATH}:${ANDROID_HOME}/platform-tools
     > export PATH=${PATH}:${ANDROID_HOME}/tools
     > export PATH=${PATH}:${ANDROID_HOME}/platforms
     > export PATH=${PATH}:${ANDROID_HOME}/build-tools/31.0.3（如果AndroidManager里面没有版本号，就去本地文件夹查看）

 - 安装homebrew

   - > /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

     ```
     # 查看 brew.git 当前源
     $ cd "$(brew --repo)" && git remote -v
     origin    https://github.com/Homebrew/brew.git (fetch)
     origin    https://github.com/Homebrew/brew.git (push)
     
     # 查看 homebrew-core.git 当前源
     $ cd "$(brew --repo homebrew/core)" && git remote -v
     origin    https://github.com/Homebrew/homebrew-core.git (fetch)
     origin    https://github.com/Homebrew/homebrew-core.git (push)
     
     # 修改 brew.git 为阿里源
     $ git -C "$(brew --repo)" remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git
     
     # 修改 homebrew-core.git 为阿里源
     $ git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git
     
     # zsh 替换 brew bintray 镜像
     $ echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc
     $ source ~/.zshrc
     
     # bash 替换 brew bintray 镜像
     $ echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.bash_profile
     $ source ~/.bash_profile
     ```

 - 安装nodejs

   >```coffeescript
   >npm install -g cnpm --registry=https://registry.npm.taobao.org
   >```

 - 安装xcode(直接去app store中下载即可)(没什么用)

 - 安装appium

   - > npm install appium-doctor -g cnpm --registry=https://registry.npm.taobao.org

     > 开始检查，在终端输入：appium-doctor
     >
     > android could NOT be found in /Users/henrydu/Library/Android/sdk!
     >
     > 这个被弃用了，忽略就好，不影响使用

 - 下载appium-desktop.app 和 [appium-inspector](https://github.com/appium/appium-inspector)

   - > [https://github.com/appium/appium-desktop/releases](http://appium.io/)
     >
     > https://github.com/appium/appium-inspector

### appium设置

![image-20221029003007455](/Users/henrydu/Library/Mobile Documents/com~apple~CloudDocs/Documents/note/技术笔记/resources/image-20221029003007455.png)

### ADB获取deviceName、appPackage、appActivity

```
参考：https://www.jianshu.com/p/87ba984ebc3d
参考：https://www.cnblogs.com/iloverain/p/9614262.html
参考：https://blog.csdn.net/hxy199421/article/details/85065809
```

```shell
# 获取设备号
adb devices
# 进入设备终端
adb shell
# 获取appPackage、appActivity
dumpsys activity activities | grep mResumedActivity
# android10 要用上边的命令，网上教程要用findstr，但是不可用所以换回grep
# mResumedActivity: ActivityRecord{c5264e2 u0 com.baidu.baidutranslate/.activity.MainActivity t17}
# 包名：com.baidu.baidutranslate
# 启动类名：.activity.MainActivity
```

### appium-inspector设置

```url
参考：
https://www.jianshu.com/p/a4fe290dfac9
https://blog.csdn.net/mz1997/article/details/115939732
https://blog.csdn.net/qq_31362767/article/details/123180809
https://github.com/appium/appium-desktop/issues/1927
```

> localhost 选这个
>
> /wd/hub 是必须得
>
> 最下脚那个勾要勾上
>
> 最好通过左边的配置自动生成json，直接粘贴json有概率报错

> ```json
> {
>   "platformName": "Android",
> 	"platformVersion": "10",
>     "deviceName": "emulator-5554",
>     "automationName": "appium",
>     "appPackage": "com.baidu.baidutranslate",
>     "appActivity": ".activity.MainActivity"
> }
> ```

![image-20221029003447465](/Users/henrydu/Library/Mobile Documents/com~apple~CloudDocs/Documents/note/技术笔记/resources/image-20221029003447465.png)

### 控制程序

```python
from time import sleep

from appium import webdriver
from appium.webdriver.common.appiumby import AppiumBy
from selenium.webdriver import ActionChains
from selenium.webdriver.common.actions import interaction
from selenium.webdriver.common.actions.action_builder import ActionBuilder
from selenium.webdriver.common.actions.pointer_input import PointerInput

desired_caps = {
    "platformName": "Android",  # 操作系统
    "platformVersion": "10",  # 设备版本号
    "deviceName": "emulator-5554",  # 设备 ID
    "automationName": "appium",
    "appPackage": "com.baidu.baidutranslate",  # app 包名
    "appActivity": ".activity.MainActivity",  # app 启动时主 Activity
    'noReset': True,  # 是否保留 session 信息，可以避免重新登录
    'unicodeKeyboard': True,  # 使用 unicodeKeyboard 的编码方式来发送字符串
    'resetKeyboard': True  # 将键盘给隐藏起来
}


def RunApp(driver):
    try:
        el4 = driver.find_element(by=AppiumBy.ID, value="com.baidu.baidutranslate:id/tab_main_favorite_text")
        el4.click()
        actions = ActionChains(driver)
        actions.w3c_actions = ActionBuilder(driver, mouse=PointerInput(interaction.POINTER_TOUCH, "touch"))
        actions.w3c_actions.pointer_action.move_to_location(724, 2145)
        actions.w3c_actions.pointer_action.pointer_down()
        actions.w3c_actions.pointer_action.move_to_location(750, 1229)
        actions.w3c_actions.pointer_action.release()
        actions.perform()

        el5 = driver.find_element(by=AppiumBy.ID,
                                  value="com.baidu.baidutranslate:id/recommend_plan_reason_text")
        el5.click()

        while 1:
            try:
                el6 = driver.find_element(by=AppiumBy.ID,
                                          value="com.baidu.baidutranslate:id/sentence_edit")
                el6.send_keys("how are you")
                sleep(1)
                el7 = driver.find_element(by=AppiumBy.ID,
                                          value="com.baidu.baidutranslate:id/analysis_button")
                el7.click()
                sleep(1)
                driver.back()
                sleep(1)
            except:
                continue
    except:
        # 关闭程序
        driver.terminate_app('com.baidu.baidutranslate')


if __name__ == '__main__':
    driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
    while 1:
        try:
            RunApp(driver)
        except:
            continue
```

# mitmproxy

> 注意：
>
> mitmproxy包因为使用了pyopenssl库所以不支持m1芯片的Python版本
>
> 需要使用conda创建x86版本的Python以及依赖库
>
> mitmproxy库版本必须在3.9以上，建议使用3.10<=> 3.11
>
> > 创建虚拟Python环境强制使用x86版本：CONDA_SUBDIR=osx-64 conda create -n English-word-collectionx64 python=3.10 mitmproxy

> 参考：
>
> http://events.jianshu.io/p/03c7b78159f5
>
> https://docs.snowflake.com/en/developer-guide/snowpark/python/setup.html#prerequisites
>
> https://www.jianshu.com/p/0b95b3d48b99
>
> https://github.com/pyca/pyopenssl/issues/873#
>
> https://github.com/mitmproxy/mitmproxy/issues/4605
>
> https://stackoverflow.com/questions/64963370/error-cannot-install-in-homebrew-on-arm-processor-in-intel-default-prefix-usr
>
> https://github.com/mitmproxy/mitmproxy/issues/4411

#### python安装

```shell
pip3 install mitmproxy
```

#### 证书安装

> 证书安装：
>
> mac：双击证书，在Mac-钥匙-永久信任
>
> ios：通用-证书-安装；通用-关于本机-底部-信任证书
>
> Android：本地文件安装，部分机型需要在安全-信任证书（未印证）

```url
http://mitm.it/
```

#### 启动

intercept.py  : 过滤规则，支持热更新

--listen-port：代理端口

--web-port：web端端口

```shell
 mitmweb  --listen-port 8081 --web-port 8080 -s intercept.py  
```

#### Python示例：

```python
import mitmproxy.http
from mitmproxy import ctx


class Interceptor:
    def __init__(self):
        ctx.log.info("init")

    def request(self, flow: mitmproxy.http.HTTPFlow):
        ctx.log.info("request() called")

    def response(self, flow: mitmproxy.http.HTTPFlow):
        ctx.log.info("response() called")


addons = [
    Interceptor()
]

'''
mitmweb  --listen-port 8081 --web-port 8080 -s intercept.py  

'''

```

