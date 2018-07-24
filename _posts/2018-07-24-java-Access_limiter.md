---
layout: post
title: "java 객체 배열 생성 방법"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, 접근 제한자, public, protected, static, default, 자바 접근 제한자, 자바 public, 자바 제한자]
category: java
---
## 접근제한자(Access Modifier)
---
* 클래스 및 클래스의 구성 멤버에 대한 접근을 제한하는 역할

  * 다른 패키지에서 클래스를 사용하지 못하도록(클래스 제한)

  * 클래스로부터 객체를 생성하지 못하도록(생성자 제한)

  * 특정 필드와 메소드를 숨김 처리(필드와 메소드 제한)

+ **접근 제한자의 종류**
<table border="1">
<tr>
<th>접근 제한</th>
<th>적용 대상</th>
<th>접근할 수 없는 클래스</th>
</tr>
<tr>
<td>public</td>
<td>클래스, 필드, 생성자, 메소드</td>
<td>없음</td>
</tr>
<tr>
<td>protected</td>
<td>필드, 생성자, 메소드</td>
<td>자식 클래스가 아닌 <strong>다른 패키지</strong>에 소속된 클래스</td>
</tr>
<tr>
<td>default</td>
<td>클래스, 필드, 생성자, 메소드</td>
<td><strong>다른 패키지</strong>에 소속된 클래스</td>
</tr>
<tr>
<td>private</td>
<td>필드, 생성자, 메소드</td>
<td><strong>모든</strong> 외부 클래스</td>
</tr>
</table>

* **default**
클래스 선언할 때 public 생략한 경우
다른패키지에는 사용 불가

* **public**
다른 개발자가 사용할 수 있도록 라이브러리 클래스로 만들 때 유용
