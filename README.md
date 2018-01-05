# 教你用 Python 来玩微信跳一跳
## 游戏模式

> 2017 年 12 月 28 日下午，微信发布了 6.6.1 版本，加入了「小游戏」功能，并提供了官方 DEMO「跳一跳」。这是一个 2.5D 插画风格的益智游戏，玩家可以通过按压屏幕时间的长短来控制这个「小人」跳跃的距离。分数越高，那么在好友排行榜更加靠前。通过 Python 脚本自动运行，让你轻松霸榜。

![](https://github.com/wangshub/wechat_jump_game/blob/master/resource/image/jump.gif)

可能刚开始上手的时候，因为时间距离之间的关系把握不恰当，只能跳出几个就掉到了台子下面。**如果能利用图像识别精确测量出起始和目标点之间测距离，就可以估计按压的时间来精确跳跃。**

## 原理说明

1. 将手机点击到《跳一跳》小程序界面

2. 用 ADB 工具获取当前手机截图，并用 ADB 将截图 pull 上来
```shell
adb shell screencap -p /sdcard/autojump.png
adb pull /sdcard/autojump.png .
```

3. 计算按压时间
  * 手动版：用 Matplotlib 显示截图，用鼠标先点击起始点位置，然后点击目标位置，计算像素距离；
  * 自动版：靠棋子的颜色来识别棋子，靠底色和方块的色差来识别棋盘；

4. 用 ADB 工具点击屏幕蓄力一跳
```shell
adb shell input swipe x y x y time(ms)
```

## 使用教程

- 方法 1：使用 app 进行一键操作。目前已适配 Win10 64位/macOS 平台 Android 一键操作，下载请移步 [STOP_jump](https://github.com/wangshub/wechat_jump_game/releases)

- 方法 2：相关软件工具安装和使用步骤请参考 [Android 和 iOS 操作步骤](https://github.com/wangshub/wechat_jump_game/wiki/Android-%E5%92%8C-iOS-%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4)

## FAQ

- 详见 [Wiki-FAQ](https://github.com/wangshub/wechat_jump_game/wiki/FAQ)

## 更新日志

- 详见 [changelog](https://github.com/wangshub/wechat_jump_game/blob/master/changelog.md)

## 开发者列表

- 详见 [contributors](https://github.com/wangshub/wechat_jump_game/graphs/contributors)

## QQ 交流

- 314659953 (1000人 已满)
- 176740763 (500人 已满)
- 89213434 (2000人 已满)
- 64389940 (2000人)

## 打包成windows下exe的方法
- 基于https://github.com/wangshub/wechat_jump_game/commit/5576e548b6df671e2aa5536b4a8097d3b255c35b
- 参考了https://github.com/wangshub/wechat_jump_game/releases里MrLevo520的打包成果
0. wechat_jump_auto.py所在目录定义为顶层目录
1. 激活虚拟环境
2. 在虚拟环境 pip install pyinstaller
3. setuptools降版至19.2,因为numpy绑定失败的问题
3. 更改comm/config.py, 因为会找不到路径,在这里5576e548b6df671e2aa5536b4a8097d3b255c35b的config.py被重命名为congig.py.bak,config.py已经被改了
4. 在顶层目录执行, F:\wechat_jump_env\Scripts\pyinstaller.exe为自己的虚拟环境安装的pyinstaller的绝对路径
    F:\wechat_jump_env\Scripts\pyinstaller.exe --clean --win-private-assemblies -F wechat_jump_auto.py -p F:\\wechat_jump_env\\lib\\site-packages
5. 拷贝dist\wechat_jump_auto.exe至 顶层目录
6. 拷贝Tools\adb\目录下的adb.exe, fastboot.exe, AdbWinApi.dll, AdbWinUsbApi.dll到 顶层目录
7. 删除顶层目录下的build，dist目录机及其他不需要的py文件
 
- 自己的打包成功的虚拟环境
(wechat_jump_env) F:\wechat_jump_env\wechat_jump_game>pip list
- DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=- - (legacy|columns) in your pip.conf under the [list] section) to disable this warning.
- altgraph (0.15)
- backports.functools-lru-cache (1.4)
- cycler (0.10.0)
- future (0.16.0)
- macholib (1.9)
- matplotlib (2.1.1)
- numpy (1.13.3)
- olefile (0.44)
- opencv-python (3.4.0.12)
- pefile (2017.11.5)
- Pillow (4.3.0)
- pip (9.0.1)
- PyInstaller (3.3.1)
- pyparsing (2.2.0)
- pypiwin32 (220)
- python-dateutil (2.6.1)
- pytz (2017.3)
- setuptools (19.2)
- six (1.11.0)
- wheel (0.30.0)
