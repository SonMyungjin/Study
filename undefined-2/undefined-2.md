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

