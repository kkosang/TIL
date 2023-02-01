# _2023-02-01 WED_

## <em> Annotation? </em>

- annotation의 사전적 정의는 주석
- 나 또는 다른사람이 코드를 보았을때 무슨 코드인지 알아보기 쉽도록 돕기 위함
- 차이점이 있다면, 어노테이션은 사람에게 정보를 제공하기 위함이 아닌 프로그램에게 정보를 제공해주는 메타데이터 역할
- 어노테이션은 클래스나 메소드위에 붙음
- @(at)기호로 이름이 시작됨
- 어노테이션은 자바가 기본으로 제공해주는 것도 있고(JDK 1.5 버전이상), 사용자가 직접 만들 수도 있음

## <em> Annotation의 용도 </em>

- 컴파일러에게 코드 작성 문법 에러를 체크 하도록 정보 제공
- 개발자들이 빌드나 배치시 코드를 자동으로 생성할 수 있도록 정보 제공
- 런타임시 특정 기능을 실행하도록 정보 제공

## <em> Annotation의 종류 </em>

- 내장 어노테이션

  - @Override
    - 선언한 메서드가 오버라이드 되었다는 것을 나타냄
    - 상위 클래스에서 해당 메서드를 찾을 수 없다면 컴파일 에러 발생
  - @Deprecated
    - 해당 메서드가 더 이상 사용되지 않음
    - 사용시 컴파일 경고 발생
    - 하위 호환성을 위해서 Deprecated로 선언하는 것은 꼭 필요
  - @SuppressWarnings
    - 선언한 곳의 컴파일 경고를 무시하도록 함

- 메타 어노테이션

  - @Retention
    - 얼마나 오래 어노테이션 정보가 유지되는지, 즉 특정 시점까지 영향을 미치는지 결정
    ```java
        @Retention(Retention.Policy.RUNTIME)
    ```
    - 요소타입
      - SOURCE : 어노테이션 정보가 컴파일시 사라짐
      - CLASS : 클래스 파일에 있는 어노테이션 정보가 컴파일러에 의해서 참조 가능함, 하지만 JVM에서는 사라짐
      - RUNTIME : 실행시 어노테이션 정보가 JVM에 의해서 참조 가능
  - @Documented
    - 해당 어노테이션에 대한 정보가 Javadocs(API) 문서에 포함된다는 것을 선언
  - @Target
    - 어노테이션을 어떤 것에 적용할지 선언할 때 사용
    ```java
        @Target(ElementType.METHOD)
    ```
    - 요소타입
      - CONSTRUCTOR : 생성자 선언시
      - FIELD : enum 상수를 포함한 필드값 선언시
      - LOCAL_VARIABLE : 지역 변수 선언시
      - METHOD : 메소드 선언시
      - PACKAGE : 패키지 선선이
      - PARAMETER : 매개 변수 선언시
      - TYPE : 클래스, 인터페이스, enum 등 선언시
  - @Inherited
    - 모든 클래스에서 부모 클래스의 어노테이션을 사용 가능하다는것을 선언
  - @Repeatable
    - Java8부터 지원하며, 연속적으로 어노테이션을 선언할 수 있게 함

## <em> Custom Annotation </em>

- 사용자가 직접 작성하는 어노테이션을 Custom Annotation이라고 함
- 커스텀 어노테이션 이용방법

  - 어노테이션 정의
  - 어노테이션을 클래스에서 사용(타겟에 적용)
  - 어노테이션 실행

- 패키지 익스플로러에서 [new-Annotation]을 이용하여 Count100이라는 어노테이션 생성

  - Count100 어노테이션을 JVM실행시 감지할 수 있도록 하려면, 어노테이션을 정의한 부분에 @Retention(RetentionPolicy.RUNTIME)를 붙여줘야 함

  ```java
    import java.lang.annotation.Retention;
    import java.lang.annotation.Retention.Policy;

    @Retention(RetentionPolicy.RUNTIME)
    public @interface Count100{

    }
  ```

  - "hello"를 출력하는 hello()메소드를 가지는 MyHello라는 클래스 작성
    - 타겟 메소드(hello메소드)위에 @Count100 어노테이션을 붙임

  ```java
    public class MyHello(){
        @Count100
        public void hello(){
            System.out.println("hello");
        }
    }
  ```

  - MyHello클래스를 이용하는 MyHelloExam클래스 작성
    - MyHello의 hello메소드가 @Count100어노테이션이 설정되어 있을 경우, hello()메소드를 100번 호출하도록 함

  ```java
    import java.lang.reflect.Method;

    public class MyHello(){
        public static void main(String[] args){
            MyHello hello = new MyHello();

            try{
                // 메서드에 대한 정보 얻기
                Method method = hello.getClass().getDeclaredMethod("hello"); // getClass로부터 클래스에 대한 정보를 얻고, hello란 이름에 대한 메서드를 얻어옴
                if(method.isAnnotationPresent(Count100.class)){ // 특정 어노테이션(Count100)이 method에 적용이 되어 있는지 알아내기 위함
                    for(int i=0; i<100; i++)
                        hello.hello();
                    else
                        hello.hello();
                }
            }catch(Exception ex){
                ex.printStackTrace();
            }
        }
    }
  ```
