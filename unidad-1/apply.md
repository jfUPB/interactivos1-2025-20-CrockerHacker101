# Unidad 1

## 🛠 Fase: Apply  

# Actividad 05  

## Sistema Interactivo Web con micro:bit

## Contexto general

Esta aplicación web está creada con **p5.js** y se conecta a un **micro:bit** via comunicacion serial para intercambiar datos. La interfaz es sencilla e incluye dos botones: uno para conectar o desconectar el micro:bit y otro para enviar un mensaje al micro:bit.

## Componentes del sistema

### Interfaz gráfica

- Se crea un canvas de 400x400 píxeles.
- Hay un círculo blanco dibujado en el centro del canvas (100 píxeles de diámetro).
- Hay dos botones en la pantalla:
- **Conectar/Desconectar micro:bit**
- **Enviar "Love"**

### Conexión serial con micro:bit

- Se usa **createSerial()** para crear un objeto de conexión serial.
- El botón **“Connect to micro:bit”** abre o cierra la conexión serial con el dispositivo micro:bit a 115200 baudios.
- Cuando está desconectado, el botón muestra: **“Connect to micro:bit”**.
- Cuando está conectado, el botón cambia a: **“Disconnect”**.

### Intercambio de datos

- Cuando el micro:bit envía datos por serial, el programa lee esos datos byte a byte (**port.read(1)**).
- Dependiendo del dato recibido:
  - Si recibe **A**, el círculo cambia a **rojo**.
  - Si recibe **B**, cambia a **amarillo**.
  - Si recibe cualquier otro carácter, cambia a **verde**.
- En el centro del círculo se muestra el carácter recibido en texto negro.

### Envío de datos al micro:bit

- Al presionar el botón **Enviar "Love"**, el programa envía un carácter **h** al micro:bit.

## Funcionamiento general

- El usuario conecta el navegador con el micro:bit mediante el botón.
- Se visualizan los estados enviados por el micro:bit cambiando el color del círculo.
- El usuario puede enviar un mensaje al micro:bit con el botón "Enviar Love".

¿Quieres el código completo o algún otro detalle para complementar este README?  

# Actividad 06  

## enlace del trabajo ##    
https://editor.p5js.org/CrockerHacker101/sketches/3Lf_WWBIH  

## Codigo p5.js ##  
let xPos;  
let targetX;  
let port;  
let reader;  
let keepReading = false;  

function setup() {  
  createCanvas(400, 400);  
  xPos = 200;  
  targetX = xPos;  
  const connectButton = createButton('Unirse al Fent World');  
  connectButton.position(135, 300);  
  connectButton.mousePressed(connectSerial);  
}  

function draw() {  
  background(220);  
  xPos = lerp(xPos, targetX, 0.1);  
  circle(xPos, 200, 100);  
  fill("blue")  
}  

async function connectSerial() {  
  port = await navigator.serial.requestPort();  
  await port.open({ baudRate: 115200 });  

  const decoder = new TextDecoderStream();  
  port.readable.pipeTo(decoder.writable);  
  reader = decoder.readable.getReader();  

  keepReading = true;  
  readLoop();  
}  

async function readLoop() {  
  while (keepReading) {  
    const { value, done } = await reader.read();  
    if (done) {  
      reader.releaseLock();  
      break;  
    }  
    if (value) {  
      processInput(value.trim());  
    }  
  }  
}  

function processInput(data) {  
  for (let char of data) {  
    if (char === 'A') {  
      targetX -= 10;  
    } else if (char === 'B') {  
      targetX += 10;  
    }  
    targetX = constrain(targetX, 25, width - 25);  
  }  
}  
# Codigo Micro:bit #  
from microbit import * 

uart.init(baudrate=115200)  
display.show(Image.ALL_CLOCKS);  

while True:  
    if button_a.was_pressed():  
        uart.write('A')  
    if button_b.was_pressed():  
        uart.write('B')  
    sleep(100)  

