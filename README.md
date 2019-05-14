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
    
