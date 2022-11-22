<script>
import MyList from "@/components/MyList";

export default {
  name: "App",
  components: { MyList },
};
</script>
<template>
  <div id="app">
    <my-list />
  </div>
</template>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a {
  color: #42b983;
}
.product .btn_cart {
  padding-left: 0;
}
</style>
