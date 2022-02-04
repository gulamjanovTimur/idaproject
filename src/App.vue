<template>
  <div id="app">
    <CreateProduct />
  </div>
</template>

<script>
import CreateProduct from "./components/CreateProduct";
export default {
  name: "App",
  components: {
    CreateProduct,
  },
};
</script>

<style lang="scss">
@font-face {
  font-family: "Source Sans Pro";
  font-weight: normal;
  src: url("./assets/fonts/SourceSansPro-Regular.ttf");
}
* {
  font-family: Source Sans Pro;
}
#app {
  padding: 30px;
  min-height: 100vh;
  box-sizing: border-box;
  background-color: #e5e5e5;
}
body {
  margin: 0;
}
</style>
