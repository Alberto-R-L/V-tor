<template class="header">
    <header>
        <div class="header-menu flex-center">
            <button onclick="toggleSide()" class ="header-menu-button"> <!-- Search -->
                ╚
                <img width="20px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Hamburger_icon.svg/1200px-Hamburger_icon.svg.png">
            </button>
        </div>
        <div class="header-logos flex-center">
            <img class="header-logos-img" src="" height="50vh">
            <a class="logo flex-center" onclick="scrollUp()">
                
                <img src="./icons/logo.svg">
                 - Tor

            </a>
        </div>

        <div class="header-input flex-center">
            <input id ="search-input" placeholder="Type your search">
                <button onclick="clearAndSearch()" id ="search-button"> <!-- Search -->
                    <img src="https://cdn-icons-png.flaticon.com/512/64/64673.png" width="15px">
                </button>
            <!--<button id="clearButton" onclick="clearResults()"> X </button>-->
            <div id="search-status"></div>
        
        </div>
        <div class="header-logsign flex-center">
            <div>Log - in | Sign up</div>
        </div>


        <div class="flex-center">
            <button id="app-button"> ç </button>
        </div>

        <!--
            
            <div>

        </div>
    
    -->
    </header>
</template>

<script>
window.onload = function(){

    
}


export default {
    data(){

    }

}
</script>

<style lang="scss">



header{

    button{
        min-width: 5vh;
        width: 5vh;
        height: 5vh;
        
    }

        /* Position */
    position: fixed;
    top: 0;
    left: 0;
    z-index: 3;
    width: 100vw;
    min-height: 75px;
    height: 7vh;
    background-color: rgba(245, 245, 245, 0.95); /* whitesmoke */
    
        /* Flex */

        /* Grid */
    display: grid;
    grid-template-columns: 5fr 20fr 50fr 20fr 5fr;

        /* Border */
    border: 2px outset ;
    border-left: 0px;
    border-right: 0px;
    box-shadow: 0px 0px 10px;

        /* Font */  
    font-family: 'Quicksand', sans-serif;

    .header-logos{
        /* Flex */
        

        

        .logo{
            font-size: 2rem;
            margin-top: 0px;
            margin-bottom: 0px;
            cursor: pointer;
            background-image: none;

            

            :hover > &{
                background-image: radial-gradient(farthest-corner at 0px 50%,
                rgba(50, 187, 112, 0.5) 0%, rgba(0, 0, 0, 0) 100%)
            }

            img{
                height: 2rem;
            }
        }
    }
    
    .header-input{
    grid-column: 3;
    min-width: 50px;

    input{
        height: 5vh;
        width: 200px;
        border-radius: 5px;
        border: 1px slategray solid;
        transition: width 0.4s ease-in-out;
        padding: 10px;
        

        &:focus{
            width: 500px;
        }
    }
    
}

}


</style>