# Code_BookArduino

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

