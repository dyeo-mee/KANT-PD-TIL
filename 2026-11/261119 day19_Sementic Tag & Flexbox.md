## 1. HTML 구조와 시맨틱 태그
>시맨틱 태그가 필요한 이유를 접근성과 연결해 설명할 수 있음<br>
디자이너가 HTML을 알면 무엇이 좋은가?

- 웹 화면의 재료 - 3대 언어
    - HTML(구조): 웹 페이지의 뼈대와 구조.<br>
        → 여는 태그와 닫는 태그가 존재<></>(예외도 있음 ex. img, input)<br>
        → 속성 type=”” 태그에 붙이는 추가 요소
    - CSS(디자인): 어떻게 보이는지 나타내는 스타일.
    - JavaScript(기능): 누르면 무엇이 바뀌는지 동작과 반응.<br>
    
    → 개발자와 협업 의도도 있지만 내가 디자인하는 화면이 어떻게 구현되는지 파악하고 있어야 하는 이유도 중요함

- 디자인과 코드: Figma에서 만든 것은 웹에서 각자 맡는 언어가 있음.

    | Figma | Web |
    |---|---|
    | 레이어, 프레임 | HTML 태그 |
    | Fill, 글자, 간격, Auto Layout | CSS 속성 |
    | 프로토타입, 상태 전환 | JS 이벤트, 상태 변경 |
    | 컴포넌트 | React(재사용하는 코드 묶음) |

- 시맨틱 태그: 의미를 나타내는 태그. 보이는 화면은 같아도 ***⇒ 보조 기술이 읽는 내용이 달라짐***

> ✅ Figma 레이어가 곧 HTML의 구조가 됨.

## 2. CSS 박스 모델과 Flexbox
> Auto Layout은 코드에서 무엇이 되는가?
- CSS: 어떤 요소의 무엇을 어떻게 바꿀지 적는 규칙
    - 선택자: 어떤 요소에 적용할지 정하는 것. ***#(id) - 단일요소, .(class) - 다중요소***
    - 속성: 무엇을 바꿀지 정하는 것 (ex. 배경색, 패딩, 그림자)
    - 값: 얼마나 어떻게 적용할지 적는 수치 (ex. 16px, #0057FF)

- 박스 모델: 웹의 모든 요소는 상자로 이루어짐.
    - 내용(label) → 안쪽 여백(padding) → 테두리(border line) → 바깥 여백(margin) 순서로 감싸짐

- Figma와 CSS

    | 개념 | Figma | CSS |
    |---|---|---|
    | 안쪽 여백 | Auto Layout: Padding | padding |
    | 테두리 | Stroke(Inside, Center, Outside) | border |
    | 요소 사이 간격 | Auto Layout: Gap | gap |
    | 바깥 여백 | 부모요소의 Gap or Padding | margin |

    → 피그마에서 오토 레이이웃으로 자동정렬되면 gap, 프레임을 수동정렬하면 margin으로 반영됨.

- Flexbox: 요소를 가로/세로로 나란히 놓고 간격, 정렬을 정하는 CSS 방식 = Figma Auto layout

    | Auto Layout | Flexbox | 뜻 |
    |---|---|---|
    | 정렬 | justify-content, align-item | 방향쪽, 반대쪽 정렬 |
    | Hug | width: auto (fit-content) | 내용만큼 차지함 |
    | Fill | flex: 1 / width: 100% | 부모요소만큼 늘림 |
    | Fixed | width: px | px 값 고정 |
    | Wrap | flex-wrap: wrap | 영역을 넘으면 다음 줄로 넘김 |

    - flexbox를 사용할지 정의하는 속성: display<br>
    → default, flex, inline-flex
    - flexbox의 옵션 값을 설정하는 속성: flex-direction, flex-wrap, flex-flow<br>
    - flex 위치를 지정하는 속성: justify-content, align-items, align-content<br>
    → justify-content: X 축 정렬<br>
    → align-items: Y 축 정렬<br>
    → align-content: 행간 여백(flex 된 요소가 여러줄인 경우)<br>
    [[CSS flexbox|브런치]](https://brunch.co.kr/@swimjiy/25)

- Figma의 Auto layout 설정은 그대로 CSS(Flexbox) 코드가 됨.<br>
→ 웹에선 글자 크기에 rem 수치를 사용. 폰트 크기를 지정해놓으면 디바이스마다 비율로 줄고 늘게끔 함.<br>
→ Display: flex = Figma: Auto Layout

## 3. JavaScript와 상태
> 화면과 버튼에 필요한 상태를 빠짐없이 나열할 수 있다.<br>
실제 데이터의 제약을 디자인에 반영할 수 있다.

- JavaScript 역할: 사용자 행동을 감지해 값을 바꾸고, 값에 맞게 화면을 다시 그림.
    - 사용자 행동 → 이벤트 감지 → 상태 변경 → 화면 변경
    - 상태(State): 지금 화면이 어떤 모습인지 정하는 값.

- 화면 상태: 로딩(skeleton), 빈 화면(empty state), 오류(error), 정상<br>
→ 발생 가능한 모든 변수를 고려해 화면을 설계함 = 버튼과 같은 컴포넌트의 상태도 포함

- 구현 제약 - 시안과 실제의 차이<br>
실제 데이터: 시안은 이상적인 데이터로 예상해 그리지만 실제 데이터는 길고, 비어있고, 느림.
    1. 긴 글자: 생략된 모습도 설계
    2. 빈 데이터: 후기가 없는 상태의 화면도 예상하고 그려둠.
    3. 느린 응답: 데이터를 전송하거나 받는 상황을 사용자에게 실시간으로 보여줘야 함.
    4. 다른 화면: 다른 환경의 디바이스에서 어떻게 보여질지 고려함.

---
- [실시간 실습](https://www.figma.com/design/uEVcMFnERuCLrQliZDqY6d/5%EC%A1%B0---%EB%AC%B4%ED%99%94%EA%B3%BC-4---UX-UI-%EC%8B%A4%EC%8B%9C%EA%B0%84-%EC%97%B0%EC%8A%B5--%EA%B9%80%EC%A7%80%EC%9C%A0-%EA%B9%80%ED%98%84%EA%B2%BD-%EA%B9%80%ED%98%84%EC%A7%80-?node-id=4153-2218&t=GAVlU0uHkvkiXz4k-1)<br>
→ 하면서 느낀 점
    - 썸네일을 이미지 자체로 넣지말고, 프레임으로 한번 더 묶으라는 이유<br>
    → 오버레이나 버튼이 이미지 위에 올라가는 구조도 있기 때문임
        ```html
            <div>
            <img src="">
            <button></button>
            <div>오버레이 영역</div>
            </div>
        ```
    - HTML/CSS/JS docs: [developer.mozilla](https://developer.mozilla.org/ko/docs/Web/HTML),[w3schools](https://www.w3schools.com/html/default.asp)