<template>
  <div>
    <div class="title">
      <van-nav-bar
        title="注册"
        left-text=""
        left-arrow
        @click-left="onClickLeft"
      >
      </van-nav-bar>
    </div>
    <van-form @submit="onSubmit">
      <van-field
        v-model="username"
        name="用户名"
        label="用户名"
        placeholder="用户名"
        :rules="[{ required: true, message: '请填写用户名' }]"
      />
      <van-field
        v-model="phone"
        name="账号"
        label="账号"
        placeholder="账号"
        :rules="[{ required: true, message: '请填写账号' }]"
      />
      <van-field
        v-model="password"
        type="password"
        name="密码"
        label="密码"
        placeholder="密码"
        :rules="[{ required: true, message: '请填写密码' }]"
      />
      <van-field
        v-model="passwords"
        type="password"
        name="再次输入密码"
        label="再次输入密码"
        placeholder="再次输入密码"
        :rules="[{ required: true, message: '请填写密码' }]"
      />
      <div style="margin: 16px">
        <van-button round block color="#ff6700" native-type="submit">
          注册
        </van-button>
      </div>
    </van-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      passwords: "",
      phone: "",
    };
  },
  methods: {
    onSubmit() {
      // console.log("submit", this.username);
      if (this.password != this.passwords) {
        this.$dialog.alert({
          message: "两次密码不同",
        });
      } else {
        let data = {
          username: this.username,
          password: this.password,
          passwords: this.passwords,
          phone: this.phone,
        };
        this.$api.addUser(data).then((response) => {
          this.$dialog
            .alert({
              message: response.data.msg,
            })
            .then(() => {
              // on close
              if (response.data.msg == "注册成功") {
                this.$router.push({ path: "/logIn" });
              }
            });
        });
      }
    },
    onClickLeft() {
      this.$router.push({ path: "/logIn" });
    },
  },
};
</script>

<style scoped>
.title /deep/ .van-nav-bar__content {
  background-color: #f2f2f2;
}
.title /deep/ .van-nav-bar__title {
  color: rgb(102, 102, 102);
}
.title /deep/ .van-nav-bar .van-icon {
  color: rgb(102, 102, 102);
}
</style>