遇到这样的需求并踩了坑：  
设置密码或者输入密码的时候要求输入框的右侧有个眼睛的图标，点击可以开启和关闭密码显示状态  
我的实现：  
```html
<!-- 错误示范 -->
<view>
  <input type="{{isShow?'text':'password'}}" />
  <icon class="iconfont icon-show" bindtap="changeState"></icon>
</view>
```
```js
Page({
  data:{
    isShow:false
  },
  changeState(){
    let state = !this.data.isShow
    this.setData({
      isShow:state
    })
  }
})
```
如果使用上面的方法，在小程序开发ide中没问题，点击后也能正常的显示和隐藏  
但是在手机端预览时会出现点击图标无法切换的问题

要想生效，需要采用`password`属性
```html
<input password="{{isShow}}" bindtap="changeState" />
```
当isShow为true时，此input会改为密码输入框，内容会被隐藏，手机端预览与实际需求一致