#include "GyverEncoder.h"
#define CLK 3
#define DT 2
#define SW 4
#define S0 7
#define S1 8
#define S2 9
#define S3 10
#define sensorOut 5
#include <LiquidCrystal_I2C.h> //Дисплей
#include <EEPROM.h>
LiquidCrystal_I2C lcd(0x27,20,4); //Параметры дисплея
//unsigned long Tick;
uint32_t Timer_1, Timer_2, Timer_3, Timer_4, Timer_5;
Encoder enc1(CLK, DT, SW);  // для работы c кнопкой
int freg = 0;
int frequency = 0;
int fregpic = 0;
int fregvno = 0;
int SELCT = 1;
// int GREEN[] = {175, 189, 194};
// int RED[] = {123, 57, 81};
// int BLUE[] = {210, 225, 240};
int taraskvas[] = {189, 190, 185};
int skovoroda[] = {220, 220, 218};
int kupur = 0;
int SENSOR = A0;
int MOTOR = 11;
int DOOR = 12;
int PAGE = 1;
int MONEYP11 = 0;
int MODE = 1;
int STEP = 0;  
int ADD = 0;  
int ROVNO = 0; 
int one = 0;
int two = 0;
int three = 0;
int onetwo = 0;
int twotwo = 0;
int threetwo = 0;
int onethree = 0;
int twothree = 0;
int threethree = 0;
int onefour = 0;
int twofour = 0;
int threefour = 0;

int SELECTED = 1;
int SELECTEDF = 1;
int CONFIRMED = 0;
bool CHAGE = true; 
int R = 0;
int G = 0;
int B = 0;
int COUNT = 0;
int ACTIVATE = 0;
int RED = 0;
int GREEN = 0;
int BLUE = 0;
int var = 0;
long banknote = 0;
long kuk = 0;
void setup() {

  EEPROM.get(0,one);
  EEPROM.get(2,two);
  EEPROM.get(4,three);
  EEPROM.get(6,onetwo);
  EEPROM.get(8,twotwo);
  EEPROM.get(10,threetwo);
  EEPROM.get(12,onethree);
  EEPROM.get(14,twothree);
  EEPROM.get(16,threethree);
  EEPROM.get(18,onefour);
  EEPROM.get(20,twofour);
  EEPROM.get(22,threefour);


  enc1.setType(TYPE2);
  lcd.init(); 
  lcd.backlight();
  Serial.begin(9600);
  pinMode(MOTOR, OUTPUT);
  pinMode(DOOR, OUTPUT);
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(sensorOut, INPUT);
  digitalWrite(S0,1);
  digitalWrite(S1,1);

}

