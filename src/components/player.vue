<template>
  <div ref="palyerparent" class="player-parent">
    <div class="player">
      <div class="grad">
        <div
          class="play-pause"
          v-on:click="play=!play"
          :style="{ 'background-image': 'url('+image+')'}"
        >
          <div v-if="play" class="pause">
            <div class="bar"></div>
            <div class="bar"></div>
          </div>
          <div v-else class="play"></div>
        </div>
        <div class="names">
          <span class="name">{{name}}</span>
          <br>
          <span class="freq">{{freq}}</span>
        </div>
        <audio ref="audio" autoplay :src="currentUrl"></audio>

        <div class="social">
          <img src="/img/icons/twitter.png" v-on:click="social=!social">
         
        </div>
      </div>
    </div>
    <div v-if="social" class="embed" v-bind:style="{ width:width}">
      <Timeline :id="twit" :sourceType="'profile'" :options="{ theme: 'dark', height:'100vh' }">
        <div class="spinner"></div>
      </Timeline>
    </div>
  </div>
</template>

<script>
import { bus } from "../bus.js";
import { Timeline } from "vue-tweet-embed";
export default {
  components: {
    Timeline: Timeline
  },
  computed(){
    
  },
  data() {
    return {
      currentUrl:"https://streamingv2.shoutcast.com/nrg-radio-ke",
      image: "/img/nrg.webp",
      play: true,
      name: "NRG Radio",
      freq: "97.1 fm",
      twit: "NRGRadioKE",
      social: false,
      width: "500px"
    };
  },
  methods: {},
  created() {
    bus.$on("stationChanged", data => {
      this.currentUrl = data.url;
      this.image = data.image;
      this.name = data.name;
      this.freq = data.freq;
      this.twit = data.twit;
      this.social = data.social;
    });
  },
  mounted() {
    this.currentUrl = "https://streamingv2.shoutcast.com/nrg-radio-ke";
  },
  updated() {
    if (this.play == false) {
      this.$refs.audio.pause();
    } else {
      this.$refs.audio.play();
    }
    console.log(this.social);
    if (this.social == true) {
      this.width = "500px";
    } else {
      this.width = "0px";
    }
    this.reload;
  }
};
</script>
<style>
</style>
