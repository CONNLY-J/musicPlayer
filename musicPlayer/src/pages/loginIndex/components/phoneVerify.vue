<template>
  <account-login>
    <div class="wrapper">
      <verify-info></verify-info>
      <verify-code></verify-code>
    </div>
  </account-login>
</template>

<script>
import verifyInfo from './verifyInfo'
import verifyCode from './verifyCode'
import accountLogin from './accountLogin'
export default {
  name: 'phoneVerify',
  components: {
    verifyInfo,
    verifyCode,
    accountLogin
  }
}
</script>

<style lang="less" scoped>
.wrapper {
  box-sizing: border-box;
  padding: 0.23rem;
}
</style>
