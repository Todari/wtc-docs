# 🧑🏼‍🚀 BOM을 알아야 하는 이유

❗유저에게 경고창을 띄우고 싶은 경우,  
❗유저의 yes or no와 같은 선택에 따라 다른 응답을 보여주고 싶은 경우  
❗유저가 브라우저 창을 닫기 전에 정말 떠날 것인지 확인하고 싶은 경우  
❗유저가 접속한 환경을 알고 싶은 경우  
❗현재 url 위치 및, 접속 history를 알고 싶은 경우

여러 ui를 직접 만들고 자바스크립트로 직접 제어할 수도 있지만, 브라우저에서 제공하는 기본 API를 사용한다면 훨씬 빠르고 간단하게 프로토타이핑을 할 수 있습니다.

# 🙋🏻‍♂️ 이 문서를 보고 나면

✔️`alert`을 이용하며 사용자에게 메세지를 띄울 수 있다.  
✔️`confirm`을 이용하여 사용자가 동작을 결정할 수 있게 설정할 수 있다.  
✔️`prompt`를 이용하여 사용자가 입력한 값을 받아올 수 있다.  
✔️사용자가 페이지를 떠나기 전에 확인하는 경고 메세지를 띄울 수 있다,

# 🖼️ BOM: Browser Object Model

BOM(Browser Object Model)은 웹 브라우저 환경의 다양한 기능을 객체처럼 다루는 모델입니다. 대부분의 브라우저에서 구현은 되어있지만, 정의된 표준이 없어 브라우저 제작사 마다 세부사항이 다르고 다소 한정적이라는 특징이 있습니다. BOM의 역할은 웹 브라우저의 버튼, URL 주소 입력 창, 타이틀 바 등 웹브라우저 윈도우 및 웹페이지의 일부분을 제어할수 있게끔 하는 것입니다. window 객체를 통해 접근이 가능합니다. 아래는 대표적인 BOM 객체들입니다.

- **1) window**: Global Context. 브라우저 창 객체
- **2) screen**: 사용자 환경의 디스플레이 정보 객체
- **3) location**: 현재 페이지의 url을 다루는 객체
- **4) navigator**: 웹브라우저 및 브라우저 환경 정보 객체
- **5) history**: 현재의 브라우저가 접근했던 URL history

![Tip](https://img.shields.io/static/v1.svg?label=&message=Tip&style=flat-square&color=673ab8)  
`beforeunload`이벤트를 사용하면 페이지를 벗어날 때 확인 메세지를 표시할 수 있습니다. 단, 크롬에서는 경고창에 문구가 나타나진 않습니다.

```javascript
window.onbeforeunload = function() {
    return '작성 중인 메시지가 있습니다.'
}

```

![](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/2020-04-21T15:31:35.512%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-04-21%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.31.25.png)

# 📘 정리

- BOM은 웹 브라우저의 기능들을 객체처럼 다루는 모델이다.
- 정의된 표준이 없어 브라우저 제작사마다 구현이 다르다.
- BOM에서 제공하는 API를 적극 활용하면, 사용자 경험을 향상시킬 수 있다.

# 🔗 참고 링크

- [window객체와 BOM](https://www.zerocho.com/category/JavaScript/post/573b321aa54b5e8427432946)