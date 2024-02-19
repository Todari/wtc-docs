
# 🤔 들어가기 전에 생각해보기

프리코스에서 테스트 코드와 함께 개발해 본 경험이 어떠했는지 생각해 보자.

- 개발하는 데에 어떻게 도움이 되었을까?
    - 도움이 되었다면 어떤 부분에서 되었는가?
    - 오히려 방해가 되었다면 어떤 이유에서 방해가 되었을까?
- 테스트 코드는 정말 필요할까?

# '테스트'?

> "Software testing is an investigation  
> to provide information about the quality of the software product or service"  
> -Wikipedia

- 제품의 품질(quality)을 확인하고 보장하기 위한 작업
- 이걸 코드를 써서 하면 테스트 '코드' → '자동화된 테스트'

테스트 '코드'를 쓰지 않았을 뿐, 기본적으로 프로그램을 구현했다면 '테스트'는 할 수밖에 없다.

- 처음 구현할 때에는 **요구사항대로 잘 구현되었는지 확인**하기 위해서
- 유지보수를 하면서는 **계속 변하는 요구사항에 대응하면서, 동시에 안정적인 품질을 유지**하기 위해서

# 단위 테스트?

![테스트의 종류](https://miro.medium.com/max/1400/1*Tcj3OsK8Kou7tCMQgeeCuw.png)  
(출처: https://betterprogramming.pub/the-test-pyramid-80d77535573)

### 테스트 대상 범위

![image.png](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/a5b359c687dd4ee89aae2ec4c193a824)

# 테스트 코드가 필요하지 않은 경우는?

- 테스트 코드는 항상 필요한가?
- 테스트 코드를 쓰지 않는 게 오히려 나은 경우는 없을까?

# 기본 용어

## production code vs test code

### production code

'실제 코드'. 즉, 테스트 대상이 되는 코드

### test code

- 실제 코드와 별도 파일에 둔다.
    - 일반적으로 테스트 대상 코드가 `Car.js`라면, 이에 대한 테스트 코드는 `Car.test.js` 로 명명
    - 컨벤션에 따라 실제 코드와 같은 디렉터리에 나란히 두기도 하고, 혹은 `__tests__`와 같은 별도 디렉터리에 따로 모아두기도 한다.

## 테스트 케이스(test case)

- 하나의 테스트 케이스는 일반적으로 세 개의 섹션으로 구성된다.
    - 준비: 테스트할 동작을 호출하기 위해 필요한 사전 준비 작업
    - 실행: 테스트 대상 동작 호출
    - 단언: 호출 결과가 기대한 결과와 동일한 지 확인
- 각 단계를 아래와 같은 용어로 부르기도 한다. (테스트 철학에 따라 뉘앙스는 다르지만 의미하는 바는 동일하다)
    - arrange/act/assertion
    - given/when/then

```javascript
test("랜덤값이 4이상이면 1칸 전진", () => {
  // given
  const car = new Car("우택");

  // when
  car.move(4);

  // then 
  expect(car.position).toBe(1);
});

```


## [setup & teardown](https://jestjs.io/docs/setup-teardown)

- beforeAll
- beforeEach
- afterEach
- afterAll
- describe

## [Jest Matchers](https://jestjs.io/docs/using-matchers)

- Jest는 단언에서 활용할 수 있는 다양한 matcher를 제공한다. 용도에 맞는 matcher가 무엇인지 고민해보고, 적절한 matcher를 선택해서 사용하자.
    - 적절한 matcher는 테스트 단언문을 더 이해하기 쉽게 만들어준다.

# 무엇을 테스트할까?

- 정상 케이스
- 예외 케이스

# 🔗 참고 자료

- [다양한 유형의 소프트웨어 테스트](https://www.atlassian.com/ko/continuous-delivery/software-testing/types-of-software-testing)

## 추천 플러그인

VSCode 를 쓰고 있다면, 테스트 작성과 실행을 조금 더 편리하게 해주는 각종 플러그인을 활용해볼 수 있습니다.  
본인에게 편리한 설정이나 플러그인들을 설치해서 활용해 보세요 :)

- [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
- [Jest Snippets](https://marketplace.visualstudio.com/items?itemName=andys8.jest-snippets)
- 혹은 각 플러그인마다 제공해주는 Command (Ctrl/Cmd + P) 를 활용해보실 수도 있습니다.