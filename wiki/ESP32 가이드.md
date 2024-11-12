[아두이노IDE 사용방법](https://blog.naver.com/PostSearchList.nhn?blogId=elepartsblog&categoryNo=0&SearchText=ESP32+%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0&orderBy=date)를 참고하여 작성하였고, ARDUINO IDE_MAC_ENGLISH 버전을 토대로 작성하였습니다.

[ESP32실습 참고](https://velog.io/@emv_55555/posts)

# 1. ESP32 CP210x USB to UART DRIVER

[CP210x_Windows_Drivers.zip](https://github.com/commanderk9826/KDL-distribution/blob/main/CP210x_Windows_Drivers.zip)

CP210xVCPInstaller를 각자의 노트북에 환경에 맞는 프로그램을 선택해서 설치합니다.

# 2. 아두이노 IDE

- [보드 매니저 url 추가](https://dl.espressif.com/dl/package_esp32_index.json) (Arduino IDE → Preferences → Additional boards manager URLs)

- ESP32Dev Module 라이브러리 설치(Tools → Board → Boars Manager)

# 3. 라이브러리 설치

Library Manager에서 설치진행하면 됩니다.

- **WebSockets** by Markus Sattler
- **RingBuf** by Jean-Luc-Locoduino
- **ArduionoJson** by Benoit Blanchon

# 4. Parameter Setting

- **Board/Seiral Port Settings**

    <img src='https://www.commanderk.site/assets/readme/5-1.jpeg' width="475px" height="250px">  

    
    
- **Tools Setting**

    <img src='https://www.commanderk.site/assets/readme/5-2.png' width="475px" height="250px"> 
    

# 5. Code Review
**[telemetry.ino](https://github.com/commanderk9826/KDL-distribution/blob/main/device/telemetry/telemetry.ino) 의 세팅 값 사용자 정의**

- **<YOUR_HOTSPOT_ID>** : 핫스팟의 이름입니다.

- **<YOUR_HOTSPOT_PW>** : 핫스팟의 비밀번호입니다.

- **<YOUR_SERVER_DOMAIN>** : 서버의 도메인 주소입니다.(ex. commanderk.site, www.commanderk.site)

- **<YOUR_CHANNEL_NAME>, <YOUR_CHANNEL_KEY>** : `KDL/server/config.json` 파일의 `channel` 값


    
# 6. 마무리

<aside>
💡 Hot-spot 사용시, 애플폰은 안되고, 삼성폰으로만 가능합니다. Hot-Spot 세부설정에서 CPU Frequency 세팅값에 맞게 설정해주세요.

</aside>

- **Uploading Success Terminal**
    
    <img src='https://www.commanderk.site/assets/readme/5-3.jpeg' width="750px" height="200px"> 