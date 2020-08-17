<template>
    <div class="search-form">
        <div class="inside">
            <form class="form" action="">
                <i class="fas fa-search"></i>
                <input class="input"  placeholder="Search for a country" type="text" v-model="searchCountry">
            </form>
            <select class="select" @change="getCountry()" v-model="region" required>
                <option value="" hidden >Filter by region</option>
                <option>Africa</option>
                <option>Americas</option>
                <option>Asia</option>
                <option>Europe</option>
                <option>Oceania</option>
            </select>
            
        </div>
    </div>
</template>

<script>
    export default {
                data() {
            return {
                searchCountry:"",
                region:"",
    
            }
        },      
        methods: {
            getCountry() {
                fetch(`https://restcountries.eu/rest/v2/region/${this.region}`)
                .then(response => response.json())
                .then(data =>{
                   let RestApiCountries= data.map(country => 
                    this.extractData(country))
                    this.$root.$emit('api-countries', RestApiCountries)
                    this.$root.$emit('animation')
                    
                      
                
                })
            },
            extractData({
            capital:capital,
            name:name,
            nativeName:nativeName,
            population:population,
            region:region,
            subregion:subregion,
            currencies:currencies,
            languages:languages,
            topLevelDomain:topLevelDomain,
            borders:borders,
            flag:flag,

            }){
    
                return{capital,name,nativeName,population,region,subregion,currencies,languages,topLevelDomain,borders,flag};
            },
        },
        created(){
            fetch(`https://restcountries.eu/rest/v2/all`)
                .then(response => response.json())
                .then(data =>{
                   let RestApiCountries= data.map(country => 
                    this.extractData(country))
                    this.$root.$emit('api-countries', RestApiCountries)
                    this.$root.$emit('animation')
                      
                
                })
        },
        watch: {
            searchCountry(value) {
                this.$root.$emit('inputchanged', value)
            }
        },
      
   
        
    }
</script>

<style lang="scss" scoped>

@import '@/assets/scss/_variables';

    .search-form{
       
        height: 6em;
        padding-top: 3em;

    }
    .inside{
        max-width: 1440px;
        padding: 0 3em;
        display: flex;
        margin: 0 auto;
        justify-content: space-between;
    }

    .form{
        position: relative;
        i{
            position: absolute;
            top: 20px;
            left: 12px;
        }
        .input{
            width: 25em;
            height: 3.5em;
            border: none;
            outline: none;
            margin-top: 3px;
            padding-left: 4em;
            box-shadow: 0px 0px 5px 0px rgba(219,219,219,1);
            background: inherit;
            color: inherit;

        }
    }


    .select{
        width: 12em;
        outline: none;
        border: none;
        height: 3.5em;
        box-shadow: 0px 0px 5px 0px rgba(219,219,219,1);
        background: inherit;
        color: inherit;
    
        option{
            color: black;
        }
   
    }



    @media screen and (max-width: 760px){
        .inside{
            flex-direction: column;
        }
        .form{
            margin-bottom: 1em;
            width: 90%;
            display: flex;
            align-items: center;
        }
        .input{
            width: 90%;
        }


    }

</style>