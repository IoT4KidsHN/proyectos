# Semáforo Inteligente

El proyecto Semáforo Inteligente de IoT4Kids tiene como objetivo enseñar a niños, niñas y jóvenes los fundamentos de la electrónica, la programación y el Internet de las Cosas (IoT) mediante la construcción y control de un sistema de semáforo automatizado.

Utilizando componentes electrónicos como LEDs de colores (rojo, amarillo y verde), resistencias, placas de desarrollo (como Arduino o Raspberry Pi) y sensores opcionales (como botones, sensores de movimiento o sensores de luz), los estudiantes aprenden a simular el funcionamiento de un semáforo real. Además, pueden programar diferentes modos de operación, como control por tiempo, detección de peatones o respuestas automáticas a condiciones del entorno.

Este proyecto promueve el pensamiento lógico, el diseño de sistemas, y la resolución de problemas reales, al tiempo que introduce conceptos clave en automatización, seguridad vial y ciudades inteligentes, de forma accesible, divertida y educativa.

## Objetivo

Simular el funcionamiento de un semáforo real controlado por código, con posibilidad de integrar sensores como botones o sensores de movimiento para detectar peatones o vehículos.

## Componentes necesarios (del Freenove Kit)

* Raspberry Pi 5 con Raspbian OS
* 3 LEDs: Rojo, Amarillo y Verde
* 3 resistencias (220Ω recomendadas)
* 1 Pulsador (opcional, para simular botón de cruce peatonal)
* Cables Dupont (M/M)
* Protoboard (Breadboard)

## Conexiones

| Componente       | GPIO (BCM) | Resistencia | Comentario                  |
|------------------|------------|-------------|-----------------------------|
| LED Rojo         | GPIO 17    | 220Ω        | Semáforo en alto            |
| LED Amarillo     | GPIO 27    | 220Ω        | Cambio de estado            |
| LED Verde        | GPIO 22    | 220Ω        | Paso libre                  |
| Botón (opcional) | GPIO 18    | Pull-down   | Simula botón de peatón      |

Todos los cátodos (piernas cortas) de los LEDs deben conectarse a GND a través de la resistencia.

## Lógica del Programa (Python)

```python
import RPi.GPIO as GPIO
import time

# Configuración de pines
GPIO.setmode(GPIO.BCM)
led_rojo = 17
led_amarillo = 27
led_verde = 22
boton = 18  # Pin opcional para cruce peatonal

GPIO.setup([led_rojo, led_amarillo, led_verde], GPIO.OUT)
GPIO.setup(boton, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)

# Secuencia normal del semáforo
def semaforo_normal():
    GPIO.output(led_rojo, GPIO.HIGH)
    time.sleep(3)
    GPIO.output(led_rojo, GPIO.LOW)

    GPIO.output(led_amarillo, GPIO.HIGH)
    time.sleep(1)
    GPIO.output(led_amarillo, GPIO.LOW)

    GPIO.output(led_verde, GPIO.HIGH)
    time.sleep(3)
    GPIO.output(led_verde, GPIO.LOW)

try:
    while True:
        if GPIO.input(boton) == GPIO.HIGH:
            print("Botón presionado: cruzando peatón")
            GPIO.output(led_verde, GPIO.LOW)
            GPIO.output(led_amarillo, GPIO.HIGH)
            time.sleep(1)
            GPIO.output(led_amarillo, GPIO.LOW)
            GPIO.output(led_rojo, GPIO.HIGH)
            time.sleep(4)
            GPIO.output(led_rojo, GPIO.LOW)
        else:
            semaforo_normal()

except KeyboardInterrupt:
    print("Programa detenido.")
    GPIO.cleanup()
```

## Expansiones posibles

* Sensor de movimiento para detectar vehículos.
* Módulo Wi-Fi o Bluetooth para control remoto.
* Pantalla LCD para mostrar tiempo restante.
* Control vía app o dashboard.

# 🚦 Semáforo Inteligente con Freenove Starter Kit y Raspberry Pi 5

Este proyecto utiliza el **Freenove Ultimate Starter Kit para Raspberry Pi 5** para simular un semáforo con LEDs controlados por Python y GPIO.

---

## ✅ Lista de Materiales

| Componente                        | Cantidad |
|----------------------------------|----------|
| LED Rojo, Amarillo y Verde       | 1 de cada color |
| Resistencias de 220Ω             | 3        |
| Raspberry Pi 5                   | 1        |
| Cables de conexión (Jumper wires)| 6-8      |
| Breadboard                       | 1        |

---

## 🔌 Diseño del Breadboard

Cada LED está conectado a un pin GPIO a través de una resistencia de 220Ω.

**GPIO sugeridos:**

* LED Rojo → GPIO 17
* LED Amarillo → GPIO 27
* LED Verde → GPIO 22

**Conexión:**
GPIO17 o Pin 11 ---[220Ω]---|>|--- GND → LED Rojo
GPIO27 o Pin 13 ---[220Ω]---|>|--- GND → LED Amarillo
GPIO22 o Pin 15 ---[220Ω]---|>|--- GND → LED Verde

## Diagrama

![diagrama](imagenes/diagrama.png)
