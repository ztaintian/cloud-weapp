<template>
  <view class="money">
  
  </view>
</template>

<script>
export default {
  data() {
    return {
      title: "Hello"
    };
  },
  onLoad() {
    this.getDate();
  },
  methods: {
    getDate() {
      // 查询数据库
      const db = wx.cloud.database();
      // 查询当前用户所有的 counters
      db.collection("money")
        .where({})
        .get({
          success: res => {
            console.log(res);
          },
          fail: () => {
            Taro.showToast({
              icon: "none",
              title: "查询记录失败"
            });
          }
        });
    }
  }
};
</script>

<style>
.content {
  text-align: center;
  height: 400upx;
}

.logo {
  height: 200upx;
  width: 200upx;
  margin-top: 200upx;
}

.title {
  font-size: 36upx;
  color: #8f8f94;
}
</style>
