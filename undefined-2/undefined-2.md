# 정렬

## 정렬 알고리즘

* 원소들을 번호순이나 사전 순서와 같이 일정한 순서대로 열거하는 알고리즘이다. 효율적인 정렬은 탐색이나 병합 알고리즘처럼 (정렬된 리스트에서 바르게 동작하는) 다른 알고리즘을 최적화하는 데 중요하다.



## 정렬 알고리즘 종류

### 선택정렬

* 선택 정렬은 제자리 비교 정렬이다.&#x20;
* 복잡도는 O(n^2)이므로 큰 리스트에는 비효율적이며, 유사한 삽입 정렬보다 성능이 더 떨어지는 것이 일반적이다.&#x20;
* 선택 정렬은 단순함이 특징이며 특정한 상황에서는 더 복잡한 알고리즘보다 성능상 우위가 있다.
* 이 알고리즘은 최솟값을 찾고 값을 최초 위치와 바꾼 다음 리스트의 나머지 부분에 대해 이 과정을 반복한다.&#x20;
* 교환 과정은 n개를 넘지 않으므로 교환 비용이 많이 드는 상황에서 유용하다.

![](<../.gitbook/assets/image (12).png>)

* Java 코드

```java
import java.util.Arrays;

public class StackList {
    public static void main(String[] args) {
		    int[] arr = {33, 5, 98, 75, 87, 12, 4, 61, 100};
		    selectionSort(arr);
		         
		    System.out.println(Arrays.toString(arr));
		}
 
 public static void selectionSort(int[] arr) {
      int idxMin, tmp;
     
	    for (int i = 0; i < arr.length - 1; i++) {
	        idxMin = i;
	        for (int j = i + 1; j < arr.length; j++) {
	            if (arr[j] < arr[idxMin]) {
	                idxMin = j;
	            }
	        }
	        tmp = arr[idxMin];
	        arr[idxMin] = arr[i];
	        arr[i] = tmp;
	     }
	 }
}
```

```jsx
// 출력
[4, 5, 12, 33, 61, 75, 87, 98, 100]
```



### 삽입정렬

* 삽입 정렬은 작은 리스트와 대부분 정렬된 리스트에 상대적으로 효율적인 단순한 정렬 알고리즘이며 더 복잡한 알고리즘의 일부분으로 사용되기도 한다.
* 리스트로부터 요소를 하나씩 취한 다음 마치 돈을 지갑에 넣는 방식과 비슷하게 이들을 올바른 위치에, 새로 정렬된 리스트에 삽입함으로써 동작한다.&#x20;
* 배열의 경우 새 리스트와 남아있는 요소들은 배열 공간을 공유할 수 있으나 삽입의 경우 잇따르는 모든 요소를 하나씩 이동해야 하므로 비용이 많이 든다.&#x20;
* 셸소트는 큰 리스트에 더 효율적인 삽입 정렬의 변종이다.

![](<../.gitbook/assets/image (18).png>)

* Java 코드

```java
public static void main(String[] args) {
   int[] arr = {33, 5, 98, 75, 87, 12, 4, 61, 100};
   insertionSort(arr);

	 System.out.println(Arrays.toString(arr));
	 // 출력 : [4, 5, 12, 33, 61, 75, 87, 98, 100]
}

public static void insertionSort(int[] arr){
     for(int idx = 1; idx < arr.length; idx++) {
         int tmp = arr[idx];
         int aux = idx - 1;

         while(aux >= 0 && arr[aux] > tmp) {
              arr[aux + 1] = arr[aux];
              aux--;
         }

         arr[aux + 1] = tmp;
      }
}
```
