<template>
  <div class="player-parent">
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
      </div>
    </div>
  </div>
</template>

<script>
import { bus } from "../bus.js";

export default {
  data() {
    return {
      currentUrl: "https://icecast2.getstreamhosting.com:8050/stream.mp3",
      image: "/img/capital.jpg",
      play: true,
      name: "Capital fm",
      freq: "98.5"
    };
  },
  methods: {},
  created() {
    bus.$on("stationChanged", data => {
      this.currentUrl = data.url;
      this.image = data.image;
      this.name = data.name;
      this.freq = data.freq;
    });
  },
  updated() {
    if (this.play == false) {
      this.$refs.audio.pause();
    } else {
      this.$refs.audio.play();
    }
  }
};
</script>
<style>
.player-parent {
  height: 100%;
  width: 320px;
  grid-column-end: -1;
  z-index: 100;
  grid-row-start: 1;
  background-color: black;
}
.player {
  height: 100%;
  position: relative;
  background: url("/img/audio.gif") no-repeat center center;
}
.grad {
  height: 100%;
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
  bottom: 20%;
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
</style>
