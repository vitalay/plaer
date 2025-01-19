<script setup>
import  Board  from './components/Board.vue'
</script>

<template>

 
<div class="app">
 <img class="logo" alt="Vue logo"src="./assets/logo.svg"  />
 <h1 class="h1">VUE 3</h1>
 <p>Запомни и открой все <br>зеленые квадратики</p>
 <Board /> 
</div>


</template>

<style scoped>
.app {
  font-family: Helvetica, sans-serif;
  text-align: center;
  margin-top: 40px;
}
.logo {
  width: 100px;
  height: 100px;

}

</style>
