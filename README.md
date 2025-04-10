# Pip-I-Larm
Alarma sonora economica, con esp32 y sensor de humedad.

Su diseño está basado en las experiencias de personas con insensibilidad e incontinencia urinaria.

Puede servir para otros usos, o adaptarse para ello.


## Componentes
- ESP32
- Sensor de humedad y temperatura del aire (por ejemplo, DHT11 o DHT22)
- Buzzer

---
---
---

## Código DHT11
Puedes utilizar el framework de Arduino para programar el ESP32. Aquí te presento un ejemplo de código que puedes utilizar como base para un **DHT11**:

---
````
const int pinBuzzer = 5; // Pin del buzzer
const int pinDHT = 4; // Pin del sensor DHT
const int rangoHumedadMin = 60; // Rango mínimo de humedad
const int rangoHumedadMax = 100; // Rango máximo de humedad

DHT dht(pinDHT, DHT11); // Inicializa el sensor DHT

void setup() {
  pinMode(pinBuzzer, OUTPUT); // Configura el pin del buzzer como salida
  dht.begin(); // Inicializa el sensor DHT
}

void loop() {
  float humedad = dht.readHumidity(); // Lee la humedad del aire
  float temperatura = dht.readTemperature(); // Lee la temperatura del aire

  if (humedad > rangoHumedadMin && humedad < rangoHumedadMax) {
    // Si la humedad está dentro del rango, no suena el buzzer
    noTone(pinBuzzer);
  } else if (humedad > rangoHumedadMax) {
    // Si la humedad es mayor que el rango máximo, suena el buzzer con frecuencia creciente
    int frecuencia = map(humedad, rangoHumedadMax, 100, 100, 1000); // Mapea la humedad a una frecuencia
    tone(pinBuzzer, frecuencia); // Suena el buzzer con la frecuencia calculada
  } else if (humedad < rangoHumedadMin) {
    // Si la humedad es menor que el rango mínimo, suena el buzzer con frecuencia decreciente
    int frecuencia = map(humedad, 0, rangoHumedadMin, 1000, 100); // Mapea la humedad a una frecuencia
    tone(pinBuzzer, frecuencia); // Suena el buzzer con la frecuencia calculada
  }

  delay(1000); // Espera 1 segundo antes de leer nuevamente los valores
}
````
---



#### Explicación
- El código utiliza la biblioteca DHT para leer los valores de humedad y temperatura del aire.
- El código utiliza la función map() para mapear la humedad a una frecuencia para el buzzer.
- El código utiliza la función tone() para sonar el buzzer con la frecuencia calculada.
- El código utiliza la función noTone() para detener el sonido del buzzer cuando la humedad está dentro del rango.

### Importante
- Asegúrate de instalar la biblioteca DHT en tu entorno de desarrollo.
- Ajusta los valores de rangoHumedadMin y rangoHumedadMax según tus necesidades.
- Puedes modificar el código para ajustar la frecuencia y el volumen del buzzer según tus preferencias.


---
---
---

## Código base para un **DHT21**:

---
````
Claro! Aquí te presento el código modificado para un DHT21:


const int pinBuzzer = 5; // Pin del buzzer
const int pinDHT = 4; // Pin del sensor DHT
const int rangoHumedadMin = 60; // Rango mínimo de humedad
const int rangoHumedadMax = 80; // Rango máximo de humedad

DHT dht(pinDHT, DHT21); // Inicializa el sensor DHT21

void setup() {
  pinMode(pinBuzzer, OUTPUT); // Configura el pin del buzzer como salida
  dht.begin(); // Inicializa el sensor DHT
}

void loop() {
  float humedad = dht.readHumidity(); // Lee la humedad del aire
  float temperatura = dht.readTemperature(); // Lee la temperatura del aire

  if (humedad > rangoHumedadMin && humedad < rangoHumedadMax) {
    // Si la humedad está dentro del rango, no suena el buzzer
    noTone(pinBuzzer);
  } else if (humedad > rangoHumedadMax) {
    // Si la humedad es mayor que el rango máximo, suena el buzzer con frecuencia creciente
    int frecuencia = map(humedad, rangoHumedadMax, 100, 100, 1000); // Mapea la humedad a una frecuencia
    tone(pinBuzzer, frecuencia); // Suena el buzzer con la frecuencia calculada
  } else if (humedad < rangoHumedadMin) {
    // Si la humedad es menor que el rango mínimo, suena el buzzer con frecuencia decreciente
    int frecuencia = map(humedad, 0, rangoHumedadMin, 1000, 100); // Mapea la humedad a una frecuencia
    tone(pinBuzzer, frecuencia); // Suena el buzzer con la frecuencia calculada
  }

  delay(1000); // Espera 1 segundo antes de leer nuevamente los valores
}
````

# Cambios
- La única diferencia con el código anterior es que se ha cambiado el tipo de sensor DHT a DHT21 en la línea DHT dht(pinDHT, DHT21);.

# Importante
- Asegúrate de instalar la biblioteca DHT en tu entorno de desarrollo.
- Ajusta los valores de rangoHumedadMin y rangoHumedadMax según tus necesidades.
- Puedes modificar el código para ajustar la frecuencia y el volumen del buzzer según tus preferencias.

---

# CONEXIONES:

El DHT21 es un sensor de humedad y temperatura que utiliza un protocolo de comunicación de un solo cable (1-Wire) para transmitir los datos. A continuación, te explico cómo conectar los cables del DHT21 al ESP32 según el código anterior:

## Conexiones
- Rojo (VCC): Conecta el cable rojo del DHT21 al pin 3V3 del ESP32. Este pin proporciona la alimentación de 3,3V necesaria para el sensor.
- Negro (GND): Conecta el cable negro del DHT21 al pin GND del ESP32. Este pin es la tierra común para el sensor y el ESP32.
- Amarillo (DATA): Conecta el cable amarillo del DHT21 al pin D4 (o cualquier otro pin digital disponible) del ESP32. En el código anterior, se utiliza el pin D4 para leer los datos del sensor.

### Código
En el código anterior, se define el pin del sensor DHT como const int pinDHT = 4;. Esto significa que el cable amarillo del DHT21 debe estar conectado al pin D4 del ESP32.

### Importante
- Asegúrate de que los cables estén conectados correctamente y que no haya cortocircuitos.
- Verifica que el ESP32 esté configurado para utilizar el pin correcto para leer los datos del sensor.

----

Este es un codigo para mi uso personal, espero que le sirva a alguien más :D

