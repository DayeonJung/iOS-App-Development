# Certificates & Provisioning Profiles

1. 인증서 서명 요청(CSR 파일 생성)
2. Certificate 생성
3. Provisioning Profile 생성의 순서로 진행됩니다.

## 1. 인증서 서명 요청(CSR 파일 생성)

CSR파일은 Certificate를 생성하는데 필요한 파일입니다.

![Certificates%20&%20Provisioning/_2020-07-06__11.32.24.png](Certificates%20&%20Provisioning/_2020-07-06__11.32.24.png)

![Certificates%20&%20Provisioning/_2020-07-06__11.32.47.png](Certificates%20&%20Provisioning/_2020-07-06__11.32.47.png)

사용자 이메일 주소에 애플 개발자로 등록되어 있는 계정을 입력하면 됩니다.(기본적으로는 기기에 로그인되어 있는 계정이 입력됩니다.)

요청 항목에 "디스크에 저장됨"을 선택합니다.

계속을 눌러 CSR파일 생성을 완료합니다.

생성을 완료하면 키체인 접근의 Key항목에서 확인해 볼 수 있습니다.

## 2. Certificate 생성

Certificate를 생성하는 것은 애플이 개발자를 신뢰하여 애플 대신 앱을 실행 할 수 있는 권한을 부여받게 되는 것을 의미합니다.

개발을 하기 위한 **iOS App Development,** 배포를 하기 위한 **iOS Distribution** 두 가지 타입을 모두 만들어 주어야 합니다.

개발/배포하는 **기기**를 인증하는 것이기 때문에 기기별로 unique한 인증서가 생성됩니다. 예를 들어 글쓴이의 맥북프로로 두 개의 별개의 앱 프로젝트를 개발할 경우, 두 개의 인증서를 생성할 것 없이 한 개의 인증서만 생성하면 됩니다. (물론 development, distribution 두 가지 타입이 필요합니다.)

![Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.33.44.png](Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.33.44.png)

Certificate를 generate한 후 download한 후 생성된 파일을 더블클릭하면 키체인 접근의 내 인증서에 .cer파일이 추가됩니다. 이 때 중요한 것은 **private key와 함께 쌍으로 존재해야 제대로 생성된 것**입니다. 만약 .cer파일만 생성이 된다면 위에서 만든 CRS파일과 제대로 연결되지 않은 것이므로 다시 생성하여 반드시 키쌍으로 존재하도록 만들어야 합니다.

## 3. Provisioning Profile 생성

위에서 만든 Certificate와 iOS 개발 기기를 연결시켜 주는 것이 프로비저닝 프로파일 입니다. 프로비저닝 프로파일 또한 **개발용**, **배포용** 두가지 타입을 모두 생성해주어야 합니다. 앱을 개발하면서 Simulator가 아닌 실제 아이폰으로 테스트해 보고 싶을 때 반드시 세팅되어 있어야 합니다.

![Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.34.21.png](Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.34.21.png)

위의 그림에서 보듯이 Provisioning Profile에는 App ID(앱 스토어에 등록될 Bundle ID), Certificate, Device(디바이스 고유정보) 세 가지 정보가 들어가게 됩니다.

실제 프로젝트의 Bundle ID와 App ID가 일치해야 하므로 **각 프로젝트마다 별도의 프로비저닝 프로파일을 만들어 주어야 합니다**.

프로비저닝 프로파일이 올바르게 생성되면 아래와 같이 Xcode의 Provisioning Profile이 알맞게 세팅됩니다.

혹시 맞게 생성한 것 같은데 private key가 연결되어 있지 않다는 등의 에러메시지가 뜰 경우, Xcode를 종료한 후 재 실행해 확인해 보아야 합니다. Xcode 버그일 가능성이 있습니다.

![Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.34.51.png](Certificates%20&%20Provisioning%20Profiles/_2020-07-06__11.34.51.png)

### * 다른 앱 개발자가 같은 앱 프로젝트를 개발하려 할 때 전달해주어야 하는 것들은?

키체인 접근의 인증서 항목에서 해당 기기와 연결되어 있는 **Certificate 키쌍을 내보내기**하여 .p12 파일형태로 전달하면 됩니다!

iOS 기기로 개발하기 위해 필요한 Provisioning Profile은 **.mobileprovision 파일 그대로 전달**하거나 [developer.apple.com](http://developer.apple.com/) 의 Profile에서 다운로드 받아 사용이 가능합니다.

따라서 profile을 변경하는 등 갱신을 할 경우, **업데이트된 profile을 같이 협업하는 개발자와 반드시 공유**하여야 원활한 개발이 가능합니다.

Certificate가 만료되었을 경우, 

iOS 앱을 개발하고 배포할 때 필요한 인증서, 프로파일을 설정하는 방법을 알아봅니다.
