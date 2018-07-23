---
layout: post
title: "java 객체 배열 생성 방법"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, 클래스 배열, 자바 클래스 배열, 객체 배열]
category: java
---
### 객체 배열(클래스 배열) : 객체에 대한 레퍼런스를 원소로 갖는 배열

**Studnet 클래스**
```java
public class Student {
	private String name;
	private int ssn;
	private String address;

	public Student(String name, int ssn, String address) {
		this.name = name;
		this.ssn = ssn;
		this.address = address;
	}
	@Override
	public String toString() {
		return name + " " + ssn + " " + address;
	}

}
```

**Student Main클래스**
```java
import java.util.Arrays;

public class StudentLexiMain {

	public static void main(String[] args) {
		//StudentLexiComparator lc = StudentLexiComparator.getInstance();
		Student[] sg = new Student[7];

		sg[0] = new Student("김말뚝", 101001,"서울");
		sg[1] = new Student("홍길동", 101001,"경기");
		sg[2] = new Student("최순동", 101001,"인천");
		sg[3] = new Student("이연람", 101001,"부산");
		sg[4] = new Student("하하호", 101001,"창원");
		sg[5] = new Student("김경민", 101001,"목포");
		sg[6] = new Student("김소연", 101001,"제주");
		System.out.println("이름 출력 ===============");
		prints(sg);
	}

	public static void prints(Student[] a) {
		int num = a.length;
		for(int i = 0; i < num; i++) {
			System.out.println(a[i]);
		}
		System.out.println();
	}

}
```

실행시킨 결과는 다음과 같다.
(./assets/img/object_array.jpg)
