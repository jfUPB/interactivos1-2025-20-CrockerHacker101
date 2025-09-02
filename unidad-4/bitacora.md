# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/SyEx9qqp1V)

Código a modificar:

``` js
// P_1_2_3_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * generates specific color palettes
 *
 * MOUSE
 * position x/y        : row and coloum count
 *
 * KEYS
 * 0-9                 : creates specific color palettes
 * s                   : save png
 * c                   : save color palette
 */
'use strict';

var tileCountX = 50;
var tileCountY = 10;

var hueValues = [];
var saturationValues = [];
var brightnessValues = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  // init with random values
  for (var i = 0; i < tileCountX; i++) {
    hueValues[i] = random(360);
    saturationValues[i] = random(100);
    brightnessValues[i] = random(100);
  }
}

function draw() {
  // white back
  background(0, 0, 100);

  // limit mouse coordinates to canvas
  var mX = constrain(mouseX, 0, width);
  var mY = constrain(mouseY, 0, height);

  // tile counter
  var counter = 0;

  // map mouse to grid resolution
  var currentTileCountX = int(map(mX, 0, width, 1, tileCountX));
  var currentTileCountY = int(map(mY, 0, height, 1, tileCountY));
  var tileWidth = width / currentTileCountX;
  var tileHeight = height / currentTileCountY;

  for (var gridY = 0; gridY < tileCountY; gridY++) {
    for (var gridX = 0; gridX < tileCountX; gridX++) {
      var posX = tileWidth * gridX;
      var posY = tileHeight * gridY;
      var index = counter % currentTileCountX;

      // get component color values
      fill(hueValues[index], saturationValues[index], brightnessValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (key == 'c' || key == 'C') {
    // -- save an ase file (adobe swatch export) --
    var colors = [];
    for (var i = 0; i < hueValues.length; i++) {
      colors.push(color(hueValues[i], saturationValues[i], brightnessValues[i]));
    }
    writeFile([gd.ase.encode(colors)], gd.timestamp(), 'ase');
  }

  if (key == '1') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = random(100);
      brightnessValues[i] = random(100);
    }
  }

  if (key == '2') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = random(100);
      brightnessValues[i] = 100;
    }
  }

  if (key == '3') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(360);
      saturationValues[i] = 100;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '4') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 0;
      saturationValues[i] = 0;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '5') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 195;
      saturationValues[i] = 100;
      brightnessValues[i] = random(100);
    }
  }

  if (key == '6') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = 195;
      saturationValues[i] = random(100);
      brightnessValues[i] = 100;
    }
  }

  if (key == '7') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(180);
      saturationValues[i] = random(80, 100);
      brightnessValues[i] = random(50, 90);
    }
  }

  if (key == '8') {
    for (var i = 0; i < tileCountX; i++) {
      hueValues[i] = random(180, 360);
      saturationValues[i] = random(80, 100);
      brightnessValues[i] = random(50, 90);
    }
  }

  if (key == '9') {
    for (var i = 0; i < tileCountX; i++) {
      if (i % 2 == 0) {
        hueValues[i] = random(360);
        saturationValues[i] = 100;
        brightnessValues[i] = random(100);
      } else {
        hueValues[i] = 195;
        saturationValues[i] = random(100);
        brightnessValues[i] = 100;
      }
    }
  }

  if (key == '0') {
    for (var i = 0; i < tileCountX; i++) {
      if (i % 2 == 0) {
        hueValues[i] = 140;
        saturationValues[i] = random(30, 100);
        brightnessValues[i] = random(40, 100);
      } else {
        hueValues[i] = 210;
        saturationValues[i] = random(40, 100);
        brightnessValues[i] = random(50, 100);
      }
    }
  }

}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/CrockerHacker101/sketches/2PiwbafWt)

Código modificado:

``` js
let tileCountX = 50;
let tileCountY = 10;

let hueValues = [];
let saturationValues = [];
let brightnessValues = [];

let port;
let connectBtn;
let connectionInitialized = false;

let latestData = "0,0,0,0";
let mX = 0;
let mY = 0;
let buttonA = 0;
let buttonB = 0;
let lastButtonA = 0;
let paletteIndex = 0;

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noStroke();

  generatePalette(paletteIndex);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(20, height - 40);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(0, 0, 100);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

if (port.opened()) {
  let data = port.readUntil('\n');
  if (data) {
    data = data.trim();
    if (data.length > 0) {
      let parts = data.split(",");
      if (parts.length >= 4) {
        let xRaw = int(parts[0]);
        let yRaw = int(parts[1]);

        buttonA = parts[2].trim().toLowerCase() === "true" ? 1 : 0;
        buttonB = parts[3].trim().toLowerCase() === "true" ? 1 : 0;

        mX = map(xRaw, -1024, 1024, 0, width);
        mY = map(yRaw, -1024, 1024, 0, height);
      }
    }
  }
}

  let clampedMX = constrain(mX, 0, width);
  let clampedMY = constrain(mY, 0, height);

  let currentTileCountX = int(map(clampedMX, 0, width, 1, tileCountX));
  let currentTileCountY = int(map(clampedMY, 0, height, 1, tileCountY));
  let tileWidth = width / currentTileCountX;
  let tileHeight = height / currentTileCountY;

  let counter = 0;

  for (let gridY = 0; gridY < tileCountY; gridY++) {
    for (let gridX = 0; gridX < tileCountX; gridX++) {
      let posX = tileWidth * gridX;
      let posY = tileHeight * gridY;
      let index = counter % currentTileCountX;
      fill(hueValues[index], saturationValues[index], brightnessValues[index]);
      rect(posX, posY, tileWidth, tileHeight);
      counter++;
    }
  }

  if (buttonA === 1 && lastButtonA === 0) {
paletteIndex = paletteIndex === 0 ? 1 : 0;
    generatePalette(paletteIndex);
  }
  lastButtonA = buttonA;

if (buttonB === 1 && lastButtonB === 0) {
  saveCanvas('screenshot', 'png');
}
lastButtonB = buttonB;

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function generatePalette(index) {
  for (let i = 0; i < tileCountX; i++) {
    switch (index) {
      case 0:
        hueValues[i] = random(360);
        saturationValues[i] = random(100);
        brightnessValues[i] = random(100);
        break;
      case 1:
        hueValues[i] = random(360);
        saturationValues[i] = random(100);
        brightnessValues[i] = random(100);
        break;
    }
  }
}

```

## Video

[Video demostratativo](URL)






