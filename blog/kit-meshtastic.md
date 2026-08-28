---
slug: kit-meshtastic
title: "¿Cómo implementar Meshtastic en el combate de incendios?"
sidebar_label: "Kit Meshtastic"
authors:
  - key: MrNetsky
    title: Autor
  - key: nicopace
    title: Colaborador
tags:
  - dispositivos
  - bitacora
  - meshtastic
---

import useBaseUrl from '@docusaurus/useBaseUrl';

La tecnología Meshtastic junto al protocolo LoRa tiene muchas potencialidades. Sin embargo, una vez superado el entusiasmo inicial, surge una pregunta fundamental:

**¿Cómo implementamos esta tecnología en un contexto real de combate de incendios?**

La respuesta parece sencilla hasta que comenzamos a profundizar en el problema. ¿Qué dispositivos deberían utilizarse? ¿Quiénes van a utilizarlos? ¿Qué funciones debería cumplir cada uno? ¿Cómo se integra esta tecnología con los métodos de trabajo ya existentes?

En este artículo compartiremos parte del proceso que nos llevó a replantear varias de nuestras ideas iniciales y a formular nuevas preguntas que todavía estamos intentando responder.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/blog_kit_meshtastic(1).png")}
    alt="Ilustración del problema de implementación de Meshtastic"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
  <p>****</p>
</div>

## Nuestra postura inicial
En un principio creíamos que cada combatiente debía portar un nodo Meshtastic. La idea parecía lógica: permitir que todos pudieran comunicarse entre sí y, al mismo tiempo, conocer la ubicación de cada integrante de la brigada ante cualquier eventualidad.

También asumimos que el dispositivo ideal debía contar con pantalla. De esta forma, cada combatiente podría leer mensajes y enviar respuestas predefinidas directamente desde el propio nodo.

Otra de nuestras preocupaciones era el uso de los equipos con guantes. Considerábamos que un combatiente no debería verse obligado a quitarse elementos de protección para utilizar una herramienta de comunicación. Bajo esa premisa, nos preguntábamos si este tipo de dispositivos serían realmente prácticos durante una intervención.

Con el tiempo descubrimos que algunas de estas suposiciones eran correctas y otras no tanto.

## La charla con una brigada de combatientes del fuego
La conversación con la brigada de Chiviquín resultó reveladora.

Nos permitió obtener un panorama mucho más cercano a la realidad operativa y contrastar varias de nuestras ideas con la experiencia de quienes efectivamente combaten incendios.

Por ejemplo, descubrimos que los combatientes no siempre mantienen colocados los guantes durante toda la operación. Aunque desde el punto de vista de la seguridad esto no sea lo ideal, la realidad es que muchas tareas requieren interactuar con herramientas y aplicaciones que ya forman parte de su trabajo cotidiano.

También observamos que aplicaciones como WhatsApp u OruxMaps forman parte de las herramientas que utilizan para coordinar actividades, compartir información y orientarse en el terreno.

Esta conversación nos ayudó a comprender que el problema no debía analizarse únicamente desde las características técnicas del hardware, sino también desde las prácticas reales de quienes lo utilizarían.

## Cambiando de perspectiva
Para ese momento ya habíamos adquirido y probado gran parte de los dispositivos que inicialmente habíamos considerado para el proyecto.

A medida que acumulábamos experiencia con diferentes modelos y contrastábamos nuestras observaciones con la realidad operativa de los brigadistas, comenzamos a cuestionar otra de nuestras ideas iniciales: la necesidad de que todos los combatientes utilizaran nodos con pantalla.

Si bien las pantallas ofrecen ventajas evidentes, los dispositivos tipo tarjeta comenzaron a parecer una alternativa más adecuada dentro de las opciones disponibles actualmente en el mercado. Son más compactos, livianos, simples de transportar y, en algunos casos, cuentan con certificaciones de protección que resultan especialmente interesantes para entornos exigentes.

También comenzamos a considerar que, independientemente del nodo utilizado, resulta difícil evitar por completo el uso del teléfono móvil. Sin embargo, creemos que Meshtastic tiene el potencial de reducir la cantidad de aplicaciones necesarias durante una operación.

Actualmente muchos combatientes recurren a herramientas como WhatsApp para la comunicación y OruxMaps para la navegación y visualización de información geográfica. En teoría, Meshtastic reúne parte de estas capacidades en una única aplicación, permitiendo intercambiar mensajes y utilizar un mapa compartido dentro de la misma plataforma.

