<template>
  <div class="wrapper">
    <general-nav @returnPage="returnPage" class="titleFixed">
      <!-- 通过改变 listFixed 来控制 title 的显示与否-->
      <span class="text">发送消息</span>
    </general-nav>
    <!-- <div class="split"></div> -->
    <!-- <page-loading v-show="load"></page-loading> -->
    <div class="msgcenter">
      <ul class="ulmsg">
        <li class="msg-item" v-for="item in msgList">
          <p>{{msgList}}</p>
        </li>
      </ul>
    </div>
    <van-search
      class="border-top commentInp"
      v-model="input"
      :placeholder="placeholder"
      show-action
      :clearable="false"
      background="#fff"
      left-icon
      @search="pushMsg(input)"
    >
      <div slot="action" :class="{disable: !input}" @click="pushMsg(input)">发送</div>
    </van-search>
     
  </div>
</template>

<script>
import { Toast } from 'vant'
import generalNav from 'base/generalNav'
// import pageLoading from 'base/pageLoading'
import api from 'api'
export default {
  name: 'sendMsg',
  data () {
    return {
      // isShow: false,
      load: true,
      input: '',
      placeholder: '',
      msgList:{}
      // visible:false
    }
  },
  // activated () {
  //   this.load = true
  //   this.params = this.$route.params
  //   const params = this.params
  //   if (Object.keys(params).length === 0) {
  //     this.$router.back()
  //   }
  // },
  methods: {
    pushMsg (id,msg) {
      Toast.allowMultiple()
      let loadingToast = Toast.loading({
        forbidClick: true,
        duration: 1000
      })
      const params = this.params
      let user_ids = localStorage.getItem('accountUid')
      id = id || user_ids
      api.pushMsgFn(id, msg)
        .then(res => {
          const { data } = res
          console.log(data)
          if (data.code === 200) {
            this.input = ''
           
            loadingToast.clear()
            Toast({
              position: 'bottom',
              message: '发送成功'
            })
            // this.pushMsgInCon(params)
            //  this.msgList = this.input
          }
        })
        .catch(err => {
          if (err) {
            loadingToast.clear()
            Toast(err.msg || '发送失败')
          }
        })
        this.msgList = this.input
    },
   
    returnPage () {
      this.$router.go(-1)
    }
  },
  components: {
    generalNav,
    
    // pageLoading,
    
  }
}
</script>

<style lang='less' scoped>
@import url("~styles/global.less");
.wrapper {
  background-color: #f1f5f1;
  .text {
    font-size: 0.3rem;
  }
  .titleFixed{
    background-color: #f9fcf9
  }
  .msgcenter{
    width: 370px;
    height: 400px;
    // border: solid 1px #00ff00;
    .msg-item{
    float: right;
    font-size: 16px;
    // padding-right: 20px;
    // padding-top: 10px;
    border: 1px solid #b8b6b6;
    border-radius: 20%;
    margin-right: 20px;
    margin-top: 10px;
    // width: 40px;
    height: 25px;
    line-height: 25px;
    text-align: center
  }
  }
  
  .commentInp {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    // z-index: 1;
    // .disable {
    //   color: #ccc;
    // }
  }
}
</style>
