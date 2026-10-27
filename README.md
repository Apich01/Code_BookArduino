# Code_BookArduino

## Libery
### LiquidCrystal_I2C
### MQTT

<br>
## Bug เชื่อม Wifi
<img width="888" height="650" alt="image" src="https://github.com/user-attachments/assets/713ec94d-dc6a-4968-81b4-874cbc34f744" />

<br>
## สูตรแปลงค่าดิจิทัล (Raw ADC Value) ให้เป็นระดับแรงดันไฟฟ้าจริง (Voltage) ในหน่วยโวลต์ (V)
```
<br>

## LED

<img width="835" height="452" alt="image" src="https://github.com/user-attachments/assets/52ead8e7-27ce-4c60-a4e4-963e68c4e16c" />

```c
int Red_LED = 9;

void setup()
{
  pinMode(Red_LED, OUTPUT);
}

void loop()
{
  digitalWrite(Red_LED, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(Red_LED, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```
<br>

## FADING LED

<img width="1137" height="542" alt="image" src="https://github.com/user-attachments/assets/b4302eef-ea2c-40a9-abe6-e5ba09c239c0" />

```c
void setup()
{
  pinMode(3, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop()
{
  for (int fadeValue = 0; fadeValue <= 255; fadeValue += 5) {
  	analogWrite(3, fadeValue);
    delay(30);
  }
  
  for (int fadeValue = 0; fadeValue <= 255; fadeValue += 10) {
  	analogWrite(5, fadeValue);
    delay(30);
  }
  
  for (int fadeValue = 255; fadeValue >= 0; fadeValue -= 5) {
  	analogWrite(6, fadeValue);
    delay(30);
  }
  
  for (int fadeValue = 127; fadeValue <= 255; fadeValue += 5) {
  	analogWrite(9, fadeValue);
    delay(30);
  }
}
```

<br>

## KeyPad & 7Seg

<img width="336" height="477" alt="image" src="https://github.com/user-attachments/assets/3b60cfe3-976f-4f65-a714-e9d06bf71ff1" />

<img width="830" height="690" alt="image" src="https://github.com/user-attachments/assets/cd22083c-cd09-440d-bf1d-ac82e1b2a97a" />

```
int num_array[16][7] = {  { 1,1,1,1,1,1,0 },    // 0
                          { 0,1,1,0,0,0,0 },    // 1
                          { 1,1,0,1,1,0,1 },    // 2
                          { 1,1,1,1,0,0,1 },    // 3
                          { 0,1,1,0,0,1,1 },    // 4
                          { 1,0,1,1,0,1,1 },    // 5
                          { 1,0,1,1,1,1,1 },    // 6
                          { 1,1,1,0,0,0,0 },    // 7
                          { 1,1,1,1,1,1,1 },    // 8
                          { 1,1,1,0,0,1,1 },	// 9
						  { 1,1,1,0,1,1,1 }, 	//A
						  { 0,0,1,1,1,1,1 },	//B
						  { 1,0,0,1,1,1,0 },	//C
						  { 0,1,1,1,1,0,1 },	//D
						  { 0,0,0,0,0,0,1 },	//*
						  { 0,1,1,0,1,1,0 } };	//#

// Define the pins for each segment of the 7-segment display
const int segment_a = A0; 
const int segment_b = A1; 
const int segment_c = A2;
const int segment_d = A3;
const int segment_e = A4;
const int segment_f = A5;
const int segment_g = 0;

void setup() { 
  pinMode(9, INPUT_PULLUP);
  pinMode(8, INPUT_PULLUP);
  pinMode(7, INPUT_PULLUP);
  pinMode(6, INPUT_PULLUP);
  pinMode(5, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(2, OUTPUT);
  // set pin modes for each segment
  pinMode(segment_a, OUTPUT);   
  pinMode(segment_b, OUTPUT);   
  pinMode(segment_c, OUTPUT);   
  pinMode(segment_d, OUTPUT);   
  pinMode(segment_e, OUTPUT);   
  pinMode(segment_f, OUTPUT);   
  pinMode(segment_g, OUTPUT);   
}

void loop() {
  digitalWrite(5, LOW);
  digitalWrite(4, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    displayDigit(1);
  } else if (digitalRead(8) == LOW) {
    displayDigit(4);
  } else if (digitalRead(7) == LOW) {
    displayDigit(7);
  } else if (digitalRead(6) == LOW) {
    displayDigit(14);
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, LOW);
  digitalWrite(3, HIGH);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    displayDigit(2);
  } else if (digitalRead(8) == LOW) {
    displayDigit(5);
  } else if (digitalRead(7) == LOW) {
    displayDigit(8);
  } else if (digitalRead(6) == LOW) {
    displayDigit(0);
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, HIGH);
  digitalWrite(3, LOW);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    displayDigit(3);
  } else if (digitalRead(8) == LOW) {
    displayDigit(6);
  } else if (digitalRead(7) == LOW) {
    displayDigit(9);
  } else if (digitalRead(6) == LOW) {
  	displayDigit(15);
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(2, LOW);
  
  if (digitalRead(9) == LOW) {
    displayDigit(10);
  } else if (digitalRead(8) == LOW) {
    displayDigit(11);
  } else if (digitalRead(7) == LOW) {
    displayDigit(12);
  } else if (digitalRead(6) == LOW) {
    displayDigit(13);
  }
}

// Function to display a specific digit on the 7-segment display
void displayDigit(int digit) {
  // Set each segment according to the num_array for the given digit
  digitalWrite(segment_a, num_array[digit][0]);
  digitalWrite(segment_b, num_array[digit][1]);
  digitalWrite(segment_c, num_array[digit][2]);
  digitalWrite(segment_d, num_array[digit][3]);
  digitalWrite(segment_e, num_array[digit][4]);
  digitalWrite(segment_f, num_array[digit][5]);
  digitalWrite(segment_g, num_array[digit][6]);
}
```

<br>

## 7Seg

<img width="957" height="553" alt="image" src="https://github.com/user-attachments/assets/7346973b-2e46-43dd-9560-24bd8cf5dbef" />

```c
int num_array[10][7] = {  { 1,1,1,1,1,1,0 },    // 0
                          { 0,1,1,0,0,0,0 },    // 1
                          { 1,1,0,1,1,0,1 },    // 2
                          { 1,1,1,1,0,0,1 },    // 3
                          { 0,1,1,0,0,1,1 },    // 4
                          { 1,0,1,1,0,1,1 },    // 5
                          { 1,0,1,1,1,1,1 },    // 6
                          { 1,1,1,0,0,0,0 },    // 7
                          { 1,1,1,1,1,1,1 },    // 8
                          { 1,1,1,0,0,1,1 }};   // 9

// Define the pins for each segment of the 7-segment display
const int segment_a = 2; 
const int segment_b = 3; 
const int segment_c = 4;
const int segment_d = 5;
const int segment_e = 6;
const int segment_f = 7;
const int segment_g = 8;

void setup() { 
  // set pin modes for each segment
  pinMode(segment_a, OUTPUT);   
  pinMode(segment_b, OUTPUT);   
  pinMode(segment_c, OUTPUT);   
  pinMode(segment_d, OUTPUT);   
  pinMode(segment_e, OUTPUT);   
  pinMode(segment_f, OUTPUT);   
  pinMode(segment_g, OUTPUT);   
}

void loop() {
  // Loop through each digit (0-9)
  for (int digit = 0; digit < 10; digit++) {
    displayDigit(digit);
    delay(1000); // Wait for 1 second before displaying the next digit
  }
}

// Function to display a specific digit on the 7-segment display
void displayDigit(int digit) {
  // Set each segment according to the num_array for the given digit
  digitalWrite(segment_a, num_array[digit][0]);
  digitalWrite(segment_b, num_array[digit][1]);
  digitalWrite(segment_c, num_array[digit][2]);
  digitalWrite(segment_d, num_array[digit][3]);
  digitalWrite(segment_e, num_array[digit][4]);
  digitalWrite(segment_f, num_array[digit][5]);
  digitalWrite(segment_g, num_array[digit][6]);
}
```

<br>

## 2 7Seg

<img width="1037" height="562" alt="image" src="https://github.com/user-attachments/assets/d1a22c73-61eb-49a1-ba6f-ba2e526976d0" />

```c
// C++ code
//
int num_array[10][7] = {  { 1,1,1,1,1,1,0 },    // 0
                          { 0,1,1,0,0,0,0 },    // 1
                          { 1,1,0,1,1,0,1 },    // 2
                          { 1,1,1,1,0,0,1 },    // 3
                          { 0,1,1,0,0,1,1 },    // 4
                          { 1,0,1,1,0,1,1 },    // 5
                          { 1,0,1,1,1,1,1 },    // 6
                          { 1,1,1,0,0,0,0 },    // 7
                          { 1,1,1,1,1,1,1 },    // 8
                          { 1,1,1,0,0,1,1 }};   // 9

// Define the pins for each segment of the 7-segment display
const int segment_a = 2; 
const int segment_b = 3; 
const int segment_c = 4;
const int segment_d = 5;
const int segment_e = 6;
const int segment_f = 7;
const int segment_g = 8;

void setup() { 
  // set pin modes for each segment
  pinMode(segment_a, OUTPUT);   
  pinMode(segment_b, OUTPUT);   
  pinMode(segment_c, OUTPUT);   
  pinMode(segment_d, OUTPUT);   
  pinMode(segment_e, OUTPUT);   
  pinMode(segment_f, OUTPUT);   
  pinMode(segment_g, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
}

void loop() {
  // Loop through each digit (0-9)
  int list_left[4] = {6, 0, 0, 0};
  int list_right[4] = {8, 7, 2, 2};
  
  for (int digit = 0; digit < 4; digit++) {
    for (int i=0; i<10; i++) {
    	displayDigit(list_left[digit]);
      	digitalWrite(12, LOW);
      	digitalWrite(13, HIGH);
      	delay(50);
      
      	displayDigit(list_right[digit]);
      	digitalWrite(12, HIGH);
      	digitalWrite(13, LOW);
    	delay(50);
    }
  }
}

// Function to display a specific digit on the 7-segment display
void displayDigit(int digit) {
  // Set each segment according to the num_array for the given digit
  digitalWrite(segment_a, num_array[digit][0]);
  digitalWrite(segment_b, num_array[digit][1]);
  digitalWrite(segment_c, num_array[digit][2]);
  digitalWrite(segment_d, num_array[digit][3]);
  digitalWrite(segment_e, num_array[digit][4]);
  digitalWrite(segment_f, num_array[digit][5]);
  digitalWrite(segment_g, num_array[digit][6]);
}
```

<br>

## RGB

<img width="1168" height="547" alt="image" src="https://github.com/user-attachments/assets/b06836e6-4144-4a1e-b3db-d186e185f139" >

```c
void setup()
{
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
}

void loop()
{
  digitalWrite(9, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(9, HIGH);
  delay(0); // Wait for 1000 millisecond(s
  
  
  digitalWrite(10, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(10, HIGH);
  delay(0); // Wait for 1000 millisecond(s)
  
  digitalWrite(11, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(11, HIGH);
  delay(0); // Wait for 1000 millisecond(s)
}
```

<br>

## Ultrasonic Sensor

<img width="985" height="706" alt="image" src="https://github.com/user-attachments/assets/14308e38-bd99-48cb-8502-e47305791e5b" />

```c
// C++ code
//
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup()
{
 pinMode(9, OUTPUT); //Trig
 pinMode(8, INPUT); //Echo
  
 lcd.init();
 lcd.backlight();
}
void loop()
{
 digitalWrite(9, HIGH);
 delayMicroseconds(10);
 digitalWrite(9, LOW);

 int pulseWidth = pulseIn(8, HIGH);
 double distance = pulseWidth/29.0/2.0;
 lcd.setCursor(0, 0);
 lcd.print("D: ");
 lcd.print(distance, 1);
 lcd.print(" cm   ");

 delay(500);
}
```

<br>

## Temperature Sensor && Serial

<img width="998" height="708" alt="image" src="https://github.com/user-attachments/assets/29ace6b8-9e3b-4a0a-86ec-9076224fc316" />

```c
void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600);
}

void loop()
{
  
  //double temp = (analogRead(A1)-500)/10;
  double volt = (analogRead(A1) / 1023.0) * 5.0; 
  double temp = (volt-0.5)/0.01;
  int solid = (analogRead(A0)/876.0)*100;
  Serial.print("Temp: ");
  Serial.print(temp);
  Serial.print(" C | Solid: ");
  Serial.print(solid);
  Serial.println("%");
  
  delay(1000);
}
```

<br>

## KeyPad & LCD

<img width="720" height="677" alt="image" src="https://github.com/user-attachments/assets/9023bf00-1721-4642-9ad3-8f636fd6a5c2" />

```c
// C++ code
//
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);
byte newChar1[8] = {
  B00000,
  B00000,
  B10001,
  B01010,
  B11111,
  B01010,
  B10001,
  B00000 };

byte newChar2[8] = {
  B00101,
  B01010,
  B11111,
  B01010,
  B11111,
  B01010,
  B10100,
  B00000 };

void setup()
{
  pinMode(9, INPUT_PULLUP);
  pinMode(8, INPUT_PULLUP);
  pinMode(7, INPUT_PULLUP);
  pinMode(6, INPUT_PULLUP);
  pinMode(5, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(2, OUTPUT);
  
  lcd.init();
  lcd.backlight();
  
  lcd.createChar(1, newChar1);
  lcd.createChar(2, newChar2);
  
  lcd.setCursor(1, 0);
}

void loop()
{
  bool keyPressed = false;

  digitalWrite(5, LOW);
  digitalWrite(4, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("1");
    keyPressed = true;
  } else if (digitalRead(8) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("4");
    keyPressed = true;
  } else if (digitalRead(7) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("7");
    keyPressed = true;
  } else if (digitalRead(6) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.write(byte(1));
    keyPressed = true;
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, LOW);
  digitalWrite(3, HIGH);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("2");
    keyPressed = true;
  } else if (digitalRead(8) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("5");
    keyPressed = true;
  } else if (digitalRead(7) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("8");
    keyPressed = true;
  } else if (digitalRead(6) == LOW) {
   	lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("0");
    keyPressed = true;
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, HIGH);
  digitalWrite(3, LOW);
  digitalWrite(2, HIGH);
  
  if (digitalRead(9) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("3");
    keyPressed = true;
  } else if (digitalRead(8) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("6");
    keyPressed = true;
  } else if (digitalRead(7) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("9");
    keyPressed = true;
  } else if (digitalRead(6) == LOW) {
  	lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.write(byte(2));
    keyPressed = true;
  }
  
  digitalWrite(5, HIGH);
  digitalWrite(4, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(2, LOW);
  
  if (digitalRead(9) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("A");
    keyPressed = true;
  } else if (digitalRead(8) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("B");
    keyPressed = true;
  } else if (digitalRead(7) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("C");
    keyPressed = true;
  } else if (digitalRead(6) == LOW) {
    lcd.clear();
  	lcd.setCursor(1, 0);
    lcd.print("D");
    keyPressed = true;
  }
  if (keyPressed) {
    delay(250);
  }
}
```

<br>

## Potentiometer

<img width="950" height="421" alt="image" src="https://github.com/user-attachments/assets/67dd4499-b0a3-4a3d-aad7-f18a640c174c" />

```c
void setup()
{
  Serial.begin(9600);
}

void loop()
{
  int value = analogRead(A0);
  delay(1000);
  Serial.println(value);
}
```

<br>

## Thermistor Sensor

<img width="1272" height="575" alt="image" src="https://github.com/user-attachments/assets/958a02eb-903e-4f3e-9948-55a70f1f6873" />

```c
void setup()
{
  Serial.begin(9600);
}

void loop()
{
  int value1 = analogRead(A1);
  float r = 10000.0 * value1 / (1023.0 - value1);
  float temp = 1.0 / (log(r / 10000.0) / 3950.0 + 1.0 / 298.15) - 273.15;
  Serial.println(temp);
}
```

## BUTTON

<br>

<img width="887" height="670" alt="image" src="https://github.com/user-attachments/assets/b2a753dc-c1a5-4cd5-8c74-427e9ddecdc6" />

<br>

<img width="907" height="652" alt="image" src="https://github.com/user-attachments/assets/094f7e15-6b78-4f77-8e02-990b420c9dfa" />

<br>

<img width="863" height="653" alt="image" src="https://github.com/user-attachments/assets/07266dda-426b-4c35-8cf3-e5f4a90ea745" />

<br>

<img width="887" height="672" alt="image" src="https://github.com/user-attachments/assets/137ae4a8-3b05-45c8-84f3-51341ba7c96e" />