void loop() 
{
  enc1.tick();
    if (analogRead(SENSOR) > 600)
  {
      
        PAGE = 4;
        CHAGE = true;
        lcd.clear();
        Serial.println(PAGE);
         lcd.setCursor(3, 3);
         lcd.print("       ");
         lcd.setCursor(3, 2);
         lcd.print("       ");
         lcd.setCursor(0, 1);
         lcd.print("       ");
         lcd.setCursor(12, 3);
         lcd.print("    ");
         lcd.setCursor(12, 2);
         lcd.print("    ");
      digitalWrite(MOTOR, HIGH);
      Serial.println(var);
      delay(200);

      while(var < 10)
      {
      
      
        //R
        digitalWrite(S2,LOW);
        digitalWrite(S3,LOW);
        frequency = pulseIn(sensorOut, LOW);
        R = frequency;
        Serial.print(R);
        Serial.print(" ");
        //G
        digitalWrite(S2,HIGH);
        digitalWrite(S3,HIGH);
        frequency = pulseIn(sensorOut, LOW);
        G = frequency;
        Serial.print(G);
        Serial.print(" ");
        //B
        digitalWrite(S2,LOW);
        digitalWrite(S3,HIGH);
        frequency = pulseIn(sensorOut, LOW);
        B = frequency;
        Serial.print(B);
        Serial.print(" ");
        COUNT +=1;
        var++;
        Serial.println(var);

        //long RGB = (R << 16) | (G << 8) | B;
        //Serial.println(RGB, HEX);

      
        RED = R; /// COUNT;
        GREEN = G; /// COUNT;
        BLUE = B; /// COUNT;


          if ((118 < RED) and (RED < 132))
          {
              if ((70 < GREEN) and (GREEN < 89))
              {
                if ((32 < BLUE) and (BLUE < 40))
                {
                    lcd.setCursor(0, 2);
                    lcd.print("20");
                    kupur = 20;

                }
              }
          }
          if ((19 < RED) and (RED < 30))
          {
              if ((26 < GREEN) and (GREEN < 40))
              {
                if ((36 < BLUE) and (BLUE < 50))
                {
                    lcd.setCursor(0, 1);
                    lcd.print("yellow");
                    Serial.println("gggg");
                    kupur = 50;
                }
              }
          }
          if ((59 < RED) and (RED < 85))
          {
              if ((35 < GREEN) and (GREEN < 48))
              {
                if ((50 < BLUE) and (BLUE < 65))
                {
                    lcd.setCursor(0, 1);
                    lcd.print("Green");
                    Serial.println("gggg");
                    kupur = 100;
                }
              }
          }
          if ((15 < RED) and (RED < 28))
          {
              if ((58 < GREEN) and (GREEN < 78))
              {
                if ((53 < BLUE) and (BLUE < 70))
                {
                    lcd.setCursor(0, 1);
                    lcd.print("Red");
                    Serial.println("gggg");
                    kupur = 200;
                }
              }
          }
          if ((28 < RED) and (RED < 43))
          {
              if ((20 < GREEN) and (GREEN < 36))
              {
                if ((15 < BLUE) and (BLUE < 25))
                {
                    lcd.setCursor(0, 1);
                    lcd.print("Grey");
                    Serial.println("gggg");
                    kupur = 500;
                }
              }
          }
          if ((52 < RED) and (RED < 83))
          {
              if ((56 < GREEN) and (GREEN < 83))
              {
                if ((26 < BLUE) and (BLUE < 43))
                {
                    lcd.setCursor(0, 1);
                    lcd.print("Purple");
                    Serial.println("gggg");
                    kupur = 1000;
                }
              }
          }
          kuk = banknote + kuk;
          // lcd.setCursor(0, 3);
          // lcd.print(banknote);
          // lcd.setCursor(0, 2);
          // lcd.print(kuk);
          banknote = 0;
          
      }
    var = 0;
  }
        if (analogRead(SENSOR) < 600 ) 
        {
        digitalWrite(MOTOR, LOW);

        }
  
  if (millis() - Timer_1 >= 500)
  {
    Timer_1 = millis();

  }

  digitalWrite(DOOR, LOW);
  digitalWrite(MOTOR, LOW);
  if (millis() - Timer_2 >= 500)
  {
      Timer_2 = millis();
      if (CHAGE == true)
      {
        if (PAGE == 5)
        {
                                                                                                   
        }
        if (PAGE ==1 )
        {
          lcd.clear();
            Serial.println("3333333312222");
            lcd.setCursor(1, 0);
            lcd.print("1.");
            lcd.setCursor(3, 0);
            lcd.print(one);
            lcd.setCursor(8, 0);
            lcd.print(",");
            lcd.setCursor(9, 0);
            lcd.print(two);
            lcd.setCursor(14, 0);
            lcd.print(",");
            lcd.setCursor(15, 0);
            lcd.print(three);
            lcd.setCursor(1, 1);
            lcd.print("2.");
            lcd.setCursor(3, 1);
            lcd.print(onetwo);
            lcd.setCursor(8, 1);
            lcd.print(",");
            lcd.setCursor(9, 1);
            lcd.print(twotwo);
            lcd.setCursor(14, 1);
            lcd.print(",");
            lcd.setCursor(15, 1);
            lcd.print(threetwo);
            lcd.setCursor(1, 2);
            lcd.print("3.");
            lcd.setCursor(3, 2);
            lcd.print(onethree);
            lcd.setCursor(8, 2);
            lcd.print(",");
            lcd.setCursor(9, 2);
            lcd.print(twothree);
            lcd.setCursor(14, 2);
            lcd.print(",");
            lcd.setCursor(15, 2);
            lcd.print(threethree);
            lcd.setCursor(1, 3);
            lcd.print("4.");
            lcd.setCursor(3, 3);
            lcd.print(onefour);
            lcd.setCursor(8, 3);
            lcd.print(",");
            lcd.setCursor(9, 3);
            lcd.print(twofour);
            lcd.setCursor(14, 3);
            lcd.print(",");
            lcd.setCursor(15, 3);
            lcd.print(threefour);
            CHAGE = false ;
          
        }
        if (PAGE == 4)
        {
          lcd.clear();
         lcd.setCursor(0, 0);
         lcd.print("                      ");

         lcd.setCursor(3, 1);
         lcd.print("pocket:");
         lcd.setCursor(10, 1);
         lcd.print(kupur);
         lcd.setCursor(1, 2);
         lcd.print("1:");
         lcd.setCursor(3, 2);
         lcd.print(one);
         lcd.setCursor(10, 2);
         lcd.print("2:");
         lcd.setCursor(12, 2);
         lcd.print(onetwo);
         lcd.setCursor(1, 3);
         lcd.print("3:");
         lcd.setCursor(3, 3);
         lcd.print(onethree);
         lcd.setCursor(10, 3);
         lcd.print("4:");
         lcd.setCursor(12, 3);
         lcd.print(onefour);
        }
        if (PAGE ==2)
          {
            lcd.clear();
            lcd.setCursor(1, 0);
            lcd.print("1.");
            lcd.setCursor(3, 0);
            lcd.print(two);
            lcd.setCursor(8, 0);
            lcd.print("             ");
            lcd.setCursor(1, 1);
            lcd.print("2.");
            lcd.setCursor(3, 1);
            lcd.print(twotwo);
           lcd.setCursor(8, 1);
            lcd.print("             ");
            lcd.setCursor(1, 2);
            lcd.print("3.");
            lcd.setCursor(3, 2);
            lcd.print(twothree);
            lcd.setCursor(8, 2);
            lcd.print("             ");
            lcd.setCursor(1, 3);
            lcd.print("4.");
            lcd.setCursor(3, 3);
            lcd.print(twofour);
            lcd.setCursor(8, 3);
            lcd.print("             ");
            Serial.println(CHAGE);
            CHAGE = false;
        }
        if (PAGE ==3)
          {
            lcd.clear();
            Serial.println("fffff");
            lcd.setCursor(1, 0);
            lcd.print("1.");
            lcd.setCursor(3, 0);
            lcd.print(one);
            lcd.setCursor(8, 0);
            lcd.print(",");
            lcd.setCursor(9, 0);
            lcd.print(two);
            lcd.setCursor(14, 0);
            lcd.print(",");
            lcd.setCursor(15, 0);
            lcd.print(three);
            lcd.setCursor(1, 1);
            lcd.print("2.");
            lcd.setCursor(3, 1);
            lcd.print(onetwo);
            lcd.setCursor(8, 1);
            lcd.print(",");
            lcd.setCursor(9, 1);
            lcd.print(twotwo);
            lcd.setCursor(14, 1);
            lcd.print(",");
            lcd.setCursor(15, 1);
            lcd.print(threetwo);
            lcd.setCursor(1, 2);
            lcd.print("3.");
            lcd.setCursor(3, 2);
            lcd.print(onethree);
            lcd.setCursor(8, 2);
            lcd.print(",");
            lcd.setCursor(9, 2);
            lcd.print(twothree);
            lcd.setCursor(14, 2);
            lcd.print(",");
            lcd.setCursor(15, 2);
            lcd.print(threethree);
            lcd.setCursor(1, 3);
            lcd.print("4.");
            lcd.setCursor(3, 3);
            lcd.print(onefour);
            lcd.setCursor(8, 3);
            lcd.print(",");
            lcd.setCursor(9, 3);
            lcd.print(twofour);
            lcd.setCursor(14, 3);
            lcd.print(",");
            lcd.setCursor(15, 3);
            lcd.print(threefour);

            CHAGE = false;
        }
      }
    
    
  }

  if (MODE == 1)
  {
    if (PAGE == 1)
    {

    
    
      if (enc1.isRight()) 
      {
        PAGE = 2;
        MODE = 1;
      }
      if (enc1.isClick())
      {
        one = 0;
        two = 0;
        three = 0;
        onetwo = 0;
        twotwo = 0;
        threetwo = 0;
        onethree = 0;
        twothree = 0;
        threethree = 0;
        onefour = 0;
        twofour = 0;
        threefour = 0;
        EEPROM.put(0,int(one));
        EEPROM.put(2,int(two));
        EEPROM.put(4,int(three));
        EEPROM.put(6,int(onetwo));
        EEPROM.put(8,int(twotwo));
        EEPROM.put(10,int(threetwo));
        EEPROM.put(12,int(onethree));
        EEPROM.put(14,int(twothree));
        EEPROM.put(16,int(threethree));
        EEPROM.put(18,int(onefour));
        EEPROM.put(20,int(twofour));
        EEPROM.put(22,int(threefour));
      } 
    }
    if (PAGE == 4)
    {
      if (SELCT == 1)
      {
        lcd.setCursor(0, 2);
        lcd.print(">");
      }
      if (SELCT == 2)
      {
        lcd.setCursor(9, 2);
        lcd.print(">");
      }
      if (SELCT == 3)
      {
        lcd.setCursor(0, 3);
        lcd.print(">");
      }
      if (SELCT == 4)
      {
        lcd.setCursor(9, 3);
        lcd.print(">");
      }
    
    
      if (enc1.isRight()) 
      {
        SELCT = SELCT + 1;
        CHAGE = true;
      }
      if (enc1.isRight()) 
      {
        SELCT = SELCT - 1;
        CHAGE = true;
      }
      if (enc1.isClick())
      {
        if (SELCT == 1)
        {

        one = one + kupur;
        EEPROM.put(0,int(one));
        Serial.println(one);
        kupur = 0;
        PAGE = 1;
        lcd.clear();
        CHAGE = true;
        }
        if (SELCT == 2)
        {

        onetwo = onetwo + kupur;
        EEPROM.put(6,int(onetwo));
        Serial.println(onetwo);
        kupur = 0;
        PAGE = 1;
        lcd.clear();
        CHAGE = true;
        }
        if (SELCT == 3)
        {

        onethree = onethree + kupur;
        EEPROM.put(12,onethree);
        Serial.println(kupur);
        Serial.println(onethree);
        kupur = 0;
        PAGE = 1;
        lcd.clear();
        CHAGE = true;
        }
        if (SELCT == 4)
        {

        onefour = onefour + kupur;
        EEPROM.put(18,onefour);
        Serial.println(kupur);
        Serial.println(onefour);
        kupur = 0;
        PAGE = 1;
        lcd.clear();
        CHAGE = true;
        }
      } 
    }


    if (PAGE == 2)
    {

    
    
      if (enc1.isRight())
      {
        PAGE = 3;
        CHAGE = true;
      }
      if (enc1.isLeft()) 
      {
        PAGE = 1;
        CHAGE = true;
      }
      if (enc1.isClick())
      {
        MODE = MODE + 1;
        CHAGE = true;
      } 
    }
  }

  if (MODE == 2)
  {
    if (SELECTED == 1)
    {
      if (PAGE == 2)
      {
          lcd.setCursor(0, 0);
          lcd.print(">");
        
        
        if (enc1.isRight()) 
        {
          SELECTED = SELECTED + 1;
          CHAGE = true;
        }
        if (enc1.isLeft()) 
        {
          SELECTED = SELECTED - 1;
          CHAGE = true;
        }
        if (enc1.isClick())
        {
          MODE = 3;
          CHAGE = true;

        } 
      }
    }
  }
    if (SELECTED == 1)
    {
      if (PAGE == 2)
      {
        if (MODE == 3)
        {
            lcd.setCursor(0, 0);
            lcd.print(">");
        
        
            if (enc1.isRight()) 
            {
              two = two + 1;
              EEPROM.put(2,int(two));
              CHAGE = true;
            }
            if (enc1.isRight()) 
            {
              two = two - 1;
              EEPROM.put(2,int(two));
              CHAGE = true;
            }
            if (enc1.isClick())
            {
              MODE = 1;
              CHAGE = true;

            } 
        }
      }
    }
    
  if (MODE == 2)
  {  
    if (SELECTED == 2)
    {
      if (PAGE == 2)
      {
          lcd.setCursor(0, 1);
          lcd.print(">");
        
        
        if (enc1.isRight()) 
        {
          SELECTED = SELECTED + 1;
          CHAGE = true;
        }
        if (enc1.isLeft()) 
        {
          SELECTED = SELECTED - 1;
          CHAGE = true;
        }
        if (enc1.isClick())
        {
          MODE = 3;
          CHAGE = true;

        } 
      }
    }
  }
    if (SELECTED == 2)
    {
      if (PAGE == 2)
      {
        if (MODE == 3)
        {
            lcd.setCursor(0, 1);
            lcd.print(">");
        
        
            if (enc1.isRight()) 
            {
              twotwo = twotwo + 1;
              EEPROM.put(8,int(twotwo));
              CHAGE = true;
            }
            if (enc1.isRight()) 
            {
              twotwo = twotwo - 1;
              EEPROM.put(8,int(twotwo));
              CHAGE = true;
            }
            if (enc1.isClick())
            {
              MODE = 1;
              CHAGE = true;

            } 
        }
      }
    }
  if (MODE == 2)
  {
    if (SELECTED == 3)
    {
      if (PAGE == 2)
      {
          lcd.setCursor(0, 2);
          lcd.print(">");
        
        
        if (enc1.isRight()) 
        {
          SELECTED = SELECTED + 1;
          CHAGE = true;
        }
        if (enc1.isLeft()) 
        {
          SELECTED = SELECTED - 1;
          CHAGE = true;
        }
        if (enc1.isClick())
        {
          MODE = 3;
          CHAGE = true;

        } 
      }
    } 
  }
    if (SELECTED == 3)
    {
      if (PAGE == 2)
      {
        if (MODE == 3)
        {
            lcd.setCursor(0, 2);
            lcd.print(">");
        
        
            if (enc1.isRight()) 
            {
              twothree = twothree + 1;
              EEPROM.put(14,twothree);
              CHAGE = true;
            }
            if (enc1.isLeft()) 
            {
              twothree = twothree - 1;
              EEPROM.put(14,twothree);
              CHAGE = true;
            }
            if (enc1.isClick())
            {
              MODE = 1;
              CHAGE = true;

            } 
        }
      }
    }

      
  if (MODE == 2)
  { 
    if (SELECTED == 4)
    {
      if (PAGE == 2)
      {
          lcd.setCursor(0, 3);
          lcd.print(">");
        
        
        if (enc1.isRight()) 
        {
          SELECTED = SELECTED + 1;
          CHAGE = true;
        }
        if (enc1.isLeft()) 
        {
          SELECTED = SELECTED - 1;
          CHAGE = true;
        }
        if (enc1.isClick())
        {
          MODE = 3;
          CHAGE = true;

        } 
      }
    }
  }
    if (SELECTED == 4)
    {
      if (PAGE == 2)
      {
        if (MODE == 3)
        {
            lcd.setCursor(0, 3);
            lcd.print(">");
        
        
            if (enc1.isRight()) 
            {
              twofour = twofour + 1;
              EEPROM.put(20,twofour);
              CHAGE = true;
            }
            if (enc1.isLeft()) 
            {
              twofour = twofour - 1;
              EEPROM.put(20,twofour);
              CHAGE = true;
            }
            if (enc1.isClick())
            {
              MODE = 1;
              CHAGE = true;

            } 
        }
        
      }
    }
  if (PAGE == 3)
  {
    if (MODE == 1)
    {
            lcd.setCursor(0, 0);
            lcd.print(" ");
              if (enc1.isRight()) 
              {
                PAGE = 1;
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                PAGE = 2;
                CHAGE = true;
              }
              if (enc1.isClick())
              {
                MODE = 2;
                CHAGE = true;

              }       
      
    }
    if (MODE == 2)
    {
              lcd.setCursor(0, 0);
              lcd.print(" ");
              if (enc1.isRight()) 
              {
                SELECTEDF = SELECTEDF + 1;
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                SELECTEDF = SELECTEDF - 1;
                CHAGE = true;
              }
              if (enc1.isClick())
              {
                MODE = 3;
                CHAGE = true;

              }       
      
    }

    if (SELECTEDF == 1)
    {
                  lcd.setCursor(0, 0);
            lcd.print(">");
      if (MODE == 3)
      {
              if (enc1.isRight()) 
              {
                three = three - 1;
                EEPROM.put(4,int(three));
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                three = three + 1;
                EEPROM.put(4,int(three));
                CHAGE = true;
              }
              if (enc1.isClick())
              {
                MODE = 1;
                CHAGE = true;
                digitalWrite(DOOR, HIGH);
                delay(200);
                digitalWrite(DOOR, LOW);

              }       
      }
    } 

    if (SELECTEDF == 2)
    {

                  lcd.setCursor(0, 1);
            lcd.print(">");
      if (MODE == 3)
      {
              if (enc1.isRight()) 
              {
                onetwo = onetwo + 1;
                EEPROM.put(6,int(onetwo));
                threetwo = threetwo - 1;
                EEPROM.put(10,threetwo);
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                onetwo = onetwo - 1;
                EEPROM.put(6,int(onetwo));
                threetwo = threetwo + 1;
                EEPROM.put(10,threetwo);
                CHAGE = true;
              }
              if (enc1.isClick())
              {
                MODE = 1;
                CHAGE = true;
                digitalWrite(DOOR, HIGH);
                delay(200);
                digitalWrite(DOOR, LOW);


              }       
      }
    }

    if (SELECTEDF == 3)
    {
                  lcd.setCursor(0, 2);
            lcd.print(">");
      if (MODE == 3)
      {

              if (enc1.isRight()) 
              {
                onethree = onethree + 1;
                EEPROM.put(12,onethree);
                threethree = threethree - 1;
                EEPROM.put(16,threethree);
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                onethree = onethree - 1;
                EEPROM.put(12,onethree);
               threethree = threethree + 1;
               EEPROM.put(16,threethree);
               CHAGE = true;
              }
              if (enc1.isClick())
              {
                MODE = 1;
                CHAGE = true;
                digitalWrite(DOOR, HIGH);
                delay(200);
                digitalWrite(DOOR, LOW);


              }       
      }
    }

    if (SELECTEDF == 4)
    {
                  lcd.setCursor(0, 3);
            lcd.print(">");
      if (MODE == 3)
      {

              if (enc1.isRight()) 
              {
                onefour = onefour + 1;
                EEPROM.put(18,onefour);
                threefour = threefour - 1;
                EEPROM.put(22,threefour);
                CHAGE = true;
              }
              if (enc1.isLeft()) 
              {
                onefour = onefour - 1;
                EEPROM.put(18,onefour);
                threefour = threefour + 1;
                EEPROM.put(22,threefour);
                CHAGE = true;
              }
              if (enc1.isClick())
              {
                Serial.println("eed");
                MODE = 1;
                CHAGE = true;
                Serial.println("salis");
                digitalWrite(DOOR, 1);
                delay(100);
                digitalWrite(DOOR, 0);

              }       
      }
    }
  }

  if (MODE > 3)
  {
    MODE = 0;
    CHAGE = true;
  }
  if (MODE < 0)
  {
    MODE = 3;
    CHAGE = true;
  }
  if (three > two)
  {
    three--;
    one++;
    EEPROM.put(0,int(one));
    EEPROM.put(4,int(three));
  }
  if (threetwo > twotwo)
  {
    threetwo--;
    onetwo++;
    EEPROM.put(10,threetwo);
    EEPROM.put(6,int(onetwo));

  }
  if (threethree > twothree)
  {
    threethree--;
    onethree++;
    EEPROM.put(16,threethree);
    EEPROM.put(12,onethree);

  }
  if (threefour > twofour)
  {
    threefour--;
    onefour++;
    EEPROM.put(22,threefour);
    EEPROM.put(18,onefour);

  }
  if (one < 0)
  {
    three--;
    one++;

  }
  if (onetwo < 0)
  {
    threetwo--;
    onetwo++;
    EEPROM.put(10,threetwo);
    EEPROM.put(6,int(onetwo));
  }
  if (onethree < 0)
  {
    threethree--;
    onethree++; 
    EEPROM.put(16,threethree);
    EEPROM.put(12,onethree);

  }
  if (onefour < 0)
  {
    threefour--;
    onefour++;
    EEPROM.put(22,threefour);
    EEPROM.put(18,onefour);

  }
  if (three < 0)
  {
    three++;
    one--;

  }
  if (threetwo < 0)
  {
    threetwo++;
    onetwo--;
    EEPROM.put(10,threetwo);
    EEPROM.put(6,int(onetwo));
  }
  if (threethree < 0)
  {
    threethree++;
    onethree--;
    EEPROM.put(16,threethree);
    EEPROM.put(12,onethree);
   
  }
  if (threefour < 0)
  {
    threefour++;
    onefour--;
    EEPROM.put(22,threefour);
    EEPROM.put(18,onefour);

  }
  


  if (SELCT > 4)
  {
    SELCT = 1;
    CHAGE = true;
  }
  if (SELCT < 1)
  {
    SELCT = 4;
    CHAGE = true;
  }

}



