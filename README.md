# INTERFAZ II
1. [Hola Mundo](#ejercicio-n1-arduino-hola-mundo) <br>
2. [Leds parpadeantes](#ejercicio-n2-leds-parpadeantes) <br>
3. [Control por pulsador](#ejercicio-n3-control-por-pulsador) <br>
4. [Leds con potenciómetro](#ejercicio-n4-leds-con-potenci%C3%B3metro) <br>
5. [Semáforo](#ejercicio-n5-sem%C3%A1foro) <br>
  5.1 [Semáforo con luz verde peatonal parpadeante](#ejercicio-n51-sem%C3%A1foro-con-luz-verde-peatonal-parpadeante) <br>
6. [Potenciómetro+Processing](#ejercicio-n6--elipse-interactivo-potenci%C3%B3metro--processing) <br>
7. [Pulsador + Processing](#ejercicio-n7-pulsador--processing)
8. [Pulsador + Potenciómetro + Processing](#ejercicio-n8-pulsador--potenci%C3%B3metro--processing) <br>
9. [If, else if, else con potenciómetro](#ejercicio-n9-if-else-if-else-con-potenci%C3%B3metro) <br>
  9.1 [For, if, else con LED](#ejercicio-n91-for-if-else-con-led) <br>
10. [Botonera LED](#ejercicio-n10-botonera-led) <br>
11. [Sensor distancia visual](#ejercicio-n11-sensor-distancia-visual) <br>
12. [Cámara y signos](#ejercicio-n12-c%C3%A1mara-y-signos) <br>
13. [Sensor de humedad (DFRobot)](#ejercicio-n13-sensor-de-humedad-dfrobot)<br>
14. ["Cuerpo, vídeo, sensor sharp](#ejercicio-n14-cuerpo-v%C3%ADdeo-sensor-sharp)<br>
15. [Promedio de Imágenes llamando una carpeta + potenciometro](#ejercicio-n15-promedio-de-im%C3%A1genes-llamando-una-carpeta--potenciometro)<br>
16. [Evaluación 2: "Rastros sin Contacto"](#evaluaci%C3%B3n-2-rastros-sin-contacto)<br>


### Ejercicio n°1 Arduino: "Hola Mundo"

```js
void setup() {
  Serial.begin(9600); // Inicia la comunicación serie a 9600 bps
  Serial.println("Hola, Mundo!"); // Envía "Hola, Mundo!" al monitor serie
}

void loop() {
  // No es necesario poner nada en el loop para este ejemplo
}
```
### Ejercicio n°2 "Leds parpadeantes"
```js
void setup() {  // Configuración inicial (ej: pines como entrada/salida)
  pinMode(13, OUTPUT);  // Pin 13 como salida
  pinMode (8, OUTPUT); // Pin 8 como salida
}

void loop() {   // Se repite infinitamente
  digitalWrite(13, HIGH);  // Encender LED rojo
  delay(1000);             // Esperar 1 segundo
  digitalWrite(13, LOW);   // Apagar LED rojo
  //delay(1000);             // Esperar 1 segundo
  digitalWrite(8, HIGH);  // Encender LED verde
  delay(1000);             // Esperar 1 segundo
  digitalWrite(8, LOW);   // Apagar LED verde
  //delay(1000);             // Esperar 1 segundo
}

```
<img 
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Led%20parpadeante.png"
 />
 #### Registros físicos
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250819_120523.jpg"
/>
https://drive.google.com/file/d/16hHIkAbMyoYRTPSeGQQg5N0coOsQ1my-/view?usp=sharing
### Ejercicio n°3 "Control por pulsador"
```js
void setup() {
  pinMode(2, INPUT);  // Botón como entrada
  pinMode(13, OUTPUT);
}
void loop() {
  if (digitalRead(2) == HIGH) {  // Si se presiona el botón
    digitalWrite(13, HIGH);
  } else {
    digitalWrite(13, LOW);
  }
}
```
<img 
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Pulsador.png"
 />

### Ejercicio n°4 "Leds con potenciómetro"
```js
void setup() {
  pinMode(9, OUTPUT);  // Pin PWM (símbolo ~)
}
void loop() {
  int valor = analogRead(A0);           // Leer potenciómetro (0-1023)
  int brillo = map(valor, 0, 1023, 0, 255);  // Convertir a rango PWM
  analogWrite(9, brillo);               // Ajustar brillo
}
```
<img 
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Potenciometro.png"
 />
 #### Registro físico
 <img
 src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250819_133310.jpg"
 />
 
### Ejercicio n°5 "Semáforo"
```js
// C++ code - Semáforo Autos y Peatones

// Definición de pines
int LED_1 = 6;  // Luz roja autos
int LED_2 = 7;  // Luz amarilla autos
int LED_3 = 8;  // Luz verde autos
int LED_4 = 9;  // Luz verde peatones
int LED_5 = 10; // Luz roja peatones

void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
}

void loop() {
  // 🚦 Fase 1: Autos en verde, peatones en rojo
  digitalWrite(LED_1, LOW);   // Rojo autos apagado
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado
  digitalWrite(LED_3, HIGH);  // Verde autos encendido
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 2: Amarillo autos, peatones siguen en rojo
  digitalWrite(LED_3, LOW);   // Verde autos apagado
  digitalWrite(LED_2, HIGH);  // Amarillo autos encendido
  delay(2000); // 2 segundos
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado

  // 🚦 Fase 3: Rojo autos, verde peatones
  digitalWrite(LED_1, HIGH);  // Rojo autos encendido
  digitalWrite(LED_5, LOW);   // Rojo peatones apagado
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 4: Rojo autos, rojo peatones (tiempo intermedio)
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(2000); // 2 segundos
}
```
<img 
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Sem%C3%A1foro.png"
 />

### Ejercicio n°5.1 "Semáforo con luz verde peatonal parpadeante"

```js
// C++ code - Semáforo Autos y Peatones

// Definición de pines
int LED_1 = 6;  // Luz roja autos
int LED_2 = 7;  // Luz amarilla autos
int LED_3 = 8;  // Luz verde autos
int LED_4 = 9;  // Luz verde peatones
int LED_5 = 10; // Luz roja peatones

void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
}

void loop() {
  // 🚦 Fase 1: Autos en verde, peatones en rojo
  digitalWrite(LED_1, LOW);   // Rojo autos apagado
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado
  digitalWrite(LED_3, HIGH);  // Verde autos encendido
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 2: Amarillo autos, peatones siguen en rojo
  digitalWrite(LED_3, LOW);   // Verde autos apagado
  digitalWrite(LED_2, HIGH);  // Amarillo autos encendido
  delay(2000); // 2 segundos
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado

  // 🚦 Fase 3: Rojo autos, verde peatones
  digitalWrite(LED_1, HIGH);  // Rojo autos encendido
  digitalWrite(LED_5, LOW);   // Rojo peatones apagado
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(3000); // 3 segundos
 
  for(int i =0; i<5; i++) {
    digitalWrite(LED_4, LOW);
    delay(300);
    digitalWrite(LED_4, HIGH);
    delay(300);
  }
 
 
  // 🚦 Fase 4: Rojo autos, rojo peatones (tiempo intermedio)
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  //delay(2000); // 2 segundos
}
```
 #### Registros físicos
 <img
 src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250826_125443.jpg"
 />
https://drive.google.com/file/d/1mlSG6fUnIexw690-91uKM2A44RmK5soX/view?usp=sharing

### TRABAJO CON NOTA código modificado del ejercicio del semáforo
```js
// Definición de pines
int LED_1 = 6;  // Luz roja
int LED_2 = 7;  // Luz roja			
int LED_3 = 8;  // Luz roja
int LED_4 = 5;  // Luz amarilla
int LED_5 = 4; // Luz amarilla
int LED_6 = 3; // Luz amarilla
int LED_7 = 13; // Luz verde
int LED_8 = 12; // Luz verde
int LED_9 = 11; // Luz verde


void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
  pinMode(LED_6, OUTPUT);
  pinMode(LED_7, OUTPUT);
  pinMode(LED_8, OUTPUT);
  pinMode(LED_9, OUTPUT);
}

void loop() {
//FASE 1
 digitalWrite(LED_1, HIGH);   
  delay(200);
  digitalWrite(LED_2, HIGH); 
  delay(200);
  digitalWrite(LED_3, HIGH);  
  delay(200);
  digitalWrite(LED_4, HIGH);
  delay(200);
  digitalWrite(LED_5, HIGH); 
  delay(200);
  digitalWrite(LED_6, HIGH);
  delay(200);
  digitalWrite(LED_7, HIGH);
  delay(200);
  digitalWrite(LED_8, HIGH);
  delay(200);
  digitalWrite(LED_9, HIGH);
  delay(100);
  // FASE 2
  digitalWrite(LED_9, LOW);   
  delay(200);
  digitalWrite(LED_8, LOW); 
  delay(200);
  digitalWrite(LED_7, LOW);  
  delay(200);
  digitalWrite(LED_6, LOW);
  delay(200);
  digitalWrite(LED_5, LOW); 
  delay(200);
  digitalWrite(LED_4, LOW);
  delay(200);
  digitalWrite(LED_3, LOW);
  delay(200);
  digitalWrite(LED_2, LOW);
  delay(200);
  digitalWrite(LED_1, LOW);
  delay(500);
  }
```
<img
src= "https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-07%20113653.png"
/>
<img
src= "https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20251007_122731.jpg"
/>
https://drive.google.com/file/d/1E66RT5fyDiQHEzSPEaJsZVLlKjOaHmVS/view?usp=sharing

### Ejercicio n°6 " Elipse Interactivo: Potenciómetro + Processing"

```js
Serial myPort;  // Crear objeto de la clase Serial
static String val;    // Datos recibidos desde el puerto serial
int sensorVal = 0;

void setup()
{
  background(0); 
  //fullScreen(P3D);
   size(1080, 720);
   noStroke();
  noFill();
  String portName = "COM3";// Cambia el número (en este caso) para que coincida con el puerto correspondiente conectado a tu Arduino. 

  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort = new Serial(this, Serial.list()[0], 9600);

}

void draw()
{
  if ( myPort.available() > 0) {  // Si hay datos disponibles,
  val = myPort.readStringUntil('\n'); 
  try {
   sensorVal = Integer.valueOf(val.trim());
  }
  catch(Exception e) {
  ;
  }
  println(sensorVal); // léelos y guárdalos en vals!
  }  
 //background(0);
  // Escala el valor de mouseX de 0 a 640 a un rango entre 0 y 175
  float c = map(sensorVal, 0, width, 0, 400);
  // Escala el valor de mouseX de 0 a 640 a un rango entre 40 y 300
  float d = map(sensorVal, 0, width, 40,500);
  fill(255, c, 0);
  ellipse(width/2, height/2, d, d);
}
```
#### Registro físico
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250826_132143.jpg"
/> 
https://drive.google.com/file/d/1SS2iqvV8yQ0-BHBpgFph9AiLawvGEEtV/view?usp=sharing

### Ejercicio n°7 "Pulsador + Processing"

```js
int buttonPin = 2;  // Pin del botón
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    Serial.println(1);        // Enviar un "1" a Processing
    delay(200);               // Evitar rebotes
  }
}
```
### Ejercicio n°8 "Pulsador + Potenciómetro + Processing"
```js

int buttonPin = 2;       // Pin del botón
int potPin = A0;         // Pin del potenciómetro
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    int potValue = analogRead(potPin);   // 0 - 1023
    Serial.print("BTN,");     // etiqueta para Processing
    Serial.println(potValue); // mando el valor junto con el evento
    delay(200);               // debounce simple
  }
}
```
#### Registro físico
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250902_130559.jpg"
/>

### Ejercicio n°9 "If, else if, else con potenciómetro" 

```js
int valor;  // aquí guardaremos la lectura del sensor

void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial
}

void loop() {
  valor = analogRead(A0);   // lee el pin analógico A0

  if (valor < 400) {
    Serial.println("Muy bajo");
  } else if (valor < 700 ) {
    Serial.println("Medio");
  } else {
    Serial.println("Alto");
  }

  delay(500); // medio segundo entre lecturas
}
```

### Ejercicio n°9.1 "For, if, else con LED"
```js
int leds[] = {2, 3, 4, 5}; // Creamos un arreglo con los pines donde van conectados los LEDs

void setup() {
  // Esta función corre solo una vez al iniciar Arduino
  for (int i = 0; i < 4; i++) {         // Recorre el arreglo desde i = 0 hasta i = 3
    pinMode(leds[i], OUTPUT);           // Configura cada pin del arreglo como salida (para controlar LEDs)
  }
}

void loop() {
  // Esta función corre en bucle infinito
  for (int i = 0; i < 4; i++) {         // Recorre los 4 LEDs, uno por uno
    if (i % 2 == 0) {                   // Si el índice es par (0, 2)... Se puede poner =1 y serian los impares
      digitalWrite(leds[i], HIGH);      // Enciende el LED correspondiente
    } else {                            // Si el índice es impar (1, 3)...
      digitalWrite(leds[i], LOW);       // Apaga el LED correspondiente
    }
    //delay(500);                         // Espera 0,5 segundos antes de pasar al siguiente
  }
}
```
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/forifelse.png"
/>

### Ejercicio n°10 "Botonera LED"
```js
// --- Configuración de botones ---
const int numButtons = 3;
const int buttonPins[numButtons] = {2, 4, 7};
const int ledButtonPins[numButtons] = {9, 10, 11}; // LEDs botones

// --- Configuración de potenciómetros ---
const int numPots = 2;
const int potPins[numPots] = {A0, A1};
const int ledPotPins[numPots] = {3, 5}; // LEDs PWM

// Variables de estados previos
int lastButtonState[numButtons];
int lastPotValue[numPots];

void setup() {
  Serial.begin(9600);

  // Configurar botones y LEDs
  for (int i = 0; i < numButtons; i++) {
    pinMode(buttonPins[i], INPUT_PULLUP);
    pinMode(ledButtonPins[i], OUTPUT);
    lastButtonState[i] = digitalRead(buttonPins[i]);
  }

  // Configurar LEDs de potenciómetros
  for (int i = 0; i < numPots; i++) {
    pinMode(ledPotPins[i], OUTPUT);
    lastPotValue[i] = analogRead(potPins[i]);
  }
}

void loop() {
  // Leer y enviar botones
  for (int i = 0; i < numButtons; i++) {
    int buttonState = digitalRead(buttonPins[i]);

    // LED se enciende cuando botón está presionado
    digitalWrite(ledButtonPins[i], buttonState == LOW ? HIGH : LOW);

    if (buttonState != lastButtonState[i]) {  // enviar cambios
      Serial.print("B");
      Serial.print(i); 
      Serial.print(":");
      Serial.println(buttonState);
      lastButtonState[i] = buttonState;
    }
  }

  // Leer y enviar potenciómetros
  for (int i = 0; i < numPots; i++) {
    int potValue = analogRead(potPins[i]); // 0–1023
    int pwmValue = potValue / 4;           // 0–255

    // Ajustar LED según valor
    analogWrite(ledPotPins[i], pwmValue);

    if (abs(pwmValue - lastPotValue[i]) > 2) { // evitar ruido
      Serial.print("P");
      Serial.print(i);
      Serial.print(":");
      Serial.println(pwmValue);
      lastPotValue[i] = pwmValue;
    }
  }

  delay(10);
}
```
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/botoneraLED.png"
/>
## Registros físicos
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/20250923_125657.jpg"
/>
https://drive.google.com/drive/folders/1BS_4HVPIA8Epd3rhjGsshbNoOhZ9KH9F

### Ejercicio n°11 "Sensor distancia visual"
```js
// Definir el pin del sensor Sharp
int sharpPin = A0;

void setup() {
  Serial.begin(9600); // Iniciar comunicación serial
}

void loop() {
  int sensorValue = analogRead(sharpPin); // Leer valor del sensor
  Serial.println(sensorValue); // Enviar valor a Processing
  delay(100); // Esperar un momento
}
```
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-14%20115129.png"
/>
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-14%20115143.png"
/>
## Registros físicos
<img
src="https://github.com/kminugami/INTERFAZ/blob/main/img/20251014_114258.jpg"
/>
https://drive.google.com/file/d/1Nt6zh9Op5ze5TjNsoD9sP6wmIRcp49fC/view?usp=drive_link

### Ejercicio n°12 "Cámara y signos"
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-14%20120252.png"
/>


### Ejercicio n°13 "Sensor de humedad (DFRobot)"
```js
void setup()
{
  Serial.begin(9600);// abre el puerto serial y Establece la velocidad en baudios a 9600 bps
}
void loop()
{
  int sensorValue;
  sensorValue = analogRead(0);   //conectar el sensor de humedad al pin analogo 0
  Serial.println(sensorValue); //imprime el valor a serial.
  delay(200);
}
```
<img
src="https://github.com/kminugami/INTERFAZ/blob/main/img/Captura%20de%20pantalla%202025-10-14%20125809.png"
/>
### Ejercicio n°14 "Cuerpo, vídeo, sensor sharp"
```js
// --- Sensor Sharp conectado al pin A0 ---
int sensorPin = A0;
int valor;

void setup() {
  Serial.begin(9600);
}

void loop() {
  valor = analogRead(sensorPin);
  Serial.println(valor);
  delay(50); // envío cada 50 ms
}
```
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-21%20125429.png"
/>
<img
src="https://raw.githubusercontent.com/kminugami/INTERFAZ/refs/heads/main/img/Captura%20de%20pantalla%202025-10-21%20130105.png"
/>

### Ejercicio n°15 "Promedio de Imágenes llamando una carpeta + potenciometro"
```js
void setup() {
  Serial.begin(9600);
}

void loop() {
  int potValue = analogRead(A0);
  Serial.println(potValue);
  delay(20);
}
```
#### No se pudo hacer por el error "ArrayIndexOutOfBoundsException: Index 345600 out of bounds for length 345600"

### Evaluación 2: "Rastros sin Contacto"
#### Integrantes: Sofía Becerra, Camila Gallegos, Daniela Reyes.
#### Código Arduino 
```js
void setup() {
Serial.begin(9600);
}
void loop() {
int valor = analogRead(A0); // Lee el potenciómetro
Serial.println(valor); // Envía el valor (0–1023)

delay(50); // Evita saturar el puerto serie
}
```

#### Código Processing
```js
import processing.video.*;
import processing.serial.*;
Capture cam;
Serial myPort;
// --- Variables de movimiento ---
PImage prevFrame;
float threshold = 40; // sensibilidad
PVector motionPos;
// --- Estela (seguimiento) ---
int num = 60;
float mx[] = new float[num];
float my[] = new float[num];
// --- Color controlado por potenciómetro ---
float potValue = 0;
color trailColor = color(255, 255, 255);
// --- Círculo interactivo ---
PVector targetCircle;
float circleSize = 60;
boolean circleVisible = true;
boolean exploding = false;
float explosionSize = 0;
float explosionAlpha = 255;
// --- Límites seguros ---
float margin = 100;

void setup() {
size(640, 480);
// Iniciar cámara
String[] cameras = Capture.list();
if (cameras.length == 0) {
println("No se detectó ninguna cámara.");
exit();
}
cam = new Capture(this, cameras[0]);
cam.start();
prevFrame = createImage(width, height, RGB);
motionPos = new PVector(width/2, height/2);
noStroke();
// Crear círculo aleatorio
targetCircle = new PVector(random(margin, width - margin), random(margin, height
- margin));
// --- Inicializar puerto serie ---
println(Serial.list()); // muestra los puertos disponibles
String portName = "COM8"; // ✅ Puerto correcto
myPort = new Serial(this, portName, 9600);
myPort.bufferUntil('\n');
}
void captureEvent(Capture cam) {
cam.read();
}
void serialEvent(Serial myPort) {
String inString = trim(myPort.readStringUntil('\n'));
if (inString != null && inString.length() > 0) {
try {
potValue = float(inString);
potValue = constrain(potValue, 0, 1023);
// 🎨 Mapear valor del potenciómetro a un tono de color HSB (0-255)
colorMode(HSB, 255);
float hue = map(potValue, 0, 1023, 0, 255);
trailColor = color(hue, 255, 255); // tono, saturación, brillo
colorMode(RGB, 255); // volver a RGB para el resto del dibujo

} catch (Exception e) {
println("Error al leer potenciómetro: " + e);
}
}
}
void draw() {
if (cam.width == 0) return;
background(0);
PImage diff = createImage(width, height, RGB);
cam.loadPixels();
prevFrame.loadPixels();
diff.loadPixels();
float avgX = 0;
float avgY = 0;
int motionCount = 0;
// Detectar movimiento (mano)
for (int i = 0; i < cam.pixels.length; i++) {
color curr = cam.pixels[i];
color prev = prevFrame.pixels[i];
float diffR = abs(red(curr) - red(prev));
float diffG = abs(green(curr) - green(prev));
float diffB = abs(blue(curr) - blue(prev));
float diffVal = (diffR + diffG + diffB) / 3;
if (diffVal > threshold) {
diff.pixels[i] = color(255);
int x = i % width;
int y = i / width;
avgX += x;
avgY += y;
motionCount++;
} else {
diff.pixels[i] = color(0);
}
}
diff.updatePixels();
prevFrame.copy(cam, 0, 0, width, height, 0, 0, width, height);

// Posición promedio del movimiento
if (motionCount > 500) {
motionPos.set(width - (avgX / motionCount), avgY / motionCount);
}
// --- Estela colorida controlada por potenciómetro ---
int which = frameCount % num;
mx[which] = motionPos.x;
my[which] = motionPos.y;
noStroke();
for (int i = 0; i < num; i++) {
int index = (which + 1 + i) % num;
float alpha = map(i, 0, num, 50, 200);
fill(red(trailColor), green(trailColor), blue(trailColor), alpha);
ellipse(mx[index], my[index], i, i);
}
// --- Círculo amarillo interactivo ---
if (circleVisible) {
fill(255, 200, 0, 200);
ellipse(targetCircle.x, targetCircle.y, circleSize, circleSize);
float d = dist(motionPos.x, motionPos.y, targetCircle.x, targetCircle.y);
if (d < circleSize / 2) {
circleVisible = false;
exploding = true;
explosionSize = circleSize;
explosionAlpha = 255;
}
}
// --- Explosión ---
if (exploding) {
fill(255, random(150, 255), 0, explosionAlpha);
ellipse(targetCircle.x, targetCircle.y, explosionSize, explosionSize);
explosionSize += 15;
explosionAlpha -= 20;
if (explosionAlpha <= 0) {
exploding = false;
targetCircle.set(random(margin, width - margin), random(margin, height -
margin));
circleVisible = true;

}
}
}
```
https://www.youtube.com/watch?v=XciaUtJu_mo
https://youtu.be/OPgpKR6e550
