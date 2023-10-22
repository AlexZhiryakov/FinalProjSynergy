<template>  
    <div class="container">
      <NavComp/>
      <router-view></router-view>
    </div>
</template>

<script>
import NavComp from './components/NavComp.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    NavComp
  }
}
</script>

<style>
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: whitesmoke;
  margin-top: 60px;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
}

html {
  background-image: url(https://c.wallhere.com/photos/1c/d0/6600x3600_px_digital_art_drawing_landscape_painting_TacoSauceNinja-837552.jpg!d);
  background-repeat: no-repeat;
  background-position: center center;
  background-attachment: fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}
</style>
