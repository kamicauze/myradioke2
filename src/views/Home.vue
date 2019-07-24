<template>
  <div class="home">
    <div class="background"></div>
    <!-- <sidenav></sidenav> -->
    <stations></stations>
    <player></player>
  </div>
</template>

<script>
// @ is an alias to /src
// import sidenav from "@/components/sidenav.vue";
import stations from "@/components/stations.vue";
import player from "@/components/player.vue";

export default {
  name: "Home",
  components: {
    player: player,
    // sidenav: sidenav,
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
.background {
  background-image: url("../assets/skull-headphones-wallpaper-58695-60469-hd-wallpapers.jpg");
  background-position: center;
  background-size: cover;

  grid-column: 1 /-1;
  height: 100vh;
  grid-row-start: 1;
  z-index: -1;
}
</style>
