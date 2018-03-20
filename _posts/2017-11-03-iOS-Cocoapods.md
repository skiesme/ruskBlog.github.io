---
layout: post
title: 'iOS Cocoapods'
date: 2017-11-03
author: 王那么一个振
catalog:      true
tags: 
    - CocoaPods
    - iOS
---

# iOS Cocoapods
这里需要创建至少两个远程仓库，一个用来作为私有库的索引，其余的根据自己需要来创建不同的仓库。 
* 内容库的创建
例如:``XXXKit``、``YYYKit``
* 索引库的创建 --> 这个仓库决定了以后你 在引用是的地址。
例如:``XXXKitSpec``


## 1.Register
```
pod trunk register wangzhen@outlook.com 'xxxx' --description='ios developer' --verbose
```

```
pod trunk me
```

```
pod spec cerate XXX
```

## 2.podspec
具体内容需要根据自己的项目来配置。

```
Pod::Spec.new do |s|
    s.name             = "XXXKit"
    # 这里面填写 你发包的 tag 号如：0.0.2、1.0.0
    s.version          = "0.0.1"
    # 简介
    s.summary          = "xxxx"
    # 描述
    s.description      = <<-DESC
                       （这里是描述，记得字数一定要比 s.summary 长！）
                       DESC

    s.homepage         = "https://gitee.com//XXXKit"
    s.license          = 'MIT'
    s.author           = { "xxx" => "xxxx@gmail.com" }
    s.source           = { 
    :git => "https://gitee.com/xxxx/XXXXKit.git", (内容库的地址)
    :tag => s.version 
    }
    
    #(对应 库的最小支持版本)
    s.platform     = :ios, '8.0' 
    s.requires_arc = true

# 资源文件
#s.source_files = 'XWCocoa/Classes/**/*'
# s.resource_bundles = {
#   'XWCocoa' => ['Pod/Assets/*.png']
# }
# s.public_header_files = 'XWCocoa/Classes/**/*.h'

    # 1.子库: 如 常用Category
    s.subspec 'Category' do |cat|
    # 文件路径
      cat.source_files = 'Classes/Category/**/*.{h,m}'
      cat.public_header_files = 'Classes/Category/**/*.h'
      
      #子库 所需要的 framework
      cat.frameworks = 'UIKit'
      
      #子库 所需要的 依赖
      view.dependency 'Masonry'
    end
    
    # 整个库所需要的依赖
    # s.dependency 'IGListKit'
end
```

## 3.Push
* 验证 ``.podspec`` 文件进行验证。

```
pod lib lint --verbose --allow-warnings
```

* 提交到CocoaPods
执行命令``pod trunk push``即可完成提交，该命令会首先验证你本地的 ``.podspec`` 文件，之后会上传spec文件到trunk，最后会将你上传的podpec文件转换为需要的json文件。

```
pod trunk push XWCocoa.podspec --verbose --allow-warnings
```

* 将刚才好的``.podsec``文件上传到本地这个文件夹并且上传到远程目录管理服务器

```
pod repo push XWCocoaSpec XWCocoa.podspec --verbose --allow-warnings
```



##  4.Error
*  如果发现``pdo atal error: 'UIKit/UIKit.h' file not found``错误，可尝试加入 
    
```
s.platform     = :ios, '8.0'
s.requires_arc = true
```

*  如果发现`` file patterns: The `source_files` pattern did not match any file.``错误，这个原因是由于 ``view.source_files`` 或者 ``view.public_header_files``配置错误导致。这里需要 检查每一个路径书写。
    

* 如果发现`` did not pass validation ,due to 1 wanrings (but you can use --allow-warnings to ignore them) ``错误，在命令后面加``--allow-warnings`` 即可。


