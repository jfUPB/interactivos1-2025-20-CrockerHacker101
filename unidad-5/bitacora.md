
# Sustentación de la unidad 5

### 1. Profundidad de la Indagación:  

A lo largo de esta actividad no solo aprendí a enviar datos del micro:bit hacia p5.js, sino que también investigué y comprendí los desafíos del diseño de protocolos de comunicación. Me di cuenta de que usar ASCII puede ser útil en etapas tempranas, pero que en sistemas más robustos es esencial migrar a binario por eficiencia y velocidad. Esto me llevó a preguntar sobre estrategias de framing, errores de sincronización y cómo mejorar la confiabilidad del sistema. Las decisiones de diseño en la comunicación serial —como usar un byte de inicio y checksum— no son triviales, y entenderlas me
ayudó a mejorar mi criterio técnico y a pensar como un desarrollador de sistemas de comunicación más completo, ademas:  

- Entendí y explicaste cómo el micro:bit envía los datos.  
- Analise cómo p5.js los recibe y transforma.    
- Compare protocolos ASCII vs binario.  
- Cuantificaste ahorro de bytes y explicaste su impacto.  
- Identificaste causas raíz de errores (desincronización.

Nota: 5.0

### 2. Calidad de la Experimentación:  


NOTA: 1.9

### 3. Análisis y Reflexión:  

En esta actividad entendí cómo el micro:bit puede enviar datos de sensores (acelerómetro y botones) en formato ASCII por UART. Usar ASCII tiene ventajas iniciales: los datos son fáciles de leer y depurar, y \n sirve como un delimitador natural que actúa como un mecanismo básico de framing, Sin embargo, reflexionando más a fondo, me di cuenta de que este método, aunque simple, es frágil si se pierde un carácter o si el receptor empieza a leer desde la mitad del mensaje. No hay forma de saber si los datos están completos o no. En protocolos más eficientes como los binarios, este problema es más grave, ya que no hay delimitadores visibles. Ahí es donde entendí el valor real de incluir un byte de inicio (como 0xAA) y un checksum, El byte de inicio permite sincronizar el receptor: si hay ruido o pérdida de datos, puede buscar ese byte específico para "reengancharse". El checksum actúa como verificador: si los datos están corruptos, simplemente se descartan, evitando que el sistema tome decisiones equivocadas con datos malos, Esta comprensión me llevó a analizar el trade-off entre usar ASCII (más simple, pero más pesado y lento) y usar binario (más rápido, pero más complejo). En prototipos, ASCII puede ser suficiente, pero en proyectos reales donde la eficiencia y la confiabilidad importan, usar binario con framing y verificación de errores es indispensable.  

Finalmente, construí un modelo mental más claro: desde que el micro:bit recolecta los datos, los empaca, los transmite por UART, hasta que p5.js los recibe, los parsea y genera eventos visuales, Cada etapa tiene puntos de falla potenciales, y ahora sé cómo abordarlos con diseño robusto de protocolos de comunicación, ademas:

- Explicas correctamente el flujo de datos y los eventos.  
- Entiendes cómo funciona la lectura de UART en p5.js.  
- Usas bien términos técnicos como split, draw, int, boolean, etc.
- Tu redacción es clara, y se entiende tu razonamiento.  

NOTA: 4.0

### 4. Apropiación y Articulación de Conceptos:  

El uso de un protocolo binario con header y checksum es fundamental para manejar el flujo asíncrono e ininterrumpido de bytes en la comunicación serial. Sin él, los datos podrían desincronizarse, generando errores y lecturas inválidas.

Este protocolo convierte una transmisión caótica en un sistema organizado y robusto que permite una comunicación rápida, eficiente y confiable entre el micro:bit y p5.js.

NOTA 4.0



