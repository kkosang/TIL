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
