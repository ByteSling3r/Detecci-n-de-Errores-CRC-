Requiere Usar PYTHON3

Modo de ejecución: Ejecutar Receiver.py python3 receiver.py

Luego Ejecutar el sender.py python3 sender\_gui.py

Librerias usadas:

* socket

* tkinter

* threading

* time

![](img/img.png)

**Documentación del Programa Sender - CRC**

**Descripción Detallada**

Este programa en Python se utiliza para realizar la codificación de datos mediante el algoritmo de Verificación de Redundancia Cíclica (CRC) y enviarlos a través de una conexión de socket. El CRC es un método eficiente para detectar errores en la transmisión de datos y es ampliamente utilizado en comunicaciones.

**Estructura del Código**

**Importación de Módulos**

En esta sección se importan los módulos necesarios para el funcionamiento del programa:

- socket: Permite la comunicación por sockets para enviar datos a través de una red.
- tkinter as tk: Importa la biblioteca Tkinter para crear una interfaz gráfica de usuario 

  (GUI).

- time: Se utiliza para introducir un pequeño retraso en la transmisión de la clave del generador.

**Funciones**

**xor\_operation(a, b)**

Esta función realiza una operación XOR entre dos cadenas binarias a y b. Itera sobre las cadenas y compara cada bit, devolviendo una cadena resultante con los bits XOR de las entradas.

**mod2div(dividend, divisor)**

La función mod2div lleva a cabo una división módulo-2 entre dos cadenas binarias dividend (dividendo) y divisor (divisor). Utiliza una técnica de división por XOR iterativa para calcular el residuo.

**encodeData(data, key)**

Esta función se encarga de codificar los datos de entrada utilizando el algoritmo CRC. Toma dos argumentos: data (los datos a codificar) y key (la clave del generador). La función agrega ceros al final de los datos para igualar la longitud de la clave del generador, luego calcula el CRC y lo agrega a los datos originales antes de devolver el resultado.

**calculate\_crc()**

La función calculate\_crc() se activa cuando se hace clic en el botón "Calculate CRC and TX" en la interfaz de usuario. Recopila los datos de entrada y la clave del generador de los campos de entrada de la GUI y llama a la función encodeData() para calcular el CRC. Luego, muestra el CRC calculado en la GUI.

**send\_data()**

La función send\_data() se ejecuta al hacer clic en el botón "Send Data". Crea un socket, se conecta

a la dirección IP 127.0.0.1 en el puerto 17091, recopila los datos de entrada y la clave del 

generador, calcula el CRC llamando a encodeData(), y finalmente, envía los datos codificados a través del socket. Se agrega un pequeño retraso antes de enviar la clave del generador para evitar que los datos de transmisión y la clave lleguen al receptor al mismo tiempo.

**Interfaz Gráfica de Usuario (GUI)**

El programa utiliza Tkinter para crear una interfaz gráfica simple con etiquetas de entrada de datos, campos de entrada de datos y clave del generador, botones para calcular el CRC y enviar los datos, y etiquetas para mostrar los resultados.

**Uso del Programa**

1. Ejecuta el programa, lo que abrirá una ventana de GUI.
1. Ingresa los datos que deseas enviar en el campo "Enter data you want to send".
1. Ingresa la clave del generador en el campo "Enter a Generator".
1. Haz clic en el botón "Calculate CRC and TX" para calcular el CRC y mostrarlo en la GUI.
1. Haz clic en el botón "Send Data" para enviar los datos codificados a través de una conexión de socket a la dirección IP 127.0.0.1 en el puerto 17091.

**Notas Adicionales**

- El programa utiliza una dirección de bucle local (127.0.0.1) y el puerto 17091 para la comunicación a través del socket.
- Se agrega un pequeño retraso (time.sleep(0.2)) antes de enviar la clave del generador para asegurarse de que la transmisión del CRC no llegue al receptor al mismo tiempo que la clave.
- Los resultados del cálculo del CRC se muestran en la GUI.

**Documentación del Programa Receiver - CRC**

**Descripción Detallada**

Este programa en Python actúa como receptor (receiver) y se utiliza para recibir datos codificados mediante el algoritmo de Verificación de Redundancia Cíclica (CRC) a través de una conexión de socket. Luego, verifica si los datos contienen errores utilizando el CRC y envía una respuesta al remitente.

**Estructura del Código**

**Importación de Módulos**

En esta sección, se importan los módulos necesarios para el funcionamiento del programa:

- socket: Permite la comunicación por sockets para recibir datos de una red.
- tkinter as tk: Importa la biblioteca Tkinter para crear una interfaz gráfica de usuario 

  (GUI).

- threading: Se utiliza para crear un hilo separado para recibir datos y mantener la interfaz de usuario (UI) interactiva.

**Funciones**

**xor\_operation(a, b)**

Esta función realiza una operación XOR entre dos cadenas binarias a y b. Itera sobre las cadenas y compara cada bit, devolviendo una cadena resultante con los bits XOR de las entradas.

**mod2div(divident, divisor)**

La función mod2div lleva a cabo una división módulo-2 entre dos cadenas binarias divident (dividendo) y divisor (divisor). Utiliza una técnica de división por XOR iterativa para calcular el residuo.

**decodeData(data, key)**

Esta función se encarga de decodificar los datos recibidos utilizando el algoritmo CRC. Toma dos argumentos: data (los datos recibidos) y key (la clave del generador utilizada para la codificación). La función agrega ceros al final de los datos para igualar la longitud de la clave del generador, luego calcula el CRC y lo compara con un patrón de ceros para verificar si hay errores en la transmisión.

**receive\_data()**

La función receive\_data() se ejecuta en un hilo separado cuando se hace clic en el botón "Start Receiver" en la interfaz de usuario. Configura un socket, lo vincula a un puerto específico (en este caso, 17091), y escucha las conexiones entrantes. Cuando se establece una conexión con un remitente,

recibe los datos y la clave del generador, calcula el CRC y verifica si hay errores. Luego, envía una respuesta al remitente indicando si se encontraron errores o no.

**start\_receiving()**

La función start\_receiving() se llama cuando se hace clic en el botón "Start Receiver" en la interfaz de usuario. Inicia un hilo utilizando threading.Thread() que ejecuta la función receive\_data().

**close\_connection()**

La función close\_connection() se llama cuando se hace clic en el botón "Close" en la interfaz de usuario. Cierra la conexión de red y destruye la ventana de la GUI.

**Interfaz Gráfica de Usuario (GUI)**

El programa utiliza Tkinter para crear una interfaz gráfica simple con botones para iniciar el receptor, etiquetas para mostrar los resultados del CRC y los datos recibidos, y un botón para cerrar la conexión.

**Uso del Programa**

1. Ejecuta el programa, lo que abrirá una ventana de GUI.
1. Haz clic en el botón "Start Receiver" para iniciar el receptor.
1. El receptor esperará conexiones entrantes en el puerto 17091.
1. Cuando se establezca una conexión con un remitente, mostrará los datos recibidos y el resultado del CRC en la GUI.
1. Si no se encuentran errores en los datos, se enviará un mensaje de agradecimiento al remitente junto con los datos.
1. Si se encuentran errores en los datos, se enviará un mensaje de error al remitente.
1. Haz clic en el botón "Close" para cerrar la conexión.

**Notas Adicionales**

- El programa utiliza una dirección de bucle local (127.0.0.1) y el puerto 17091 para la comunicación a través del socket.
- Los resultados del cálculo del CRC y los datos recibidos se muestran en la GUI.
