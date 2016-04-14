---
layout: post
title: Android Multidex 문제 해결방법
---
안드로이드 스튜디오에서 개발을 하던 도중 Multidex 문제가 발생했다. 사용하는 라이브러리가 많아지면서 발생한 듯 하다.그래서 해결 방법을 구글링해서 해결했다!!
아직 그래들이나 빌드시스템에 대해서 잘 몰라서 일단 적용부터 하였다. 그 부분도 알아둘 필요가 있는 것 같다 매번 오류 날때마다 구글링 하니까 근본적인 해결법을 몰라서 답답한 경우가 많다.

[참고 블로그 - http://ohlab.kr/w/archives/153#respond](http://ohlab.kr/w/archives/153#respond)

##해결방법 

* SDK build-tools를 21.1.1이상으로 업그레이드
* build.gradle을 수정

~~~javascript
build.gradle
apply plugin:'com.android.application'

android {
	compileSdkVersion 23
	// 빌드툴버전이 21.1.1이상만 가능
	buildToolsVersion "23.0.3"
	// … 중략 …
	defaultConfig {
		applicationId "com.test.myapp"
		minSdkVersion 14
		targetSdkVersion 21
		versionCode 1
		versionName "1.0"
		multiDexEnabled true
	}

	dexOptions {
		javaMaxHeapSize "4g"
		preDexLibraries = false
	}
}

dependencies {
	// … 생략
	// multidex를 추가
	compile 'com.android.support:multidex:1.0.0'
}
~~~
* Application 클래스 수정

~~~java
public class MyApplicationClass extends android.support.multidex.MultiDexApplication
~~~





