---
layout: post
title: "new와 getInstance의 차이"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, getInstance, new]
category: java
---
**new생성자를 통한 객체 선언**
```java
NewObject obj = new NewObject();
```


**getInstance메서드로 객체 선언**
```java
NewObject obj = NewObject.getInstance();
```


생성자를 통한 객체 선언은 **일반적** 인 경우

메서드를 통한 객체 선언은 **싱글톤 패턴** 을 적용한 경우


요청시마다 동일한 객체를 매번 생성하지 않고, 최초 호출시 JVM에 정적(static)인 클래스의 인스턴스를 생성해서 사용하고자 함이 이유

즉, 메모리의 효율적 관리를 위하여 JVM내에 유일하게 객체생성을 한 후 사용하는 경우에는 싱글톤 패턴을 사용 결과적으로 new와 getInstance는 일반적 객체생성과 싱글톤 패턴을 통한 객체생성의 차이점이라 볼 수 있다.


**요약**
  
new : 객체를 계속 만들 수 있다.
getInstance() : 싱글톤 패턴, 하나의 인스턴스만 가지고 공유해서 쓴다.
