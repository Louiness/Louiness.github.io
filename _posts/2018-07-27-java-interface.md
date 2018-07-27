---
layout: post
title: "인터페이스(Interface)"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, interface, 자바 인터페이스, 인터페이스, 자바 상속, java interface]
category: java
---
- **객체의 사용 방법** 을 정의한 타입
- 객체의 교환성을 높여주어서 다형성을 구현하는 매우 중요한 역할을 함
- 개발 코드와 객체가 서로 통신하는 접점 역할
- 코드 변경 없이 실행 내용과 리턴값을 다양화할 수 있음
- 물리적 형태는 클래스와 동일하고 소스를 작성할 때 선언하는 방법이 다름


인터페이스는 하나의 객체가 아니라 여러 객체들과 사용이 가능하므로 어떤 객체를 사용하느냐에 따라서 실행 내용과 리턴값이 다를 수 있다.


```java
[ public ] interface 인터페이스명 { ... }
```


인터페이스 이름은 클래스 이름을 작성하는 방법과 *동일* 하다. **영어 대소문자를 구분** 하며 첫 문자를 **대문자** 로 하고 나머지는 소문자로 작성하는 것이 관례이다.



인터페이스는 **상수와 메소드만을 구성 멤버로 가진다**. 인터페이스는 객체로 생성할 수 없기 때문에 생성자를 가질 수 없다. 자바 7까지는 인터페이스의 메소드는 실행 블록이 없는 추상 메소드로만 선언이 가능햇지만, 자바 8부터는 디폴트 메소드와 정적 메소드도 선언이 가능하다.

```java
interface 인터페이스명 {
  //상수
  타입 상수명 = 값;

  //추상 메소드
  타입 메소드명(매개변수, ...);

  //디폴트 메소드
  default 타입 메소드명(매개변수, ...) { ... }

  //정적 메소드
  static 타입 메소드명(매개변수) { ... }
}
```



### 상수 필드(Constant Field)

인터페이스는 객체 사용 설명서이므로 런타임 시 데이터를 저장할 수 있는 필드를 선언할 수 없다. 그러나 상수 필드는 선언이 가능하다. 상수는 인터페이스에 고정된 값으로 런타임 시에 데이터를 바꿀 수 없다. 상수를 선언할 때에는 반드시 초기값을 대입해야 한다.




### 추상 메소드(Abstract Method)

추상 메소드는 객체가 가지고 있는 메소드를 설명한 것으로 호출할 때 어떤 매개값이 필요하고, 리턴 타입이 무엇인지만 알려준다. 실제 실행부는 객체(구현 객체)가 가지고 있다.




### 디폴트 메소드(Default Method)

디폴트 메소드는 인터페이스에 선언되지만 사실은 객체(구현 객체)가 가지고 있는 인스턴스 메소드라고 생각해야 한다.




### 정적 메소드(Static Method)

디폴트 메소드와는 달리 객체가 없어도 인터페이스만으로 호출이 가능하다.




## 상수 필드 선언
---
상수는 **public static final** 로 선언한다. 이 부분은 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.

상수명은 대문자로 작성하되, 서로 다른 단어로 구성되어 있을 경우에는 언더바( _ )로 연결하는 것이 관례이다.

인터페이스 상수는 static {} 블록으로 초기화할 수 없기 때문에 반드시 선언과 동시에 초기값을 지정해야 한다.



```java
public interface RemoteControl {
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;
}
```



## 추상 메소드 선언
---
```java
[ public abstract ]리턴타입 메소드명(매개변수, ...);
```



인터페이스를 통해 호출된 메소드는 **최종적으로 객체에서 실행** 된다. 그렇기 때문에 인터페이스의 메소드는 실행 블록이 필요 없는 추상 메소드로 선언한다. 인터페이스에 선언된 추상 메소드는 모두 public abstract의 특성을 갖기 떄문에 public abstract를 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.


```java
public interface RemoteControl {
  //상수
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;

  //추상 메소드
  public void turnOn();
  public void turnOff();
  public void setVolume(int volume);
}
```




## 디폴트 메소드 선언
---
```java
[ public ] default 리턴타입 메소드명(매개변수, ...) { ... }
```


형태는 클래스의 인스턴스 메소드와 동일하지만, default 키ㅝ드가 리턴 타입 앞에 붙는다. 디폴트 메소드는 public 특성을 갖기 때문에 public을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.


