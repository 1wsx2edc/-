#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
 #include <avr/power.h> // Required for 16 MHz Adafruit Trinket
#endif
#define LED 13 // LED 핀 정의
#define PIN        7
#define NUMPIXELS 8
#define LIGHT_SENSOR_PIN A0 // 조도 센서 핀 정의

// 센서 값의 범위 설정 (최대값과 최소값)
#define MAX_SENSOR_VAL 1023 // 아날로그 센서의 최대 값 (1023)
#define MIN_SENSOR_VAL 0 // 아날로그 센서의 최소 값 (0)

Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
    Serial.begin(115200); // 시리얼 통신 시작
    pinMode(LED, OUTPUT); // LED 핀을 출력 모드로 설정
    pixels.begin();
}

void loop() {
    // 아날로그 센서 값 읽기 (0 ~ 1023 범위)
    int sensorValue = analogRead(LIGHT_SENSOR_PIN);

    // 어두운 곳에서는 밝아지도록 매핑: 0은 가장 어두운 곳(밝게), 1023은 가장 밝은 곳(어둡게)
    int brightness = map(sensorValue, MIN_SENSOR_VAL, MAX_SENSOR_VAL, 255, 0); // 어두우면 밝고, 밝으면 어두운 값으로 매핑

    // 센서 값 및 밝기 값을 시리얼 모니터에 출력 (디버깅 용)
    Serial.print("Sensor Value: ");
    Serial.print(sensorValue);
    Serial.print("\tBrightness: ");
    Serial.println(brightness);

    // LED 밝기 조절
    control_brightness(brightness);
    
    delay(100); // 잠시 대기 (0.1초)
    
}

void control_brightness(int light)
{
  for(int i=0; i<NUMPIXELS; i++)
  { 
    pixels.setPixelColor(i, pixels.Color(light, light, light));
    pixels.show();   
  }
}

void turn0ff()
{
  for(int i=0; i<NUMPIXELS; i++)
  { 
    pixels.setPixelColor(i, pixels.Color(0, 0, 0));
    pixels.show();   
  }
}
