<template>
  <div id="app" class="light">
      
    <the-navigation />
    <router-view />


  </div>
</template>

<script>

import TheNavigation from './components/TheNavigation.vue'


export default {
    data() {
        return {
        }
    },
  name: 'App',
  components: {
    TheNavigation,

  },

}
</script>

<style src="@/assets/scss/main.scss" lang="scss">

</style>
