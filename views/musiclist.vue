<template>
  <div class="musiclist">
    <div>
      <van-button plain type="primary" @click="gohead">返回</van-button>
    </div>
    <div class="zzc"></div>
    <div class="container">
      <div class="center-block">
        <div id="aplayer" class="aplayer aplayer-withlrc aplayer-withlist">
          <div
            class="aplayer-pic"
            style="background-image: url(&quot;https://api.hibai.cn/music/Music/Music?id=1345848098&amp;type=pic&quot;);"
          ></div>
          <div class="aplayer-info">
            <div class="aplayer-music">
              <span class="aplayer-title">绿色(纯歌版)</span>
              <span class="aplayer-author">陈雪凝</span>
            </div>
          </div>
          <div class="fix">
            <img class="img" :src="data.pbg[0]" alt>
            <img class="img" :src="data.pbg[1]" alt>
            <img class="img" :src="data.pbg[2]" alt>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapState } from "vuex";
import router from "vue-router";
import APlayer from "aplayer";
import { Toast } from "vant";
export default {
  name: "musiclist",
  // data() {
  //   return {
  //     id: "564801446"
  // 141998296
  // 3778678 云音乐热歌榜
  // 3779629 云音乐新歌榜
  // 2884035 网易原创歌曲榜
  // 991319590 江小白YOLO云音乐说唱榜
  // 2847251561 说唱TOP榜
  // 2250011882 抖音排行榜
  // 645765966 张国荣
  // 564801446 陈奕迅
  // 1081635 周二珂
  // 439937402 薛之谦
  // 988690134 百听不厌的老歌
  // 2111010477 舒缓减压催眠曲（纯音乐）
  // 2829998155 愿你知足且上进，温柔而坚定
  // 2324451155 华语民谣丨治愈孤独患者的暖心民谣歌单
  // 2440498598 听rapper说情话
  // 2232237850 耳朵喜欢你 好听到可以单曲循环
  // 411680085 全世界最好听的钢琴曲
  // 2602222983 精选 | 网络热歌分享
  // 2715933347 精选｜Cover的那些循环歌曲
  // 2142526217 能让你写代码写出拯救世界的感觉
  // 2417099944 『后驱车』 Music专属
  // 2511560749 温柔暴击 | 沉溺于男友音的甜蜜乡
  //   };
  // },
  computed: {
    ...mapState(["data"])
  },
  methods: {
    gohead() {
      this.$router.push({ name: "head" });
    }
  },
  mounted() {
    if (this.$route.params.id) {
      var music = new Array();
      $.ajax({
        type: "POST",
        url: "https://api.hibai.cn/api/index/index",
        dataType: "json",
        data: {
          TransCode: "020112",
          OpenId: "123456789",
          Body: { SongListId: this.$route.params.id },
          cache: 1
        },
        success: function(result) {
          var ap = new APlayer({
            element: document.getElementById("aplayer"),
            narrow: false,
            mutex: true,
            showlrc: 3,
            theme: "#e6d0b2",
            mode: "random",
            preload: "metadata",
            listmaxheight: "800px",
            music: result.Body
          });
        }
      });
    } else {
      Toast.fail({
        duration: 1000,
        message: "点击排行榜进入"
      });
      this.$router.push({ name: "head" });
    }
  }
};
</script>
<style scoped>
.img {
  width: 100%;
  margin: 0.19rem 0;
}
.out {
  background-color: rgba(163, 27, 27, 0.8);
  font-size: 0.25rem;
  height: 0.5rem;
  line-height: 0.5rem;
  color: #fff;
}
.zzc {
  z-index: 999;
  width: 0.2rem;
  height: 0.2rem;
  background-color: #fff;
  position: fixed;
  top: 2.05rem;
  right: 0.16rem;
}
.musiclist {
  background-color: #fff;
  color: #000;
}
.aplayer-narrow {
  width: 66px;
}
.aplayer-narrow .aplayer-info {
  display: none;
}

.aplayer-withlrc.aplayer-narrow {
  width: 90px;
}

.aplayer-withlrc.aplayer .aplayer-pic {
  height: 90px;
  width: 90px;
}

