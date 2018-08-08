---
layout: post
title: "String 클래스"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, 자바 String, string, 자바 메모리 영역, 자바 문자열, 자바 string 클래스, string class]
category: java
---
자바 String 클래스는 기본적으로 final형이므로 클래스내에 모든 내용을 변경할 수 없다.


```java
public class StringExample {

	public static void main(String[] args) {
		String str = "abc";
		String str1 = new String("abc");
		String str2 = new String("abc");
		System.out.println(str);
		System.out.println(str.hashCode() == str1.hashCode());

		System.out.println(str.equals(str2));		//각 인스턴스의 주소에 저장된 리터럴을 확인하므로 true
		System.out.println(str == str2);		  	//stack영역에 저장된 각 인스턴스의 주소값을 확인하므로 false

		System.out.println(str.hashCode());
		str = "cde";			                      //새로운 heap 영역에 cde가 저장된 공간을 생성하여 str의 주소를 cde가 있는 공간으로 이동한다
		System.out.println(str.hashCode());			//주소가 바뀐 것을 확인할 수 있음. abc가 저장된 공간은 남아 있음.
	}

}
```
![null](/assets/img/stringexample.JPG)