No obstante, todavía observamos algunas limitaciones importantes. Por ejemplo, actualmente Meshtastic no permite intercambiar imágenes ni mensajes de voz, recursos que suelen utilizarse con frecuencia durante las operaciones. Del mismo modo, aunque las capacidades de mapa resultan muy útiles, todavía existen herramientas y funcionalidades presentes en aplicaciones especializadas como OruxMaps que podrían complementar significativamente la experiencia de uso.

Por este motivo, más que considerar a Meshtastic como un reemplazo completo de estas herramientas, lo vemos como una tecnología con un enorme potencial y un amplio margen de evolución para adaptarse mejor a las necesidades del terreno.

Sin embargo, esta conclusión vino acompañada de otra observación importante: creemos que ninguno de los dispositivos disponibles actualmente fue diseñado específicamente para el combate de incendios.

Desde nuestra perspectiva, todavía existen necesidades que el hardware actual no cubre completamente. Algunas de ellas podrían resolverse con pantallas más grandes, botones físicos de mayor tamaño, sistemas de ingreso de texto más eficientes o diseños mejor adaptados al uso con elementos de protección personal.

Naturalmente, un cambio de hardware de este tipo también requeriría adaptaciones en el firmware para aprovechar adecuadamente las nuevas capacidades.

## Nuestra conclusión actual
Luego de las pruebas realizadas, de las conversaciones con brigadistas y de la experiencia acumulada utilizando diferentes dispositivos, hemos llegado a algunas conclusiones que, aunque todavía pueden cambiar con futuras pruebas, hoy orientan nuestra forma de pensar esta tecnología.

La primera es que no creemos que exista un kit universal para el combate de incendios. Cada brigada opera en terrenos diferentes, con necesidades distintas y bajo condiciones que pueden variar enormemente de una región a otra.

Particularmente, creemos que el relieve del terreno tiene una influencia determinante en el desempeño de las comunicaciones LoRa. Nuestra experiencia hasta el momento indica que la presencia de elevaciones, quebradas o montañas afecta mucho más a las comunicaciones que la vegetación. Por este motivo, no consideramos adecuado definir una cantidad fija de nodos repetidores para todas las situaciones.

Creemos que cada brigada debería estudiar el territorio donde opera habitualmente y planificar la cantidad y ubicación de los repetidores en función de ese análisis. Desde nuestra perspectiva, la infraestructura de la red debe adaptarse al terreno y no al revés.

También consideramos que la información de posición tiene un enorme valor operativo. Aunque algunas brigadas nos han manifestado que sus integrantes rara vez se separan durante una intervención, creemos que las situaciones imprevistas forman parte de cualquier emergencia. Poder conocer la última ubicación reportada por un combatiente puede aportar información valiosa cuando las cosas no salen según lo planificado.

Por este motivo, actualmente nos inclinamos por la idea de que cada combatiente disponga de su propio nodo. Dentro de las opciones disponibles hoy en el mercado, los dispositivos tipo card son los que mejor se adaptan a esta función debido a su tamaño, peso y simplicidad de uso.

Al mismo tiempo, no creemos que Meshtastic deba asumir hoy el rol de sistema principal de comunicaciones. La tecnología todavía presenta limitaciones importantes y no consideramos prudente depender exclusivamente de ella en situaciones donde la seguridad de las personas está en juego.

Sin embargo, sí creemos que puede convertirse en una herramienta complementaria de enorme valor. La posibilidad de compartir ubicaciones, mensajes y otra información operativa puede mejorar significativamente la conciencia situacional de los equipos y aportar capacidades que los sistemas tradicionales de comunicación no ofrecen de forma nativa.

Quizás la pregunta de ahora en adelante sea cómo integrar esta tecnología dentro de los procedimientos existentes para aprovechar sus fortalezas sin ignorar sus limitaciones.

Por el momento, esa es la dirección que consideramos más prometedora y sobre la cual continuaremos realizando pruebas, desarrollando materiales de capacitación y dialogando con brigadas que nos ayuden a seguir aprendiendo.

## ¿Por dónde comenzar?
A lo largo de este artículo hemos argumentado que no creemos que exista un kit universal para el combate de incendios. Las necesidades de cada brigada dependen del terreno, la cantidad de personal disponible, el área de cobertura requerida y los procedimientos de trabajo propios de cada organización.

Sin embargo, también entendemos que quienes se acercan por primera vez a esta tecnología necesitan un punto de partida. Por ese motivo, proponemos dos configuraciones iniciales que pueden servir como referencia para comenzar a experimentar y adquirir experiencia operativa.

