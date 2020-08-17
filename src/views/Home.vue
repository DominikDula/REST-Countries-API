<template>
  <div >

    <show-countries  />

  </div>
</template>

<script>
// @ is an alias to /src
import ShowCountries from '@/components/ShowCountries.vue';



export default {
  name: 'Home',
  components: {
    ShowCountries,


  }
}
</script>
