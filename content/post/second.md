---
title: "Elektrotechnik Labor"
date: 2022-11-13T15:05:13+02:00
draft: false
summary: "Um mit Sensoren und Microcontrollern abreiten zu können muss man grunlegendes über Strom, Spannung und Widerstand wissen, damit z.B. elektronische Bauteile wie LEDs, Kondensatoren etc. nicht durchbrennen oder gar explodieren.
Des weiteren haben wir gelernt die man mit einem Multimeter Spannungen, Stromstärke und Widerstände messen kann."
math: true
---
# SwH - Elektotechnik Labor

Im heutigen Elektrotechnik Labor haben wir die Grundlagen der Elektrotechnik besprochen, welche wir benötigen um im weiteren Labor Platinen und Bauteile jeglicher Art miteinander verbinden zu können. Um mit Sensoren und Microcontrollern abreiten zu können muss man grunlegendes über Strom, Spannung und Widerstand wissen, damit z.B. elektronische Bauteile wie LEDs, Kondensatoren etc. nicht durchbrennen oder gar explodieren.

Angefangen hat das Labor mit einer theoretischen Besprechnung der Grundlagen, wieso fließt elektrischer Strom und wieso kann dieser Arbeit verrichten. Eine wichtige Formel ist die Definition von Strom

$$ I = \frac{Q}{t} $$ 


Wobei I = **Stromstärke** Q = **Ladung** und t die **Zeit** in der die Ladung transportiert wird.

Dabei nennt man die “zeitliche Änderung einer Ladung Strom”. Wenn man sagt, dass Ladung abfließt, so liegen Ladungen getrennt vor und Ladung fließt von hohem zu niedrigem Potential. Dies wird auch als Spannung beschrieben. Die Formel die hierfür besprochen wurde ist:
$$ U = \frac{W}{Q} $$
Wobei U=**Spannung**, W=**Arbeit** und Q=**Ladung** gilt.

## Labor praxis - Teil 1

Nach dieser ersten Einführung in die Marterie ging es ins Labor um ein bisschen zu Löten. Nachdem wir eine allgemeine Einführung in Labor bekommen haben ging es eigentlich gleich zur Sache. Ich habe bereits zuvor gelötet und kannte daher das Prozedere, aber da ich bisher nicht wusste, dass man Lötpaste verwenden kann um bessere Lötstellen zu bekommen, sahen meine früheren Lötergebnisse nicht so gut aus, wie im Labor.

Wir bekamen ein paar Bauteile, welche wir festlöten sollten.

![loeten_bauteile](../2-lab1.jpg)

Und das taten wir:

![loeten_1](../2-lab2.jpg)

![loeten_2](../2-lab3.jpg)

![loeten_3](../2-lab4.jpg)

Mit ein bisschen Übung gelang es uns ziemlich schnell einigermaßen saubere Kontakte zu löten.

![loeten_4](../2-lab5.jpg)

Und letztlich hatten wir einige Bauteile auf unserer Probeplatine festgelötet.

![loeten_5](../2-lab6.jpg)

## Ohmsches Gesetz

Nach diesem praktischen “Ausflug” ging es nun wieder daran wichtige Themen zur weiteren Anwendung im Labor zu lernen.

Wobei das bisher besprochene generell informieren sollte, ging es beim Ohmschen Gesetzt um etwas sehr praxisbezogenes, was wir später im zweiten Teil des Labors anwenden mussten. Wir haben in diesem Zusammenhang besprochen, dass jedes Teil, auch Leitungen, einen Widerstand besitzt und weshalb Widerstände benötigt werden.

Die wohl wichtigste Formel, die wir in diesem Labor gelernt haben ergibt sich mit:

$$ R = \frac{U}{I} $$
wobei R=**Widerstand**, wieder U=**Spannung** und I=**Strom** gilt.

Grundsätzlich fließt Strom nicht verlustfrei, je Länger also eine Leitung ist, desto mehr Spannung wird “verbraucht”. Widerstände kann man sich somit als eng verwickelten Draht vorstellen, welcher Strom “verbraucht”. Die somit abgegebene Energie wird meist durch Wärme freigegeben.

Des weiteren war es sehr interessant zu erfahren, dass die Leistungsabgabe quadratisch erfolgt:

$$ P = R*I^2 $$
wobei P=**Leistungsabgabe**, wieder R=**Widerstand** und I=**Strom** gilt.

Wenn man also den fließenden Strom verdoppelt, so wird die Leistungsabgabe vervierfacht. Dies kann zur Folge haben, da Leistungsabgabe meist durch die abgabe von Wärme geschieht, dass bei einer geringen Erhöhung der Spannung Bauteile durchbrennen. Um zu verhindern, das Bauteile durchbrennen kann man **Vorwiderstände** verwenden.

Vor dem nächsten praktischen Teil bekamen wir nun noch erklärt wie man mit einem Multimeter Spannungen, Stromstärke und Widerstände messen kann.

![multimeter](../2-Multimeter.png)