```java
public interface RemoteControl {
  //상수
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;

  //추상 메소드
  public void turnOn();
  public void turnOff();
  public void setVolume(int volume);

  //디폴트 메소드
  default void setMute(boolean mute) {           //실행 내용까지 작성
    if(mute) {
      System.out.println("무음 처리합니다.");
    } else {
      System.out.println("무음 해제합니다.");
    }
  }
}
```




## 정적 메소드 선언
---
```java
[ public ] static 리턴타입 메소드명(매개변수, ...) { ... }
```


클래스의 정적 메소드와 완전 동일하다. 정적 메소드는 public 특성을 갖기 때문에 public을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.



```java
public interface RemoteControl {
  //상수
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;

  //추상 메소드
  public void turnOn();
  public void turnOff();
  public void setVolume(int volume);

  //디폴트 메소드
  default void setMute(boolean mute) {           //실행 내용까지 작성
    if(mute) {
      System.out.println("무음 처리합니다.");
    } else {
      System.out.println("무음 해제합니다.");
    }
  }

  //정적 메소드
  static void changeBattery() {
    System.out.println("건전지를 교환합니다.");
  }
}
```





## 인터페이스 구현
---
개발 코드가 인터페이스 메소드를 호출하면 인터페이스는 객체의 메소드를 호출한다. 객체는 인터페이스에서 정의된 추상 메소드와 동일한 메소드 이름, 매개 타입, 리턴 타입을 가진 **실체 메소드** 를 가지고 있어야 한다. 이러한 객체를 인터페이스의 구현(implement) 객체라고 하고, 구현 객체를 생성하는 클래스를 구현 클래스라고 한다.




### 구현 클래스


```java
public class 구현클래스명 implements 인터페이스명 {
  //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
}
```


인터페이스를 사용하기 위해선 위와 같은 implements를 클래스옆에 붙여주어야 한다.



다음은 Television과 Audio라는 이름을 가지고 있는 RemoteControl 구현 클래스를 작성하는 방법을 보여준다. 클래스 선언부 끝에 implements RemoteControl이 붙어 있기 때문에 이 두 클래스는 RemoteControl 인터페이스로 사용이 가능하다. RemoteControl에는 3개의 추상 메소드가 있기 때문에 Television과 Audio는 이 추상 메소드들에 대한 실체 메소드를 가지고 있어야 한다.
```java
public class Television implements RemoteControl {
	//필드
	private int volume;

	//turnOn() 추상 메소드의 실체 메소드
	public void turnOn() {
		System.out.println("TV를 켭니다.");
	}

	//turnOff() 추상 메소드의 실제 메소드
	public void turnOff() {
		System.out.println("TV를 끕니다.");
	}

	//setVolume() 추상 메소드의 실체 메소드
	public void setVolume(int volume) {

		if(volume > RemoteControl.MAX_VOLUME)
			this.volume = RemoteControl.MAX_VOLUME;

		else if(volume < RemoteControl.MIN_VOLUME)
			this.volume = RemoteControl.MIN_VOLUME;

		else this.volume = volume;

		System.out.println("현재 TV 볼륨 : " + volume);
	}

}
```


```java
public class Audio implements RemoteControl{
	//필드
	 private int volume;

	@Override
	public void turnOn() {
		System.out.println("Audio를 켭니다.");
	}

	@Override
	public void turnOff() {
		System.out.println("Audio를 끕니다.");
	}

	@Override
	public void setVolume(int volume) {
		if(volume > RemoteControl.MAX_VOLUME) this.volume = RemoteControl.MAX_VOLUME;
		else if(volume < RemoteControl.MIN_VOLUME) this.volume = RemoteControl.MIN_VOLUME;
		else this.volume = volume;

		System.out.println("현재 Audio 볼륨 : " + volume);

	}

}
```



```java
public class RemoteControlExample {

	public static void main(String[] args) {
		RemoteControl rc;
		rc = new Television();
		rc = new Audio();
	}

}
```




### 익명 구현 객체


구현 클래스를 만들어 사용하는 것이 일반적이고, 클래스를 재사용할 수 있기 때문에 편리하지만, 일회성의 구현 객체를 만들기 위해 소스 파일을 만들고 클래스를 선언하는 것은 비효율적이다. 자바는 소스 파일을 만들지 않고도 구현 객체를 만들 수 있는 방법을 제공하는데, 그것이 익명 구현 객체이다.


