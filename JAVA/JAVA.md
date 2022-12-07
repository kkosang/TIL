# _2022-10-31 MON_

## <em> 변수의 scope와 static </em>

- 변수의 스코프
  - 변수들은 사용 가능한 범위를 가지는데, 그 범위를 변수의 스코프라고 함

```java
public class ValScopeExam{
    int globalScope = 10; // 인스턴스 변수

    public void scopeTest(int value){
        int localScope =10;
        System.out.println(globalScope);
        System.out.println(localScope);
        System.out.println(value);
    }
}
// 클래스 속성으로 선언된 globalScope 의 스코프는 클래스 전체
// 매개변수로 선언된 value 의 스코프는 메소드 블럭내
// 메소드 블럭내에서 선언된 localScope 의 스코프는 메소드 블럭내
```

- static한 main 메소드에서 사용하기
  - 같은 클래스지만, globalScope 사용 불가
  - static한 메소드에서는 static 하지 않은 필드 사용 불가

```java
    public class VariableScopeExam {
        int globalScope = 10;

        public void scopeTest(int value){
            int localScope = 20;
            System.out.println(globalScope);
            System.out.println(localScope);
            System.out.println(value);
        }
        public static void main(String[] args) { // static 메소드
            System.out.println(globalScope);  //오류
            System.out.println(localScope);   //오류
            System.out.println(value);        //오류
        }
    }
```

## <em> 열거형 (enum) </em>

- 열거타입을 이용하여 변수를 선언할 때 변수타입으로 사용 가능
- 열거형 정의 방법

```java
    enum Gender{
        MALE, FEMALE;
    }
```

- 열거형 사용 방법

```java
    Gender gender2;

    gender2 = Gender.MALE;
    gender2 = Gender.FEMALE;

    // Gender타입의 변수에는 MALE이나 FEMALE만 대입이 가능
    // 특정 값만 대입하고 싶을 때 열거형 사용
```

## <em> 생성자 </em>

- 모든 클래스는 인스턴스화 될때 생성자를 사용한다
- 생성자의 특징
  - 생성자는 리턴타입이 없음
  - 생성자를 프로그래머가 만들지 않으면 매개변수가 없는 생성자가 컴파일할 때 자동으로 만들어짐
  - 매개변수가 없는 생성자를 기본생성자라고 함
  - 생성자를 하나라도 만들었다면, 기본생성자는 자동으로 만들어지지 않음
  - 클래스명과 같은 메소드로 인스턴스화 될때 자동으로 호출하는 특수한 메소드

```java
 public class Car{
        String name;
        int number;

        public Car(String n){
            name = n;
        }
    }
```

## <em> this </em>

- 현재 객체, 자기 자신을 나타냄

```java
 public Car(String name){
        name = name;
    }
// name=name은 가깝게 선언된 변수를 우선 사용하기에, 매개변수 name의 값을 매개변수 name에 대입하라는 의미가 됨
// 컴파일러와 JVM에게 알려주기 위해서 this라는 키워드를 사용
```

```java
    public Car(String name){
        this.name = name;
    }
// this.name은 현재 필드의 name을 말하고 뒤의 name은 매개변수를 의미
```

- 클래스 안에서 자기 자신이 가지고 있는 메소드를 사용할 때도 this.메소드명()으로 호출 가능

## <em> 메소드 오버로딩 </em>

- 매개변수의 유형과 개수를 다르게 하여 같은 이름으로 여러개의 메소드를 정의함
- 메소드 오버로딩

```java
    class MyClass2{
        public int plus(int x, int y){
            return x+y;
        }

        public int plus(int x, int y, int z){
            return x + y + z;
        }

        public String plus(String x, String y){
            return x + y;
        }

        public int plus(int i, int f){ // 맨위의 메소드와 동일함, 변수명만 다른건 허용 X
        return i+f;
        }
    }
```

## <em> 생성자 오버로딩과 this </em>

- 생성자도 매개변수의 유형과 개수를 다르게 하여 같은 이름으로 여러개의 메소드를 정의함

```java
  public class Car{
        String name;
        int number;

        public Car(){

        }

        public Car(String name){
            this.name = name;
        }

        public Car(String name, int number){
            this.name = name;
            this.number = number;
        }
    }
```

- 자기 생성자를 호출하는 this()
  - 기본생성자를 호출하였을 때 name을 "이름없음",숫자를 0으로 초기화

```java
  public Car(){
        this.name = "이름없음";
        this.number = 0;
    }
```

    - 위처럼 작성했을 경우 코드의 중복 발생
    - this를 이용하여 다른 생성자 호출

