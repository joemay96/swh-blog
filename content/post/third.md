---
title: "Microcontroller Lab"
date: 2022-12-05T15:05:13+02:00
draft: false
summary: "Das Microcontroller Labor ging 2 Vorlesungen lang. In den zwei Microcontroller Labs haben wir erste Erfahrungen mit Microcontrollern sammeln können. Dabei Konnten wir verschiedene Microcontroller wie den Arduino Uno, aber auch z.B. den Arduino Mega ausprobieren können."
---
# Das Microcontroller Lab

In den zwei Microcontroller Labs haben wir erste Erfahrungen mit Microcontrollern sammeln können. Dabei Konnten wir verschiedene Microcontroller wie den Arduino Uno, aber auch z.B. den Arduino Mega ausprobieren können.

## Tag 1

Zu aller erst haben wir einen kleinen Einblick in die Maker Community bekommen und welche interessanten Projekte durch Microcontroller umgesetzt werden können. Erstaunlich finde ich immernoch, dass es für so ziemlich jeden Anwendungsfall bereits Komponenten gibt, welche man kaufen und verwenden kann und diese nicht entwickeln muss.

Wir haben uns zuerst mit dem Arduino Uno vertraut gemacht

![1.png](images/3/1.png)

und verstanden welche Pins grundlegend wofür verwendet werden. Später bei der Anwendung verschiedener Bauteile hat sich ergeben wofür alle weiteren Pins verwendet werden.

```arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}
```

Die erste Aufgabe nachdem wir den Arduino an unseren Laptops eingerichtet hatten bestand darin eine LED durch den Arduino zum blicken zu bringen.

![3.png](images/3/3.png)

![4.png](images/3/4.png)

Dafür haben wir die Standard Eingaben verwendet.

```arduino
int led_pin = 2;

void setup() {
  pinMode(led_pin, OUTPUT);
}

void loop() {
  digitalWrite(2, HIGH);
  delay(2000);
  digitalWrite(2, LOW);
  delay(2000);
}
```

Zum einen gibt es bei jedem Arduino Programm eine setup() Phase in welcher Pins und Einstellungen vorgenommen werden können und weiter eine loop() welche das Programm abbildet, welches sich permanent wiederholt.

Am ersten Tag habe ich mich noch mit mit einem **Potentiometer** beschäftigt. Es handelt sich dabei um einen dynamisch einstellbaren Widerstand und dieses habe ich dazu verwendet die Helligkeit der LED zu regeln, indem ich das Potentiometer hoch oder runter geregelt habe.

![11.png](images/3/11.png)

```arduino
int led_pin = 2;

int read_value = 0;
int led_value = 0;

void setup() {
  pinMode(led_pin, OUTPUT);
}

void loop() {
  read_value = analogRead(A1);
  led_value = map(read_value, 0, 1024, 0, 255);
  analogWrite(led_pin, led_value);
}
```

Als nächstes wollte ich mich mit einigen Sensoren vertraut machen, welche ich für die Wetterstation benötige.

Angefangen habe ich mit einem Luftfeuchtigkeitssensor, auch wenn ich anfangs ein paar Startschwierigkeiten hatte, da die Auslesung der Werte nicht so gut funktioniert hat, da ich zum Teil Widerstände vergessen habe einzubauen.

![12.png](images/3/12.png)

```arduino
//Benötigte Libraries
#include <Wire.h>
//Deklarieren der benötigten Variablen
#define adress 0x4F

void setup() {
  Serial.begin(9600);
  //Starten der Sensor Verbindung
  Wire.begin();
}

void loop() {
  //Ausführen der unten deklarierten Funktion
  int c1 = read_temp(adress);
  // Ausgabe des ermittelten Sensorwertes
  Serial.print("Sensor: ");
  Serial.print(c1);
  Serial.print("\n");
  //Pause
  delay(1000);
}

int read_temp(int address){
  //Start der Übertragung mit dem Sensor
  Wire.beginTransmission(address);
  //Senden eines Bits zum erhalt der Informationen
  Wire.write(0x00);
  //Anfrage 1 Bytes des Sensors
  Wire.requestFrom(address, 2);
  //Warten auf eine Antwort
  if (Wire.available() == 0) {
    //Speichern und Rückgabe des Wertes
    int c = Wire.read();
    //Beende Übertragung
    Wire.endTransmission();
    return c;
  } else {
    //Beende Übertragung
    Wire.endTransmission();
    return 0;
  }
}
```

Weiter habe ich einen Temperatursensor angeschlossen (dieser kann mit dem I2C Protokoll betrieben werden). Die Werte dieses Bauteils liesen sich ohne weitere Probleme auslesen.

