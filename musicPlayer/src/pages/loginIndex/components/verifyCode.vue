<template>
  <div class="code">
    <van-password-input
      :value="value"
      :length="4"
      :gutter="15"
      :focused="showKeyboard"
      @focus="showKeyboard = true"
    />
    <van-number-keyboard
      :show="showKeyboard"
      @input="onInput"
      @delete="onDelete"
      @blur="showKeyboard = false"
    />
  </div>
</template>

<script>
import api from 'api'
import { Toast } from 'vant'
import { getPhone } from 'utils/getPhone'

export default {
  name: 'verifyCode',
  data () {
    return {
      value: '',
      showKeyboard: true
    }
  },
  methods: {
    async onInput (key) {
      this.value = (this.value + key).slice(0, 4)
      if (this.value.length === 4) {
        const phone = getPhone()
        const captcha = this.value
        try {
          const { data } = await api.verifyFn(phone, captcha)
          if (data.code === 200) {
            Toast('验证成功')
          }
        } catch (error) {
          if (error) {
            Toast(error.msg || '验证失败')
            this.value = ''
          }
        }
      }
    },
    onDelete () {
      this.value = this.value.slice(0, this.value.length - 1)
    }
  }

}
</script>

<style lang="less" scoped>
.code /deep/ li {
  border-bottom: 2px solid #aaa;
}
</style>
