# 파일 구조
- Assets 아래로 다음과 같이 구성된다.

- Imports: 외부 에셋 등을 담아두는 용도로 사용하며 .gitignore에서 받지 않도록 해야 하는 리소스. 하위로는 아래와 같이 4개의 카테고리 폴더 경로로 분류한다.
  - Animation
  - Audio
  - Image
  - 3D Modeling

- Scene: 각 Scene들이 담겨져 있으며, 해당 폴더 안에는 테스트가 끝난 기능 단위가 추가가 된 완성된 Scene이다. 하위 폴더로 Test가 있는데 하나의 기능을 테스트 하기 위해 임시 Scene들을 두는 공간이다.
  - Test

- Prefab: 세팅이 끝난 Hirarchy의 리소스들을 저장하기 위한 공간이다. 카테고리 폴더들은 다음과 같다.
  - Player
  - UI
  - GameManager
  - Monster

- Scripts: 소스 코드를 담는 스크립트들이 있는 경로이다. 카테고리 폴더들은 다음과 같다. Test는 정식적인 스크립트로 편입되기 전에 테스트 용도의 스크립트들을 모아놓는 곳이다. 기능이 정식적으로 추가가 되었을 경우 혼동 방지를 위해 지워준다.
  - Player
  - UI
  - GameManager
  - Monster
  - Interface
  - Test

- 50mb 이상의 리소스들은 필히 검수를 받을 것.