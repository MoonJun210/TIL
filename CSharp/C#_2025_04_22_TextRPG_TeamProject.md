# [C#] 팀 프로젝트 - 퀘스트 시스템 구현  
📅 2025.04.22

## 📌 오늘 배운 것  
- 퀘스트 시스템 기초 설계  
- `Quest` 클래스 제작  
- `Func<>` 델리게이트를 통한 조건 검사 설계  
- `QuestMenu` 클래스로 퀘스트 목록 관리

## 🧠 이해한 내용  
- 팀 프로젝트에서 오늘은 **퀘스트 기능 구현을 담당**했음.  
- `Quest` 클래스에는 다음과 같은 정보들을 포함시킴:
  - 퀘스트 제목 (string) 
  - 퀘스트 내용 (string)
  - 보상 (골드, 아이템 등)
  - 완료 여부
- 플레이어가 특정 행동을 했는지 체크하기 위해 **`Func<Player, bool>` 형태의 델리게이트를 사용**할 계획임.
  - 예를 들어, "몬스터 3마리 처치" 같은 조건을 `Func<Player, bool>`로 표현하여, 조건이 만족될 때 자동으로 퀘스트를 완료 처리할 수 있도록 구현할 예정.

```csharp
public class Quest
{
    public string Title { get; private set; }
    public string Description { get; private set; }
    public int RewardGold { get; private set; }
    public bool IsCompleted { get; private set; }
    public Item? Item { get; private set; }
    public bool IsActive { get; set; }

    private Func<Player, bool> comepleteCheck;

    public Quest(string title, string description, int rewardGold, Func<Player, bool> comepleteCheck)
    {
        Title = title;
        Description = description;
        RewardGold = rewardGold;
        IsCompleted = false;
        this.comepleteCheck = comepleteCheck;
    }

    public Quest(string title, string description, int rewardGold, Item item, Func<Player, bool> comepleteCheck)
    {
        Title = title;
        Description = description;
        RewardGold = rewardGold;
        IsCompleted = false;
        Item = item;
        IsActive = false;
        this.comepleteCheck = comepleteCheck;
    }


    public void CheckCompletion(Player player)
    {
        if (!IsCompleted && comepleteCheck(player))
        {
            IsCompleted = true;
            Console.WriteLine($"퀘스트 완료! 보상으로 {RewardGold} 골드를 획득했습니다.");
            player.Gold += RewardGold;
            if (Item != null)
            {
                // 플레이어 인벤토리에 아이템 추가 
                player.Inventory.AddItem(Item);
            }
        }
    }

    public void ShowQuestInfo()
    {
        Console.WriteLine($"[퀘스트] {Title}");
        Console.WriteLine($"- 설명: {Description}");
        Console.WriteLine($"- 보상: {RewardGold} G");
        Console.WriteLine($"- 상태: {(IsCompleted ? "완료" : "미완료")}");
        Console.WriteLine();
        if(IsActive)
        {
            Console.WriteLine("이미 수령한 퀘스트 입니다.");

        } else
        {
            Console.WriteLine("1. 수락");
        }
        Console.WriteLine("0. 나가기");
    }
}
```

### 💡 느낀 점 / 생각
- 조건을 유연하게 처리할 수 있는 Func<> 델리게이트를 퀘스트 로직에 활용하는 아이디어가 굉장히 깔끔하고 유지보수에도 좋을 것 같다는 생각이 들었음.
- 추후에 퀘스트에 관련된 메서드들만 모아두는 방안을 검토중
- 객체지향의 원칙에 따라 Quest, QuestMenu 등 각 기능별로 클래스를 분리하면서, 전체 코드가 정돈되어 가는 느낌을 받음.