![16.png](images/3/16.png)

```arduino
int val;
int encoder0PinA = 7;
int encoder0PinB = 6;
int encoder0PinC = 5;
int encoder0Pos = 0;
int encoder0PinALast = LOW;
int n = LOW;

void setup() {
  pinMode (encoder0PinA,INPUT);
  pinMode (encoder0PinB,INPUT);
  pinMode (encoder0PinC,INPUT);
  Serial.begin (9600);
}

void loop() {
  n = digitalRead(encoder0PinA);
  if ((encoder0PinALast == LOW) && (n == HIGH)) {
    if (digitalRead(encoder0PinB) == LOW) {
      encoder0Pos--;
    } else {
      encoder0Pos++;
    }
    Serial.print ("Encoder: ");
    Serial.print (encoder0Pos);
    Serial.print (", ");
    int button = digitalRead(encoder0PinC);
    Serial.print ("Button pressed: ");
    Serial.print (button);
    Serial.println (" ");
  }
  encoder0PinALast = n;
}
```

Zu guter Letzt benötige ich noch einen Sensor um die Windgeschwindigkeit zu messen. Dies kann ich durch die Verwendung eines Rotationssensors bewerkstelligen, für welchen ich noch eine geeignete Konstruktion benötige, damit der Rotationssenor durch den Wind gedreht wird und die Wetterstation die Windgeschwindigkeit messen kann.

Auch die Ansteuerung des Rotationssensors verlief reibungslos. Interessanter Weise besitzt der Rotationssensor noch einen Knopf.

![21.png](images/3/21.png)

```arduino
int val;
int encoder0PinA = 7;
int encoder0PinB = 6;
int encoder0PinC = 5;
int encoder0Pos = 0;
int encoder0PinALast = LOW;
int n = LOW;

void setup() {
  pinMode (encoder0PinA,INPUT);
  pinMode (encoder0PinB,INPUT);
  pinMode (encoder0PinC,INPUT);
  Serial.begin (9600);
}

// encoder0Pos zeigt in welche Richtung der Rotationssensor sich bewegt und man 
// kann feststellen, wann er eine vollständige Rotation durchgeführt hat
void loop() {
  n = digitalRead(encoder0PinA);
  if ((encoder0PinALast == LOW) && (n == HIGH)) {
    if (digitalRead(encoder0PinB) == LOW) {
      encoder0Pos--;
    } else {
      encoder0Pos++;
    }
    Serial.print ("Encoder: ");
    Serial.print (encoder0Pos);
    Serial.print (", ");
    int button = digitalRead(encoder0PinC);
    Serial.print ("Button pressed: ");
    Serial.print (button);
    Serial.println (" ");
  }
  encoder0PinALast = n;
}
```

## Tag 2

Am zweiten Tag habe ich beschlossen, dass die Wetterstation ihre Daten per WLAN eine Datenbank senden könnte und diese ohne zu viel Aufwand online verfübar  sein könnten. Daher habe ich mich mit den Wfi Modulen z.B. dem Wemos D1 Mini vertraut gemacht. Eigentlich hätte die Einrichtung relativ einfach sein sollen, nur leider hat das gesamte Prozedere nicht so funktioniert wie ich es mir vorgestellt habe. Nachdem ich das Modul angeschlossen habe und mich auch versichert habe, dass das Modul korrekt eingesteckt ist hat mein Laptop den Arduino leider nicht erkannt. Nach viel debugging hat sich herausgestellt, dass das Problem weder am Arduino noch an den Wifi Modulen gelegen hat. Leider hat mein Laptop die Treiber für besagten Arduino mit integiertem Wifi (Lolin wemos r2) nicht verwenden können, auch wenn laut diverser Quellen diese benötigten Treiber bereits im Linux Kernel integiert sein sollen. Nach weiterem herumprobieren habe ich probiert nur den verwendeten Arduino anzuschließen und auch das hat nicht funktioniert.

Es war nun also klar, dass die Problemtik nicht umbedingt an den Wifi Modulen lag sondern am Chipsatz des Arduino. Nachdem ich auf einen Arduino Uno umgestiegen bin, welcher einen aufgesteckten Microcontroller hat und dieser nicht als Chip festgelötet ist (ich nehme an, es handelt sich um ein neueres Modell) hat alles weitere reibungslos funktioniert, da dieser Arduino andere Treiber verwendet.

Da ich mich aber dem neueren Modell mit integiertem Wifi nicht geschlagen geben wollte habe ich probiert diesen an meinem Windows Rechner zum laufen zu bringen. Dies funktionierte reibungslos und war Kinderleicht.

