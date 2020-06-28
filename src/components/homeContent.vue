<template>
  <div>
    <div class="home_left">
      <div class="home_lt">
        <div class="home_lt1"></div>
        <div class="home_lt2"></div>
      </div>
      <div class="home_lb"></div>
    </div>
    <div class="home_right"></div>
  </div>
</template>

<script>
    export default {
        name: "homeContent",
        data() {
            return {
                msg: "Hello Vue.js"
            }
        },
        component: {
            //someComponent
        },
        mounted() {
        },
        method: {},

    }
</script>

<style>
.home_left{
  width: 30%;
  height: 80%;
  background-color: white;
}
</style>
