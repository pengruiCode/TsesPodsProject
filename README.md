# TsesPodsProject

### 本地私有库创建
    创建一个文件夹,把你需要拆分的代码放到文件夹中，然后通过终端把你的这个文件夹进行git进行管理
    git init  /   git add. / git commit -m 'xx'/
    
    之后创建个spec文件进行框架的描述
    pod spec create xxx(你创建的文件夹的名字)
    
    字段描述如下
    s.name         = "LocalFiles"
    s.version      = "0.0.2"
    s.summary      = "LocalFiles"
    s.description  = "LocalFiles本地库测试"
    s.homepage     = "https://github.com/pengruiCode/TsesPodsProject.git"
    s.license      = "MIT"
    s.source       = { :git => "", :tag => "#{s.version}" }  #本地的git不用填
    s.author       = {'pengrui' => 'pengruiCode@163.com'}
    s.source_files = "*"
    
 ### 现在进行主工程项目进行cocoapods管理   
    platform :ios, '8.0'
    inhibit_all_warnings!
    def pods
    pod 'LocalFiles',            :path => '../LocalFiles'
    end
    target 'TsesPodsProject' do
        pods
    end
    配置完成之后 直接pod install 安装你本地的私有化库
    安装成功后pod里会有Development Pods文件夹
    
 ##### tips:本地库关联的远程仓库如果建了README.md文件，第一次git push -u origin master会失败，是因为没有将README.md文件同步到本地，用git pull --rebase origin master命令合并代码，再推完成。
    
## 远程库创建
    在组件工程里新建spec
    pod spec create xxx(你创建的文件夹的名字)
    
    s.name         = "SQRNetworkRequset"
    s.version      = "0.2.0"
    s.summary  	   = '网络请求'
    s.homepage     = "https://github.com/pengruiCode/SQRNetworkRequset.git"
    s.license      = { :type => "MIT", :file => "LICENSE" }
    s.author       = {'pengrui' => 'pengruiCode@163.com'}
    s.source       = { :git => 'https://github.com/pengruiCode/SQRNetworkRequset.git', :tag => s.version}
    s.platform 	   = :ios, "8.0"
    s.source_files = "SQRNetworkRequset/**/*.{h,m}"
    s.resource     = "SQRNetworkRequset/LoginLoseEfficacyView.xib"
    s.requires_arc = true
    s.description  = <<-DESC
			简易网络请求，依赖YYCaache实现缓存
                   DESC
    s.subspec "YYCache" do |ss|
        ss.dependency "YYCache"
    end

    s.subspec "AFNetworking" do |ss|
        ss.dependency "AFNetworking"
    end

    s.subspec "SQRBaseDefineWithFunction" do |ss|
        ss.dependency "SQRBaseDefineWithFunction"
    end
    
##### 部分字段描述
    s.name：名称，pod search 搜索的关键词,注意这里一定要和.podspec的名称一样,否则报错
    s.version：版本号
    s.ios.deployment_target:支持的pod最低版本
    s.summary: 简介
    s.homepage:项目主页地址
    s.social_media_url:社交网址,这里我写的微博默认是百度,如果你写的是你自己的博客的话,你的podspec发布成功后会@你
    s.license:许可证
    s.author:作者
    s.source:项目的地址
    s.requires_arc: 是否支持ARC
    s.source_files:需要包含的源文件
    s.public_header_files:公开的头文件
    s.resources: 资源文件
    s.dependency：依赖库，不能依赖未发布的库，可以写多个依赖库
    
##### 需要注意部分字段写法
    dependency:写法
    s.dependency = 'AFNetworking' , 'SDWebImage'
    
    source_files: 写法 
    'SQRNetworkRequset/*'
    'SQRNetworkRequset/SQRNetworkRequset/*.{h,m}'
    'SQRNetworkRequset/**/*.h'
    '*'表示匹配所有文件
    '*.{h,m}' 表示匹配所有以.h和.m结尾的文件
    '**' 表示匹配所有子目录
    
    source: 常见写法
    s.source = { :git => "https://github.com/zhangyqyx/ZYRunTimeCoT.git", :commit => "68defea" }
    s.source = { :git => "https://github.com/zhangyqyx/ZYRunTimeCoT.git", :commit => "68defea", :tag => 1.0.0 }
    s.source = { :git => "https://github.com/zhangyqyx/ZYRunTimeCoT.git", :tag => s.version }
    commit => "68defea" 表示将这个Pod版本与Git仓库中某个commit绑定
    tag => 1.0.0 表示将这个Pod版本与Git仓库中某个版本的comit绑定
    tag => s.version 表示将这个Pod版本与Git仓库中相同版本的comit绑定
    
##### LICENSE文件 
    如果前面没有选择创建这个LICENSE文件， 创建LICENSE(许可证/授权)文件,此文件必须要有
    创建一个文件名字命名为LICENSE,内容为:只需要把前面的版权改一下就行了,后面的都一样
    Copyright (c) 2013-2015 ZYRunTimeCoT (https://github.com/zhangyqyx/ZYRunTimeCoT)
    
##### 提交和验证
    git  add .
    git commit-m"Release 1.0.1"
    git push origin master
    git tag 1.0.1(添加tag)
    git push--tags (推送tag到远程)
    
    pod lib lint xxx.podspec    本地验证
    pod spec lint xxx.podspec   远程验证
    pod trunk push xxx.podspec  推送到远程
    --allow-warnings --use-libraries 加上这一句会在验证和发布时候忽略警告并读取静态库文件
    搜索不到私有库时，在搜索命令后加 --simple
    
    
