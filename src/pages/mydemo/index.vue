<template>
  <div>
    <van-notice-bar
      left-icon="volume-o"
      mode="closeable"
      text="足协杯战线连续第2年上演广州德比战，上赛季半决赛上恒大以两回合5-3的总比分淘汰富力。"
    />
    <van-tabs swipeable custom-class="verical-tabs">
      <van-tab title="点单" >
        <view style="display: flex">
          <van-badge-group :active="currId" @change="onChange" style="width:85px;">
            <van-badge title="创业专享" />
            <van-badge title="咖啡系列" info="8" />
            <van-badge title="套餐系列" info="99" />
            <van-badge title="下午茶" info="99+" />
          </van-badge-group>
          <view style="flex: 1">
            <view v-if="currId === 0">
              <van-card
                v-for="(item, index) in goodslist"
                :key="index"
                :price="item.price"
                :desc="item.desc"
                :title="item.title"
                :thumb="item.imgUrl"
              >
                <view slot="tags" style="float: right;">
                  <van-stepper v-if="item.num > 0" :value="item.num" min="0" @change="onChangeNum($event, index)" />
                  <view v-else @click="item.num = item.num + 1"><van-icon name="add" size="26px" color="#f44" /></view>
                </view>
              </van-card>
            </view>
          </view>
        </view>

      </van-tab>
      <van-tab title="优惠" >内容 2</van-tab>
      <van-tab title="评价(64)" >内容 3</van-tab>
      <van-tab title="商家信息" >内容 4</van-tab>
    </van-tabs>
    <van-submit-bar
      :price="price"
      button-text="下单"
      @submit="onClickButton"
      :tip="tip"
    >
      <van-tag type="primary" style="padding-left:20px;">
        <van-icon name="shopping-cart" size="30px" color="#f44" />
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
        goodslist:[
          {id:555, title:'商品标题1', desc:'描述信息', price: '55',  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
          {id:11, title:'商品标题2', desc:'描述信息', price: '6',  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
          {id:7, title:'商品标题3', desc:'描述信息', price: '66',  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'},
          {id:8, title:'商品标题4', desc:'描述信息', price: '88',  num: 0, imgUrl:'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg'}
        ],
        pageNav:[
          {name: '创业专享'},
          {name: '咖啡系列'},
          {name: '套餐系列'},
          {name: '下午茶'}
        ],
        currId: 0,
        tip: true
      }
    },
    methods: {
      onClickIcon() {
        Toast('点击图标');
      },

      onClickButton() {
        Toast('点击按钮');
      },

      onChange(event) {
        this.currId = event.mp.detail
      },
      onChangeNum(event, idx) {
        this.goodslist[idx].num =  event.mp.detail
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