```java
 public Car(){
    this("이름없음",0); // 자기 자신의 생성자 호출하여 코드중복 방지
 }
```

# _2022-11-01 TUE_

## <em> 패키지 </em>

- 패키지 정의

  - 패키지란 서로 관련 있는 클래스 또는 인터페이스들을 묶어 놓음
  - 클래스를 패키지 이름과 함께 계층적인 형태로 사용함으로써 다른 그룹에 속한 클래스와 발생할 수 있는 클래스 이름간의 충돌을 막아서 클래스의 관리를 편하게 해줌

- 패키지 정의방법
  - package이름은 도메인 이름을 거꾸로 적은 후, 그 뒤에 프로젝트 이름을 붙여서 만듬
  - 도메인 이름이 8cruz.com이고 프로젝트 이름이 javastudy라면, com.eightcruz.javastudy.Hello로 패키지 지정

## <em> 상속 </em>

- 부모 클래스가 자식 클래에게 물려주는것을 의미
- Car 를 상속받은 Bus를 class로 표현하는 방법

  ```java
      public class Car{
       public void run(){
              System.out.println("달리다.");
          }
      }

      public class Bus extends Car{

      }
      // 클래스 이름 뒤에 extends 키워드를 적고 부모클래스 이름을 적으면 상속
      // 자식클래스(Bus)는 부모클래스(Car)가 가지고 있는 것을 사용할 수 있음
  ```

- Car를 상속받은 Bus 사용

  ```java
    public class BusExam{
          public static void main(String args[]){
              Bus bus = new Bus();
              bus.run();
              // Bus 클래스에는 아무런 코드를 가지지 않지만, 그럼에도 run 이라는 메소드를 사용하는데 문제가 발생되지 않음
          }
      }
  ```

## <em> 접근제한자 </em>

- 접근제한자란 클래스 내에서 멤버의 접근을 제한하는 역할
- 접근제한자의 종류
  - public : 어떤 클래스든 접근할 수 있음
  - default(접근제한자를 적지 않음) : 자기자신과 같은 패키지에서만 접근할 수 있음
  - protected : 같은패키지, 다른 패키지여도 상속 받은 자식 클래스에서는 접근할 수 있음
  - private : 자기 자신만 접근할 수 있음

```java
    public class AccessObj{
        private int i = 1;
        int k = 2; // default접근 제한자
        public int p = 3;
        protected int p2 = 4;
    }
```

## <em> 추상클래스 </em>

- 추상 클래스란 구체적이지 않은 클래스를 의미
- 새,포유류 처럼 구현한 클래스를 추상 클래스라고 함
- 추상 클래스 정의
  - 클래스 앞에 abstract 키워드 이용
  - 추상 클래는 미완성의 추상 메소드를 포함할 수 있음
    - 추상 메소드란, 내용이 없는 메소드 즉, 구현되지 않은 메소드
    - 리턴 타입 앞에 abstract 키워드를 붙여야 함
  - 추상 클래스는 인스턴스를 생성할 수 없음

```java
    public abstract class Bird{
        public abstract void sing();

        public void fly(){
            System.out.println("날다.");
        }
    }
```

- 추상 클래스를 상속받는 클래스 생성
  - 추상 클래스를 상속받은 클래스는 추상 클래스가 갖고 있는 추상 메소드를 반드시 구현
  - 추상 클래스를 상속받고, 추상 클래스가 갖고 있는 추상 메소드를 구현하지 않으면 해당 클래스도 추상 클래스가 된다

```java
    public class Duck extends Bird{
        @Override
        public void sing() {
            System.out.println("꽥꽥!!");
        }
    }
```

- 사용

  ```java
      public class DuckExam {
          public static void main(String[] args) {
              Duck duck = new Duck();
              duck.sing();
              duck.fly();

              //Bird b = new Bird();
          }
      }
      // Bird는 추상 클래스 이므로 객체를 생성할 수 없음
  ```

## <em> super와 부모생성자 </em>

- class가 인스턴스화 될때 생성자가 실행되면서 객체의 초기화를 함
- 만약 부모 클래스가 있다면 자신의 생성자만 실행되는것이 아니고, 부모의 생성자 -> 자식의 생성자 실행됨
- 부모 생성자

  ```java
      public class Car{
          public Car(){
              System.out.println("Car의 기본생성자입니다.");
          }
      }

      public class Bus extends Car{
          public Bus(){
              System.out.println("Bus의 기본생성자입니다.");
          }

      }
  ```