```java
인터페이스 변수 = new 인터페이스() {
  //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
};
```

익명 구현 객체를 생성해서 인터페이스 변수에 대입하는 코드이다. 작성 시 주의할 점은 하나의 실행문이므로 끝에는 세미코론(;)을 반드시 붙여야 한다.
new 연산자 뒤에는 클래스 이름이 와야 하는데, 이름이 없다. 인터페이스() {}는 인터페이스를 구현해서 중괄호 {}와 같이 클래스를 선언하라는 뜻이고, new 연산자는 이렇게 선언된 클래스를 객체로 생성한다. 중괄호 {}에는 인터페이스에 선언된 모든 추상 메소드들의 실체 메소드를 작성해야 한다. 그렇지 않으면 **컴파일 에러** 가 발생한다.
다음은 RemoteControl의 익명 구현 객체를 만들어 본 것이다.
```java
public class RemoteControlExample {
  public static void main(String[] args) {
    RemoteControl rc = new RemoteControl() {
      public void turnOn() { /*실행문*/ }
      public void turnOff() { /*실행문*/ }
      public void setVolume(int volume) { /*실행문*/ }
    };
  }
}
```





### 다중 인터페이스 구현 클래스
인터페이스 A와 인터페이스 B가 객체의 메소드를 호출할 수 있으려면 객체는 이 두 인터페이스를 모두 구현해야 한다. 따라서 구현 클래스는 다음과 같이 작성되어야 한다.
```java
public class 구현클래스명 implements 인터페이스A, 인터페이스B {
  //인터페이스 A에 선언된 추상 메소드의 실체 메소드 선언
  //인터페이스 B에 선언된 추상 메소드의 실체 메소드 선언
}
```


다중 인터페이스를 구현할 경우, 구현 클래스는 모든 인터페이스의 추상 메소드에 대해 실체 메소드를 작성해야 한다. 만약 하나라도 없으면 추상 클래스로 선언해야 한다.



```java
public interface Searchable {
  void search(String url);
}
```




```java
public class SmartTelevision implements RemoteControl, Searchable {
  private int volume;

  public void turnOn() {
    System.out.println("TV를 켭니다.");
  }
  public void turnOff() {
    System.out.println("TV를 끕니다.");
  }
  public void setVolume(int volume) {
    if(volume > RemoteControl.MAX_VOLUME) {
      this.volume = RemoteControl.MAX_VOLUME;
    } else if(volume < RemoteControl.MIN_VOLUME) {
      this.volume = RemoteControl.MIN_VOLUME;
    } else {
      this.volume = volume;
    }
    System.out.println("현재 TV 볼륨: " + volume);
  }

  public void search(String url){
    System.out.println(url + "을 검색합니다.");
  }
}
```




### 인터페이스 사용


인터페이스로 구현 객체를 사용하려면 다음과 같이 인터페이스 변수를 선언하고 구현 객체를 대입해야 한다. 인터페이스 변수는 참조타입이기 때문에 구현 객체가 대입될 경우 구현 객체의 번지를 저장한다.
```java
RemoteControl rc;
rc = new Television();
rc = new Audio();
```


개발 코드에서 인터페이스는 클래스의 필드, 생성자 또는 메소드의 매개 변수, 생성자 또는 메소드의 로컬 변수로 선언될 수 있다.

```java
public class MyClass {
  //필드
  RemoteControl rc = new Television();

  //생성자
  MyClass(RemoteControl rc) {
    this.rc = rc;
  }

  //메소드
  void methodA() {
    //로컬 변수
    RemoteControl rc = new Audio();
  }

  void methodB(RemoteControl rc) { ... }
}
```





### 추상 메소드 사용


구현 객체가 인터페이스 타입에 대입되면 인터페이스에 선언된 추상 메소드를 개발 코드에서 호출할 수 있게 된다.



```java
public class RemoteControlExample {
  public static void main(String[] args) {

    RemoteControl rc = null;      //인터페이스 변수 선언

    rc = new Television();        //Television 객체를 인터페이스 타입에 대입
    rc.turnOn();                  //인터페이스의 turnOn(), turnOff() 호출
    rc.turnOff();

    rc = new Audio();             //Audio 객체를 인터페이스 타입에 대입
    rc.turnOn();                  //인터페이스의 turnOn(), turnOff() 호출
    rc.turnOff();

  }
}
```




### 디폴트 메소드 사용
