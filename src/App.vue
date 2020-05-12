<script>
export default {
  onLaunch: function() {
    console.log("App Launch");
    wx.cloud.init();
  },
  onShow: function() {
    console.log("App Show");
  },
  onHide: function() {
    console.log("App Hide");
  }
};
</script>

<style lang="scss">
/*每个页面公共css */
.index {
  .content {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: space-around;
    border-bottom: 1rpx solid #eee;
    padding: 15rpx 0;

    view {
      min-width: 80px;
      display: inline-block;
      text-align: center;
      text-align: center;
    }

    .title {
      color: #0070c5;
    }
  }

  .input {
    padding: 30rpx 10rpx;
    display: flex;
    align-items: center;
    border-bottom: 1rpx solid #eee;

    view {
      margin-right: 10rpx;
    }
  }

  .add {
    width: 80%;
    line-height: 70rpx;
    border-radius: 10rpx;
    background: #00b26a;
    color: #ffffff;
    text-align: center;
    margin: 40rpx auto 0;
  }
}
</style>
