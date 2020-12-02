<!--
 * @Description: 
 * @version: 
 * @Author: ximusunian
 * @Date: 2020-11-30 16:57:49
 * @LastEditors: ximusunian
 * @LastEditTime: 2020-12-01 17:03:40
-->
<template>
  <div class="network_box">
    <div class="box">
      <div class="top">
        <img src="@/assets/images/net_close.png" class="close_img" @click="closeBox"/>
      </div>
      <img src="@/assets/images/net_logo.png" class="new_logo" />
      <div class="bottom" v-if="type == 1">
        <div class="tips">
          <p>需要开启助手才能做任务</p>
          <p>如打开失败，请重新安装</p>
        </div>
        <div class="operation">
          <span class="download" @click="download">重新下载</span>
          <span class="wake" @click="openApp">打开助手</span>
        </div>
      </div>
      <div v-if="type == 0">
        <div class="tips">
          <p>需要开启助手才能做任务</p>
        </div>
        <div class="operation1" style="text-align: center">
          <span class="wake" id="newDownload" @click="download">立即安装</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Clipboard from "clipboard";
import {Overlay} from "vant"
export default {
  name: "install",
  props: {
    type: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      netWork: this.$store.state.netWork,
      downloadUrl: ""
    }
  },
  components: {
    [Overlay.name]: Overlay,
  },
  watch: {},
  mounted() {},
  methods: {
    closeBox() {
      this.$store.commit("setNetWork", false)
      location.reload()
    },
    download() {
      let channelKey = localStorage.getItem("channelKey")
      let channelUid = localStorage.getItem("channelUid")
      let str = `**channelKey=${channelKey}&&channelUid=${channelUid}**`
      let clipboard = new Clipboard("#newDownload", {
        text:() => {
            return str;
          }
      });
      clipboard.on("success", function() {
        console.log("success");
      });
      clipboard.on("error", function() {
        console.log("error");
      });
      this.$api.getInstallUrl().then(res => {
        if(res.success) {
          // window.location = res.result
          window.location = "https://apps.apple.com/cn/app/id1535787537"
        }
      })
    },
    openApp() {
      window.location = "com.BoyEye.cn:/"
    }
  }
}
</script>

<style scoped lang="scss">
.network_box {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  .box {
    width: 74%;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0.453rem 0.426rem 0.666rem;
    background-color: #ffffff;
    border-radius: 0.2rem;
    .top {
      display: flex;
      justify-content: flex-end;
      width: 100%;
    }
    .close_img {
      width: 0.53rem;
      height: 0.53rem;
      right: 0.2rem;
    }
    .new_logo {
      width: 2.4rem;
      height: 2.4rem;
      margin-top: 0.48rem;
    }
    .tips {
      color: #333;
      font-size: 0.426rem;
      margin-top: 0.933rem;
      text-align: center;
    }
    .bottom {
      width: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
    .operation {
      width: 100%;
      display: flex;
      justify-content: space-between;
      margin-top: 0.8133rem;
      font-size: 0.48rem;
      span {
        width: 3.2rem;
        height: 1rem;
        border-radius: 1rem;
        line-height: 1rem;
        text-align: center;
      }
      .download {
        color: #F4370F;
        border: 1px solid #F4370F;
      }
      .wake {
        color: white;
        background-image: linear-gradient(#FB6823, #F4370F);
      }
    }
    .operation1 {
      width: 100%;
      display: flex;
      justify-content: center;
      margin-top: 0.8133rem;
      font-size: 0.48rem;
      span {
        width: 3.2rem;
        height: 1rem;
        border-radius: 1rem;
        line-height: 1rem;
        text-align: center;
      }
      .wake {
        color: white;
        background-image: linear-gradient(#FB6823, #F4370F);
      }
    }
  }
}
</style>
