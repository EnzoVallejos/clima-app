<template>
  <City/>
  <Temperature/>
  <Hora/>
</template>

<script>
import City from './components/City.vue'
import Temperature from './components/Temperature.vue'
import Hora from './components/Hora.vue'

export default {
  name: 'App',
  components: {
    City,
    Temperature,
    Hora
  }
}
</script>

<style>

</style>
