<template>
  <div id="app">
    <Reviews :isMobile="isMobile"/>
  </div>
</template>

<script>
  import Reviews from '@/components/Reviews'

  export default {
    name: 'App',
    components: { Reviews },
    data() {
      return {
        isMobile: false
      }
    },
    mounted() {
      this.isMobile = window.innerWidth > 566 ? false : true
      
      window.addEventListener('resize', () => {
        if (window.innerWidth > 566) {
          this.isMobile = false
        } else {
          this.isMobile = true
        }
      })
    }
  }
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
