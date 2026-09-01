---
slug: flasheo-de-repetidores
title: "El problema de flashear nodos ubicados en posiciones estratégicas" 
sidebar_label: "Flasheo de repetidores"
authors:
  - key: MrNetsky
    title: Autor
  - key: nicopace
    title: Colaborador
tags:
  - dispositivos
  - meshtastic
---

El proceso de actualización del firmware es importante para todos los nodos y, en dispositivos portátiles, suele ser relativamente sencillo de realizar. Sin embargo, la situación cambia cuando hablamos de nodos instalados en puntos estratégicos y elevados con el objetivo de ampliar la cobertura de la red.

Dejar un nodo con la última versión disponible del firmware al momento de instalarlo es relativamente sencillo. El problema aparece cuando necesitamos actualizarlo después de su instalación, ya que acceder físicamente al dispositivo puede requerir desplazarse hasta el lugar donde se encuentra e incluso realizar tareas de ascenso.

Actualmente, tampoco consideramos necesario realizar este procedimiento cada vez que aparece una nueva versión. Hasta el momento, ninguna de las versiones estables que hemos utilizado nos ha impedido comunicar nodos que ejecutan versiones anteriores. Desde que comenzamos nuestras pruebas, hemos trabajado principalmente con las versiones estables 2.6.9, 2.7.15 y 2.7.26, siendo esta última la que utilizamos actualmente.

Aun así, consideramos que la actualización de nodos instalados en ubicaciones de difícil acceso es un problema que merece ser estudiado. Por este motivo, hemos evaluado dos posibles alternativas para realizar el procedimiento sin necesidad de retirar el nodo de su ubicación: Bluetooth y conexión serial.

:::info Alcance de las pruebas
Todos los procedimientos de flasheo descritos en este artículo fueron realizados y comprobados utilizando dispositivos Android. Los procedimientos mediante iOS no han sido probados por nuestro equipo, por lo que no podemos asegurar su funcionamiento en este sistema operativo.
:::

## Flasheo vía Bluetooth

:::warning Nivel avanzado
El contenido de este apartado requiere conocimientos técnicos adicionales a los procedimientos habituales de actualización. Si no estás familiarizado con el modo DFU y el funcionamiento del flasheo OTA, recomendamos utilizar el procedimiento vía serial explicado más adelante.
:::

El flasheo OTA (Over-The-Air) permite actualizar el firmware de determinados dispositivos de forma inalámbrica, utilizando Bluetooth Low Energy (BLE), sin necesidad de conectar 
físicamente el nodo a una computadora.

Para explorar esta posibilidad tuvimos en cuenta dos alternativas: la última versión de la aplicación Meshtastic para Android, obtenida desde el repositorio oficial de GitHub de la aplicación, y la aplicación nRF Connect, desarrollada por Nordic Semiconductor, fabricante de los microcontroladores nRF52 utilizados por algunos de los nodos que forman parte de nuestras pruebas, como el SenseCAP Solar Node P1 y el ThinkNode M6.

### Aplicación Meshtastic

Con el flasheo desde la aplicación de Meshtastic no hemos obtenido buenos resultados. La primera vez que intentamos utilizar esta opción, hace aproximadamente ocho meses, lo hicimos debido a nuestra inexperiencia y sin conocer las limitaciones del procedimiento. Como consecuencia, tuvimos que desmontar el dispositivo, desconectar la batería, realizar el flasheo mediante otra vía y volver a ensamblarlo.

Decidimos repetir la experiencia utilizando la última versión de la aplicación disponible desde GitHub. En esta ocasión observamos una diferencia importante respecto de aquella primera experiencia: la aplicación consigue colocar el nodo en modo DFU, pero posteriormente no logra completar el proceso.

Nuestra hipótesis es que, una vez que el nodo entra en modo DFU, se pierde la conexión Bluetooth y la aplicación deja de poder comunicarse con el dispositivo, impidiendo que el proceso de actualización continúe.

Sin embargo, este comportamiento nos permitió encontrar una alternativa que resultó útil para continuar el procedimiento: una vez que el nodo se encuentra en modo DFU, es posible conectarlo a una computadora y continuar el proceso desde el Web Flasher de Meshtastic, como si se hubiera puesto el dispositivo en DFU mediante el procedimiento habitual.

Al finalizar el procedimiento, el nodo vuelve a funcionar con normalidad. No obstante, no podemos afirmar que este haya sido el comportamiento que observamos durante nuestro primer intento, ya que aquella experiencia no fue registrada adecuadamente y nuestros recuerdos de ese momento, sumados a la poca experiencia que teníamos entonces, no son suficientes para establecer una conclusión.

