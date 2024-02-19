# 🧑🏼‍🚀 Prototype을 알아야 하는 이유

❗프로토타입에 대해서 개념서에서만 보고, 실제로는 어떤 원리인지 잘 모르겠다면

# 🙋🏻‍♂️ 이 문서를 보고 나면

- 프로토타입의 구조를 이해하고, 객체를 설계 할 수 있다.

# 프로토타입

자바스크립트는 프로토타입기반 언어입니다. 클래스 기반 언어에서는 '상속'을 사용하지만 프로토타입 기반 언어에서는 어떤 객체를 원형으로 삼고 이를 복제(참조)함으로써 상속과 비슷한 효과를 얻습니다. 프로토타입을 이해하기 위해서는 크게 3가지 `constructor`, `prototype`, `instance`를 기억해주시면 됩니다.

```javascript
const instacne = new Constructor(); 
```

이는 아래의 도식으로 이해할 수 있습니다.  

![](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/f6db4967415c4636be6c5cd0e57ebb8f)

위 그림대로 new 연산자로 constructor를 호출하면 instance가 만들어지고, 이 instance가 가지고 있는 생략 가능한 프로퍼티인 `__proto__`는 constructor의 prototype을 참조합니다.

자바스크립트는 함수에 자동으로 객체인 prototype 프로퍼티를 생성해 놓습니다. 그래서 해당 함수를 생성자 함수로써 사용할 경우, 즉 new 연산자와 함께 함수를 호출할 경우, 그로부터 생성된 인스턴스에는 숨겨진 프로퍼티인 `__proto__`가 자동으로 생성됩니다. 그리고 이 프로퍼티는 생성자 함수의 prototype을 참조합니다. `__proto__` 프로퍼티는 생략 할 수 있도록 구현돼 있기 때문에 생성자 함수의 prototype에 어떤 메서드나 프로퍼티가 있다면 인스턴스에서도 마치 자신의 것처럼 해당 메서드나 프로퍼티에 접근할 수 있게 됩니다.

# Mixin

자바스크립트 객체는 상속받거나 인스턴스화해도 자동으로 복사작업이 일어나지 않습니다. 자바스크립트엔 인스턴스로 만들 개념 자체가 없고 오직 객체만 있기 때문인데요. 객체는 다른 객체에 복사되는게 아니라 서로 연결됩니다. Mixin은 다른 언어와 달리 자바스크립트에선 없는 클래스 복사 기능을 흉내 낸 것으로 Wikipedia에서는 [믹스인(mixin)](https://en.wikipedia.org/wiki/Mixin)을 **다른 객체를 상속받을 필요 없이 구현되어있는 메서드를 담고 있는 객체**라고 정의합니다. 즉 믹스인은 특정 행동을 실행해주는 메서드를 제공하는데 단독으로 쓰이지 않고, 다른 객체에 행동을 더해주는 용도로 사용됩니다.

다음은 버튼 동작을 정의하는 믹스인 오브젝트입니다.

```javascript
const clickableMethods = {
  hover() {
    console.log('hovering')
  },
  press() {
    console.log('button pressed')
  },
  click() {
    console.log('button clicked')
  },
}

```

상속이 아닌 믹스인만을 이용해서 위의 클릭과 관련한 함수 기능을 그대로 활용하고자 한다면 다음과 같이 사용할 수 있습니다.

```javascript
function Button(size, color) {
  this.size = size
  this.color = color
}

Object.assign(Button.prototype, clickableMethods)

new Button(20, 'primary').hover() // hovering
```

# 📘 정리

- 어떤 생성자 함수를 new 연산자와 함께 호출하면 Constructor에 정의된 내용을 바탕으로 새로운 인스턴스가 생성됩니다. 이 인스턴스에는 `__proto__`라는, Constructor의 prototype 프로퍼티를 참조하는 프로퍼티가 자동으로 부여됩니다.
- `__proto__`는 생략 가능한 속성이라, 인스턴스는 Constructor.prototype의 메서드를 마치 자신의 메서드인 것처럼 호출할 수 있습니다.
- 프로토타입을 도식화한 삼각형의 대각선 방향인 `__proto__` 방향을 계속 찾아가면 최종적으로는 Object.prototype에 도달합니다. 이런 식으로 `__proto__` 안에 다시 `__proto__`를 찾아가는 과정을 프로토타입 체이닝이라고 합니다. 이 체이닝을 통해 각 프로토타입 메서드를 자신의 것처럼 호출할 수 있습니다. 이때 접근 방식은 자신으로부터 가장 가까운 대상부터 찾아 나가며, 원하는 값을 찾으면 검색을 중단합니다.
- 믹스인 은 객체 지향 언어에서 범용적으로 쓰이는 용어로, 다른 클래스들의 메서드 조합을 포함하는 클래스를 의미합니다.
- 몇몇 언어는 다중상속을 허용합니다. 자바스크립트는 다중상속을 지원하지 않는데, 믹스인을 사용하면 메서드를 복사해 프로토타입에 구현할 수 있습니다.

# 🔗 참고 자료

- [MDN Object-oriented_JS](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object-oriented_JS)
- [MDN_상속과 프로토타입](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Inheritance_and_the_prototype_chain)
- [MDN_Mixin](https://developer.mozilla.org/en-US/docs/Glossary/Mixin)
<iframe width="752" height="423" src="https://www.youtube.com/embed/RYxgNZW3wl0" title="[10분 테코톡] 💼 크리스의 Prototype" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe><iframe width="752" height="423" src="https://www.youtube.com/embed/TqFwNFTa3c4" title="[10분 테코톡] 아놀드의 프로토타입 뽀개기" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe><iframe width="752" height="423" src="https://www.youtube.com/embed/HujbNZ9IWF8" title="[10분 테코톡] 도리의 Class" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>