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
