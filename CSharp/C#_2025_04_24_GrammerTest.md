# [C#] 배치고사 오답노트 및 회고  
📅 2025.04.24

## 📌 오늘 배운 것  
- `ref` 키워드 사용 방식 복습  
- DFS(깊이 우선 탐색) & BFS(너비 우선 탐색) 개념 정리  

## 🧠 이해한 내용  

### ✅ 오답 1 - `ref` 키워드 문제  
```csharp
class Program
{
    private static void Add(int i, ref int result)
    {
        result += i;
    }

    static void Main(string[] args)
    {
        int total = 10;
        Console.WriteLine(total);        // 출력: 10
        Add(200, ref total);
        Console.WriteLine(total);        // 출력: 210
    }
}
```
- 틀린 이유 :
- 문제를 푸는 과정에서 ref라는 키워드를 아예 놓치고 out이라는 키워드에 집중했더니 당연하지만 문제가 풀리지 않았다.  

### ✅ 오답 2 - 탐색 알고리즘 순서 문제  

- 깊이 우선 탐색 : 1 > 2 > 3 > 6 > 9 > 7 > 4 > 8 > 5
- 너비 우선 탐색 : 1 > 2 > 3 > 4 > 5 > 6 > 7 > 8 > 9

- 틀린 이유 :
- 방문 순서를 헷갈렸다. 다시 정리하면서 외워야 겠다.

- 깊이 우선 탐색 순서 : 왼쪽부터 쭉 파고들면서 탐색
- 너비 우선 탐색 순서 : 왼쪽부터 가까운 노드들을 순서대로 탐색

#### 💡 느낀 점 / 생각
- ref와 out은 알고 있었지만 실제 사용 용도와 차이점을 놓치고 있었던 것 같아. 오늘 문제를 통해 그 차이를 다시 명확히 이해하게 됐다.
- 알고리즘은 아직 익숙하지 않아서 DFS/BFS 같은 대표적인 탐색 방법은 따로 시간을 들여 정리하면 좋을 것 같다.