Durch Widerstände im Multimeter lassen sich Stromstärke und Spannug messen (diese sind intern im Multimeter verarbeitet um das jeweilige zu messen). Dabei wird für die **Messung der Stromstärke (A)** das Multimete**r in Reihe** geschaltet - der Widerstand im Multimeter soll dabei so klein wie möglich sein um die Messung so wenig wie möglich zu beeinflussen. Wenn die **Spannung (V)** gemessen werden soll wir das Messgerät **parallel** geschaltet, wobei der Widerstand im Multimeter sehr groß ist, damit die meiste Spannung durch den gemessenen Abschnitt fließt.

Weiter haben wir neben Widerständen noch Komponenten wir Kondensatoren, Spulen und Dioden besprochen bevor es wieder ins Labor ging und wir Messungen durchführen mussten.  

## Labor praxis - Teil 2

In den weiteren Laborversuchen mussten wir wir das Ohmsche Gesetzt anwenden und mit den in den im praktischen Teil erklärten Konzepten vertraut machen.

### Versuch 1

Im Versuch sollten wir mit dem Multimeter die Spannung und die Stromstärke messen, welche durch den Widerstand läuft um heraus zu finden, um welchen Widerstand es sich handelt und wie viel Ohm dieser hat.

![labor_1](../2-e1.jpg)

![labor_2](../2-e2.jpg)

Wir musste eine Reihe von Werten nehmen, bei welchen wir sowohl Spannung, als auch Stromstärke durch ein Multimeter bestimmten und daraus mit der Formel $$R = \frac{U}{I}$$.

![daten_1](../2-versuch1.png)

Durch unsere Messungen haben wir herausfinden können, dass es sich um einen 100Ohm Widerstand gehandelt hat. Durch unsere Versuchsreihe haben sind wir auf 99 Ohm gekommen.

Als wir ihn direkt mit dem Multimeter gemessen haben hatte er 101 Ohm.

![labor_3](../2-e3.jpg)

### Versuch 2

In einem zweiten Versuchsaufbau haben wir einen neuen Widerstand über einen Messwiderstand gemessen, so wie das im Multimeter auch intern funktioniert, wenn man es auf die Messung eines Widerstands einstellt.

![daten_2](../2-versuch2.png)

Diesmal haben wir die Formel für Spannungsteiler verwenden können: 

$$
U_{R_2} = U_{ges} * \frac{R_2}{R_1 + R_2}
$$

![labor_4](../2-e4.jpg)

Wir haben nach unserer Versuchsreihe mit 7 Messwerten herausgefunden, dass der Widerstand 233 Ohm hat, wobei dieser bei 220 Ohm beschrieben war. Mit dem Multimeter haben wir 221 Ohm gemessen. Wir hatten somit eine Abweichung von ungefähr 5%, was noch im Rahmen liegt. 

## Weitere angewandte elektrotechnische Thematiken

Wir haben zum Abschluss weitere Einsatzgebiete von Widerständen angesehen, welche häufig Anwendung finden. Darunter Strombegrenzungen und Pull-Ups/Pull-Downs, was sehr interessant war, da ich davor noch nie etwas davon gehört habe. Weiterhin haben wir kurz über Kondensatoren, Relais, Transistoren, Treiberschaltungen, Reedschalter, Dioden, Optokoppler und Spannungsregler geredet und abschließend wurde noch das Oszilloskop vorgestellt.

## Kritik

Alles in allem hat mir das Elektrotechnik Labor sehr gut gefallen. Mir hat sowohl der theoretische Aspekt, sowie der praktische Teil sehr gefallen. Gerade das es sehr Hand in Hand ging, indem man das gelernte direkt anwenden konnte und das etappenweise, hat mir sehr zugesagt. Die Grundlagen, welche wir durch die Präsentation gelernt haben waren mir zu großen Teilen bereits bekannt, allerdings hat eine Auffrischung sicher nicht geschadet und ich habe noch viel neues dazugelernt.

## Projektwahl

Ich habe mich für das Projekt “Wetterstation” entschieden. Es bietet mir die Möglichkeit mit verschiedenen Sensoren zu experimentieren, zu lernen diese anzustuern und mit diesen zu hantieren und zu verstehen wie man sie einsetzt.

Dies ist noch ein kleiner Aufbau des Schaltplans, wie ich mir zur Zeit vorstelle die Wetterstation zu bauen.

![Wetterstation](../2-Wetterstation.png)

**Was ich für die Wetterstation benötige:**

- Rotationssensor für die Widngeschwindigkeit
- Ein Gerüst für den Rotationssensor zum umwandeln der Windstärke in eine Rotation
- Einen Feuchtigkeits Sensor
- Einen Temperatur Sensor
- Einen Luftdruck Sensor
- Entsprechende Gehäuse für die Sensoren zum Schutz und zur korrekten Aufnahme der Messwerte
    - Eventuell weitere Sensoren?
- Ein Display zur Darstellung der gemessenen Werte
    - Eventuell Weiterleitung der Daten per API an eine WebUI?

### Fritzing Schaltplan
![Fritzing_Entwurf_Wetterstation](../2-Wetterstation_Fritzing.png)
Dies ist mein erster Entwurf für den Schaltplan der Wetterstation, auch wenn ich mir wegen der Ansteuerung noch nicht sicher bin, ob es so funktionieren wird wie ich mir das vorstelle.