<template>
  <div class="btn">
    <button id="btn"></button>
    <label class="label" for="btn" ref="btnText">{{ title }}</label>
  </div>
</template>

<script>
export default {
  name: 'loginBtn',
  // 定义默认的 button 内容为下一步
  props: {
    title: {
      type: String,
      default: '下一步'
    }
  }
}
</script>

<style lang="less" scoped>
@import url("~styles/global.less");
.btn {
  .flex-center();
  text-align: center;
  #btn {
    position: absolute;
    clip: rect(0, 0, 0, 0);
  }
  .label {
    box-sizing: border-box;
    margin-top: 30px;
    padding: 8px;
    border-radius: 20px;
    line-height: 20px;
    width: 80%;
    color: rgb(32, 32, 32);
    background: #cecfce;
  }
}
</style>
