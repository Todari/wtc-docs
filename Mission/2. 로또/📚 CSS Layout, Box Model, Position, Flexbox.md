# 🧑🏼‍🚀 Layout을 알아야 하는 이유

❗화면의 구성을 원하는 대로 배치하고 싶다면?  
❗웹페이지에서 가장 많이 사용되는 CSS 지식을 우선적으로 알고 싶다면?

# 🙋🏻‍♂️ 이 문서를 보고 나면

- Box Model, Position, Flexbox에 대해서 이해하고, 레이아웃을 구성해볼 수 있다.

# 레이아웃

css 프로퍼티는 약 500개가 넘을 정도로 굉장히 방대합니다. 그 css 프로퍼티를 처음부터 모두 알려고 하면 끝이 없을 텐데요. 뭐든지 어려울 수록 전략이 필요합니다. 자주 사용하는 css 프로퍼티들이 어떤 것인지 안다면 훨씬 명확해지겠죠?  
[https://chromestatus.com/metrics/css/popularity](https://chromestatus.com/metrics/css/popularity) 이 링크는 크롬에서 제공하는 크롬에서 자주 사용되는 css 프로퍼티 랭킹을 보여주고 있습니다. 가장 상위에 있는 것들은 레이아웃과 관련된 값입니다. 레이아웃은 매우 중요합니다. 이쁘게 꾸며주는건 여러 디자인 라이브러리로 가능하지만, 레이아웃은 직접 작성해야 하는 경우가 많기 때문입니다.

# Box Model

레이아웃을 이루는 2가지 기본 개념은 `크기`와 `위치`입니다.  
이 크기를 정하는데 중요한 개념이 `Box Model`입니다. 모든 HTML의 element는 사각형 박스의 형태를 가집니다. 다음과 같은 속성을 가집니다.

![](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/8ed0282c53d446ac9242e7420b8b282e)

보통 css에서 box model를 다룰 때 고민이 되는 지점은 바로 겹쳐지는 부분입니다.

### 인접한 두 개의 block element가 서로 다른 margin을 가지고 있다면?

> 큰 값을 가진 margin값이 공유되어 사용됩니다(마진 병합)  
> 10px + 20px = 20px

### 인접한 두 개의 inline element의 margin은?

> 각각의 margin 의 합으로 표현된다.  
> 10px + 20px = 30px

### margin, padding의 다양한 축약표기법

```javascript
margin : 0px 0px 0px 10px; (top , right , bottom, left) 
margin : 10px; (네개의 분면이 모두 10px)
margin : 10px 15px; (top, bottom 은 10px , right, left는 15px)
```

실제 레이아웃을 만들 때, 본인이 원하는 대로 동작하지 않는다면, 꼭 MDN을 통해 해당 속성에 대해서 학습해보고 넘어가주세요.

# Position

position은 element를 어떻게 배치할 것인가를 결정합니다. 크게 4가지의 상태가 있습니다.

- static
- absolute
- relative
- fixed

## 1) static

모든 element 의 default 값입니다. 문서의 흐름대로 위치가 결정됩니다.  
![스크린샷 2021-01-27 오전 11.37.34.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/7cf0dea24817476eaadef8d3428c0b4e)

## 2) relative

원래 위치에 상대적인 위치  
![스크린샷 2021-01-27 오전 11.38.35.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/a9d44e1f90104607bb0f3b620b3b5d9b)

relative 속성의 실제 사용은,  
absolute속성을 가진 자식의 기준점으로 더 많이 활용됩니다.

![스크린샷 2021-01-27 오전 11.40.20.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/aae93fbff886460498056b19fbe85d0f)

## 3) absolute

절대적인 위치이며 문서의 흐름에서 제외.  
기준점은 상위element 중 **static 속성이 아닌 element**  
위치설정은 top, bottom 중 한 개와 left, right 중 한개를 선택해서 설정

![스크린샷 2021-01-27 오전 11.38.41.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/40116865d7914d6db4607ea6a617aa42)

## 4) fixed

진정한 절대적인 위치를 차지  
문서의 흐름에서 제외.  
viewport(보이는 화면)를 기준으로 위치값을 가짐

# Flexbox

대부분의 웹페이지의 레이아웃 구성은 위-아래의 수직 구성입니다. 레이아웃을 구성할 때 가장 많이 사용하는 요소들이 기본적으로 블록 형태로 표시되며 이는 위에서 아래로 쌓이기 때문에 수직 구성은 상대적으로 쉽게 만들 수 있습니다.  
하지만 수평구성의 경우는 상황이 조금 다릅니다.  
문제는 수평 구조를 만드는 속성이 명확하지 않았기 때문인데, 그래서 많은 경우

나 float 혹은 inline-block 등의 도움을 받았습니다. 하지만 이러한 방법들은 대부분 수평 레이아웃 구성의 차선책이었습니다. 그래서 많은 엔지니어들의 연구 결과 Flex(Flexible Box)라는 명확한 개념을 이용하여 레이아웃을 쉽게 구성할 수 있습니다.

자동차 경주 게임을 웹 버전으로 아래와 같은 레이아웃으로 구성할 때에도 Flexbox를 사용할 수 있습니다.

![image.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/9fabea754bc44cdeb45d405448143b01)  
Flex는 요소의 크기가 불분명하거나 동적인 경우에도, 각 요소를 정렬할 수 있는 효율적인 방법을 제공합니다.  
가능하면 화면의 ui을 설정할 때 FlexBox로 구성하는 연습을 해보시는 것을 추천합니다.

다음 링크들에서 Flexbox에 대해 좀 더 알아가보세요 :)

- [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)
- [이번에야말로 CSS Flex를 익혀보자](https://studiomeal.com/archives/197)
- [CSS Froggy](https://flexboxfroggy.com/#ko)

# 🔗 참고 링크

- [MDN_Layout](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout)
- [MDN BoxModel](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/%EC%83%81%EC%9E%90_%EB%AA%A8%EB%8D%B8#css_box_model%EC%9D%B4%EB%9E%80_%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
- [MDN_Position](https://developer.mozilla.org/ko/docs/Web/CSS/position)
- [MDN FlexBox](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Flexbox%EC%9D%98_%EA%B8%B0%EB%B3%B8_%EA%B0%9C%EB%85%90)