<template>
  <div id="paint-tools">
    
    


    <table id="tools">
      <tr>
        <td><button id="t1">T</button></td>
        <td><button id="t2">T</button></td>
        <td><button id="t3">T</button></td>
        <td><button id="t4">T</button></td>
      </tr>
      <tr>
        <td><button id="t5">T</button></td>
        <td><button id="t6">T</button></td>
        <td><button id="t7">T</button></td>
        <td><button id="t8">T</button></td>
      </tr>
      <tr>
        <td><button id="t9">T</button></td>
        <td><button id="t10">T</button></td>
        <td><button id="t11">T</button></td>
        <td><button id="t12">T</button></td>
      </tr>
      <tr>
        <td><button id="t13">T</button></td>
        <td><button id="t14">T</button></td>
        <td><button id="t15">T</button></td>
        <td><button id="t16">T</button></td>
      </tr>
      <tr>
        <td><button id="t17">T</button></td>
        <td><button id="t18">T</button></td>
        <td><button id="t19">T</button></td>
        <td><button id="t20">T</button></td>
      </tr>
      <tr>
        <td><button id="t21">T</button></td>
        <td><button id="t22">T</button></td>
        <td><button id="t23">T</button></td>
        <td><button id="t24">T</button></td>
      </tr>
      
    </table>

    <div id="t-colors">
      
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      <button>a</button>
      

      
    
      
    
    
    
    </div>


  </div>
</template>

<script>
let colorArray =["#000000", "#FFFFFF", "#FF0000","#FA8072", "#FF1493", "#FFC0CB", "#FFA500", "#FF4500", "#FFFF00", "#8B4513", "#FF00FF", "#4B0082", "#00FF00", "#006400", "#00FFFF", "#0000FF"] 
console.log(colorArray);

function reloadColors(){
for(i = 0 ; i > colorArray.length ; i++){
  colorTab.append(colorBut);
  colorBut.css("backgroundColor", colorArray[i]);
  console.log(i);
}

  }

function changeColor(){
  
}






window.onload = function(){

reloadColors();

// for(i = 0 ; i < colorArray.length ; i++){
//   buttonC = document.getElementById("c" + i)
//   buttonC.style.backgroundColor = colorArray.i;
// }

//  Append all the colors

var colorButId = [];
// colorRow = document.createElement(tr);
// colorCol = document.createElement(td);
colorTab = document.getElementById("t-colors");
colorBut[colorButId] = document.createElement(button);





}










export default {

}






</script>

<style lang="scss">

#paint-tools{
    background-color: slategray;
    z-index: 1;
    top: 20px;
    left: 0px;
    color: white;
    height: calc(100vh - 40px);
    width: 150px;
    font-size: 12.5px;
    position: fixed;
    outline: 1px solid black;
    flex-direction: row;
    align-content: space-between;

    #t-colors{
      bottom: 0;
      display: flex;
      flex-wrap: wrap;
        button{
          margin: 0;
          padding: 0;
          height: 25px;
          width: 25px;
          border-radius: 0;
          border: 3px inset #333;
          background-color: red;
          &:active{
            outline: 1px inset;
            transform: scale(.75);
            scale: 21, 1;
            box-shadow: 0 1px #999;
          }
        }
      }




    table{
      border:dimgray 2px inset ;

      button{
        margin: 0;
        padding: 0;
        height: 25px;
        width: 25px;
        border-radius: 0;
      }

      



    }



  }


</style>