### Aplicación nRF Connect

La segunda alternativa que estamos evaluando consiste en realizar el proceso mediante **nRF Connect**, una herramienta de Nordic Semiconductor.

El procedimiento es diferente al utilizado mediante la aplicación de Meshtastic, principalmente porque requiere trabajar con un archivo de firmware en formato `.zip`. Esto también implica una diferencia respecto del procedimiento de actualización mediante Web Flasher que hemos utilizado habitualmente, donde para los dispositivos nRF52 trabajamos con archivos `.uf2`.

Para realizar esta prueba es necesario obtener el archivo correspondiente a la versión estable del firmware desde el [repositorio de GitHub de Meshtastic](https://github.com/meshtastic/firmware/releases). En nuestro caso, descargamos el archivo `firmware-nrf52840-2.7.26.54e0d8d.zip` y, dentro de este archivo, buscamos el firmware correspondiente al dispositivo que estamos utilizando.

Como la prueba se está realizando con un WioTracker L1 Pro, el archivo correspondiente es:

`firmware-seeed_wio_tracker_L1-2.7.26.54e0d8d-ota`

Con todos los elementos necesarios preparados, nos enlazamos desde la aplicación con el nodo. Luego nos dirigimos a la configuración y ajustamos la cantidad de paquetes a **8**, ya que lo más probable es que esta opción aparezca configurada en 10.

Es importante destacar que esta no es una sugerencia propia. Al buscar información sobre el procedimiento, encontramos un blog de MeshCore que realiza esta recomendación y, además, en conversaciones con la comunidad de Discord recibimos la misma sugerencia.

Luego nos dirigimos a nuestro dispositivo y veremos, en la parte superior de la pantalla, una opción que dice `DFU`. Al seleccionarla aparecerá un menú con cuatro opciones. En este caso utilizaremos **Distribution packet (ZIP)**, que suele estar seleccionada por defecto.

Después de presionar **OK**, la aplicación nos permitirá buscar el archivo de firmware. Una vez localizado y seleccionado, comenzará el proceso de actualización, que puede demorar varios minutos. Durante este tiempo podremos observar el progreso y la velocidad a la que se realiza el proceso.

Una vez finalizado, el nodo se reiniciará y volverá a conectarse automáticamente con la aplicación.

Podremos comprobar si el proceso se realizó correctamente de dos maneras. Si el nodo cuenta con pantalla, al iniciarse mostrará la versión del firmware que tiene instalada. También podemos comprobarlo desde la aplicación, ingresando en **Device Information → Firmware Revision String**, donde se mostrará la versión del firmware instalada.

Es importante aclarar que el flasheo de dispositivos mediante OTA es posible, pero existen varias advertencias respecto de este procedimiento, ya que un fallo durante la actualización podría **brickear** el nodo.

Nuestros resultados no fueron esos. A través de la aplicación de Meshtastic, el proceso simplemente quedó detenido en el modo DFU, situación que pudimos resolver con facilidad conectando posteriormente el nodo a una PC y continuando el proceso de actualización. En cambio, mediante la aplicación nRF Connect pudimos completar el procedimiento correctamente.

A pesar de estos resultados, por el momento no creemos que valga la pena asumir el riesgo de realizar una actualización mediante alguna de estas dos vías. Entendemos que mantener actualizado el firmware es importante, pero no consideramos que sea imprescindible realizarlo mediante OTA.

Por este motivo, recomendamos utilizar el procedimiento que explicamos en el siguiente apartado o recurrir al Meshtastic Web Flasher. Si aún así se decide realizar la actualización mediante OTA, es importante hacerlo teniendo en cuenta los riesgos asociados al procedimiento.

Si en el futuro encontramos mejoras significativas en alguno de estos procesos, las documentaremos y compartiremos los resultados en una nueva actualización.

### Flasheo vía serial

La conexión serial es, hasta el momento, la alternativa que consideramos más práctica para actualizar un nodo instalado en una ubicación de difícil acceso. Sin embargo, creemos que no es necesario realizar este procedimiento cada vez que aparece una nueva versión estable del firmware.

Nuestra recomendación inicial es evaluar la necesidad de actualizar el nodo y, salvo que exista un motivo concreto para hacerlo antes, considerar la actualización cada dos o tres versiones estables. Esto podría representar aproximadamente una o dos intervenciones por año, aunque la frecuencia dependerá de la evolución del firmware y de las necesidades de cada instalación.

Esta recomendación busca reducir la cantidad de intervenciones necesarias sobre los nodos instalados en lugares de difícil acceso. Cada organización podrá, naturalmente, establecer una frecuencia diferente si considera necesario mantener sus equipos permanentemente actualizados.

Existe, además, una excepción importante: cuando una nueva versión introduce cambios incompatibles (breaking changes) que impiden la comunicación con otros nodos de la red, o cuando incorpora una funcionalidad que resulte especialmente necesaria para la operación. En esos casos, puede estar justificado realizar la actualización independientemente del intervalo establecido.

Nuestra propuesta es evitar, siempre que sea posible, desmontar el nodo o trasladarlo hasta una computadora para realizar el procedimiento. En los dispositivos compatibles, el objetivo es llevar el firmware hasta el lugar donde se encuentra instalado el nodo y realizar allí la actualización utilizando un teléfono.

El procedimiento que hemos planteado es el siguiente. Antes de desplazarse hasta el nodo, recomendamos llevar un nodo portátil adicional que permita comprobar la comunicación con el repetidor una vez finalizada la actualización. De esta manera, no será necesario depender únicamente de la información que muestra el propio dispositivo para verificar que el nodo volvió a integrarse correctamente en la red.

1. Identificar el nodo que debe actualizarse y descargar previamente en el teléfono el archivo de firmware correspondiente en formato `.uf2`.
2. Llevar un cable USB-C a USB-C que permita la transferencia de datos. Es recomendable comprobar su funcionamiento antes de desplazarse hasta el nodo.
:::tip Recomendación
Si el acceso al nodo requiere desplazarse por zonas elevadas, pendientes o terrenos irregulares, recomendamos utilizar una correa, cordón o sistema similar para asegurar el teléfono. Esto permite mantener las manos libres y reduce el riesgo de que el dispositivo se caiga durante el procedimiento.
:::
3. Una vez en el lugar donde se encuentra instalado el nodo, acceder al dispositivo.
4. Poner el nodo en modo DFU presionando dos veces consecutivas el botón RST (Reset).
5. Conectar el cable USB al nodo.
6. Conectar el otro extremo del cable al teléfono. Dependiendo del modelo y del sistema operativo, puede ser necesario habilitar o autorizar la transferencia de datos mediante USB. El nodo debería aparecer como una unidad de almacenamiento.
7. Buscar el archivo de firmware descargado previamente y copiarlo a la unidad correspondiente al nodo.
8. Esperar a que el nodo complete el proceso y se reinicie. Una vez iniciado nuevamente, conectarse a él mediante la aplicación Meshtastic, ya sea por conexión serial o Bluetooth, y comprobar que funciona correctamente.
9. Si el procedimiento se completó correctamente, puede retirarse del lugar. Si no fue posible actualizarlo, puede intentarse nuevamente. Si el segundo intento tampoco resulta exitoso, recomendamos retirar el nodo y realizar el procedimiento mediante una computadora.

:::warning El proceso no funciona en todos los Andriod
Durante nuestras pruebas pudimos completarlo correctamente utilizando un Xiaomi POCO X6 Pro 5G, mientras que no fue posible realizarlo con un Samsung Galaxy S21 FE.

Por este motivo, recomendamos probar previamente el procedimiento con un nodo en un entorno controlado, antes de intentar actualizar un nodo instalado en una ubicación de difícil acceso. De esta manera, podrá comprobar si el teléfono reconoce correctamente algún dispositivo LoRa con chip nRF52 en modo DFU y permite copiar el archivo de firmware.

No recomendamos realizar la primera prueba directamente sobre un nodo instalado en altura o en un lugar de difícil acceso.
:::

## Conclusiones

Actualizar el firmware de un nodo instalado en una ubicación de difícil acceso presenta desafíos que no existen en los dispositivos portátiles. Por este motivo, consideramos importante evaluar alternativas que permitan realizar el procedimiento sin necesidad de desmontar el equipo.

Las pruebas realizadas nos permitieron comprobar que existen alternativas para actualizar un nodo de forma inalámbrica mediante Bluetooth, aunque por el momento consideramos que el riesgo asociado al proceso OTA no justifica su utilización como método habitual. En cambio, la actualización mediante conexión serial nos resulta una alternativa más práctica para los dispositivos compatibles, ya que permite trasladar el procedimiento hasta el lugar donde se encuentra instalado el nodo.

También consideramos importante no convertir la actualización del firmware en una tarea rutinaria. Mientras las versiones continúen siendo compatibles entre sí, creemos que tiene más sentido evaluar la necesidad de actualizar y realizar el procedimiento cuando exista un motivo concreto para hacerlo.

Este proceso de experimentación todavía no está cerrado. Continuaremos evaluando las distintas alternativas y, a medida que obtengamos nuevos resultados o encontremos mejoras en los procedimientos, publicaremos nuevas experiencias.
