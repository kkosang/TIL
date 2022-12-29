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

# _2022-12-09 FRI_

## <em> Throws </em>

- 예외가 발생했을 때 method내에서가 아니라 호출한 쪽에서 처리하도록 함

```java
    public class ExceptionExam2 {
        public static void main (String[] args){
            int i=10;
            int j=0;
            int k = divide(i,j);
            System.out.println(k);
        }

        public static int divide(int i,int j) throws ArithmeticException{
            int k= i/j;
            return k;
        }
        // divide메소드는 ArithmeticException이 발생하니 divide메소드를 호출하는 쪽에서 오류를 처리
    }
```

```java
    package javaStudy;
    public class ExceptionExam2 {

        public static void main(String[] args) {
            int i = 10;
            int j = 0;
            try{
                int k = divide(i, j);
                System.out.println(k);
            } catch(ArithmeticException e){
                System.out.println("0으로 나눌수 없습니다.");
            }

        }

        public static int divide(int i, int j) throws ArithmeticException{
            int k = i / j;
            return k;
        }

    }
```

## <em> Exception 발생시키기 </em>

- 강제로 오류를 발생시키는 throw
- throw는 오류를 떠넘기는 throws와 보통 같이 사용

```java
    public class ExceptionExam3 {
        public static void main(String args[]){
            int i=10;
            int j=0;
            int k = divide(i,j);
            System.out.println(k);
        }
        public static int divide(int i,int j){
            if(j==0){
                System.out.println("2번째 매개변수가 0일 수 없습니다");
                return 0;
            }
            int k=i/j;
            return k;
        }
        // k변수의 값은 0
        // 0으로 나눈 결과는 0이 아님
    }
```

```java
    // 오류를 발생하지 않고, 올바른 결과를 리턴
    public class ExceptionExam3{
        public static void main(String[] args){
            int i=10;
            int j =0;
            int k = divide(i,j);
        }
        public static int divide(int i, int j) throws IllegalArgumentException{
            if(j==0)
            {
                throw new IllegalArgumentException("0으로 나눌 수 없음");
            }
            int k= i/j;
            return k;
        }
    }
    // j가 0일 경우에 new 연산자를 통해 IllegalArgumentException 객체 만들어짐
    // new 앞에 throw는 해당 라인에서 익셉션이 발생한다는 의미
    // 익셉션 클래스 이름을 통해 Argument가 잘못되어서 발생한 오류라는 것을 알 수 있음

```

```java
    // divide 메소드를 호출 한 쪽에서 오류처리
          public static void main(String[] args) {
            int i = 10;
            int j = 0;
            try{
                int k = divide(i, j);
                System.out.println(k);
            }catch(IllegalArgumentException e){
                System.out.println("0으로 나누면 안됩니다.");
            }
        }
```

## <em> 사용자 정의 Exception </em>

- Exception 클래스를 상속 받아 정의한 checked Exception
  - 반드시 오류 처리를 해야만 하는 Exception
  - 예외 처리를 하지 않으면 컴파일 오류 발생
- RuntimeException 클래스를 상속 받아 정의한 unChecked Exception

  - 예외 처리를 하지 않아도 컴파일 시에는 오류를 발생시키지 않음

- RuntimeException을 상속받은 BizException 객체

  ```java
      public class BizException extends RuntimeException{
          // 생성자 2개
          public BizException(String msg){
              super(msg);
          }
          public BizException(Exception ex){
              super(ex);
          }
      }
  ```

- BizService클래스는 업무를 처리하는 메소드를 가지고 있다고 가정

  ```java
      public class BizService{
          public void bizMethod(int i) throws BizException{
            System.out.println("로직 시작");
          if(i<0)
              throw new BizException("매개변수 i는 0이상이어야 함");
          System.out.println("로직 종료");
          }
      }
  ```

- BizService를 이용하는 BizExam 클래스
  ```java
  public class BizExam{
      public static void main(String[] args){
          BizService biz = new BizService();
          biz.bizMethod(5);
          try(
              biz.bizMethod(-3);
          )catch(Exception ex){
              ex.printStackTrace();
          }
      }
  }
  ```

# _2022-12-12 MON_

## <em> Object와 오버라이딩 </em>

