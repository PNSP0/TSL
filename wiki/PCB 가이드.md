## 설계도

### 1. PCB
[hardware(KDL).zip](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/hardware(KDL).zip)

## 제작

[gerber.zip](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/gerber.zip)

PCB 업체에 샘플 PCB를 주문합니다.

[JLPCB](https://jlcpcb.com/)에서 거버 파일을 업로드하면 자동으로 견적이 나오고 온라인으로 주문이 가능합니다.

>참고) 최소5장 단위로 구매 가능하고, PCB 색상만 골라서 주문하면 됨.

## 기판 둘러보기
<img src='https://www.commanderk.site/assets/readme/6-1.png' width="475px" height="250px">  

<img src='https://www.commanderk.site/assets/readme/6-2.png' width="475px" height="250px">  

### 2. BOM (Bill of Materials)

데이터로거 기판에 사용되는 부품 목록입니다.

#### 2-0. BOM 리스트

필요한 모든 부품들을 담아놓은 BOM 리스트입니다.

- 표시된 수량은 제작에 필요한 최소 수량입니다.
- BOM list
    
    [eleparts.xls](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/eleparts.xls)
    
    [devicemart.xlsx](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/devicemart.xlsx)
    
---
| 항목 | 판매처 | 링크 |
| --- | --- | --- |
| PCB | JLPCB | https://jlcpcb.com |
| Cortex-M4 STM32F407VET6 | Aliexpress | https://ko.aliexpress.com/item/4000311704641.html?spm=a2g0o.order_list.order_list_main.20.2449140fZApjZx&gatewayAdapt=glo2kor |
| 여러부품 | 엘레파츠 | [eleparts.xls](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/eleparts.xls) |
| 여러부품 | 디바이스마트 | [devicemart.xlsx](https://github.com/commanderk9826/KDL-distribution/blob/main/device/hardware/devicemart.xlsx) |
| 아두이노 3A 강하형 MP1584EN 초소형 DC-DC 스텝 다운 가변 모듈 | 알파마이크로 | https://smartstore.naver.com/misoparts/products/5356716694 |

#### 2-1. 필수부품
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| PCB | - | 1 | JLPCB |  |
| Cortex-M4 STM32F407VET6 | U5 | 1 | Aliexpress |  |
| 아두이노 3A 강하형 MP1584EN 초소형 DC-DC 스텝 다운 가변 모듈 | U1 | 1 | 알파마이크로 | 3.3V 고정이 아닌 가변 타입입니다. 가변저항 돌리면서 멀티미터로 3.3V 맞춰 놓고 사용하면 됩니다. |
| 5569-12A | J1 | 1 | 디바이스마트 |  |
| 5557-12R | - | 1 | 디바이스마트 |  |
| 5556T | - | 30 | 디바이스마트 | 5557용 클림프 |
| 확산형 5mm 고휘도 LED | D1-D6 | 6 | 디바이스마트 | 색깔은 취향에 맞게 골라 저항값만 맞춰 사용하면 됩니다.(100Ω or 220Ω ) ⇒ 추천 : 노랑 1, 초록 1, 빨강2, 파랑 2 |
| RES SMD 100 OHM 1% 1/4W 1206(CRCW1206100RFKEA) | R7-R12 | 6 | 디바이스마트 | D1-D6 LED 공급 전압은 3.3V입니다.LED 색깔별 전압강하에 맞게 적절한 저항값을 선정합니다. [LED res Calc](https://www.digikey.kr/ko/resources/conversion-calculators/conversion-calculator-led-series-resistor) / 대략 100 ~ 330Ω 박으면 됩니다. R7(PWR), R8(ERR), R9(HEARTBEAT), R10(SD), R11(CAN), R12(TELEMETRY)  |
| B4B-XH-A | J3 | 1 | 디바이스마트 | 커넥터4핀 |
| SXH-001T-P0.6N | - | 40 | 디바이스마트 | B4B-XH-A용 클림프 |
| SMW200-02 | J4 | 1 | 디바이스마트 | 커넥터2핀 |
| SMW200-03 | J2 | 1 | 디바이스마트 | 커넥터3핀 |
| YST200 | - | 50 | 엘레파츠 | SMW200용 클림프 |
| CAP TANT 0.1UF 35V 10% 1206(293D104X9035A2TE3) | C2-C5 | 4 | 디바이스마트 | I/O Connector용 RC필터 |
| FHO1(2.54)-DS80P(2열 80핀) | - | 2 | 엘레파츠 | 개발보드가 2열48핀이므로 2개를 구매해서 잘라서 사용합니다. |
| FH01(2.54)-SS40P(1열 40핀) | - | 1 | 엘레파츠 | 개발보드가 4핀*1이므로 잘라서 사용합니다. |
| PH01(2.54)-SS40P-11.5MM(1열 40핀 핀헤더) | - | 2 | 엘레파츠 | ESP32(19핀*2), MP1584EN 3.3V DC-DC 컨버터(2핀*4), ADXL345 가속도센서 모듈(SZH-EK054 5핀*2), NEO-7M GPS 모듈(4핀*1) |
| RES SMD 9.1K OHM 1% 1/4W 1206(CRCW12069K10FKEA) | R1 | 1 | 디바이스마트 |  |
| RES SMD 1.3K OHM 1% 1/4W 1206(CRCW12061K30FKEA) | R2 | 1 | 디바이스마트 |  |

>아두이노 3A 강하형 MP1584EN 초소형 DC-DC 스텝 다운 가변 모듈는 장착 방향에 유의해야 합니다. 페이지 상단 완성품 이미지를 보고 방향을 잘 맞춰 가장 큰 정사각형 부품이 좌측 하단에 오도록 장착합니다.

>STM32 개발보드 또한 SD카드 슬롯이 위쪽을 향하도록 장착합니다.

#### 2-2. Telemetry 영역
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| NodeMCU-32S Lua WiFi - ESP32 개발보드(USB-C)  | U4 | 1 | 엘레파츠 | 기왕 사는거 C타입으로 구매합니다.알리에서는 ESP32 CP2102 TYPE-C 옵션을 선택해야 합니다.PCB 모서리에 마운팅 홀이 없는 제품입니다.ESP32-devkit 등 비슷한 제품이 많으니 주의합니다. |
| RES SMD 2.7K OHM 5% 1/4W 1206(CRCW12062K70JNEA) | R17, R18 | 2 | 디바이스마트 |  |
| CAP TANT 10UF 10% 16V 1206(293D106X9016A2TE3) | C1 | 1 | 디바이스마트 | 보드 장착 시 EN 버튼을 누르지 않고 업로드가 가능하게 해주는 커패시터입니다. |

>ESP32 개발보드는 USB 단자가 위쪽을 향하도록 방향에 유의하여 장착합니다. `C1` 커패시터 또한 datasheet를 참고하여 극성에 유의합니다.

#### 2-3. CAN 영역
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| SN65HVD1050DR CAN Transceiver 모듈 | U7 | 1 | 디바이스마트 | datasheet상 TXD가 오른쪽 하단 |
| CFS-0102MB(스위치) | S1 | 1 | 디바이스마트 |  |
| CDSOT23-T24(다이오드)  | CR1 | 1 | 디바이스마트 |  |
| CAP TANT 0.1UF 35V 10% 1206 (293D104X9035A2TE3) | C6 | 1 | 디바이스마트 | CAN Transceiver용 RC필터 |
| RES SMD 120 OHM 1% 1/4W 1206(CRCW1206120RFKEA) | R21 | 1 | 디바이스마트 |  |

CAN 트랜시버는 칩셋이 있는 쪽이 기판 아랫면을 향하도록 장착합니다. 

#### 2-4. DIGITAL 영역
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| 2N3904 범용 NPN 트랜지스터 | Q1, Q2 | 2 | 엘레파츠 | 핀 피치가 1.27mm이 아니라 2.54mm인 Wide TO-92 풋프린트입니다. |
| RES SMD 1K OHM 1% 1/4W 1206 (CRCW12061K00FKEA) | R3-R6 | 4 | 디바이스마트 |  |

#### 2-5. ANALOG 영역(직접 자신의 차량에 맞게 저항값을 계산하여 장착합니다)
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| RES SMD 470 OHM 1% 1/4W 1206 (CRCW1206470RFKEA) | R13, R15 | 2 | 디바이스마트 |  |
| RES SMD 910 OHM 1% 1/4W 1206 (CRCW1206910RFKEA)  | R14, R16 | 2 | 디바이스마트 |  |

>STM32의 ADC 최대 입력 전압은 3.3V으로, 입력할 신호의 전압에 따라 적절한 저항값을 선정해야합니다.5V 아날로그 신호를 입력하는 경우 홀수 번호 저항에 470Ω, 짝수 번호 저항에 910Ω을 사용합니다.다른 전압을 사용하는 경우, 최대 전압이 3.3V가 되도록 저항값을 계산합니다.

>`최대 입력 전압 * (짝수 번호 저항값) / (홀수 번호 저항값 + 짝수 번호 저항값) = 3.3` 이 되도록 하면 됩니다.

#### 2-6. ACCELEROMETER 영역
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| ADXL345 가속도센서 모듈[SZH-EK054] | U6 | 1 | 디바이스마트 | 길쭉하고 양쪽에 핀이 달린 모듈을 사야 합니다. 한쪽에만 6-8개의 핀이 있는 GY-291과 헷갈리지 않도록 주의합니다. |
| RES SMD 2.7K OHM 5% 1/4W 1206 (CRCW12062K70JNEA) | R19, R20 | 2 | 디바이스마트 |  |

>가속도 센서는 기판에 적힌 핀 이름과 센서에 적힌 핀 이름이 일치하도록 방향에 유의하여 장착합니다.

#### 2-7. GPS 영역
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| NEO-7M GPS 모듈 | U2 | 1 | 디바이스마트 | 모듈 아랫면에 안테나가 부착된 제품은 사용할 수 없습니다. 기본 제공되는 외장 안테나는 사용하지 않습니다. |
| GNSS/GPS 안테나 1M(외장/SMA/차량용)[SZH-GANT01] | - | 1 | 디바이스마트 | 모듈의 기본 안테나 대신 사용하는 외장 안테나입니다. |
| SMA to uFL/u.FL/IPX/IPEX RF Adapter Cable [ada-851] | - | 1 | 디바이스마트 | 모듈의 기본 안테나 대신 외장 안테나를 사용하기 위한 케이블입니다. |

#### 2-8. 기타
---
| 부품명 | 번호 | 수량 | 가격 및 구매처 | 비고 |
| --- | --- | --- | --- | --- |
| 120ohm resistor(종단저항)  | - | 2 | 엘레파츠 | CAN 실습시 사용되는 종단저항용 |
| ST Link/V2(정품) | - | 1 | 디바이스마트 |  |
| 32GB microSD 메모리카드 | - | 1 | 디바이스마트 | 32GB용량 메모리 카드만 구매해야합니다. |
| 아두이노 FT232RL USB TO UART 컨버터모듈 | - | 1 | 디바이스마트 | DEBUG UART 출력을 읽고, RTC를 동기화하는데 사용되는 컨버터. |