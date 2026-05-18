---
slug: configuracion-meshtastic
title: Guía de configuración inicial paso a paso para tu dispositivo Meshtastic
sidebar_label: Configuración inicial Meshtastic
authors:
  - key: MrNetsky
    title: Autor
  - key: nicopace
    title: Colaborador
  - key: aguslasp
    title: Colaborador
tags: 
  - dispositivos
  - meshtastic
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

:::warning Atención
Este artículo fue creado en mayo de 2026. Podés consultar aquí la fecha de su última actualización. Tené en cuenta que Meshtastic evoluciona constantemente, por lo que algunas opciones o procedimientos pueden cambiar con el tiempo.
:::

En esta sección vas a aprender a configurar tu primer nodo Meshtastic y dejarlo operativo. A lo largo de un proceso simple, vamos a cubrir tres aspectos principales:

- <u>*Configuración inicial*</u>: Cómo encender el dispositivo, vincularlo a tu teléfono mediante la app Meshtastic (Bluetooth) y establecer las configuraciones necesarias para comenzar a operar.
- <u>*Parámetros de comunicación*</u>: Cómo definir la región, el canal y otras configuraciones clave para poder comunicarte con otros nodos.
- <u>*Primeros pasos en la red*</u>: Cómo integrarte a la malla y comenzar a utilizar el sistema de mensajería.

El objetivo es que, en pocos minutos, puedas tener tu nodo funcionando y listo para integrarse a la malla.

## Obtención de un dispositivo

