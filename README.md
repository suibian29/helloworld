#include <stdio.h>

#define MAX_SIZE 100  // 定义数组的最大大小

void insert(int arr[], int *n) {
    if (*n >= MAX_SIZE) {
        printf("数组已满，无法插入新元素。\n");
        return;
    }

    int num, pos;
    printf("请输入要插入的数：");
    scanf("%d", &num);
    printf("请输入插入的位置（0 到 %d）：", *n);
    scanf("%d", &pos);

    if (pos < 0 || pos > *n) {
        printf("插入的位置无效！\n");
        return;
    }

    for (int i = *n; i > pos; i--) {
        arr[i] = arr[i - 1];
    }
    arr[pos] = num;
    (*n)++;

    printf("插入后数组为：\n");
    for (int i = 0; i < *n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

void remove_element(int arr[], int *n) {
    int pos;
    printf("请输入要移除的位置（0 到 %d-1）：", *n);
    scanf("%d", &pos);

    if (pos < 0 || pos >= *n) {
        printf("删除的位置无效！\n");
        return;
    }

    for (int i = pos; i < *n - 1; i++) {
        arr[i] = arr[i + 1];
    }
    (*n)--;  // 减少当前元素的数量

    printf("移除后数组为：\n");
    for (int i = 0; i < *n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

void update(int arr[], int n) {
    int pos, num;
    printf("请输入要更新的位置（0 到 %d-1）：", n);
    scanf("%d", &pos);

    if (pos < 0 || pos >= n) {
        printf("更新的位置无效！\n");
        return;
    }

    printf("请输入新值：");
    scanf("%d", &num);
    arr[pos] = num;  // 更新指定位置的数字

    printf("更新后数组为：\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

void print_array(int arr[], int n) {
    printf("当前数组为：\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int count(int arr[], int n, int target) {
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            count++;
        }
    }
    return count;
}

void search(int arr[], int n) {
    int target;
    printf("请输入要查找的数：");
    scanf("%d", &target);
    
    printf("数 %d 的位置：", target);
    int found = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            printf("%d ", i);
            found = 1;
        }
    }
    if (!found) {
        printf("未找到该数。\n");
    }
    printf("\n");
}

int min(int arr[], int n) {
    int minimum = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < minimum) {
            minimum = arr[i];
        }
    }
    return minimum;
}

int max(int arr[], int n) {
    int maximum = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > maximum) {
            maximum = arr[i];
        }
    }
    return maximum;
}

int main() {
    int arr[MAX_SIZE];
    int n = 0; // 当前元素数量
    int choice;

    while (1) {
        printf("\n菜单：\n");
        printf("1. 插入元素\n");
        printf("2. 移除元素\n");
        printf("3. 更新元素\n");
        printf("4. 打印数组\n");
        printf("5. 查找最小值\n");
        printf("6. 查找最大值\n");
        printf("7. 计数元素\n");
        printf("8. 查找元素\n");
        printf("9. 退出\n");
        printf("请输入你的选择：");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                insert(arr, &n);
                break;
            case 2:
                remove_element(arr, &n);
                break;
            case 3:
                update(arr, n);
                break;
            case 4:
                print_array(arr, n);
                break;
            case 5:
                if (n > 0) {
                    printf("数组中的最小值为：%d\n", min(arr, n));
                } else {
                    printf("数组为空，无法查找最小值。\n");
                }
                break;
            case 6:
                if (n > 0) {
                    printf("数组中的最大值为：%d\n", max(arr, n));
                } else {
                    printf("数组为空，无法查找最大值。\n");
                }
                break;
            case 7: {
                int target;
                printf("请输入要计数的数：");
                scanf("%d", &target);
                int count_result = count(arr, n, target);
                printf("数 %d 的数量为：%d\n", target, count_result);
                break;
            }
            case 8:
                search(arr, n);
                break;
            case 9:
                printf("退出程序。\n");
                return 0;
            default:
                printf("无效选择，请重试。\n");
                break;
        }
    }

    return 0;
}
