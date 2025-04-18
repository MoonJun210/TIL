# [C#] 텍스트 RPG 리팩토링  
📅 2025.04.18

## 📌 오늘 배운 것  
- C# 텍스트 RPG 코드 리팩토링
- 클래스 분리 원칙 (SRP - 단일 책임 원칙)
- 메서드 기능 위임
- 유지보수성과 가독성 향상 방법

## 🧠 이해한 내용  
- `Program` 클래스에서는 더 이상 기능 구현을 하지 않고, 오직 **메서드 호출만 담당**하게 역할을 축소함.
- 각 기능별 상세 로직은 `Handle` 클래스에서 구현하여 **기능을 모듈화**함.
- 이를 통해 코드가 훨씬 **깔끔하고 명확하게 분리**되어 유지보수가 쉬워졌고, 테스트 및 디버깅도 용이해짐.
- 실질적인 "행동"은 Handle 클래스가 처리하고, Program은 흐름만 제어하는 구조로 변경.

```csharp
// 예시 구조
class Program
{
    static void Main()
    {
        Handle.ShowMainMenu();
    }
}

class Handle
{
    public static void ShowMainMenu()
    {
        // 메뉴 출력 및 사용자 입력 처리
    }
}
```
