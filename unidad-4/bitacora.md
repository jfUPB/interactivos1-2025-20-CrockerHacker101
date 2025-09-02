# Evidencias de la unidad 4

## Código

[[Enlace a la aplicación a modificar](https://editor.p5js.org/CrockerHacker101/sketches/2PiwbafWt)](URL)

Código a modificar:

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

[Enlace a la aplicación modificada](URL)

Código modificado:

``` js

```

## Video

[Video demostratativo](URL)



