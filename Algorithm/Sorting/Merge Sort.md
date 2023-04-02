<h2> Merge Sort </h2>
<em>Abstract</em>

    합병 정렬이라고 부르며, 분할 정복 방법을 통해 구현한다.

    분할 정복이란
    :   큰 문제를 작은 문제 단위로 쪼개면서 해결해 나가는 방식
    cf) 크기가 10인 배열에서 최댓값을 찾을 때, 크기가 5인 배열 2개로 나눈 후, 각각의 배열에서 최댓값을 찾고 그 최댓값끼리 비교해서 최댓값을 찾는 방식이다.

    빠른 정렬로 분류되며, 퀵소트와 함께 많이 언급되는 정렬 방식이다.

    요소를 쪼갠 후, 다시 합병 시키면서 정렬해나가는 방식으로, 쪼개는 방식은 퀵정렬과 유사하다.

<em>Process</em>

1.  원소의 개수가 n인 배열을 절반으로 분할하여 부분리스트로 나눈다.(Divide)
2.  해당 부분리스트의 길이가 1이 아니라면 1번 과정을 반복한다.
3.  합병 대상이 되는 인접한 부분리스트를 단순 비교하여 정렬하여 합친다. (Conqure)
4.  3번 과정을 반복한다.

<em>Java Code</em>

```java
public static void main(String[] args) {
        int [] arr = {3,401,32,12,4,5,6,12,23,2,1,4};
        int l = 0, r=arr.length-1;
        mergeSort(arr,l,r);
        System.out.println(Arrays.toString(arr));
    }

    public static void mergeSort(int[] arr,int left,int right) {
        /* 왼쪽 index와 오른쪽 index가 같은경우 , 즉 부분리스트가 1개의 원소만 있는경우,
        더이상 쪼갤 수 없으므로 return */
        if(left == right) return;

        /* 왼쪽 index와 오른쪽 index가 엇갈리지 않았다면*/
            int mid = (left+right)/2; // left와 right의 중간지점

            mergeSort(arr,left,mid); // 절반 중 왼쪽 부분리스트
            mergeSort(arr,mid+1,right); // 절반 중 오른쪽 부분리스트
            merge(arr,left,mid,right); // 합병
    }

    public static void merge(int []arr,int left,int mid,int right){
        int i = left; // 왼쪽 부분리스트 시작점
        int j = mid+1; // 오른쪽 부분리스트 시작점
        int k = left;  // 채워넣을 배열의 인덱스
        int [] temp=new int[arr.length]; // 임시배열

        /* 왼쪽 부분리스트의 시작점이 끝지점보다 작거나 같고, 오른쪽 부분리스트의 시작점이 끝지점보다 작거나 같을동안*/
        while(i<=mid && j <= right){
            /* 왼쪽 부분리스트의 i번째 원소가 오른쪽 부분리스트 j번째 원소보다 작거나 같은 경우 */
            if(arr[i]<=arr[j]){
                temp[k++] = arr[i++];
            }
            /* 오른쪽 부분리스트 j번째 원소가 왼쪽 부분리스트 i번째 원소보다 작거나 같은 경우 */
            else{
                temp[k++] = arr[j++];
            }
        }

        /* 아직 남아있는 부분이 있는 경우 채워주기 */
        while(i<=mid){ // 왼쪽 부분리스트 원소가 남아있는경우
            temp[k++] = arr[i++];
        }
        while(j<=right){ // 오른쪽 부분리스트 원소가 남아있는경우
            temp[k++] =arr[j++];
        }

        /* 정렬된 새 배열을 기존 배열에 복사하여 옭김 */
        for(int r=left; r<= right;r++){
            arr[r] = temp[r];
        }
    }

```

<em>시간복잡도</em>

- 데이터의 개수가 n일 때,

  - n = 1인경우 0
  - otherwise인경우 T[n/2] + T[n/2] + n

- 시간복잡도는 <em>O(nlogn)</em>

<em>장점</em>

1.  항상 두 부분리스트로 쪼개어 들어가기 때문에 최악의 경우에도 O(nlogn)시간 소요
2.  안정정렬이다.(정렬 후에 같은 값인 요소의 순서가 보장되는 정렬 방식)

<em>단점</em>

1.  정렬과정에서 추가적인 보조 배열공간(temp)을 사용하기 때문에 메모리 사용량이 많다.
2.  보조 배열에서 원본 배열로 복사하는 과정은 많은 시간을 소비하기 때문에 데이터가 많을경우 상대적으로 시간이 많이 소요된다.
