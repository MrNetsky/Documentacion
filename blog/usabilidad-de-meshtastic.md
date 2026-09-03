---
slug: usbilidad-de-meshtastic
title: "¿Qué tan usable es Meshtastic para personas que no provienen del mundo tecnológico?" 
sidebar_label: "Usabilidad de Meshtastic"
authors:
  - key: MrNetsky
    title: Autor
  - key: aguslasp
    title: Colaborador
tags:
  - dispositivos
  - meshtastic
---

Toda tecnología nueva requiere un proceso de aprendizaje. Sin embargo, algunas herramientas resultan más intuitivas que otras y pueden incorporarse a las tareas cotidianas con mayor facilidad.

Esto nos llevó a plantearnos una pregunta sencilla: **¿qué tan usable es Meshtastic?**

Antes de responder, es importante aclarar que la interacción con Meshtastic puede realizarse a través de tres elementos diferentes:

- El propio dispositivo LoRa que ejecuta el firmware Meshtastic.  
- La aplicación móvil para Android o iOS.  
- El cliente web oficial.

Cada uno de estos componentes ofrece una experiencia de uso distinta y presenta ventajas, limitaciones y desafíos propios. Por este motivo, analizaremos la usabilidad de Meshtastic desde cada una de estas perspectivas.

Para este artículo únicamente tendremos en cuenta las herramientas oficiales del proyecto. Existen clientes desarrollados por terceros, pero su evaluación excede el alcance de este trabajo.

## Dispositivo LoRa

:::warning Atención  
Los nodos de los que se hablará en esta sección son dispositivos comerciales que están listos para su uso, fabricados y distribuídos por marcas especializadas. No se incluirán placas o kits orientados al armado o modificación por parte del usuario (DIY).  
:::

La usabilidad del firmware de Meshtastic está fuertemente condicionada por el hardware sobre el cual se ejecuta. A diferencia de otras aplicaciones, donde la experiencia de uso suele ser relativamente uniforme, en Meshtastic dos dispositivos pueden ofrecer formas de interacción muy diferentes aun ejecutando exactamente el mismo firmware.

De manera general, podemos dividir los nodos en dos grandes grupos: dispositivos sin pantalla y dispositivos con pantalla.

Los dispositivos sin pantalla incluyen tanto a los repetidores como a muchos nodos tipo card. En estos casos, la interacción directa con el equipo es limitada y suele reducirse a algunos botones físicos, indicadores luminosos y, en determinados modelos, alertas sonoras.

Esto hace que su funcionamiento diario resulte relativamente sencillo, pero también implica una fuerte dependencia de la aplicación móvil o de un computador para realizar configuraciones, consultar información o acceder a funciones avanzadas.

La experiencia de uso puede variar significativamente entre modelos. Algunos dispositivos comunican de manera clara su estado mediante luces, sonidos o vibraciones, mientras que en otros casos puede resultar más difícil interpretar qué está ocurriendo si no se conoce previamente el significado de cada indicador. Por este motivo, la consulta de los manuales de uso continúa siendo importante para aprovechar correctamente las capacidades de cada nodo.

Desde nuestro punto de vista, los dispositivos sin pantalla presentan una curva de aprendizaje baja para las tareas básicas de uso cotidiano, pero dependen casi por completo de la aplicación móvil para acceder a la mayor parte de las funcionalidades que ofrece Meshtastic.

Los nodos con pantalla presentan una experiencia de uso diferente. Aunque todos ejecutan Meshtastic, existen diferencias importantes entre modelos, ya sea por el tipo de pantalla utilizada, la cantidad de botones disponibles o la interfaz implementada por cada fabricante.

En líneas generales, estos dispositivos ofrecen un mayor grado de independencia respecto del teléfono o la computadora. Es posible consultar mensajes, modificar configuraciones básicas, habilitar o deshabilitar funciones como Bluetooth o GPS e incluso navegar por diferentes menús directamente desde el nodo.

La facilidad de uso depende en gran medida de cómo se haya implementado la interfaz. Factores como el idioma disponible, la organización de los menús, el tamaño de la pantalla y la cantidad de botones influyen directamente en la experiencia del usuario.

Por ejemplo, algunos dispositivos disponen de varios botones dedicados a la navegación, mientras que otros utilizan un único botón para recorrer los menús y ejecutar acciones, lo que puede requerir una adaptación inicial por parte del usuario.

A pesar de estas diferencias, nuestra experiencia indica que la mayoría de los nodos con pantalla resultan relativamente sencillos de utilizar para las tareas básicas. Con un breve período de práctica es posible familiarizarse con las funciones más habituales, incluso cuando la interfaz se encuentra únicamente en inglés.

