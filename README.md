# 10-data-quicksort
10萬筆data  quicksort

#include <stdlib.h>
#include <time.h>

void Exchange(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

void QSORT(int *nums, int left, int right) {
    if (left >= right) return; // 終止條件
    int l = left + 1; // 左
    int r = right; // 右
    int key = nums[left];
    while (1) {
        while (l <= right) {
            if (nums[l] > key) break;
            l++;
        }
        while (r > left) {
            if (nums[r] < key) break;
            r--;
        }
        if (l > r) break;
        Exchange(&nums[l], &nums[r]);
    }
    // key 和 相遇的值 互換
    Exchange(&nums[left], &nums[r]);
    // 分小組繼續進行
    QSORT(nums, left, r - 1);
    QSORT(nums, r + 1, right);
}

int main(void) {
    double start, end;
    start = clock();

    srand(time(NULL)); // 初始化隨機種子

    int number = 100000;
    int array[number];

    // 產生隨機數填充陣列
    for (int i = 0; i < number; i++) {
        array[i] = rand() % 101; // 產生 0 到 100 之間的隨機數
    }

    QSORT(array, 0, number - 1);

    // 印出排序後的結果
    for (int i = 0; i < number; i++) {
        printf("%d\n ", array[i]);
    }
    printf("\n");

    end = clock();

    double diff = end - start; // ms
    printf("Time taken: %f ms\n", diff);
    printf("Time taken: %f seconds\n", diff / CLOCKS_PER_SEC);

    return 0;
}










