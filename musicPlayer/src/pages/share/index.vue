<template>
  <div>
    <div class="bdsharebuttonbox">

      <!-- 以下链接和setShare()中的bdSelectMiniList属性相对应 -->
      <a href="#" class="bds_more" data-cmd="more"></a>
      <a href="http://127.0.0.1:8081/#/albumPage" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a>
      <a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a>
      <a href="#" class="bds_tqq" data-cmd="tqq" title="分享到腾讯微博"></a>
      <a href="#" class="bds_renren" data-cmd="renren" title="分享到人人网"></a>
      <a href="#" class="bds_weixin" data-cmd="weixin" title="分享到微信"></a>
    </div>
  </div>
</template>

<script>
export default {
  name: "share",
  data() {
    return {};
  },
  mounted: function() {
    const that = this;
    setTimeout(() => {
      that.setShare();
    }, 0);
  },
  methods: {
    setShare() {
      //分享相关代码
      window._bd_share_config = {
        common: {
          bdSnsKey: {},
          bdText: "",
          bdMini: "1",
          bdMiniList: false,
          bdPic: "",
          bdStyle: "1",
          bdSize: "24"
        },
        share: {},
        selectShare: {
          bdContainerClass: null,
          // 这里和html标签里链接相对应
          bdSelectMiniList: ["sqq", "qzone", "tsina", "renren","weixin"]
        }
      };
      const s = document.createElement("script");
      s.type = "text/javascript";
      s.src =
        "/static/api/js/share.js?v=89860593.js?cdnversion=" +
        ~(-new Date() / 36e5);
      document.body.appendChild(s);

      // 百度分享有自动销毁的逻辑，加这么一段代码   重新初始化就没问题了。
      if (window._bd_share_main) {
        window._bd_share_main.init();
      }
    }
  }
};
</script>

<style scoped>
.bdsharebuttonbox {
  width: 200px;
  height: 40px;
  line-height: 60px;
  /* background: #fff; */
  border: 1px solid #666;
  /* position: fixed;
  bottom: 36px;
  right: 0; */
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>