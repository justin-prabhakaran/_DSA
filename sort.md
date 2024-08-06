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
