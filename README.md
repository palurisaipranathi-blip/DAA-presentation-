#include <stdio.h>

// Merge Sort
void merge(int a[], int l, int m, int r) {
    int temp[100], i = l, j = m + 1, k = 0;

    while (i <= m && j <= r) {
        if (a[i] <= a[j])
            temp[k++] = a[i++];
        else
            temp[k++] = a[j++];
    }

    while (i <= m)
        temp[k++] = a[i++];

    while (j <= r)
        temp[k++] = a[j++];

    for (i = l, k = 0; i <= r; i++)
        a[i] = temp[k++];
}

void mergeSort(int a[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(a, l, m);
        mergeSort(a, m + 1, r);
        merge(a, l, m, r);
    }
}

// Quick Sort
void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}

int partition(int a[], int low, int high) {
    int pivot = a[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (a[j] < pivot) {
            i++;
            swap(&a[i], &a[j]);
        }
    }

    swap(&a[i + 1], &a[high]);
    return i + 1;
}

void quickSort(int a[], int low, int high) {
    if (low < high) {
        int p = partition(a, low, high);
        quickSort(a, low, p - 1);
        quickSort(a, p + 1, high);
    }
}

// Binary Search
int binarySearch(int a[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (a[mid] == key)
            return mid;
        else if (a[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return -1;
}

int main() {
    int a[] = {50, 20, 40, 10, 60, 30};
    int b[6], n = 6, key = 40;

    for (int i = 0; i < n; i++)
        b[i] = a[i];

    printf("Original Array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    mergeSort(a, 0, n - 1);

    printf("\nMerge Sort: ");
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    quickSort(b, 0, n - 1);

    printf("\nQuick Sort: ");
    for (int i = 0; i < n; i++)
        printf("%d ", b[i]);

    int result = binarySearch(a, n, key);

    if (result != -1)
        printf("\nBinary Search: %d found at position %d",
               key, result + 1);
    else
        printf("\nElement not found");

    return 0;
}
