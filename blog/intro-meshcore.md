---
slug: intro-meshcore
title: 'Explorando alternativas LoRa: Primer contacto con MeshCore'
sidebar_label: "Intro a MeshCore"
authors: 
  - key: MrNetsky
    title: Autor
  - key: nicopace
    title: Colaborador
  - key: aguslasp
    title: Colaborador
tags:
  - meshcore
  - meshtastic
  - dispositivos
---

##  ¿Qué es MeshCore? ¿Y qué relación tiene con Meshtastic?

Si bien algo ya hemos mencionado en un [*artículo anterior*](/blog/formatos-digitales-de-comunicacion), lo mencionaremos nuevamente: MeshCore es un sistema multiplataforma que permite comunicaciones off-grid (fuera de la red) basadas en texto, mediante hardware de radio LoRa (Long Range). Similar a Meshtastic hasta el momento, pero... ¿Qué los diferencia?

### Comportamiento de la malla

La forma de enviar los mensajes es similar para ambos, ya que el mensaje recorre la red que estos dispositivos crean entre sí buscando a su destinatario. Pero MeshCore va más allá, ya que, una vez encontrado su destinatario, guarda la ruta de comunicación con dicho nodo. Debido a esto, cuando se vuelvan a comunicar entre ellos, el mensaje sólo se transmitirá a nodos que repitan el mensaje y que se encuentren en la ruta de comunicación entre ambos (siempre y cuando el camino siga funcionando para que el mensaje llegue). Haciendo un paralelismo, si usted quiere visitar a su amigo que vive a 4 cuadras, una vez que encuentre el recorrido más corto para llegar, probablemente lo repita cada vez que quiera visitarlo. Pero si luego se muda a 12 cuadras el camino que usaba para llegar a destino cambiará, por lo cual deberá encontrar un nuevo camino y luego usará el mismo para llegar. 
Esta cualidad contribuye a que las redes que se pueden crear con Meshcore puedan ser significativamente más grandes, llegando a los 64 saltos. En el caso de Meshtastic, el límite es de 7 saltos. Esta no es una limitación arbitraria, sino una decisión de diseño pensada para optimizar el funcionamiento en entornos urbanos.

Pero… ¿Qué es exactamente un “salto”?

Un salto ocurre cada vez que un nodo retransmite un mensaje para acercarlo a su destino. Es decir, cuando un dispositivo recibe un mensaje y lo vuelve a emitir para que otro nodo más lejano pueda captarlo. Una forma sencilla de entenderlo es imaginar una carrera de postas: cada corredor recorre un tramo y le pasa la posta al siguiente. De la misma manera, cada nodo transmite el mensaje al siguiente, hasta que finalmente llega al destinatario.

## ¿Cómo funciona?

Funciona de manera similar que Meshtastic y opera en los mismos dispositivos. Nosotros ya tenemos algunos de ellos adquiridos, por lo que no nos representa un costo extra probarla. Lo único que debemos hacer es flashear nuestros dispositivos con firmware MeshCore, y lo podremos hacer desde la siguiente página. El proceso es similar tanto para los dispositivos con nRF52, como con ESP32, pero si hay que hacer una gran salvedad en este apartado, los firmware de la gran mayoría de dispositivos, están pensado para cumplir una única función.

Me explico... En Meshtastic, es posible cambiar qué función va a desempeñar el aparato y puede usar todos los métodos de conexión a la pc o celular desde un mismo firmware, mientras que en MeshCore hay firmware dedicado para diferentes situaciones. Por ejemplo, existen 4 firmwares para el Elecrow ThinkNode M1, dependiendo de si el dispositivo que envía y recibe mensajes va a usar la conexión vía BLE o vía USB, si es repetidor exclusivo o si es un room server (depósito de mensajes para quien no haya podido recibirlos acceda y los pueda ver). Aunque, en la última versión del firmware, le permite a los nodos con una determinada configuración enviar y repetir, es una función limitada en comparación al funcionamiento de Meshtastic.

En nuestra primera experiencia, más a principio de año, se sufrieron fallas en la conexión USB y en el proceso de flasheo del dispositivo, dejando una sensación de fragilidad de dicho procedimiento. Pero con el paso del tiempo esto ha mejorado exponencialmente y en nuestras últimas pruebas con esta tecnología NO hemos experimentado fallo alguno. De manera similar surgieron problemas con la conexión Bluetooth en nuestros primeros contactos con esta tecnología, pero en las últimas pruebas han solucionado esto casi por completo dejando muy buenas sensaciones.

Ambos tienen app de celular, pero... Meshtastic tiene una plataforma traducida al Español casi en su totalidad, mientras que MeshCore está en Inglés. Hay que reconocer que en la última versión de la app se han agregado múltiples idiomas, sin embargo, el Español NO es uno de ellos. Esperamos que en próximas versiones sea incluído. Encontramos positivo que estén agregando más idiomas poco a poco.

El hecho de que el firmware de MeshCore esté directamente asociado a una forma de conexión o función intrínsecamente, limita la forma en la que podemos usar el dispositivo, mientras que con Meshtastic esto no sucede.

En cuanto al hardware en el que corre Meshtastic y MeshCore es el mismo, sin embargo podemos notar grandes diferencias en el firmware que se ejecuta en dicho hardware. Para empezar, ambos están en inglés para la gran mayoría de hardwares disponibles. La interfaz de usuario es notablemente mejor en el caso de Meshtastic y hace un mejor aprovechamiento del hardware que tiene a disposición el dispositivo en el que está instalado. Mientras que en MeshCore, se siente que es un firmware poco optimizado para un dispositivo en particular y se siente que ha sido porteado de uno en particular a los demás. Esto hace que no pueda adaptarse de forma óptima al hardware de todos los dispositivos en los que se instala. Al menos eso sucedió para todos nuestros dispositivos, a excepción del T-Deck, donde no realizamos pruebas con MeshCore aún.

