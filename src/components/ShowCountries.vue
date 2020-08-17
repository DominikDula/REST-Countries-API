<template>
<div>

    <search-countries  />  
 
    <div class="countries">   
        <transition-group  name="fade" tag="div" class="display-countries">
            <single-countries v-for="(singleCountry,index) in filteredCountries" :key="index+1" :countries="singleCountry" :index="index"/>
        </transition-group >
    </div>
    
    
</div>
  
</template>

<script>
import SingleCountries from './SingleCountries.vue'
import SearchCountries from './SearchCountries.vue'
    export default {
        data() {
            return {
                allCountries:[],
                search:"",

                
            }
        },
        components: {
            SingleCountries,
            SearchCountries,
        },
        mounted() {
		this.$root.$on('api-countries', data => (this.allCountries = data))
        this.$root.$on('inputchanged', value => (this.search = value))
        this.$root.$on('animation', () => (this.filterAnimation()))
        
    },
    computed: {
        filteredCountries() {
            return this.allCountries.filter(country => {
            return country.name.toLowerCase().includes(this.search.toLowerCase())
            
})
        },
    },
    methods: {
        filterAnimation() {
            let replaceCountries = this.allCountries
            this.allCountries = []
           setTimeout(()=>{ this.allCountries = replaceCountries; }, 0)
        },
 
        
    },
  
        
    }
</script>

<style lang="scss" scoped>

@import '@/assets/scss/_variables';

.countries{
    height: 100%;
}

.display-countries{
    padding: 0 3em 3em;
    max-width: 1440px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
     grid-gap: 4em;
    grid-auto-rows: minmax(300px, auto);
}

.fade-enter-active{
	transition: all 0.5s ease;
}

.fade-enter {
	transform: scale(0.5);
}


@media screen and (max-width: 760px){
        .countries{
            margin-top: 4em;
            
        }
        

    }

    @media screen and (max-width: 400px){
        .display-countries{
                    padding: 0 2em;
                }
    }



</style>