### Kit mínimo
Pensado para brigadas que desean realizar las primeras pruebas de campo con la menor inversión posible.
- 1 nodo portátil tipo tarjeta por cuadrilla.
- 1 nodo portátil tipo tarjeta para la base de operaciones. 
- 1 nodo repetidor.

En este escenario, el nodo portátil de cada cuadrilla sería utilizado por su responsable para intercambiar mensajes y compartir información operativa, mientras que el nodo asignado a la base permitiría mantener la coordinación entre las distintas cuadrillas. El repetidor tendría como objetivo extender la cobertura y mejorar la conectividad de la red.

Esta configuración no permite conocer la ubicación individual de todos los integrantes, pero sí brinda una primera aproximación al funcionamiento de Meshtastic en un entorno real.

### Kit máximo
Pensado para brigadas que buscan obtener el mayor beneficio posible de las capacidades actuales de la tecnología.
- 1 nodo portátil tipo tarjeta por combatiente.
- 1 nodo portátil adicional de reserva.
- 1 nodo portátil tipo tarjeta para la base de operaciones.
- La cantidad de repetidores necesaria para cubrir el área de operación habitual.
- 1 repetidor adicional de reserva.

En este modelo, cada combatiente puede transmitir su posición, mientras que el encargado de participar de la red sigue siendo el responsable de las comunicaciones de la cuadrilla, mejorando la conciencia situacional del equipo y permitiendo disponer de información más detallada sobre el despliegue en el terreno.

La cantidad exacta de repetidores no puede definirse de forma general, ya que depende directamente de las características geográficas de la zona. Por este motivo, consideramos indispensable realizar un estudio previo del terreno para determinar cuántos repetidores son necesarios y dónde deberían ubicarse.

Por ejemplo, si una brigada opera habitualmente en una zona donde un único repetidor proporciona cobertura suficiente para una cuadrilla de cinco combatientes, una configuración máxima podría estar compuesta por:
- 6 nodos portátiles tipo tarjeta (5 operativos y 1 de reserva).
- 2 repetidores (1 operativo y 1 de reserva).

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/blog_kit_meshtastic(2).png")}
    alt="Propuestas de kits"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

## Nuestra primera experiencia
La propuesta de kit máximo presentada en este artículo representa la dirección hacia la que actualmente creemos que deberían orientarse las futuras implementaciones. Sin embargo, durante nuestra primera capacitación práctica todavía no disponíamos de la cantidad de dispositivos necesaria para equipar a las brigadas siguiendo esa propuesta.

Por este motivo, decidimos adaptar el equipamiento disponible sin perder de vista los objetivos del proyecto. Más que intentar replicar el kit que proponemos, buscamos validar los criterios sobre los cuales fue pensado y seguir obteniendo información que nos permita confirmar o replantear nuestras hipótesis.

Cada una de las tres brigadas recibió un conjunto de dispositivos compuesto por un RAK WisMesh Tag, un Seeed Studio SenseCAP T1000-E, un Meshnology N37 y un Elecrow ThinkNode M1, acompañados por un Seeed Studio SenseCAP Solar Node P1 utilizado como repetidor.

La selección respondió a dos criterios. El primero fue la disponibilidad de equipamiento del proyecto, que todavía no nos permitía entregar un nodo tipo tarjeta a cada combatiente ni disponer de equipos de reserva para cada brigada. El segundo fue la necesidad de continuar evaluando distintos formatos de hardware. Incorporar dispositivos con características diferentes nos permitió contrastar nuestras hipótesis con la experiencia de los combatientes y obtener observaciones sobre aspectos como la portabilidad, la facilidad de uso y la interacción con cada tipo de nodo.

Creemos que este tipo de experiencias son fundamentales para el desarrollo del proyecto. Nuestro objetivo no es validar un dispositivo en particular, sino construir criterios que nos permitan comprender qué características resultan realmente valiosas para el combate de incendios y, a partir de ello, seguir mejorando nuestras recomendaciones sobre cómo implementar esta tecnología en el terreno.

---

Creemos que este tipo de experiencias son fundamentales para el desarrollo del proyecto. En esta etapa no buscamos validar dispositivos, sino validar criterios que nos permitan comprender qué características resultan realmente valiosas para el combate de incendios.

Todavía nos queda mucho por aprender. Este artículo refleja únicamente el estado actual de nuestras pruebas y conclusiones, por lo que no debe interpretarse como un resultado definitivo. Con el tiempo continuaremos publicando nuevas experiencias, compartiendo los avances del proyecto y actualizando aquellas recomendaciones que la evidencia nos invite a replantear.
