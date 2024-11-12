## 0. Specification
<img src='https://www.commanderk.site/assets/readme/1-1.jpeg' width="450px" height="250px">

### Electrical Characteristics
---
| Parameter | Min | Typ | Max | Unit |
| --- | --- | --- | --- | --- |
| Supply Voltage | 4.5 | 12 | 28 | V |
| Power Consumption | - | - | - | W |
| DIN input voltage | - | - | 50 | V |
| AIN input voltage | - | - | Specified by resistors in ANALOG section | V |

ESP32 C타입 USB단자나, MCU의 8핀 USB단자를 통해 데이터 로거 전체에 전원을 공급 가능.단, USB 단자로 전원 공급 중 장비가 오동작한다면, 전류가 부족한 것이니 VIN 단자를 통해 Power Supply로 전원을 공급해야 합니다.

### Mechanical Characteristics
<img src='https://www.commanderk.site/assets/readme/7-2.png' width="475px" height="250px">  

<img src='https://www.commanderk.site/assets/readme/7-3.png' width="475px" height="250px">  

<img src='https://www.commanderk.site/assets/readme/7-4.png' width="225px" height="200px">  


## 1. 기능

### 1-1. SD카드 로그 저장

STM32F4 개발보드 상단의 SD 카드 슬롯을 사용하여, Micro SD 카드에 모든 로그를 기록함.

<img src='https://www.commanderk.site/assets/readme/7-5.jpeg' width="275px" height="225px">

SD 카드를 정상적으로 인식한 경우 SD_LED가 켜지며, SD카드가 분리되거나 고장난 경우 꺼집니다.