- 생성자 테스트

  ```java
      public class BusExam{
          public static void main(String args[]){
              Bus b = new Bus(); // 자식클래스로 인스턴스화
          }
      }
  ```

- 결과

  ```java
  Car의 기본생성자입니다.
  Bus의 기본생성자입니다.
  ```

- new 연산자로 Bus 객체를 생성하면, Bus 객체가 메모리에 올라가기전에 부모인 Car도 함께 메모리에 올라감
- 생성자는 객체를 초기화 하는 일을 함
- 생성자가 호출될 때 자동으로 부모의 생성자 호출되면서 부모 객체를 초기화 함

- super

  - 자신을 가리키는 키워드가 this라면, 부모를 가리키는 키워드는 super임
  - super()는 부모의 생성자를 의미함
  - 부모의 생성자를 임의로 호출하지 않으면, 부모 class의 기본 생성자가 자동으로 호출됨

  ```java
    public Bus(){
    super(); // 없어도 자동으로 부모의 기본 생성자 호출
    System.out.println("Bus의 기본생성자입니다.");
    }
  ```

- 부모의 기본생성자가 아닌 다른 생성자 호출 방법
  ```java
      public class Car{
      public Car(String name){
          System.out.println(name + " 을 받아들이는 생성자입니다.");
      }
  }
  ```
- Car class가 수정되면, 부모의 기본생성자가 없기 때문에 Bus 생성자에서 컴파일 오류
- 해결하기 위해, 자식 클래스의 생성자에서 직접 부모의 생성자를 호출
  ```java
      public Bus(){
          super("소방차"); // 문자열을 매개변수로 받는 부모 생성자를 호출하였다.
          System.out.println("Bus의 기본생성자입니다.");
      }
  ```

## <em> 오버라이딩 </em>

- 부모가 가지고 있는 메소드와 똑같은 모양의 메소드를 자식이 가지고 있음
- 부모의 메소드를 자식의 메소드에서 재정의 함
- 메소드 오버라이딩

  - Car 클래스를 상속받은 Bus 클래스는 부모클래스가 가지고 있는 run() 메소드를 사용

    ```java
        //run 메소드를 가지고 있는  Car클래스
    public class Car{
        public void run(){
            System.out.println("Car의 run메소드");
        }
    }

    //Car 를 상속받는 Bus 클래스
    public class Bus extends Car{

    }

    public class BusExam{
      public static void main(String args[]){
          Bus bus = new Bus();
          bus.run();  //Car의 run메소드가 실행
      }
    }
    ```

  - Bus클래스에 부모가 가지고 있는 메소드와 모양이 같은 메소드 선언

    ```java
    public class Bus extends Car{
    public void run(){
    System.out.println("Bus의 run메소드");
    }
    }

    public class BusExam{
    public static void main(String args[]){
    Bus bus = new Bus();
    bus.run(); //Bus run메소드가 실행
    }
    }
    ```

- super 키워드를 이용하여 부모의 메소드도 호출 가능
  ```java
    public class Bus extends Car{
      public void run(){
          super.run(); // 부모의  run()메소드를 호출
          System.out.println("Bus의 run메소드");
      }
  }
  ```

## <em> 클래스 형변환 </em>

- 부모타입으로 자식객체를 참조하게 되면 부모가 가지고 있는 메소드만 사용할 수 있음
- 자식객체가 가지고 있는 메소드나 속성을 사용하고 싶으면 형변환을 해야 함
- 형변환

  ```java
      public class Car{
      public void run(){
          System.out.println("Car의 run메소드");
      }
  }

  public class Bus extends Car{
      public void ppangppang(){
          System.out.println("빵빵.");
      }
  }
  ```

  - 부모타입으로 자식객체 참조

    - 부모타입으로 자식객체를 참조하게 되면 부모가 가지고 있는 메소드만 사용가능

      ```java
       public class BusExam{ public static void main(String args[]){ Car car = new Bus(); // 부모타입으로 자식객체 참조 car.run(); car.ppangppang(); // 컴파일 오류 발생 } } // ppangppang은 자식객체 메소드
      ```

    - ppangppang() 메소드를 호출하고 싶다면 Bus타입의 참조변수로 참조해야 함

      ```java
      public class BusExam{
      public static void main(String args[]){
      Car car = new Bus();
      car.run();
      //car.ppangppang(); // 컴파일 오류 발생

              Bus bus = (Bus)car;  //부모타입을 자식타입으로 형변환
              bus.run();
              bus.ppangppang();
          }

      }
       // 객체들 끼리도 형변환이 가능하지만, 상속관계에 있을때만 가능
       // 부모타입으로 자식타입의 객체를 참조할 때는 묵시적으로 형변환이 일어남
       // 부모타입의 객체를 자식타입으로 참조할 때는 명시적으로 형변환 해줘야 함
      ```

