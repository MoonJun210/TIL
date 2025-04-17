# [알고리즘] 정렬 & 탐색 알고리즘 정리  
📅 2025.04.17

## 📌 오늘 배운 것
- 정렬 알고리즘: 버블 정렬(Bubble Sort), 선택 정렬(Selection Sort), 삽입 정렬(Insertion Sort), 퀵 정렬(Quick Sort)
- 탐색 알고리즘: 선형 탐색(Linear Search), 이진 탐색(Binary Search)
- 시간 복잡도와 효율성 비교

## 🧠 이해한 내용
- **정렬 알고리즘**
  - **버블 정렬**: 인접한 두 값을 비교하여 큰 값을 뒤로 보내는 방식. 시간 복잡도는 O(n²)
```csharp
int[] arr = {5, 3, 8, 4};
for (int i = 0; i < arr.Length - 1; i++)
{
    for (int j = 0; j < arr.Length - i - 1; j++)
    {
        if (arr[j] > arr[j + 1])
        {
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```

  - **선택 정렬**: 가장 작은 값을 선택해서 앞에 배치. 시간 복잡도는 O(n²)
```csharp
int[] arr = {5, 3, 8, 4};
for (int i = 0; i < arr.Length - 1; i++)
{
    int minIndex = i;
    for (int j = i + 1; j < arr.Length; j++)
    {
        if (arr[j] < arr[minIndex])
            minIndex = j;
    }
    int temp = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = temp;
}
```

  - **삽입 정렬**: 앞쪽에서 정렬된 배열을 기준으로 적절한 위치에 삽입. 평균 O(n²), 거의 정렬된 경우 O(n)
```csharp
int[] arr = {5, 3, 8, 4};
for (int i = 1; i < arr.Length; i++)
{
    int key = arr[i];
    int j = i - 1;
    while (j >= 0 && arr[j] > key)
    {
        arr[j + 1] = arr[j];
        j--;
    }
    arr[j + 1] = key;
}
```

  - **퀵 정렬**: 분할 정복(divide and conquer) 방식으로 피벗(pivot)을 기준으로 좌우를 분할하여 재귀적으로 정렬. 평균 시간 복잡도는 O(n log n), 최악은 O(n²)
```csharp
void QuickSort(int[] arr, int left, int right)
{
    if (left >= right) return;

    int pivot = arr[(left + right) / 2];
    int index = Partition(arr, left, right, pivot);
    QuickSort(arr, left, index - 1);
    QuickSort(arr, index, right);
}

int Partition(int[] arr, int left, int right, int pivot)
{
    while (left <= right)
    {
        while (arr[left] < pivot) left++;
        while (arr[right] > pivot) right--;
        if (left <= right)
        {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
    return left;
}
```

- **탐색 알고리즘**
  - **선형 탐색**: 순차적으로 하나씩 확인. 단순하지만 비효율적 (O(n))
```csharp
int[] arr = {3, 7, 1, 9};
int target = 7;
for (int i = 0; i < arr.Length; i++)
{
    if (arr[i] == target)
    {
        Console.WriteLine($"Index: {i}");
        break;
    }
}
```

  - **이진 탐색**: 정렬된 배열에서만 사용 가능. 중간 값을 기준으로 범위를 반씩 줄임 (O(log n))
```csharp
int[] arr = {1, 3, 5, 7, 9};
int target = 5;
int left = 0, right = arr.Length - 1;

while (left <= right)
{
    int mid = (left + right) / 2;
    if (arr[mid] == target)
    {
        Console.WriteLine($"Index: {mid}");
        break;
    }
    else if (arr[mid] < target)
        left = mid + 1;
    else
        right = mid - 1;
}
```

- 정렬 알고리즘은 데이터의 정돈 상태에 따라 효율이 달라지며, 탐색 알고리즘은 정렬 여부가 핵심 조건임을 학습함.
- 퀵 정렬은 실무에서도 많이 쓰이는 효율적인 정렬 방식으로 이해됨.

## 💡 느낀 점 / 생각
- 기본 정렬 알고리즘을 익히면서 시간 복잡도 개념이 더 구체적으로 다가옴.
- 퀵 정렬은 코드 이해가 처음엔 어려웠지만, 재귀 구조와 피벗 선택의 중요성을 체감함.
- 탐색 알고리즘은 효율 차이를 직접 눈으로 보니 이진 탐색의 강점을 확실히 느꼈음.
