---
layout: post
title: "예외 처리"
tags: [자바, 자바 꿀팁,자바 tip, 자바 기본, 이클립스, 이클립스 tip, 자바 기초, 자바 Exception, Exception, 자바 예외, 자바 예외처리]
category: java
---
**예외**: 개발자의 잘못된 코딩으로 인해 발생하는 프로그램 오류
  - 예외가 발생되면 프로그램은 곧바로 종료된다는 점에서는 에러와 동일
  - 예외 처리를 통해 프로그램을 종료하지 않고 정상 실행 상태가 유지되도록 할 수 있음
  - 자바에서는 예외를 클래스로 관리
    - JVM은 프로그램을 실행하는 도중에 예외가 발생하면 해당 예외 클래스로 객체를 생성




## 일반 예외(Exception)
---
- 컴파일러 체크 예외라고도 부른다
  - 자바 소스를 컴파일하는 과저에서 예외 처리 코드가 필요한지 검사. 예외 처리 코드가 없다면 컴파일 오류가 발생
- Exception을 상속받지만 Runtime Exception을 상속받지 않는 클래스



## 실행 예외(Runtime Exception)
---
- 컴파일 하는 과정에서 예외 처리 코드를 검사하지 않는 예외(컴파일러가 체크하지 않음)
  - 오로지 개발자의 경험에 의해서 예외 처리 코드를 삽입해야 함


<a name="nullException"></a>
### 1. NullPointerException
객체 참조가 없는 상태, 즉 **null** 값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용했을 때 발생한다.
  - 객체가 없는 상태에서 객체를 사용하려 했으니 예외가 발생하는 것


```java
package test;

public class nullexception {

	public static void main(String[] args) {
		String data = null;
		System.out.println(data.toString());
	}

}
```

![null](/assets/img/nullexception.JPG)

6번째 줄에서 data 변수는 null 값을 가지고 있기 떄문에 String 객체를 참조하고 있지 않다. 하지만 그 다음 줄에서 String 객체의 toString()메소드를 호출하고 있다. 여기서 NullPointerException이 발생한다.


<a name="arrayException"></a>
### 2. ArrayIndexOutOfBoundsException
배열에서 인덱스 범위를 초과하여 사용할 경우 발생하는 실행 예외

```java
package test;

public class ArrayIndexOutOfBoundsExceptionExample {

	public static void main(String[] args) {
		int[] a = new int[2];
		a[0] = 1;
		a[1] = 3;
		a[2] = 5;
	}
}
```

![null](/assets/img/arrayindexexception.JPG)

배열의 개수가 2개인 정수형 배열 a를 생성하였다. 하지만 위 코드에서는 3개의 배열에 각각 값을 초기화하였다. 이런 경우 ArrayIndexOutOfBoundsException 실행 예외가 발생한다. 인덱스가 0부터 시작하므로 배열 a는 a[0], a[1]까지 생성되지만 a[2]에도 값을 초기화해줘서 에러가 난거다.


<a name="classException"></a>
### 3. ClassCastException
타입 변환(Casting)은 상위 클래스와 하위 클래스 간에 발생하고 구현 클래스와 인터페이스 간에도 발생한다. 이러한 관계까 아니라면 클래스는 다른 클래스로 타입 변환을 할 수 없다. 억지로 타입 변환을 시도할 경우 ClassCastException이 발생한다.

```java
package test;

public class ClassCastExceptionExample {

	public static void main(String[] args) {
		Dog dog = new Dog();
		changeDog(dog);

		Cat cat = new Cat();
		changeDog(cat);
	}

	public static void changeDog(Animal animal) {
		Dog dog = (Dog)animal;
	}

}

class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }
```

![null](/assets/img/classcastexception.JPG)

예제를 실행하면 14라인에서 ClassCastException이 발생한다. 그 이유는 9번째 줄에서 Cat객체를 매개값으로 주었기 때문에 Dog타입으로 변환할 수 없다. 이렇게 잘못된 매개값이 들어올 수 있기 때문에 타입 변환 전에 타입 변환이 가능한지 instanceof연산자로 확인하는 것이 좋다. instanceof 연산의 결과가 true이면 좌항 객체를 우항 타입으로 변환 가능하다는 뜻이다.
```java
Animal animal = new Dog();
if(animal instanceof Dog) {
  Dog dog = (Dog)animal;
} else if(animal instanceof Cat) {
  Cat cat = (Cat)animal;
}
```