# _2022-11-08 TUE_

## <em> 인터페이스 만들기 </em>

- 서로 관계가 없는 물체들이 상호 작용을 하기 위해서 사용하는 장치나 시스템
- 인터페이스 정의

  - 추상 메소드와 상수를 정의

  ```java
  public interface TV{
    public int MAX_VOLUME = 100;
    public int MIN_VOLUME = 0;

    public void turnOn();
    public void turnOff();
    public void changeVolume(int volume);
    public void changeChannel(int channel);

  }
  // 인터페이스에서 변수를 선언하면 컴파일시 자동으로
    public static final int MAX_VOLUME = 100;
    public static final int MIN_VOLUME = 0;

  // 인터페이스에서 정의된 메소드는 모두 추상 메소드임 위에서 선언된 메소드는 컴파일시 자동으로
    public abstract void  turnOn();
    public abstract void turnOff();
    public abstract void changeVolume(int volume);
    public abstract void changeChannel(int channel);
  ```

## <em> 인터페이스 사용하기 </em>

- 인터페이스를 구현하는 클래스에서 implements 키워드 사용
  ```java
     public class LedTV implements TV{
        public void on(){
            System.out.println("켜다");
        }
        public void off(){
            System.out.println("끄다");
        }
        public void volume(int value){
            System.out.println(value + "로 볼륨조정하다.");
        }
        public void channel(int number){
            System.out.println(number + "로 채널조정하다.");
        }
    }
  ```

## <em> 인터페이스의 default method </em>

- default 메소드

  - 인터페이스가 default 키워드로 선언되면 메소드가 구현될 수 있음
  - 원래는 추상 메소드이므로 구현 불가능
  - 구현하는 클래스는 default 메소드를 오버라이딩 할 수 있음

  ```java
  public interface Calculator{
    public int plus(int i,int j);
    public int multiple(int i,int j ); // 추상메소드이므로 구현은 불가

    default int exec(int i,int j){ // default 메소드로 구현가능
        return i+j;
    }

    //Calculator 인터페이스를 구현한 MyCalculator class
    public class MyCalculator implements Calculator{
        @override
        public int plus(int i, int j){
            return i+j;
        }

        @override
        public int multiple(int i, int j){
            return i*j;
        }
    }

    public class MyCalculator{
        public static void main(String[] args){
            Calculator cal = new MyCalculator; // 참조타입으로 인터페이스
            int value = cal.exec(5,10);
            System.out.println(value);
        }
    }
  }
  // 인터페이스가 변경되면, 인터페이스를 구현하는 모든 클래스들이 해당 메소드를 구현해야하는 문제가 있음 => static 메소드 선언으로 해결
  ```

- static 메소드

  ```java
  public interface Calculator{
    public int plus(int i, int j);
    public int multiple(int i, int j);
    default int exec(int i,int j){
        return i+j;
    }
    public static int exec2(int i,int j){ // static 메소드
    return i*j;

    }
  }

    public class MyCalculatorExam {
        public static void main(String[] args){
            Calculator cal = new MyCalculator();
            int value = cal.exec(5, 10);
            System.out.println(value);

            int value2 = Calculator.exec2(5, 10);  //static메소드 호출
            System.out.println(value2);
        }
        // 인터페이스에서 정의한 static 메소드는 반드시 인터페이스명.메소드 형식으로 호출해야함
    }
  ```

## <em> 내부클래스 </em>

