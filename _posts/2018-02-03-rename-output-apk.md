---
layout: post
title:  "重命名Gradle打包生成的apk文件"
date:   2018-02-04 12:59:01 +0800
categories: jekyll update
---

Android项目的build.gradle文件

```groovy
android {
  buildTypes {
    // 遍历所有的variant并执行重命名逻辑
    applicationVariants.all { variant ->
      renameAPK(variant)
    }
  }
}

def renameAPK(variant) {
    variant.outputs.each { output ->

        // 获取输出文件
        def file = output.outputFile

        // 获取HEAD的git分支名
        def branch = getGitRevParseInfo("--abbrev-ref")

        // 获取HEAD的commit信息
        def revision = ext.revision = getGitRevParseInfo("--short")

        // 重新生成一个输出的文件名
        def fileName = variant.buildType.name + "_" + branch + "_" + revision + ".apk"

        // 设置新的文件名给输出文件
        output.outputFile = new File(file.parent, fileName)
  	}
}

// 适应Android Gradle Plugin 3.0.0以上的版本的方法
def renameAPKNewVersion(variant) {
    // 使用all替换了each，原因见官方的文档说明
    variant.outputs.all { output ->

        // 获取HEAD的git分支名
        def branch = getGitRevParseInfo("--abbrev-ref")

        // 获取HEAD的commit信息
        def revision = ext.revision = getGitRevParseInfo("--short")

        // 重新生成一个输出的文件名
        def fileName = variant.buildType.name + "_" + branch + "_" + revision + ".apk"

        // 设置新的文件名给输出文件
        outputFileName = fileName
    }
}

// 获取git的信息
static def getGitRevParseInfo(what) {
    def cmd = "git rev-parse " + what + " HEAD"
    def process = cmd.execute()
    process.text.trim()
}
```

*applicationVariants*是Android Gradle扩展中的一个属性，获取到的是一个*DomainObjectSet\<ApplicationVariant\>*，[参考文档](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.AppExtension.html#com.android.build.gradle.AppExtension:applicationVariants)

*ApplicationVariant.outputs*会获取到一个*List\<BaseVariantOutput\>*，包含了variant的输出信息

*BaseVariantOutput.outputFile*会获取到一个*File*，即输出的apk文件

*getGitRevParseInfo(what)*方法用于获取git的一些信息，其中*cmd.execute()*使用了Groovy JDK API中String的能力，把String直接作为命令来执行，[参考文档](http://groovy-lang.org/groovy-dev-kit.html#process-management)

## 参考文档

* http://dcow.io/android-gradle-plugin-docs/
* https://developer.android.com/studio/build/gradle-plugin-3-0-0-migration.html#variant_api