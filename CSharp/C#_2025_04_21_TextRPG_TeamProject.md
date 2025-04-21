# [C#] 텍스트 RPG 팀 프로젝트 시작 & 추상 클래스 활용  
📅 2025.04.21

## 📌 오늘 배운 것  
- 텍스트 RPG 팀 프로젝트 시작  
- 플레이어 스크립트 작성  
- 추상 클래스(Abstract Class) 이해 및 활용  
- 직업 시스템 설계 (전사 / 마법사)

## 🧠 이해한 내용  
- 오늘부터 팀 프로젝트로 텍스트 RPG 게임 개발을 시작했고, 나는 **플레이어 관련 스크립트 제작**을 맡음.  
- 플레이어 클래스에서는 다음과 같은 속성들을 초기화:
  - 이름, 직업, 체력, 공격력, 방어력, 보유 골드  
- 상태를 확인할 수 있는 `ShowStatus()` 메서드 제작.

- 직업 시스템은 **추상 클래스 `Job`을 기반으로 전사(`Warrior`)와 마법사(`Magician`) 클래스를 구현**함.  
  - 추상 클래스는 인스턴스화할 수 없고, 자식 클래스에서 반드시 구현해야 하는 멤버를 정의함.  
  - 각 직업은 `JobName`, `BaseAtkDmg`, `BaseDefence`, `PrintSkillInfo()` 등을 오버라이딩함.
  - **기초 공격력과 방어력의 차별화**로 직업 특성을 표현할 수 있음.

```csharp
public abstract class Job
{
    public abstract string JobName { get; }
    public abstract float BaseAtkDmg { get; }
    public abstract int BaseDefence { get; }
    public abstract void PrintSkillInfo();
}

public class Warrior : Job
{
    public override string JobName => "전사";
    public override float BaseAtkDmg => 1.0f;
    public override int BaseDefence => 1;

    public override void PrintSkillInfo()
    {
        // 스킬 정보 출력 예정
    }
}

public class Magician : Job
{
    public override string JobName => "마법사";
    public override float BaseAtkDmg => 2.0f;
    public override int BaseDefence => 0;

    public override void PrintSkillInfo()
    {
        // 스킬 정보 출력 예정
    }
}
```

### 💡 느낀 점 / 생각
- 개인 프로젝트로 진행했었던 텍스트RPG를 팀프로젝트로 만들게 되었는데 다른 사람들의 코드를 보고 추상클래스를 활용하면 깔끔한 코드가 된다는 것을 배웠다.
- 추상 클래스의 개념을 직업클래스에 접목하면서 실제로 써보았는데 유지보수나 확장성 측면에서 좋은것 같다. 
- SkillA, SkillB 같은 스킬 구현도 각 직업 클래스에서 다형성을 통해 처리할 예정.
- 기존의 주먹구구식 코딩보다 객체지향의 장점을 더 활용해야된다는것을 깨달았다. 