- Object클래스는 모든 클래스의 최상위 클래스
- 아무것도 상속받지 않으면 자동으로 Object를 상속
- Object가 가지고 있는 메소드는 모든 클래스에서 다 사용할 수 있음
- 일반적으로 객체를 출력할 때는 Object의 toString(); 사용

## <em> java.lang패키지와 오토박싱/언박싱 </em>

- java.lang패키지의 클래스는 import하지 않고도 사용 가능
- java.lang패키지에는 기본형 타입을 -> 객체로 변환시킬 때 사용하는 Wrapper 클래스가 있음
  - Boolean, Byte, Short, Integer, Long, Float, Double
- 모든 클래스의 최상위 클래스인 Object도 java.lang 패키지
- 문자열과 관련된 String, StringBuffer, StringBuilder도 모두 java.lang패키지
- System클래스도 java.lang패키지
- Math클래스도 java.lang패키지
- Thread와 관련된 중요 클래스들이 java.lang패키지
- 이외에도 다양한 클래스와 인터페이가 java.lang패키지에 속함

```java
    public class WrapperExam{
        public static void main(String[] args){
            int i =5;
            Integer i2 = new Integer(5); // 숫자 5를 Integer형태로 형변환
            Integer i3 =5 ; // 오토박싱
            int i4 = i2.intValue();
            int i5 = i2; // 오토 언박싱

        }
    }
    // Auto Boxing : 기본형 숫자 5를 자동으로 Integer형태로 변환
    // Auto unBoxing : Integer객체타입의 값을 기본형 int 로 자동 변환

```

## <em> 스트링버퍼 클래스 </em>

- 아무 값도 가지고 있지 않은 StringBuffer 객체를 생성

  ```java
    StringBuffer sb = new StringBuffer();

    // 해당 스트링 버퍼에 "hello", 공백, "world"를 차례로 추가

    sb.append("hello");
    sb.append(" ");
    sb.append("world");

    // StringBuffer에 추가된 값을 toString() 메소드를 이용하여 반환

    String str = sb.toString();

    // 출력결과 : hello world
  ```

- StringBuffer가 가지고 있는 메소드들은 대부분 자기 자신, this를 반환
  ```java
    StringBuffer sb2 = new StringBuffer();
    StringBuffer sb3 = sb2.append("hello");
    if(sb2==sb3){
        System.out.println("sb2==sb3");
    }
  ```
  - 자기 자신의 메소드를 호출하여 자기 자신을 return하여 값을 바꿔 나가는것을 메소드체이닝이라고 한다
  - StringBuffer클래스는 메소드 체인 방식으로 사용가능
    ```java
    String str2 = new StringBuffer().append("hello").append(" ").append("world").toString();
    System.out.println(str2);
    ```

## <em> 스트링 클래스의 문제점 </em>

- String 클래스는 문자열을 다룰 때 사용하는 클래스
- String 클래스는 불변클래스이다

```java
    String str1 = "hello world";
    String str2 = str1.substring(5);
    System.out.println(str1);
    System.out.println(str2);

    // 출력 결과
    hello world
     world
    // 기존의 str1은 전혀 변화 없음
    // substring은 5번째부터 문자열 잘라서 새로운 문자열 반환
```

```java
    String str3 = str1 + str2;
    System.out.println(str3);

    // 새로운 문자열을 만들어서 (new) 반환하기 때문에 성능상 문제
```

- 문자열과 문자열을 더하게 되면 내부적으로는 다음과 같은 코드 실행

```java
    String str4 = new StringBuffer().append
    (str1).append(str2).toString();

    // 반복문을 사용할 경우,
    // 매번 new 를 사용해서 String 객체를 만들어 내기 때문에 속도가 느려짐
```

- 문자열을 반복문 안에서 더하는 것은 성능상 문제가 생길 수 있음

## <em> Math 클래스 </em>

- 수학계산을 위한 클래스
- cos, sin, tan, abs, random등의 메소드가 있음
- Math 클래스는 생성자가 private으로 되어 있기 때문에 new 연산자를 이용하여 객체 생성 불가
- 객체를 생성할 수는 없지만 모든 메소드와 속성이 static으로 정의되어 있어 객체를 생성하지 않고 바로 사용 가능

