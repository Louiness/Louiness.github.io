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


<pre class="prttyprint">
[ public ] interface 인터페이스명 { ... }
</pre>


인터페이스 이름은 클래스 이름을 작성하는 방법과 *동일* 하다. **영어 대소문자를 구분** 하며 첫 문자를 **대문자** 로 하고 나머지는 소문자로 작성하는 것이 관례이다.



인터페이스는 **상수와 메소드만을 구성 멤버로 가진다**. 인터페이스는 객체로 생성할 수 없기 때문에 생성자를 가질 수 없다. 자바 7까지는 인터페이스의 메소드는 실행 블록이 없는 추상 메소드로만 선언이 가능햇지만, 자바 8부터는 디폴트 메소드와 정적 메소드도 선언이 가능하다.

<pre class="prttyprint">
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
</pre>



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



<pre class="prttyprint">
public interface RemoteControl {
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;
}
</pre>



## 추상 메소드 선언
---
<pre class="prttyprint">
[ public abstract ]리턴타입 메소드명(매개변수, ...);
</pre>



인터페이스를 통해 호출된 메소드는 **최종적으로 객체에서 실행** 된다. 그렇기 때문에 인터페이스의 메소드는 실행 블록이 필요 없는 추상 메소드로 선언한다. 인터페이스에 선언된 추상 메소드는 모두 public abstract의 특성을 갖기 떄문에 public abstract를 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.


<pre class="prttyprint">
public interface RemoteControl {
  //상수
  public int MAX_VOLUME = 10;
  public int MIN_VOLUME = 0;

  //추상 메소드
  public void turnOn();
  public void turnOff();
  public void setVolume(int volume);
}
</pre>




## 디폴트 메소드 선언
---
<pre class="prttyprint">
[ public ] default 리턴타입 메소드명(매개변수, ...) { ... }
</pre>


형태는 클래스의 인스턴스 메소드와 동일하지만, default 키ㅝ드가 리턴 타입 앞에 붙는다. 디폴트 메소드는 public 특성을 갖기 때문에 public을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.


<pre class="prttyprint">
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
</pre>




## 정적 메소드 선언
---
<pre class="prttyprint">
[ public ] static 리턴타입 메소드명(매개변수, ...) { ... }
</pre>


클래스의 정적 메소드와 완전 동일하다. 정적 메소드는 public 특성을 갖기 때문에 public을 생략하더라도 자동적으로 컴파일 과정에서 붙게 된다.



<pre class="prttyprint">
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
</pre>





## 인터페이스 구현
---
개발 코드가 인터페이스 메소드를 호출하면 인터페이스는 객체의 메소드를 호출한다. 객체는 인터페이스에서 정의된 추상 메소드와 동일한 메소드 이름, 매개 타입, 리턴 타입을 가진 **실체 메소드** 를 가지고 있어야 한다. 이러한 객체를 인터페이스의 구현(implement) 객체라고 하고, 구현 객체를 생성하는 클래스를 구현 클래스라고 한다.




### 구현 클래스


<pre class="prttyprint">
public class 구현클래스명 implements 인터페이스명 {
  //인터페이스에 선언된 추상 메소드의 실체 메소드 선언
}
</pre>


인터페이스를 사용하기 위해선 위와 같은 implements를 클래스옆에 붙여주어야 한다.



다음은 Television과 Audio라는 이름을 가지고 있는 RemoteControl 구현 클래스를 작성하는 방법을 보여준다. 클래스 선언부 끝에 implements RemoteControl이 붙어 있기 때문에 이 두 클래스는 RemoteControl 인터페이스로 사용이 가능하다. RemoteControl에는 3개의 추상 메소드가 있기 때문에 Television과 Audio는 이 추상 메소드들에 대한 실체 메소드를 가지고 있어야 한다.