Sin embargo, aunque estos dispositivos permiten operar de forma autónoma en determinadas situaciones, siguen sin ofrecer el mismo nivel de comodidad, velocidad y cantidad de opciones que la aplicación móvil. Por este motivo, consideramos que la pantalla del nodo debe entenderse como un complemento útil y no como un reemplazo completo de la aplicación.

Durante nuestras pruebas también llegamos a una conclusión que consideramos importante desde el punto de vista de la usabilidad: no siempre disponer de más opciones implica una mejor experiencia de uso.

En contextos donde el usuario debe concentrarse en una tarea principal, como ocurre durante el combate de incendios, creemos que resulta conveniente que exista un único camino claramente definido para realizar cada acción.

Por este motivo, nuestra tendencia actual es utilizar el nodo principalmente como dispositivo de transmisión y recepción, mientras que la configuración, lectura y redacción de mensajes se realizan desde la aplicación móvil. Esta separación reduce la posibilidad de errores y simplifica el proceso de aprendizaje para nuevos usuarios.

## App móvil

Si tuviéramos que señalar cuál es el componente más accesible de todo el ecosistema Meshtastic, probablemente sería la aplicación móvil.

Uno de sus principales puntos a favor es que se encuentra traducida al español en gran parte de su interfaz, algo que reduce considerablemente la barrera de entrada para nuevos usuarios. Además, la aplicación organiza sus funciones en apartados relativamente claros: conversaciones, contactos, mapa, ajustes y conexiones.

La navegación general resulta sencilla y, en líneas generales, las funciones más utilizadas suelen encontrarse donde el usuario espera encontrarlas. Particularmente, creemos que las últimas versiones han mejorado la organización de muchas opciones de configuración, facilitando la localización de parámetros que anteriormente resultaban más difíciles de encontrar.

Sin embargo, no todas las modificaciones recientes han mejorado la experiencia de uso.

Uno de los apartados que consideramos menos intuitivos es el de **Conexiones**, generando confusión es la selección de dispositivos Bluetooth. La aplicación mantiene visibles los nodos a los que el usuario se conectó anteriormente, independientemente de que se encuentren encendidos o disponibles en ese momento.

Técnicamente es posible distinguir los dispositivos disponibles observando el valor RSSI, ya que únicamente los nodos detectados activamente mostrarán este parámetro. Sin embargo, esta información puede pasar desapercibida para usuarios sin experiencia o para quienes desconocen el significado de dicho indicador. A medida que aumenta la cantidad de nodos almacenados, puede resultar difícil identificar rápidamente cuál es el dispositivo al que se desea conectar.

A pesar de estas observaciones, consideramos que la aplicación móvil posee una curva de aprendizaje relativamente baja. La mayoría de los usuarios logra familiarizarse con sus funciones principales en poco tiempo y, una vez comprendida la lógica general de funcionamiento, el resto de las opciones suele descubrirse de manera progresiva.

Como posible mejora, creemos que sería interesante incorporar un sistema de ayuda inicial o un modo de asistencia para primeros usuarios. Una serie de explicaciones breves o consejos contextuales podría facilitar enormemente la adopción de la herramienta sin necesidad de consultar documentación externa.

Por último, aunque existen diferencias visuales y de organización entre las versiones para Android e iOS, no consideramos que esto represente un problema significativo de usabilidad. La mayoría de los usuarios aprenderá a utilizar una única plataforma y, en caso de cambiar posteriormente de sistema operativo, gran parte del conocimiento adquirido seguirá siendo aplicable.

## Cliente Web oficial

El cliente web oficial de Meshtastic es, probablemente, el componente menos maduro de los tres que analizamos en este artículo. Aunque comparte gran parte de las funcionalidades presentes en la aplicación móvil, la experiencia general todavía transmite la sensación de encontrarse en una etapa de desarrollo más temprana.

Uno de los problemas más notorios que encontramos está relacionado con la gestión de dispositivos conectados. Durante nuestras pruebas observamos que, si un nodo se reinicia o se apaga, es frecuente encontrarse con errores al intentar reconectarlo. En algunos casos aparece el mensaje:

`Failed to execute 'open' on 'SerialPort': Failed to open serial port.`

Si bien el problema puede resolverse reconectando el dispositivo o volviendo a autorizar el puerto, desde el punto de vista de la usabilidad resulta una situación confusa para usuarios sin experiencia técnica.

