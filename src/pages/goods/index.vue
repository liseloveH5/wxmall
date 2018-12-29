<template>
  <div>
    <van-notice-bar
      left-icon="volume-o"
      mode="closeable"
      :text="notice"
    />
    <van-tabs swipeable custom-class="verical-tabs">
      <van-tab title="点单" >
        <view style="display: flex;">
          <van-badge-group :active="currId" @change="onChange" style="width:85px;">
            <van-badge :title="nav.title"  v-for="(nav, index) in pageNav" :key="index"/>
          </van-badge-group>
          <view style="flex: 1; height:70vh; overflow-x: hidden">
            <view v-if="currId === id" v-for="(goods, id) in goodslist" :key="id">
              <van-card
                v-for="(item, index) in goods.children"
                :key="index"
                :price="item.price"
                :desc="item.desc"
                :title="item.title"
                :thumb="item.imgUrl"
              >
                <view slot="tags" style="float: right;">
                  <van-stepper v-if="item.num > 0" :value="item.num" min="0" @change="onChangeNum($event, index, id)" />
                  <view v-else @click="item.num = item.num + 1"><van-icon name="add" size="26px" color="#f44" /></view>
                </view>
              </van-card>
            </view>
          </view>
        </view>

      </van-tab>
      <van-tab title="优惠" >优惠单页</van-tab>
      <van-tab title="评价(64)" >评价</van-tab>
      <van-tab title="商家信息" >商家信息</van-tab>
    </van-tabs>
    <van-submit-bar
      :price="price"
      button-text="下单"
      @submit="onClickButton"
      :tip="tip"
    >
      <van-tag type="primary" style="padding-left:20px;">
        <van-icon name="shopping-cart" size="30px" color="#f44" :info="totalNum" />
      </van-tag>
      <view slot="tip">
        您的收货地址不支持同城送, <text>修改地址</text>
      </view>
    </van-submit-bar>
  </div>
</template>

<script>
  export default {
    name: "index",
    data () {
      return {
        goodslist:[{
          parentId: 1,
          children:[
            {id:555,  title:'商品标题1', desc:'描述信息', price: 5,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:11, title:'商品标题2', desc:'描述信息', price: 1,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:7, title:'商品标题3', desc:'描述信息', price: 1,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:7, title:'商品标题3', desc:'描述信息', price: 1,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:7, title:'商品标题3', desc:'描述信息', price: 1,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:8, title:'商品标题4', desc:'描述信息', price: 1,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'}
          ]
        },{
          parentId: 2,
          children:[
            {id:45, title:'商品标题5', desc:'描述信息', price: 10,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:6, title:'商品标题6', desc:'描述信息', price: 10,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
            {id:5, title:'商品标题7', desc:'描述信息', price: 10,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
          ]
        },{
          parentId: 3,
          children:[
            {id:54, title:'商品标题8', desc:'描述信息', price: 10,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'}
          ]
        },{
          parentId: 4,
          children:[
            {id:74, title:'商品标题9', desc:'描述信息', price: 10,  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'}
          ]
        }],
        pageNav:[
          {title: '创业专享'},
          {title: '咖啡系列'},
          {title: '套餐系列'},
          {title: '下午茶'}
        ],
        currId: 0,
        tip: true,
        notice: '足协杯战线连续第2年上演广州德比战，上赛季半决赛上恒大以两回合5-3的总比分淘汰富力。'
      }
    },
    computed:{
      // 计算总价
      price: function() {
        let total = 0
        this.goodslist.forEach(val => {
          val.children.forEach(v => {
          total = total + v.num * v.price
          })
        })
        return total *100
      },
      // 计算总数量
      totalNum: function() {
        let num = 0
        this.goodslist.forEach(val => {
          val.children.forEach(v => {
          num = num + v.num
        })
      })
        return num
      }
    },
    methods: {
      onClickIcon() {
        Toast('点击图标');
      },

      onClickButton() {
        if(this.totalNum == 0){
          wx.showToast({
            icon: 'none',
            title: `您的购物车空空如也~`
          });
          return
        }
        const url = '../toPay/main'
        wx.navigateTo({ url })
      },

      onChange(event) {
        this.currId = event.mp.detail
      },
      onChangeNum(event, index, id) {
        this.goodslist[id].children[index].num =  event.mp.detail
      }
    }
  }
</script>

<style>
  /*.verical-tabs{*/
    /*display: flex!important;*/
  /*}*/
  /*.verical-tabs .van-tabs__nav{*/
    /*flex-direction: column;*/
  /*}*/
  /*.verical-tabs .van-tabs__wrap{*/
    /*width: 100px;*/
    /*height: auto!important;*/
  /*}*/


</style>
