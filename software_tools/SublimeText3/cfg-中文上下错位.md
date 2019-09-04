最后使用文泉驿微米黑等宽字体解决sublime 3143版本上述字体错位, 空格缩小的问题, 步骤如下:
1.从ubuntu apt安装源安装文泉驿微米黑字体:
```
sudo apt-get install ttf-wqy-microhei
```
2.等待安装完成后, 在sublime的Preferences->settings配置文件中加入文泉驿微米黑等宽字体:
```
"font_face": "WenQuanYi Micro Hei Mono",
```