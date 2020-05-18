<template>
  <div class="wrapper" @click="goBack">
    <div class="phoneLogin" @click.stop="goPhone">手机号登陆</div>
  </div>
</template>

<script>
export default {
  name: 'loginPage',
  methods: {
    goBack () {
      history.go(-1)
    },
    goPhone () {
      this.$router.push('/phone')
    }
  }
}
</script>

<style lang="less" scoped>
@import url("~styles/global.less");

.wrapper {
  width: 100vw;
  height: 100vh;
  background-color: #fafdfa;
  display: flex;
  justify-content: center;
  align-items: center;
  .phoneLogin {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 5.3rem;
    height: 0.8rem;
    border-radius: 0.4rem;
    background-color: rgb(204, 200, 200);
    color: @bgcolor;
    font-weight: 500;
    letter-spacing: 3px;
  }
}
</style>
