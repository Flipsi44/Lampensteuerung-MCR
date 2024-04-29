# Lampensteuerung-MCR
Gruppe Arne Beckmann, Philipp Kulas

**Aufagabe ist es, mit zwei verschiedenen Microcontroller und I²C Protokoll eine Lampe anzusteuern.** 

**Als Microcontroller werden die STM401RE verwendet.** 

**Beide Microcontroller werden mit C++ programmiert, jedoch benutz der Slave die Arduino Framework und der Matser die Cmsis Framework.** 

**Der Master soll Bytes senden und empfangen. Durch die Eingabe von Befehlen über UART werden die Bytes an den Slave geschickt. Der Slave muss dann diese Bytes erkennen und dann die Lampen, je nach Byte ansteuern. Auserdem soll der Master erkennen können ob der Slave bereit ist zum empfangen.**

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
//
//Receive:
//0x10    -> All LEDs OFF
//0x11    -> All LEDs ON
//0x12    -> LED red ON               -> yellow & green off
//0x13    -> LED yellow ON            -> red & green off
//0x14    -> LED green ON             -> red & yellow off
//0x15    -> LEDs red & yellow ON     -> green off
//0x16    -> LEDs red & green ON      ->yellow off
//0x17    -> LEDs yellow & green ON   ->red off

**Slave:**
**Der Slave benutzt die Arduino Framework und muss daher die Ardunio Bibliothek und die Wire Bibliothek eingefügt werden.**

Der Slave verwendet die Arduino Framework















































