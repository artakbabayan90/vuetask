<script setup>
import Calendar from './components/Calendar.vue'

</script>

<template>
  <div class="between:flex small(flex-column) ">
    <div class="box width-4/12 padding-2">
      <Calendar/>
    </div>
  </div>
</template>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
}
</style>
