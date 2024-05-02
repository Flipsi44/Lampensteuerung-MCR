# Lampensteuerung-MCR
Gruppe Arne Beckmann, Philipp Kulas

**Aufagabe ist es, mit zwei verschiedenen Microcontroller und I²C Protokoll eine Lampe anzusteuern.** 

**Als Microcontroller werden die STM401RE verwendet.** 

**Beide Microcontroller werden mit C++ programmiert, jedoch benutzt der Slave die Arduino Framework und der Master die Cmsis Framework.** 

**Der Master soll Bytes senden und empfangen. Durch die Eingabe von Befehlen über UART werden die Bytes an den Slave geschickt. Der Slave muss dann diese Bytes erkennen und dann die Lampen, je nach Byte ansteuern.**

//Bytes:

//Send:

//0x01    -> All LEDs OFF

//0x02    -> All LEDs ON

//0x03    -> LED red ON

//0x04    -> LED red OFF

//0x05    -> LED yellow ON

//0x06    -> LED yellow OFF

//0x07    -> LED green ON

//0x08    -> LED green OFF

//0x09    -> READ LED Status

//Receive:

//0x10    -> All LEDs OFF

//0x11    -> All LEDs ON

//0x12    -> yellow & green off               

//0x13    -> red & green off
            
//0x14    -> red & yellow off             

//0x15    -> green off   

//0x16    -> yellow off    

//0x17    -> red off   


**Slave:**

Der Slave verwendet die Arduino Framework. Deshalb müssen auch die Arduino Bibliothekt und die Wire Bibliothek installiert werden. 
Durch die Wire Bibliothek, können wir mit WIre.anviable() den Status auf der Leitung prüfen, mit Wire.write() die Transmitt Bytes übertragen und mit Wire.read() empfangene Bytes lesen. 

Durch die Case Struktur, die in der Loop ist, wird der RxByte abgefragt. Je nach wert springt die Loop dann in einen Case und steuert die Lampen. 

In der IF-Anweisung in der I2C_TxHandler werden die drei bool Variablen, stateRed, stateYellow und stateGreen als Bedingung abgefragt. Je nachdem welchen Status die LED haben, springt der I2C_TxHandler in einen der If-else fälle. 
















































