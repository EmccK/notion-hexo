---
updated: '2025-01-07T13:47:00.000Z'
date: '2024-06-03T15:18:00.000Z'
categories: Mac
urlname: mac-first-step
tags:
  - Mac
title: Mac配置流程
cover: 'https://cn.bing.com/th?id=OHR.CuxhavenTower_ZH-CN5580118944_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# 常用命令


## 让Docker栏自动显示和隐藏的更顺滑


在终端执行以下命令行


**❗前提条件：**

1. 已经关闭自动显示隐藏Docker栏
2. 已经关闭缩放

```shell
defaults write com.apple.Dock autohide-delay -float 0 && killall Dock
```


执行完之后，先打开缩放，再打开自动显示和隐藏Docker栏


**恢复原来的样子**


```shell
defaults delete com.apple.dock; killall Doc
```


## 安装HomeBrew


安装`HomeBrew`之前需要先安装`git`


在终端输入`git`即可，使用苹果`xcode`安装`git`


然后执行下面的命令即可安装`HomeBrew`，


```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```


如果遇到下面的错误，可以修改网络的`DNS`，添加`8.8.8.8`


```text
curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 3 ms: Couldn't connect to server
```


## 安装oh-my-zsh


### 安装


```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


### 安装zsh-autosuggestions插件


```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```


### 安装zsh-syntax-highlighting插件


```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```


最后修改配置文件：`.zshrc`文件，找到下面的一行，添加上上面的插件


```shell
plugins=( [plugins...] zsh-autosuggestions zsh-syntax-highlighting)
```


## 安装常用字体


```shell
brew install --cask font-fira-code
brew install --cask font-lxgw-wenkai
```


# 常用软件


## 使用Brew安装的


先安装`warp`终端软件，然后后面的命令都在`warp`中执行


### Warp: 终端软件


```shell
brew install --cask warp
```


安装完`warp`之后，可以一次性安装以下所有的软件，可以自己按需安装


```shell
brew install --cask warp notion microsoft-edge visual-studio-code mos monitorcontrol betterandbetter postman orbstack ollama motrix
```


### Notion


```shell
brew install --cask notion
```


### Microsoft Edge


```shell
brew install --cask microsoft-edge
```


### VS Code


```shell
brew install --cask visual-studio-code
```


### Mos: 在Mac上更好的使用鼠标


```shell
brew install --cask mos
```


### Snipaste: Mac截屏工具


```shell
brew install --cask snipaste
```


### IINA: 视频播放软件


```shell
brew install --cask iina
```


### MonitorControl: 控制显示器亮度软件


```shell
brew install --cask monitorcontrol
```


### BetterAndBetter: 鼠标和键盘控制


```shell
brew install --cask betterandbetter
```


### Postman: 网络请求软件


```shell
brew install --cask postman
```


### OrbStack: Mac上的docker管理工具


```shell
brew install --cask orbstack
```


### Ollama: 本地运行大模型软件


```shell
brew install --cask ollama
```


### Motrix: Aria2下载文件


```shell
brew install --cask motrix
```


### Topit: Mac置顶软件


```sql
brew install lihaoyun6/tap/topit
```


## AppStore常用软件

- **`QQ`**：可下可不下，现在几乎不用了
- **`QQ音乐`**：听音乐软件
- **`微信`**：聊天工具，必备
- **`Hidden Bar`**：隐藏状态栏图标
- **`SafeInCloud`**：密码管理工具
- **`Magnet`**：让Mac可以像Windows一样分屏
- **`Paste`**：记录历史剪切板工具
- **`Thor`**：快捷键启动
- **`The Unarchiver`**：解压缩工具
- **`Bob`**：划词翻译工具
- **`RunCat`**：状态栏显示小猫
