1. 연구배경 및 필요성(중요성)

저희는 일상생활에서 스탠드를 사용하는 상황에서 밝기를 조절할 때 수동으로 해왔습니다.          
그동안 어두운 곳에서 공부 하거나 독서를 할 때 스탠드를 켜서 공부 하는 상황에서 밝기가 맞지 않아서 눈이 빨리 피로 해진 적이 있었나요?  
저희 조는 그런 경험을 많이 했습니다.  
이런 단점 뿐 아니라 전기세를 조금이라도 더 절약하기 위해서 만들기로 결심했습니다.  
만약 이 제품이 만들어지게 된다면 이러한 단점들을 보완 할 수 있을거라 생각합니다. 

2. 관련기술의 현황  
요즘에 쓰는 스마트폰들은 저절로 밝기 조절이 되는걸로 알고 있습니다.  

3. 기대효과 및 활용  
- 전기세 절감  
- 눈의 피로를 줄여줌    
- 자동으로 알맞은 밝기로 조절해줌으로 편리함  

4. 목표
그동안 어두운 곳에서 공부 하거나 독서를 할 때 스탠드를 켜서 공부 하는 상황에서 밝기가 맞지 않아서 눈이 빨리 피로 해진 적이 있었다.   
 우리 조는 그런 경험을 많이 했었다. 이런 단점 뿐 아니라 전기세를 조금이라도 더 절약하기 위해서 만들기로 결심했다.

- 밝기 조절 센서의 개발  
- 스탠드 개발  
- 밝기 알고리즘 개발  

5. 구현 방법  
(1) 구현방법  
- 자동 밝기 시스템의 개념설계를 한다.
- 각자 문제해결을 위한 자료를 수집하고 분석한다.
- 분석한 자료를 발표하고 지도 교수와 토론을 한다.
- 각 문제의 해결방법을 하나로 결정하고 이것에 대해 문제를 해결한다.
- 상세설계를 하고 제품을 제작한다
- 특성실험을 실시한다. 
- 보고서를 작성한다.

(2) 추진체계


![image](https://github.com/user-attachments/assets/a9a261bd-d69b-4cc6-ac95-39fee2fd51e1)


7.진행과정  

![image](https://github.com/user-attachments/assets/d3b437f6-7a33-423d-93e2-22df3fcd414e)

==> 밝은 환경 --> 스탠드 불이 안 켜짐
빨간줄을 5v에 꼽고, 검정줄은 GND에 꼽고, 노란줄은 A0에 꼽음

![image](https://github.com/user-attachments/assets/c8f02dea-ccf0-41be-8500-4653b1361efb)

==> 어두운 환경 --> 스탠드가 밝기가 높아짐


![20241128_151310](https://github.com/user-attachments/assets/9b9b1d5f-0071-429d-a8be-4aecada02b1c)
LED전구를 활용하여 밝은 곳에서의 LED의 밝기 조절


![20241128_151314](https://github.com/user-attachments/assets/88c7178c-37e3-4eef-bcbe-805b1685eb10)
LED전구를 활용하여 어두운 곳에서의 LED의 밝기 조절


-LED전구 자동 밝기 조절 코드

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

void setup() 
{  
    Serial.begin(115200); // 시리얼 통신 시작  
    pinMode(LED, OUTPUT); // LED 핀을 출력 모드로 설정  
    pixels.begin();  
}  
  
void loop() 
{  
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


 **제품 완성**


![image](https://github.com/user-attachments/assets/c8ca63e0-58ea-4da7-a0fa-12a56a330667)

주변 밝기가 어두울때의 스탠드 밝기




![불킨거](https://github.com/user-attachments/assets/09473f88-1978-4d01-acd2-e9db48addd9f)

주변 밝기가 밝을때의 스탠드 밝기





**발표 대본 추가**

발표 대본: 스마트 스탠드 개발 프로젝트
1. 소개 (1분)
안녕하세요. 저희는 팀 11입니다. 발표를 맡은 고은석입니다.
오늘 저희가 소개할 주제는 **"스마트 스탠드: 눈 건강과 작업 효율을 위한 혁신"**입니다.

스마트 스탠드는 현대인의 작업 환경에서 조명의 중요성을 고려해 개발한 제품입니다.
잘못된 조명이 눈 건강과 작업 효율에 부정적인 영향을 미칠 수 있다는 점에 착안해, 
저희는 자동으로 주변 밝기에 맞게 조절되는 스탠드를 설계했습니다.

2. 프로젝트 목표 (1분)
저희 프로젝트의 목표는 세 가지로 요약할 수 있습니다.

눈 건강 보호: 최적화된 조도로 눈의 피로를 줄이고 건강을 지킵니다.
에너지 절약: 필요한 만큼만 조명을 사용해 전력 소비를 줄입니다.
사용자 편의성: 자동 조절 기능으로 사용자의 개입을 최소화합니다.


3. 개발 과정 (3분)
저희는 다섯 단계에 걸쳐 프로젝트를 진행했습니다.

요구 사항 분석: 사용자의 필요와 원하는 기능을 조사했습니다.
기술 조사: 조도 센서와 LED 기술을 연구해 활용 방안을 찾았습니다.
설계: 하드웨어와 소프트웨어 설계를 진행했습니다.
제작: 프로토타입을 제작하고 다양한 테스트를 거쳤습니다.
피드백 및 개선: 사용자 테스트를 통해 부족한 점을 보완했습니다.



4. 기술적 구현 (2분)
스마트 스탠드의 기술적 구현을 살펴보겠습니다.

하드웨어 구성: 조도 센서, LED 조명, 마이크로컨트롤러를 사용했습니다.
소프트웨어: 센서 데이터를 수집하고 밝기를 조절하는 알고리즘을 설계했습니다.


5. 테스트 결과 (2분)
저희는 다양한 환경에서 성능을 테스트했고, 사용자들의 만족도를 조사했습니다.

성능 테스트 결과, 다양한 조명 환경에서도 안정적으로 작동했습니다.
팀원들과 사용자들 모두 높은 만족도를 보였습니다.


6. 향후 계획 (1분)
저희는 이 제품을 더욱 발전시키기 위해 다음과 같은 계획을 세웠습니다.

스마트폰 연동: 모바일 앱을 통해 원격으로 제어할 수 있도록 개선하겠습니다.
사용자 선호도 학습: 머신러닝을 적용해 개인화된 조명 환경을 제공합니다.
에너지 절약 최적화: 더욱 효율적인 전력 소비 방안을 연구하겠습니다.


7. 결론 (1분)
마지막으로, 스마트 스탠드가 가져올 변화는 다음과 같습니다.

눈 건강 증진: 눈의 피로를 줄이고 건강을 보호합니다.
작업 효율성 향상: 최적화된 조명 환경으로 집중력과 생산성이 증가합니다.+
에너지 절약: 스마트한 조명 사용으로 전력 소비를 줄입니다.
이상으로 발표를 마치겠습니다. 감사합니다. 질문 있으시면 받겠습니다.



