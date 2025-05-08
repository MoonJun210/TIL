# Unity - LegendOFArcher 모작 프로젝트
📅 2025.05.08

## 📌 오늘 배운 것
- 팀 프로젝트 분업 및 컨벤션 설정
- 공통 기능을 위한 상속 구조 설계 (BaseController → Enemy, Player)
- Git 브랜치 전략(PR 기반 병합)
- Player 이동 및 무기 시스템 구현

### 🧠 이해한 내용
- 게임 개발 시 팀 프로젝트의 협업 효율성을 높이기 위해 사전에 코드 컨벤션과 구조를 잘 설계하는 것이 중요하다는 점을 다시 한번 느꼈다.
 BaseController를 통해 Player와 Enemy가 공통적으로 가지는 행동(이동, 회전 등)을 묶고, 이를 상속한 각 컨트롤러에서 세부 구현을 하는 방식이 유지보수와 확장에 유리하다고 생각했고 이를 통해 진행하기로 결정했다.

[예시코드]
```csharp
public class BaseController : MonoBehaviour
{
    protected Rigidbody2D _rigidbody;

    [SerializeField] protected SpriteRenderer characterRenderer;

    protected Vector2 movementDirection = Vector2.zero;
    public Vector2 MovementDirection { get { return movementDirection; } }

    protected Vector2 lookDirection = Vector2.zero;
    public Vector2 LookDirection { get { return lookDirection; } }

    protected virtual void Awake()
    {
        _rigidbody = GetComponent<Rigidbody2D>();
 
    }

    protected virtual void Start()
    {

    }

    protected virtual void Update()
    {
        Debug.Log("ㅂㅊㅇ");
        HandleAction();
        Rotate(lookDirection);
    }

    protected virtual void FixedUpdate()
    {
        Movment(movementDirection);
        
    }

    protected virtual void HandleAction()
    {

    }

    protected virtual void Movment(Vector2 direction)
    {
        direction = direction * 5f; // 속도 조절은 여기서

        _rigidbody.velocity = direction;
    }

    protected virtual void Rotate(Vector2 direction)
    {
        float rotZ = Mathf.Atan2(direction.y, direction.x) * Mathf.Rad2Deg;
        bool isLeft = Mathf.Abs(rotZ) > 90f;

        characterRenderer.flipX = isLeft;

    }
}
```


- Git에서 각자 브랜치를 만들어 작업하고 PR을 통해 병합하면 충돌(Conflict)을 줄이고 코드 품질을 유지할 수 있다는 협업 전략을 선택했다.

#### 💡 느낀 점 / 생각
- 이전 프로젝트 경험이 있어서 협업 컨벤션을 잡는 데에 좀 더 적극적으로 참여할 수 있었고, 구조를 공유한 덕분에 팀원들과 방향성을 잘 맞출 수 있었다.
- Player 이동 및 무기 시스템을 담당하면서 BaseController 설계를 어떻게 해야 재사용성을 높일 수 있을지 고민하는 시간이 유익했다.
- 이런 구조적인 설계가 협업에서 얼마나 중요한지를 체감했고, 실제 업무에서는 어떤방식으로 진행하는지 궁금하다.