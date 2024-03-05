#### 媒体查询
 
 >媒体查询是响应式 Web 设计的关键部分，因为它允许你按照视口的尺寸创建不同的布局，不过它也可以用来探测和你的站点运行的环境相关联的其他条件，比如用户是在使用触摸屏还是鼠标。

 ```css
    @media media-type and (media-feature-rule) {
    /* CSS rules go here */
    }

 ```

 它由以下部分组成：

- 一个媒体类型，告诉浏览器这段代码是用在什么类型的媒体上的（例如印刷品或者屏幕）媒体类型是可选的，如果没有指定媒体查询类型，那么媒体查询默认会设为用于全部媒体类型；
- 一个媒体表达式，是一个被包含的 CSS 生效所需的规则或者测试
- 一组 CSS 规则，会在测试通过且媒体类型正确的时候应用。

你可以指定的媒体类型为：
- all 适用于所有设备。
- print 主要用于打印机和打印预览模式。
- screen 主要用于电脑屏幕、平板、智能手机等。
- speech 适用于基于语音识别的设备。

你可以指定的媒体规则为：
- width and height  最大，最小 宽度和高度
- orientation 描述设备的方向
  - portrait（竖屏）
  - landscape（横屏）
- device-width and device-height 这两个特性用于描述设备的物理尺寸
- resolution 描述设备的分辨率(value-eg:300dpi)
- aspect-ratio and device-aspect-ratio 前者描述的是显示区域的宽高比，后者描述设备物理屏幕的宽高比(value-eg:16/9)
##### 混合规则

- 与
  ```css
    @media screen and (min-width: 400px) and (orientation: landscape) {
        body {
            color: blue;
        }
    }
  ```

- 或
   ```css
    @media screen and (min-width: 400px), screen and (orientation: landscape) {
        body {
            color: blue;
        }
    }
  ```

- 非
  ```css
    @media not all and (orientation: landscape) {
        body {
                color: blue;
            }
    }
  ```

- only
  ```css
    @media only screen and (min-width: 600px) {
        .sidebar {
            display: block;
        }
    }
    可以用来隐藏样式表 ，不会被旧的浏览器应用。这是因为老的浏览器不支持媒体查询，它们会忽略only关键字和后面的所有表达，而新的浏览器会把它作为普通的媒体查询来处理。
```
