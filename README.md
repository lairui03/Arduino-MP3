# Arduino

```
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <IRremote.h>
#include "Arduino.h"
#include "SoftwareSerial.h"
#include "DFRobotDFPlayerMini.h"
LiquidCrystal_I2C lcd(0x27, 16, 2);
int value;
String canciones[]={"Feel Me","x-industry baby","Central CEE Day in The Life","bum bum tam tam","xo tour lif3"};
const byte IR_RECEIVE_PIN = 9;
SoftwareSerial mySoftwareSerial(10, 11); // RX, TX
DFRobotDFPlayerMini myDFPlayer;
void printDetail(uint8_t type, int value);
void setup()
{
   
   mySoftwareSerial.begin(9600);
   Serial.begin(9600);
   IrReceiver.begin(IR_RECEIVE_PIN, ENABLE_LED_FEEDBACK);
    if (!myDFPlayer.begin(mySoftwareSerial)) {  //Use softwareSerial to communicate with mp3.
    Serial.println(F("Unable to begin:"));
    Serial.println(F("1.Please recheck the connection!"));
    Serial.println(F("2.Please insert the SD card!"));
    while(true);
    
  }
  
} 

void loop(){
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0,0);
       if (IrReceiver.decode())
   {
      value = IrReceiver.decodedIRData.command;
      IrReceiver.resume();
    
    if (value == 12){
    myDFPlayer.play(1);
    lcd.print("cancion " + canciones[0]);
   
   }
    else if(value == 24){
      lcd.clear();
      myDFPlayer.play(2);
   lcd.print("cancion " + canciones[1] );
    
      }
    else if(value == 94){
      lcd.clear();
       myDFPlayer.play(3);
    lcd.print("cancion " + canciones[2] );
      }
    else if(value == 8){
      lcd.clear();
       myDFPlayer.play(4);
    lcd.print("cancion " + canciones[3] );
      }
     else if(value == 28){
      lcd.clear();
       myDFPlayer.play(5);
    lcd.print("cancion " + canciones[4] );
      }

    else if (value == 9){
       myDFPlayer.volume(30);
      }
     else if (value == 7){
       myDFPlayer.volume(5);
      }
     else if (value == 67){
      myDFPlayer.next();
      }
     else if (value == 68){
       myDFPlayer.previous();
      }
     else if(value == 66){
      myDFPlayer.pause();
      }
     else if (value == 82){
        myDFPlayer.start();
        } 
   } 
    
}

```
