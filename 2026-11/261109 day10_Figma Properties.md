## 1. Component Properties
- 프로퍼티로 관리 해야하는 이유<br>
: Variants 폭증. 경우의 수 마다 개수가 곱셈으로 늘어나기 때문

- Property 4종
    - Variant: 모양, 상태가 달라질 때 ex.State=Disabled
    - Text: 문구만 바뀔 때 ex.예약하기 → 대기신청
    - Boolean: 보이기, 숨기기 ex.Show icon=off
    - Instance swap: 같은 자리, 다른 부품 ex.heart icon ↔ check icon
    
    → 인스턴스를 고르면 오른쪽 패널에서 바로 바꿈. “고쳐도 되는 자리”를 main에서 지정.

- Property 3종 만들기
    - 속성 패널: Property는 만들고 레이어에 연결해야 동작함.<br>
        → 인스턴스를 고르고 오른쪽 디자인 패널에 variant와 property가 모여 보임.<br>
        *레이어를 열지 않고 패널에서 바꾸는게 핵심.*
        
    - 레이어 연결

        |---|---|---|---|  
        | Property | 연결하는 레이어 | 만드는 법 | 인스턴스에서 |  
        | Text | 텍스트 레이어 | 텍스트 레이어 선택 → 연결 아이콘 | 글자 입력 |  
        | Boolean | 숨길 수 있는 레이어 | 레이어 선택 → layer 영역 연결 아이콘<br>(Layout 아래 Apperance 설정) | 토글 켜기/끄기 |  
        | Instance swap | 아이콘 인스턴스 | 인스턴스 선택 → 연결 아이콘 | 목록에서 고르기 |

        1. Main Component(혹은 Component Set) → 오른쪽 패널 properties 옆 **+** → 타입, 이름, 기본값 입력 → 연결
        2. 적용할 레이어 선택 → 오른쪽 패널 속성 연결 아이콘(apply variable/property)
        - Boolean: ***(Layout 아래 Apperance 설정에서 연결 가능)***

        → 연결 확인: main 레이어 이름 옆에 속성 표시 생김.(인스턴스 패널에서 바꿨을 때 캔버스가 바뀌면 성공)

        - Preferred values: Instance swap 목록에 먼저 보여줄 컴포넌트를 정하는 기능.<br>
        → 아이콘이 많아도 자리에 맞는 것만 골라 보여줌.


- Variant와 Property
    - 구분 기준
        - 모양(색/크기/배치)이 달라지면 ***Variant***
        - 내용, 표시 여부, 부품 교체는 ***Property***

    - Property 이름<br>
    : 속성 이름은 패널에 바로 보임. 무엇을 바꾸는지 바로 알 수 있게, 같은 규칙으로 네이밍.


## 2. 라이브러리 정리와 발행
> 컴포넌트 라이브러리 페이지를 Cover/Foundations/Components로 나눠서 구성<br>
섹션/이름/설명(desc) 규칙으로 컴포넌트를 정리<br>
라이브러리 Publish하고 다른 파일에서 Update 받는 흐름 이해하기

- 라이브러리 페이지
    - 페이지 구조
        - 표지(Cover)
        - 색, 글자 기초(Foundations)
            1. 아토믹(원색표): 색 자체에 붙인 이름 ex.blue/500, gray/900
            2. 시맨틱(역할/용도): 스타일 이름 ex.text/primary, status/error
        - 부품(Components)
    - 정리 규칙<br>
    : 섹션으로 묶고 이름은 슬래시 규칙으로 지음. 설명은 Main component의 description에 적음.
    → description은 팀원, 개발자, AI가 읽는 설명서

- Publish와 Update
    - 발행/업데이트 흐름<br>
        : 라이브러리 파일에서 publish하면 다른 파일에서 컴포넌트를 불러 씀.
        → main component를 수정하고 다시 publish하면, update를 눌러야 반영됨.

    - 발행 전 확인할 내용들
        - 플랜: 유료 플랜에서 발행
        - 파일 위치: 드래프트 파일은 발행 불가
        - 권한: Full seat + 편집 권한
        - 발행 버튼: 컴포넌트여야하고, 바뀐 내용이 있어야 켜짐.

- 좋은 라이브러리란?<br>
    : 처음 열어본 사람도 찾고, 고르고, 바로 쓸 수 있어야한다.
    
    - 찾기 - 섹션으로 나뉨, 기본 이름이 없음, description 있음.
    - 고르기 - 일관된 variant 이름, property 연결 → 속성 패널만으로 변형 가능
    - 쓰기 - 예시 화면 1개 이상 제공, 인스턴스로만 조립됨, detach 없음
    (detach를 사용하면 컴포넌트 연결이 끊어지므로 일괄 수정이나 유지보수가 어려워짐.)

    > 💡 기존 컴포넌트를 최대한 재사용하면서도 필요한 디자인 변경은 Variant, Properties, Overrides 등을 통해 유연하게 할 수 있도록 설계하는 것이 중요 !!!

    <details>
        <summary>Publish → 다른 파일에서 쓰기 → Update 받기</summary>
        - 내 파일을 팀 프로젝트로 옮김(드래프트 파일은 발행 불가.)<br>
        - 왼쪽 Assets⊕ → 라이브러리 아이콘 → This file 옆 Publish → 라이브러리 이름적고 Publish<br>
        - 새 디자인 파일에서 Assets 탭 → 내 라이브러리 켜기.<br>
        - Publish 한 라이브러리 요소로 화면을 만들어보고 기존 작업 파일로 돌아와 원본 컴포넌트를 수정 후 다시 발행하기.<br>
        - 새 디자인 파일에서 라이브러리 아이콘에 파란 배지가 뜨면 수정된 내용이 있다는 뜻.<br>
        → Update 하기 전, 바뀐 내용을 검토하고 적용.
    </details>

---

- [실시간 실습](https://www.figma.com/design/NHR0qJ0VxtBZRtPmaPi554/-%EA%B9%80%ED%98%84%EA%B2%BD--Figma-%EB%A7%88%EC%8A%A4%ED%84%B0-%EC%8B%A4%EC%8A%B5?node-id=36-6000&t=KV0sR7CtWkp4khXO-1)<br>
    → 하면서 느낀 점
    - 인스턴스에 Property를 지정해두면, 복제해 사용 할 때 레이어 구조를 들여다보지 않아도 오른쪽 Variant/Property 패널에서 수정이 용이하다.
    - 썸네일(Thumbnail)은 컴포넌트라서 Instance swap으로 추가함.(아이콘 처럼)
    - 라이브러리 설명은 컴포넌트(혹은 Variants set)에서만 작성/수정 가능함. 
    → 복제된 인스턴스에선 설명이 읽기 전용으로 보임.
    - Component Property 및 라이브러리 점검 체크리스트<br>
        [ ]  기본 이름(Component, Frame12)이 하나도 없음<br>
        [ ]  Cover에 이름, 버전, 업데이트 날짜, 구성이 있음<br>
        [ ]  모든 컴포넌트에 description, 사용법이 적혀있음<br>
        [ ]  속성 패널만으로 인스턴스를 바꿀 수 있음(연결 누락 0)<br>
        [ ]  예시 화면의 부품이 모두 인스턴스이고 Detach 없음<br>