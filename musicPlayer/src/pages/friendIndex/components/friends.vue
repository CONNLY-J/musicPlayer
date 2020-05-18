<template>
  <div id="attention">
    <ul class="friends">
     <li v-for="(item, index) in myFollowing" :key="index" class="friends-list">
       {{item.nickname}}
     </li>
    </ul>
    <should-login v-show="isLogin === 0"></should-login>
  </div>
</template>

<script>
// import Information from '../../../components/Information'
import api from 'api'
import shouldLogin from 'base/shouldLogin'

export default {
  name: "friends",
  components:{
    shouldLogin
  },
  data(){
      return{
          myFollowing:[],
          isLogin: +localStorage.getItem('loginState') || 0
      }
  },
  methods: {
    _getFindInfo (id) {
      let uid = localStorage.getItem('accountUid')
      id = id || uid
      api.userFollowsFn(id)
        .then(res => {
          // 接受数据
          const data = res.data
          // 查看返回数据的 code 状态，如果是 200 的话进行使用
          if (data.code === 200) {
        this.myFollowing = data.follow
        console.log(this.myFollowing)
      }
        })
        .catch(error => {
          console.log(error)
        })
    },
    // getFindInfoSuc (res) {
    //   if (res.status === 200 && res.statusText === 'OK') {
    //     res = res.data.myFollowing
    //     this.myFollowing = res
    //   }
    // }
  },
  mounted () {
    this._getFindInfo()
  }
}
</script>

<style scoped>
.attention{
border: #333333;
position: relative;
}
.friends{
  font-size: 20px;
  line-height: 40px;
  height: 40px;
  margin-left: 15px;
  margin-top: 10px;
}
.friends-list{
  border-bottom: solid 1px #a1a3a1;
  width: 350px;
}
</style>