<template>
  <list-global
    title="视频"
    :more="videoList.more"
    :moreText="videoList.moreText"
    linkPage="video"
    :keyW="keyword"
  >
    <list-con
      :videoList="true"
      v-for="(item, index) in videoList"
      :key="index"
      @click.native="toVideoCom(item.vid)"
      line="two"
      :ImgUrl="item.coverUrl"
      :name="item.title"
      :isMv="item.vid.length < 20"
      :durationms="item.durationms"
      :nicknames="item.creator"
      :playTime="item.playTime"
    ></list-con>
  </list-global>
</template>

<script>
import listCon from 'base/interchangeable'
import listGlobal from 'base/titleFooter'

export default {
  name: '',
  components: {
    listCon,
    listGlobal
  },
  props: {
    videoList: {
      type: Array
    },
    keyword: {
      type: String
    }
  },
  methods: {
    toVideoCom (id) {
      this.$router.push({ name: 'videoComments', params: { id } })
    }
  }
}
</script>

<style lang='less' scoped>
.video-list {
  margin-top: 0.26rem;
  .title {
    height: 0.3rem;
    line-height: 0.3rem;
  }
  .more {
    height: 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 0.26rem;
    color: #ccc;
    .youjiantou {
      color: #aaa;
    }
  }
}
</style>
