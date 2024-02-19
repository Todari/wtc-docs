### [슬기로운 우테코 생활](https://techcourse.woowahan.com/s/sSPHidEx/ls/kyB58rOF)

### [좋은 코드](https://techcourse.woowahan.com/s/sSPHidEx/ls/r1Mqwu3b)

### [단위테스트](https://techcourse.woowahan.com/s/sSPHidEx/ls/n2GEdWZu)

---
- [Jest 공식 문서](https://jestjs.io/docs/api)를 참고하여 method 확인
- 테스트코드 <-> 프로덕션 코드(기능 구현이 된 코드)
- AAA (Arrange, Act, Assert) 검증

```javascript
describe(("게산기 기능 검증", () => {

  test("두 수를 받아서 덧셈을 한다", () => {
    // Arrange
    const calculator = new Calculator();
	const a = 1;
	const b = 2;
	const c = 3;
	
    // Act
    const result = caculator.add(a, b);
    
    // Assert
    expect(result).toBe(c);
  };

  test.only("두 수를 받아서 뺄셈을 한다", () => {
    // Arrange
    const calculator = new Calculator();
	const a = 3;
	const b = 2;
	const c = 1;
	
    // Act
    const result = caculator.sub(a, b);
    
    // Assert
    expect(result).toBe(c);
  };

  test.skip("두 수를 받아서 곱셈을 한다", () => {
    // Arrange
    const calculator = new Calculator();
	const a = 3;
	const b = 2;
	const c = 6;
	
    // Act
    const result = caculator.mul(a, b);
    
    // Assert
    expect(result).toBe(c);
  };

  test("두 수를 받아서 나눗셈을 한다", () => {
    // Arrange
    const calculator = new Calculator();
	const a = 10;
	const b = 2;
	const c = 5;
	
    // Act
    const result = caculator.div(a, b);
    
    // Assert
    expect(result).toBe(c);
  };

  test("0으로 나누면 예외를 발생시킨다.", () => {
    // Arrange
    const calculator = new Calculator();
	const a = 10;
	const b = 0;
    
    // Assert
    expect(() => {
      //Act
      calculator.div(a,b);
      
    }).toThrow()
  };
})
```

- 예외값을 넣어서 테스트 검증을 하는것도 필요
- test.only, test.skip을 이용하여 describe 내에서 테스트 통제 가능
- test.skip과 xtest, xdescribe 모두 사용 가능하지만, x를 붙이는 것은 명시성이 좋지 않음
- 프로덕션코드와 테스트코드를 한번에 리팩토링 하는 것은 좋지 않음
- 프로덕션 코드를 먼저 리팩토링 한 후 테스트코드가 제대로 작동하는지 확인 후 테스트코드 리팩토링