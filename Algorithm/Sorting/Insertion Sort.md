<h2> Insertion Sort </h2>
<em>Abstract</em>

       Selection Sort와 유사하지만, 좀 더 효율적인 알고리즘.
       2번째 원소부터 시작하여 그 앞의 원소들과 비교하여 삽입할 위치를 지정한 후, shift연산 후 지정된 자리에 자료를 삽입하는 알고리즘.
       최선의 경우 O(N)시간만큼 소요

<em>Process (오름차순)</em>

1.  2번째 위치(index)의 값을 temp로 저장한다.
2.  temp값과 이전에 있는 원소들과 비교하며 삽입한다.
3.  삽입이 끝났다면, 다음 위치(index)의 값을 temp에 저장하고 반복한다.

<em>Java Code</em>

```java
public static void insertionSort(int[] arr) {
        for(int i=1;i<arr.length;i++){
            int temp = arr[i]; // 삽입하고자 하는 원소값 저장

            int j = i-1;

            // 삽입하고자 하는 원소보다 작아지는 원소 찾기
            while(j>=0 && temp < arr[j]){
                arr[j+1] = arr[j]; // shift 연산
                j--;
            }

            // 삽입하고자 하는 원소보다 작은 원소를 찾았다면 삽입
            arr[j+1]=temp;
        }
    }
```

<em>시간복잡도</em>

- 데이터의 개수가 n일 때,

  - (n-1) + (n-2) + ... + 2 + 1 => n(n-1)/2
  - O(n^2)시간만큼 소요

- 모두 정렬이 되어있는 경우(Optimal)한 경우, <em>O(n)</em>
- 평균,최악의 경우 모두 시간복잡도는 <em>O(n^2)</em>

<em>장점</em>

1.  추가적인 메모리 소비가 작다.
2.  거의 정렬 된 경우 매우 효율적임, 즉 최선의 경우 O(n)시간 소요

<em>단점</em>

1.  역순에 가까울 수록 매우 비효율적임, 즉 최악의 경우 O(n^2)시간 소요
2.  데이터의 상태에 따라 성능의 편차가 매우 크다.