[로그 프로토콜](https://github.com/commanderk9826/KDL-distribution/wiki/로그-프로토콜)에 따라 바이너리 형식으로 로그를 사람이 읽을 수 있는 파일로 변환하려면 [데이터 분석 도구 가이드](https://github.com/commanderk9826/KDL-distribution/wiki/데이터-분석-도구-가이드)를 참고하세요.

- RTC 시간 동기화를 최소 1회 먼저 하고 장비를 재부팅해야 로그 파일 이름이 실제 시간으로 제대로 저장됩니다.
- 로그 파일 이름은YYYY-MM-DD-HH-mm-ss.log 형식으로 정해지며, 데이터 분석 도구가 로그 발생 시각을 계산하는데 사용하므로 변경해서는 안됩니다.

### 1-2. RTC 실제 시간 추적

데이터로거는 RTC(Real-Time Clock)을 이용하여 전원이 꺼져도 실제 시간 정보를 계속 저장합니다.

STM32 개발보드에 있는 작은 코인 배터리가 RTC 시계의 배터리로, 배터리를 제거하면 시간이 2023년 5월 12일 00시 00분 00초로 초기화됩니다.

RTC 유닛은 두 가지 방법으로 실제 시간과 동기화할 수 있습니다.

- 텔레메트리 기능을 사용하는 경우 중계 서버와 연결되면 자동으로 서버 시간으로 동기화됩니다.
- 텔레메트리 기능을 사용하지 않는 경우, STM32CUBEIDE를 이용해, 컴퓨터의 시스템 시간과 동기화할 수 있습니다.

### 1-3. 텔레메트리

데이터로거가 기록한 로그를 실시간으로 무선 전송하여 원격에서 모니터링할 수 있는 기능입니다.

드라이버가 가지고 탑승한 스마트폰의 핫스팟 네트워크를 통해 인터넷에 연결하여 로그를 중계 서버로 전송함.

데이터 로거가 웹 서버와 연결되면 보드의 TELEMETRY_LED가 켜지고, 연결이 끊기면 꺼짐. 부팅 직후 STM32와 ESP32가 통신 초기화에 성공하면 LED가 빠르게 3회 점멸함.

- 네트워크 문제로 실시간 모니터링이 끊겨도 모든 로그는 손실 없이 SD 카드에 저장됨.
- 삼성 스마트폰 핫스팟과 가장 호환성이 좋음.

### 1-4. 로그 출력(UART/I2C)

데이터로거가 수집한 로그를 차량에 탑재된 다른 MCU가 사용할 수 있도록 다시 출력하는 기능.

#### 1-4-1. UART
---
Main I/O 커넥터의 U_TX, U_RX 핀을 통해 115200bps 3.3V UART로 로그를 출력함.

출력되는 로그는 헤더 2 byte(0x05, 0x12)가 기존 16 byte의 [로그 프로토콜](https://github.com/commanderk9826/KDL-distribution/wiki/로그-프로토콜) 앞에 붙은 18 byte 규격.

사용하지 않는다면 비활성화해야 성능 이득을 볼 수 있음.

- 이론상 최대로 전송 가능한 로그는 초당 640개.

#### 1-4-2. I2C
---
STM32는 I2C 통신을 통해 ESP32로 수집한 로그를 전달함. 이 때, I2C General Call Address인 0x0 으로 로그를 전송함.

따라서, I2C 버스에 General Call 수신 기능이 구현된 다른 노드를 연결하면 로그 패킷을 수신할 수 있음.

- 텔레메트리 기능을 사용하고, ESP32가 서버에 연결되었을 때만 로그가 I2C 포트로 출력됨.
- Main I/O 커넥터의 SDA, SCL 핀을 통해 수신할 수 있으며, I2C 특성상 먼 거리는 전송불가능.

### 1-5. CAN 트래픽 모니터링

CAN 통신 버스의 모든 트래픽을 모니터링함. 125 kbit/s, 250 kbit/s, 500 kbit/s, 1 Mbit/s 의 CAN baud rate를 지원함.

- CAN 버스 에러를 감지하면 보드의 CAN_LED가 꺼짐.
- STM32CUBE IDE에서 CAN baud rate를 설정할 수 있음.

#### 1-5-1. CAN Message
---
CAN 2.0A(standard)는 11개, CAN 2.0B(extended format)는 29개 비트를 사용하여 CAN 메시지 ID를 표현함.

한편, 데이터 로거는 로그 프로토콜규격상 CAN ID를 저장하는 key 필드에 8개 비트만 사용할 수 있음.

따라서, 모든 CAN 메시지는 ID의 하위 8개 비트만 로그에 key 값으로 기록됨.

즉, 0b1111 0000(0xF0)과0b110 1111 0000(0x6F0)은 로그에서 동일한 메시지 ID로 취급되며, 로그의 key 필드에 0xF0 이 저장됨.

#### 1-5-2. 종단 저항
---
CAN 버스에는 버스 양 끝단에 120Ω 종단 저항이 하나씩, 총 2개 존재해야 합니다.

데이터로거의 CAN 트랜시버에는 기본적으로 120Ω 저항이 장착되어 있습니다. 차량 설계 시 이를 고려하여 CAN 버스를 구성해야 합니다.

다른 장비에 이미 종단 저항이 2개 있다면, 트랜시버의 120Ω 종단저항은 제거함.

### 1-6. 디지털 신호

2개의 DIN 채널의 디지털 HIGH/LOW를 기록하는 기능임. 0V면 LOW, 1V 이상이 입력되면 HIGH로 인식함. 50V까지 입력할 수 있음.

- 100ms마다 기록됨.

### 1-7. 아날로그 신호

2개의 AIN 채널을 통해 아날로그 전압을 기능임. ANALOG 영역의 전압 분배 회로를 거쳐 STM32의 3.3V ADC에 입력되므로, 전압 분배 저항을 적절히 설정하면 다양한 아날로그 전압을 입력받을 수 있습니다.

- 100ms마다 기록됨.

### 1-8. 3축 가속도

3축 가속도를 100ms마다 측정하고 기록함. 측정 범위는 ±4g임.

### 1-9. GPS 위치 정보

GPS 위치 정보를 100ms마다 수신하고 기록함. GPS 모듈로부터 수신한 NMEA GPRMC 메시지를 해석하여 위치 정보를 기록함.

### 1-10. 전원 전압 / CPU 온도

1s마다 전원 전압과 STM32F4 코어 온도를 기록합니다. 기본기능으로 비활성화할 수 없음. 데이터로거의 최대 공급 전압은 28V이나, 26.4V를 초과하는 전원 전압은 26.4V로 기록됨.

## 2. 커넥터

### 2-1. Main I/O 커넥터(J1)

- Model: 5569-12A
- Mate: 5557-12R
- Mate Terminal: 5556T

<img src='https://www.commanderk.site/assets/readme/7-6.png' width="150px" height="175px">

<img src='https://www.commanderk.site/assets/readme/7-7.png' width="150px" height="75px">

| VBUS | DIN0 | AIN0 | U_TX(F407_PC6) | SDA(F407_PB7) | CANH |
| --- | --- | --- | --- | --- | --- |
| 1 | 2 | 3 | 4 | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 |
| GND | DIN1 | AIN1 | U_RX(F407_PC7) | SCL(F407_PB6) | CANL |

### 2-2. DEBUG UART Header(J2)

- Connector: SMW200-03(커넥터 3핀)
- Terminal: YST200

<img src='https://www.commanderk.site/assets/readme/7-8.png' width="150px" height="120px">

<img src='https://www.commanderk.site/assets/readme/7-9.png' width="75px" height="100px">

| 1 | U_TX_DEBUG(F407_PA9) |
| --- | --- |
| 2 | U_RX_DEBUG(F407_PA10) |
| 3 | GND |

>UART로 로그출력

### 2-3. I/O 커넥터(J3)

- Connector: B4B-XH-A(커넥터 4핀)
- Terminal: SXH-001T-P0.6N

<img src='https://www.commanderk.site/assets/readme/7-10.png' width="150px" height="80px">

<img src='https://www.commanderk.site/assets/readme/7-11.png' width="75px" height="100px">

| 1 | IO1(F407_PD2) |
| --- | --- |
| 2 | IO2(F407_PD3) |
| 3 | IO3(F407_PD4) |
| 4 | IO4(F407_PD5) |

>필요 시 사용하는 여분 STM I/O핀(현재 미사용 통신 채널을 더 뚫는 등의 경우에 사용).

### 2-4. CAN SUPPLY I/O(J4)

- Connector: SMW200-02(커넥터 2핀)
- Terminal: YST200

<img src='https://www.commanderk.site/assets/readme/7-12.png' width="150px" height="90px">

<img src='https://www.commanderk.site/assets/readme/7-13.jpeg' width="75px" height="100px">

| 1 | 5V |
| --- | --- |
| 2 | GND |

>CAN 5V 공급용