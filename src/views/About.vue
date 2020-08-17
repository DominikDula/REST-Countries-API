<template>

    <div class="about" >
        <div class="button-holder">
            <router-link class="back-button" to="/"><i class="fas fa-arrow-left"></i>Back</router-link>
        </div>        
        <div class="country-show">
            <div class="country-image">
                <img :src="countryObject.flag" alt="">
            </div>
            <div class="country-info">
                <div class="detail-info">
                    <h1>{{countryObject.name}}</h1>
                    <div class="country-description">
                        <div class="left">
                            <p><b>Native name:</b> {{countryObject.nativeName}}</p>
                            <p><b>Population:</b> {{countryObject.population | formatNumber}}</p>
                            <p><b>Region:</b> {{countryObject.region}}</p>
                            <p><b>Sub region:</b> {{countryObject.subregion}}</p>
                            <p><b>Capital:</b> {{countryObject.capital}}</p>             
                        </div>
                        <div  class="right">
                            <p v-if="countryObject.topLevelDomain"><b>Top Level Domain:</b> {{countryObject.topLevelDomain[0]}}</p>
                            <p v-if="countryObject.currencies"><b>Currencies:</b> {{countryObject.currencies[0].code}}</p>
                            <p><b>Languages:</b><span v-for="(lng,index) in countryObject.languages" :key="index+1">{{lng.name}},</span></p>
                        </div>
                    </div>
                </div>
                <div class="borders">
                    <p><b>Border Countries: </b>
                    <span v-for="(border,index) in countryObject.borders" :key="index" v-show="index<3">{{border}}</span>
                    </p>
                </div>
            </div>
        </div>
    </div>

</template>

<script>


    export default {


        data() {
            return {
               countryObject : {},
               boolean:"",
            }
        },
        created() {
        this.$root.$on('each-country', data => (this.countryObject = data))
        this.$root.$on('toggle', data => (this.boolean=data))


    },

    filters: {
            formatNumber: function numberWithCommas(number) {
               return String(number).replace(/(.)(?=(\d{3})+$)/g,'$1,')
}
        },

        
    }
</script>

<style lang="scss" scoped>

@import '@/assets/scss/_variables';

    .about{
        height: 100vh;
    }
    
    .button-holder{
        max-width: 1440px;
        margin: 0 auto;
        padding: 0 3em;
        text-align: left;
        height: 12em;
        display: flex;
        align-items: center;
        
    }

    .back-button{
        width: 8em;
        display: flex;
        height: 2.5em;
        justify-content: space-evenly;
        align-items: center;
        text-decoration: none;
        border-radius: 10px;
        box-shadow: 0px 0px 3px 1px rgba(133,133,133,0.65);
        background: inherit;
        color: inherit;


    }


    .country-show{
        max-width: 1440px;
        padding: 0 3em;
        display: flex;
        margin: 0 auto;
    }
    .country-image{
        display: flex;
        height: 400px;
        width: 50%;
        img{
            width: 80%;
            height: 400px;
            object-fit: cover;
            align-self: center;
        }
    }
    .country-info{
        width: 50%;
        display: flex;
        flex-direction: column;
        justify-content: center;

    }
    .detail-info{
        width: 60%;

        h1{
            text-align: left;
        }
    }

    .country-description{
        text-align: left;
        display: flex;
        justify-content: space-between;
    }

    .borders{
        text-align: left;


        span{
            padding: 5px 37px;
            box-shadow: 0px 0px 3px 0px rgba(133,133,133,0.65);
            margin: 0 20px;
            font-size: 75%;

        }
    }


    @media screen and (max-width: 1300px){
        .detail-info{
        width: 75%;
        }
        .country-image{
        img{
            width: 80%;
            height: auto;
            object-fit: cover;
            align-self: center;
        }
    }
    }

    @media screen and (max-width: 1200px){
        .detail-info{
        width: 100%;
        }
    }
    @media screen and (max-width: 900px){
     .country-show{
         flex-direction: column;
     }
     .country-image{
        width: 100%;
        img{
            width: 100%;
            height: 400px;
            object-fit: contain;
        }
    }
    .country-info{
        width: 100%;
    }
    .country-description{
        align-items: flex-start;
        flex-direction: column;
        display: flex;
    }
    }

    .borders{
        p{
            b{
                display: block;
                margin-bottom: 10px;
            }
            span{
                padding: 5px 27px;
                margin: 0px 4px;

            }
        }
    }

    @media screen and (max-width: 500px){
        .about{
            position: relative;
        }
        
        .button-holder  {
            height: 2em;
            a{
                position: absolute;
                top: 50px;
            }
            
           }


    }
    
  
</style>
