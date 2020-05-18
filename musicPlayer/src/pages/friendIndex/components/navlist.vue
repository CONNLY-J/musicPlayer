<template>

  <div class="wrapper pd23" ref="navs">

    <!-- 使用 replace 它不会向 history 添加新记录 -->

    <router-link

      :to="item.text | setPage"

      class="nav-list"

      v-for="(item, index) in list"

      :key="index"

      exact

      replace

    >{{ item.text }}</router-link>

    <!-- <span class="more">

      <i class="recommend ziyuanxhdpi"></i>

    </span> -->

  </div>

</template>



<script>

export default {

  name: '',

  methods: {

    handleScroll (index) {

      this.$refs.navs.scrollLeft = index * 85

    },

    getPage (val) {

      let index = this.toLink.indexOf(val)

      this.handleScroll(index)

    }

  },

  filters: {

    setPage: function (val) {

      if (val) {

        if (val === '好友列表') {

          val = '/friends'

        } else if (val === '消息') {

          val = '/message'

        } else {

          val = '/addFriends'

        }

      }

      return val

    }

  },

  data () {

    return {

      linkPage: '',

      list: [

        {

          text: '好友列表'

        }, {

          text: '消息'

        }, {

          text: '添加好友'

        }

      ]

    }

  }

}

</script>



<style lang='less' scoped>

@import url("~styles/global.less");

.wrapper {

  position: relative;

  display: flex;

  flex-wrap: nowrap;

  box-sizing: border-box;

  margin-top: 0.16rem;

  overflow-x: auto;

  border-bottom: 1px solid #ddd;

  margin-right: 0.3rem;

  .nav-list {

    position: relative;

    display: flex;

    justify-content: center;

    align-items: center;

    min-width: 1.2rem;

    height: 0.7rem;

    box-sizing: border-box;

    padding: 0.03rem;

    margin: 0 0.5rem;

    color: #000;

    &::before {

      content: "";

      position: absolute;

      bottom: 0;

      left: 0;

      right: 0;

      height: 2px;

      background-color: @bgcolor;

      transform-origin: bottom right;

      transform: scaleX(0);

      transition: transform 0.5s ease;

    }

    &.ac {

      color: @bgcolor;

    }

    &.ac::before {

      transform-origin: bottom left;

      transform: scaleX(1);

    }

  }

  .more {

    position: fixed;

    right: 8px;

    top: 1.3rem;

    // transform: translateY(-50%);

    .recommend {

      font-size: 0.4rem;

    }

  }

}

::-webkit-scrollbar {

  display: none;

}

</style>