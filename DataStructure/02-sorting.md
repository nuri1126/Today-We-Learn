# Sorting
> 19-03-18 (월)

<a href="https://github.com/jinnyy">@jinnyy</a>

<br>

### 순서
1. Selection Sort
2. Bubble Sort
3. Insesrtion Sort
4. Merge Sort
5. Quick Sort



<br><br><br>

# 1. Selection Sort
1. `sorted part`와 `unsorted part`를 유지한다.
2. `unsorted part`에서 최솟값을 찾아 `sorted part`에 넣는다. ← [반복]

* 공간복잡도: O(1) (In place)
* 시간복잡도: O(n^2)

```java
void selectionSort(int arr[]) 
{ 
    int n = arr.length; 

    // unsorted array를 돈다. i는 unsorted array의 끝을 표시하게 된다.
    for (int i = 0; i < n-1; i++) 
    { 
        // unsorted array의 최솟값을 찾는다.
        int min_idx = i; 
        for (int j = i+1; j < n; j++) 
            if (arr[j] < arr[min_idx]) 
                min_idx = j; 

        // 최솟값과 첫 번째 값을 서로 바꾼다. 
        // (각 값이 들어 있는 칸의 내용을 서로 바꿈)
        int temp = arr[min_idx]; 
        arr[min_idx] = arr[i]; 
        arr[i] = temp; 
    } 
}
```

<br><br>

# 2. Bubble Sort
연속한 두 원소를 비교하면서 서로 다를 때 swap한다.

* 공간복잡도: O(1)
* 시간복잡도
  - Worst / Average: O(n^2)
  - Best Case: O(n^2)

```java
void bubbleSort(int arr[]) 
{ 
    int n = arr.length; 
    for (int i = 0; i < n-1; i++) 
        for (int j = 0; j < n-i-1; j++) 
            if (arr[j] > arr[j+1]) 
            { 
                // swap arr[j+1] and arr[i] 
                int temp = arr[j]; 
                arr[j] = arr[j+1]; 
                arr[j+1] = temp; 
            } 
} 
```
위 코드를 optimize하면 아래와같이 수정가능하다.

* 공간복잡도: O(1)
* 시간복잡도
  - Worst / Average: O(n^2)
  - Best Case: O(n) (이미 정렬된 수열이 주어졌을 때)
  
```java
static void bubbleSort(int arr[], int n) 
{
    int i, j, temp; 
    boolean swapped; 
    for (i = 0; i < n - 1; i++)  
    { 
        swapped = false; 
        for (j = 0; j < n - i - 1; j++)  
        { 
            if (arr[j] > arr[j + 1])  
            { 
                // swap arr[j] and arr[j+1] 
                temp = arr[j]; 
                arr[j] = arr[j + 1]; 
                arr[j + 1] = temp; 
                swapped = true; 
            }
        } 

        // inner loop에서 swap이 일어나지 않았다면 break한다.
        // 더이상 정렬될 여지가 없다는 것을 의미하기 때문이다.
        if (swapped == false) 
            break; 
    } 
}
```


<br><br>

# 3. Insertion Sort
숫자를 하나씩 차례대로 확인하면서 해당 숫자의 위치를 찾아 넣는다.

* 공간복잡도: O(1)
* 시간복잡도: O(n^2)

```java
void insertionSort(int arr[]) 
{ 
    int n = arr.length; 
    for (int i = 1; i < n; ++i) {
        int key = arr[i]; 
        int j = i - 1;

        // 뒤쪽에 있는 숫자들을 한 칸씩 뒤로 보낸다.
        while (j >= 0 && arr[j] > key) { 
            arr[j + 1] = arr[j]; 
            j = j - 1; 
        } 
        arr[j + 1] = key; 
    } 
} 
```

<br><br>

# 4. Merge Sort
Divide & Conquer를 통해 수열을 최소 단위까지 쪼갰다가 다시 합친다.

* 공간복잡도: O(n)
* 시간복잡도: O(n Logn)

```java
void merge(int arr[], int l, int m, int r) 
{ 
    // merge될 array의 크기를 찾는다.
    int n1 = m - l + 1; 
    int n2 = r - m; 

    /* temp array 생성 */
    int L[] = new int [n1]; 
    int R[] = new int [n2]; 

    /* temp array로 값 copy */
    for (int i=0; i<n1; ++i) 
        L[i] = arr[l + i]; 
    for (int j=0; j<n2; ++j) 
        R[j] = arr[m + 1+ j]; 


    /* Merge the temp arrays */

    // first and second subarray들의 인덱스 초기값
    int i = 0, j = 0; 

    // merged subarry들의 인덱스 초기값
    int k = l; 
    while (i < n1 && j < n2) 
    { 
        if (L[i] <= R[j]) 
        { 
            arr[k] = L[i]; 
            i++; 
        } 
        else
        { 
            arr[k] = R[j]; 
            j++; 
        } 
        k++; 
    } 

    /* L[]에 값이 남아있다면 모두 복스 */
    while (i < n1) 
    { 
        arr[k] = L[i]; 
        i++; 
        k++; 
    } 

    /* R[]에 값이 남아있다면 모두 복사 */
    while (j < n2) 
    { 
        arr[k] = R[j]; 
        j++; 
        k++; 
    } 
} 


// Main function that sorts arr[l..r] using merge() 
void sort(int arr[], int l, int r) 
{ 
    if (l < r) 
    { 
        // Find the middle point 
        int m = (l+r)/2; 

        // Sort first and second halves 
        sort(arr, l, m); 
        sort(arr , m+1, r); 

        // Merge the sorted halves 
        merge(arr, l, m, r); 
    } 
}
```


<br><br>

# 5. Quick Sort
한 element를 pivot으로 지정하고 해당 값을 기준으로 주어진 수열의 값을 분류한다.
(작은 것은 왼쪽에, 큰 것은 오른쪽에)
그리고 왼쪽과 오른쪽 각각에 대해서 퀵소트를 (recursively) 다시 실행한다.

* 공간복잡도: O(logn)
* 시간복잡도
  - Average: O(n logn)
  - Worst: O(n^2)
  - Best: Ω(n log(n))

```java
int partition (int arr[], int low, int high) 
{ 
    int pivot = arr[high];    // pivot 
    int i = (low - 1);  // Index of smaller element 
  
    for (int j = low; j <= high- 1; j++) 
    { 
        // If current element is smaller than or 
        // equal to pivot 
        if (arr[j] <= pivot) 
        { 
            i++;    // increment index of smaller element 
            swap(&arr[i], &arr[j]); 
        } 
    } 
    swap(&arr[i + 1], &arr[high]); 
    return (i + 1); 
} 
  
/* The main function that implements QuickSort 
 arr[] --> Array to be sorted, 
  low  --> Starting index, 
  high  --> Ending index */
void quickSort(int arr[], int low, int high) 
{ 
    if (low < high) 
    { 
        /* pi is partitioning index, arr[p] is now 
           at right place */
        int pi = partition(arr, low, high); 
  
        // Separately sort elements before 
        // partition and after partition 
        quickSort(arr, low, pi - 1); 
        quickSort(arr, pi + 1, high); 
    } 
}
```

<br><br>



<br><br><br>

# References
* https://www.geeksforgeeks.org/sorting-algorithms/

<br>

#### 추가로 참고
- <a href="https://www.geeksforgeeks.org/heap-sort/">Heap Sort</a>

