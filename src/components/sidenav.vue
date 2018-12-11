<template>
  <div class="sidenav"></div>
</template>

<script>
export default {
  name: "Sidenav",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sidenav {
  grid-column-start: 1;
  grid-row-start: 1;
  width: 95px;
  box-shadow: 10px 10px 6px -10px rgb(31, 30, 31);
  background-color: rgb(30, 30, 31);
  height: 100vh;
  z-index: 99;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
