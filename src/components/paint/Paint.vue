<script setup>
import PaintHeader from './PaintHeader.vue'
import PaintFooter from './PaintFooter.vue'

import PaintCanvas from './PaintCanvas.vue'


</script>

<template>
    <div id="paint">
        <PaintHeader/>

        <PaintCanvas/>
        <PaintFooter/>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">

 #paint{
     top: 0;
     left: 0;
 }

    .paint-bar{
    background-color: slategray;
    top: 0px;
    left: 0px;
    color: white;


  }



</style>