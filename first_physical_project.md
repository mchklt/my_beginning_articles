# How i made a door system unlock with card 
<img src="https://5.imimg.com/data5/FM/AE/MY-9254645/electronic-card-lock-door-access-system-500x500.jpg">


when you go to modern hoteles for reserve a chambre you gonna get a card not a key the card works like [Watch me](https://youtube.com/embed/rGLLfDZJFks)


# What is the card used in ?
The card it's a RFID Badge/Tag 

    RFID tags transmit data about an item through radio waves to the antenna/reader combination. 
   [More About RFID badges](https://www.analogictips.com/rfid-tag-and-reader-antennas/ "Read More")


RFID tag looks like 
<center><img src="https://m.media-amazon.com/images/I/71mr97JqFUL._SL1500_.jpg" width="530" height="450"></center>


RFID tag internal looks like 

<center><img src="http://www.analogictips.com/wp-content/uploads/2017/04/RFID-basics-Fig-3.jpg"></center>


**Chip**

    Tag chip contains memory which stores the product’s electronic product code and other variable information so that it can be read and tracked by RFID readers anywhere.
**Antenna**

    Reader antennas convert electrical current into electromagnetic waves that are then radiated into space where they can be received by a tag antenna and converted back to electrical current.
    
# What is RFID reader ?
<center> <b>This is a RFID reader</b> </center>
<center><img src="https://www.elecrow.com/pub/media/catalog/product/cache/f8158826193ba5faa8b862a9bd1eb9e9/1/3/13994513771_1.jpg" ></center>


**RFID** *(radiofrequency identification)*. is a technology in which identification of the products/items/objects is being done by radio frequencies (Antenna).
## How does it work ?
<center><img src="https://ibb.co/StR4jJn"></center>

**RFID reader** sends continuous radio frequencies from the device this makes the process highly simple and easy as, then after coming in a specific distance from the RFID reader, the RFID tags send the message to the RFID reader.

The Computer system it's mostly an **arduino** 
<center><Img src="https://ma.jumia.is/unsafe/fit-in/680x680/filters:fill(white)/product/95/381093/1.jpg?2626"></center>

**Arduino** is an open-source electronics platform based on easy-to-use hardware and software.

# Cooking time
right now we know how does the hotel card work, let's make it just with kitchen toolses :smirk:


<center><img src="https://www.rfidcard.com/wp-content/uploads/2019/02/RFID-has-expanded-into-a-new-field-cooking-equipment-1024x768-1024x585.jpg"></center>

### Needed tools

 - Arduino.
 - RFID + RFID tags.
 - Servo.
 - Computer (to program the arduino).




**Servo** motor is an electric device used for precise control of angular rotation
<center><img src="https://www.electronicwings.com/storage/PlatformSection/TopicContent/364/description/servo.jpg"></center>

### Let's setup our lock door system 

**the virtual setup be like** 
<center><img src="https://i.ibb.co/v4h25fT/lock-3-G0-Oa-II6-MP-removebg-preview.png"></center>

**the real setup be like**
<center><img src="https://i.ibb.co/Q8hZF7r/index.jpg"></center>

our lock door system  is ready but we need to program it 

    

> but before, i gonna do some edits for more creativity

i added some edits like buzzer (plays the role of  ring), leds and a carton (plays door role)
<center><img src="https://i.ibb.co/4KYLjpj/Eyy8-Yud-WYAES8-I0-1.jpg"></center>

**the last look of our lock door system** 
<center><img src="https://i.ibb.co/FXnHc5Y/Screenshot-from-2022-07-27-00-48-14.png"></center>

**now let's program it** 
```cpp
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>
 
#define SS_PIN 10
#define RST_PIN 9
#define LED_G 5 //define green LED pin
#define LED_R 4 //define red LED
#define BUZZER 2 //buzzer pin
MFRC522 mfrc522(SS_PIN, RST_PIN);   // Create MFRC522 instance.
Servo myServo; //define servo name
 
void setup() 
{
  Serial.begin(9600);   // Initiate a serial communication
  SPI.begin();      // Initiate  SPI bus
  mfrc522.PCD_Init();   // Initiate MFRC522
  myServo.attach(3); //servo pin
  myServo.write(0); //servo start position
  pinMode(LED_G, OUTPUT);
  pinMode(LED_R, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  noTone(BUZZER);
  Serial.println("Put your card to the reader...");
  Serial.println();

}
void loop() 
{
  // Look for new cards
  if ( ! mfrc522.PICC_IsNewCardPresent()) 
  {
    return;
  }
  // Select one of the cards
  if ( ! mfrc522.PICC_ReadCardSerial()) 
  {
    return;
  }
  //Show UID on serial monitor
  Serial.print("UID tag :");
  String content= "";
  byte letter;
  for (byte i = 0; i < mfrc522.uid.size; i++) 
  {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     content.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  Serial.println();
  Serial.print("Message : ");
  content.toUpperCase();
  if (content.substring(1) == "73 1D 22 95") //change here the UID of the card/cards that you want to give access
  {
    Serial.println("Authorized access");
    Serial.println();
    delay(500);
    digitalWrite(LED_G, HIGH);
    tone(BUZZER, 500);
    delay(100);
    noTone(BUZZER);
    myServo.write(180);
    delay(100);
    myServo.write(0);
    digitalWrite(LED_G, LOW);
  }
 
 else   {
    Serial.println(" Access denied");
    digitalWrite(LED_R, HIGH);
    tone(BUZZER, 300);
    delay(100);
    digitalWrite(LED_R, LOW);
    noTone(BUZZER);
  }
}
```

> actually before run the code i scan my rfid tag for know the
> chip code of my card
## simple explaine for the  code
the  code means if the rfid reader know the rfid tag then run the servo, turn on the blue led
else turn on the buzzer, red led .

# Demo Time
**this is my video about how it work**
- [x] White Badge
- [ ] Blue Badge

[![watch me](https://i.ibb.co/sbPJggR/Screenshot-from-2022-07-27-03-17-26.jpg)](https://streamable.com/iw7097)

\
Some times don't imagine too much
<center><img src="https://i.ibb.co/b7H8jTH/60464057-312956569630236-7569920616998219954-n-9580763662.jpg"></center>

# What does this benefit us as  red teamers ?

as well we can use it for steal informations from (compnaies employees, Hotel users...) after some researching for make it strong and can read a tag from far place we need to add some edits like **using higher gain antennas** that's mean using a high rfid readers .
[example](https://youtu.be/Qt2Gn2CoJ74)


<center><img src="https://image.slidesharecdn.com/25-sales-interview-questions-150708211925-lva1-app6891/85/25-sales-interview-questions-to-recruit-superstar-reps-64-320.jpg?cb=1436458421"></center>
