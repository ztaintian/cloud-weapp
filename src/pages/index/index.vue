<template>
  <div class="index">
    <div class="content">
      <div class="title">姓名</div>
      <div class="title">生日</div>
      <!-- <div>阳历</div> -->
      <div class="title">操作</div>
    </div>
    <!-- {
          this.state.list.map(function (item, index) {
            return 
          })
    }-->
    <div class="content" v-for="(item,index) in list" :key="index">
      <div>{{item.name}}</div>
      <!-- <div>{{item.sunMonth}}</div> -->
      <div>{{item.moonMonth}}</div>
      <div>删除</div>
    </div>
    <div class="input">
      <div>姓名:</div>
      <input type="text" v-model="name" placeholder="请输入姓名" />
    </div>
    <!-- <div class="input">
      <div>生日:</div>
      <input type="text" v-model="sunMonth" placeholder="请输入阳历生日" />
    </div> -->
    <div class="input">
      <div>生日:</div>
      <input type="text" v-model="moonMonth" placeholder="请输入阴历生日" />
    </div>
    <div class="add" @click="submit">添 加</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Hello",
      list: [],
      name: "",
      moonMonth: "",
      sunMonth: ""
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
    submit() {
      // 添加数据库
      const db = Taro.cloud.database();
      db.collection("counters").add({
        data: {
          name: this.state.name,
          sunMonth: this.state.sunMonth,
          moonMonth: this.state.moonMonth
        },
        success: () => {
          // 在返回结果中会包含新创建的记录的 _id
          Taro.showToast({
            title: "添加成功"
          });
          this.name = "";
          this.moonMonth = "";
          this.getDate();
        },
        fail: () => {
          Taro.showToast({
            icon: "none",
            title: "添加失败"
          });
        }
      });
    },
    getDate() {
      // 查询数据库
      const db = wx.cloud.database();
      // 查询当前用户所有的 counters
      db.collection("counters")
        .where({})
        .get({
          success: res => {
            console.log(res);
            this.list = res.data;
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
  color: red;
}
</style>
