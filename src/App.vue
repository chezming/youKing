<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-width: 1200px;
  width: 100%;
  height: 100vh;
}
/*@font-face {*/
/*  font-family: 'fangzheng'; //自定义字体名称*/
/*  src: url('../static/font/fangzheng.ttf'); //注意引入正确位置*/
/*}*/
*{
  margin: 0;
  padding: 0;
  border: 0;
  box-sizing: border-box;
  list-style: none;
}
</style>
