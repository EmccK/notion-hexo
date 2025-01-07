---
updated: '2025-01-07T13:45:00.000Z'
date: '2024-12-05T14:29:00.000Z'
categories: 实用教程
urlname: config-mac-rime
tags:
  - 实用教程
  - Mac
  - Windows
title: Rime输入法配置
cover: 'https://cn.bing.com/th?id=OHR.MonoTufa_ZH-CN4998806540_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

## 各平台下载


### Windows


[link_preview](https://github.com/rime/weasel)


### Mac


[link_preview](https://github.com/rime/squirrel)


brew安装输入法


```shell
brew install --cask squirrel
```


brew安装字体包


```shell
brew install --cask font-lxgw-wenkai
```


### IOS


[link_preview](https://github.com/imfuxiao/Hamster)


### Android


[link_preview](https://github.com/osfans/trime)


## 配置


[link_preview](https://github.com/Mintimate/oh-my-rime)


## 配色方案


### 小狼毫-Windows


**`weasel.yaml`**


```yaml
# Weasel settings
# encoding: utf-8

# 感谢 @[Mirtle](https://github.com/mirtlecn) 整理
# Rime 定制指南 <https://github.com/rime/home/wiki/CustomizationGuide#定製指南>
# Weasel 定制文档 <https://github.com/rime/weasel/wiki/Weasel-定製化>
# Weasel 字体设定 <https://github.com/rime/weasel/wiki/字體設定>

# 部分选项需要将 Weasel 更新至最新开发版才能生效
config_version: "2024-03-02"

# [app_options]
# 针对特定应用的设置
app_options:
  firefox.exe:
    inline_preedit: true # 行内显示预编辑区：规避 <https://github.com/rime/weasel/issues/946>

# [global settings]
show_notifications: true                   # 是否显示状态变化的通知：true；false；option_list（方案内的开头 option）
show_notifications_time: 1200              # 通知显示的时间，单位 ms
global_ascii: false                        # 切换为 ascii 模式时，是否影响所有窗口：true；false
# [End of <global settings>]

# [style]
# 字体；候选项、候选窗口的行为、布局及样式
style:
  color_scheme: Emcck             # 默认配色方案
  color_scheme_dark: mint_dark_blue         # 深色模式下，Weasel 的配色方案，Windows 10 1809+ 可用

  # 全局字体
  # 格式：字体1:起始码位:结束码位:字重:字形,字体2……，字体会依次 fallback
  # 详细设定请参考 <https://github.com/rime/weasel/wiki/字體設定>
  font_face: "LXGW WenKai:Bold:7c:7c, Segoe UI Emoji:30:39, Segoe UI Emoji:23:23, Segoe UI Emoji:2a:2a, Segoe UI Emoji:fe0f:fe0f, Segoe UI Emoji:20e3:20e3, Arial:600:6ff, LXGW WenKai:Bold, Segoe UI Emoji, Noto Color Emoji SVG"
  label_font_face: "LXGW WenKai:Bold"       # 标签字体
  comment_font_face: "LXGW WenKai:Bold"     # 注释字体
  font_point: 16                           # 全局字体字号
  label_font_point: 12                     # 标签字体字号，不设定 fallback 到 font_point
  comment_font_point: 14                   # 注释字体字号，不设定 fallback 到 font_point

  inline_preedit: true                     # 行内显示预编辑区：true；false
  preedit_type: composition                # 预编辑区内容：composition（编码）； preview（选中的候选）；preview_all（全部候选）
  
  fullscreen: false                        # 候选窗口全屏显示：true；false
  vertical_text: false                     # 竖排文本：true；false
  text_orientation: horizontal             # 文本排列方向，效果和 `vertical_text` 相同：horizontal；vertical
  candidate_list_layout: linear            # stacked | linear  候选项排列方向（似乎只有在custom内才可以生效）
  vertical_text_left_to_right: false       # 竖排方向是否从左到右：true；false
  vertical_text_with_wrap: false           # 文本竖排模式下，自动换行：true；false
  vertical_auto_reverse: false             # 文本竖排模式下，候选窗口位于光标上方时倒序排列：true；false
  
  label_format: "%s "                      # 标签字符：例如 %s. 效果为 1. 2. 3. ....
  mark_text: "|"                           # 标记字符，显示在选中的候选标签前，需要在配色方案中指定颜色；如该项为空字符串 "" 而配色方案中 hilited_mark_color 非透明色，则显示 Windows 11 输入法风格标记
  ascii_tip_follow_cursor: false           # 切换 ASCII 模式时，提示跟随鼠标，而非输入光标
  enhanced_position: true                  # 无法定位候选框时，在窗口左上角显示候选框：true；false
  display_tray_icon: false                 # 托盘显示独立于语言栏的额外图标：true；false
  antialias_mode: default                  # 次像素反锯齿设定：default；force_dword；cleartype；grayscale；aliased
  candidate_abbreviate_length: 30          # 候选项略写，超过此数字则用省略号代替。设置为 0 则不启用此功能
  mouse_hover_ms: 0                        # 鼠标悬停选词响应时间（ms），设置为 0 时禁用该功能
  paging_on_scroll: true                   # 在候选窗口上滑动滚轮的行为：true（翻页）；false （选中下一个候选）
  click_to_capture: false                  # 鼠标点击候选项，创建截图：true；false

  layout:
    align_type: center                     # 标签、候选文字、注解文字之间的相对对齐方式：top ; center ; bottom
    max_height: 0                          # 候选框最大高度，horizontal 布局如宽超此尺寸则换行显示候选，设置为 0 不启用此功能
    max_width: 0                           # 候选框最大宽度，文本竖排模式下如高度超此尺寸则换列显示候选，设置为 0 不启用此功能
    min_height: 0                          # 候选框最小高度
    min_width: 0                           # 候选框最小宽度
    border_width: 0                        # 边框宽度；又名 border
    margin_x: 40                           # 主体元素和候选框的左右边距；为负值时，不显示候选框
    margin_y: 40                           # 主体元素的上下边距；为负值时，不显示候选框
    spacing: 10                            # inline_preedit 为否时，编码区域和候选区域的间距
    candidate_spacing: 28                  # 候选项之间的间距
    hilite_spacing: 1                      # 候选项和相应标签的间距
    hilite_padding: 20                     # 高亮区域和内部文字的间距，影响高亮区域大小
    # hilite_padding_x: 20                 # 高亮区域和内部文字的左右间距，如无特殊指定则依 hilite_padding 设置
    # hilite_padding_y: 8                  # 高亮区域和内部文字的上下间距，如无特殊指定则依 hilite_padding 设置
    shadow_radius: 16                      # 阴影区域半径，为 0 不显示阴影；需要同时在配色方案中指定非透明的阴影颜色
    shadow_offset_x: 8                     # 阴影左右偏移距离
    shadow_offset_y: 8                     # 阴影上下偏移距离
    corner_radius: 24                      # 候选窗口圆角半径
    round_corner: 12                       # 候选背景色块圆角半径，又名 hilited_corner_radius
    # type: vertical                       # 布局设置，效果和 style 下的设置相同：
                                           # horizontal（横向）；vertical（竖向） ; vertical_text（竖排文本） ; vertical+fullscreen（全屏） ; horizontal+fullscreen（横向全屏）
# [End of <style>]

# [preset_color_schemes]
# 配色设定
# 在小狼毫用户目录新建 preview 文件夹，将自定义皮肤的截图重命名为 color_scheme_<name>.png 放入此文件夹，可以在「输入法设定」中看到自定义皮肤效果

# 小狼毫配色在线设计：
# [RIME 西米](https://fxliang.github.io/RimeSeeMe/)
# [润笔](https://pdog18.github.io/rime-soak/#/theme)

# [小狼毫配色详解](https://github.com/rime/weasel/wiki/定制小狼毫配色)
preset_color_schemes:


  Emcck:
    name: "Emcck"
    author: "Emcck"
    back_color: 16777215
    border_color: 16777215
    shadow_color: 0xCDCDCD
    label_color: 6579300
    hilited_text_color: 0
    hilited_back_color: 13948116
    candidate_text_color: 3815994
    comment_text_color: 10395294
    hilited_candidate_text_color: 16777215
    hilited_comment_text_color: 16777215
    hilited_candidate_back_color: 7778560
    hilited_label_color: 16777215

  # 以下是一个配色方案示例
  nord:                                      # 在 `style/color_schema` 指定的配色方案值
    name: "远山／Nord"                       # 方案设置中显示的配色名称
    author: Mirtle                           # 配色作者名称
    color_format: rgba                       # 颜色格式：argb（0xaarrggbb）；rgba（0xrrggbbaa）；abgr（0xaabbggrr 默认）
    # 默认配色
    text_color: 0x2E3440                     # 文字
    shadow_color: 0x000000b4                 # 阴影
    label_color: 0x4C566A                    # 标签
    comment_text_color: 0xD08770             # 注释
    border_color: 0xECEFF4                   # 边框
    back_color: 0xECEFF4                     # 背景
    # 普通候选项配色
    candidate_back_color: 0xECEFF4           # 背景
    # candidate_border_color:                # 边框
    # candidate_shadow_color:                # 阴影
    candidate_text_color: 0x2E3440           # 文字
    # 编码区域配色
    hilited_text_color: 0x000000             # 文字
    hilited_back_color: 0xEBCB8B             # 背景
    # hilited_shadow_color:                  # 阴影
    # 选中的候选区域配色
    hilited_mark_color: 0xBF616A             # 标签前的标记
    hilited_label_color: 0x4C566A            # 标签
    hilited_comment_text_color: 0xBF616A     # 注释
    hilited_candidate_text_color: 0x2E3440   # 文字
    hilited_candidate_border_color: 0x8FBCBB # 边框
    hilited_candidate_back_color: 0x8FBCBB   # 背景
    # hilited_candidate_shadow_color:        # 阴影
    # inline_preedit: false 时翻页箭头颜色，不设置则不显示箭头
    # nextpage_color: 0x000000               # 下一页
    # prevpage_color: 0x000000               # 上一页

  mint_light_blue:
    name: "蓝水鸭／Mint Light Blue"
    author: Mintimate <"Mintimate's Blog">
    # 拼音串
    text_color: 0x6495ed 
    # 背景
    back_color: 0xefefef 
    # 预选栏编号颜色
    label_color: 0xcac9c8 
    # 边框
    border_color: 0xefefef 
    shadow_color: 0xb4000000
    # 注解文字
    comment_text_color: 0xcac9c8 
    # 非第一候选项
    candidate_text_color: 0x424242 
    # 拼音串高亮
    hilited_text_color: 0xed9564 
    # 拼音串高亮背景
    hilited_back_color: 0xefefef 
    # 第一候选项背景
    hilited_candidate_back_color: 0xed9564 
    # 第一候选项
    hilited_candidate_text_color: 0xefefef
    # 第一候选项编号颜色
    hilited_label_color: 0xcac9c8
    # 注解文字高亮
    hilited_comment_text_color: 0xefefef 
    

  mint_dark_blue:
    name: "黑水鸭／Mint Dark Blue"
    author: Mintimate <"Mintimate's Blog">
    # 拼音串
    text_color: 0x6495ed 
    # 背景
    back_color: 0x424242 
    # 预选栏编号颜色
    label_color: 0xefefef 
    # 边框
    border_color: 0x424242 
    shadow_color: 0xb4000000
    # 注解文字
    comment_text_color: 0xefefef 
    # 非第一候选项
    candidate_text_color: 0xefefef
    # 拼音串高亮
    hilited_text_color: 0xc6c01a
    # 拼音串高亮背景
    hilited_back_color: 0x424242
    # 第一候选项背景 
    hilited_candidate_back_color: 0xc6c01a 
    # 第一候选项
    hilited_candidate_text_color: 0xefefef
    # 第一候选项编号颜色
    hilited_label_color: 0xffffff
    # 注解文字高亮
    hilited_comment_text_color: 0xffffff 
# [End of <preset_color_schemes>]

```


### 鼠须管-Mac


**`squirrel.yaml`**


```yaml
# Squirrel settings
# encoding: utf-8
#
# squirrel[.custom].yaml 是鼠须管的前端配置文件，小狼毫是 weasel[.custom].yaml
# 各平台皮肤配置并不一致。
#
# 鼠须管内置皮肤展示： https://github.com/NavisLab/rime-pifu
# 鼠须管界面配置指南： https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/鼠鬚管介面配置指南.md
# 鼠须管作者写的图形化的皮肤设计器： https://github.com/LEOYoon-Tsaw/Squirrel-Designer

# 要比共享目录的同名文件的 config_version 大才可以生效
config_version: '2024-03-02'

# options: last | default | _custom_
# last: the last used latin keyboard layout
# default: US (ABC) keyboard layout
# _custom_: keyboard layout of your choice, e.g. 'com.apple.keylayout.USExtended' or simply 'USExtended'
keyboard_layout: default
# for veteran chord-typist
chord_duration: 0.1  # seconds
# options: always | never | appropriate
show_notifications_when: appropriate

style:
  # 选择皮肤，亮色与暗色主题
  color_scheme: mint_light_blue
  color_scheme_dark: mint_dark_blue
  
  # 预设选项。如果皮肤没写，则使用这些属性；如果皮肤写了，使用皮肤的。
  text_orientation: horizontal  # horizontal | vertical
  candidate_list_layout: linear # stacked | linear  候选项排列方向（似乎只有在custom内才可以生效）
  
  # 内嵌预编辑
  inline_preedit: true
  # 选中框 圆角半径
  hilited_corner_radius: 0
  # 窗口边界高度，大于圆角半径才生效
  border_height: 0
  # 窗口边界宽度，大于圆角半径才生效
  border_width: 0
  # 外边框 圆角半径
  corner_radius: 10
  # 色彩空间： srgb | display_p3
  color_space: srgb
  line_spacing: 5
  spacing: 10
  #candidate_format: '%c. %@'
  #base_offset: 6
  # 全局字体及大小
  font_face: "PingFang SC"
  font_point: 16
  # 序号字体及大小
  label_font_face: "PingFang SC"
  label_font_point: 16
  # 注字体及大小
  comment_font_face: "PingFang SC"
  comment_font_point: 14


preset_color_schemes:
  mint_light_blue:
    name: "蓝水鸭／Mint Light Blue"
    author: Mintimate <"Mintimate's Blog">
    translucency: false                     # 磨砂： false | true
    mutual_exclusive: false                 # 色不叠加： false | true
    shadow_size: 0                       `  # 阴影大小
    line_spacing: 5                         # 行间距
    base_offset: 0                          # 字基高
    alpha: 1                                # 透明度，0~1
    spacing: 10                             # 拼音与候选项之间的距离 （inline_preedit: false）
    back_color: 0xefefef                    # 底色
    hilited_candidate_back_color: 0xed9564  # 选中底色
    label_color: 0xcac9c8                   # 序号颜色
    hilited_candidate_label_color: 0xefefef # 选中序号颜色
    candidate_text_color: 0x424242          # 文字颜色
    hilited_candidate_text_color: 0xefefef  # 选中文字颜色
    comment_text_color: 0xcac9c8            # 注颜色
    hilited_comment_text_color: 0xefefef    # 选中注颜色
    text_color: 0x6495ed                    # 拼音颜色 （inline_preedit: false）
    hilited_text_color: 0xed9564            # 选中拼音颜色 （inline_preedit: false）
    
  mint_dark_blue:
    name: "黑水鸭／Mint Dark Blue"
    author: Mintimate <"Mintimate's Blog">
    translucency: false                     # 磨砂： false | true
    mutual_exclusive: false                 # 色不叠加： false | true
    shadow_size: 0                       `  # 阴影大小
    line_spacing: 5                         # 行间距
    base_offset: 0                          # 字基高
    alpha: 1                                # 透明度，0~1
    spacing: 10                             # 拼音与候选项之间的距离 （inline_preedit: false）
    back_color: 0x424242                    # 底色
    hilited_candidate_back_color: 0xc6c01a  # 选中底色
    label_color: 0xefefef                   # 序号颜色
    hilited_candidate_label_color: 0xefefef # 选中序号颜色
    candidate_text_color: 0xefefef          # 文字颜色
    hilited_candidate_text_color: 0xefefef  # 选中文字颜色
    comment_text_color: 0xefefef            # 注颜色
    hilited_comment_text_color: 0xffffff    # 选中注颜色
    text_color: 0x6495ed                    # 拼音颜色 （inline_preedit: false）
    hilited_text_color: 0xc6c01a            # 选中拼音颜色 （inline_preedit: false）
```


**`squirrel.custom.yaml`**


```yaml
patch:
  show_notifications_when: appropriate     # 状态通知，可设为全开（always）全关（never）  

  # 皮肤主题名称输入在下方，分为浅色和深色
  # 浅色主题
  style/color_scheme: wechat_light
  # 深色主题
  style/color_scheme_dark: wechat_dark

  # 皮肤主题
  preset_color_schemes:
    wechat_light:
      name: 微信键盘浅色
      back_color: 0xFFFFFF                      # 候选条背景色
      border_height: 0                          # 窗口上下高度，大于圆角半径才生效
      border_width: 8                           # 窗口左右宽度，大于圆角半径才生效
      candidate_format: "%c %@ "                # 用 1/6 em 空格 U+2005 来控制编号 %c 和候选词 %@ 前后的空间
      comment_text_color: 0x999999              # 拼音等提示文字颜色
      corner_radius: 5                          # 窗口圆角
      hilited_corner_radius: 5                  # 高亮圆角
      font_face: 'LXGW WenKai'                  # 候选词字体
      font_point: 16                            # 候选字大小
      hilited_candidate_back_color: 0x75B100    # 第一候选项背景色
      hilited_candidate_text_color: 0xFFFFFF    # 第一候选项文字颜色
      label_font_point: 12                      # 候选编号大小
      text_color: 0x424242                      # 拼音行文字颜色
      inline_preedit: true                      # 拼音位于： 候选框 false | 行内 true

    wechat_dark:
      name: 微信键盘深色
      back_color: 0x2e2925                      # 候选条背景色
      border_height: 0                          # 窗口上下高度，大于圆角半径才生效
      border_width: 8                           # 窗口左右宽度，大于圆角半径才生效
      candidate_format: "%c %@ "                # 用 1/6 em 空格 U+2005 来控制编号 %c 和候选词 %@ 前后的空间
      comment_text_color: 0x999999              # 拼音等提示文字颜色
      corner_radius: 5                          # 窗口圆角
      hilited_corner_radius: 5                  # 高亮圆角
      font_face: 'LXGW WenKai'                  # 候选词字体
      font_point: 16                            # 候选字大小
      hilited_candidate_back_color: 0x75B100    # 第一候选项背景色
      hilited_candidate_text_color: 0xFFFFFF    # 第一候选项文字颜色
      label_font_point: 12                      # 候选编号大小
      text_color: 0x424242                      # 拼音行文字颜色
      label_color: 0x999999                     # 预选栏编号颜色
      candidate_text_color: 0xe9e9ea            # 预选项文字颜色
      inline_preedit: true                      # 拼音位于： 候选框 false | 行内 true

    mac_light:
      name: Mac浅色
      candidate_format: "%c %@ "   # 用 1/6 em 空格 U+2005 来控制编号 %c 和候选词 %@ 前后的空间
      corner_radius: 5                             # 窗口圆角
      hilited_corner_radius: 5                     # 高亮圆角
      line_spacing: 10                             # 行间距(适用于竖排)
      border_height: 4                             # 窗口上下高度，大于圆角半径才生效
      border_width: 4                              # 窗口左右宽度，大于圆角半径才生效
      font_face: "PingFangSC"                      # 候选词字体
      font_point: 16                               # 候选字大小
      label_font_point: 13                         # 候选编号大小
      text_color: 0x424242                    # 拼音行文字颜色
      back_color: 0xFFFFFF                    # 候选条背景色
      border_color: 0xFFFFFF                  # 边框色
      label_color: 0x999999                   # 预选栏编号颜色
      candidate_text_color: 0x3c3c3c          # 预选项文字颜色
      comment_text_color: 0x999999            # 拼音等提示文字颜色
      hilited_text_color: 0x999999            # 高亮拼音 (需要开启内嵌编码)
      hilited_back_color: 0xD75A00            # 第一候选项背景背景色
      hilited_candidate_text_color: 0xFFFFFF  # 第一候选项文字颜色
      hilited_candidate_label_color: 0xFFFFFF # 第一候选项编号颜色
      hilited_comment_text_color: 0x999999    # 注解文字高亮

    mac_dark:
      name: Mac深色
      candidate_format: "%c %@ "   # 用 1/6 em 空格 U+2005 来控制编号 %c 和候选词 %@ 前后的空间
      corner_radius: 5                             # 窗口圆角
      hilited_corner_radius: 5                     # 高亮圆角
      line_spacing: 10                              # 行间距(适用于竖排)
      border_height: 4                             # 窗口上下高度，大于圆角半径才生效
      border_width: 4                              # 窗口左右宽度，大于圆角半径才生效 
      font_face: "PingFangSC"                      # 候选词字体
      font_point: 16                               # 候选字大小
      label_font_point: 13                         # 候选编号大小
      text_color: 0x424242                    # 拼音行文字颜色
      back_color: 0x252a2e                    # 候选条背景色
      border_color: 0x050505                  # 边框色
      label_color: 0x999999                   # 预选栏编号颜色
      candidate_text_color: 0xe9e9ea          # 预选项文字颜色
      comment_text_color: 0x999999            # 拼音等提示文字颜色
      hilited_text_color: 0x999999            # 高亮拼音 (需要开启内嵌编码)
      hilited_back_color: 0xD75A00            # 第一候选项背景背景色
      hilited_candidate_text_color: 0xFFFFFF  # 第一候选项文字颜色
      hilited_candidate_label_color: 0xFFFFFF # 第一候选项编号颜色
      hilited_comment_text_color: 0x999999    # 注解文字高亮
  
  # 特定App默认中/英文输入
  app_options:
    com.apple.Spotlight: # 聚焦搜索
      ascii_mode: true             # true默认英文,false默认中文
    com.runningwithcrayons.Alfred: # alfred
      ascii_mode: true
    com.apple.Terminal: # 终端
      ascii_mode: true
    com.microsoft.VSCode: # Visual Studio Code
      ascii_mode: true
      ascii_punct: true            # 中文状态输出英文标点(半角)
    dev.warp.Warp-Stable: # Visual Studio Code
      ascii_mode: true
      ascii_punct: true            # 中文状态输出英文标点(半角)
    com.tencent.Lemon: # 腾讯柠檬
      ascii_mode: true
    com.apple.dt.Xcode: # Xcode
      ascii_mode: true
    com.nektony.App-Cleaner-SII: # App Cleaner & Uninstaller
      ascii_mode: true
    com.xunyong.hapigo: # hapigo
      ascii_mode: true
    com.termius-dmg.mac: # termius
      ascii_mode: true
    com.raycast.macos: # Raycast
      ascii_mode: true
    com.jetbrains.intellij: # idea
      ascii_mode: true
```

