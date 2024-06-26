# 상태 소개
1. 상태(state)의 정의
- 사물이나 현상이 놓여 있는 모양이나 형편. 

2.  상태의 종류
- 컴포넌트 상태: 컴포넌트 내부에서 관리되는 상태.
- 전역 상태(Global State): 어디서든 접근 가능한 전역적인 상태.
- 서버 상태(Server State): 서버와의 통신을 통해 가져온 상태로, 주로 데이터를 관리.

3. 상태의 관리와 발생하는 문제점
- 상태 변경 및 최적화: 상태를 변경할 때마다 발생하는 렌더링 최적화 등의 문제를 해결해야함.
- 불변성 유지: 상태의 변경 시 불변성을 유지해야함.
- 상태 관리자 선택: 다양한 상태 관리 라이브러리 중에서 적합한 것을 선택하고 관리해야함.


***
# 올바른 초기값 설정
1.  초기값
 - 가장 먼저 렌더링될때 순간적으로 보여질 수 있는 값이기도 함.
 - 당연히 초기에 렌더링 되는 값
2.  초기값을 지키지 않을 경우
 - 렌더링 이슈, 무한 루프, 타입 불일치로 의도치 않는 동작 => 런타임 에러
 - 넣지 않으면? => undefined
 - 상태를 crud => 상태를 지울때도 초기값을 잘 기억해놔야 원상태로 돌아감.
 - 빈값? null 처리를 할 때 불필요한 방어코드도 줄여줌.

 ~~~

{undefinded.map()}

 ~~~


## 결론
- 초기상태를 올바르게 처리하자


***
# 업데이트되지 않는 값

1. 문제점
- 불필요한 렌더링: 매번 컴포넌트가 렌더링될 때마다 변수를 다시 참조하고 계산해야 함. => 성능저하
- 내부 로직 부족: 변수를 변경하지 않는 상태로 가지고 있기 때문에 컴포넌트 내부에는 상태 변화에 대한 로직이 없음.

2. 해결책
- 외부로 내보내기: 컴포넌트가 렌더링될 때마다 변수를 재참조할 필요가 없어짐.
- 리액트 상태로 관리하기: 변수의 변경이 상태로 반영되어 컴포넌트가 적절하게 렌더링됨.

## 결론
 - 업데이트가 되지 않는 일반적인 객체라면 리액트 외부로 내보내기

***
# 플래그 상태

1. 플래그 변수란?
- 프로그래밍 언어에서 플래그 변수란 특정 조건을 나타내거나 흐름을 제어하기 위한 불리언 값. 주로 로그인 여부, 인증 및 인가 상태, 유효성 검사 등 다양한 조건을 표현하는 데 사용됨.

2. 문제점
- 내부 변수 관리: 컴포넌트 내부에서 플래그 변수를 다루는 경우, 매 렌더링마다 조건을 계산하고 변수를 관리해야 함.
- 불필요한 상태 생성: 플래그 변수를 리액트 상태로 만들 경우, 불필요한 상태가 생성되어 코드가 복잡해질 수 있음.

3. 해결책
- 외부 변수 활용: 컴포넌트 외부에서 플래그 변수를 정의하고 조건식에서 직접 참조하는 방법. 이렇게 하면 렌더링 시마다 변수를 다시 계산할 필요가 없어짐.
- 컴포넌트 내부 변수: 플래그 변수를 useState 등을 사용하여 상태로 만들지 않고, 컴포넌트 내부에서 변수로 관리. 간단한 플래그 변수의 경우에는 상태를 만들지 않고도 쉽게 관리할 수 있음.

## 결론
- useState 대신 플래그로 상태를 정의할 수 있다.


***
# 불필요한 상태

1. 변수 활용의 필요성
- 변수를 활용하여 컴포넌트 내부에서 특정 값을 다뤄야할 경우가 있음.

2. 필터링 예시
- 완료된 일만 필터링: filter 함수를 사용하여 completed가 true인 항목들만 골라내는 방식.

3. 내부 변수 활용의 장점
- 렌더링마다 고유 값: 컴포넌트 내부에 변수를 만들고, 렌더링될 때마다 이 변수를 활용하여 계산된 값을 사용할 수 있음. 컴포넌트 내부에서 고유한 값이 필요한 경우에 유용.
- 상태 조작 최소화: 내부 변수를 활용하면 상태를 조작하지 않고도 원하는 값을 얻을 수 있으며, set state를 사용하지 않아도 됨.

## 결론
- props를 useState에 넣지 않고 바로 return문에 사용하기
- 컴포넌트 내부 변수는 렌더링마다 고유한 값을 가짐.