```java
    public class MathExam{
        public static void main(String[] args){
            int val1 = Math.max(5,20);
            int val2 = Math.min(5,-5);
            int val3 = Math.abs(-5);
            double val4 = Math.random(); // double형으로 0에서 1.0사이의 랜덤값 return
            double val5 = Math.sqrt(25); // double형으로 제곱근을 return
        }
    }
```

# _2022-12-19 MON_

## <em> java.util 패키지 </em>

- 날짜와 관련된 클래스인 Date, Calendar 클래스
- 자료구조와 관련된 컬렉션 프레임워크와 관련된 인터페이스와 클래스
- deprecated는 더이상 지원하지 않으니 사용 지양
- Date 클래스는 지역화를 지원하지 않음
  - 지역화란 국가별로 현재 날짜와 시간이 다를 수 있는데 그 부분을 지원하지 못함
  - 지역화와 관련된 클래스들은 Locale로 시작되는 이름을 가진 클래스
- List,Set,Collection,Map은 자료구조 즉 컬렉션 프레임워크와 관련된 인터페이스

## <em> 컬렉션 프레임워크 </em>

- java.util 패키지에는 자료를 다룰 수 있는 자료구조 클래스가 다수 존재함, 자료구조 클래스들을 컬렉션 프레임워크라고 함
- 자료구조란 자료를 저장할 수 있는 구조
- 자료구조 클래스들을 컬렉션 프레임워크라고 함
- 컬렉션 프레임워크에서 가장 기본이 되는 interface는 Collection인터페이스
  - Collection인터페이스는 여기에 자료가 있다는 것을 표현
  - 중복도 허용하고, 자료가 저장된 순서도 기억하지 못함
  - 대표적인 메소드는 add(), size(), iterator()
  - Collection은 저장된 자료를 하나씩 꺼낼 수 있는 iterator라는 인터페이스를 반환한다
    - Iterator는 꺼낼것이 있는지 없는지 살펴보는 hasNext()메소드와 하나씩 자료를 꺼낼때 사용하는 next()메소드를 가지고 있음
- Set : 중복을 허용하지 않는 자료구조를 표현하는 인터페이스
  - Collection인터페이스를 상속 받음
  - add() 메소드는 같은 자료가 있으면 false, 없으면 true 반환
- List : 중복은 허용하면서 순서를 기억하는 자료구조
  - Set과 마찬가지로 Collection인터페이스를 상속받음
  - List는 순서를 기억하고 있기 때문에 n번째의 자료를 꺼낼 수 있는 get(int)메소드를 가지고 있음
- Map : Key와 Value를 가지는 자료구조
  - 저장할 때 put()를 이용하여 key와 value를 함께 저장
  - 원하는 값을 꺼낼떄는 key를 매개변수로 받아들이는 get()을 이용하여 값을 꺼냄
  - Map에 저장되어 있는 모든 Key들은 중복값을 가질 수 없음
  - 모든 Key에 대한 정보를 읽어들일 수 있는 Set을 반환하는 KeySet()메소드

## <em> Generic </em>

- Generic을 사용함으로써 선언할때는 가상의 타입으로 선언하고, 사용시에는 구체적인 타입을 설정함으로써 다양한 타입의 클래스를 이용하는 클래스를 만들 수 있음
- 사용시 따로 형변환을 할 필요 없음
- Generic을 사용하는 대표적인 클래스는 컬렉션 프레임워크와 관련된 클래스

- Box Class

  ```java
      public class Box{
          private Object obj;
          public void setObj (Object obj){
              this.obj = obj;
          }
          public Object getObj(){
              return obj;
          }
      }
  ```

- BoxExam Class

  ```java
      public class BoxExam{
          public static void main(String[] args){
              Box box = new Box(); // 객체생성
              box.setObj(new Object());
              Object obj = box.getObj();

              box.setObj("hello"); // Object의 후손 String으로 set
              String str= (String)box.getObj(); // Object로 반환되었기 때문에 String으로 형변환
              System.out.println(str);

              box.setObj(3); // Object의 후손 Integer으로 set
              int value = (int)box.getObj();
              // int로 형변환
              System.out.println(value);
          }
      }
      // Box는 매개변수로 Object를 하나 받아들이고, Object를 반환함
      // Object를 받아들일 수 있다는 것은 Object의 후손이라면 무엇이든 받아들일 수 있음
  ```

