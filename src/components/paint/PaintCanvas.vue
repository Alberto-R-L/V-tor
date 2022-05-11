<script setup>
import PaintTools from "./PaintTools.vue";
</script>

<template>
  <div>
    <!-- <PaintTools /> -->
    <div id="paint-canvas">
      <canvas id="canvas" width="720" height="480"></canvas>
      <div id="paint-tools">
        <div id="color-palette"></div>
        <button id="add-color">Add current color</button>
        <button id="remove-color">-</button>
        <div id="width-tool">
          <div>Width:</div>
        </div>
        <div id="canvas-size">
          <div>Canvas:</div>
        </div>
        <!-- <input type="color"> -->
        <div>
          <!--Tools-->
          <div>
            <input type="radio" id="brush" value="brush" name="tool" checked />
            <label for="brush"> Brush </label>
          </div>
          <div>
            <input type="radio" id="fill" value="fill" name="tool" />
            <label for="fill"> fill </label>
          </div>
          <div>
            <input type="radio" id="line" value="line" name="tool" />
            <label for="line"> line </label>
          </div>
          <div>
            <input type="radio" id="select" value="select" name="tool" />
            <label for="select"> select </label>
          </div>
          <div>
            <input type="radio" id="spray" value="spray" name="tool" />
            <label for="spray"> spray </label>
          </div>
          <div>
            <input type="radio" id="rectangle" value="rectangle" name="tool" />
            <label for="rectangle"> rectanble </label>
          </div>
          <div>
            <input type="radio" id="ellise" value="ellise" name="tool" />
            <label for="ellise"> ellise </label>
          </div>
        </div>
        <div id="source-div">
          <input id="source-url" placeholder="Paste url and press enter" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
window.onload = function(){
  load();
}




