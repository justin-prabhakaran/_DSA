### Insertion Sort
```java
import java.util.*;
public class Main {
    public static void main(String[] args) {
        int[] arr = new int[] {1,3,5,7,2,4,6,8};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }

    private static void sort(int[] arr){
        int n = arr.length;
        for(int i=1;i<n;i++){
            int k = arr[i];
            int j = i-1;
            while (j>=0 && arr[j] > k){
                arr[j+1] = arr[j];
                j--;
            }
            arr[j+1] = k;
        }

    }
}
````
### Merge Sort
```java
import java.util.*;
public class Main {
    public static void main(String[] args) {
        int[] arr = new int[] {1,3,5,7,2,4,6,8};
        sort(arr,0, arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    private static void sort(int[] arr,int start, int end){
        if(start < end){
            int mid = start+ (end - start) / 2;
            sort(arr,start,mid);
            sort(arr,mid+1,end);

            merge(arr,start,mid,end);
        }
    }
    private static void merge(int[] arr , int start, int mid,int end){
        int n1 = mid - start + 1 ;
        int n2 = end - mid;

        int[] left = new int[n1];
        int[] right = new int[n2];

        for(int i=0;i<n1;i++){
            left[i] = arr[start + i];
        }
        for(int i=0;i<n2;i++){
            right[i] = arr[mid + 1 + i];
        }

        int i=0,j=0,k =start;
        while(i < n1 && j < n2){
            if(left[i] <= right[j]){
                arr[k++] = left[i++];
            }else{
                arr[k++] = right[j++];
            }
        }

        while (i < n1){
            arr[k++] = left[i++];
        }
        while (j < n2){
            arr[k++] = right[j++];
        }
    }
}

```

### Heap Sort
```java
import java.util.Arrays;

public class Heap {

    public static void main(String[] args) {
        int[] arr = new int[]{1,3,5,7,9,2,4,6,8};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }

    private static void sort(int[] arr){
        int n = arr.length -1;

         build(arr,n);
         for (int i=arr.length-1; i > 0;i--){
             int temp = arr[0];
             arr[0] = arr[i];
             arr[i] = temp;

             n--;
             maxHeapify(arr,0,n);
         }
    }

    private static void maxHeapify(int[] arr, int i, int n){
        int l = left(i);
        int r = right(i);
        int largest;

        if(l <= n && arr[l] > arr[i]) largest = l;
        else largest = i;

        if(r <= n && arr[r] > arr[largest]) largest = r;

        if(largest != i){
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;


            maxHeapify(arr,largest,n);
        }
    }

    private static void build(int[] arr,int n){
        for(int i=n / 2; i >= 0 ;i--){
            maxHeapify(arr,i, n);
        }
    }
    private static int left(int i){
        return 2 * i;
    }

    private static int right(int i){
        return (2 * i) + 1;
    }
}
```
### Quick Sort
```java
import java.util.*;

public class Quicksort {
    public static void main(String[] args) {
        int[] arr = new int[]{1,3,5,7,9,2,4,6,8,10};
        sort(arr,0,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }
    private static void sort(int[] arr,int start, int end){

        if(start < end){
            int mid = partition(arr,start,end);
            sort(arr,start,mid-1);
            sort(arr,mid,end);
        }
    }

    private static int partition(int[] arr, int start, int end){
        int i = start -1;
        for(int j=start;j<end;j++){
            if(arr[j] <= arr[end]){
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }

        }

        int temp = arr[i+1];
        arr[i+1] = arr[end];
        arr[end] = temp;

        return i+1;

    }
}

```
### Counting Sort
```java
import java.util.Arrays;

public class Counting {
    public static void main(String[] args) {
        int[] arr = new int[]{1,3,5,7,9,2,4,6,8,10};
        sort(arr,arr.length);
        System.out.println(Arrays.toString(arr));
    }

    private static void sort(int[] arr, int n){
        int[] res = new int[n];
        int max = Arrays.stream(arr).max().orElse(1);
        int[] count = new int[max+1];

        for(int i : arr){
            count[i]++;
        }

        for(int i=1;i<count.length;i++){
            count[i] += count[i-1];
        }

        for(int i=n-1;i>=0;i--){
            res[count[arr[i]] - 1] = arr[i];
            --count[arr[i]];

        }

        System.arraycopy(res, 0, arr, 0, n);
    }

}
```
