# Unity - ScriptableObject란?
📅 2025.04.11

## 📌 오늘 배운 것
- ScriptableObject는 Unity의 데이터 컨테이너이다.
- 오브젝트를 인스턴스화하지 않고도 데이터 자산을 만들 수 있다.
- 메모리 효율 + 데이터 재사용성 ↑

## 🧠 이해한 내용
- MonoBehaivor처럼 씬에 붙어있는 컴포넌트가 아니고 에셋형식으로 데이터를 관리한다. 여러 오브젝트간에 동일한 데이터를 공유할 때 유용하다.

## 💡 느낀 점 / 생각
- 다양한 적들이라거나 동일한 틀로 만들어질 캐릭터들의 데이터를 저장해 두면 유용할것 같다. 



### 예시
```csharp
[CreateAssetMenu(fileName = "NewItemData", menuName = "Item/Data")]
public class ItemData : ScriptableObject {
    public string itemName;
    public int power;
}
