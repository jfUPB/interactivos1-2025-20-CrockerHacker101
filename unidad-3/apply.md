# Unidad 3


## 🛠 Fase: Apply  

# Activida 06  

### 1. codigo con micro:bit

```
let port;
let connectBtn;
let connectionInitialized = false;

let validChars = "ABST";

let bombaArmada = false;     
let secuencia = "";           
const secuenciaCorrecta = "ABA";

function setup() {
  createCanvas(400, 400);
  background(220);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);
  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  textAlign(CENTER);
  text("Press A,B,S,T to simulate micro:bit keys", width / 2, height / 2);

  if (bombaArmada) {
    text("Bomba ARMADA! Ingresa secuencia ABA para desactivar", width / 2, height / 2 + 30);
  }

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function keyPressed() {
  let keyValue = key.toUpperCase();
  if (validChars.includes(keyValue)) {
    console.log(keyValue);
    port.write(keyValue);

    if (bombaArmada) {
      secuencia += keyValue;
      if (secuencia.length > 3) {
        secuencia = secuencia.slice(-3); 
      }

      if (secuencia === secuenciaCorrecta) {
        bombaArmada = false;
        secuencia = "";
        console.log("Bomba Desactivada we");
      }
 
    } else {
      if (keyValue === 'S') {
        bombaArmada = true;
        secuencia = "";
        console.log("Bomba Activada we");
      }
    }
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
```
### 2. codigo sin Micro:bit  

```
let validChars = "ABST";  
let bombaArmada = false;      
let bombaExplotada = false;
let bombaDesactivada = false;
let secuencia = "";            
const secuenciaCorrecta = "ABA";  
let tiempoRestante = 0; 
let tiempoTotal = 20;  

function setup() {   
  createCanvas(400, 400);   
  background(220);   
  textSize(15);
  tiempoRestante = tiempoTotal; 
}  

function draw() {   
  background(220);   
  textAlign(CENTER);   

  if (bombaExplotada) {
    text("KAPLUUUUM!!!!!", width / 2, height / 2);  
    text("Presiona T para reiniciar", width / 2, height / 2 + 40);  
    return;
  }

  if (bombaDesactivada) {
    text("Bomba desactivada", width / 2, height / 2);  
    text("Presiona T para reiniciar", width / 2, height / 2 + 40);  
    return;
  }

  text("Tiempo actual: " + tiempoTotal + "s", width / 2, 40);

  text("S para que la bomba haga KABOOOM!!", width / 2, height / 2 - 40);
  
  if (bombaArmada) {
    let tiempo = max(0, floor(tiempoRestante - millis()/1000));
    text("Autodestruccion iniciada", width / 2, height / 2);
    text("Ingrese el codigo para abortar", width / 2, height / 2 + 30);
    text("Tiempo restante: " + tiempo + "s", width / 2, height / 2 + 60);

    if (tiempo <= 0) {       
      bombaArmada = false;       
      bombaExplotada = true;     
    }   
  } else {     
    text("Presiona 'S' para activar", width / 2, height / 2 + 30);   
  } 
}

function keyPressed() {   
  let keyValue = key.toUpperCase();   

  if (keyValue === 'T') {
    bombaArmada = false;
    bombaExplotada = false;
    bombaDesactivada = false;
    secuencia = "";
    tiempoTotal = 20;
    tiempoRestante = tiempoTotal;
    return;
  }

  if (keyValue === 'A') {
    tiempoTotal += 1;
    tiempoRestante = millis()/1000 + tiempoTotal;
  }
  if (keyValue === 'B') {
    if (tiempoTotal > 1) { // evitar que sea 0 o negativo
      tiempoTotal -= 1;
      tiempoRestante = millis()/1000 + tiempoTotal;
    }
  }

  if (validChars.includes(keyValue)) {     
    console.log("Tecla:" + keyValue);      

    if (bombaArmada) {       
      secuencia += keyValue;       
      if (secuencia.length > 3) {         
        secuencia = secuencia.slice(-3);        
      }        

      if (secuencia === secuenciaCorrecta) {         
        bombaArmada = false;         
        bombaDesactivada = true;         
        secuencia = "";         
        console.log("Bomba Desactivada we");       
      }     
    } else {       
      if (keyValue === 'S') {         
        bombaArmada = true;         
        secuencia = "";         
        tiempoRestante = millis()/1000 + tiempoTotal;         
        console.log("Bomba Activada we");       
      }     
    }   
  } 
}
```
# Actividad 07   

### Codigo Micro:bit  

