# pip-I-Larm
Alarma economica sonora, con esp32 y sensor de humedad.
Su diseño está basado en experiencias de personas con insensibilidad e incontinencia urinaria.
Puede servir para otros usos, o adaptarse para ello.

Un proyecto interesante!

Para lograr esto, necesitarás:

# Componentes
- ESP32
- Sensor de humedad y temperatura del aire (por ejemplo, DHT11 o DHT22)
- Buzzer

# Código
Puedes utilizar el framework de Arduino para programar el ESP32. Aquí te presento un ejemplo de código que puedes utilizar como base:

---

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


---


# Explicación
- El código utiliza la biblioteca DHT para leer los valores de humedad y temperatura del aire.
- El código utiliza la función map() para mapear la humedad a una frecuencia para el buzzer.
- El código utiliza la función tone() para sonar el buzzer con la frecuencia calculada.
- El código utiliza la función noTone() para detener el sonido del buzzer cuando la humedad está dentro del rango.

# Importante
- Asegúrate de instalar la biblioteca DHT en tu entorno de desarrollo.
- Ajusta los valores de rangoHumedadMin y rangoHumedadMax según tus necesidades.
- Puedes modificar el código para ajustar la frecuencia y el volumen del buzzer según tus preferencias.


---

Este es un codigo de uso personal, espero que le sirva a alguien más.

:D
