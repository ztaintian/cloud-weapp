<template>
  <view class="content">
   
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
    // wx.cloud
    //   .callFunction({
    //     name: "login"
    //   })
    //   .then(res => {
    //     console.log("用户信息", res);
    //   })
    //   .catch(console.log);
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
            console.log(res)
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

<style lang="scss">
.aa {
  color:red;
}
</style>
