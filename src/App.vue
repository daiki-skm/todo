<template>
  <div id="app">
    <to-do></to-do>
  </div>
</template>

<script>
import toDo from './components/ToDo.vue'

export default {
  name: 'App',
  components: {
    'to-do':toDo
  }
}
</script>

<style>

</style>