Mein zweiter Tag hat sich somit als nicht sonderlich effizient herausgestellt, wenn man ihn anhand verwendeter Sensoren betrachtet. Für mich war der gesamte Tag allerdings durchaus lehrreich. Ich habe viel über die verschiedenen Wifi Module, über die verschiedenen Chipsätze und Treiber, welche zum Betreiben der Arduinos verwendet wird, gelernt.

### Displays

Weiter möchte ich aber auch ein Display für meine Wetterstation verwenden, damit direkt (und nicht nur über eine online Plattform) die Werte ausgelesen werden können. Ebenfalls möchte ich mich gerne mit Displays beschäftigen, da diese für viele Projekte verwendet werden.

![7.png](images/3/7.png)

Ich habe mich für ein kleines 1.3” Oled Display entschieden, da es sich zum einen herausgestellt hat, dass ich keine Spannungsregler verwenden muss, wie das bei anderen Displays der Fall ist und zum anderen finde ich es passend ein kleines, funktioniales Display für eine kleine, funktioniale Wetterstation zu verwenden 😃

```arduino
#include "U8glib.h"
U8GLIB_SH1106_128X64 u8g(U8G_I2C_OPT_NONE);

void draw(void) {
  u8g.setFont(u8g_font_profont12);
  u8g.setPrintPos(0, 10);
  u8g.print("Hallooooo :D");
  u8g.setPrintPos(0, 25);
  u8g.print("OLED i2c Display");
  u8g.setPrintPos(0, 40);
  u8g.setFont(u8g_font_profont10);
  u8g.print("Hello from another world!");
}

void draw2(void) {
  u8g.setFont(u8g_font_profont12);
  u8g.setPrintPos(0, 10);
  u8g.print("Another Site");
  u8g.setPrintPos(0, 25);
  u8g.print("Check this out!");
  u8g.setPrintPos(0, 40);
  u8g.setFont(u8g_font_profont10);
  u8g.print("This is a very long text");
}

void setup(void) {
}

void loop(void) {
  u8g.firstPage();
  do {
    draw();
  } while (u8g.nextPage() );
  delay(3500);
  u8g.firstPage();
  do {
    draw2();
  } while (u8g.nextPage());
  delay(3500);
}
```

Der Code für das Display war einigermaßen straightforward. Interessant finde ich daran, dass der Inhalt der auf das Display geschrieben wird in einer Schleife ist um ständig refreshed zu werden. Dies ist im nachhinein logisch, war am Anfang für mich aber eine echte Erkenntnis.

Des weiteren hat sich das Display angeboten, da dieses mit dem seriellen I2C Protokoll betrieben wird und ich dadurch Möglichkeit hatte das I2C Protokoll auszuprobieren.

![6.png](images/3/6.png)

Wie man auf diesem Bild sieht habe ich den Text von ersten Display (rechtes Display) and das zweite Display weitergeleitet. Normalerweise wird I2C dafür verwendet um mehrere Geräte an einem Strang per ID ansprechen zu können. Dies ist zum Beispiel sinnvoll, wenn eine LED Kette angeschlossen wird und man jede LED einzeln ansteuern möchte, aber nicht für jede LED einen Pin am Arduino belegen möchte. Es muss dann die gesamte LED Kette (oder anderes I2C Gerät) nur an die Stromversorgung und an die SDA (Arduino Pin A4) und SCL (Arduino Pin A5) angeschlossen werden.

Leider konnte ich das I2C Protokoll codetechnisch nicht voll ausreitzen, da jedes Display nicht seine eigene ID besitzt. Es war somit nur möglich den gleichen Inhalt auf beiden Displays  zu zeigen, allerdings nicht verschiedene Inhalte und das Display somit zu erweitern. Daher habe ich mich in der restlichen Zeit noch mit Interrupts beschäftigt.

### Interrupt

Interrupts scheinen ein wichtiges Konzept auch bei Microcontrollern zu sein. Interrupts stoppen, wenn sie gefeuert werden, den aktuellen Programmablauf des Arduino um auf ein Event zu reagieren. Diese Funktionalität kann für sehr viele Anwendungen verwendet werden. Ein Beispiel, welches mir in Erinnerung geblieben ist, ist ein Arduino, welcher die meiste Zeit in einem StandBy Modus läuft und diesem durch einen Interrupt geweckt wird, falls sich ein Client per Wifi verbindet. Dieser Arduino läuft nur anhand eines Akkus und kann durch die geschickte Verwendung des StandBy Modus und des Interrupts wesentlich länger mit dem Strom haushalten, als das bei normalem Betrieb möglich wäre.

