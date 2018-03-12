# Ionic3
Ionic3， 基于angular4和Typescript的app前端开发框架








Github	  https://github.com/ionic-team/ionic/releases
BLOG	https://blog.ionicframework.com/
Slack 	http://ionicworldwide.herokuapp.com/
线上测试工具ion-view		https://ionicframework.com/docs/pro/view/
懒加载		https://www.jianshu.com/p/97533115a934	https://blog.ionicframework.com/ionic-and-lazy-loading-pt-2/

安装：
npm install -g ionic cordova
初始化:
ionic start project-name (tabs/blank/sidemenu)
ionic serve 浏览器运行
使用ionic v1版本
ionic start project-name --type ionic1
编译打包:
(sudo) ionic build (--prod 打包的同时进行压缩  )  三个平台全部打包（ios、android、微信）

网页版编译打包
浏览器：
npm run build --prod
或者是  ionic build --prod
微信端: 微信下的适配体验
添加依赖
ionic cordova platform add browser
打包
ionic cordova build browser
部署platform/browser/www文件夹到对应服务器(静态站点部署)



Android和Ios编译打包
Ios:
ionic cordova platform 显示已经安装的平台和可以安装的平台
ionic cordova platform add ios (mac下需要添加sudo， windows下需要确认命令行以管理员身份进行)
注意获获取目录权限的问题：sudo chomd -R 777 项目文件名
ionic cordova build ios  在platform中找到ios/MyApp.xcodeproj 在Xcode中运行打开

ios9以下的真机调试需要Apple 开发者账号(缴费的)

Android:
ionic cordova build android 可以直接生成apk
或者可以ionic build 之后 使用android studio进行打包生成apk(推荐)





快速生成组件(page pipe directive tabs component provider)
ionic generate  page 文件目录       默认位置在pages下(简写： ionic g )
ionic g page chat      ionic g page chat/chatlist














### 命令行   ionic2版本
    1、项目创建 ionic start new-page blank --v2  创建一个空页面的项目  --blank 可以替换为 tabs menu ...
    2、创建一个组件  ionic generate page new-page
    3、浏览器运行     ionic serve
    4、项目打包测试    npm run ionic:build --prod  压缩后的文件存储在 www目录下
    5、添加平台支持    ionic platform add android/ios



    6、配置app图标和启动页  ionic resources 可以是psd/ai/png格式  建议大小 1024*1024  和   2208*2208
                1、在添加了平台支持之后，会出现一个resources的文件，里面里面有android、iso、icon.png、splash.png几个文件。替换icon和splash图片，便可以更改启动页的图片和app的logo图标。
                icon的大小最好是1024*1024的，splash的大小最好是2208*2208的。之后执行 ionic resources就可以替换了。禁忌，图片指支持.png .ai .psd形式的。有时候网络不好的时候，会出现resources失败的情况。
                 解决加载时出现的启动页之后的一段时间白屏现象：
                    添加启动动画插件
                    ionic plugin add cordova-plugin-splashscreen

                    修改xml文件
                    <preference name="ShowSplashScreenSpinner" value="false"/>
                    <preference name="SplashMaintainAspectRatio" value="true"/>
                    <preference name="SplashShowOnlyFirstTime" value="false"/>
                    <preference name="SplashScreenDelay" value="10000"/>
                    <preference name="FadeSplashScreen" value="false"/>

                    在app.component.ts中更改js
                    $ionicPlatform.ready(function () {
                           if (window.cordova && window.cordova.plugins.Keyboard) {
                               cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);

                               cordova.plugins.Keyboard.disableScroll(true);

                               //延迟splash screnn 隐藏时间,不然会有短暂的白屏出现
                               setTimeout(function () {
                                   navigator.splashscreen.hide();
                               }, 1000);
                           }
                           });
    7、打包安卓版本apk  ionic build android
                a、第一步配置java环境，版本需要在1.8_以上
                b、下载Android Studio（此软件自带着SDK环境，SDK是安卓打包的必备环境，必须要有的。下载软件Android Studio之后，可以通过SDK Manager进行管理，下载安装需要的SDK环境。）
                c、前面步骤都是打包的必要环境，下面是代码操作步骤
                d、在webStrom项目中，运行 ionic platfrom add android ，添加安卓的平台支持。之后会在platform文件中看到多了一个Android文件。利用Android Studio，打开这个Android文件。
                    在Android Studio上方的Tools中找到，Android，里面有一个ADV Manager，添加需要模拟的设备，进行下载安装。Android Studio中项目不能包含中文字符。
                    在Android Studio打开android项目的时候，会创建一个gradle文件。之后创建了这个文件之后，才可以进行ionic build android操作，否则无法打包
                e、在webStorm中，运行ionic build andorid，打包安卓环境。之后你会看到在Android中看到之前的Android文件会有少许改动。
                f、在Android Studio中点击一个向右箭头的标志，便可以进行仿真机的模拟。模拟之后，便可以点击上方的build ， 里面有个build APk。点击，就会打包apk，然后将apk发送到安卓手机上，便可以进行安装了。
    8、打包发布版本    ionic build --release andorid/ios  （安卓版本为 android-release-unsinged.apk） （苹果版本为name.xcodeproj）
    