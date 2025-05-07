# Metaverse Game - 트러블슈팅 및 구조 설계 개선
📅 2025.05.07

## 📌 오늘 배운 것
- 씬 전환 간 데이터 유지 방법
- 싱글톤 패턴의 활용
- EventManager를 통한 메서드 호출 구조화
- BaseController 기반 확장성 있는 캐릭터 시스템 설계
- SpriteRender를 변경했는데 적용이 안되는 문제

## 🧠 이해한 내용
- **씬 전환 후 데이터 초기화 문제**  
  메타버스 게임에서 메인 씬 → 미니게임 → 메인 씬 구조로 전환할 때, 메인 씬에서 미니게임 결과가 초기화되는 문제가 발생함.  
  이를 해결하기 위해 **GameManager를 싱글톤**으로 제작하여 데이터를 보존하도록 설계.

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public GameObject playerPrefab;
    public GameObject rankingPrefab;
    private GameObject player;

    public StatData playerStatData;

    public Dictionary<int, MiniGameResult> miniGameResults = new();


    private void Awake()
    {
        // 싱글톤 설정
        if (instance != null && instance != this)
        {
            Destroy(gameObject);
            return;
        }

        instance = this;
        playerStatData = new StatData();
        DontDestroyOnLoad(gameObject); // 씬이 바뀌어도 파괴되지 않음
    }
```

- **EventManager 스크립트 활용**  
  `EventManager`를 별도로 제작하여, `Awake()`에서 이벤트들을 일괄적으로 등록하고  
  `TriggerEvent()`를 통해 필요한 메서드를 호출하는 구조를 구성함.  
  이로 인해 코드의 가독성이 올라가고, 유지보수가 쉬워졌음.

``` csharp
  public void RegisterEvent(string eventName, Action listener)
  {
      if (eventDictionary.TryGetValue(eventName, out Delegate thisEvent))
      {
          thisEvent = Delegate.Combine(thisEvent, listener);
          eventDictionary[eventName] = thisEvent;
      }
      else
      {
          eventDictionary[eventName] = listener;
      }
      Debug.Log($"Event '{eventName}' registered");

  }

    public void TriggerEvent(string eventName)
  {
      if (eventDictionary.TryGetValue(eventName, out Delegate thisEvent))
      {
          (thisEvent as Action)?.Invoke();
      }
      else
      {
          Debug.LogWarning($"Event '{eventName}' not found!");
      }
  }
```

- **BaseController 구조 설계**  
  플레이어와 NPC가 **공통된 BaseController**를 상속받아 구현되어 있음.  
  새로운 NPC가 추가되어도 같은 구조를 사용하므로 **확장성과 코드 재사용성**이 매우 높아졌음.

- **SpriteRenderer 문제**
  게임중 플레이어의 색상을 바꿔야되는 과제가 있는데 자연스럽게 sp.color를 변경했지만 적용이 안됐다. 검색결과 sp.color로 색상을 접근하는게 아니라
  sp.material.color로 접근을 해야 바꿀 수 있었다. 근데 또 테스트 해본 결과 오브젝트의 setactive가 꺼져있을때는 sp.color로 변경이 가능했는데 
  setactive가 켜져있을때는 작동을 안하는 것이였다. 이 점 유의해야겠다.

## 💡 느낀 점 / 생각
- 메타버스 게임처럼 여러 씬 간 데이터 흐름이 중요한 프로젝트에서는 **싱글톤 관리의 중요성**을 절실히 느낌.
- 이벤트를 등록하고 호출하는 방식을 **중앙 집중화**하니 로직 흐름이 훨씬 명확해지고 디버깅도 쉬워졌음.
- 구조적으로 설계된 BaseController 패턴 덕분에 추후 기능을 추가하거나 캐릭터를 확장할 때 수고가 크게 줄어들었음.
- 제작을 진행하면서 멀티플레이 구조로 언제든지 적용할 수 있도록 최대한 설계는 했지만 시간이 부족해 멀티쪽은 손도 못댄게 아쉬움..