La gestión de dispositivos guardados también presenta inconvenientes. Es posible almacenar múltiples veces un mismo nodo utilizando el mismo puerto serial e incluso asignándole distintos nombres. Además, si una conexión deja de funcionar, el registro permanece guardado sin ningún tipo de advertencia. Esto puede provocar situaciones donde varios perfiles parecen estar conectados simultáneamente cuando en realidad corresponden al mismo dispositivo físico.

Otro aspecto que consideramos mejorable es la persistencia de la información. Al recargar la página se pierde gran parte del contexto de trabajo, incluyendo los mensajes intercambiados durante la sesión. Esto obliga al usuario a reconstruir parte de la información cada vez que vuelve a abrir el cliente.

Un aspecto positivo es la existencia de soporte para múltiples idiomas. La infraestructura parece estar preparada para futuras traducciones, algo que valoramos especialmente. Sin embargo, al momento de realizar esta evaluación el español todavía no se encuentra disponible, lo que puede representar una barrera adicional para nuevos usuarios.

En términos generales, la organización de las opciones resulta familiar para quienes ya utilizan la aplicación móvil. La mayoría de las configuraciones mantienen una lógica similar, aunque algunas funciones se encuentran ubicadas en lugares diferentes. Por ejemplo, compartir un código QR con la configuración de canales se realiza desde la sección de conversaciones en Android, mientras que en el cliente web esta opción se encuentra dentro de la configuración de canales.

La gestión de canales es funcional y permite generar claves automáticamente o seleccionar distintos niveles de longitud para las mismas. Sin embargo, observamos que cierta información relacionada con la seguridad de los canales no resulta tan visible como en otras interfaces, algo que podría ayudar a los usuarios a comprender mejor las implicancias de participar en determinados canales públicos o privados.

También valoramos la presencia de un buscador de configuraciones. A medida que Meshtastic incorpora nuevas funcionalidades, localizar rápidamente una opción específica se vuelve cada vez más importante y esta herramienta simplifica considerablemente dicha tarea.

Por otra parte, encontramos algunas limitaciones funcionales. Durante nuestras pruebas no encontramos la posibilidad de crear o compartir puntos de interés desde el mapa, una característica que sí consideramos especialmente útil en la aplicación móvil. Dado que el cliente web suele utilizarse en pantallas considerablemente más grandes, creemos que podría ser un entorno muy adecuado para trabajar con información geográfica de forma más cómoda y detallada.

Respecto a la conectividad, la experiencia puede variar según el sistema operativo y el navegador utilizado. En nuestro caso, utilizando una Lenovo ThinkPad T470s con Linux Mint Cinnamon, no fue posible utilizar conexiones Bluetooth debido a que el navegador indicaba que Web Bluetooth no estaba soportado. Esto no necesariamente constituye una limitación de Meshtastic, pero sí afecta la experiencia general de uso del cliente web.

Tampoco encontramos una opción equivalente a la función de compartir la ubicación del teléfono presente en la aplicación móvil. Aunque probablemente no sea una necesidad habitual en equipos de escritorio o portátiles, sí creemos que podría resultar útil disponer de mecanismos más simples para establecer o actualizar ubicaciones desde esta interfaz.

En definitiva, cualquier usuario familiarizado con la aplicación móvil podrá adaptarse relativamente rápido al cliente web. La lógica general de funcionamiento es similar y la curva de aprendizaje no resulta particularmente elevada. Sin embargo, también es el componente donde más margen de mejora encontramos. Actualmente cumple adecuadamente para tareas de configuración y administración, pero todavía presenta aspectos de usabilidad que podrían refinarse para ofrecer una experiencia más sólida y consistente con el resto del ecosistema Meshtastic.

## Conclusión

La usabilidad de Meshtastic no depende exclusivamente del firmware o de la aplicación móvil, sino de la interacción entre ambos. Un mismo firmware puede ofrecer experiencias muy diferentes según el hardware utilizado.

Actualmente consideramos que la aplicación móvil constituye la interfaz más madura y accesible del ecosistema, mientras que el nodo cumple principalmente el rol de proporcionar conectividad LoRa.

Desde nuestra perspectiva, la experiencia de uso más consistente se obtiene cuando cada componente cumple una función claramente definida: el nodo como medio de comunicación y la aplicación como interfaz principal de interacción.

Como toda tecnología en evolución, Meshtastic todavía presenta oportunidades de mejora. Sin embargo, el nivel de desarrollo alcanzado actualmente permite que usuarios sin conocimientos técnicos avanzados puedan aprender a utilizarla y beneficiarse de sus capacidades con un período de adaptación relativamente breve.
