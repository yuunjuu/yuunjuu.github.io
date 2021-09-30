---
title: "[개발 환경 구축] Windows에 JDK, 이클립스(Eclipse), 톰캣(Tomcat)"
excerpt: "Windows에 자바 개발 환경을 구축한다."

categories:
  - Setup
tags:
  - [Java, JDK, Eclipse, Tomcat]

toc: true
toc_sticky: true

date: 2021-09-30
last_modified_at: 2021-09-30
---

# 1. JDK 설치
---
1. [Oracle 홈페이지](https://www.oracle.com/java/technologies/downloads/#java8)에서 Java SE Development kit 8u301 설치 파일(jdk-8u301-windows-x64.exe)을 다운로드한다.
   
2. 저장 위치를 따로 설정하지 않으면 C:\Program Files에 Java라는 이름의 폴더가 생성된다. Java 폴더(C:\Program Files\Java)에는 jdk 폴더와 jre 폴더가 생성된 것을 확인할 수 있다.
   
3. 환경 변수 설정을 위해 jdk 폴더의 bin 폴더로 들어가 파일 경로(C:\Program Files\Java\jdk1.8.0_291\bin)를 복사한다.
   
4. Windows 검색창에 '시스템 환경 변수 편집'으로 이동하면 '시스템 속성' 창이 나타난다. '고급' 탭의 하단에 '환경 변수'를 클릭하면 환경 변수를 설정할 수 있는 창이 나타난다.
   
5. '환경 변수' 창의 '시스템 변수'의 Path를 더블 클릭하면 '환경 변수 편집' 창이 나타나고, '새로 만들기'를 클릭하여 복사한 주소를 붙여넣는다.
   
6. 환경 변수 설정이 제대로 되었는지 확인하기 위해 CMD창에서 java -version과 javac -version을 각각 입력하여 엔터를 치면 설치한 JDK 버전이 나타나는 것을 확인할 수 있다.

# 2. 이클립스(Eclipse) 설치
---
1. [이클립스 홈페이지](https://www.eclipse.org/downloads/packages/)에서 원하는 버전의 운영체제에 맞는 Eclipse IDE for Enterprise Java 압축 파일을 다운로드한다. 필자는 Eclipse IDE 2020-06 R Packages에서 다운로드하였다.

2. C: 드라이브에서 이클립스 작업을 할 폴더를 생성한다. 필자는 'workspace'라는 이름으로 생성하였다.
   
3. 다운로드한 이클립스 압축 파일을 원하는 경로에서 해제하고, 해당 폴더에 있는 eclipse.exe를 실행한다.

4. eclipse.exe을 실행하면  워크스페이스를 지정할 수 있는 창이 나타난다. 앞서 생성한 폴더(workspace)의 경로를 지정하여 Launch 버튼을 클릭하면 이클립스가 실행된다.

# 3. 톰캣(Tomcat) 8.5 설치
---
1. [아파치 톰캣 홈페이지](https://tomcat.apache.org/)로 이동하여 원하는 버전의 Tomcat 압축 파일을 다운로드한다. 필자는 Tomcat 8.5를 다운로드하였다.
2. 설치 파일을 실행한다. Configuration 화면에서 Server Shutdown Port는 8005, HTTP/1.1Connector Port는 8181로 변경한다.
3. Java Virtual Machine 화면에서는 자바 가상 머신과 연결하기 위한 작업을 한다. Java의 jre가 있는 경로로 지정한다.
4. 설치를 완료 후 웹 브라우저에 http://localhost:8005를 입력한다. Apache Tomcat/8.5 화면이 나타나면 톰캣 설치를 성공한 것이다.