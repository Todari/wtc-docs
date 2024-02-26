## Motivation

- 기능명세서를 최대한 자세히 작성한 뒤 수행하는 역할별로 묶어 domain 분리를 하고자 하였습니다.
- 함수명 및 변수명과 코드를 가독성이 좋게 하려고 하였습니다.
- 도메인 테스트에서 최대한 모든 경우의 unit test를 진행하려고 하였습니다.
## To Reviewers

### 1. 간단한 모듈에서의 constructor + getter 사용 vs return을 갖는 method public 사용
   
   간단한 생성과 리턴만이 필요한 모듈에서, 내부 필드를 만들어 constructor + getter를 사용하여 값을 받아오는 방법과, return값을 갖는 public method를 사용하여 값을 받아오는 방법 중, 불필요한 필드 최소화와 테스트 용이성을 근거로 후자를 적용했습니다.
   
   물론 상황따라 다르고, 사람마다 다르겠지만 리뷰어님께서는 어떻게 생각하시는지 의견이 궁금합니다!
```javascript
class LottoBuyer {
  #budget; 
  #lottoNumber;

  constructor(buyLottoPrice) {
    this.#budget = buyLottoPrice;
    this.#purchase;
  }

  #purchase() {
    const lottoCount = this.#budget / LottoBuyer.LOTTO_PRICE_PER_UNIT;
    this.#lottonumber = Array.from({ length: lottoCount }, () => Lotto.from().createNumber());
  }

  getLottoNumber() {
    return this.#lottoNumber
  }
}

//const lotto = new Lotto();
//console.log(lotto.getLottoNumber());
```
   
```javascript
class LottoBuyer {
  #budget;

  constructor(buyLottoPrice) {
    this.#budget = buyLottoPrice;
  }

  purchase() {
    const lottoCount = this.#budget / LottoBuyer.LOTTO_PRICE_PER_UNIT;
    return Array.from({ length: lottoCount }, () => Lotto.from().createNumber());
  }
}

//const lottoNumber = new Lotto().purchase();
//console.log(lottoNumber);
```
   
### 2. 테스트 코드에서의 명세 포맷팅
페어와 테스트 코드 포맷팅 중 명세의 가독성에 관해 의견이 엇갈려 토의 후 테스트 코드에서의 설명글에 조건값(ex: 로또 숫자 범위는 1~45)은 하드코딩을, 입력값(ex: 로또 숫자가 46인 case)은 포맷팅을 하기로 컨벤션을 정했습니다.

```javascript
//example
CONDITION_RANGE = {min : 1, max : 45};
SUCCESS_CASES = [44, 45];
ERROR_CASES = [46, 47];

describe('정상 작동 테스트', () => {
  test.each(SUCCESS_CASE)('입력값이 45 이하일 때 에러가 발생하지 않는다.', ({ input }) => {
    expect(() => validateRetryCommand(input)).not.toThrow();
  });

  test.each(ERROR_CASE)('입력값이 "$input" 일 때 에러가 발생한다 않는다.', ({ input }) => {
    expect(() => validateRetryCommand(input)).toThrow(new AppError(expectedErrorMessage));
  });
});
```

리뷰어님꼐선 주로 테스트 케이스에서의 포맷팅을 어떤식으로 하시는지 의견이 궁금합니다.

### 3. validation 분기

```plain text
1. 당첨 번호는 구분자(`,`)로 연결된 6개여야 한다.
2. 당첨 번호는 1 ~ 45의 자연수여야 한다.
3. 당첨 번호는 서로 중복되지 않아야 한다.
```
위와 같은 요구사항에서, 더 포괄적인 내용을 먼저 검사하는 방식인,
1. 정규표현식 `/^([1-9]\d?)(,[1-9]\d?)*$/`를 이용하여 확인(구분자로 연결 되었는가?)
2. `split(,).map(Number)` 배열의 요소가 6개인지 확인
3. `split(,).map(Number)` 배열에서 각 요소의 1~45 범위 확인
4. `split(,).map(Number)` 배열에 중복되는 요소 확인

의 순서로 진행했습니다.
하지만 어차피 정규표현식을 사용한다면, 최소한 1,2번은 한번에 검증할 수 있을 것이란 생각을 했고 그에 따라 적용하려다 사용자 입장에서 에러는 세분화 될 수록 길을 잃지 않을거라는 판단 하에 분리를 하였습니다.
현업에서는 기획에 따라 달라질 것 같다는 생각이 들고, 상황 및 사람에 따라서도 다른것은 인지하고 있지만, 리뷰어님의 의견이 궁금합니다.
