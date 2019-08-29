### Tab 联动
做小程序商城项目的时候遇到一个需求，展示一个商品分类tab，可滑动tab和商品列表，切滑动商品时如果商品所在分类不在当前视图，tab标签栏会自动滑动到当前分类，在此记录下自己的完成过程。

标签栏因为要滑动，所以使用`scroll-view`来做容器
```html
<!-- tab标签 -->
<scroll-view class="swiper-tab" scroll-x="{{true}}" scroll-left="{{scroll_left}}" scroll-with-animation="{{true}}">
  <view wx:for="{{product_sorts}}" wx:key="index" class="swiper-tab-item {{currentTab==index?'active':''}}" data-current="{{index}}" bind:tap="clickTab">
    {{item}}
  </view>
</scroll-view>

<!-- 可滑动切换商品内容展示 -->
<swiper class="swiper-content" current="{{currentTab}}" duration="300" bind:change="swiperTab" style="height:{{scrollHeight}}rpx;">
  <swiper-item wx:for="{{products}}" wx:for-item="items" class="swiper_item" wx:key="index">
    <scroll-view scroll-y="{{true}}" class="scroll-h">
      <view class="product_container">
        <v-product class="product_item" wx:for="{{items}}" wx:key="index" product="{{item}}" />
      </view>
    </scroll-view>
  </swiper-item>
</swiper>
```
- 在标签的`scroll-view`中添加`scroll-width-animation`会有较好的过度效果，否则滑动会很生硬
- 目前的小程序版本`swiper`需要一个高度，否则会使用默认的150px的高度，为了适配手机屏幕，所以我们需要计算可用高度`scrollHeight`

在js中，控制current的值来控制标签的选中状态
```js
Page({
  data:{
    currentTab:0,   // swiper切换选中位置
    scrollHeight: 0 // 自适应swiper内容高度
    tabTrigger: 2   // 这里要注意tabLength的取值，为可见tab数量-2，例如你最大能放4个tab，那么tabLength取值为2，这样联动后你所选中的tab会处于较中间的位置
  },

  onLoad(){
    this.setHeight();
    this._loadData();
  },

  // 设置scrollHeight
  setHeight(){
    let systemInfo = wx.getSystemInfoSync();
    let windowHeight = systemInfo.windowHeight;
    const promise = new Promise((resolve,reject)=>{
      const query = wx.createSelectorQuery()
      query.select(selector).boundingClientRect()
      query.exec(function (res) {
        resolve(res[0].height)
      })
    })
    promise.then((res)=>{
      this.setData({
        scrollHeight: windowHeight - res
      })
    })
  },

  // 获取数据
  _loadData(){
    // TODO 获取商品分类数据
  },

  /**
  * 点击tab，切换产品列表视图
  * @param {Event} event 触发事件对象
  */
  clickTab(e){
    let eCurrent = e.target.dataset.current;
    if(eCurrent == this.data.currentTab)
      return;
    this.setData({
      currentTab: eCurrent
    })
  }

  /**
  * 滑动产品列表视图，联动tab
  * @param {Event} event 触发事件对象
  */
  swiperTab(e){
    // 这里注意current_tap的取值
    let current_tap = event.detail.current,
        left = 0;
    if(current_tap >= this.data.tabTrigger){
      left = parseInt(current_tap - this.data.tabTrigger) * 100;
    }
    this.setData({
      currentTab: current_tap, // 这一步是联动的关键
      scroll_left: left
    })
  }
})
```

样式有一部分要说的是，在设置了swiper的高度后，swiper-item的高度只需要设置为100%就可以了
```css
/* tab标签 */
.swiper-tab{
  overflow: hidden;
  white-space: nowrap;
  width:100%;
}
.swiper-tab-item{
  display:inline-flex;
  width:200rpx;
  height:100rpx;
  justify-content: center;
  align-items:center;
  overflow:scroll;
}
.swiper-tab-item.active{
  color:red;
  flex-basis: 20%;
}
/* 内容部分 */
.swiper-content{
  margin-top:168px;
  font-size:14px;
  width:100%;
}
.scroll-h{
  height:100%;
}
```