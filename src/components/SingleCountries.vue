<template>

        <div @click="getCountyInfo()"  class="single" >
            <router-link  tag="div" class="routlink"  to="/about">
            <img :src=countries.flag alt="">
            <h3>{{countries.name}}</h3>
            <p><b>Population:</b> {{countries.population | formatNumber}}</p>
            <p><b>Region:</b> {{countries.region}}</p>
            <p><b>Capital:</b> {{countries.capital}}</p>
            </router-link>
        </div>
 
</template>

<script>
    export default {
        data() {
            return {

            }
        },
        props: {
            countries: {
                type: Object,
               
            },
        
            
        },
        
        filters: {
            formatNumber: function numberWithCommas(number) {
                return String(number).replace(/(.)(?=(\d{3})+$)/g,'$1,')
}
        },
        methods: {
           getCountyInfo(){
                  fetch(`https://restcountries.eu/rest/v2/region/Europe`)
                .then(response => response.json())
                .then(data =>{

                    this.$root.$emit('each-country', this.countries)                
                
                })
        },

        },

        
        
    }
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_variables';

.single{
    box-shadow: 0px 0px 20px 0px #56555524;
    h3{
        font-weight: 900;
    }
    img{
        width: 100%;
        height: 200px;
        object-fit: cover;
        
    }
}


.routlink{
    cursor: pointer;
    text-align: left;
}
.routlink {
    h3, p{
        margin-left: 30px;
    }
}





</style>