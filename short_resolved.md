## 희소배열 멀리하기

자바스크립트 배열은 배열 흉내를 내는 객체이다. 그리고 희소 배열(sparse array)이다.
그리고 그 반대가 밀집 배열(dense array)이다.

우리가 보통 말하는 배열은 밀집 배열을 의미한다. 그리고 밀집 배열은 두 가지 특징을 가진다.

1. 하나의 데이터 타입으로 통일되어 있다.
2. 인접한 메모리 공간을 차지한다.

하지만 희소 배열은 아니다.

알고리즘 문제를 풀 때 아래와 같은 패턴이 자주 나와서 실제 개발할 때도 사용을 해봤는데 생각해보니 사용하면 안되는 것 같다.

```typescript
const arr: Item[] = [];

// ...

arr[targetIndex] = arr[targetIndex] || { id, stocks };
```

배열의 기본적인 개념과 맞지도 않을 뿐더러, 있지도 않은 인덱스에 접근하는 행위 자체가 런타임 에러의 발생 가능성을 높이는 것 같다.

## `findIndex` 메서드는 타입적으로 안전하지 않은 것 같다.

아래 코드는 런타임 에러가 발생하지만, 컴파일 타임에 에러를 알려주지 않는다.

```typescript
const arr: { id: number; items: string[] }[] = [];
const targetIndex = arr.findIndex(({ id }) => id === targetId);
const targetItems = arr[targetIndex].items;
```

다만 `find` 메서드는 찾지 못하는 경우 `undefined` 타입이 되기 때문에 비교적 이러한 위험으로부터 안전하다.

## [NAMING] 변수명을 지을 때 prefix로 `prior` vs `previous`

[Prior vs Previous: Definition, Uses, Examples | Proofreading](https://www.proofreading.co.uk/blog/prior-vs-previous-definition-uses-examples/)에 의하면, previous는 순서상 단순 이전을 나타내고 prior은 현재와 관련이 있는 이전의 일을 의미한다.

예를들면, `그녀가 이전에 매니저로 근무했다`는 `previous`가 적합하다.
반면에 `그녀가 이전에 매니저로 근무하면서 이 직무에 필요한 기술들을 습득했다`는 `prior`가 적합하다.

변수명을 지을 때 대입해보면, 캐러셀 혹은 페이지네이션과 같이 배열 기반 UI에서 이전 컨텐츠를 보기 위한 버튼 명은 `previous`가 적합하다.
만약 어떤 상태를 바꿔야하는데, 이전 상태에 기반하여 현재 상태를 업데이트 해야 한다면 `prior`가 적합하다.

## [JAVASCRIPT] `Nullish Coalescing Operator(??)`로 코드 단축하기

종종 다음과 같은 패턴을 사용할 때가 존재한다.

```javascript
array[id] = array[id] || initialValue;
```

배열의 특정 인덱스에 값이 존재하면 해당 값을 사용하고, 값이 존재하지 않으면 초기화 값을 사용하는 패턴이다.

위 패턴은 `array[id]`가 빈 문자열(`''`)과 같이 `falsy`한 값이 존재해도 initialValue가 할당된다는 문제점이 있다.

이를 `??` 연산자를 이용하여 다음과 같이 단축이 가능하다.

```javascript
array[id] ??= initialValue;
```

## [NAMING] ~의 개수 네이밍시 `count` vs `number`

크게 count를 이용하는 방법과 number를 이용하는 방법이 있는데, number의 경우 [중의적인 의미(`index` | `count`)](https://stackoverflow.com/questions/6358588/how-to-name-a-variable-numitems-or-itemcount)가 담길 수 있으므로 가급적 count를 사용한다.

## [JAVASCRIPT] if 문의 범위 잡기

if 문의 범위를 너무 크게 잡으면, 가독성은 좋을 수 있으나 반복되는 코드가 많아질 수 있고, if 문의 범위를 너무 작게 잡으면, 반복되는 코드는 적어지나 가독성은 나빠질 수 있다.

```javascript
if (isPepperoniPizza) {
  prepareDough();
  prepareSauce();
  preparePepperoniTopping();
  assembleAndBake();
}

if (isHawaiianPizza) {
  prepareDough();
  prepareSauce();
  prepareHawaiianTopping();
  assembleAndBake();
}

prepareDough();
prepareSauce();
isPepperoniPizza ? preparePepperoniTopping() : prepareHawaiianTopping();
assembleAndBake();
```

## [DEBUGGING]

에러는 크게 두 가지로 나뉜다.

(1) 원인을 알 수 있는 에러
(2) 원인을 모르겠는 에러

(2)의 경우, `try`문이 상당히 넓은 영역을 커버하는 상황에서 에러가 발생했을 때, 그리고 catch에서 로깅하는 에러 메세지를 이해하지 못하겠을 때, 혹은 `try ~ catch`와는 별개인 런타임 에러가 발생했을 때이다.

이럴 때 디버거를 쓰면 종단점을 빠르게 찾을 수 있다.
