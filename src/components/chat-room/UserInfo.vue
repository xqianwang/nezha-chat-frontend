<template>
  <div class="userinfo">
    <div class="header">详细信息</div>
    <div class="content">
      <img :src="img" />
      <p class="username">{{username}}</p>
      <button class="btnAddUser" v-on:click="AddUser()">添加好友</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserInfo",
  props: ["img", "username", "id"],
  data: () => {
    return {};
  },
  methods: {
    getToken() {
      return this.$store.getters.token;
    },
    AddUser() {
      this.$FriendService
        .post("post", { user_id: this.id }, this.getToken())
        .then(response => {
          if (response.status === 200) {
            alert("用户添加成功");
          }
        })
        .catch(error => {
          alert("用户添加失败", error);
        });
    }
  }
};
</script>

<style lang="stylus" scoped>
.userinfo {
  .header {
    height: 50px;
    line-height: 50px;
    text-emphasis-color: black;
    border-bottom: dotted 1px black;
    vertical-align: middle;
  }

  .content {
    img {
      margin-top: 80px;
      height: 100px;
      width: 100px;
      display: inline-block;
    }

    .username {
      margin-top: 30px;
      display: block;
      height: 22px;
      font-size: 20px;
    }

    .btnAddUser {
      margin-top: 130px;
      height: 40px;
      width: 200px;
      color: white;
      background-color: green;
    }
  }
}
</style>
