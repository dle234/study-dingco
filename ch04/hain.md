# 04. 액션에서 계산 빼내기

## 📝 핵심 내용

- 암묵적인 입출력을 가진다면 액션이다.
- 반면, 계산은 암묵적인 입출력이 없어야 한다.
- 전역 변수는 암묵적인 입출력을 가지므로 지양해야 한다.
- 명시적인 입출력 (인수와 리턴값)으로 바꿔야 한다.

## 🤔 궁금한 점

- 1. (75p.) 만약 인자로 전달한 배열을 직접 변경한다면, 그 함수는 계산일까요? 계산이 아니라면 왜 아닌가요?

  - 👉 이에 대한 나의 생각: 인자로 전달한 배열을 직접 변경하는 것은 외부 세계를 변경하는, 즉 부수효과를 일으키므로 액션이라고 생각한다. 이를 계산으로 변경하기 위해서는 인자로 전달받은 배열을 복사하여 변경하고, 그 변경한 배열을 리턴해주어야 한다. 그런 다음 해당 함수를 부른 곳에서 리턴값으로 받은 새로운 배열을 재할당 해주어야 한다.
    (재할당 과정은 어쩔 수 없는 액션이 되겠지만 적어도 해당 함수는 계산으로 유지할 수 있다.)

- 2. (84p.) 아래 함수는 계산으로 분리된 함수이다. 이때 20은 기준 정보인데, 이 기준 정보가 바뀌는 것에 대해서는 대응해주지 않아도 되는가? 이 기준 정보도 인수로 빼주어야 하는가?

  - 👉 이에 대한 나의 생각: 상수 분리에 대해 생각해본다. 상수를 분리하는 이유는 휴먼 에러를 막기 위해서이기도 하지만, 상수를 추후 편하게 변경하기 위함이다. 그러나 상수가 변경된다 하더라도, 상수는 프로그램이 동작하는 과정에서 변경될 여지가 없으므로 계산에 해당한다고 볼 수 있을 것 같다. 그러므로 인수로 빼주는 것은 개발자의 선호라고 생각한다. (개인적으로 나는 인자로 기준도 넘겨주어서 util 함수로 사용하는 것을 선호하긴 하는 것 같다. 왜냐하면, 그 편이 사용 범위가 더 넓다고 생각하기 때문이다.)
    (+)그런데 이러한 상수를 전역변수의 개념으로 볼 수 있을까?

```js
function gets_free+shipping(total, item_price){
    return item_price + total >= 20
}
```

## 🚀 더 생각해볼 점

- 전역 변수를 사용하면 안되는 이유

  - 전역 변수를 사용하지 말라고 하고, class 에서 public 멤버 변수를 사용하지 말라고 한다. 우리만의 언어로 그 이유를 정리해보면 좋을 것 같다.

  - `점심 뭐 먹지` 미션에서 음식점 목록(AllRestaurantList)를 인스턴스로 만들어 여기저기서 불러서 사용하고 있다. 즉, 전역변수처럼 사용하고 있다. 그런데 index.js 에서 사용하고 있고, 다른 곳에서도 너무 많이 사용하고 있는데 이럴 경우에도 계속 인자로 넣어주는 것이 더 좋은가?