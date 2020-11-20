<template>
  <div class="home">
    <stations></stations>
    <player></player>
  </div>
</template>

<script>
// @ is an alias to /src

import stations from "@/components/stations.vue";
import player from "@/components/player.vue";

export default {
  name: "Home",
  components: {
    player: player,

    stations: stations
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto");
.home {
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: whitesmoke;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
}
</style>
