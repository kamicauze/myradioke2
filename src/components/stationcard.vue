<template>
  <div
    class="cards"
    :style="{ 'background-image': 'url('+station.image+')'}"
    v-on:click="changeStation"
  >
    <div class="card">
      <div class="text">
        <span class="name">{{station.name}}</span>
        <br>
        <span class="freq">{{station.frequency}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { bus } from "../bus.js";
export default {
  props: ["station"],
  data() {
    return {};
  },
  methods: {
    changeStation: function() {
      bus.$emit("stationChanged", {
        url: this.station.url,
        image: this.station.image,
        name: this.station.name,
        freq: this.station.frequency,
        twit: this.station.twitter
      });
    }
  }
};
</script>
