<template>
  <div>
    <div class="load" v-show="loading">
      <!-- <page-loading></page-loading> -->
    </div>
    <div v-show="!loading">
      <audio-all-title @beginAudioAll="beginAudioAll" :trackCount="trackCount" class="titleMt"></audio-all-title>
      <song-list
        v-for="(item, index) in chineseList"
        :key="index"
        :songName="item.name"
        :artists="item.artists"
        :albumName="item.album.name"
        :imgUrl="item.album.picUrl"
        @beginSong="setAudioList(item, index)"
        @showSlider="showSlider"
        :nowSong="item.id === audioSong.id"
      ></song-list>
      <slider
      ref="slider"
      :title="title"
      :id="id"
      :homeFavoritelistSlider="homeFavoritelistSlider"
      :homePlaylistSlider="homePlaylistSlider"
    ></slider>
    </div>
  </div>
</template>

<script>
import api from 'api'
import audioAllTitle from 'base/audioAllTitle'
// import pageLoading from 'base/pageLoading'
import songList from 'base/song'
import slider from 'base/slider'
import { mapActions, mapGetters } from 'vuex'

export default {
  name: '',
  data () {
    return {
      trackCount: 0,
      chineseList: [],
      loading: true,
       title: '',
      id: 0,
       homePlaylistSlider: false,
      homeFavoritelistSlider: false
    }
  },
  computed: {
    ...mapGetters({ audioSong: 'AUDIO_ING_SONG' })
  },
  created () {
    this._getChineseInfo(7)
  },
  methods: {
    /**
     * 获取相关数据
     * @param {Number} type 接口参数
     */
    _getChineseInfo (type) {
      api.newSongsFn(type)
        .then(res => {
          const data = res.data
          if (data.code === 200) {
            this.chineseList = data.data
            this.trackCount = data.data.length
            this.loading = false
          }
        })
    },
    beginAudioAll () {
      this.startPlayAll({
        list: this.chineseList
      })
    },
    setAudioList (item, index) {
      this.selectPlay({
        list: this.chineseList,
        index
      })
    },
    showSlider (name, id, type) {
      this.title = '歌曲：' + name
      this.id = id
      if (type) {
        this.homeFavoritelistSlider = true
        this.homePlaylistSlider = false
      } else {
        this.homeFavoritelistSlider = false
        this.homePlaylistSlider = true
      }
      this.$refs.slider.showSlider()
    },
    ...mapActions(['selectPlay', 'startPlayAll'])
  },
  components: {
    audioAllTitle,
    songList,
    slider
    // pageLoading
  }
}
</script>

<style lang='less' scoped>
.titleMt {
  margin-top: 0.2rem;
}
</style>
