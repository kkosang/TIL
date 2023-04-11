# <em> StringBuffer와 StringBuilder </em>

- StringBuffer와 StringBuilder는 문자열을 변경하고 관리하는 클래스이다.
- 자바에서 String이외에도 StringBuffer와 StringBuilder가 있다.
- String은 불변(immutable)하기 때문에 값을 변경할 수 없다.
  - .concat이나 +를 이용하는 것은 값을 변경하는게 아닌, 기존에 있던 String값을 버리고 새로운 값을 할당하는 것이다.
  - 따라서 속도 측면에서 매우 비효율적이다.
- 이때 사용할 수 있는게 StringBuffer와 StringBuilder인데 둘 모두 변할(mutable) 수 있기 때문이다.

## <em> StringBuffer / StringBuilder </em>

- StringBuffer는 공통 메소드가 동기화되므로 멀티 쓰레드 환경에서는 StringBuffer를 사용하는 것이 안전하다.
  - 값이 예상치 못하게 변경되는 것을 방지
- 그 외에는 StringBuilder가 성능이 뛰어나기에 StringBuilder를 사용하는 것이 좋다.

## <em> 주요 메소드 </em>

- append(값)
  - StringBuffer,StringBuilder 뒤에 값을 붙인다.
- insert(인덱스,값)
  - 특정 인덱스부터 값을 삽입한다.
- delete(인덱스,인덱스)
  - 특정 인덱스부터 인덱스까지 값을 삭제한다.
- substring(인덱스,인덱스)
  - 인덱스부터 인덱스까지 값을 잘라온다.
- indexOf(값)
  - 값이 어느 인덱스에 들어있는지 확인한다.
- replace(인덱스,인덱스,값)
  - 인덱스부터 인덱스까지 값으로 변경한다.
- reverse()
  - 글자 순서를 뒤집는다.

## <em> 구문(Syntax) <em>

```java
    StringBuffer sb = new StringBuffer(); // StringBuffer 객체 sb 생성
    sb.append("hello");
    sb.insert(5," ");
    sb.append("java");
    String result = sb.toString();
    System.out.println(result); // hello java 출력

```