Ich habe mich dafür entschieden, da ich die Displays noch angeschlossen hatte, durch einen Interrupt die Seite auf dem Display zu wechseln. Dieser Interrupt wird der einfachheit halber durch einen Button ausgelöst. Auch wenn man diesen Aufbau ohne einen Interrupt hätte bwerkstelligen können, so ist es ebenfalls durch einen Interrupt lösbar.

![2.png](images/3/2.png)

Nach dem Auslösen des Interrupts durch das Betätigen des Buttons erhält man eine neue Seite.

![5.png](images/3/5.png)

Den Code für den Interrupt hatte ich mir schwerer vorgestellt, allerdings gibt es hierfür die Methode **attachInterrupt()** welche aufgerufen werden kann. Der Methode wird als erster Parameter der digitale Pin für einen Interrupt übergeben, als nächstes der name der Funktion, welche im Falle eines Interrupts ausgeführt werden soll und als dritter Parameter wird einer der Konstanten übergeben: **LOW, CHANGE, FALLING**. Hierbei geht es darum bei welchem Event der Interrupt feuern soll. **LOW** triggert, wenn der pin auf low steht, **CHANGE** respektive sobald der Pin seinen Wert ändert und **FALLING**, wenn der Pin von high nach low geht.

In dem Beispiel mit dem triggern des Interrupts anhand eines Buttons hat sich CHANGE als der richtige Trigger herausgestellt.

```arduino
#include "U8glib.h"
#define INTERRUPT_PIN 2 //Der Pin 2 und 3 können als interrupt Pins verwendet werden
#define INTERRUPT_STATE CHANGE
bool disable_display = false;

U8GLIB_SH1106_128X64 u8g(U8G_I2C_OPT_NONE);

void draw(void) {
  u8g.setFont(u8g_font_profont12);
  u8g.setPrintPos(0, 10);
  u8g.print("OLED i2c Display");
  u8g.setPrintPos(0, 25);
  u8g.print("Hallooooo :)");
  u8g.setPrintPos(0, 40);
  u8g.setFont(u8g_font_profont10);
  u8g.print("Hello from another world!");
}

void draw2(void) {
  u8g.setFont(u8g_font_profont12);
  u8g.setPrintPos(0, 10);
  u8g.print("Check out the project");
  u8g.setPrintPos(0, 25);
  u8g.print("This is the second Page");
  u8g.setPrintPos(0, 40);
  u8g.setFont(u8g_font_profont10);
  u8g.print("Change page with interrupt");
}

void setup(void) {
  Serial.begin(9600);
  // attach the interrupt to trigger the interruptfunction
  //digitalPinToInterrupt(INTERRUPT_PIN)
  attachInterrupt(0, interrupt_display, FALLING);
  Serial.println("Started");
}

void loop(void) {
  if(!disable_display) {
    Serial.print("0");
    u8g.firstPage();
    do {
      draw();
    } while (u8g.nextPage() );
    delay(1000);
  } else {
    Serial.print("1");
    u8g.firstPage();
    do {
      draw2();
    } while (u8g.nextPage() );
    delay(1000);
  }
}

void interrupt_display() {
  // change state
  Serial.println("Interrupt");
  disable_display = true; //!disable_display;
}
```

Eine Problematik, die sich beim Erzeugen des Interrupts speziell durch einen Button ergeben hat, ist das der Button durch Spannungsspitzen oder ähnliches mehrfach ausgelöst werden kann und dies den Effekt haben kann, dass mehrere Interrupts ausgelöst werden. Um dies zu verhindern müsste ein Timeout weitere Interrupts eingerichtet werden, allerdings bin ich dazu nicht mehr gekommen. Eine mögliche Lösung für das Problem habe ich allerdings [hier](https://create.arduino.cc/projecthub/rafitc/interrupts-basics-f475d5) gefunden.

### Weiteres Lernen

Gerne hätte ich noch weitere Sensoren wie einen Licht und einen UV-Sensor angeschlossen und ausgelesen oder probiert einen CO Sensor in Betrieb zu nehmen. Außerdem hätte ich gerne mehr Zeit damit verbracht das Wifi Modul wirklich auszutesten, da mir dazu leider ein wenig die Zeit abhanden ist.

Ebenso würde ich mich, wenn ich mehr Zeit mit Microkontrollern hätte mich noch mehr mit der Thematik der seriellen Protokolle auseinander gesetzt und versucht die einzelnen Protokolle (nicht nur I2C) besser zu verstehen.

Alles in allem begeistern mich Microcontroller sehr, da sie so vielfälltig sind und ich freue mich sie in meinem Projekt benutzen und verwenden zu können.
