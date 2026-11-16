> *사용자가 어려워하는 화면은 어떻게 찾는 걸까?*<br>
→ 프로토타입 Flow(흐름)가 끊기지 않고 어떤 화면에서든 자연스럽게 연결되게끔 하는 것.<br>
흐름이 끊기는 지점이 곧 개선해야할 포인트!

## 1. Flow, Connection, Trigger
- 프로토타입의 목적: 화면을 실제 앱처럼 눌러보게 만든 시안.<br>
    → 개발 전, 흐름을 확인하고 팀과 같은 그림을 보기 위해 만듦.
    - 검증 - 개발 전 흐름을 눌러보며 문제 찾기
    - 공유 - PM, 개발자, 고객사가 같은 흐름을 보며 소통 가능.
    - 설명 - 움직임과 전환을 말 대신 보여 줌

- 프로토타입 기초
    - Prototype 탭과 Flow 시작점
        - Flow 시작점은 재생을 시작하는 첫 화면
        - 인터랙션: 상호작용 요소, Trigger/Action/Animation

- 연결의 3요소
    - Trigger: 발동 조건(언제)
        - After Delay: 앱 시작 후 사라지는 첫 화면(splash)의 시간(300ms)을 정함.<br>
        → 실제 앱에선 시작 로딩이 끝나면 사라지고, 프로토타입에선 모션만 따라하는 셈.
    - Action: 트리거가 발생하면 “무슨 행동”을 할지 정하는 역할.(어디로)
        - Destination: 도착 지점(⊕ 드래그해서 지정)
        - Back: 히스토리 백(하이어라키(계층) back은 Navigate to→ 사용)
        - Scroll to: 버튼을 누르면 특정 지점으로 스크롤.
    - Animation: 어떻게(모션 지정)
        - 하단 탭바같은 경우 한 화면에서 움직이는 모습을 의도하므로 *Instance 애니메이션*을 씀.

- Flow 흐름도<br>
    : 화면이 끊기는 지점 없이 계속 이어질 수 있게 확인.
    - 막힌 경로(dead end): 들어갔는데 나갈 길이 없는 화면.
    - 재생과 공유<br>
        : Present ▶️ 재생 후  화면에서 Flows(목록) 선택 가능.
        - R: 리셋
        - Share: 프로토타입 링크
    > 💡 필요에 따라 클로드로 코드베이스 시안을 만들거나 프로토파이 같은 서비스로 딥한 인터렉션 시뮬레이션을 만들기도 함.

## 2. Smart Animate·Overlay·Scroll
- Animation 기초
    - animation 종류: 화면이 어떻게 전환될지 정하는 것.
        - Instant: 바로 바뀜
        - Dissolve: 서서히 겹치며 바뀜
        - Move in: 새 화면이 위에 덮임
        - Push: 새 화면이 밀어냄

    - Smart Animate: 같은 이름을 가진 레이어 모습으로 변환됨
    (레이어 이름과 구조가 같아야 올바르게 동작함.)<br>
    → 애니메이션을 고르는 기준? 화면의 목적과 형태를 파악해 어떤 전환이 자연스러운지 판단력을 길러야 함.

    - Easing & Duration
        - Easing: 속도가 변하는 모양
        - Duration: 변하는 시간

- Smart Animate 동작 조건
    - 이름이 같음 → 부드럽게 동작
    - 두 화면에서 이름(과 계층)이 같은 레이어를 찾아 위치나 모양을 알아서 변환되게 함.
    - 반대로 함께 동작하지 않게 연결을 끊고싶다면, 레이어 명을 다르게 수정하기.

- 바텀시트 Overlay<br>
    : 지금 화면 위에 다른 프레임을 겹쳐 띄우는 Action.<br>
    → 잠깐 띄워놓고 닫는 모달 같은 요소에 많이 사용.
    - position 및 시트 안 버튼까지 동작하게 설정에 유의하기!

- Scroll - 고정헤더, 하단 바<br>
    : 움직이지 않게 고정되야할 요소는 constratint L+R top/bottom 설정하기<br>
    ***Scroll Behavior: Position Fixed***
    
    - 가로 스크롤<br>
        : 부모요소인 viewport의 너비가 자식요소인 카드들의 너비보다 작아야 스크롤 가능함. 
        또한 viewport: clip content ON 설정하기.

- Fixed, Sticky, Overflow
    - Overflow: 스크롤 방향
    - Fixed: 처음부터 고정된 위치
    - Sticky: 지정된 위치에 스크롤이 닿으면 이후부터 따라다님. 스크롤 지점을 되돌아가면 원래 위치로.<br>
        → Autolayout 안의 요소는 Fixed/Sticky 적용이 불가능. ***ignore auto layout 설정을 켜야함!!***

---

- [실시간 실습](https://www.figma.com/design/NHR0qJ0VxtBZRtPmaPi554/-%EA%B9%80%ED%98%84%EA%B2%BD--Figma-%EB%A7%88%EC%8A%A4%ED%84%B0-%EC%8B%A4%EC%8A%B5?node-id=36-3594&t=KV0sR7CtWkp4khXO-1)<br>
→ 하면서 느낀 점
    - 하단 탭바에 인터랙션을 넣게되면 갯수만큼 곱해져 연결선이 복잡해진다.<br>
    → 이럴 때 하단 탭바를 메인 컴포넌트로 만들고 각 탭을 화면에 연결해주면, 복제된 인스턴스들은 부모인 메인 컴포넌트의 인터랙션을 상속받게됨. 결과적으로 연결선 12개 → 4개로 줄어들게 된다!
    - 하단 오버레이 창닫기 버튼은 Action: Back이 아닌 Close overlay로 지정.
    - 찜 눌렀을 때 떠오른 토스트 탭은 일정 시간이 지나 사라지게끔(After delay: 1500ms) 화면 전체에 적용함.
    <details>
        <summary>Smart Animation 적용 후 같은 화면에서 다른 애니메이션을 적용할 수 있을까?</summary>
        피그마에서 만든 프로토타입은 개발 단계에 가기 전, 사용성 테스트(UT/유저 테스트)를 위해 임시로 만들어둔 기능이다.<br>
        따라서 개발 단계에서 필요한 디테일 요구사항은 User Flow나 Wire Frame 단계에서 작성하고, 프로토타입에서 한 화면에 여러 애니메이션을 적용하는 건 불가능하다.<br>
        (피그마의 프로토타입 애니메이션 종류/적용의 한계가 존재하기 때문.)
    </details>