Existe un gran variedad de dispositivos y el que hayas de elegir dependerá de su [*función*](http:///blog/tipos-de-dispositivos), también hay una gran variedad de [*marcas*](http:///blog/fabricantes-ensambladores) que se dedican al universo Meshtastic. Nosotros no usaremos uno en particular para esta guía porque el proceso es similar para todos.

## Conexión

:::danger ¡Importante!
Antes de encender cualquier equipo LoRa, conectá la antena al dispositivo. De lo contrario, podrías dañarlo.
:::

:::warning Advertencia  
Si el nodo que adquiriste ya viene con Meshtastic instalado, podés comenzar directamente con la configuración. En caso contrario, dirigite al apartado de [<u>**firmware**</u>](#firmware) y luego continuá con esta sección.  
:::

Podés enlazar tu nodo Meshtastic a un teléfono o computadora de dos formas: por USB (serial) o mediante Bluetooth.

- **Conexión por USB (serial):**
Simplemente conectá el dispositivo a través de un cable USB. La app lo reconocerá automáticamente.
- **Conexión por Bluetooth:**
Al encender el nodo, podrás vincularlo desde tu teléfono o PC como cualquier otro dispositivo Bluetooth.
  - Si el nodo tiene pantalla, mostrará un código de emparejamiento que deberás ingresar en el dispositivo desde el cual te estás conectando.
  - Si el nodo no tiene pantalla, el código de emparejamiento por defecto es *123456*.

Este código se utiliza únicamente la primera vez para establecer la conexión.

## Preparación del dispositivo

### Configuraciones de radio

Estas configuraciones vienen preconfiguradas para facilitar el uso del dispositivo y, en la práctica, funcionan correctamente. No obstante, si tenés los conocimientos necesarios, podés optar por no utilizarlas y realizar una configuración completamente personalizada.

#### Región

:::info información
Estas configuraciones están pensadas para Argentina. Si te encontrás en otro país, es posible que debas elegir una región diferente, aunque el procedimiento es el mismo.
:::

La configuración de la región es esencial para poder comunicarte con otros dispositivos, ya que define las frecuencias de operación.

Podés configurarla de tres maneras: desde el dispositivo, desde la app del celular o mediante Meshtastic CLI (Command Line Interface). En este artículo no se abordará el uso de esta última herramienta.

- **Desde el dispositivo (si tiene pantalla):**
  - Al iniciar, antes de vincularlo con un teléfono (en firmware igual o superior a 2.7.15), se te solicitará configurar la región. Deberás elegir *ANZ (Australia/Nueva Zelanda)*.
  - También podés hacerlo desde el menú: LoRa Info → LoRa Region, donde deberás seleccionar *ANZ*.
- **Desde la app:**
  - Luego de la vinculación, si el dispositivo no tiene región configurada, aparecerá una opción para definirla. Allí deberás seleccionar *Australia/Brasil/Nueva Zelanda*.
  - También podés modificarla en cualquier momento desde Ajustes → LoRa.

Esto se debe a que en estos países, al igual que en Argentina, se utilizan frecuencias entre 902 y 928 MHz (comúnmente referidas como banda de 915 MHz). Estas frecuencias son de uso libre y no requieren una licencia especial para operar.

#### Radio presets

Los radio presets son un conjunto de tres parámetros preconfigurados: **SF** (*Spreading Factor*), **BW** (*Bandwidth*) y **CR** (*Coding Rate*). En conjunto, estos definen cómo se transmite la señal, afectando directamente el alcance, la velocidad de transmisión y la tolerancia a errores.

De forma simplificada, cuanto mayor alcance se busca, menor será la velocidad de transmisión y mayor la robustez de la señal.

Por defecto, el dispositivo viene configurado en **LongFast**, por lo que no es necesario modificarlo para un uso general. Podrás comunicarte con cualquier nodo que tenga configurada la misma región y el mismo radio preset.

En caso de necesitar ajustarlo, podés elegir entre los siguientes presets: *LongSlow*, *LongMedium*, *LongFast*, *MediumFast*, *MediumSlow*, *ShortSlow*, *ShortFast* y *ShortTurbo*.

Podés modificar esta configuración desde:

- *Dispositivo (con pantalla)*: LoRa → Radio Preset
- *App móvil*: Ajustes → LoRa

### Firmware

Si el nodo que adquiriste ya viene con Meshtastic instalado, podés comenzar a utilizarlo completando las configuraciones anteriores. No obstante, dado que se trata de una tecnología en constante evolución, es recomendable mantener el firmware actualizado.

En caso de que el dispositivo no tenga Meshtastic instalado, el proceso de instalación y actualización es el mismo, por lo que deberás realizarlo manualmente.

Existen dos métodos para hacerlo: vía BLE (Bluetooth Low Energy) o mediante conexión USB.

Desde este espacio, no recomendamos el uso de BLE (al menos a la fecha de publicación de este artículo), ya que durante las pruebas el proceso resultó inestable y puede dejar el dispositivo en un estado no funcional, requiriendo intervención manual para recuperarlo.

El método por USB, en cambio, es más estable y confiable, por lo que es el recomendado.

El procedimiento varía según el tipo de hardware del nodo (nRF52 o ESP32). A continuación, se detallan los pasos para cada caso:

<Tabs>
  <TabItem
    value="nrf52"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>nRF52</span>
      </div>
    }
    default
  >

1. Ingresá a la [herramienta de flasheo](https://flasher.meshtastic.org/).
2. Seleccioná el dispositivo que vas a utilizar.
   Si no lo encontrás fácilmente, podés filtrar por marca.
   En caso de dispositivos ensamblados, deberás identificar el modelo de la placa base.
   Por ejemplo un Meshnology N37 corresponde a un Wio Tracker L1. Para saber qué placa lleva, lee bien la descripción del dispositivo que vayas a comprar. En nuestro caso particular ya sabíamos qué placa traía, pero como había que armarlo, en la caja que venía la placa también especificaba esta importante información.
3. Seleccioná la versión de firmware.
   - Alpha: inestable
   - Beta: estable  
   Se recomienda utilizar la última versión beta disponible.
4. Conectá el dispositivo por USB. Ten en cuenta que:
    - Podés hacerlo en cualquier momento del proceso.
    - Usar cable USB de datos (NO sólo carga).
    - NO desconectar durante el proceso.
5. Ingresá el dispositivo en modo DFU (Device Firmware Update):
   - Oprima dos veces el botón de reset.
   - El dispositivo aparecerá como una unidad de almacenamiento en el sistema.
6. Recomendación de instalación según el tipo de pantalla del dispositivo:

<Tabs>
  <TabItem
    value="led"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>LCD, LED o sin pantalla</span>
      </div>
    }
    default
  >

Se recomienda descargar el archivo de extensión .uf2 en la carpeta del dispositivo. El proceso es similar a cuando descarga cualquier otro archivo y lo ubica en la capeta que desea de su computador. Esto aplica para todos los SO (Linux, MacOS y Windows).

También puedes descargarlo en cualquier carpeta del equipo y luego copiar o mover dicho archivo a la carpeta a la del dispositivo.

<div style={{ display: 'flex', gap: '20px', justifyContent: 'center' }}>
  <div style={{ flex: 1, textAlign: 'center' }}>
    <img
      src={useBaseUrl("/img/flash_nRF52_1.png")}
      alt="flash_nRF52_1"
      style={{
        maxWidth: '100%',
        height: 'auto',
        maxHeight: '300px',
        objectFit: 'contain'
      }}
    />
    <p>**Oprima "Descargar UF2"**</p>
  </div>

  <div style={{ flex: 1, textAlign: 'center' }}>
    <img
      src={useBaseUrl("/img/flash_nRF52_2.png")}
      alt="flash_nRF52_2"
      style={{
        maxWidth: '100%',
        height: 'auto',
        maxHeight: '300px',
        objectFit: 'contain'
      }}
    />
    <p>**Elija la carpeta de descarga**</p>
  </div>
</div>

---
  
  </TabItem>

  <TabItem
    value="inkpaper"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>E-Paper</span>
      </div>
    }
  >

