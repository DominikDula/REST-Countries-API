<template>
    <div class="nav">
        <div class="content">
            <h1>Where in the world?</h1>
            <div class="dark-mode">
                
                <button class="toggle-button" @click="toggleClick()"><i class="far fa-moon"></i>Dark mode</button>  
            </div>
       </div> 
    </div>
</template>

<script>
    export default {
        data() {
            return {
                darkmode:false
            }
        },
        methods: {
            toggleClick() {
                this.darkmode =! this.darkmode;
      
              
                let app =document.querySelector("body");
                let nav =document.querySelector(".nav");
                let icon =document.querySelector(".fa-moon");
              
                app.classList.toggle("light-dark");
                nav.classList.toggle("nav-dark");
                icon.classList.toggle("fas");
                                    
                                              
                this.$root.$emit('toggle', this.darkmode)
                
            }
        },

    }
</script>

<style lang="scss" scoped>

@import '@/assets/scss/_variables';
    .nav{
        
        height: 5em;
        color: $light-mode-tx;
        
        background: $dark-mode-bg-tx;
        box-shadow: 0px 2px 5px 0px rgba(133,133,133,0.65);
        h1{
            font-weight: bold;
        }
    }
    .nav-dark{
        background: $dark-mode-bg;
        color: $dark-mode-bg-tx;
        box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.65);
       
    }
    .content{
        max-width: 1440px;
        padding: 0 3em;
        display: flex;
        margin: 0 auto;
        justify-content: space-between;
    }
    .dark-mode{
        display: flex;
        justify-content: center;
        align-items: center;
        .toggle-button{
            border: none;
            outline: none;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
                background: inherit;
                color: inherit;
            i{
                margin-right: 1em;
            }

        }
        .toggle-button-dark{
            background: $dark-mode-elements;
            color: $dark-mode-bg-tx;
        }
    }

    @media screen and (max-width: 760px){
        .nav{
            display: flex;
            align-items: center;
        }
        .content{
            padding: 0;
            font-size: 70%;
            h1{
                    margin-right: 2em;
            }
        }
    }
</style>
