<template>
  <StopWatch :start="true"/>
</template>

<script>
import StopWatch from './components/StopWatch.vue'

export default {
  name: 'App',
  components: {
    StopWatch
  }
}
</script>

<style>

#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(90deg, #3f2b96 0%, #a8c0ff 100%);
}
</style>