window.load = function () {
  var penColor = "#000000"; 
  var backgroundColor = "#FFFFFF";
  var penSize = "2";
  var posX = 0;
  var posY = 0;
  var tool = "brush";
  var toolType = "";
  var imageWidth = 720;
  var imageHeigh = 480;

  let drawing = false;

  const myCnv = document.getElementById("canvas");
  const context = myCnv.getContext("2d");
  context.imageSmoothingEnabled = true;
  const colorField = document.createElement("input");
  const sizeField = document.createElement("input");
  // const canvas = document.getElementById("paint-canvas");
  const toolList = document.getElementsByName("tool");
  const saveButton = document.createElement("button");
  const palleteDiv = document.getElementById("color-palette");
  const imageLoader = document.getElementById("source-url");
  const toolBoard = document.getElementById("paint-tools");
  const widthTool = document.getElementById("width-tool");
  const addColorButton = document.getElementById("add-color");
  const removeColorButton = document.getElementById("remove-color");
  const canvasDiv = document.getElementById("canvas-size");
  const fillButton = document.createElement("button");

  const widthField = document.createElement("input");
  const heighField = document.createElement("input");

  

  let colorArray = [
    "#000000", //Black
    "#FF0000", //Red
    "#FFD700", //Gold
    "#7CFC00", //Limegreen
    "#00FFFF", //Aqua
    "#191970", //MidnightBlue

    "#666666", //Gray
    "#FF4500", //Orangered
    "#FFFF00", //Yellow
    "#32CD32", //Green
    "#00BFFF", //DeepSkyBlue
    "#4B0082", //Indigo

    "#FFFFFF", //White
    "#FFA500", //Orange
    "#FFFF99", //LightYellow
    "#008000", //DarkGreen
    "#0000FF", //Blue
    "#FF00FF", //Magenta
  ];

  createColorfield();
  createSizeField();
  createToolSelector();
  createPalette();
  createSaveButton();
  createFillButton();
  createToolEvent();
  createWHFields();
  fillCanvas();

  //  Load image
  // Add load event
  imageLoader.addEventListener("keyup", function (event) {
    if (event.keyCode === 13) {
      event.preventDefault();
      console.log(imageLoader.value);
      loadImageUrl(context, imageLoader.value);
      imageLoader.value = "";
    }
  });

  // Resizer
  function createWHFields() {
    //Width
    
    widthField.id = "width-field";
    widthField.defaultValue = "720";
    canvasDiv.appendChild(widthField);
    //
    const sizeSeparator = document.createElement("a");
    sizeSeparator.innerHTML = "x";
    canvasDiv.appendChild(sizeSeparator);
    //Heigh
    
    heighField.id = "heigh-field";
    heighField.defaultValue = "480";
    canvasDiv.appendChild(heighField);
  }

  canvasDiv.addEventListener("keyup", function (event) {
      event.preventDefault();
      imageWidth = widthField.value
      imageHeigh = heighField.value
      rescaleImage(imageWidth, imageHeigh);
  });

  // Load the image
  function loadImageUrl(context, url) {
    var img = document.createElement("img");
    img.addEventListener("load", function () {
      var color = context.fillStyle;
      var size = context.lineWidth;
      rescaleImage(img.width, img.height);
      context.drawImage(img, 0, 0);
      context.fillStyle = color;
      context.strokeStyle = color;
      context.lineWidth = size;
    });
    img.src = url;
  }

  loadImageUrl();

  //  Save Imgage

  // Create the button
  function createSaveButton() {
    toolBoard.appendChild(saveButton);
    saveButton.innerText = "Save Image";
  }
  function createFillButton() {
    toolBoard.appendChild(fillButton);
    fillButton.innerText = "Fill";
  }
  // Add the event
  saveButton.addEventListener("click", function (e) {
    const dLink = document.createElement("a");
    dLink.download = "image.png";
    dLink.href = myCnv.toDataURL();
    dLink.click();
    dLink.delete;
  });



  fillButton.addEventListener("click", function (e) {
    backgroundColor = penColor;
    fillCanvas();
  });

  //  Scale the image
  function rescaleImage(width, height) {
    context.canvas.width = width;
    context.canvas.height = height;
  }

  //  Draw
  // Start drawing
  myCnv.addEventListener("mousedown", (e) => {
    if (e.buttons == 1) {
      // Define 1st point

      posX = e.offsetX;
      posY = e.offsetY;
      drawing = true;

      switch (tool) {
        case "brush":
          toolType = "brush";
          break;
        case "spray":
          toolType = "spray";
          break;
        case "rectangle":
          toolType = "notHold";
          break;
        case "ellise":
          toolType = "notHold";
          break;
        case "line":
          toolType = "notHold";
          break;
        case "fill":
          fillFlood(context, posX, posY)
          break;
      }
    }
  });
  // Draw While moving
  myCnv.addEventListener("mousemove", (e) => {
    if (drawing == true) {
      if (toolType == "brush") {
        drawLine(context, posX, posY, e.offsetX, e.offsetY);
        drawBrush(context, posX, posY, e.offsetX, e.offsetY);
        console.log("drawing");
        posX = e.offsetX;
        posY = e.offsetY;
      } else if (toolType == "spray") {
        drawBrush(context, posX, posY, e.offsetX, e.offsetY);
        console.log("spraying");
        posX = e.offsetX;
        posY = e.offsetY;
      }
    }
  });
  //  Stop drawing
  // Stop drawing when mouseup
  myCnv.addEventListener("mouseup", (e) => {
    stopPainting(e);
  });
  // Stop drawing when mouse outside canvas
  myCnv.addEventListener("mouseout", (e) => {
    stopPainting(e);
  });
  // Function stop drawing
  function stopPainting(e) {
    if (drawing == true) {
      if (toolType !== "notHold") {
        drawBrush(context, posX, posY, e.offsetX, e.offsetY);
        drawLine(context, posX, posY, e.offsetX, e.offsetY);
      } else if (tool == "rectangle") {
        drawRectangle(context, 0, 0, 0, 0);
        drawRectangle(context, posX, posY, e.offsetX, e.offsetY);
      } else if (tool == "ellise") {
        drawEllise(context, 0, 0, 0, 0);
        drawEllise(context, posX, posY, e.offsetX, e.offsetY);
      } else if (tool == "line") {
        drawLine(context, posX, posY, e.offsetX, e.offsetY);
        console.log(e.offsetX);
      }
      posX = 0;
      posY = 0;
      drawing = false;
      context.save();
    }
  }
  function drawRectangle(context, x1, y1, x2, y2) {
    context.beginPath();
    context.rect(x1, y1, x2 - x1, y2 - y1);
    console.log(x1, y1, x2 - x1, y2 - y1);
    context.stroke();
    context.strokeStyle = penColor;
    context.lineWidth = penSize;
    context.closePath();
}
  function drawEllise(context, x1, y1, x2, y2) {
    context.beginPath();
    context.ellipse(
      ((x2 - x1)/2) + x1,
      ((y2 - y1)/2) + y1,
      Math.abs(x2 - x1)/2,
      Math.abs(y2 - y1)/2,
      0,
      0,
      Math.PI * 2
    );
    console.log(x1, y1, x2, y2, 0, 0, Math.PI * 2);
    context.stroke();
    context.strokeStyle = penColor;
    context.lineWidth = penSize;
  }

  //  Functions for drawing
  // Function for drawing a straight section
  function drawLine(context, x1, y1, x2, y2) {
    if (tool == "brush" || tool == "line") {
      context.beginPath();
      context.strokeStyle = penColor;
      context.lineWidth = penSize;
      context.moveTo(x1, y1);
      context.lineTo(x2, y2);
      context.stroke();
      context.closePath();
    }
  }
  //Function for drawing a end of section
  function drawBrush(context, x1, y1, x2, y2) {
    switch (tool) {
      case "brush":
        toolBrush(context, x1, y1);
        break;
      case "spray":
        for(var i = 0 ; i < penSize/4 ; i++){
        toolSpray(context, x1, y1);
        }
        break;
    }
  }

  function toolBrush(context, x1, y1) {
    context.beginPath();
    context.fillStyle = penColor;
    context.arc(x1, y1, penSize / 2, 0, Math.PI * 2);
    context.fill();
    context.closePath();
  }

  function toolSpray(context, x1, y1) {
    var xRan = Math.random() * penSize - penSize / 2 + x1;
    var yRan = Math.random() * penSize - penSize / 2 + y1;
    context.beginPath();
    context.beginPath();
    context.fillStyle = penColor;
    context.arc(xRan, yRan, 1, 0, Math.PI * 2);
    context.fill();
    context.closePath();
  }
  // function toolSpray(context, x1, y1){
  //     var radius = widthTool/4;
  //     var area = radius * radius * Math.PI;
  //     var dPT = Math.ceil(area/30);
  //     var spray = setInterval(function(){
  //       for(i = 0 ; i < dPT ; i++){
  //         var offset = randomPoint(radius);
  //         toolBrush(context, offset, offset);
  //       }
  //     }
  // }
  function toolRect(context, x1, y1, x2, y2) {}
  // Function to fill
  function fillFlood(context, x1, y1) {
    var path = new Path2D();
    path.moveTo(x1, y1);
    // path.addPath();
    context.fill(path);
    // path.closePath();

  }


  // Add event for changing tool
  function createToolEvent() {
    toolList.forEach((i) => {
      i.addEventListener("change", (e) => {
        tool = i.value;
        console.log(tool);
      });
    });
  }

  //Function for Color Change
  function createColorfield() {
    colorField.setAttribute("type", "color");
    palleteDiv.appendChild(colorField);
    colorField.id = "color-selector";
  }
  // Add event to change color
  colorField.addEventListener("change", (e) => {
    penColor = colorField.value;
  });

  //Brush size change
  function createSizeField() {
    sizeField.id = "size-input";
    sizeField.setAttribute("type", "number");
    sizeField.defaultValue = 2;
    widthTool.appendChild(sizeField);
  }

  sizeField.addEventListener("change", (e) => {
    penSize = sizeField.value;
  });

  //  Palette selector
  function createSingleButton(color) {
    // Create each number
    var paletteButton = document.createElement("button");
    palleteDiv.appendChild(paletteButton);
    paletteButton.id = "palette-button;";
    paletteButton.style.backgroundColor = color;
    paletteButton.innerText = color;

    //Event assign
    paletteButton.addEventListener("click", function (e) {
      penColor = paletteButton.innerHTML;
      console.log(penColor);
      colorField.value = penColor;
    });
  }

  // Function to remove last palettecolor
  function removeLastButton() {
    palleteDiv.removeChild(palleteDiv.lastChild);
  }

  //  Add new color to palette event
  addColorButton.addEventListener("click", function (e) {
    createSingleButton(penColor);
  });

  //  Remove last color from palette event
  removeColorButton.addEventListener("click", function (e) {
    removeLastButton();
  });
  //  Function to create the whole palette
  function createPalette() {
    colorArray.forEach((i) => {
      createSingleButton(i);
    });
  }

  //  Tool selector
  function createToolSelector() {
    sizeField.setAttribute("type", "number");
    widthTool.appendChild(sizeField);
  }

  // Event for changing the pen size
  sizeField.addEventListener("change", (e) => {
    penSize = sizeField.value;
  });

  function fillCanvas(){
    context.fillStyle = backgroundColor;
    context.fillRect(0, 0, canvas.width, canvas.height)
  }

};