## 예외 처리 코드
프로그램에서 예외가 발생했을 경우 프로그램의 갑작스러운 종료를 막고, 정상 실행을 유지할 수 있도록 처리하는 코드

예외처리 코드는 try-catch-finally 블록을 이용한다. try-catch-finally 블록은 생성자 내부와 메소드 내부에서 작성되어 일반 예외와 실행 예외가 발생할 경우 예외 처리를 할 수 있도록 해준다.

![try-catch-finally](/assets/img/exception_algorithm.JPG)


try 블록에는 예외 발생 가능 코드가 위치한다. try 블록의 코드가 예외 발생 없이 정상 실행되면 catch 블록의 코드는 실행되지 않고 finally 블록의 코드를 실행한다. 만약 try 블록의 코드에서 예외가 발생하면 **즉시 실행을 멈추고** catch블록으로 이동하여 예외 처리 코드를 실행한다. 그리고 finally 블록의 코드를 실행한다. *finally 블록은 옵션으로 생략 가능하다.*

```java
public class TryCatchFinallyExample {
  public static void main(String[] args) {
    try {
      Class clazz = Class.forName("java.lang.String2");
    } catch(ClassNotFoundException e){
      System.out.println("클래스가 존재하지 않습니다.");
    }
  }
}
```

위 예제를 실행시키면 4라인에서 ClassNotFoundException이 발생하는데, 이것은 java.lang.String2 클래스가 존재하지 않기 때문이다. 4라인에서 예외가 발생하면 5라인을 실행해서 예외 처리를 하게 된다. <a href="#arrayException" class="scroll">ArrayIndexOutOfBoundsException</a>이나 <a href="#nullException" class="scroll">NullPointerException</a>, <a href="#classException" class="scroll">ClassCastException</a>과 같은 실행 예외는 컴파일러가 예외 처리 코드를 체크하지 않기 때문에 이클립스에서도 빨간 밑줄이 생기지 않는다.

![try-catch-finally_example](/assets/img/trycatch_example.JPG)



## 예외 종류에 다른 처리 코드
---

### 다중 catch와 cath 순서

만약 하나의 try 블록에 여러 개의 catch 블록이 있다 하더라도 단 하나의 catch블록만 실행이 된다. 그 이유는 try 블록에서 동시 다발적으로 예외가 발생하지 않고, 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 catch블록으로 이동하기 때문이다. 따라서 이 경우, 발생되는 예외별로 예외 처리 코드를 처리할 수 있도록 **순서대로** 다중 catch블록을 작성해 주어야 한다.
```java
public class CatchByExceptionKindExample {
  public static void main(String[] args) {
    try {
      String data1 = args[0];
      String data2 = args[1];
      int value1 = Integer.parseInt(data1);
      int value2 = Integer.parseInt(data2);
      int result = value1 + value2;
      System.out.println(data1 + " + " + data2 + " = " + result);
    } catch(ArrayIndexOutOfBoundsException e) {
      System.out.println("실행 매개값의 수가 부족합니다.");
      System.out.println("[실행 방법]");
      System.out.println("java CatchByExceptionKindExample  num1  num2");
    } catch(NumberFormatException e) {
      System.out.println("숫자로 변환할 수 없습니다.");
    } catch(Exception e) {
      System.out.println("실행에 문제가 있습니다.");
    } finally {
      System.out.println("다시 실행하세요.");
    }
  }
}
```

![catchbyexception](/assets/img/catchbyexception.JPG)


![catchbyexception](/assets/img/catchbyexception2.JPG)

4번째 줄과 5번째 줄에서 ArrayIndexOutOfBoundsException이 발생한다면 11~13번째 줄이 실행되고, 6번째 줄과 7번째 줄에서 NumberFormatException이 발생한다면 15번째 줄이 실행된다. 17번째 줄은 예외 발생 여부와 상관없이 실행된다. 만약 16번째 줄이 첫 번째 catch로 들어갔다면 잘못된 코딩이다. Exception은 ArrayIndexOutOfBoundsException이나 NumberFormatException의 상위 예외 클래스이기 때문에 첫 번째 catch블록만 선택되어 시리행되고 두 번째 catch블록은 어떤 경우에라도 실행 되지 않는다.





