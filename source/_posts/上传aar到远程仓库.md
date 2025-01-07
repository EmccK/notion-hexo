---
updated: '2025-01-07T13:47:00.000Z'
date: '2024-06-16T06:26:00.000Z'
categories: Android
urlname: upload-aar-to-maven
tags:
  - Android
  - Gradle
title: 上传aar到远程仓库
cover: 'https://cn.bing.com/th?id=OHR.RedFoxDad_ZH-CN4894022141_UHD.jpg&rf=LaDigue_UHD.jpg&pid=hp&w=3840&h=2160&rs=1&c=4'
---

[bookmark](https://docs.gradle.org/nightly/userguide/publishing_maven.html#publishing_maven)


# 使用maven-publish插件


在`Gradle7.0`以下，可以使用`maven`插件上传代码，但是在`Gradle7.0`之后，maven插件就不可用了，需要换成`maven-publish`插件，下面是`maven-publish`插件的使用例子

> 注意：`maven-publish`插件最低支持Gradle-Tools的版本为**`3.6.0`**，现在的工程一般都在**`3.6.0`**以上了吧

什么都不说了，直接上代码，下面的代码分别是普通的`groove`文件和Kotlin的`kts`文件


## 新的Gradle KTS的方式


```kotlin

plugins {
		// 下面两种方式都可以
		id("maven-publish")
		`maven-publish`
}

android {
		...
		// 这里是在打包的时候把源码和文档同时上传到Maven仓库
		publishing {
				singleVariant("release") {
						withSourcesJar()
						withJavadocJar()
				}
		}
}

val localRepoURL = "file://" + File(System.getProperty("user.home"), ".m2/repository").absolutePath
val publishGroupId = "com.test.example"
val publishArtifactId = "Test"
val publishVersion = "1.0.0"
// 根据版本号上传不同的仓库
val publishUrl = if (publishVersion.contains("SNAPSHOT", true)) {
    "https://test.snapshot-maven.com"
} else {
    "https://test.release-maven.com"
}

afterEvaluate {
    publishing {
        publications {
            create<MavenPublication>("maven") {
                from(components["release"])
                groupId = publishGroupId
                artifactId = publishArtifactId
                version = publishVersion
            }
        }

        repositories {
            maven {
                url = uri(publishUrl)
                isAllowInsecureProtocol = true
                credentials {
                    username = "username"
                    password = "password"
                }
            }
            maven {
                url = uri(localRepoURL)
                isAllowInsecureProtocol = true
                name = "local"
            }
        }
    }
}
```


## 老的Groovy的方式


```groovy
apply plugin: 'maven-publish'


android {
		...
		// 这里是在打包的时候把<u>**源码和文档**</u>同时上传到Maven仓库
		publishing {
				singleVariant("release") {
						withSourcesJar()
						withJavadocJar()
				}
		}
}

def localRepoURL = 'file://' + new File(System.getProperty('user.home'), '.m2/repository').absolutePath
def PUBLISH_GROUP_ID = 'com.test.example'
def PUBLISH_ARTIFACT_ID = 'Test'
def PUBLISH_VERSION = "1.0.0"
def GITHUB_REPO_PATH = ""
if (PUBLISH_VERSION.contains('SNAPSHOT')) {
		// SNAPSHOT Maven仓库地址
    GITHUB_REPO_PATH = "https://test.snapshot-maven.com"
} else {
    // Release Maven仓库地址
    GITHUB_REPO_PATH = "https://test.release-maven.com"
}

afterEvaluate {
    publishing {
        publications {
            Production(MavenPublication) {
                from components.release
                groupId = PUBLISH_GROUP_ID
                artifactId = PUBLISH_ARTIFACT_ID
                version = PUBLISH_VERSION
            }
        }
        repositories {
						// 远程仓库
            maven {
								// 如果你的仓库地址是http，则需要加这个参数
                allowInsecureProtocol = true
                url = GITHUB_REPO_PATH
                credentials {
                    username = "username"
                    password = "password"
                }
            }
						// 本地仓库
            maven {
                allowInsecureProtocol = true
                url = localRepoURL
                name = "local"
            }
        }
    }
}
```


# 直接上传本地aar文件到远程


```kotlin
publishing {
    publications {
        create<MavenPublication>("aar") {
            // 设置 groupId, artifactId 和 version
            groupId = "com.example"
            artifactId = "mylibrary"
            version = "1.0.0"

            <u>**// 指定要上传的文件**</u>
            artifact("$buildDir/outputs/aar/mylibrary-release.aar")

            // 可选：如果需要生成 POM 文件
            pom.withXml {
                // 配置 POM 文件的内容
            }
        }
    }

    repositories {
        maven {
            url = uri("http://your-maven-repo-url")

            // 如果需要认证
            credentials {
                username = "your-username"
                password = "your-password"
            }
        }
    }
}
```

