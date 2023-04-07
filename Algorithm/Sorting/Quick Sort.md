<h2> Quick Sort </h2>
<em>Abstract</em>

     기본적으로 '분할 정복'알고리즘을 기반으로 정렬되는 방식이다. 병합정렬(Merge Sort)와 '분할 정복' 알고리즘을 사용한다는 점에서 유사하지만, 다른점은 병합정렬의 경우 하나의 리스트를 '절반'으로 나누어 분할 정복을 하고, 퀵 정렬(Quick Sort)의 경우 피벗(pivot)의 값에 따라 비균등하게 나뉜다.
     불안정 정렬에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 비교정렬에 속한다.

<em>Process</em>

1.  배열의 값중 하나를 피벗(pivot)으로 선택한다.
2.  피벗을 기준으로 양쪽에서 피벗보다 큰 값, 혹은 작은 값을 찾는다. 왼쪽에서부터는 피벗보다 큰 값을 찾고, 오른쪽에서부터는 피벗보다 작은 값을 찾는다.
3.  양 방향에서 찾은 두 원소를 교환한다.
4.  왼쪽에서 탐색하는 위치와 오른쪽에서 탐색하는 위치가 엇갈리지 않을 때까지 2번의 과정을 반복한다.
5.  엇갈린 기점을 기준으로 두 개의 부분리스트로 나누어 1번으로 돌아가 해당 부분리스트의 길이가 1이 아닐때까지 1번 과정을 반복한다. (Divide->분할)
6.  인접한 부분리스트끼리 합친다. (Conqure->정복)

<em>Java Code</em> - <em> 왼쪽 피벗 선택방식 </em>

```java
    public static void sort(int [] a){
        l_pivot_sort(a,0,a.length-1);
    }

    /*
    * @param a : 정렬할 배열
    * @param l : 현재 부분배열의 왼쪽
    * @param r : 현재 부분배열의 오른쪽
    * */
    private static void l_pivot_sort(int[]a, int l,int r){
        /* l이 r보다 크거나 같으면, 정렬 할 원소가 1개 => return */
        if(l>=r)
            return;
        /*
         * 피벗을 기준으로 요소들이 왼쪽과 오른쪽으로 약하게 정렬 된 상태로
         * 만들어 준 뒤, 최종적으로 pivot의 위치를 얻는다.
         *
         * 그리고나서 해당 피벗을 기준으로 왼쪽 부분리스트와 오른쪽 부분리스트로 나누어
         * 분할 정복을 해준다.
         *
         * [과정]
         *
         * Partitioning:
         *
         *   a[left]          left part              right part
         * +---------------------------------------------------------+
         * |  pivot  |    element <= pivot    |    element > pivot   |
         * +---------------------------------------------------------+
         *
         *
         *  result After Partitioning:
         *
         *         left part          a[lo]          right part
         * +---------------------------------------------------------+
         * |   element <= pivot    |  pivot  |    element > pivot    |
         * +---------------------------------------------------------+
         *
         *
         *  result : pivot = lo
         *
         *
         *  Recursion:
         *
         * l_pivot_sort(a, lo, pivot - 1)     l_pivot_sort(a, pivot + 1, hi)
         *
         *         left part                           right part
         * +-----------------------+             +-----------------------+
         * |   element <= pivot    |    pivot    |    element > pivot    |
         * +-----------------------+             +-----------------------+
         * lo                pivot - 1        pivot + 1                 hi
         *
         */

        int pivot = partition(a,l,r);

        l_pivot_sort(a,l,privot-1);
        l_pivot_sort(a,pivot+1,r);
    }

    /*
    * @param a : 정렬할 배열
    * @param l : 현재 배열의 가장 왼쪽 부분
    * @param r : 현재 배열의 가장 오른쪽 부분
    * @return 최종적인 피벗의 위치 반환
    * */
    private static int partition(int [] a, int left, int right) {
        int lo = left;
        int ri = right;
        int pivot = a[left]; // 왼쪽 요소를 피벗으로 설정

        while (l < r) {
            /* right가 left보다 크면서, right의 요소가
             * pivot보다 작거나 같은 원소를 찾을 때 까지, right감소 */
            while (a[r] >= pivot && left < right) // 오른쪽에서 피벗보다 작은값찾기
                right--;

            /* right가 left보다 크면서, left의 요소가
             *pivot보다 큰 원소를 찾을 때 까지, left증가
             */
            while (a[l] <= pivot && left < right) // 왼쪽에서 피벗보다 큰 값 찾기
                left++;

            // 교환 될 두 원소를 찾았으면 swap
            swap(a, left, right);
        }

        /* pivot값과 a[left]의 원소와 left가 가리키는 원소를 바꾼다. */
        swap(a,left,lo);

        // 두 요소가 교환되었다면 피벗이었던 요소는 left에 위치하므로 left를 반환한다.
        return left;
    }

    /*
    * @param a : 배열
    * @param i : 왼쪽에서 찾은 값
    * @param j : 오른쪽에서 찾은 값
    * */
    private static void swpa(int[] a,int i,int j){
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
```

<em>C Code</em>

```C
void quickSort(int* data, int start, int end) {
	if (start >= end) // 원소가 1개일때
		return;
	int key = start; // key값
	int i = start + 1; // 왼쪽에서부터 l 큰값찾기
	int j = end; // 오른쪽에서부터 r 작은값 찾기

	while (i <= j) { // 엇갈릴때 까지
		// 왼쪽에서부터 key값보다 큰값 찾기
		while (data[key]>=data[i] && i<=end) {
			i++;
		}

		// 오른쪽에서부터 key값보다 작은값 찾기
		while (data[key] <= data[j] && j> start) {
			j--;
		}

		// 엇갈리면 key값과 스왑
		int temp;
		if (i >= j) {
			temp = data[key];
			data[key] = data[j];
			data[j] = temp;
		}
		else { // 스왑
			temp = data[i];
			data[i] = data[j];
			data[j] = temp;
		}
	}

	quickSort(data, start, j - 1);
	quickSort(data, j+1, end);


}
```

<em>시간복잡도</em>

- 최선의 경우(Best cases) : T(n) = O(nlogn)

  - 비교 횟수 (logn)
    - n = 2^k의 경우, k(k=logn)임을 알 수 있다.
  - 각 순환 호출 단계의 비교 연산 (n)
    - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번정도의 비교가 이루어진다.
  - 따라서, n \* logn => O(nlogn)이 된다.

- 최악의 경우(Worst cases) : T(n) = O(n^2)

  - 최악의 경우는 정렬하고자 하는 배열이 오름차순 정렬되어 있거나, 내림차순 정렬되어 있는경우이다.
  - 비교 횟수 (n)
    - n = 2^k라고 했을때, 순환 호출의 깊이는 n임을 알 수 있다.
  - 각 순환 호출 단계의 비교 연산 (n)
    - 평균 n번 정도의 비교가 이루어진다.
  - 따라서 n \* n => O(n^2)이 된다.

- 평균의 경우(Average cases) : T(n) = O(nlogn)

<em>장점</em>

1.  불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 떄문에, 시간 복잡도가 O(nlogn)를 가지는 다른 정렬 알고리즘과 비교했을때도 가장 빠르다. merge sort에 비해 2~3배정도 빠르다.
2.  정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.

<em>단점</em>

1.  불안정 정렬이다.
2.  정렬된 배열에 대해서는 Quick Sort의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
3.  재귀를 사용하기 때문에 재귀를 사용하지 못하는 환경일 경우 그 구현이 매우 복잡해진다.