- 내부 클래스란 클래스 안에 선언된 클래스

  - 첫번째, 클래스 안에 인스턴스 변수, 즉 필드를 선언하는 위치에 선언되는 경우
    - 중첩클래스 or 인스턴스 클래스라고 함
    - 내부에 있는 Cal 객체를 생성하기 위해서는, 밖에 있는 innerExam1의 객체를 만든 후에 innerExam1.Cal cal = t.new Cal();와 같은 방법으로 Cal 객체를 생성 후 사용
    ```java
    public class InnerExam1{
        class Cal{
            int value= 0;
            public void plus(){
                value++;
            }
        }
        public static void main(String args[]){
            InnerExam1 t = new InnerExam1(); // InnerExam1의 객체 생성
            InnerExam1.Cal cal = t.new Cal(); // Cal 객체를 생성
            cal.plus();
            System.out.println(cal.value);
        }
    }
    ```
  - 두번째, 내부 클래스가 static으로 정의된 경우

    - 정적 중첩 클래스 or static 클래스라고 함
    - 필드 선언시 스태틱한 필드로 선언한 것과 같음
    - InnerExam2 객체를 생성할 필요없이 new InnerExam2.Cal()로 객체를 생성할 수 있음

    ```java
    public class InnerExam2{
     static class Cal{
         int value =0;
         public void plus(){
             value++;
         }
     }

     public static void main(String args[]){
         InnerExam2.Cal cal = new InnerExam2.Cal();
         cal.plus();
         System.out.println(cal.value);
     }
    }
    ```

  - 세번째, 메소드 안에 클래스를 선언한 경우

    - 지역 중첩 클래스 or 지역 클래스
    - 메소드 안에서 해당 클래스를 이용

    ```java
        public class InnerExam3{
        public void exec(){
            class Cal{
                int value = 0;
                public void plus(){
                    value++;
                }
            }
            Cal cal = new Cal();
            cal.plus();
            System.out.println(cal.value);
        }


        public static void main(String args[]){
            InnerExam3 t = new InnerExam3();
            t.exec();
        }
    }
    ```

  - 네번째, 익명클래스

    - 익명 중첩 클래스는 익명 클래스라고 말하며, 내부 클래스이기도 하다

    ```java
    // 추상클래스 Action
    public abstract class Action{
        public abstract void exec();
    }

    // 추상클래스 Action을 상속받은 클래스 MyAction
    public class MyAction extends Action{
        public void exec(){
            System.out.println("exec");
        }
    }

    // MyAction을 사용하는 클래스 ActionExam
    public class ActionExam{
        public static void main(String args[]){
            Action action = new MyAction();
            action.exec();
        }
    }

    // MyAction을 사용하지 않고 Action을 상속받는 익명 클래스를 만들어서 사용함
    public class ActionExam{
        public static void main(String args[]){
            Action action = new Action(){
                public void exec(){
                    System.out.println("exec");
                }
            };
            action.exec();
        }
    }
    ```

    - 생생성자 다음에 중괄호 열고 닫고가 나오면, 해당 생성자 이름에 해당하는 클래스를 상속받는 이름없는 객체를 만든다는 것을 뜻함
    - 괄호 안에는 메소드를 구현하거나 메소드를 추가할 수 있다. 이렇게 생성된 이름 없는 객체를 action이라는 참조변수가 참조하도록 하고, exec()메소드를 호출함
    - 익명클래스를 만드는 이유는 Action을 상속받는 클래스를 만들 필요가 없을 경우
    - Action을 상속받는 클래스가 해당 클래스에서만 사용되고 다른 클래스에서는 사용되지 않는 경우

# _2022-12-07 WED_

## <em> Exception </em>

- 프로그램 실행 중 예기치 못한 사건을 예외라고 함
- 예외 상황을 미리 예측하고 처리하는 것을 예외 처리라고 함

  ```java
      public class ExceptionExam {
      public static void main(String[] args) {
          int i = 10;
          int j = 5;
          int k = i / j;
          System.out.println(k);
          System.out.println(main 종료!!);
      }
  }
  // j를 0으로 바꾸면 Exception 발생
  // j를 0으로 바꾸면 ArithmeticException 발생하면서 프로그램 종료
  // 정수를 정수로 나눌 때 0으로 나누면 오류 발생

  ```

- 예외처리하는 문법
  - 오류가 발생할 예상 부분을 try{} 블록으로 감싼 후, 발생할 오류와 관련된 Exception을 catch라는 블록에서 처리함
  - 오류와 상관없이 무조건 실행되는 finally라는 블록을 가질 수 있음
  - finally{}는 생략가능

```java
     public class ExceptionExam {
        public static void main(String[] args) {
            int i = 10;
            int j = 0;
            try{
                int k = i / j;
                System.out.println(k);
            }catch(ArithmeticException e){
                System.out.println("0으로 나눌 수 없습니다. : " + e.toString());
            }finally {
                System.out.println("오류가 발생하든 안하든 무조건 실행되는 블록입니다.");
            }
        }
    }
    // 실행결과 : 0으로 나눌 수 없습니다 와 finally {} 블록
```

- 예외처리를 하지 않으면 프로그램 강제 종료
- try{}에서 여러종류의 Exception이 발생한다면 catch{}을 여러개 둘 수 있음
- Exception클래스들은 모두 Exception클래스를 상속받으므로, 예외클래스에 Exception을 두게 되면 어떤 오류가 발생하든지 간에 하나의 catch블록에서 모든 오류처리 가능
