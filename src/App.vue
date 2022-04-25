<template>
  <div id="app">
        <Terapeutas/>
  </div>
</template>

<script>
import Titulo from "./components/_share/Titulo.vue";
import Terapeutas from "./components/Terapeuta/Terapeutas.vue";

export default {
  name: 'App',
  components: {
    Titulo,
    Terapeutas
},
  data() {
    return {
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