### 멀티 catch
자바 7부터 하나의 catch 블록에서 여러 개의 예외를 처리할 수 있도록 멀티(multi) catch기능을 추가했다. catch 괄호() 안에 동일하게 처리하고 싶은 예외를 |로 연결하면 된다.
```java
public class CatchByExceptionKindExample {
  public static void main(String[] args) {
    try {
      String data1 = args[0];
      String data2 = args[1];
      int value1 = Integer.parseInt(data1);
      int value2 = Integer.parseInt(data2);
      int result = value1 + value2;
      System.out.println(data1 + " + " + data2 + " = " + result);
    } catch(ArrayIndexOutOfBoundsException | NumberFormatException e) {
      System.out.println("실행 매개값의 수가 부족하거나 숫자로 변환할 수 없습니다.");
    } catch(Exception e) {
      System.out.println("알수 없는 예외 발생");
    } finally {
      System.out.println("다시 실행하세요.");
    }
  }
}
```


![multicatch](/assets/img/multicatch.JPG)






### 예외 떠넘기기

메소드 내부에서 예외가 발생할 수 있는 코드를 작성하 때 try-catch 블록으로 예외를 처리하는 것이 기본이지만, 경우에 따라서는 메소드를 호출한 곳으로 예외를 떠넘길 수도 있다. 이때 사용하는 키워드가 **throws** 이다. throws 키워드는 메소드 선언부 끝에 작성되어 메소드에서 처리하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 한다. throws 키워드 뒤에는 떠넘길 예외 클래스를 쉼표로 구분해서 나열해주면 된다.
```java
리턴타입 메소드명(매개변수, ...) throws 예외클래스1, 예외클래스2, ... {
}
```


throws 키워드가 붙어있는 메소드는 반드시 try 블록 내에서 호출되어야 한다. 그리고 catch 블록에서 떠넘겨 받은 예외를 처리해야 한다.
```java
public class ThrowsExample {
  public static void main(String[] args) {
	  try {
		  findClass();
	  } catch(ClassNotFoundException e) {
		  System.out.println("클래스가 존재하지 않습니다.");
	  }
  }

  public static void findClass() throws ClassNotFoundException {
	  Class clazz = Class.forName("java.lang.String2");
  }
}
```


![throw](/assets/img/throwsexample.JPG)


main() 메소드에서도 throws 키워드를 사용해서 예외를 떠넘길 수 있는데, main() 메소드에서 throws Exception을 붙이는 것은 좋지 못한 예외 처리 방법이다. 프로그램 사용자는 프로그램이 알 수 없는 예외 내용을 출력하고 종료되는 것을 좋아하지 않는다. 그렇기 때문에 main()에서 try-catch 블록으로 예외를 최종 처리하는 것이 바람직하다.




### 예외 정보 얻기

try 블록에서 예외가 발생되면 예외 객체는 catch 블록의 매개 변수에서 참조하게 되므로 매개 변수를 이용하면 예외 객체의 정보를 알 수 있다. 모든 예외 객체는 Exception 클래스를 상속하기 때문에 Exception이 가지고 있는 메소드들을 모든 예외 객체에서 호출할 수 있다. 그 중에서도 가장 많이 사용되는 메소드는 **getMessage()** 와 **printStackTrace()** 이다. 예외를 발생시킬 때 다음과 같이 String 타입의 메시지를 갖는 생성자를 이용하였다면, 메시지는 자동적으로 예외 객체 내부에 저장된다.

```java
throw new XXXException("예외 메시지");
```


예외 메시지의 내용에는 왜 예외가 발생했는지에 대한 간단한 설명이 포함된다. 좀 더 상세한 원인을 세분화하기 위해 예외 코드를 포함하기도 하는데, 예를 들어 데이터베이스에서 발생한 오류들은 예오 코드가 예외 메시지로 전달된다. 이와 같은 예외 메시지는 다음과 같이 catch 블록에서 getMessage() 메소드의 리턴값으로 얻을 수 있다.

```java
} catch(Exception e) {
  //예외가 가지고 있는 Message 얻기
  String message = e.getMessage();

  //예외의 발생 경로를 추적
  e.printStackTrace();
}
```


