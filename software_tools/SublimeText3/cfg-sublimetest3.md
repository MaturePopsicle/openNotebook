下载并安装一款对中文支持比较好的字体
    从ubuntu apt安装源安装文泉驿微米黑字体:
        sudo apt-get install ttf-wqy-microhei
    等待安装完成后, 在sublime的Preferences->settings配置文件中加入文泉驿微米黑等宽字体:
        "font_face": "WenQuanYi Micro Hei Mono",

下面是我的配置：

    {
        "caret_style": "phase",
        "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
        "font_face": "WenQuanYi Micro Hei Mono",
        "font_size": 11,
        "highlight_line": true,
        "highlight_modified_tabs": true,
        "ignored_packages":
        [
            "Vintage"
        ],
        "tab_size": 4,
        "translate_tabs_to_spaces": true,
        "update_check": false,
        "word_wrap": true
    }




Ctrl+Shift+P -> install -> 搜索安装包SyncedSidebarBg，自动同步侧边栏底色为编辑窗口底色。
PS：有时改完后侧边栏颜色没变化，不知什么原因，打开包控制，然后列一下已安装包就刷新了。


PS：国内使用SublimeText3，经常可能遇到无法安装可用插件问题，可remove掉Package Control重新安装下；如遇到连Package Control也无法安装，则可以在别处拷贝一份关于Package Control的文件－(Package Control.sublime-package)存放于Installed Packages目录之下即可。

作者：晚晴幽草
链接：http://www.jianshu.com/p/3cb5c6f2421c
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。