Esta interfaz sólo va a estar disponible para los nodos cuyas pantallas sean de papel electrónico. Para instalarla, deberás habilitar la opción *Instalar pantalla InkHUD*, porque viene deshabilitada por default.

Se recomienda descargar el archivo de extensión .uf2 en la carpeta del dispositivo. El proceso es similar a cuando descarga cualquier otro archivo y lo ubica en la capeta que desea de su computador. Esto aplica para todos los SO (Linux, MacOS y Windows).

También puedes descargarlo en cualquier carpeta del equipo y luego copiar o mover dicho archivo a la carpeta a la del dispositivo.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/InkHUD_flash.png")}
    alt="flash_inkhud_nrf52"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

Es una interfaz más simple, con menos independecia del teléfono, posee como función destacada la rotación de pantalla, que le permite usar el dispositivo de una manera más cómoda, esto aplica para los nodos como el *Elecrow ThinkNode M1*, *LilyGo T-Echo* y *Heltec MeshPocket Qi2* (son los nodos donde pudimos probar esta función).

---

  </TabItem>
</Tabs>

  </TabItem>

  <TabItem
    value="esp32"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>ESP32</span>
      </div>
    }
  >

1. Ingresá a la [herramienta de flasheo](https://flasher.meshtastic.org/)
2. Seleccioná el dispositivo que vas a utilizar.
   Si no lo encontrás fácilmente, podés filtrar por marca.
   En caso de dispositivos ensamblados, deberás identificar el modelo de la placa base.
   Por ejemplo un Meshnology N37 corresponde a un Wio Tracker L1. Para saber qué placa lleva, lee bien la descripción del dispositivo que vayas a comprar. En nuestro caso particular ya sabíamos qué placa traía, pero como había que armarlo, en la caja que venía la placa también especificaba esta importante información.
3. Seleccioná la versión de firmware.
   - Alpha: inestable
   - Beta: estable  
   Se recomienda utilizar la última versión beta disponible.
4. Conectá el dispositivo por USB. Ten en cuenta que:
    - Podés hacerlo en cualquier momento del proceso.
    - Usar cable USB de datos (NO sólo carga).
    - NO desconectar durante el proceso.
5. Recomendación de instalación según el típo de pantalla del dispositivo:

<Tabs>
  <TabItem
    value="lcd"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>LCD, LED o sin pantalla</span>
      </div>
    }
    default
  >

Se recomienda realizar un borrado completo e instalación limpia.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/flash_ESP32.png")}
    alt="Flash_ESP32"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

---
  
  </TabItem>

  <TabItem
    value="epaper"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>E-Paper</span>
      </div>
    }
  >

Se recomienda realizar un borrado completo e instalación. No se recomienda hacer uso de esta interfaz (al menos a la fecha de la emisión de este artículo.), ya que para el Elecrow ThinkNode M5 Pro no pudimos hacer funcionar el dispositivo con esta interfaz, tuvimos que re-flashear. Por lo que recomendamos dejar deshabilitada la opción InkHUD.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/InkHUD_flash_ESP32.png")}
    alt="Flash_InkHUD_ESP3S2"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

---

  </TabItem>

  <TabItem
    value="deck"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Tipo blackberry</span>
      </div>
    }
  >

