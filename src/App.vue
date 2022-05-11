<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Main from './components/Main.vue'
import Paint from './components/paint/Paint.vue'

</script>

<template>
  <main>
    <button class="paint-button" v-on:click="paint = !paint">{{paint}}</button>

    <Paint v-show="paint"/>
    <Main v-if="!paint"/>
    
  </main>
</template>






<script>
export default {
  data () {
    return{
      paint:false

    }
  }
}


function changeView(){
  console.log(paint)
  paint = !paint;
}









</script>

<style>
@import './assets/base.css';

.flex-center{
        display: flex;
        justify-content: center;
        align-items: center;
}

.paint-button{
  z-index: 5;
  margin: 5px;
  background-color: red;
}





/* 








#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0rem;

  font-weight: normal;

  transition-duration: 0.5s;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
} */
</style>
