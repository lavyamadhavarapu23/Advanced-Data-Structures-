1.Merge sort
public class MergeSort {

    // Merge two subarrays
    public static void merge(int arr[], int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int L[] = new int[n1];
        int R[] = new int[n2];

        for (int i = 0; i < n1; i++)
            L[i] = arr[left + i];

        for (int i = 0; i < n2; i++)
            R[i] = arr[mid + 1 + i];

        int i = 0, j = 0, k = left;

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        while (i < n1) {
            arr[k++] = L[i++];
        }

        while (j < n2) {
            arr[k++] = R[j++];
        }
    }

    // Divide array
    public static void mergeSort(int arr[], int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }

    public static void main(String[] args) {
        int arr[] = { 38, 27, 43, 3, 9, 82, 10 };

        System.out.println("Original Array:");
        for (int num : arr)
            System.out.print(num + " ");

        mergeSort(arr, 0, arr.length - 1);

        System.out.println("\n\nSorted Array:");
        for (int num : arr)
            System.out.print(num + " ");
    }
}
Output:Original Array:
38 27 43 3 9 82 10 

Sorted Array:
3 9 10 27 38 43 82

2.Quick Sort
public class QuickSort {

    // Function to partition the array
    public static int partition(int arr[], int low, int high) {
        int pivot = arr[high]; 
        int i = (low - 1);    

        for (int j = low; j < high; j++) {

            if (arr[j] < pivot) {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    // Recursive quicksort
    public static void quickSort(int arr[], int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);

            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        int arr[] = { 10, 7, 8, 9, 1, 5 };

        System.out.println("Original Array: ");
        for (int x : arr)
            System.out.print(x + " ");

        quickSort(arr, 0, arr.length - 1);

        System.out.println("\n\nSorted Array: ");
        for (int x : arr)
            System.out.print(x + " ");
    }
}
Output:
Original Array: 
10 7 8 9 1 5 

Sorted Array: 
1 5 7 8 9 10


3. 0/1 Knapsack problem using Dynamic programming
#include <stdio.h>
int max(int a, int b) {
    return (a > b) ? a : b;
}
int knapsack(int W, int wt[], int val[], int n) {
    int dp[n + 1][W + 1];
    for (int i = 0; i <= n; i++) {
        for (int w = 0; w <= W; w++) {
            if (i == 0 || w == 0)
                dp[i][w] = 0;
            else if (wt[i - 1] <= w)
                dp[i][w] = max(val[i - 1] + dp[i - 1][w - wt[i - 1]],
                               dp[i - 1][w]);
            else
                dp[i][w] = dp[i - 1][w];
        }
    }
    return dp[n][W];
}

int main() {
    int val[] = {60, 100, 120};
    int wt[] = {10, 20, 30};
    int W = 50;
    int n = sizeof(val) / sizeof(val[0]);

    printf("Maximum Profit = %d\n", knapsack(W, wt, val, n));
    return 0;
}
Output:
Maximum Profit = 220


4.  0/1 Knapsack problem by using Greedy method
#include <stdio.h>

struct Item {
    int weight;
    int profit;
    float ratio;
};
int main() {
    int capacity = 50;
    int n = 3;

    struct Item items[3] = {
        {10, 60, 0},
        {20, 100, 0},
        {30, 120, 0}
    };

    // Calculate profit/weight ratio
    for (int i = 0; i < n; i++) {
        items[i].ratio = (float)items[i].profit / items[i].weight;
    }

    // Sort items by ratio (descending) - Bubble Sort
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (items[j].ratio < items[j + 1].ratio) {
                struct Item temp = items[j];
                items[j] = items[j + 1];
                items[j + 1] = temp;
            }
        }
    }

    int totalWeight = 0, totalProfit = 0;

    // Greedy selection
    for (int i = 0; i < n; i++) {
        if (totalWeight + items[i].weight <= capacity) {
            totalWeight += items[i].weight;
            totalProfit += items[i].profit;
        }
    }

    printf("Total Profit (Greedy 0/1 Knapsack): %d\n", totalProfit);

    return 0;
}
Output:
Total Profit (Greedy 0/1 Knapsack): 160
LINKED LIST
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* head = NULL;

void insert() {
    struct Node* newnode;
    newnode = (struct Node*)malloc(sizeof(struct Node));

    printf("Enter data: ");
    scanf("%d", &newnode->data);

    newnode->next = head;
    head = newnode;
}

void delete() {
    if (head == NULL) {
        printf("List is empty\n");
        return;
    }

    struct Node* temp = head;
    printf("%d deleted\n", temp->data);
    head = head->next;
    free(temp);
}

void display() {
    struct Node* temp = head;

    if (temp == NULL) {
        printf("List is empty\n");
        return;
    }

    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    int choice;

    while (1) {
        printf("\n1.Insert\n2.Delete\n3.Display\n4.Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: insert(); break;
            case 2: delete(); break;
            case 3: display(); break;
            case 4: return 0;
            default: printf("Invalid choice\n");
        }
    }
}
BINARY SEARCH
#include <stdio.h>

int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1, mid;

    while (low <= high) {
        mid = (low + high) / 2;

        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return -1;
}

int main() {
    int arr[100], n, key, result;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter sorted elements:\n");
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    printf("Enter element to search: ");
    scanf("%d", &key);

    result = binarySearch(arr, n, key);

    if (result == -1)
        printf("Element not found\n");
    else
        printf("Element found at position %d\n", result + 1);

    return 0;
}
DYNAMIC MEMORY ALLOCATION
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n, i;
    int *arr;
    int sum = 0;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    // Dynamic memory allocation
    arr = (int*)malloc(n * sizeof(int));

    if(arr == NULL) {
        printf("Memory not allocated\n");
        return 0;
    }

    printf("Enter %d elements:\n", n);
    for(i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Elements are:\n");
    for(i = 0; i < n; i++) {
        printf("%d ", arr[i]);
        sum += arr[i];
    }

    printf("\nSum = %d", sum);

    // Free allocated memory
    free(arr);

    return 0;
}
