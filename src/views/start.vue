<!--
 * @Description: 
 * @version: 
 * @Author: ximusunian
 * @Date: 2020-12-02 09:41:18
 * @LastEditors: ximusunian
 * @LastEditTime: 2020-12-03 16:02:54
-->
<template>
  <div id="start">
    <div class="btn" @click="start">立即赚钱</div>
    <van-overlay
      :show="noOpen"
      @click="closeBox"
    >
      <div class="network_box">
        <div class="box">
          <div class="top">
            <img src="@/assets/images/net_close.png" class="close_img" @click="closeBox"/>
          </div>
          <img src="@/assets/images/net_logo.png" class="new_logo" />
          <div class="tips">
            <p>请手动打开第三方app</p>
          </div>
        </div>
      </div>
    </van-overlay>
  </div>
</template>

<script>
import {Overlay} from "vant"
export default {
  name: "start",
  data() {
    return {
      noOpen: false
    };
  },
  components: {
    [Overlay.name]: Overlay,
  },
  watch: {},
  created() {
    let _this = this
    window["hasOpen"] = function(result) {
      if(result != 1) {
        _this.noOpen = true
      }
    }
  },
  mounted() {},
  methods: {
    start() {
      window.webkit.messageHandlers.openApp.postMessage({});
    },
    closeBox() {
      this.noOpen = false
    }
  },
};
</script>

<style scoped lang="scss">
#start {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .btn {
    width: 65%;
    height: 35px;
    color: #fff;
    font-size: 16px;
    text-align: center;
    line-height: 35px;
    border-radius: 35px;
    background-image: linear-gradient(#fb6823, #f4370f);
    margin-top: 30px;
  }
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
    }
  }
}
}
</style>