printStackTrace()는 메소드 이름에서도 알 수 있듯이 예외 발생 코드를 추적해서 모두 콘솔에 출력한다. 어떤 예외가 어디에서 발생했는지 상세하게 출력해주기 때문에 프로그램을 테스트하면서 오류를 찾을 때 활용된다.




<a name=AccountPro></a>
```java
class Account {
	private long balance;

	public Account() { }

	public long getBalance() {
		return balance;
	}

	public void deposit(int money) {
		balance += money;
	}


	public void withdraw(int money) throws BalanceInsufficientException {
		//throws BalanceInsufficientException : 사용자 정의 예외 떠넘기기
		if(balance < money) {
			//사용자 예외 발생
			throw new BalanceInsufficientException("잔고부족 : " + (money - balance) + "모자람");
		}
		balance -= money;
	}
}

//사용자 정의 예외
class BalanceInsufficientException extends Exception {
	public BalanceInsufficientException() { }
	public BalanceInsufficientException(String message) {
		super(message);
	}
}

public class AccountExample {

	public static void main(String[] args) {
		Account account = new Account();
		//예금하기
		account.deposit(10000);
		System.out.println("예금액: " + account.getBalance());
		//출금하기
		try {
			account.withdraw(30000);
		} catch(BalanceInsufficientException e) { 	//예외 메시지 얻기
			String message = e.getMessage();
			System.out.println(message);
			System.out.println();					//예외 추적 후 출력
			e.printStackTrace();
		}
	}

}

```



![accountexample](/assets/img/accountexception.JPG)



다음 AccountExample 클래스는 Account 클래스를 이용해서 예금과 출금을 한다. 출금할 때 withdraw() 메소드를 사용하므로 예외 처리가 꼭 필요하다. 예외 처리 코드에서 BalanceInsufficientException 객체의 getMessage() 메소드와 printStackTrace() 메소드로 예외에 대한 정보를 얻어내고 있다.
"잔고부족: 2000 모자람"은 getMessage() 메소드의 리턴값을 출력한 것이다. printStackTrace() 메소드에 의해 출력된 내용을 보면 21번째 줄에서 최초로 예외가 발생되어 44번째 줄의 메소드 호출 위치로 예외가 떠넘겨졌음을 알 수 있다.

### 사용자 정의 예외

프로그램을 개발하다 보면 자바 표준 API에서 제공하는 예외 클래스만으로는 다양한 종류의 예외를 표현할 수가 없다. 예를 들면 위의 <a href="#AccountPro" class="scroll">Account계좌 프로그램</a>에서 잔고보다 더 많은 출금 요청이 들어왔을 경우 오류가 되며, 프로그램은 잔고 부족 예외를 발생시킬 필요가 있는데, 잔고 부족 예외는 자바 표준 API에는 존재하지 않는다. 따라서 이런 경우 우리가 직접 만들어 줄 필요가 있는데 이 때 사용하는 것이 바로 사용자 정의 예외다.


사용자 정의 예외 클래스는 컴파일러가 체크하는 일반 예외로 선언할 수도 있고, 컴파일러가 체크하지 않는 실행 예외로 선언할 수도 있다. **일반 예외** 로 선언할 경우 Exception을 상속하면 되고, **실행 예외** 로 선언할 경우에는 RuntimeException을 상속하면 된다.


```java
public class XXXException extends [ Exception | RuntimeException ] {
  public XXXException() { }
  public XXXException(String message) {
    super(message);
  }
}
```



사용자 정의 예외 클래스 이름은 Exception으로 끝나는 것이 좋다. 사용자 정의 예외 클래스도 필드, 생성자, 메소드 선언들을 포함할 수 있지만 대부분 생성자 선언만을 포함한다. 생성자는 두 개를 선언하는 것이 일반적인데, 하나는 매개 변수가 없는 기본 생성자이고, 다른 하나는 예외 발생 원인(예외 메시지)을 전달하기 위해 String 타입의 매개 변수를 갖는 생성자이다. String 타입의 매개 변수를 갖는 생성자는 상위 클래스의 생성자를 호출하여 예외 메시지를 넘겨준다. 예외 메시지의 용도는 catch{ } 블록의 예외 처리 코드에서 이용하기 위해서이다.
