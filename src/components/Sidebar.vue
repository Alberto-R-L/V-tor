<template>
  <div id="sidebar">
        <ul>Seccion 1
            <li>aqui irá un vue bucle ya sabes ah y necesito uno largo para ver como queda</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
            <li>Opcion</li>
        </ul>
        <ul>Seccion 2
            <li>la seccion 2 queda muy bien</li>
            <li>Opcion</li>
            <li>Opcion</li>
        </ul>
        <ul>Seccion 3
            <li>la seccion 2 queda muy bien</li>
            <li>Opcion</li>
            <li>Opcion</li>
        </ul>
        <ul>Seccion 4
            <li>la seccion 2 queda muy bien</li>
            <li>Opcion</li>
            <li>Opcion</li>
        </ul>



    </div>
</template>

<script>
export default {

}
</script>

<style>

#sidebar{
        /* Position */
    position: fixed;
    top: 7vh;
    left: 0;
    z-index: 4;
    height: 89vh;   
    width: 20vw;
    min-width: 300px;
    max-width: 450px;
    padding: 1vh;
    display: none;

        /* Background */
    background-color: rgb(245, 245, 245);

        /* Border */
    filter: drop-shadow(3px 3px 3px #222);
}

</style>