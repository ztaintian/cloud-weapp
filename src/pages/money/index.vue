<template>
  <div class="index">
    <div class="content">
      <div class="title">姓名</div>
      <div class="title">金额</div>
      <div class="title">操作</div>
    </div>

    <div class="content" v-for="(item,index) in list" :key="index">
      <div>{{item.name}}</div>
      <div>{{item.money}}</div>
      <div>删除</div>
    </div>
    <div class="input">
      <div>姓名:</div>
      <input type="text" v-model="name" placeholder="请输入姓名" />
    </div>
    <div class="input">
      <div>金额:</div>
      <input type="text" v-model="money" placeholder="请输入金额" />
    </div>
    <div class="add" @click="submit">添 加</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Hello",
      name: "",
      money: "",
      list: []
    };
  },
  onLoad() {
    this.getDate();
  },
  methods: {
    submit() {
      // 添加数据库
      console.log(444);
      const db = wx.cloud.database();
      db.collection("money").add({
        data: {
          name: this.name,
          money: this.money
        },
        success: () => {
          // 在返回结果中会包含新创建的记录的 _id
          wx.showToast({
            title: "添加成功"
          });
          console.log(6666);
          this.name = "";
          this.money = "";
          this.getDate();
        },
        fail: () => {
          wx.showToast({
            icon: "none",
            title: "添加失败"
          });
        }
      });
    },
    getDate() {
      // 查询数据库
      const db = wx.cloud.database();
      const _ = db.command;
      db.collection("money")
        .aggregate()
        .sort({
          money: -1
        })
        .end().then((res) => {
          console.log('aa',res)
          this.list = res.list;
        });
      // 查询当前用户所有的 counters
      // db.collection("money")
      //   .where({})
      //   .get({
      //     success: res => {
      //       console.log(res);
      //       this.list = res.data;
      //     },
      //     fail: () => {
      //       wx.showToast({
      //         icon: "none",
      //         title: "查询记录失败"
      //       });
      //     }
      //   });
    }
  }
};
</script>

<style>
</style>
