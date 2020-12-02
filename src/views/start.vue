<!--
 * @Description: 
 * @version: 
 * @Author: ximusunian
 * @Date: 2020-12-02 09:41:18
 * @LastEditors: ximusunian
 * @LastEditTime: 2020-12-02 10:13:00
-->
<template>
  <div id="start">
    <input value="**channelKey=111&&channelUid=222**" style="width: 100%;"/>
    <div class="btn" @click="start">立即赚钱</div>
  </div>
</template>

<script>
export default {
  name: "start",
  data() {
    return {};
  },
  components: {},
  watch: {},
  mounted() {},
  methods: {
    start() {
      window.webkit.messageHandlers.startPlay.postMessage({});
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
}
</style>

