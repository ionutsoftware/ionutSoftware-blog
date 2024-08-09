---
title: "Raspberry Pi Pico: Primeros pasos"
date: 2024-08-09T19:15:31+03:00
uri: "https://ionutSoftware.net/post/raspberry-py-pico-primeros-pasos"
categories: ["anything else"]
tags: []
draft: false
---

¡Hola a todos!

El día de hoy, y aprovechando que este es mi primer blog post, voy a hablaros de un aparatejo que a mí me encanta: la Raspberry Pi Pico.

Este aparato nos permite interactuar con sensores y hacer un montón de cosas. No os digo más, hace unas semanas vi una noticia de un tipo que logró hacer un Macintosh antiguo con una de estas.

No me voy a parar a explicar las especificaciones ni qué más cosas se pueden hacer con ella. Este post/tutorial se enfocará en qué hacer con ella una vez adquirida, cómo configurarla y ese tipo de cosas.

**Este post configura la Raspberry Pi Pico para usar MicroPython.**

Así que... ¡vamos allá!

## Tengo la Raspberry en la mano, ¿y ahora?

Bueno, en primer lugar, una pequeña advertencia, útil si eres tan patoso como yo.

La parte de abajo del aparato tiene unos dientecitos. Estos dientecitos se llaman pines. Lo que son y para qué sirven lo veremos en otro post, pero muy resumidamente, son la forma que tiene este aparatito para comunicarse con los posibles sensores que le queramos conectar.

¿A qué viene la advertencia? ¡Son muy, pero muy delicados! Así que intenta no ser muy brusco, no dejarla caer bruscamente boca abajo en la mesa, ni apretarla fuertemente. En estos pines radica una de las partes más importantes de esta maravilla tecnológica. No queremos romperlos, ¿verdad?

Ahora sí, empecemos a configurar.

Algo que seguro sabes si investigaste antes de comprarla, es que necesitas un cable micro USB a USB, que muy convenientemente la Raspberry no trae. Tranquilo, no es excesivamente caro. Si no lo compraste, ve y hazlo ahora. Si lo tienes, continúa aquí.

Bien. La Raspberry tiene una forma rectangular. Tiene dos lados largos y dos cortos. Los dos cortos (más concretamente uno de ellos) es el que nos interesa ahora.

Si te fijas, uno de los lados tiene una apertura para la entrada de un cable y un bulto encima de esta. Esa es la parte superior de la Pico, y así nos referiremos a ella de ahora en adelante.

Bien, vamos a empezar con la configuración inicial del aparato.

El bulto del que hablamos (dicho así, campesinamente) es un botón. Este botón se llama BOOTSEL, y servirá para poder borrar la Pico y empezar desde cero o cambiar de lenguaje cada vez que queramos (bueno, no tanto, que luego se estropea).

Para poder activar este modo BOOTSEL (porque ahora no tenemos nada dentro), debemos hacer lo siguiente:

- Conectamos el cable USB al ordenador.
- Ahora, mantenemos presionado el botón BOOTSEL de la Raspberry Pico y conectamos la parte micro USB del cable a la entrada de esta (con el botón presionado).
- ¡Y listo! Ahora, soltamos el botón. La Pico debería ser reconocida por tu ordenador como una unidad USB. El nombre debería de ser RP y una serie de letras, aunque eso es lo de menos.

### Instalar MicroPython

Para quien no sepa qué es MicroPython, en su página web se define como:

"MicroPython is a lean and efficient implementation of the Python 3 programming language that includes a small subset of the Python standard library and is optimised to run on microcontrollers and in constrained environments."

¿Entendiste algo? Yo tampoco. Pasémoslo por un traductor:

"MicroPython es una implementación ágil y eficiente del lenguaje de programación Python 3 que incluye un pequeño subconjunto de la biblioteca estándar de Python y está optimizada para ejecutarse en microcontroladores y en entornos restringidos."

Ahora sí. Bueno, pues este MicroPython, del que ahora tenemos contexto, es lo que usaremos para nuestra Raspberry Pi Pico. ¿Por qué? Pues... porque es lo que yo conozco y porque es lo más potente y con la mayor comunidad que tenemos, a mi parecer.

Para poder usar MicroPython en la Pico, lo único que debemos hacer es descargar el firmware de MicroPython y pegarlo en la Pico, que tenemos como una unidad USB.

Vamos por pasos:

- Descarga el firmware desde [aquí](https://micropython.org/download/).
- Una vez descargado, deberías obtener un archivo llamado más o menos así:
  - `RPI_PICO_W-20240602-v1.23.0.uf2`

Este es un archivo de firmware. Cópiarlo.

- Abre la unidad USB en la que se convirtió tu Raspberry.
- Pega el archivo que copiaste.

¡Listo! Ahora, la Raspberry se reiniciará sola, pero no volverá a ser una unidad USB. ¡Ahora es una shell de MicroPython!

### Acceder a la shell de MicroPython

Si trabajaste con Python, sabrás ya que este lenguaje tiene una consola interactiva, la cual nos permite poner código que se ejecuta en tiempo real.

Bueno, pues aquí pasa lo mismo. Dado que este aparato es pequeño, no tiene Linux ni cualquier otro sistema operativo instalado. Solo tiene una consola interactiva de MicroPython (de Python) instalada.

¿Pero tiene un sistema de archivos?

¡Sí! Podrás usarlo con el módulo `os`, y pues... en vez de `ls`, usarás `os.listdir()` y ese tipo de cosas.

No entraré mucho en detalle aquí, porque si os gusta esto, en próximos posts entraré más en ello.

Bien. En otros sistemas operativos todo este proceso se haría desde la terminal con algunos programas, pero aquí estamos en Windows. ¿Qué necesitamos aquí? Un programa muy útil que sirve para más cosas, llamado PuTTY.

- Descarga PuTTY desde [aquí](https://www.putty.org/).
- Instálalo, se instala como cualquier otra aplicación.

Bien, ahora, mientras se instala (o antes de conectarnos), necesitamos un dato más: el puerto serial de la Pico.

Si alguna vez te conectaste a internet y te dio por curiosear cómo funciona la conexión a una web, por ejemplo, sabes que todo va mediante peticiones y puertos. Por ejemplo, como yo me di a la tarea de tener una web segura con HTTPS, ahora estás usando el puerto 443 de mi servidor para poder leer este post.

Pues con este aparato pasa igual. Tiene unos puertos de conexión, y uno en concreto (el único) es al que te vas a conectar. En Windows, esto es muy fácil de conseguir.

**¡Espero que no hayas desconectado la Raspberry de tu ordenador!**

- Con la Raspberry enchufada, presiona `Windows + X` y ve a "Administrador de dispositivos".
- Ahí, busca algo como "Puertos (COM y LPT)".
- Expande la lista, y tendría que salir algo como "Dispositivo serie USB (COM6)".

Una vez sabes que tu puerto es, en mi caso, el 6, abre PuTTY.

- Busca un botón de radio que diga SSH. Baja con la flecha hasta `Serial`.
- Busca el cuadro `Serial line`. Pon el puerto que sacaste (en este caso, `COM6`).
- En `Speed`, pon `115200`.
- Haz clic en "Conectar".

¡Y listo! Ya estás dentro de la consola interactiva de Python.

## Conclusión

En este tutorial hemos aprendido cómo configurar y conectarse a una Raspberry Pi Pico.

Si este contenido gusta, traeré más sobre cómo subir archivos a ella y tips básicos sobre circuitos y demás.

¡Un saludo, y hasta la próxima!
