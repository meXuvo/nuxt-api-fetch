<template>
  <div class="player-container">
<div></div>
    <client-only>
      <vue-core-video-player
        :core="HLSCore"
        src="https://bitdash-a.akamaihd.net/content/MI201109210084_1/m3u8s/f08e80da-bf1d-4e3d-8899-f0f6155f6efa.m3u8"
      ></vue-core-video-player>
    </client-only>
  </div>
</template>

<script>
// import Vue from 'vue'
// if (process.client) {
const HLSCore = require('@core-player/playcore-hls')
// Vue.use(HLSCore)
// import HLSCore from '@core-player/playcore-hls'
// }

export default {
  data() {
    return {
      HLSCore,
      // Hl: null,
      // Hl: HLSCore,
    }
  },
  computed: {
    // hsl() {
    //   // const HLSCore = require('@core-player/playcore-hls')
    //   const hl = HLSCore
    //   return hl
    // },
  },
  mounted() {
    // if (process.client) {
    // const HLSCore = require('@core-player/playcore-hls')
    // Vue.use(HLSCore)
    // import HLSCore from '@core-player/playcore-hls'
    // this.Hl = HLSCore
    // }
    // this.Hl = HLSCore
  },
  // methods: {
  //   hsl() {
  //     return HLSCore
  //   },
  // },
  // created() {
  //   if (process.client) {
  //     this.Hl = HLSCore
  //   }
  // },
}
</script>

<style></style>
