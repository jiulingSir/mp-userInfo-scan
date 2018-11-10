# mpvue

> A Mpvue project

# Build Setup
 


 实现一个登录与扫码的功能

>由于登录功能小程序官方做了修改，所以要有一个button点击才能获取用户信息，这点是比较关键的。
	关键点：
	1.点击绑定方法：@getuserinfo="onGetUserInfo"
	2.登录api wx.login 调用登录接口获取用户信息
	3.扫码api wx.scanCode 通过返回值的data来获取扫码信息

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