- Generic을 이용하여 Box클래스 수정

  ```java
    public class Box<E>{
        private E obj;
        public void setObj(E obj){
            this.obj = obj;
        }

        public E getObj(){
            return obj;
        }
    }
    // <>를 이용하여 제네릭 적용
    // Box는 가상의 클래스 E를 사용한다는 의미
    // Object를 받아들이고, 리턴하던 부분이 E로 변경
    // E는 실제로 존재하는 클래스는 아님
  ```

- Generic을 이용하여 수정한 Box를 이용하는 BoxExam클래스

  ```java
    public class BoxExam{
        public static void main(String[] args){
            Box<Object> box = new Box<>();
            box.setObj = (new Object());
            Object obj = box.getObj();

            Box<String> box2 = new Box<>();
            box2.setObj = ("hello");
            String str = box2.getObj();

            Box<Integer> box3 = new Box<>();
            box3.setObj(3);
            int value = (int )box3.getObj();

        }
    }
    // 참조타입으로 <Object>, <String>, <Integer>
    // Box 인스턴스를 각각 Object,String,Integer로 사용
  ```

## <em> Set </em>

- set은 중복이 없고, 순서도 없는 자료구조
- Hashset과 TreeSet이 있음

```java
    import java.util.HashSet;
    import java.util.Iterator;
    import java.util.Set;

    public class SetExam{
        public static void main(String[] args){
            Set<String> set1 = new HashSet<>(); //제네릭 string타입 선언, set은 static이여서 바로 HashSet<>

            boolean flag1 = set1.add("Ko");
            boolean flag2 = set1.add("Kim");
            boolean flag3 = set1.add("Ko");
            // add()는 return타입으로 boolean, set은 중복이 있을 수 없어 flag3의 값은 false
            System.out.println(set1.size());
            // 중복값을 제외하고 2가 출력

            Iterator<String> iter = set1.iterator();

            while (iter.hasNext()){ // 꺼낼 것이 있으면 true 리턴
                String str = iter.next(); // next()는 하나를 꺼내고, 자동으로 다음것을 참조
                System.out.println(str);

            }
        }
    }
```

# _2022-12-29 THU_

## <em> List </em>

- 배열과 유사하지만 배열은 크기 선언시 변경 불가
- 리스트는 필요에 따라 저장공간 자유
- list의 data는 중복이 있을 수 있고, 순서도 있음
- 따라서 index를 이용할 수 있음

```java
    public class ListExam{
        public static void main (String[] args){
            List<String> list = new ArrayList<>(); // interface list
            list.add("kim");
            list.add("ko");
            list.add("kim");

            System.out.println(list.size());

            for(int i=0; i< list.size(); i++){
                String str = list.get(i);
                System.out.println(str);
            }
        }
    }
```

## <em> Map </em>

- key와 value를 쌍으로 저장하는 자료구조
- key값은 중복이 될 수 없고, value는 중복 될 수 있음

```java
    public class MapExam {
        public static void main (String[] args){
            Map<String,String> map = new HashMap<>(); // generic으로 key값과 value값 모두 string타입인 HashMap 인스턴스를 만듬

            // map에 값을 저장하기 위해 put사용
            map.put("001","ko");
            map.put("002","sang");
            map.put("003", "kim");

            map.put("003","hyun"); // key값은 중복이 될 수 없기에 003, kim이 003 hyun으로 변경

            System.out.println(map.size()); // map의 자료의 수 3이 출력

            // 키 값을 이용해 value 출력하기 위해 get 사용
            System.out.println(map.get("001"));
            System.out.println(map.get("002"));
            System.out.println(map.get("003"));

            // map에 저장된 모든 key들을 Set자료구조로 꺼냄
            Set<String> keys = map.keySet();
            // Set자료구조에 있는 모든 key를 꺼내기 위하여 Iterator를 구함
            Iterator<String> iter = keys.iterator();
            while(iter.hasNext()){
                // key를 꺼냄
                String key = iter.next();
                // key에 해당하는 value를 꺼냄
                String value = map.get(key);
                // key와 value값 출력
                System.out.println( key + ":" + value);
            }
        }
    }

```

## <em> Date </em>

