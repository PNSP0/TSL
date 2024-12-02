# Introduction

KDL(Kust Data Logger)는 대학생 자작자동차대회 출전차량을 위해 제작한 데이터로깅 플랫폼입니다. 
가이드에 따라 실시간 원격 모니터링, 데이터 분석 도구 등을 쉽게 이용할 수 있습니다.<br>


**주요 기능**
- CAN, 3축 가속도, GPS, 디지털/아날로그 신호 등 다양한 데이터 기록
- Micro SD 카드에 로그 저장
- 실시간 텔레메트리(원격 데이터 모니터링)
- 자체 시계(RTC)를 통한 실제 시간 추적
- 웹 기반 데이터 시각화 및 분석 도구


## 1. 데이터로거(KDL)

차량에 장착되어 데이터를 수집하는 장비입니다. 기록할 수 있는 데이터의 종류는

- CAN 2.0(A/B) 버스 트래픽
- 2채널 디지털 입력 신호
- 2채널 아날로그 입력 신호
- 3축 ±4g 가속도 (ADXL345)
- GPS 위치 정보 (NEO-7M)
- 전원(LV) 전압 및 자체 CPU 온도
- RTC 실제 시간 정보


<img src='https://www.commanderk.site/assets/readme/1-1.jpeg' width="450px" height="250px">

## 2. 텔레메트리 모니터

데이터로거가 통신하는 텔레메트리 서버와, 실시간 데이터 모니터링을 위한 웹 클라이언트입니다.

### 서버
따로 설정하지 않는 한 데이터로거는 기본적으로 [commanderk.site](http://pknova.site) 를 사용하여 데이터를 실시간으로 전송합니다.

> 기본 제공되는 텔레메트리 서버는 확인된 사용자만 이용할 수 있습니다.



### 클라이언트

각 사용자가 개별적으로 UI를 설정할 수 있으며, UI 설정 파일을 내보내고 불러오는 기능을 지원합니다.


<img src='https://www.commanderk.site/assets/readme/1-4.jpeg' width="700px" height="325px" >
<img src='https://www.commanderk.site/assets/readme/1-5.jpeg' width="700px" height="400px">
<img src='https://www.commanderk.site/assets/readme/1-6.jpeg' width="700px" height="130px">


## 데이터분석도구

데이터로거는 데이터를 정해진 [로그 프로토콜](https://github.com/commanderk9826/KDL-distribution/wiki/로그-프로토콜)에 따라 바이너리 파일로 SD 카드에 기록합니다.

이러한 로그를 사람이 읽을 수 있도록 json 및 csv 파일로 변환하는 해석기와, 데이터를 그래프로 시각화하는 분석 도구 모음입니다.


<img src='https://www.commanderk.site/assets/readme/1-3.jpeg' width="700px" height="1175px">
