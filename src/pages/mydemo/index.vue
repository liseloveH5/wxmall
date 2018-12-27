<template>
  <div>
    <van-notice-bar
      left-icon="https://img.yzcdn.cn/1.png"
      mode="closeable"
      text="足协杯战线连续第2年上演广州德比战，上赛季半决赛上恒大以两回合5-3的总比分淘汰富力。"
    />
    <van-tabs swipeable class="mode-class">
      <van-tab title="标签 1" tab-class="vertical">
        <van-card
          num="2"
          price="2.00"
          desc="描述信息"
          title="商品标题"
          :thumb="imageURL"
        />
        <van-card
          num="2"
          price="2.00"
          desc="描述信息"
          title="商品标题"
          :thumb="imageURL"
        />
      </van-tab>
      <van-tab title="标签 2" tab-class="vertical">内容 2</van-tab>
      <van-tab title="标签 3" tab-class="vertical">内容 3</van-tab>
      <van-tab title="标签 4" tab-class="vertical">内容 4</van-tab>
      <van-tab title="标签 5" tab-class="vertical">内容 5</van-tab>
      <van-tab title="标签 6" tab-class="vertical">内容 6</van-tab>
      <van-tab title="标签 7" tab-class="vertical">内容 7</van-tab>
      <van-tab title="标签 8" tab-class="vertical">内容 8</van-tab>
      <van-tab title="标签 9" tab-class="vertical">内容 9</van-tab>
    </van-tabs>
    <van-submit-bar
      :price="price"
      button-text="提交订单"
      bind:submit="onClickButton"
      :tip="tip"
    >
      <van-tag type="primary">标签</van-tag>
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
        imageURL: 'http://img.yzcdn.cn/upload_files/2017/07/02/af5b9f44deaeb68000d7e4a711160c53.jpg',
        price: 3050,
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
    }
  }
</script>

<style>
  .mode-class{
    background: red;
  }
  .vertical{
    background: red;
  }
  .vertical-mode .van-tabs__nav--line{
    flex-direction: column!important;
  }
  .vertical-mode .van-tabs--line .van-tabs__wrap{
    width: 100px;
  }

</style>
