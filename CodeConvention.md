# C# 코드 컨벤션
## 1. 기본 코드 네이밍 
- 이름을 지을 때, 쉬운 영단어를 사용하여 이름만 보더라도 어떤 역할을 할 수 있는지 바로 알 수 있도록 직관적이게 짓는다.

| 대상 | 규칙 | 예시 | 
|:---:|:---:|:---:|
| 클래스, 구조체, Enum | PascalCase | `PlayerController`, `WeaponType` | 
| 인터페이스 | `I` + PascalCase | `IDamageable`, `IPoolable` | 
| 추상 기본 클래스 | PascalCase + `Base` | `PlayerBase`, `MonsterBase` | 
| 메서드 | PascalCase | `TakeDamage()` | 
| 프로퍼티, 이벤트 | PascalCase | `MaxPlayerHealth`, `OnHealthChanged` | 
| 지역변수, 매개변수 | camelCase | `damageAmount`, `playerMoveSpeed` | 
| private / protected 필드 | `_camelCase` | `_currentHealth` |
| 상수 | UPPER_SNAKE_CASE | `MAX_PLAYER_LEVEL` |
| 스크립트 파일명 | PascalCase | `GameManager.cs` |  

- 외부 라이브러리·Unity 콜백(`Awake`, `Update` 등)은 원래 이름을 따른다.

## 2. 안티패턴
- Update()에서 매 프레임 GetComponent, Find, Camera.main 호출
- 다량의 기능이 들어간 God Object 생성
- 대량 오브젝트를 Instantiate/Destroy로 반복 생성·삭제 (오브젝트 풀링 안 함)
- SendMessage, 문자열 기반 호출
- Update()에서 문자열 연결 등으로 GC 할당 발생
- 싱글톤 남용, 오브젝트 간 강한 결합
- 물리 로직을 Update()에 작성 
- 무분별한 Find 계열 함수 사용
- 의미를 알 수 없는 숫자인 매직 넘버 추가

## 3. 권장 패턴
- Awake/Start에서 GetComponent, Find 결과를 받는 함수인 CacheComponents나 Initialization을 만들어 적용해 한 번만 캐싱한다.
- 단일 책임 원칙(SRP)에 따라 기능별로 컴포넌트를 분리하고, 작은 컴포넌트를 조합(Composition)해서 구성
- 대량 오브젝트는 오브젝트 풀링(`ObjectPool<T>` 또는 자체 풀)으로 비활성화 후 재사용
- 인터페이스, 직접 참조, C# `event`/`Action`/`UnityEvent` 등 타입 안전한 호출 사용 (문자열이 필요하면 `nameof()` 활용)
- Update()에서는 GC 할당 없이 처리: 값이 바뀔 때만 갱신
- `StringBuilder` 재사용, 배열·리스트 재사용, `NonAlloc` API를 사용하여 콜라이더에 대한 충돌 검사
- 의존성 주입(인스펙터·생성자·Dependecy Injection 컨테이너), 이벤트/메시지 버스, ScriptableObject 기반 데이터·이벤트 채널로 느슨한 결합 유지 (싱글톤은 정말 전역인 소수 서비스에만 제한적으로 사용)
- 물리 로직은 FixedUpdate()에서 처리하고, 입력은 Update()에서 받아 FixedUpdate()에 전달
- Find 계열 대신 `[SerializeField]` 참조 연결, 생성 시점에 등록하는 매니저/레지스트리 패턴 사용
- 매직 넘버는 `const`, `static readonly`, enum, `[SerializeField]` 필드, ScriptableObject 설정 데이터로 의미 있는 이름을 붙여 분리
- 이벤트는 OnEnable에서 구독하고 OnDisable에서 해제해 누수와 null 참조 방지
- 수천 단위 이상의 대량 오브젝트는 풀링에 더해 Job System/Burst, GPU Instancing, DOTS(ECS) 등 데이터 지향 접근 검토
- 최적화는 추측하지 말고 Profiler로 병목과 GC.Alloc을 측정한 뒤 적용