export default {
  methods: {
    mouseMove(e) {
      var posX = e.pageX;
      var posY = e.pageY;
      //   console.log(posX, posY);
    },

    // colorChange(){
    //     var penColor = "#00FF00";
    //     console.log("the color has been changed to" + penColor)
    // }
  },

  mounted() {
    window.addEventListener("mousemove", this.mouseIsMoving);
  },
};

// var canva = document.getElementById("canvas");
</script>


<style lang="scss">
#canvas {
  margin: 5px;
}

#paint-tools {
  background-color: slategray;
  z-index: 1;
  top: 20px;
  left: 0px;
  height: calc(100vh - 40px);
  width: 150px;
  font-size: 12.5px;
  position: fixed;
  outline: 1px solid black;
  align-content: space-between;

  div {
    max-width: 150px;
  }

  #size-input {
    max-width: 75px;
  }
}

#paint-canvas {
  //User select
  user-select: none;
  //Position and size
  top: 20px;
  left: 150px;
  height: 95vh;
  width: 100vw;
  position: fixed;
  font-size: 1.5vh;
  //Background
  background-color: lightgray;
  overflow: scroll;
}

#color-palette {
  //Flex
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  //Position and Size
  margin: 2.5px;
  width: 150px;
  //Background

  button {
    //position and size
    margin: 0;
    padding: 1px;
    font-size: 0px;
    color: transparent;
    height: 25px;
    width: 11.11111%;
  }
}
#color-selector {
  width: 150px;
  padding: 0px;
  background-color: transparent;
  border: none;
  margin: 0px;
}

#source-url {
  width: 150px;
  font-size: 12px;
}

#width-tool {
  display: flex;
  // flex-direction: row-reverse;
  justify-content: space-between;
}

#add-color {
  width: 122.5px;
}

#remove-color {
  width: 25px;
}

#canvas-size {
  display: flex;
  align-items: baseline;
  input {
    width: 45%;
  }
  a {
    width: 10%;
  }
}
</style>