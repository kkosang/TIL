<h2> Selection Sort </h2>
<em>Abstract</em>

     Selection Sort와 유사한 알고리즘으로 서로 인접한 두 원소의 대소를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘

<em>Process (오름차순)</em>

1.  1회전 : 첫 번째 원소와 두 번째 원소, 두 번째 원소와 세 번째 원소, .. (마지막-1) 번째 원소와 마지막 원소를 대소 비교하여 서로 교환한다.

2.  1회전 수행시 가장 큰 원소가 맨 뒤로 이동하므로(정렬완료) 2회전 수행시 맨 마지막 원소를 제외하고, 2회전 수행시 뒤에서 두 번째 원소(정렬완료), 반복해서 첫 번째 원소와 두 번째 원소까지 정렬시킨다.

<em>Java Code</em>

```java
 public static void selectionSort(int[] arr) {
        for (int i = 1; i < arr.length ; i++) {
            /* 비교횟수는 배열의 크기에서 i번 횟수를 뺌*/
            for(int j =0; j<arr.length-i;j++){

                // 현재 원소가 다음 원소보다 큰 경우 swap
                if(arr[j]>arr[j+1]){
                    int temp;
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }
```

<em>시간복잡도</em>

- 데이터의 개수가 n일 때,

  - (n-1) + (n-2) + ... + 2 + 1 => n(n-1)/2
  - O(n^2)시간만큼 소요

- 최선,평균,최악의 경우 모두 시간복잡도는 <em>O(n^2)</em>
