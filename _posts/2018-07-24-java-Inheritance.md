---
layout: post
title: "상속(Inheritance)"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, Inheritance, 자바 상속, 상속]
category: java
---
## 상속(Inheritance)
---
자식 클래스가 부모 클래스의 멤버를 무려받는것
자식이 부모를 선택해 물려받음
상속 대상: 부모의 필드와 메소드

<pre class="prttyprint">
public class B extends A{
	String field2;
void method2() { ...}
}
</pre>

상속의 효과
  - 부모 클래스 재사용해 자식 클래스 빨리 개발 가능
  - 반복된 코드 중복 줄임
  - 객체 다형성 구현 가능
  - 유지 보수 편리성 제공
상속 제한
  - 부모 클래스의 private 접근 갖는 필드와 메소드 제외
  - 부모 클래스가 다른 패키지에 있을 경우, default접근 갖는 필드와 메소드도 제외

### Class casting
<pre class="prttyprint">
package hasu;
//부모 클래스
public class E028Car {
	protected int speed = 2;
	public void show() { System.out.println("Car~~1"); }

	public int speed() { return speed; }
}
</pre>

---
<pre class="prttyprint">
package hasu;
//자식 클래스
public class E028Bus extends E028Car {
	private int passenger = 3;
	public void move() { System.out.println("Bus 3 passenger : ==> " + passenger); }
}
</pre>

---
<pre class="prttyprint">
package hasu;

public class E028Case1 {

	public static void main(String[] args) {
		E028Car car1 = new E028Car();
		E028Bus bus1 = new E028Bus();
		//부모클래스 변수 = new 자식클래스();
		E028Car car2 = new E028Bus();		//Class Casting. car2는 E028Car의 주소를 가지고있다.

		car1.show();
		System.out.println(car1.speed);

		bus1.show();
		System.out.println(bus1.speed);
		bus1.move();

		car2.show();
		System.out.println(car2.speed);
		//car2.move();			X
		E028Bus buc1 = (E028Bus)car2;		//E028Bus클래스로 car2를 강제 변환
		bus1.move();
		E028Car car0 = buc1;						//E028Car클래스의 주소를 받고있는 car0에 buc1의 주소값을 할당받음
		car0.show();
		System.out.println(car0.speed());
		E028Bus bus0 = (E028Bus)car0;		//E028Bus클래스로 car0를 강제 변환
		bus0.move();
		System.out.println("+++++++++++++++++++++++++++++++");
	}

}
</pre>

실행시킨 결과는 다음과 같다.

![Inheritance](/assets/img/Inheritance_Example.JPG)



### ※ 자바는 단일 상속 - 부모 클래스 나열 불가
class 자식클래스 extends 부모클래스 1, ~~부모클래스 2~~{
---



## 메소드 재정의(@Override)
---
* 부모 클래스의 상속 메소드 수정해 자식 클래스에서 재정의 하는 것

* 메소드 재정의 조건
  - 부모 클래스의 메소드와 동일한 시그니쳐 가져야함
  - 접근 제한을 더 강하게 오버라이딩 불가
		- public을 default나 private으로 수정 불가
		- 반대로 default는 public으로 수정 가능
  - 새로운 예외(Exception) throws 불가

ex)
<pre class="prttyprint">
package inherit;
//부모 클래스
public class Airplane {
	public void land() { System.out.println("착륙합니다."); }
	public void fly() { System.out.println("일반비행합니다."); }
	public void takeOff() { System.out.println("이륙합니다."); }
}
</pre>
<pre class="prttyprint">
	package inherit;
	//자식 클래스
	public class SupersonicAirplane extends Airplane {
		public static final int NORMAL = 1;
		public static final int SUPERSONIC = 2;

		public int flyMode = NORMAL;

		@Override
		public void fly() {
			if(flyMode == SUPERSONIC) {
				System.out.println("초음속비행입니다.");
			} else { super.fly(); }				//부모클래스의 메소드
		}
	}
</pre>


## final
---
- final 필드 : 수정 불가 필드
- final 클래스 : 부모로 사용 불가한 클래스
- final 메소드 : 자식이 재정의할 수 없는 메소드

상속할 수 없는 final 클래스
  ==>자식 클래스 만들지 못하도록 final 클래스로 생성



참조 : 이것이 자바다(한빛미디어)
