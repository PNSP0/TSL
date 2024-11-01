데이터로거가 전송한 데이터를 실시간으로 모니터링하기 위한 웹 클라이언트입니다.

[https://commanderk.site/live](https://commanderk.site/live) 에서 서비스됩니다.

<img src='https://www.commanderk.site/assets/readme/1-4.jpeg' width="700px" height="325px" >
<img src='https://www.commanderk.site/assets/readme/1-5.jpeg' width="700px" height="400px">
<img src='https://www.commanderk.site/assets/readme/1-6.jpeg' width="700px" height="130px">  

# 1. 차량 ID 설정

`차량 ID 설정` 버튼을 눌러 차량 ID와 key를 입력합니다.

차량 ID : 24KSAE, key : 3225

ID와 key를 입력하고 확인을 누르면 페이지가 새로고침되고 설정이 반영됩니다.

<img src='https://www.commanderk.site/assets/readme/4-2.png' width="300px" height="225px">

- **설정한 차량 ID와 key는 해당 브라우저에 저장됩니다. 다른 브라우저로 페이지에 접속하면 다시 설정해야 합니다.**

# 2. UI 설정

`UI 설정` 버튼을 누르면 UI 설정 창이 표시됩니다.

UI는 여러 데이터를 묶는 데이터그룹과, 데이터그룹에 속한 데이터로 구성됩니다.

<img src='https://www.commanderk.site/assets/readme/4-3.png' width="300px" height="150px">

`UI 설정 불러오기`  버튼을 누르고, 테스트 당일에 차량전장제어팀원이 공유하는 `***(모니터링용).json` 파일을 불러옵니다.

- UI export/import

UI 설정 또한 브라우저에 저장됩니다. 다른 브라우저를 사용하여 접속하면 UI를 새로 설정해야 합니다.

매번 UI를 일일히 다시 설정하지 않도록 UI 내보내기와 불러오기 기능을 지원합니다.

`UI 설정 내보내기` 버튼을 누르면 현재 설정된 UI가 `ui_config.json` 파일로 다운로드 됩니다.

<img src='https://www.commanderk.site/assets/readme/4-13.png' width="300px" height="125px">

내보냈던 `ui_config.json` 파일을 선택하고 확인 버튼을 누르면, 해당 UI가 그대로 적용됩니다.

더 자세한 사항은 [클라이언트 활용 가이드](https://github.com/commanderk9826/KDL-distribution/wiki/클라이언트-활용-가이드)를 참고합니다.