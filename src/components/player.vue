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
.player-parent {
  max-height: 100vh;
  width: fit-content;
  grid-column-end: -1;
  z-index: 100;
  grid-row-start: 1;
  background-color: black;
  display: grid;
  grid-template-columns: auto;
}
.spinner {
  background: url("/img/load.gif") no-repeat center center;
  height: 700px;
}
.player {
  width: 320px;
  grid-column: 1/2;
  height: 100%;
  position: relative;
  background: url("/img/audio.gif") no-repeat center center;
}
.social {
  height: 50px;
}
.embed {
  grid-column: 2/-1;
  max-height: 100vh;
}
.grad {
  height: 100vh;
  width: 100%;
  background: linear-gradient(
    to bottom,
    rgba(36, 33, 33, 0.11) 0%,
    rgba(13, 12, 12, 0.678) 24%,
    rgba(10, 10, 10, 0.699) 51%,
    rgb(0, 0, 0) 80%,
    rgb(0, 0, 0) 100%
  );
  color: snow;
}
audio {
  border-radius: 0;
  color: black;
  position: absolute;
  bottom: 0;
  transform: translate(-50%);
  width: 100%;
}

.play-pause {
  height: 120px;
  width: 120px;
  border-radius: 50%;
  border: solid 10px snow;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.names {
  position: absolute;
  bottom: 25%;
  left: 50%;
  transform: translate(-50%, 50%);
}
.name {
  font-size: 1em;
  font-weight: bolder;
  top: 100%;
}
.freq {
  font-weight: 100;
  font-size: 0.9em;
}
.play {
  width: 0;
  height: 0;
  border-top: 30px solid transparent;
  border-bottom: 30px solid transparent;
  position: absolute;
  top: 50%;
  left: 55%;
  transform: translate(-50%, -50%);
  border-left: 40px solid snow;
}
.pause {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
.bar {
  height: 60px;
  width: 12px;
  border-top-left-radius: 25px;
  border-top-right-radius: 25px;
  border-bottom-left-radius: 25px;
  border-bottom-right-radius: 25px;
  background-color: snow;

  top: 50%;
  margin: 10px;
}
.social {
  display: inline;
  position: absolute;
  bottom: 1%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.social img {
  height: 40px;
  margin: 10px;
}
</style>
