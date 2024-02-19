

# 🧑🏼‍🚀 Execution Context, Scope를 알아야 하는 이유

❗이후에 나올 Closure를 비롯해, 자바스크립트가 어떻게 실행되는지 원리를 이해하고 싶다면

# 🙋🏻‍♂️ 이 문서와 참고자료를 보고 학습할 키워드

- Execution Context (실행 컨텍스트)
- Scope
- 호이스팅(hoisting)
- var vs let, const

# 1. Execution Context (실행 컨텍스트)

**Execution Context(실행 컨텍스트)** 는 실행할 코드에 제공할 환경 정보들을 모아놓은 객체입니다. 자바스크립트는 어떤 실행 컨텍스트가 활성화되는 시점에 선언된 변수를 위로 **끌어올리고(hoisting)**, 외부 환경 정보를 구성하고, this 값을 설정하는 등의 동작을 수행합니다. 이런 실행컨텍스트는 자동으로 생성되는 전역 공간과 악마(?)로 취급받는 eval을 제외하면 함수를 실행할 때 생성됩니다.

# 2. Scope

스코프란 현재 접근할 수 있는 변수들의 범위를 의미합니다. 즉 현재 위치에서 볼 수 있는 변수들의 범위를 의미하는데요. 어떤 변수가 스코프 안에 선언되었으면 해당 스코프 안에서는 변수에 접근해서 읽거나 쓸 수 있고, 스코프 밖에서는 해당 변수에 접근할 수 없습니다. ES5까지의 자바스크립트는 특이하게 전역 공간을 제외하면 오직 함수에 의해서만 스코프가 생성되었습니다. 하지만 ES6에서부터는 블록에 의해서도 스코프 경계가 발생하게 함으로써 구분이 명확해졌습니다.  
이러한 **'식별자의 유효범위'** 를 안에서부터 바깥으로 차례로 검색해 나가는 것을 Scope chain이라고 합니다.

## 2-1) Scope Chain

**Scope Chain** 을 따라 스코프를 형성하면서 현재 호출된 함수가 선언될 당시의 **Lexical Environment** 를 참조합니다. 바로 이 **'선언할 당시'** 가 중요한 포인트인데요. 선언하다라는 행위가 실제로 일어날 수 있는 시점이란 콜 스택 상에서 어떤 실행 컨텍스트가 활성화된 상태일뿐입니다. 어떤 함수를 선언(정의)하는 행위 자체도 하나의 코드에 지나지 않으며, 모든 코드는 실행 컨텍스트가 활성화 상태일 때 실행되기 때문입니다.

# 📘 정리

- 실행 컨텍스트는 실행할 코드에 제공할 환경 정보들을 모아놓은 객체이다.

# 🔗 참고 자료

- [MDN 스코프](https://developer.mozilla.org/ko/docs/Glossary/%EC%8A%A4%EC%BD%94%ED%94%84)
<iframe width="752" height="423" src="https://www.youtube.com/embed/EWfujNzSUmw" title="[10분 테코톡] 💙 하루의 실행 컨텍스트" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe><iframe width="752" height="423" src="https://www.youtube.com/embed/PVYjfrgZhtU" title="[10분 테코톡] 🍧 엘라의 Scope &amp; Closure" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
