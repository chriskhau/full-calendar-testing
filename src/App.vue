<template>
  <div id="app">
        <Calendar />

  </div>
  

</template>

<script>

import Calendar from './components/test-full-calendar.vue'


export default {
  name: 'app',
  components: {

    Calendar
  }
}
</script>

<style scoped>
body {
  background-color: #eeeeee;
}
</style>
