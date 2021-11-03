---
title: "[Android] 애플리케이션의 기본 구조"
excerpt: "애플리케이션의 기본 구조"

categories:
  - Android
tags:
  - [Android]

toc: true
toc_sticky: true

date: 2021-11-03
last_modified_at: 2021-11-03
---

# 작업환경

- Windows
- Android Studio 2020.3.1

# 애플리케이션의 기본 구조

---

애플리케이션은 Java 코드와 XML 코드로 구성할 수 있다. 애플리케이션의 기본적인 작성 절차는 다음과 같다.

1. 사용자 인터페이스 작성(XML)
2. 자바 코드 작성(JAVA)
3. 매니페스트 파일 작성(XML)

기본적인 구성은 다음과 같다.

![Android_structure](https://user-images.githubusercontent.com/88693157/140077376-dbb155a8-448d-426f-80d6-4c9d9c33a9b0.png)

1. MainActivity.java
    
    ```java
    package com.example.myapplication;
    
    import androidx.appcompat.app.AppCompatActivity;
    
    import android.os.Bundle;
    
    public class MainActivity extends AppCompatActivity {
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
        }
    }
    ```    
2. activity_main.xml
3. manifests
    
    매니페스트: 환경설정 파일
    
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
        package="com.example.myapplication">
    
        <application
            android:allowBackup="true"
            android:icon="@mipmap/ic_launcher"
            android:label="@string/app_name"
            android:roundIcon="@mipmap/ic_launcher_round"
            android:supportsRtl="true"
            android:theme="@style/Theme.MyApplication">
            <activity
                android:name=".MainActivity"
                android:exported="true">
                <intent-filter>
                    <action android:name="android.intent.action.MAIN" />
    
                    <category android:name="android.intent.category.LAUNCHER" />
                </intent-filter>
            </activity>
        </application>
    
    </manifest>
    ```
    

## 레이아웃의 종류

- `<LinearLayout orientation = "vertical | horizontal">`: 가장 많이 사용하는 레이아웃
- `<Table Layout>`
- `<Grid Layout>`
- `<Relative Layout>`
- `<Tab Layout>`

### `<LinearLayout>`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/button1"
       android:text="첫 번째 버튼" />

   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/button2"
       android:text="두 번째 버튼" />

</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="horizontal">

   <Button
       android:layout_width="**wrap_content**"
       android:layout_height="wrap_content"
       android:text="버튼1" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="버튼2" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="버튼3" />
</LinearLayout>

```

## 뷰

뷰의 필드

- id: 뷰의 식별자
- layout_width: wrap_content | match_parent | 숫자
- layout_height: wrap_content | match_parent | 숫자
  - match_parent: 전체 너비 사용
  - wrap_content: 고유의 값을 그대로 사용

뷰의 크기 단위
- px
- dp(density-independent pixels): 폰트 크기에 영향을 받지 않음.
- sp(scale-independent pixels): 폰트 크기에 영향을 받음
- pt(points)
- mm(millimeters)
- in(inches)

### `<TextView>`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:background="#0000ff"
       android:text="This is a test."
       android:textColor="#ff0000"
       android:textSize="20pt"
       android:textStyle="italic"/>

</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:background="#00ff00"
       android:text="Practice
       Question."
       android:textStyle="italic"
       android:textSize="20pt"
       android:textColor="#fff"
       android:fontFamily="serif" />

</LinearLayout>
```

### `<EditView>`

에디트 텍스트

- android:drawableBottom
- android:drawableRight
- android:text
- android:singleLine
- android:hint
- android:inputType
    - none: 편집 불가능
    - Text: 일반적인 문자열
    - textMultiLine
    - textPostalAddress
    - textEmailAddress
    - textPassword
    - textVisiblePassword
    - number
    - phone
    - datetime

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="text"
       android:hint="여기에 입력할 수 있습니다." />

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="numberPassword"
       android:hint="패스워드" />

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="phone"
       android:hint="010-XXXX-XXXX" />
</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="textMultiLine"
       android:hint="multiple line" />

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="date"
       android:hint="MM/DD" />

   <EditText
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:inputType="time"
       android:hint="hh:mm" />

</LinearLayout>
```

### `<Button>`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="horizontal">

   <Button
       android:layout_width="wrap_content"
       android:layout_height="match_parent"
       android:backgroundTint="#ccc"
       android:textColor="#000"
       android:layout_marginRight="12px"
       android:text="첫 번째 버튼" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="match_parent"
       android:backgroundTint="#ccc"
       android:textColor="#000"
       android:layout_marginRight="12px"
       android:text="두 번째 버튼" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="match_parent"
       android:backgroundTint="#ccc"
       android:textColor="#000"
       android:layout_marginRight="12px"
       android:text="세 번째 버튼" />
</LinearLayout>
```

### `<ImageView>`

- android:adjustviewBounds
- android:cropToPadding
- android:maxHeigth
- android:maxWidth
- android:src

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <ImageView
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:src="@drawable/androids" />

</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

   <ToggleButton
       android:layout_width="wrap_content"
       android:layout_height="wrap_content" />

   <ImageView
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:src="@mipmap/ic_launcher_round" />

</LinearLayout>
```