Esta interfaz está disponible para el LilyGo T-Deck y similares. Se recomienda hacer un borrado e instalado y si quieres probarla deberás habilitar la opción de Meshtastic UI.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/flash_meshtastic_ui.png")}
    alt="Flash_Meshtastic_UI"
    style={{
      maxWidth: '100%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

Tiene una interfaz similar a la de un teléfono antiguo, que tiene múltiples funcionalidades extra que las demás interfaces no poseen, entre ellas permite cargar y ver mapas, sugiero que pruebes ambas y elijas a tu gusto.

---

  </TabItem>

</Tabs>

6. Ahora si oprimimos flashear y dejamos que se instale. Puede que cuando termine el proceso el nodo se desconecte, ya que se reinicia, como puede que no. Independientemente de lo que suceda, en la consola de instalación podrá observar el comportamiento del nodo.

  </TabItem>
</Tabs>

¿Cuánto es recomendable actualizar el firmware? Aún no definimos una métrica recomendable que permita asegurar cuánto debe usted actualizar el firmware. Sí recomendamos que haga este procedimiento apenas haya adquirido el producto, aunque no es necesario que lo haga antes de conectarlo al celular por primera vez.

## Configuraciones adicionales

Aquí se mostrarán las modificaciones que, quizás, no son tan esenciales pero que nosotros hemos llevado a cabo.

### Zona horaria

Es posible que esta se ajuste automáticamente al vincular el dispositivo con el teléfono. Sin embargo, puede haber diferencias entre la configuración del nodo y la del celular, por lo que conviene verificarla manualmente.

En caso de que no aparezca Argentina en la lista, deberás seleccionar una zona horaria equivalente. Para Argentina, se recomienda utilizar “Brasilia”.

Este proceso puede realizarse tanto desde el teléfono como desde el nodo (si este cuenta con pantalla).

- *Celular*: Ir a Ajustes → Dispositivo → Zona horaria. Es una de las últimas opciones dentro del menú “Dispositivo”. Allí podés optar por usar la zona horaria del teléfono o configurar una manualmente.  
- *Nodo*: Ir a Reloj → Clock Action → Timezone y seleccionar “BR/Brasilia” (en caso de estar en Argentina). Si te encontrás en otra región, deberás elegir la zona horaria correspondiente.

### Canales

<Tabs>
  <TabItem
    value="crear"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Crear canal</span>
      </div>
    }
    default
  >
Desde la app, entrás al apartado de Ajustes/Canales y verás un canal por defecto llamado “LongFast”. Este es el canal preconfigurado y su nombre está asociado al preset de radio que estés utilizando. Como de manera predeterminada viene configurado como “Long Range - Fast”, toma ese nombre. Si cambiás el preset de radio, vas a notar que el nombre del canal también cambia.

Dentro de “Canales” verás un signo “+”, el cual debés oprimir para crear uno nuevo. Una vez dentro, elegís el nombre del canal y, en la parte de la clave, es recomendable usar el símbolo de recargar para generar automáticamente una clave segura (AES-256). También podés definir una manualmente, pero en ese caso debés asegurarte de que sea válida y compatible.

Una vez terminado, salís de esta ventana y enviás los cambios al dispositivo. Este paso es muy importante: si no aplicás los cambios, el canal no se guardará y no tendrá efecto.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/canales_2.jpg")}
    alt="Crear_canales"
    style={{
      maxWidth: '70%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

  </TabItem>

  <TabItem
    value="compartir"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Compartir canal</span>
      </div>
    }
  >
Hay dos métodos. El primero es compartir la clave del canal. Es fundamental que todos los nodos que quieran comunicarse en este canal tengan exactamente la misma clave configurada.

El segundo método es compartir la configuración del canal mediante un código QR. Para ello, debés ir a la sección de “Conversaciones”, oprimir el botón de compartir ubicado en la parte inferior derecha de la pantalla y usar la opción “Share channels QR code”.

Es importante que actives la opción de **reemplazar**, ya que esto permitirá actualizar la configuración en el dispositivo que reciba el QR. Además, en caso de que formes parte de más de un canal, deberás deseleccionar aquellos que no quieras compartir, ya que por defecto estarán todos seleccionados.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/compartir_canal.jpg")}
    alt="Compartir_canales"
    style={{
      maxWidth: '50%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

  </TabItem>

  <TabItem
    value="unir"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Unirte a un canal</span>
      </div>
    }
  >
Hay dos métodos. El primero consiste en ingresar manualmente al canal. Dentro del menú de “Canales”, deberás oprimir el botón “+” y, en el campo de clave, pegar la clave del canal al que quieras unirte. También deberás asignarle un nombre; este puede ser cualquiera, ya que es una configuración local y no influye en el funcionamiento del canal.

El segundo método es mediante un código QR compartido por otro usuario. Por defecto, este método permite unirte a múltiples canales al mismo tiempo, aunque podés elegir a cuáles de los canales compartidos querés unirte.

Debés tener especial cuidado en este punto: NO debes seleccionar la opción de reemplazar tus canales, ya que esto eliminará los que ya tengas configurados junto con toda su información. Incluso si volvés a unirte posteriormente, los mensajes anteriores no se recuperarán. Para evitar esto, debés seleccionar la opción de **añadir**.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/suscribir_canal.jpg")}
    alt="Suscribir_canales"
    style={{
      maxWidth: '70%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

  </TabItem>

  <TabItem
    value="eliminar"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Eliminar canal</span>
      </div>
    }
  >
Dentro del menú de “Canales”, simplemente debés oprimir la “X” que se encuentra junto al nombre del canal que querés eliminar.

Tené en cuenta que la aplicación no solicitará confirmación antes de eliminarlo. Si lo haces por error, deberás cancelar la acción inmediatamente (si la opción está disponible) o salir del menú y volver a ingresar.

Al eliminar un canal, este se borra del dispositivo junto con su configuración.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/canales_4.jpg")}
    alt="Eliminar_canales"
    style={{
      maxWidth: '70%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

  </TabItem>

</Tabs>

### Ubicación

<Tabs>
  <TabItem
    value="precisa"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Ubicación precisa</span>
      </div>
    }
    default
  >
Dentro de la configuración del canal, existe una opción para enviar la posición. Debés activarla y, una vez hecho esto, habilitar la opción de ubicación precisa.

Luego, guardás los cambios y los enviás al dispositivo para que tengan efecto.
  </TabItem>

  <TabItem
    value="celular"
    label={
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        <span>Ubicación del teléfono</span>
      </div>
    }
  >
En el apartado de “Ajustes”, casi al final, existe la opción “Aportar la ubicación del teléfono a la malla”. Activarla es recomendable, ya que la ubicación del teléfono suele ser más precisa que la del GPS del nodo.

Esto no implica que se envíen dos ubicaciones. En lugar de eso, el nodo utilizará la ubicación del teléfono en vez de la suya propia.

Por este motivo, es recomendable desactivar el GPS del nodo, ya que de lo contrario consumirá la batería innecesariamente.
  </TabItem>

</Tabs>

## Primer mensaje y validación de comunicación

Una vez configurado el dispositivo, el siguiente paso es verificar que puede comunicarse correctamente dentro de la red.

### Envío de mensaje a un canal

La forma más simple de comprobar el funcionamiento es enviar un mensaje a un canal. Para ello, ingresá al canal en el que estés configurado (por ejemplo, el predeterminado), escribí un mensaje y envialo.

Si hay otros nodos en la red con la misma configuración (región, canal y radio preset), estos deberían recibir el mensaje.

Es importante destacar que si no hay otros nodos en alcance, no recibirás respuesta y esto no necesariamente significa que tu dispositivo esté mal configurado.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/escribir_canal.jpg")}
    alt="Escribir_canales"
    style={{
      maxWidth: '50%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

### Envío de mensaje a un nodo específico

Dirigite a la lista de nodos, seleccioná uno y utilizá la opción de enviar mensaje. La conversación aparecerá en la sección correspondiente, luego de enviar o recibir un primer mensaje.

<div style={{ textAlign: 'center', marginBottom: '40px' }}>
  <img
    src={useBaseUrl("/img/mensaje_directo.jpg")}
    alt="Escribir_mensajes_particulares"
    style={{
      maxWidth: '50%',
      height: 'auto',
      display: 'block',
      margin: '0 auto'
    }}
  />
</div>

Solo podrás comunicarte con nodos que hayan sido detectados previamente por la red. Para que esto ocurra, deben compartir la misma región y el mismo radio preset (o una configuración compatible).

Si el nodo no responde, puede estar fuera de alcance o sin conectividad en ese momento.

Es importante entender que Meshtastic no funciona como una red en tiempo real constante. Los mensajes pueden tardar en propagarse dependiendo de la distancia, la cantidad de nodos intermedios, el entorno y la configuración.

### ¿Cómo saber si está funcionando?

Al enviar mensajes, podrás ver indicadores de envío y recepción similares a aplicaciones de mensajería, aunque no tienen la misma precisión ni fiabilidad.

También podés utilizar el mapa: si otros nodos comparten su ubicación, podrás ver su posición aproximada y confirmar su presencia en la red.

Tené en cuenta que:

- Ver un nodo no garantiza una comunicación estable.
- La ausencia de respuesta no siempre indica un problema.

*La mejor forma de validar el funcionamiento es contar con al menos dos nodos configurados correctamente y realizar pruebas entre ellos.*

---

Con estas configuraciones ya podés empezar a utilizar Meshtastic y sacarle provecho en situaciones reales.

No son las únicas opciones disponibles: se trata de una herramienta potente y en constante evolución. Sin embargo, para un primer contacto, esta base es más que suficiente para comenzar a operar dentro de la red.

A medida que ganes experiencia, vas a poder ajustar parámetros y explorar configuraciones más avanzadas según tus necesidades.

El siguiente paso es ponerlo en práctica: probar en campo, validar alcances y entender cómo se comporta la red en tu entorno. ¡Buena suerte!
