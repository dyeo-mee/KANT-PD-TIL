## 1. 중첩 Auto layout과 wrap/min, max
- 중첩 Auto Layout
    - 박스 분해: 오토 레이아웃 프레임 안에 또 오토 레이아웃 프레임을 넣는 것.
    - 조립하는 순서: 서로 가깝게 위치한 요소 찾기<br>
        -  안쪽부터 묶기 → 세로로 묶기 → 바깥 묶기 → 사이즈 정하기
        - 작은 묶음에서 큰 묶음으로 요소들을 정리하다보면 레이어 구조가 저절로 정리됨.
        - 반대로, 디버깅을 할 땐 가장 큰 요소(부모요소)부터 시작해 안쪽으로 찾아가기
    - Alignment (정렬 9칸) : 아이콘이나 글자가 한 쪽으로 치우치지 않게 정렬하기

- Wrap: tag와 같이 개수가 많고 늘어날 가능성이 높은 요소들을 묶어 줄바꿈 정렬 시키는 것.

- Min/Max width - hug, Fill로 늘고 줄 때의 한계선<br>
: 최소한 유지해야하는 수치와 최대 늘어나는 값을 지정해둔 것.

- Ignore auto layout
    - 자식 하나만 auto layout에서 제외하고 원하는 자리에 겹치도록 함.<br>
    구) Absolute position
    - 부모요소 안에서 자식요소 하나만 설정하기
    - **Constraints로 정렬 할 위치 정하기**
    - ignore 설정한 요소가 가려지지 않게 레이어 순서 조정하기

- Thumbnail image
    - 썸네일 이미지 속성은 ***Fill*** => 사이즈 변동에 대응하도록
    - 이미지 위에 아이콘이 올라올 경우 *[이미지+아이콘→auto layout]* 으로 묶어 정렬하기

## 2. Auto Layout으로 홈 화면 조립하기
- 화면 구조 설계
    - 고정된 요소 ex.status-bar, header, indicator …
    - 스크롤되는 요소 ex.content/section

- Section: content 안을 나누는 단위
    - 역할에 따라 구분지음
    - 개발자, AI 에이전트는 block 단위로 값을 읽기 때문에 협업에 용이하기 위함
    - 패딩은 섹션 안에 위치하도록 설정

- 섹션 별 조립하는 과정
    1. 화면 프레임 설정
    2. 대표적인 블록 5개: status-bar, header, content, tab-bar, indicator ⇒ ***모두 constraints L+R***
    3. contente 설정: gap, padding, clip content 등 세부 옵션 설정
    4. 섹션 채우기 및 디자인 검수: 섹션의 개수는?, width 값이 fill 인가?, 섹션마다 좌우 padding 설정했는가? <br>
    → 확인과정 거치기.

- 개발 용어와 연관된 Auto layout ↔ CSS Flexbox<br>
: 개발 친화적으로 만들어진 도구로 용어가 비슷함

| Figma Auto Layout | CSS Flexbox | ex |
|---|---|---|
| Direction 세로/가로 | flex-direction: column/row | content 세로, class-card 가로 |
| Gap | gap | content Gap 24 → gap: 24px |
| Padding | padding | section 좌우 20 → padding: 0 20px |
| Alignment | justify-content / align-items | header 양쪽 끝 → space-between |
| Wrap | flex-wrap: wrap | category-chips |
| Fill container | flex: 1 / align-self: stretch | content/info |
| Min/Max width | min-width / max-width | btn/예약하기 min-width: 120px |
| Ignore auto layout | position: absolute | btn/heart |

## 실시간 실습 Figma 링크
[실시간 실습](https://www.figma.com/design/NHR0qJ0VxtBZRtPmaPi554/-%EA%B9%80%ED%98%84%EA%B2%BD--Figma-%EB%A7%88%EC%8A%A4%ED%84%B0-%EC%8B%A4%EC%8A%B5?node-id=1-3&t=laQRxHDrcrVZzw4k-1)
- 하면서 느낀 점
    - 헷갈리는 auto layout설정<br>
    "이 요소들은 콘텐츠가 추가되거나 크기가 변경됐을 때, 다른 요소들과 함께 밀리거나 재배치 되어야 하는가?”<br>
    → Yes: Auto Layout을 적극적으로 고려<br>
    → No: 일반 Frame이나 Ignore auto layout을 고려<br>

    따라서, top-bar/indicator 등과 같이 화면 최상/최하단에 위치해야하는 요소일 경우 부모 프레임을 일반 프레임으로 설정할 것. 

## 과제: 진단평가 화면 재구현하기
[진단평가 실습](https://www.figma.com/design/tuqLDmLTFoSQmChC3CA9og/Kant_%E1%84%89%E1%85%AE%E1%84%8B%E1%85%A5%E1%86%B8_Figma_%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB_%E1%84%90%E1%85%AE%E1%86%AF_%E1%84%8B%E1%85%A7%E1%86%A8%E1%84%85%E1%85%A3%E1%86%BC_%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%83%E1%85%A1%E1%86%AB-%EC%8B%A4%EC%8A%B5-%EA%B3%BC%EC%A0%9C-?node-id=2003-1019&t=YKcSaSGpMivVk4Yy-1)
- 하면서 느낀 점
    - 첫 평가 때보다 레이어 구조를 더 세분화, 더 빠르게 파악할 수 있었다.
    - 역할에 맞는 레이어 네이밍 규칙을 사용했다.
    - 디바이스 크기에 대응해 고정된 요소와 움직여야 할 요소를 판단해 적합한 디자인 옵션을 설정할 수 있었다.
    - 부모요소가 auto layout이고, 자식 요소의 width: fill로 되있는데도 너비가 늘어나지 않으면 '***gap***' 옵션 확인해보기!!