- 날짜와 시간을 구하기 위한 Date클래스
- Date 클래스는 JDK 1.0에 만들어져서 지역화에 대한 부분이 고려되지 않음
- Date 클래스의 대부분 생성자와 메소드가 Deprecated되어 있음
  - 앞으로 지원을 안하거나 문제가 발생 할 수 있으니 사용 x
- 기본 생성자를 이용한 Date클래스 생성
  ```java
    Date date = new Date();
  ```
- toString()을 이용하여 현재 시간을 문자열로 구할 수 있음
  ```java
    System.out.println(date.toString());
  ```
- java.util.SimpleDateFormat 클래스를 이용해서 원하는 형태로 출력
  - yyyy 년 MM 월 , dd 일을 표현
  - hh 시간, mm 분, ss 초, a 오전/오후 표현
  - zzz Time Zone, 한국의 경우 KST로 나옴
  ```java
      SimpleDateFormat ft =  new SimpleDateFormat ("yyyy.MM.dd 'at' hh:mm:ss a zzz");
      System.out.println(ft.format(date));
  ```
- 현재 시간을 long으로 구함
  ```java
    System.out.println(date.getTime());
    // System이 가지고 있는 currentTimeMillis()메소드를 이용해도 됨
    long today = System.currentTimeMillis();
    System.out.println(today);
  ```

## <em> Calendar </em>

- Date의 단점을 해결함
- 생성 방법
  - 추상클래스이다
  - Calendar 클래스에 대한 인스턴스를 생성하려면 getInstance() 메소드를 사용
  - getInstance()메소드는 java.util.GregorianCalendar 인스턴스를 만들어서리턴
  - GregorianCalendar는 Calendar의 자식 클래스임
  ```java
    Calendar cal = Calendar.getInstance();
  ```
- 현재 날짜와 시간 정보
  ```java
      int yyyy = cal.get(Calendar.YEAR);
      int month = cal.get(Calendar.MONTH) + 1; // 월은 0부터 시작합니다.
      int date = cal.get(Calendar.DATE);
      int hour = cal.get(Calendar.HOUR_OF_DAY);
      int minute = cal.get(Calendar.MINUTE);
  ```
- 원하는 날짜나 시간 정보
  - add사용
  ```java
    cal.add(Calendar.HOUR,5); // -5는 5시간전
  ```

## <em> java.time 패키지 </em>

- 새롭게 재 디자인한 Date,Time API를 Java SE 8부터 제공
- 새로운 API의 핵심 클래스는 오브젝트를 생성하기 위해 다양한 factory 메서드를 사용
- 오브젝트 자기 자신의 특정 요소를 가지고 오브젝트를 생성할 경우 of 메서드를 호출, 다른 타입으로 변경할 경우에는 from 메서드 호출
- LocalDateTime 클래스를 이용해서 현재 시간 time 객체 만드는 방법
  ```java
    LocalDateTime timePoint = LocalDateTime.now(); // 현재의 날짜와 시간 now는 현재 시간을 구한다
  ```
- 원하는 시간으로 time 객체 생성 방법

  ```java
    // 2022년 12월 22일의 시간에 대한 정보를 가지는 LocalDate객체를 만드는 방법
    LocalDate ld1 = LocalDate.of(2022, Month.DECEMBER, 22); // 2022-12-22 from values

        // 17시 18분에 대한 LocalTime객체를 구함
    LocalTime lt1 = LocalTime.of(17, 18); // 17:18 (17시 18분)the train I took home today

    // 10시 15분 30초라는 문자열에 대한 LocalTime객체를 구함
    LocalTime lt2 = LocalTime.parse("10:15:30"); // From a String
  ```

- 현재와 날짜와 시간 정보를 getter메소드를 이용하는 방법
  ```java
    LocalDate theDate = timePoint.toLocalDate();
    Month month = timePoint.getMonth();
    int day = timePoint.getDayOfMonth();
    int hour = timePoint.getHour();
    int minute = timePoint.getMinute();
    int second = timePoint.getSecond();
    // 달을 숫자로 출력한다 1월도 1부터 시작하는 것을 알 수 있음
    System.out.println(month.getValue() + "/" + day + "  " + hour + ":" + minute + ":" + second);
  ```
