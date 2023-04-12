# <em> for each문 </em>

- For-each문은 for, while, do-while 반복문과 같은 배열 탐색기법이다.

## <em>사용방법</em>

- 일반적인 for 반복문과 동일하게 for 키워드를 사용한다.
- 반복문 내에 카운터 변수를 선언하고 콜론(:) 다음 배열이름을 순서대로 선언한다.
- 일반적으로 배열이나 Collection 클래스(ArrayList.. 등)를 반복하는데 사용한다.

## <em> 구문(Syntax) <em>

- 일반적인 for문을 이용한 배열 탐색

  ```java
    int [] arr ={0,1,2,3,4};

    for(int i=0;i<5;i++){
        System.out.println(arr[i]);
    }
  ```

- 기본구조

  ```java
  for( 각 요소 값 : 배열이나 컨테이너 값 )
  {

     반복 수행할 작업

  }
  ```

- for each문을 사용하여 배열 탐색

```java
  int [] arr={0,1,2,3,4};

  for(int i:arr){
      System.out.println(arr[i]);
  }
```

- for each문에서 2차원배열 탐색하기

```java
   /*arr[][] = {{1,1,1},
                {2,2,2},
                {3,3,3},
                {4,4,4}
                }
    */
   for( int[]p : arr){
      for(int q : p){
        System.out.print(q+" ");
      }
      System.out.println("");
   }

   // 먼저 1차원 배열과 똑같이 arr의 배열의 아이템을 하나씩 꺼냄, {1,1,1} , {2,2,2}, ..이 전부 p[]에 담긴다, p를 q로 하나씩 빼낸다.

   // 출력형태
   1 1 1
   2 2 2
   3 3 3
   4 4 4
```

## <em> 장점 </em>

- 복잡한 배열이나 리스트의 크기를 구할 필요가 없다.
- 복잡한 반복문에 적합하며, 인덱스를 생성해 접근하는 단순 for문보다 수행속도가 빠르다.
- 코드가 짧아 가독성이 좋다.

## <em> 한계 </em>

- 반복문 내에서 배열이나 리스트의 값을 변경하거나 추가 할 수 없다.(탐색만 가능)

  ```java
    int [] arr={0,1,2,3,4};

    for(int i:arr){
        arr[i] = 3; // 에러
        arr[i+1] = 4; // 에러
    }
    // 오로지 탐색만 가능함
  ```

- 배열을 역순으로 탐색할 수 없다.