```
# Imports go at the top
from microbit import *
import utime

display.clear()

class BombTask:
    def __init__(self):
        self.PASSWORD = ['A','B','A']
        self.key = ['']*len(self.PASSWORD)
        self.keyindex = 0
        self.count = 20
        self.startTime = utime.ticks_ms()
        self.state = 'CONFIG'
        display.clear()
        display.show(self.count,wait=False)

    def update(self):
        if self.state == 'CONFIG':
            if button_a.was_pressed():
                self.count = min(self.count+1,60)
                display.show(self.count,wait=False)

            if button_b.was_pressed():
                self.count = max(10,self.count-1)
                display.show(self.count, wait=False)

            if accelerometer.was_gesture('shake'):
                self.startTime = utime.ticks_ms()
                self.state = 'ARMED'

        elif self.state == 'ARMED':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > 1000:
                self.startTime = utime.ticks_ms()
                self.count = self.count - 1
                display.show(self.count,wait=False)
                if self.count == 0:
                    display.show(Image.SKULL)
                    self.state = 'EXPLODED'

            if button_a.was_pressed():
                self.key[self.keyindex] = 'A'
                self.keyindex = self.keyindex + 1

            if button_b.was_pressed():
                self.key[self.keyindex] = 'B'
                self.keyindex = self.keyindex + 1

            if self.keyindex == len(self.key):

                passIsOK = True
                for i in range(len(self.key)):
                    if self.key[i] != self.PASSWORD[i]:
                        passIsOK = False
                        break;
                if passIsOK == True:
                    self.count = 20
                    display.show(self.count,wait=False)
                    self.keyindex = 0
                    self.state = 'CONFIG'
                else:
                    self.keyindex = 0

        elif self.state == 'EXPLODED':
            if pin_logo.is_touched():
                self.count = 20
                display.show(self.count,wait=False)
                self.startTime = utime.ticks_ms()
                self.state = 'CONFIG'

bombTask = BombTask()

while True:
    bombTask.update()
```

### Codigo P5.js  

```
let port;
let connectBtn;
let connectionInitialized = false;

let validChars = "ABST";  
let bombaArmada = false;      
let bombaExplotada = false;
let bombaDesactivada = false;
let secuencia = "";            
const secuenciaCorrecta = "ABA";  
let tiempoRestante = 0; 
let tiempoTotal = 20;  

function setup() {   
  createCanvas(400, 400);   
  background(220);   
  textSize(15);
  tiempoRestante = tiempoTotal; 

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 350);
  connectBtn.mousePressed(connectBtnClick);
}  

function draw() {   
  background(220);   
  textAlign(CENTER);   
  
  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (bombaExplotada) {
    text("KAPLUUUUM!!!!!", width / 2, height / 2);  
    text("Presiona T para reiniciar", width / 2, height / 2 + 40);  
    return;
  }

  if (bombaDesactivada) {
    text("Bomba desactivada", width / 2, height / 2);  
    text("Presiona T para reiniciar", width / 2, height / 2 + 40);  
    return;
  }

  text("Tiempo actual: " + tiempoTotal + "s", width / 2, 40);

  text("S para que la bomba haga KABOOOM!!", width / 2, height / 2 - 40);
  
  if (bombaArmada) {
    let tiempo = max(0, floor(tiempoRestante - millis()/1000));
    text("Autodestruccion iniciada", width / 2, height / 2);
    text("Ingrese el codigo para abortar", width / 2, height / 2 + 30);
    text("Tiempo restante: " + tiempo + "s", width / 2, height / 2 + 60);

    if (tiempo <= 0) {       
      bombaArmada = false;       
      bombaExplotada = true;     
    }   
  } else {     
    text("Presiona 'S' para activar", width / 2, height / 2 + 30);   
  } 

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function keyPressed() {   
  let keyValue = key.toUpperCase();   

  if (validChars.includes(keyValue) && port.opened()) {
    port.write(keyValue);
  }

  if (keyValue === 'T') {
    bombaArmada = false;
    bombaExplotada = false;
    bombaDesactivada = false;
    secuencia = "";
    tiempoTotal = 20;
    tiempoRestante = tiempoTotal;
    return;
  }

  if (keyValue === 'A') {
    tiempoTotal += 1;
    tiempoRestante = millis()/1000 + tiempoTotal;
  }
  if (keyValue === 'B') {
    if (tiempoTotal > 1) { 
      tiempoTotal -= 1;
      tiempoRestante = millis()/1000 + tiempoTotal;
    }
  }

  if (validChars.includes(keyValue)) {     
    console.log("Tecla:" + keyValue);      

    if (bombaArmada) {       
      secuencia += keyValue;       
      if (secuencia.length > 3) {         
        secuencia = secuencia.slice(-3);        
      }        

      if (secuencia === secuenciaCorrecta) {         
        bombaArmada = false;         
        bombaDesactivada = true;         
        secuencia = "";         
        console.log("Bomba Desactivada we");       
      }     
    } else {       
      if (keyValue === 'S') {         
        bombaArmada = true;         
        secuencia = "";         
        tiempoRestante = millis()/1000 + tiempoTotal;         
        console.log("Bomba Activada we");       
      }     
    }   
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
```

### Link para editar el codigo P5.js  

https://editor.p5js.org/CrockerHacker101/sketches/5fD47i5ql 
