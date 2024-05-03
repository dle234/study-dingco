<aside>
💡 **이번 장에서 살펴볼 내용**

- 액션, 계산, 데이터의 차이점 이해
- 액션, 계산, 데이터를 구분해서 적용
- 액션이 코드 전체로 퍼질 수 있다는 것을 이해
- 이미 있는 코드에서 어떤 부분이 액션인지 찾기
</aside>

# 📘 액션 vs 계산 vs 데이터

### ✅ **액션**

외부 세계에 영향을 주거나 받는 것

**실행 시점과 횟수에 의존**

부수 효과, **부수 효과가 있는 함수**, 순수하지 않은 함수라고 불림
ex) 이메일 보내기, 데이터베이스 읽기

**액션을 잘 사용하는 방법**

- 가능한 액션을 적게 사용하기
- 액션은 가능한 작게 만들기
- 액션에서 결정이나 계획과 관련된 부분은 계산으로 빼내기
- 액션이 외부 세계와 상호작용하는 것을 제한
- 액션이 호출 시점에 의존하는 것을 제한

---

### ✅ **계산**

입력값으로 출력값을 만드는 것
실행 시점과 횟수에 관계없이 **항상 같은 입력값에 대해 같은 출력값 반환**
**순수 함수**, 수학 함수라고 부르기도 함
**어떤 것을 결정**하는 일은 `계산` 으로 표현 가능
ex) 최댓값 찾기, 이메일 주소가 올바른지 확인하기

**어떻게 계산에 의미를 담을 수 있을까?**
계산에는 **연산**을 담을 수 있음

**액션보다 계산이 좋은 이유**                                                              

- 테스트하기 쉬움.
- 기계적인 분석 쉬움. 정적 분석에서 자동화된 분석 중요
- 조합하기 쉬움. 계산을 조합하여 더 큰 계산을 만들 수 있음 → `일급 계산` 사용

---

### ✅ **데이터**

이벤트에 대한 사실

**일어난 일의 결과**를 기록한 것

ex) 이메일 주소, 은행 API로 가져온 달러 수량

**어떻게 구현?**

기본 데이터 타입으로 구현 (number, string, array, object 등)

**어떻게 데이터에 의미를 담을까?**

데이터 구조로 의미 부여

**불변성**

1. 카피 온 라이트 : 변경할 때 복사본 생성
2. 방어적 복사 : 보관하려고 하는 데이터의 복사본 생성

**데이터의 장점**

- 직렬화
- 동일성 비교
- 자유로운 해석

**데이터의 단점**

해석이 반드시 필요함

해석하지 않은 데이터는 의미 없음

---

<aside>
💡 계산은 **계획이나 결정**을 할 때 적용

데이터는 계획하거나 **결정한 결과**

액션을 통해 **계산으로 만든 계획 실행**

</aside>

# 📘 액션 → 계산, 계산 → 데이터

**액션이 계산이 될 수 있는지, 계산은 데이터가 될 수 있는지 고민하기**

장보기 목록을 결정하는 것 → 계산
실제 구입하는 단계와 구입할 것을 결정하는 단계로 분리 → 액션과 계산을 나누는 것
**액션 안에는 계산, 데이터, 또 다른 액션이 존재**할 수 있음
**계산은 더 작은 계산과 데이터로 나누고 연결** 가능 → 결정과 계획은 `계산` 일 확률이 높움
데이터는 데이터만 조합 가능

# 📘 쿠폰 보내는 과정 예시

데이터베이스에서 구독자 가져오기 → 액션 (구독자는 실행 시점에 따라 바뀌기 때문)
데이터베이스에서 가져온 구독자 목록 → 데이터

### 🚨 데이터베이스에서 쿠폰 목록 가져오기

데이터베이스에서 쿠폰 목록 가져오기 → 액션
→ 쿠폰 DB는 실행 시점에 따라 바뀌기 때문
가져온 쿠폰 목록 → 데이터

**이벤트 : DB에서 쿠폰 목록 가져오기 / 데이터(이벤트에 대한 사실) : 쿠폰 목록**

### 🚨 보내야 할 이메일 목록 만들기

이메일 목록 계획하기 → 계산
이메일 목록 → 데이터 (보내야 할 이메일을 계획한 결과)

**이메일 목록을 계산할 때 구독자 목록과 쿠폰 목록을 받는다**

가능하면 액션을 쓰지 않으려 하고, 계산으로 바꿀 수 있는 액션이 있다면 바꿈

→ **테스트하기 쉽기 때문**

이메일을 실제로 보내고 결과를 주는 시스템 → 테스트 어려움
계산은 외부에 영향을 주지 않기 때문에 결과가 이메일 목록 데이터인 시스템 → 테스트 쉬움

**이메일 목록을 계획하는 계산을 더 작은 계산으로 나누기**

쿠폰 종류를 good 쿠폰, bad 쿠폰으로 나눈다면 **쿠폰 등급을 결정**하는 것을 `계산` 으로 만들기
쿠폰 등급 → 데이터

### 🚨 이메일 전송하기

수신자와 보낸 내용이 앞에서 다 만들었기 때문에 목록을 순회하면서 보내기 → 액션

**계획할 것을 미리 계획했다**

계산을 나누면 구현하기 쉬움

→ But, **충분히 구현하기 쉽다고 생각되는 경우 더 나누는 것 멈추기**

### 🚨 쿠폰 보내는 과정 구현하기

계산인지 확인하기 → `같은 입력값을 넣었을 때 같은 값이 나옴` && `함수 호출 횟수가 외부에 영향을 주지 않음`

# 📘 유의 사항

### 🚨**액션은 코드 전체로 퍼짐**

액션을 호출하는 함수도 액션

그 함수를 호출하는 함수도 액션

액션은 조심스럽게 사용해야함

### 🚨 **액션은 다양한 형태로 나타남**

함수 호출 - alert

메서드 호출 - console.log()

생성자 - new Date()

표현식 - 변수 참조, 속성 참조, 배열 참조

상태 - 값 할당, 속성 삭제

### 🚨 **함수형 프로그래밍의 구현 순서**

데이터 → 계산 → 액션