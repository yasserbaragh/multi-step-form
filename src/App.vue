<template>
  <div class="body">
      <div class="background">
        <DashBoard />
      </div>
  
  </div>
</template>

<script>
import DashBoard from './components/Dash-Board.vue';




export default {
  name: "App",
  components: { DashBoard }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Ubuntu:wght@400;500;700&display=swap');
#app {
font-family: Avenir, Helvetica, Arial, sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
text-align: center;
color: #2c3e50;
margin-top: 0;

}
body {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      height: 100%;
      font-size: 16px;
  }
* {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Ubuntu', sans-serif;
  }


</style>
