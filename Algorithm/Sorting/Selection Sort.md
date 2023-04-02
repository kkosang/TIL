<h2> Selection Sort </h2>
<em>Abstract</em>

       해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘

<em>Process (오름차순)</em>

1.  주어진 배열에서 MIN 값을 찾는다.
2.  MIN 값을 맨 앞에 위치한 값과 교환한다.
3.  배열의 맨 앞자리 인덱스를 제외하고 나머지 배열을 같은 방법으로 교환하며 반복한다.

<em>Java Code</em>

```java
    public static void selectionSort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            int min_idx = i;

            // 최솟값 인덱스 찾기
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[min_idx]) {
                    min_idx = j;
                }
            }

            // i번째(맨 앞에서부터)값과 최솟값을 교환
            int temp;
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
```

<em>시간 복잡도</em>

- 데이터의 개수가 n일 때,

  - 첫 번째 비교횟수 : 1 ~ (n-1) => n-1
  - 두 번째 비교횟수 : 2 ~ (n-1) => n-2
  - ...
  - (n-1) + (n-2) + ... + 2 + 1 => n(n-1)/2

- O(n^2)만큼 시간이 걸림
- 최선,평균,최악의 경우 모두 시간복잡도는 <em>O(n^2)</em>

<em>장점</em>

1.  추가적인 메모리 소비가 작다.

<em>단점</em>

1.  모든 경우에 O(n^2)시간 소요
2.  불안정 정렬이다.