MeshCore tiene características interesantes que nos gustaría resaltar:

Cuando configuras el nodo desde el celular, las configuraciones no reinician el dispositivo. Cosa que sí sucede para Meshtastic y que es un punto a favor de MeshCore. Es importantísimo aclarar que muchos de los cambios requieren de un reinicio al igual que en Meshtastic, pero si debes de hacer 10 cambios en éste, requerirán 10 reinicios. Mientras que en MeshCore se requiere sólo 1 luego de haber hecho todos los cambios necesarios, pero dicho reinicio deberás hacerlo de manera manual.
Desde la app podés renombrar a los nodos que tengas en tu lista de contactos. Similar como cualquier contacto del teléfono para agendarlo como quieras.
La configuración de la radio. No viene nada por default, puedes usar un preset de radio que te permita comunicarte con todos aquellos nodos que posean la misma configuración. O bien puedes configurar tú mismo una de manera particular y ambos tipos de configuraciones se pueden hacer de manera sencilla.
Puede, al igual que Meshtastic, compartir la posición GPS del teléfono aumentando la precisión.
Dentro de los canales, permite que ciertos participantes sólo puedan leer, pero no contestar, similar a un grupo de difusión de Whatsapp. Muy útil para dar directivas sin congestionar los canales de comunicación con las respuestas de todos los participantes.
Siguiendo el hilo, permite ver los participantes de un canal, NO los integrantes. Me explico, si en un canal están 40 personas y en él sólo escriben 5 personas, habrá 40 integrantes, pero sólo podrás ver a los 5 participantes, los restantes 35 no sabrás quienes son a menos que interactúen en el canal.

Es importante destacar que no está diseñado para enviar la posición de manera autónoma y regular como lo hace Meshtastic. Esto al menos para nosotros, es un problema ya que saber cuál es la ubicación es fundamental para los combatientes. Pero no es que esta tecnología no tenga la capacidad, ya que apps particulares como MeshCore SAR lo han logrado, sin embargo desde la app de MeshCore oficial esta opción no está disponible.
Otra diferencia importante está en la forma en que los nodos se comunican.
En Meshtastic, si dos o más nodos comparten la misma configuración de radio y región, pueden comunicarse automáticamente en cuanto están dentro de alcance.
En MeshCore, en cambio, el enfoque es distinto: para que dos nodos puedan comunicarse, deben ser contactos entre sí. Para lograrlo, es necesario agregarse mediante una clave pública, un código QR o a partir de un advert recibido.
Pero… ¿Qué es un advert? ¿Y una clave pública?
Un advert es un paquete de datos pequeño que un nodo emite para anunciar su presencia. Es, en esencia, una baliza ya que se utiliza para ver a la distancia la presencia de un objeto o persona. Es una forma de decir: “estoy acá y este soy yo”, permitiendo que otros nodos cercanos lo detecten e identifiquen.
Una clave pública, por su parte, es una cadena de caracteres alfanuméricos que funciona como tu identidad digital. Permite que otros nodos te reconozcan y, además, habilita la comunicación segura, evitando que terceros puedan hacerse pasar por vos o leer mensajes privados.
Como vemos, estas limitaciones vienen de la filosofía de diseño. Ya que en una ciudad no nos interesaría que todos nuestros contactos sepan nuestra ubicación todo el tiempo, ni que tampoco cualquiera nos escriba. Por ello, MeshCore te da la posibilidad de limitar a las personas con las que quieres compartir la telemetría (ubicación, batería, etc.). Esto no lo convierte en una tecnología inferior a Meshtatic, sino en una diferente. Es necesario destacar que MeshCore posee una gran diversidad de apps particulares potenciando esta tecnología u orientándola hacia una determinada dirección, denotando la activa comunidad que posee y la fé que la misma posee en esta tecnología.

Para finalizar, un dato de color... Si tienes las apps de Meshtastic y de MeshCore en tu teléfono móvil y dos nodos flasheados uno con Meshtastic y otro con MeshCore, podrás conectarte a dos nodos de manera simultánea desde el mismo celular. Pero la pregunta del millón... ¿Es útil? La verdad es que por el momento creemos que no, pero también creemos que abre una puerta a una futura colaboración entre ambas tecnologías.

---

Creemos que MeshCore es una tecnología interesante, digna de ser explorada y expandida. Creemos que las diferencias que posee respecto de Meshtastic se deben al tiempo en que salió al mundo uno respecto del otro. Además, explica también la diferencia entre el tamaño de las comunidades, ya que es mucho más grande que la de MeshCore.

Nos parece positivo que existan ambos firmwares porque creemos que ante sus diferencias los únicos beneficiados son los usuarios. Además consideramos que con el tiempo, los beneficios de uno son adoptados por el otro y viceversa.

Creemos que de momento seguiremos con Meshtastic porque creemos que es una tecnología un poco más robusta, que nos ayudará con el combate contra el fuego. No obstante, seguiremos de cerca a MeshCore considerándolo tanto como posible reemplazo, como un compañero de Meshtastic en el caso de que en un futuro ambas tecnologías puedan trabajar en conjunto, potenciando sus fortalezas y disminuyendo sus debilidades.
