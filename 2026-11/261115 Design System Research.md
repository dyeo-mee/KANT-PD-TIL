>여러 디자인 시스템을 비교하고, 좋은 점을 발견하기.<br>
컴포넌트의 상태별 모양과 사용 상황을 이해하기.<br>
Variant와 Property를 활용해 상태와 내용을 바꿀 수 있는 컴포넌트 만들기.

- [Figma 과제 링크](https://www.figma.com/design/S1tmaPg7D8oqeGWpUmHgDR/Figma-%EC%8B%A4%EC%8A%B5%EA%B3%BC%EC%A0%9C_%EA%B9%80%ED%98%84%EA%B2%BD?node-id=1082-488&t=3lQA4TS21KlzzAAJ-1)

### 1. 디자인 시스템 리서치
- 디자인 시스템 선정 기준
    1. 디자인 시스템에 대한 설명 문서와 피그마 파일에 권한 요청없이 접근 가능한가?
    2. 웹 디자인 문서에서 라이브 데모로 상태변화를 관찰 가능한가?

    | 디자인 시스템 | KRDS | Microsoft Fluent 2: iOS  | IBM Carbon DS |
    |---|---|---|---|
    | 주요 서비스 환경 | 공공 서비스 | 운영체제, 생산성 도구 | 엔터프라이즈, B2B |
    | 분석하기 좋은 영역 | 디지털 포용성<br>서비스 과업 흐름 | 인터랙션 상태, 접근성 | 복잡한 컴포넌트 분석<br>(Data Table, Form) |
    | 문서 및 피그마 접근 권한 | 공식 제공 | 공식 제공 | 일부 권한 제한 |
    | 장점 | 번역이 필요 없음<br>상세한 UI 용도 설명<br>라이브데모 가능 |  비교적 자연스러운 웹문서 번역<br>라이브데모 가능 | 라이브데모 가능 |

#### 최종 선정한 디자인 시스템: Microsoft Fluent2: iOS [공식 웹문서](https://fluent2.microsoft.design/get-started/design)
- 이유
    - 공식 문서와 Figma UI Kit(웹/앱)를 권한 요청이나 환경 세팅없이 열람 가능하고 공식 문서에서 제공하는 라이브 데모로 상태 변화를 바로 확인할 수 있어서 좋았습니다. <br>
    또한, 사용자 경험(UX)과 AI와 함께 일하며 주의해야 할점 등 프로덕트 디자이너가 설계 과정에서 고려해야 할 가이드 라인 내용도 함께 제공하고 있어 앞으로 꾸준히 참고하기 좋은 시스템이라고 생각했습니다.

#### 만들어볼 컴포넌트 종류: Button, Card, Card Nudge(Toast)
- 이유
    1. Button: 핵심적인 요소이며 다양한 상태를 가진 버튼의 기본기를 확실히 배워보고 싶습니다.
    2. Card: 썸네일은 어떻게 적용되는지, 레이어 구조의 어디쯤 오버레이가 위치하는지 분석하고 싶습니다.
    3. Card Nudge(Toast): 둘의 차이점을 이해하고 Card Nudge 컴포넌트 사용 예시까지 만들어보고 싶습니다.

> ✅ ***실습의 핵심***<br>
좋은 디자인 시스템을 직접 골라보고, 컴포넌트를 만들고 바꿔보며 그 규칙을 이해해보기.

### 2. 컴포넌트 | Microsoft Fluent 2: iOS
1. Button
- 제공되는 상태
    - Style: Accent, Outline Accent
    - State: Rest, Pressed, Focused, Disabled
    - Label: Text
    - Icon: Boolean

- 상태에 따라 달라지는 부분: 배경 색상, 라벨 색상, 테두리

> 버튼처럼 위계가 존재하고 다양한 상태가 있는 컴포넌트는 하나의 Variant 세트에서 프로퍼티를 적용해준다.<br>
ex. "Style: Primary, Secondary", "State: Default, Pressed, Focused, Disabled"

2. Card
- 제공되는 상태
    - Size: With Preview, Small
    - More: Boolean
    - L Icon: Boolean
    - Subtext: Boolean

- 상태에 따라 달라지는 부분: 프리뷰 이미지 유무, 서브 텍스트 유무, 아이콘 유무<br>
-> Image placeholder: 썸네일 사진이 올라가는 레이어 영역의 이름.<br>

3. Card Nudge
- 제공되는 상태
    - Style: Default, Outline
    - Subtitle: Boolean
    - Show icon: Boolean
    - Action: Boolean
    - Dismiss: Boolean
- 상태에 따라 달라지는 부분: 배경 색상, 부제목 유무, 행동 버튼 및 닫기 버튼 유무, 타이틀 왼쪽 아이콘 유무

---
#### 실습 메모
- 새롭게 알게된 점
    - Drop Shadow 스타일 수치를 뜯어보니, 8배수 규칙으로 세팅돼 있었다. <br>
    스타일 하나에 두 개의 드롭 섀도우가 있었고, 그동안 하나의 그림자만 사용해 온 디자인보다 훨씬 정돈되게 느껴졌다.
    - 아이콘의 사이즈도 Variant로 관리 가능하다.
    - 제목이 존재하는 Navigation bar는 Left, Center, Right로 영역이 구성돼있다.
    - Card Nudge와 Toast의 차이점
        1. Card Nudge: 기존 콘텐츠를 밀어내고 레이아웃의 변동이 생기는 알림 카드.<br>
        목적: 사용자가 어떤 기능이나 행동을 발견하고 유도하는 컴포넌트.<br>
        ex. 새로운 업데이트가 있어요. 확인해보세요!

        2. Toast: 화면의 상/하단에서 오버레이 형식으로 나타나는 일시적인 알림.<br>
        목적: 사용자가 수행한 행동의 결과나 상황을 짧게 알려주는 컴포넌트.<br>
        ex. 네트워크 연결에 실패했습니다.

- 어려웠던 점
    - Variant 세트를 만들고 인스턴스를 복제했는데 오른쪽 패널에서 속성 변경이 불가능하면, 프로퍼티 연결을 다시 확인할 것.

- 개인적인 회고
    - 디자인 시스템 최종 선정을 위해 다양한 문서들을 보며 하나의 디자인 시스템만으로는 적절한 사용법과 다양한 응용을 해보기 부족하다는 생각이 들었습니다.
    - 만드려는 컴포넌트가 다른 서비스에서는 어떤 형태를 띄는지 자연스레 궁금해지고 부족했던 UI 시스템 정의나 디자인 토큰 등을 습득하게 돼 의식적으로 디자인 시스템을 찾아보는 시간을 가져야겠다 생각했습니다.
    - 수업 시간에 배워보지 않았던 새로운 컴포넌트를 만들어보고 싶었는데, 되려 기본기를 탄탄히 다지는게 더 중요하다고 느껴졌습니다. 다음엔 KRDS를 참고해 디지털 포용성을 중점으로한 디자인 시스템을 분석해보려고 합니다.