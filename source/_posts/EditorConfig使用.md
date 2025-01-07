---
updated: '2025-01-07T13:46:00.000Z'
date: '2024-06-16T07:00:00.000Z'
categories: Android
urlname: how-to-use-editor-config
tags:
  - Android
title: EditorConfig使用
cover: 'https://cn.bing.com/th?id=OHR.NazareWave_ZH-CN4575182192_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

使用方法，一般是在项目的根目录，创建一个`.editorconfig` 文件


## Compose项目常用的配置


```toml
# noinspection EditorConfigKeyCorrectness

[*.{kt,kts}]
# 参数列表或者列表尾部可以添加,
ij_kotlin_allow_trailing_comma=true
# 参数列表或者列表尾部可以添加,
ij_kotlin_allow_trailing_comma_on_call_site=true
# 忽略Composable和Test注解的方法的大小写判断
ktlint_function_naming_ignore_when_annotated_with = Composable, Test
```

