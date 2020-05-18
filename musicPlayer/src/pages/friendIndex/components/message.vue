<template>
  <div class="list-item">
     <ul class="msg">
         <li v-for="(item,index) in msgList" :key="index" class="msgContent" @click="sendMsg()">
            <p class="msgName">{{item.fromUser.nickname}}</p>
            <p class="msgDetail">{{item.lastMsg}}</p>
         </li>
     </ul>
     <router-view>
     </router-view>
  </div>
</template>

<script>
import api from 'api'
export default {
  name: "message",
  data(){
      return{
          msgList:[],
         
          avatarUrl: {},
      }
  },
  methods: {
    _getMsgInfo (id) {
      let uid = localStorage.getItem('accountUid')
      id = id || uid
      api.msgPrivateFn()
        .then(res => {
          // 接受数据
          const data = res.data
          // 查看返回数据的 code 状态，如果是 200 的话进行使用
          if (data.code === 200) {
        this.msgList = data.msgs
       
        // this.lastmsg = data.msgs.lastmsg
        
      }
        })
        .catch(error => {
          console.log(error)
        })
    },
    sendMsg(){
      this.$router.push({name:'sendMsg'})
     
    }
  },
  mounted () {
    this._getMsgInfo()
    // this._sendMsg()
  }
}
</script>

<style lang='less' scoped>
@import url("~styles/global.less");
@import url("//at.alicdn.com/t/font_1380711_cftenqb5flc.css");
.msg{
    width: 100%;
    height: 100%;
    position: relative;
}
.msg .msgContent{
    width: 350px;
    height: 50px;
    margin-left: 10px;
    margin-top: 8px;
    border-bottom: solid 1px #babbba
    
}
.msg .msgContent .msgName{
    padding-left: 10px;
    padding-top: 8px;
}
.msg .msgContent .msgDetail{
    
    height: 25px;
    line-height: 25px;
    overflow: hidden;
    font-size: 12px;
    color: #818381;
    padding-left: 10px;
}
</style>
