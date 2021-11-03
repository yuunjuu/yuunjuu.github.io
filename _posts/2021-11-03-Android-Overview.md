---
title: "[Android] 안드로이드 기초 및 안드로이드 스튜디오 설치"
excerpt: "안드로이드 기초"

categories:
  - Android
tags:
  - [Android]

toc: true
toc_sticky: true

date: 2021-11-03
last_modified_at: 2021-11-03
---

# 1.  안드로이드

---
```
✔ 휴대용 장치를 위한 모바일 운영체제
```
안드로이드는 자바와 코틀린 언어를 이용하여 응용 프로그램을 작성할 수 있으며, SDK(Software Development Kit)를 통해 개발에 필요한 도구와 API를 제공한다.

안드로이드는 2005년 구글에서 인수한 후 2007년 안드로이드 플랫폼을 휴대용 장치 운영 체제로서 무료 공개한다고 발표한 이후 OHA(Open Handset Aliance: 모바일 장치의 개방형 표준을 선언한 동맹)에서 공개 표준을 개발하고 있다.

**안드로이드의 특징**

- SQLite 지원
- MPEG4, MP3, AAC, AMR, JPG, PNG, GIF 등
- 블루투스, 3G, 4G, 5G, Wifi 지원
- 카메라, GPS, 나침반 지원
- Java 8.0까지만 지원

**애플리케이션 구성**

- Activity: 사용자 인터페이스 화면을 갖는 하나의 작업
    - ex) 음악 재생 화면
- Service: 백그라운드에서 실행되는 컴포넌트로, 오랫동안 실행되는 작업이나 원격 프로세스를 위한 작업
    - ex) 음악 재생 서비스
- Broadcast reciver: 방송을 듣고 반응하는 컴포넌트로, 이벤트 리스너의 역할
- Content Provider: 데이터를 관리하고 다른 애플리케이션에게 제공하는 컴포넌트
  
**manifest 파일**
환경설정 파일로, XML을 사용
- `<activity>`
- `<service>`
- `<receiver>`
- `<provider>`

# 2.  안드로이드 스튜디오 설치

---

[안드로이드 공식 사이트](https://developer.android.com/studio)에서 안드로이드 2020.3.1버전을 다운로드한다.

1. 설치 파일을 실행하여 [Install] 버튼이 나올 때까지 [Next]를 클릭하여 진행한다.
   ![Android_AndroidSetup](https://user-images.githubusercontent.com/88693157/140072404-d5f5f8d3-cc65-4af0-8a9f-0f13d4315a13.png)

2. Install을 하면 다음과 같이 안드로이드 스튜디오 셋업 마법사 창이 나타난다. [Custom]을 선택하고 [Next]를 클릭한다.
   ![Android_Wizard1](https://user-images.githubusercontent.com/88693157/140072769-746a453e-e460-42db-9235-b408a81c7da8.png)

3. JDK를 저장할 위치를 선택하고 [Next]를 클릭한다.
   ![Android_Wizard2](https://user-images.githubusercontent.com/88693157/140072900-ff9d2823-6949-4585-8d68-05e27a73c88e.png)

4. 설치할 SDK 컴포넌트를 다음과 같이 체크하고, SDK를 저장할 위치를 선택한 후 [Next]를 클릭한다.
   ![Android_Wizard3](https://user-images.githubusercontent.com/88693157/140073300-7867b2df-93c7-4171-9a11-5e0b0405c1e8.png)

5. 다운로드를 완료하고 [Finish] 버튼을 클릭하면 다음과 같이 안드로이드 스튜디오 화면이 나타난다. 새로운 프로젝트를 생성하기 전에 [More Actions > SDK Manager]를 클릭한다.
   ![Android_Welcome](https://user-images.githubusercontent.com/88693157/140073467-a6fe0e71-2792-409d-a71c-3d6cce6e5ac6.png)

6. Android SDK의 이전 버전도 호환될 수 있도록 선택하여 다운로드 한다.
   ![Android_Settings](https://user-images.githubusercontent.com/88693157/140073647-b59c12c2-4e19-4d99-a3b4-11dfdc703bb2.png)

7. 다운로드가 완료된 후 [Ok] 버튼을 클릭하고 [New Project]을 클릭하면 아래와 같은 화면이 나타난다. [Empty Activity]를 선택한 후 [Next]를 클릭한다.
   ![Android_NewProject](https://user-images.githubusercontent.com/88693157/140073854-d420f4a2-973f-40d5-bc64-9b044cadc76d.png)

8. 프로젝트를 저장할 위치를 설정해주고, 언어는 Java로 설정한다.
   ![Android_EmptyActivity](https://user-images.githubusercontent.com/88693157/140074043-598cce89-b47a-4f58-a317-1fe7ccfa67f3.png)
9. [Finish]를 클릭하면 다음과 같은 화면이 나타난다.
    ![Android_main](https://user-images.githubusercontent.com/88693157/140074205-e246ba36-cd42-4de6-9bb5-853eb5e0439f.png)

10. 가상 애뮬레이터를 생성하기 위해 상단의 [No Devices > AVD Manager > Create Virtual Deivce...]를 클릭한다. 필자는 Nexus 5X를 선택하였다.
    ![Android_VirtualDeviceConfig](https://user-images.githubusercontent.com/88693157/140074379-4f33a66c-faa9-4d0d-9696-3626e4cb0444.png)

11. [Next]를 클릭하면 시스템 이미지를 선택할 수 있는 창이 나타난다. 원하는 이미지를 선택하여 다운로드한다. 필자는 R을 다운로드하였다.
    ![Android_VirtualDeviceImg](https://user-images.githubusercontent.com/88693157/140074968-d18c8249-57e1-48fd-8e7b-76ab14e5c5db.png)

12. [Finish]까지 완료한 후에는 다음과 같이 가상 애뮬레이터가 나타난다.
    ![Android_Amulator](https://user-images.githubusercontent.com/88693157/140075065-c022455b-491e-4648-a5f7-b986bc0f0649.png)
