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
          <img src="/img/icons/facebook.png">
        </div>
      </div>
    </div>
    <div v-if="social" class="embed" v-bind:style="{ width:width}">
      <Timeline :id="twit" :sourceType="'profile'" :options="{ theme: 'dark', height:'725' }">
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
  data() {
    return {
      currentUrl: "https://icecast2.getstreamhosting.com:8050/stream.mp3",
      image: "/img/capital.jpg",
      play: true,
      name: "Capital fm",
      freq: "98.5",
      twit: "CapitalFMKenya",
      social: false,
      width: 0
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
  mounted() {},
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
