# Unidad 2


## 🤔 Fase: Reflect

# Actividad 6  

## Parte 1: recuperación de conocimiento (Retrieval Practice)

### **1:** Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?
La maquina de estado es la que te permite cambiar entre estados y los cuatro componentes fundamentales son Eventos,acciones, estados y tracciones.  

### **2:** Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?   
La tecnica de la maquina de estados se usa para gestionar la concurrencia de los dispositvos como el micro:bit para que se realizen de manera simultanea sin que se bloquee.  

¿Qué problema hay con sleep()?  
- La función sleep(ms) bloquea el hilo de ejecución:
- Mientras el programa está "durmiendo", no puede hacer nada más.
- Si un botón se presiona durante un sleep(), puede que el programa no lo detecte.
- Si se usa un temporizador, puede perderse el momento exacto en que se debe ejecutar algo. 

### **3** Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

### **4:** Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.  
Un Vector de prueba es el conjunto de entrada como los botones, el touch, el shake y el tiempo que permite que se usan para verificar que la lógica del sistema funciona como debe.  
Por que es util crusial para verificar una maquina de estados? :  
- ayuda a detectar errores
- permite probar casos limite
- ahorran tiempo
- automatizan pruebas

## Parte 2:  reflexión sobre tu proceso (Metacognición)  

### **1** ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?  
mi parte que mas dificil fue y la que mas me gusto fue la parte del codigo, por que, al inicio empeze a crear el codigo por mi cuenta, sin hacer el diagrama primero, entonces me tire de una vez al codigo, lo que proboco que me enredara un poco, pero ya en la casa hice el diagrama y me fue un poco mejor en el codigo.  

### **2** Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?  
el " BUG " que encontre fue el de poner los LEDs por que tenia muchos errores a la hora de prender, pero despues logre solucionarlo y lo puse bien.  

### **3** El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?  
si, un poco pero se pudo lograr, primero intente hacerlo por mi cuenta, pero me resulto mas dificil, entonces me puse a hacer el diagrama y ya pude avanzar, y si, primero hice el codigo de forma muy simple y le fui poniendo mas cositas.  

### **4** Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?  
yo digo que reloj, que cambie de estado cada que pase 60 min se marque una hora.

# Actividad 7  
https://github.com/jfUPB/interactivos1-2025-20-natalieruizperez/blob/unidad2/apply/unidad-2/apply.md

### Analisis 
La verdad no hay nada para criticar, el trabajo esta muy bien hecho y esta usando la tecnica usada por el profe.







