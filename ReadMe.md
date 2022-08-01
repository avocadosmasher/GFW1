# ReadMe

1. [간단한 프로젝트 설명](#간단한-프로젝트-설명)
2. [버전 설명](#버전-설명)
3. [프론트 사용 기술스택](#프론트-사용-기술스택)



## 간단한 프로젝트 설명

본 프로젝트 GFW는 Go For a Walk를 줄임으로 사용자에게 **건강정보(걸음수, 소모 칼로리, 이동 거리, 이동 시간)**를 제공하며 산책을 독려하도록 하는 안드로이드 모바일 앱 프로젝트이다. 기본적으로 프론트엔드는 Android Studio를 사용하여 개발하였으며 백엔드는 Flask를 사용하였다. 각 파트별로 간단한 설명을 아래에 기술하도록 하겠다.



전체 흐름은 기능별 탭을 기준으로 설명하도록 한다. 본 프로젝트에서 기능별 구분을 위해 **로그인 탭, 메인 탭, 분석 탭, 프로필 탭, 친구 탭, 설정 탭** 이렇게 총 6가지로 구분한다.

* 로그인 탭.
  * 자체 로그인 서비스 : GFW 자체 로그인 서비스. (이메일 중복 및 비밀번호 유효성 검사까지 진행.)
  * 카카오톡 연동 로그인 서비스 : WebView를 통한 카카오톡 API를 사용한 로그인 서비스.
  * 네이버 연동 로그인 서비스 : WebView를 통한 네이버 API를 사용한 로그인 서비스.
* 메인 탭
  * 걸음수 확인 : 사용자가 설정한 목표 걸음수에 얼만큼 도달했는지 텍스트 및 Progress bar를 사용하여 가시화.
  * 목표 걸음수 설정 : 사용자가 1,000보, 5,000보, 10,000보 중에 금일의 목표 걸음수를 설정가능.
  * My 메뉴 편집 기능 : 걸음수 뿐 아니라 소모 칼로리, 이동 거리, 이동 시간 과 같은 사용자가 원하는 건강정보의 조회를 선택 가능.
* 분석 탭
  * 자신의 건강정보에 대한 주별, 월별 기록을 그래프화 하여 가시적으로 확인 가능.
  * 친구 비교 기능 : 자신이 원하는 친구와 그래프를 비교 할 수 있는 기능.
* 프로필 탭
  * 자신의 프로필 관리 : 프로필 수정(사진, 이름, 생년월일, 거주지) 및 정보 확인.
  * 일별 친구 순위 확인 : 산책에 대한 동기 부여를 위해 친구들간의 금일 걸음수 비교 기능을 넣음.
  * 메시지 확인 기능 : 친구들간의 간단한 격려, 응원 메시지를 보내고 받을 수 있도록 함.
* 친구 탭
  * 친구 관리 기능 : 친구 요청, 받은 요청 수락, 거절 기능 친구 목록 확인 기능.
* 설정 탭
  * 공지확인, 로그아웃 및 회원 탈퇴 기능.



# 버전 설명

manifest 추가 설정.

```xml
...
	<uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACTIVITY_RECOGNITION" />
    <uses-permission android:name="android.permission.USE_FULL_SCREEN_INTENT" />

<application
             ...
             android:usesCleartextTraffic="true">
    ...
</application>
```



gradle

```groovy
compiledSdkVersion 30
minSdkVersion 29
targetSdkVersion 29
```



## 프론트 사용 기술스택



#### 1. Android Studio

![Android Studio](C:\Users\rdd04\OneDrive\바탕 화면\Velog\캡스톤 2 정리\Android Studio.png)

Android Studio는 안드로이드 앱을 제작하기 위한 공식 통합 개발 환경(IDE) 로 Java와 Kotlin으로 개발이 가능하다. 처음하는 작품으로 PC의 프로그램을 선택할까 모바일 앱을 제작할까 하는 많은 고민끝에 근래에 수요가 늘어나고 있는 모바일 앱의 제작을 첫 작품으로 맞이하고자 하였고 React Native, Flutter, Swift 등과 같은 많은 모바일 앱 개발 프레임 워크들 중에서도 가장 근본적이고 시장에 뿌리깊게 자리잡은 Android 앱 개발을 위해 Android Studio를 선택하게 되었다.

#### 2. Retrofit 2

![Retrofit2](C:\Users\rdd04\OneDrive\바탕 화면\Velog\캡스톤 2 정리\Retrofit2.png)

OkHTTP를 기반으로 사용하며, Android와 서버간의 REST API 통신을 도와주는 라이브러리로 높은 성능, 가독성으로 현재 많은 사용자들에게 채택되고 있는 통신 라이브러리 중 하나이다. 해당 프로젝트의 백엔드로 Flask 라는 REST API기반 프레임워크를 사용하여 Retrofit 2를 통신 라이브러리로 채택하게 되었다.

#### 3. Google FIT API

![GoogleFIT](C:\Users\rdd04\OneDrive\바탕 화면\Velog\캡스톤 2 정리\GoogleFIT.png)

Google FIT API 는 Android내의 google fit으로 부터 수집된 건강관련 정보(걸음수, 소모 칼로리, 이동 거리 등) 과 같은 정보를 받아올 수 있도록 해주는 API이다. 해당 프로젝트에서 건강관련 정보를 수집할때 자체적인 연산을 통해 건강정보를 가져오는 것 보다는 신뢰성이 보장되어 있는 제 3자 즉 Google FIT로 부터 정보를 받아와 표기하는 방식을 취하였다.

#### 4. SQLITE

![SQLite](C:\Users\rdd04\OneDrive\바탕 화면\Velog\캡스톤 2 정리\SQLite.png)

응용 프로그램내에서 간단하게 사용할 수 있는 데이터베이스 관리 시스템이다. Android Studio에서도 이를 제공하며 서버로부터 정보를 받기보단 사용자 측면에서 간단하게 조회 및 수정을 해도 문제없는 데이터를 관리하기 위하여 사용하였다.

#### 5. FCM 

![fcm](C:\Users\rdd04\OneDrive\바탕 화면\Velog\캡스톤 2 정리\fcm.png)

FCM은 Firebase Cloud Messaging의 약자로 무료로 메시지를 전송할 수 있도록 해주는 크로스 플랫폼 메시징 솔루션이다. Android, ios 에서 모두 사용 가능하며 본 프로젝트에서는 사용자간의 메시지 전달을 위하여 BroadCast Receiver와 함께 사용하였다.





