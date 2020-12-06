<template>
  <div id="app">
    <Reviews />
  </div>
</template>

<script>
  import Reviews from '@/components/Reviews'

  export default {
    name: 'App',
    components: { Reviews },
  }
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
