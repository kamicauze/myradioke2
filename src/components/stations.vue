<template>
  <div class="stations">
    <div ref="top" class="top">
      <iframe :src="currentWeb"></iframe>
    </div>
    <div class="channels">
      <stationcard v-for="station in stations" :station="station" :key="station.url"></stationcard>
    </div>
  </div>
</template>
<script>
import data from "../assets/data/radios.json";
import stationcard from "./stationcard.vue";
import { setInterval, clearTimeout } from "timers";
import { bus } from "../bus.js";

export default {
  components: {
    stationcard: stationcard
  },
  data() {
    return {
      stations: [],
      back: "img/wonan/wonan0.jpg",
      ImagesF: [
        "/img/wonan/wonan0.jpg",
        "/img/wonan/wonan.jpg",
        "/img/wonan/wonan2.jpg",
        "/img/wonan/wonan3.jpg",
        "/img/wonan/wonan5.jpg"
      ],
      currentnum: 0,
      currentWeb: "https://nrg.radio/",
      timer: null
    };
  },
  mounted() {
    this.flip();
  },
  methods: {
    flip: function() {
      this.timer = setInterval(this.next, 8000);
    },
    next: function() {
      this.currentnum += 1;
      this.back = this.ImagesF[this.currentnum % this.ImagesF.length];
      if (this.currentnum > this.ImagesF.length) {
        this.currentnum = 0;
      }
    },
    stop: function() {
      clearTimeout(this.timer);
    }
  },
  created() {
    this.stations = data.radios;
    bus.$on("stationChanged", data => {
      this.currentWeb = data.website;
    });
  }
};
</script>
<style>
.stations {
  padding-left: 95px;
  box-sizing: border-box;

  height: 100vh;
  grid-column: 1 /6;
  grid-row-start: 1;
  background-color: rgba(0, 0, 0, 0.753);
}
.gradi {
  background: linear-gradient(
    to bottom,
    rgba(36, 33, 33, 0.11) 0%,
    rgba(13, 12, 12, 0.199) 24%,
    rgba(10, 10, 10, 0.781) 51%,
    rgb(0, 0, 0) 80%,
    rgb(0, 0, 0) 100%
  );
  color: snow;
  height: 100%;
  width: 100%;
  text-align: left;
  box-sizing: border-box;
  padding: 10px;
  display: grid;
  align-content: end;
}
.gradi p {
  color: #bbb7b7;
}
.gradi button {
  width: 100px;
  height: 40px;
  border-radius: 15px;
  border-color: transparent;
  border: 0px;
  background: linear-gradient(
    90deg,
    rgba(0, 212, 255, 1) 0%,
    rgba(2, 113, 120, 1) 100%
  );

  color: snow;
}
.head {
  font-size: 2em;
  font-weight: 900;
  font-family: "Roboto", sans-serif;
}
.top {
  height: 60%;
  background-image: url("/img/music.gif");
  background-position: center;
  background-size: cover;
}
.channels {
  height: 40%;
  background-color: #1b1b20;
  padding: 10px;
  box-sizing: border-box;
  display: flex;
  overflow-x: auto;
}
.cards {
  height: 230px;
  min-width: 190px;

  background-position: center;
  background-size: cover;
  margin: 5px;
}
.card {
  height: 100%;
  width: 100%;
  background: linear-gradient(
    to bottom,
    rgba(36, 33, 33, 0.11) 0%,
    rgba(13, 12, 12, 0.199) 24%,
    rgba(10, 10, 10, 0.781) 51%,
    rgb(0, 0, 0) 80%,
    rgb(0, 0, 0) 100%
  );
  color: snow;
  text-align: center;
  line-height: 1.2em;
  display: grid;
  align-content: flex-end;
  padding-bottom: 70px;
  box-sizing: border-box;
  box-shadow: 0px 10px 26px -5px rgba(3, 0, 3, 1);
}
.name {
  font-size: 1em;
  font-weight: bolder;
}
.freq {
  font-weight: 100;
  font-size: 0.9em;
}
.channels::-webkit-scrollbar {
  width: 1em;
}

.channels::-webkit-scrollbar-track {
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
}

.channels::-webkit-scrollbar-thumb {
  border-radius: 10px;

  background-color: #166c5b;
  outline: 1px solid slategrey;
}

</style>
