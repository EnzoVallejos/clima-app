<template>
  <City/>
  <Temperature/>
</template>

<script>
import City from './components/City.vue'
import Temperature from './components/Temperature.vue'

export default {
  name: 'App',
  components: {
    City,
    Temperature
  }
}
</script>

<style>

</style>
