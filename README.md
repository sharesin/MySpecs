# MySpecs
Cocoapods私有管理仓库

参考地址<http://www.cocoachina.com/ios/20150228/11206.html>

Cocoapods创建私有库基本步骤：

1. 创建并设置一个私有的Spec Repo。
2. 创建Pod的所需要的项目工程文件，并且有可访问的项目版本控制地址。
3. 创建Pod所对应的podspec文件。
4. 本地测试配置好的podspec文件是否可用。
5. 向私有的Spec Repo中提交podspec。
6. 在个人项目中的Podfile中增加刚刚制作的好的Pod并使用。
7. 更新维护podspec。

配置环境：`cocopods1.0.0`、`xcode8.1`、`Git2.9.5`、`macOS10.11.6`

####1. 创建私有Spec Repo

Spec Repo是所有的Pods的一个索引，相当于一个容器，把所有公开的Pods都装在里面。它存放在远端的Git服务上，当你使用了Cocoapods之后，就会被clone到本地的~/.cocoapods/repos目录下。
	
	$cd ~/.cocoapods/repos
	$git clone https://github.com/sharesin/MySpecs.git

####2. 创建Pod项目工程文件
	
	pod lib create iOS-PodsLibOne
	
参考如下，根据自己需要设定
![img](Snip20161115_1.png)

添加测试代码，详见工程`PodsOneLibUtil.h`

####3. 配置podspec文件

详见`CTMediator.podspec`文件

具体配置参考：<https://guides.cocoapods.org/syntax/podspec.html>
	
####4. 测试校验配置好的podspec文件

	$ pod lib lint 

 	-> iOS-PodsLibOne (0.1.0)
 	
	iOS-PodsLibOne passed validation.


####5. 向私有MSpec Repo中提交podspec

首信提交Pod项目工程文件，打tag标记
	
	$git add .
	$git commit -m 'Initial iOS-PodsLibOne Commit of Library'
	$git remote add origin git@github.com:sharesin/iOS-PodsLibOne.git
	$git push origin master
	
	$git tag -m 'release message.' '0.1.0'
	$git push --tags

向私有MySpecs提交podspec
	
	$pod repo push MySpecs iOS-PodsLibOne.podspec 
	
####6. 个人项目使用
	
	pod "iOS-PodsLibOne"

