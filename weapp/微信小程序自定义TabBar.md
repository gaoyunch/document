# 小程序 - 自定义TabBar

[TOC]

## 官方tabBar地址
    https://developers.weixin.qq.com/miniprogram/dev/framework/config.html

## 自定义tabBar
    小程序的页面结构分为两种: page 和 component；
    page就是普通的页面， components是小程序为实现模块化而提供的自定义组件。
- page就是普通的页面， component是小程序为实现模块化而提供的自定义组件
- 相同点：都由四个文件：.js、.json、.wxml、.wxss、构成，.wxml、.wxss写法完全相同
- 不同点： component要在json文件中注明："component": true
  ~~~json
  {
      "component": true,
      "usingComponents": {}
  }
  ~~~
  js文件的结构和生命周期函数不同，下面是自动生成的page和components代码

### page页面的.js代码结构如下:

~~~javascript
Page({
    /** 页面的初始数据 */
    data: { },
    /** 生命周期函数--监听页面加载 */
    onLoad(options) { },
    /** 生命周期函数--监听页面初次渲染完成 */
    onReady() { },
    /** 生命周期函数--监听页面显示 */
    onShow() { },
    /** 生命周期函数--监听页面隐藏 */
    onHide() { },
    /** 生命周期函数--监听页面卸载 */
    onUnload() { },
    /** 页面相关事件处理函数--监听用户下拉动作 */
    onPullDownRefresh() { },
    /** 页面上拉触底事件的处理函数 */
    onReachBottom() { },
    /** 用户点击右上角分享 */
    onShareAppMessage() { }
})
~~~

### component页面的.js代码结构如下:

~~~javascript
Component({
  /** 组件的属性列表 */
  properties: { },
  /** 组件的初始数据 */
  data: { },
  /** 组件的方法列表 */
  methods: { }
})
~~~

自定义tabBar中每个 tab 都是一个小程序中定义的 component，只有最外层包裹的是 page，因为page中只能嵌入component，component中也可以嵌入component。


### 实战与原理
例如：myapp 程序主界面包含两个 tab：主页和我的，主页又包含两个tab：最热和最新；我的也包含两个tab：电影和音乐。
1. 程序的主界面，包含了两个tab：home 和 mine，分别对应页面下方的 主页 和 我的。
要引入自定义组件需要在 myapp.json文件中声明：
~~~json
{
  "usingComponents":{
    "home": "./home/home",
    "mine": "./mine/mine"
  }
}
~~~
~~~html
<view class='container'>
  <view class='content'>
    <view wx:if='{{currentTab == 0}}'>
      <home/>
    </view>
    <view wx:if='{{currentTab == 1}}'>
      <mine/>
    </view>
  </view>
  <!-- 下面的两个tab -->
  <view class='bottom-tab'>
    <view class='tab-item {{currentTab == 0 ? "active" : ""}}' data-current="0" bindtap='switchTab'>
      <image src='{{currentTab == 0 ? "../../assets/home_active.png" : "../../assets/home.png"}}' class='item-img'></image>
      <text class='item-text'>主页</text>
    </view>
    <view class='tab-item {{currentTab == 1 ? "active" : ""}}' data-current="1" bindtap='switchTab'>
      <image src='{{currentTab == 1 ? "../../assets/mine_active.png" : "../../assets/mine.png"}}' class='item-img'></image>
      <text class='item-text'>我的</text>
    </view>
  </view>
</view>
~~~

> tab切换实现原理: 根据 wx:if 或者 hidden 来控制视图的显示和隐藏，页面的data中设置一个变量currentTab来记录当前点击的是哪个tab，每次点击的时候更新currentTab的值。

切换tab的方法：
~~~javascript
switchTab(e) {
    this.setData({ currentTab: e.currentTarget.dataset.current });
}
~~~

这里有几个需要注意的点：

- 这里判断相等用了 == 而不是 === ，因为通过 e.currentTarget.dataset.current取到的值是字符串类型的，也就是给 data 设置的值是字符串的0和1，如果用 === 就会判断出错(可以使用强转换)。
- 控制组件显示隐藏可以用 wx:if 也可以用 hidden。**两者是区别是如果用 wx:if ，每次切换tab的时候组件都会重新渲染，生命周期方法会重新调用执行。而用 hidden则不会重新渲染，生命周期函数也不会重新调用。**

2. 主页home，它本身是一个component，又包含了两个component ：最热hot 和 最新new。
同样需要在home.json中注册这两个组件
~~~json
{
  "component": true,
  "usingComponents": {
    "hot": "hot/hot",
    "new": "new/new"
  }
}
~~~
- 注意home本身是一个component，所以需要注明"component": true
  
布局文件 home.wxml
~~~html
<view class='container'>
  <view class='tab-wrapper'>
    <view id='tableft' class='tab-left {{currentTab === 0 ? "tab-active":""}}' bindtap='switchTab'>最热</view>
    <view id='tabright' class='tab-right {{currentTab === 1 ? "tab-active" : ""}}' bindtap='switchTab'>最新</view>
  </view>
  <view class='content-wrapper' wx:if='{{currentTab === 0}}'><hot/></view>
  <view class='content-wrapper' wx:if='{{currentTab === 1}}'><new/></view>
</view>
~~~
js文件 home.js
~~~javascript
Component({
  /** 组件的属性列表 */
  properties: { },
  /** 组件的初始数据 */
  data: {
    currentTab: 0
  },
  /** 组件的方法列表 */
  methods: {
    switchTab(e) {
      let tab = e.currentTarget.id
      if (tab === 'tableft') {
        this.setData({ currentTab: 0 })
      } else if (tab === 'tabright') {
        this.setData({ currentTab: 1 })
      }
    }
  }
})
~~~
给两个tab的view设置了id属性值为tableft和tabright，设置了id后就可以用e.currentTarget.id获取到当前点击的是哪个元素了。
其他几个页面的代码都大同小异，主要是判断当前点击的是哪个tab，然后根据currentTab判断该显示或隐藏哪个组件。