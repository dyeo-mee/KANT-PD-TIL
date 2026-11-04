## 1. Navigation / Tab-bar
> 화면 상/하단에서 사용자의 위치를 알려주는 기능
- Top bar(navigation)
    - 화면 맨 위에서 현재 위치와 가능한 동작을 보여주는 영역.<br>
    → 화면 역할에 따라 구성이 달라짐. ex. 홈 헤더, 뒤로가기, 검색

- 뒤로가기 탑바 구조: 터치반경 아이콘(44x44), 제목(fill container)
    - 탑바의 아이콘이 비어있는 화면의 경우 spacer를 넣어 제목 정렬을 유지
    - 닫기와 뒤로가기 - 페이지 역할과 사용자의 행동 예측에 따라 설계할 것.<br>
    → 하이어라키: 상위 계층으로 이동.<br>
    → 히스토리: 페이지 이동 기록을 역순.<br>
    [닫기와 뒤로가기 어떻게 다를까?](https://medium.com/prnd/닫기와-뒤로가기-어떻게-다를까-헤이딜러-ux-스터디-f97d83ee17ba)

- 하단 탭바
    - 선택 상태: 현재 위치를 알려주는 표시. 색, 굵기, 채운 아이콘 3가지를 함께 바꿈
    - 탭 항목 해부도
        - 아이콘: 최소 24px 권장, 선택 시 채운 아이콘으로 변경
        - 간격: 아이콘과 라벨의 간격은 4px
        - 라벨: 선택/Bold, 비선택/Medium
        - 위아래 패딩: 16, 가운데 정렬
        - 터치 영역: 탭 항목 전체를 적용하며 44px 이상
        - 크기: Width,Height fill container. 각 탭 영역이 같은 폭으로 유지되게끔 함.
    - 탭의 개수는 3~5개가 적당함. 개수가 많으면 터치영역이 좁아지거나 잘릴 우려.

- 상단 탭
    - Segment Tab(세그먼트 탭): 한 화면에서 내용을 나눠서 보여주는 탭 영역.<br>
    -> 세그먼트 탭 아래 밑줄로 화면 상태를 알려줄 땐, 프레임에 Stroke 속성을 주는게 개발 협업에 유리하다.<br>
    (개발자 도구에서 빠르게 속성 확인이 가능)

> 💡 tab-bar 아이콘은 solid, 폰트 굵기를 함께 바꿔 사용자에게 화면 전환 상태의 가시성을 높여주자.

## 2. Card/ Calendar
> 카드의 구조를 나누고 이미지 비율 고정하기<br>
7열 캘린더를 만들어 날짜와 셀 상태 표시해보기

- 카드 구조<br>
    → 한 가지 대상을 한 덩어리로 보여주는 묶음. <br>
    필요에 따라 썸네일 이미지, 정보, CTA(Call to Action)로 쌓음
    - 카드 종류: Stacked, List
    - 썸네일 이미지 비율 고정: 16:9, 1:1 *(Lock aspact ratio)*<br>
    → ***이미지 width/height 속성은 fill***

- 텍스트 넘침
    - 구조 유지 법칙: 카드 내용이 달라져도 크기와 자리 배치는 그대로여야 함.<br>
    (Truncate text: 부모 요소의 크기만큼 표시하고 생략(…)하는 기능)

- 캘린더 - 7열 그리드: 날짜 셀 7개를 가로 AL(Auto Layout) 세로로 쌓음.<br>
    → 숫자 셀은 모두 fill container.
    - 목적에 따라 선택 가능한 옵션을 예외 처리 하는것이 중요함.<br>
    ex. 날짜가 지났거나, 아직 예약이 불가능한 날짜는 선택이 불가능하게 disabled 처리
    - 날짜 셀 상태: 날짜마다 상황을 다르게 보여줌.<br>
    → 사용자에게 제공해야하는 정보를 Color, Stroke, Solid, Dot 상태로 알려주는 것. 

> 💡 카드는 이미지 비율과 텍스트 줄임으로 비율을 유지하고, 날짜 셀은 상태 값으로 정보를 나타낸다.

---
### Figma 실습 자료
- [실습 자료 링크](https://www.figma.com/design/NHR0qJ0VxtBZRtPmaPi554/-%EA%B9%80%ED%98%84%EA%B2%BD--Figma-%EB%A7%88%EC%8A%A4%ED%84%B0-%EC%8B%A4%EC%8A%B5?node-id=4057-738&t=lsR0Gj1jUV42GRb5-1)<br>
->  하면서 느낀 점:<br>
    - 알림 dot은 stroke 옵션에 따라 크기가 달라지므로 신경쓰기(inside, outline)
    - 세그먼트 탭의 line은 Frame에 stroke 속성을 넣는 걸 추천(개발 모드에서 확인이 쉽기 때문)
    - 카드에 곡률을 줄 땐 최상단 프레임에 radius 주기. (이미지, body content에 직접 radius 설정하지 않기)
    - 복제한 요소 한번에 가로/세로 정렬하기
        1. 마지막 요소 하나를 일정 간격 떨어뜨려놓고 복제한 요소들을 shift로 모두 잡는다.
        2. Position 탭의 Alignment > 오른쪽 끝 ‘more action’ > distribute (horizontal/vertical) spacing
    - cmd+shift+h : 숨기기/보이기
    - 캘린더 날짜 요소처럼 정사각 프레임이 작아 폰트 레이아웃이 깨지면 폰트 > width:hug 속성 적용하기.
    - 캘린더처럼 날짜 정렬이 깨지면 안되는 요소는 min width를 설정해준다!
    - 카드 슬라이드(card carousel): 부모요소인 viewport의 너비가 자식요소인 카드들의 너비보다 작아야 스크롤 가능함. 또한 viewport: clip content ON 설정하기.