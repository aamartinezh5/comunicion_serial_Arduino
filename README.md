# Control de 2 leds por comandos seriales con Arduino UNO 

Politécnico Grancolombiano · Internet de las Cosas · Entrega grupal 2
Noviembre 2026

## Descripción

Este proyecto controla dos leds (verde y rojo) con un Arduino UNO a partir de comandos de un solo carácter recibidos por el puerto serie a **9600 baudios**. En un montaje físico, los comandos llegarían desde un celular a través de un módulo Bluetooth HC-05. En la simulación (Wokwi), el monitor serial cumple el papel del enlace UART del módulo.

El programa interpreta los comandos, enciende o apaga los leds, informa por el monitor serial el estado de cada uno y avisa cuando recibe un comando inválido.

## Enlace de simulación

[Abrir la simulación en Wokwi] Link : https://wokwi.com/projects/481181803551169537


## Componentes

| Componente | Cantidad | Función |
|---|---|---|
| Arduino UNO R3 | 1 | Lee los comandos y controla los LEDs |
| LED verde | 1 | Indicador controlado por el comando V |
| LED rojo | 1 | Indicador controlado por el comando R |
| Resistencias de 220 Ω | 2 | Limitan la corriente de cada LED |
| Protoboard | 1 | Montaje del circuito |
| Módulo HC-05 | 1 | Solo en el montaje real. No está disponible en Wokwi |

## Conexiones

**Circuito simulado en Wokwi**

| Elemento | Conexión 
 LED verde | Pin 8 → resistencia → ánodo del LED; cátodo a GND |
 LED rojo  | Pin 9 → resistencia → ánodo del LED; cátodo a GND |
 Enlace serial | Monitor serial de Wokwi a 9600 baudios (sustituye al HC-05) |

**Montaje real con HC-05 (referencia)**

| Pin del HC-05 | Se conecta a |
|---|---|
| VCC | 5V del Arduino |
| GND | GND |
| TXD | Pin 0 (RX) del Arduino |
| RXD | Pin 1 (TX) del Arduino, a través de un divisor de voltaje |

## Comandos

| Comando | LED verde (pin 8) | LED rojo (pin 9) |
|---|---|---|
| V (o v) | Encendido | Apagado |
| R (o r) | Apagado | Encendido |
| A (o a) | Encendido | Encendido |
| 0 | Apagado | Apagado |
| Cualquier otro carácter | Sin cambios | Sin cambios (se informa como comando inválido) |

## Cómo probarlo

1. Abre el enlace de simulación de Wokwi.
2. Pulsa **Play**.
3. En el cuadro de texto del monitor serial escribe un comando y pulsa Enter.
4. Observa los LEDs y la respuesta del monitor serial.

## Pruebas realizadas

| # | Comando | Resultado esperado | Resultado | Evidencia |
|---|---|---|---|---|
| 1 | V | Verde encendido, rojo apagado | OK | [Ver captura](Evidencias/Caso2_Letra_V.PNG) |
| 2 | R | Verde apagado, rojo encendido | OK | [Ver captura](Evidencias/Caso3_Letra_R.PNG) |
| 3 | A | Ambos leds encendidos | OK | [Ver captura](Evidencias/Caso4_Letra_A.PNG) |
| 4 | 0 | Ambos leds apagados | OK | [Ver captura](Evidencias/Caso1_Inicio_Sistema.PNG) |
| 5 | X (comando inválido) | LEDs sin cambios y mensaje de error en el monitor serial | OK | [Ver captura](Evidencias/Caso5_simbolo_invalido.PNG) |

Cada captura muestra el circuito, el código y el monitor serial. Sus explicaciones detalladas están en el informe de la entrega.

## Estructura del repositorio

```
control-leds-uart-bluetooth/
├── README.md
├── sketch.ino          Código comentado para el Arduino
├── diagram.json        Circuito exportado de Wokwi
├── enlace_wokwi.txt    Enlace público de la simulación
└── evidencias/         Capturas de pantalla de las pruebas
```

## Limitaciones de la simulación de Bluetooth frente a UART

- **No hay Bluetooth real.** Wokwi no incluye el módulo HC-05, por lo que el monitor serial hace de enlace UART a 9600 baudios. No se simulan el emparejamiento, la señal de radio, el alcance ni los retardos de una conexión inalámbrica.
- **Los niveles de voltaje no se reflejan.** El HC-05 trabaja con lógica de 3,3 V, y en un montaje real el pin RXD del módulo requiere un divisor de voltaje desde el TX del Arduino. El simulador no representa esa diferencia.
- **Pines compartidos con el USB.** En el montaje físico, el módulo usaría los pines 0 y 1, los mismos de la conexión USB, por lo que conviene cargar el programa antes de conectarlo.
- **El monitor serial es instantáneo.** La comunicación por cable virtual no pierde datos ni se interrumpe, a diferencia de un enlace inalámbrico.

## Autores

- Francheska Valentina Miranda Cordero
- Diana Carolina Doria Mora
- Angel Arley Martinez Hernandez
