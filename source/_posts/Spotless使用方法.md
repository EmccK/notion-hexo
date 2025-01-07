---
updated: '2025-01-07T13:47:00.000Z'
date: '2024-06-09T10:29:00.000Z'
categories: Android
urlname: spotless-usage
tags:
  - Android
title: Spotless使用方法
cover: 'https://cn.bing.com/th?id=OHR.HummingThistle_ZH-CN5057539905_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

# **Spotless 是什么？**


Spotless是一款高效的代码格式化工具。它可以帮助开发者保持代码的整洁和一致性，提高代码的可读性和易维护性。


它支持多种编程语言，包括Java、Kotlin、JavaScript等，并提供了丰富的配置选项，可以根据开发者的需求定制代码格式化规则。


# 为什么要用Spotless?


使用Spotless的原因很多。首先，它可以帮助您维持一致的代码风格，使团队成员更容易阅读和理解代码。其次，它可以自动修复许多常见的代码格式问题，提高了开发效率。


# 项目地址


[link_preview](https://github.com/diffplug/spotless)


# 使用方法


## 添加插件


Gradle官网


[bookmark](https://plugins.gradle.org/plugin/com.diffplug.spotless)


我现在使用的都是`VersionCatalog`+`KTS`了，暂时只介绍`VersionCatalog` +`KTS` 的方式了

1. 在Toml文件中添加插件声明

```toml
[versions]

...

[libraries]

...

[plugins]
spotless = { id = "com.diffplug.spotless", version = "6.25.0" }


```

1. 在工程的`build.gradle.kts`中添加

```kotlin
plugins {
		// 添加Spotless插件
    alias(libs.plugins.spotless) apply false
}

```

1. 在模块的`build.gradle.kts`中添加，以及配置`spotless`

```kotlin
plugins {
    alias(libs.plugins.spotless)
}

...

// 配置spotless
spotless {
    val latestKtlintVersion = "1.3.0"
    java {
        target("**/*.java")
        googleJavaFormat()
    }
    kotlin {
        target("**/*.kt", "**/*.kts")
        targetExclude("**/build/**/*.kt", "**/build/**/*.kts")
        ktlint(latestKtlintVersion)
    }
    format("xml") {
        target("**/*.xml")
        targetExclude("**/build/**/*.xml")
    }
}

```


## 使用


使用起来也非常简单，主要就两条命令


### 检查校验代码风格


在项目根目录下执行


```shell
./gradlew spotlessCheck

```


执行完之后，如果有问题会报错并列出异常代码的位置


### 自动修复代码风格


在项目根目录下执行


```shell
./gradlew spotlessApply

```


执行完之后，会自动更正代码风格有问题的地方


# 使用Git hooks自动格式化代码

1. 在项目目录添加`.hooks`目录，并添加`pre-commit`文件，内容如下所示

```shell
#!/bin/bash
# 脚本说明
# 1. 检查改动的文件是否包含 Java、XML 或 Kotlin 文件
# 2. 如果包含，使用 Spotless 检查代码格式
# 3. 如果发现代码格式问题，尝试自动修复
# 4. 如果自动修复成功，将修改后的代码添加到暂存区
# 5. 如果自动修复失败，不允许提交代码

# 获取即将提交的文件列表
FILES=$(git diff --cached --name-only --diff-filter=ACMR)

# 检查文件列表中是否包含 Java、XML 或 Kotlin 文件
if echo "$FILES" | grep -E '\.(java|xml|kt|kts)$'; then
    echo "检测到 Java/XML/Kotlin 文件，执行 Spotless 检查..."
    # 使用 Spotless 检查代码格式
    ./gradlew spotlessCheck

    # 检查 spotlessCheck 命令是否成功执行
    if [ $? -ne 0 ]; then
        echo "发现代码格式问题，正在尝试自动修复..."
        # 运行 Spotless 应用格式化
        ./gradlew spotlessApply

        # 添加所有修改过的文件到暂存区
        git add -A

        # 完成自动修复后重新提交
        echo "格式化后的代码已重新添加到暂存区。请重新执行 git commit 完成提交。"
        exit 1
    fi
else
    echo "未检测到 Java/XML/Kotlin 文件，跳过 Spotless 检查。"
fi

exit 0
```

1. 在项目级的`build.gradle.kts`中添加一下`copyHooks`的任务，把钩子文件复制到`.git/hooks`里面去

```kotlin
//  build.gradle.kts

tasks.register<Copy>("copyHooks") {
    // 设置任务的描述
    description = "将.hooks目录中的钩子复制到.git/hooks目录，并设置可执行权限。"

    // 获取项目根目录路径
    val projectRoot = project.rootDir

    // 确定 .hooks 目录和 .git/hooks 目录的位置
    val hooksDir = File(projectRoot, ".hooks")
    val gitHooksDir = File(projectRoot, ".git/hooks")

    // 确保 .git/hooks 目录存在
    if (!gitHooksDir.exists()) {
        gitHooksDir.mkdirs()
    }

    // 检查 .hooks 目录是否存在并且包含文件
    if (!hooksDir.exists() || hooksDir.listFiles()?.isEmpty() != false) {
        throw GradleException(".hooks directory does not exist or is empty")
    }

    // 配置复制任务的源和目标
    from(hooksDir)
    into(gitHooksDir)

    doLast {
        hooksDir.listFiles()?.forEach { file ->
            if (file.isFile) {
                file.setExecutable(true, false)
                file.setReadable(true, false)
                file.setWritable(true, true)
            }
        }
        gitHooksDir.listFiles()?.forEach { file ->
            if (file.isFile) {
                file.setExecutable(true, false)
                file.setReadable(true, false)
                file.setWritable(true, true)
            }
        }
    }
}

```

1. 双击Ctrl键，执行`gradle copyHooks` 即可，以后每一次提交代码的时候，会自动检查代码风格，如果代码风格有问题，会自动格式化，然后需要重新`Review`完代码之后再重新提交

# 参考


[bookmark](https://juejin.cn/post/7187600446902435898)

