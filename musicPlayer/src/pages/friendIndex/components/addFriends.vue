<template>
  <div id="attention">
    <p>你可能感兴趣的人</p>
    <ul class="friends">
     <li v-for="(item,index) in deFollow" class="friends-list" :key="index"
     >
       {{item.name}}
        <span class="add" v-show="!isSubInItem" @click="addPlaylist(item.id)">+ 关注</span>
        <span class="delete" v-show="isSubInItem" @click="deletePlaylist" >取消关注
          <!-- <i class="date-song wenjianjia"></i>
          {{subscribedCountItem | setCol}} -->
        </span>
      
     </li>
     
    </ul>
    
    <!-- <should-login v-show="isLogin === 0"></should-login> -->
  </div>
</template>

<script>
// import Information from '../../../components/Information'
import api from 'api'
// import shouldLogin from 'base/shouldLogin'

export default {
  name: "friends",
  components:{
    // shouldLogin
  },
  data(){
      return{
          deFollow:[
            {
              id:1,
              name:"焦迈奇"
            },
            // {
            //   id:2,
            //   name:"TroyeSivan"
            // },
            // {
            //   id:3,
            //   name:"TaylorSwift"
            // },
            // {
            //   id:4,
            //   name:"小头菜"
            // },
            // {
            //   id:5,
            //   name:"艾辰"
            // },
            // {
            //   id:6,
            //   name:"HHW"
            // },
            // {
            //   id:7,
            //   name:"皮卡丘多多"
            // },{
            //   id:8,
            //   name:"戴风-demo"
            // },
            // {
            //   id:9,
            //   name:"任然"
            // },
            // {
            //   id:10,
            //   name:"唐映枫"
            // },
            // {
            //   id:11,
            //   name:"Zealot"
            // },
            // {
            //   id:12,
            //   name:"bbnomula"
            // },
            // {
            //   id:13,
            //   name:"RealkSHMR"
            // }
            ],
          isLogin: +localStorage.getItem('loginState') || 0,
          isSubInItem:false,
          currentIndex:0
      }
  },
   
  methods: {
   addPlaylist:function(id) {
     for(var i=0;i<this.deFollow.length;i++){
       var id = this.deFollow[i].id;
      this.isSubInItem = true
       api.addOrDeleteFriendsListFn(1,id)
        .then(res => {
          const data = res.data
          if (data.code === 200) {
            this.isSubInItem = true
            // ++this.subscribedCountItem
          }
        })
     }
    },
    /**
     * 取消收藏歌单
     */
    deletePlaylist () {
      for(var i=0;i<this.deFollow.length;i++){
      const id = this.deFollow[i].id
      api.addOrDeletePlaylistFn(2, id)
        .then(res => {
          const data = res.data
          if (data.code === 200) {
            this.isSubInItem = false
            // --this.subscribedCountItem
          }
        })
      }
    },
  }
  // mounted () {
  //   this._getFollowInfo()
    
  // }
}
</script>

<style scoped>
.attention{
border: #333333;
position: relative;
}
p{
  font-size: 18px;
  padding-top: 10px;
  padding-left: 5px;
}
.friends{
  font-size: 15px;
  line-height: 40px;
  height: 40px;
  margin-left: 15px;
  margin-top: 10px;
}
.friends-list{
  border-bottom: solid 1px #a1a3a1;
  width: 350px;
}
.add,.delete{
  float: right;
  width: 60px;
  height: 25px;
  border: solid 1px #ff2121;
  color: #f84949;
  line-height: 30px;
  border-radius: 20%;
  display: flex;
  justify-content: space-around;
  align-items: center;

}

</style>