.aplayer-withlrc.aplayer .aplayer-info {
  margin-left: 90px;
  height: 90px;
}

.aplayer-withlrc.aplayer .aplayer-lrc {
  display: block;
}

.aplayer-withlrc.aplayer .aplayer-info {
  padding: 10px 7px 0 7px;
}

.aplayer-withlist.aplayer .aplayer-info {
  border-bottom: 1px solid #e9e9e9;
}

.aplayer-withlist.aplayer .aplayer-list {
  display: block;
}

.aplayer-withlist.aplayer .aplayer-icon-menu {
  display: inline !important;
}

.aplayer {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0 !important;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
  border-radius: 2px;
  overflow: hidden;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  line-height: initial;
}
.aplayer * {
  box-sizing: content-box;
}
.aplayer .aplayer-icon {
  width: 15px;
  height: 15px;
  border: none;
  background-color: transparent;
  outline: none;
  cursor: pointer;
  opacity: 0.8;
  vertical-align: middle;
  padding: 0;
  font-size: 12px;
  display: inline;
}
.aplayer .aplayer-icon .aplayer-fill {
  -webkit-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
}
.aplayer .aplayer-lrc-content {
  display: none;
}
.aplayer .aplayer-pic {
  position: relative;
  float: left;
  height: 66px;
  width: 66px;
  background-image: url(data:image/jpeg;base64,/9j/4QAYRXhpZgAASUkqAAgAAAAAAAAAAAAAAP/sABFEdWNreQABAAQAAAAeAAD/4QMfaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wLwA8P3hwYWNrZXQgYmVnaW49Iu+7vyIgaWQ9Ilc1TTBNcENlaGlIenJlU3pOVGN6a2M5ZCI/PiA8eDp4bXBtZXRhIHhtbG5zOng9ImFkb2JlOm5zOm1ldGEvIiB4OnhtcHRrPSJBZG9iZSBYTVAgQ29yZSA1LjYtYzA2NyA3OS4xNTc3NDcsIDIwMTUvMDMvMzAtMjM6NDA6NDIgICAgICAgICI+IDxyZGY6UkRGIHhtbG5zOnJkZj0iaHR0cDovL3d3dy53My5vcmcvMTk5OS8wMi8yMi1yZGYtc3ludGF4LW5zIyI+IDxyZGY6RGVzY3JpcHRpb24gcmRmOmFib3V0PSIiIHhtbG5zOnhtcE1NPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvbW0vIiB4bWxuczpzdFJlZj0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL3NUeXBlL1Jlc291cmNlUmVmIyIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bXBNTTpEb2N1bWVudElEPSJ4bXAuZGlkOjE2NjQ3NUZBM0Y4RDExRTY4NzJCRDdCNkZCQTQ0MjNBIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjE2NjQ3NUY5M0Y4RDExRTY4NzJCRDdCNkZCQTQ0MjNBIiB4bXA6Q3JlYXRvclRvb2w9IkFkb2JlIFBob3Rvc2hvcCBDQyAyMDE1IE1hY2ludG9zaCI+IDx4bXBNTTpEZXJpdmVkRnJvbSBzdFJlZjppbnN0YW5jZUlEPSI5OENEMEFFRjM0NTI1NjE0NEREQkU4RjkxRjAwNjM3NiIgc3RSZWY6ZG9jdW1lbnRJRD0iOThDRDBBRUYzNDUyNTYxNDREREJFOEY5MUYwMDYzNzYiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz7/7gAOQWRvYmUAZMAAAAAB/9sAhAAQCwsLDAsQDAwQFw8NDxcbFBAQFBsfFxcXFxcfHhca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);
  background-size: 100%;
  -webkit-transition: all 0.3s ease;
  transition: all 0.3s ease;
}
.aplayer .aplayer-pic .aplayer-button {
  position: absolute;
  border-radius: 50%;
  opacity: 0.8;
  cursor: pointer;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  background: rgba(0, 0, 0, 0.2);
  -webkit-transition: all 0.1s ease;
  transition: all 0.1s ease;
}
.aplayer .aplayer-pic .aplayer-button:hover {
  opacity: 1;
}
.aplayer .aplayer-pic .aplayer-button .aplayer-fill {
  fill: #fff;
}
.aplayer .aplayer-pic .aplayer-hide {
  display: none;
}
.aplayer .aplayer-pic .aplayer-play {
  width: 26px;
  height: 26px;
  border: 2px solid #fff;
  bottom: 50%;
  right: 50%;
  margin: 0 -15px -15px 0;
}
.aplayer .aplayer-pic .aplayer-play .aplayer-icon-play {
  position: absolute;
  top: 3px;
  left: 4px;
  height: 20px;
  width: 20px;
}
.aplayer .aplayer-pic .aplayer-pause {
  width: 16px;
  height: 16px;
  border: 2px solid #fff;
  bottom: 4px;
  right: 4px;
}
.aplayer .aplayer-pic .aplayer-pause .aplayer-icon-pause {
  position: absolute;
  top: 2px;
  left: 2px;
  height: 12px;
  width: 12px;
}
.aplayer .aplayer-info {
  margin-left: 66px;
  padding: 14px 7px 0 10px;
  height: 66px;
  box-sizing: border-box;
}
.aplayer .aplayer-info .aplayer-music {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  margin: 0 0 13px 5px;
  -webkit-user-select: text;
  -moz-user-select: text;
  -ms-user-select: text;
  user-select: text;
  cursor: default;
  padding-bottom: 2px;
}
.aplayer .aplayer-info .aplayer-music .aplayer-title {
  font-size: 14px;
}
.aplayer .aplayer-info .aplayer-music .aplayer-author {
  font-size: 12px;
  color: #666;
}
.aplayer .aplayer-info .aplayer-controller {
  position: relative;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-bar-wrap {
  margin: 0 0 0 5px;
  padding: 4px 0;
  cursor: pointer !important;
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-bar-wrap .aplayer-bar {
  position: relative;
  height: 2px;
  width: 100%;
  background: #cdcdcd;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-bar-wrap
  .aplayer-bar
  .aplayer-loaded {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  background: #aaa;
  height: 2px;
  -webkit-transition: all 0.5s ease;
  transition: all 0.5s ease;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-bar-wrap
  .aplayer-bar
  .aplayer-played {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  height: 2px;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-bar-wrap
  .aplayer-bar
  .aplayer-played
  .aplayer-thumb {
  position: absolute;
  top: 0;
  right: 5px;
  margin-top: -4px;
  margin-right: -10px;
  height: 8px;
  width: 8px;
  border-radius: 50%;
  background: #fff;
  cursor: pointer !important;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-time {
  position: relative;
  right: 0;
  bottom: 3px;
  height: 17px;
  color: #999;
  font-size: 11px;
  padding-left: 7px;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-time .aplayer-time-inner {
  vertical-align: middle;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-time .aplayer-icon {
  cursor: pointer;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time
  .aplayer-icon
  .aplayer-fill {
  fill: #666;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time
  .aplayer-icon.aplayer-icon-mode {
  margin-right: 4px;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time
  .aplayer-icon:hover
  .aplayer-fill {
  fill: #000;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time
  .aplayer-icon.aplayer-icon-menu {
  display: none;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time.aplayer-time-narrow
  .aplayer-icon-mode {
  display: none;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-time.aplayer-time-narrow
  .aplayer-icon-menu {
  display: none;
}
.aplayer .aplayer-info .aplayer-controller .aplayer-volume-wrap {
  position: relative;
  display: inline-block;
  margin-left: 3px;
  cursor: pointer !important;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-volume-wrap:hover
  .aplayer-volume-bar-wrap {
  display: block;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-volume-wrap
  .aplayer-volume-bar-wrap {
  display: none;
  position: absolute;
  bottom: 15px;
  right: -3px;
  width: 25px;
  height: 40px;
  z-index: 99;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-volume-wrap
  .aplayer-volume-bar-wrap
  .aplayer-volume-bar {
  position: absolute;
  bottom: 0;
  right: 10px;
  width: 5px;
  height: 35px;
  background: #aaa;
}
.aplayer
  .aplayer-info
  .aplayer-controller
  .aplayer-volume-wrap
  .aplayer-volume-bar-wrap
  .aplayer-volume-bar
  .aplayer-volume {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 5px;
  -webkit-transition: all 0.1s ease;
  transition: all 0.1s ease;
}
.aplayer .aplayer-lrc {
  display: none;
  position: relative;
  height: 30px;
  text-align: center;
  overflow: hidden;
  margin: -10px 0 7px;
}
.aplayer .aplayer-lrc:before {
  position: absolute;
  top: 0;
  z-index: 1;
  display: block;
  overflow: hidden;
  width: 100%;
  height: 10%;
  content: " ";
  background: -webkit-linear-gradient(
    top,
    white 0%,
    rgba(255, 255, 255, 0) 100%
  );
  background: linear-gradient(to bottom, white 0%, rgba(255, 255, 255, 0) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ffffff', endColorstr='#00ffffff',GradientType=0 );
}
.aplayer .aplayer-lrc:after {
  position: absolute;
  bottom: 0;
  z-index: 1;
  display: block;
  overflow: hidden;
  width: 100%;
  height: 33%;
  content: " ";
  background: -webkit-linear-gradient(
    top,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.8) 100%
  );
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.8) 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#00ffffff', endColorstr='#ccffffff',GradientType=0 );
}
.aplayer .aplayer-lrc p {
  font-size: 12px;
  color: #666;
  line-height: 16px !important;
  height: 16px !important;
  padding: 0 !important;
  margin: 0 !important;
  -webkit-transition: all 0.5s ease-out;
  transition: all 0.5s ease-out;
  opacity: 0.4;
  overflow: hidden;
}
.aplayer .aplayer-lrc p.aplayer-lrc-current {
  opacity: 1;
  overflow: visible;
  height: initial !important;
}
.aplayer .aplayer-lrc .aplayer-lrc-contents {
  width: 100%;
  -webkit-transition: all 0.5s ease-out;
  transition: all 0.5s ease-out;
  -webkit-user-select: text;
  -moz-user-select: text;
  -ms-user-select: text;
  user-select: text;
  cursor: default;
}
.aplayer .aplayer-list {
  overflow: auto;
  -webkit-transition: all 0.5s ease;
  transition: all 0.5s ease;
  will-change: height;
  display: none;
}
.aplayer .aplayer-list.aplayer-list-hide {
  height: 0 !important;
}
.aplayer .aplayer-list::-webkit-scrollbar {
  width: 5px;
}
.aplayer .aplayer-list::-webkit-scrollbar-track {
  background-color: #f9f9f9;
}
.aplayer .aplayer-list::-webkit-scrollbar-thumb {
  border-radius: 3px;
  background-color: #eee;
}
.aplayer .aplayer-list::-webkit-scrollbar-thumb:hover {
  background-color: #ccc;
}
.aplayer .aplayer-list ol {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.aplayer .aplayer-list ol li {
  position: relative;
  height: 32px;
  line-height: 32px;
  padding: 0 15px;
  font-size: 12px;
  border-top: 1px solid #e9e9e9;
  cursor: pointer;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
  overflow: hidden;
}
.aplayer .aplayer-list ol li:first-child {
  border-top: none;
}
.aplayer .aplayer-list ol li:hover {
  background: #efefef;
}
.aplayer .aplayer-list ol li.aplayer-list-light {
  background: #e9e9e9;
}
.aplayer .aplayer-list ol li.aplayer-list-light .aplayer-list-cur {
  display: inline-block;
}
.aplayer .aplayer-list ol li .aplayer-list-cur {
  display: none;
  width: 3px;
  height: 22px;
  position: absolute;
  left: 0;
  top: 5px;
  cursor: pointer;
}
.aplayer .aplayer-list ol li .aplayer-list-index {
  color: #666;
  margin-right: 12px;
  cursor: pointer;
}
.aplayer .aplayer-list ol li .aplayer-list-author {
  color: #666;
  float: right;
  cursor: pointer;
}

@-webkit-keyframes aplayer-roll {
  0% {
    left: 0;
  }
  100% {
    left: -100%;
  }
}

@keyframes aplayer-roll {
  0% {
    left: 0;
  }
  100% {
    left: -100%;
  }
}
</style>


