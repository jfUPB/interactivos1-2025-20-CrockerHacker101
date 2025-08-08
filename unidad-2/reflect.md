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

¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?  
mi parte que mas dificil fue y la que mas me gusto fue la parte del codigo, por que, al inicio empeze a crear el codigo por mi cuenta, sin hacer el diagrama primero


