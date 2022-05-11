<script setup>
import Header from './Header.vue'
import Sidebar from './Sidebar.vue'
import Footer from './Footer.vue'
import NotFound from './NotFound.vue'



var notFound = false
</script>


<template>
<div>
  <Header/>
  <Content/>
  <Sidebar/>
  <Footer/>

  <NotFound v-if="notFound"/>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">

button{
    border: none;
    box-shadow: 0 3px #999;
    border-radius: 5px 5px 5px 5px;
    transition-duration: 0.1s;
    // margin: 1vw;
    padding: 5px;
    min-width: 1.5rem;

        &:active{
        outline: 1px inset tomato;
        transform: translateY(2px);
        box-shadow: 0 1px #999;
    }
  }


  

</style>