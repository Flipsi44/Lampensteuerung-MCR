# Lampensteuerung-MCR
Gruppe Arne Beckmann, Philipp Kulas

**Aufagabe ist es, mit zwei verschiedenen Microcontroller und I²C Protokoll eine Lampe anzusteuern.** 

**Als Microcontroller werden die STM401RE verwendet.** 

**Beide Microcontroller werden mit C++ programmiert, jedoch benutz der Slave die Arduino Framework und der Matser die Cmsis Framework.** 

**Der Master soll Bytes senden und empfangen. Durch die eingabe von Befehlen über UART werden die Bytes an den Slave geschickt. Der Slave muss dann diese Bytes erkennen und dann die Lampen, je nach Byte ansteuern. Auserdem soll der Master erkennen können ob der Slvae bereit ist zum empfangen.**

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

#include <Arduino.h>
#include <Wire.h>

**Die Ausgänge für die LEDs werden wie folgt deklariert.**

#define LED_RED D7
#define LED_YELLOW D4
#define LED_gruen D2

**Da die Microcontroller Bytes senden, müssen Variablen deklariert werden.** 

byte RxByte;       //R für Recieve
byte TxByte = 0;    // T für Transmitt

**Für die If-Anweisung später im Code brauchen wir Bedingunsvariablen.**

bool stateRed = false;
bool stateYellow = false;
bool stateGreen = false;

**Für das Recieven benötigen wir eine RecieveHandler Funktion**

void I2C_RxHandler(int numBytes)
{
  while(Wire.available()) {  // Ist eine verbindung da? 
    RxByte = Wire.read();    //Empfangener Byte wird in RxByte variable geschrieben
    Serial.println(RxByte);  //In den Seriel Monitor wird der emfangene byte eingetragen
  }
}

**Für das Senden der Bytes benötigen auch eine Funktion. Hier wird der Status der LEDs gelesen und je Nach status der TxByte verändert. Durch Wire.write bekommt nun der Master diesen Byte**

void I2C_TxHandler(void)
{
 
  if(!stateRed && !stateYellow && !stateGreen)
    {
        //ALL OFF
        TxByte = 0x10;
    }
    else if(stateRed && stateYellow && stateGreen)
    {
        //ALL ON
        TxByte = 0x11;
    }
    else if(stateRed && !stateYellow && !stateGreen)
    {
        //RED ON
        TxByte = 0x12;
    }
    else if(!stateRed && stateYellow && !stateGreen)
    {
        //YELLOW ON
        TxByte = 0x13;
    }
    else if(!stateRed && !stateYellow && stateGreen)
    {
        //GREEN ON
        TxByte = 0x14;
    }
    else if(stateRed && stateYellow && !stateGreen)
    {
        //RED & YELLOW ON
        TxByte = 0x15;
    }
    else if(stateRed && !stateYellow && stateGreen)
    {
        //RED & GREEN ON
        TxByte = 0x16;
    }
    else if(!stateRed && stateYellow && stateGreen)
    {
        //YELLOW & GREEN ON
        TxByte = 0x17;
    }
    Wire.write(TxByte);
}
















































