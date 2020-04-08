# Map

ES6 이전에는 키와 값을 연결하려면 객체를 이용했다. 하지만 단순 객체를 사용한다면 아래의 단점이 발생한다.

>

1. 프로토타입 체인으로 의도하지 않은 연결이 발생.
2. 객체 안에 프로퍼티의 수를 쉽게 알아내기 힘들다.
3. 객체는 프로퍼티 순서를 보장하지 않는다.
4. 키는 반드시 문자열 또는 심볼만 사용해야한다.

이러한 문제점들을 해결하기 위해 Map 객체를 사용하면 된다.

## Map 객체의 특징

> Map객체는 데이터를 수집하여 활용하기 위한 객체이다.
> 값의 고유한 식별 정보인 키와 값의 쌍을 Map 객체 안에 저장해서 사용한다.
> 외부에서 키를 사용하여 원하는 값을 추가, 삭제, 검색할 수 있다.
> 키와 값을 데이터 타입에는 제한이없다.

### 일반 객체와 Map 객체의 차이

- Map 객체에는 데이터를 수집하기 위한 다양한 메서드가 있다.
- 일반 객체는 키로 문자열만 사용할 수 있는 반면 Map 객체는 제한이 없다.
- Map 객체는 내부적으로 해시 테이블을 활용하기 때문에 데이터 검색 속도가 빠르다.
- Map 객체는 이터러블하며 for-of 문으로 순회하면 키와 값으로 구성된 배열을 반환한다.
- Map 객체는 데이터 개수를 size 프로퍼티로 구할 수 있다.

### Map 객체의 생성

Map 생성자 함수를 이용해 Map 객체를 생성한다. 인수를 생략하면 빈 Map 객체가 생성된다.

```js
const map = new Map();
console.log(map); // Map {}
```

초기 데이터를 인수로 지정해서 생성할 수 있다. 여기서 초기 데이터는 요소를 두 개 이상 포함한 배열
[key, value]을 값으로 가지는 이터러블한 객체이다.

```js
const userId = new Map([
	['doum', 'asdf123'],
	['gildong', 'qwer321'],
]);
console.log(userId); // Map(2) {"doum" => "asdf123", "gildong" => "qwer321"}
```

이번에는 제너레이터를 사용해 이터레이터를 생성하는 방식으로 위와 같은 작업을 해보겠다.

```js
function* makeUserId() {
	yield ['doum', 'asdf123'];
	yield ['gildong', 'qwer321'];
}

const userIds = makeUserId();
const userId = new Map(userIds);
console.log(userId); // Map(2) {"doum" => "asdf123", "gildong" => "qwer321"}
```

### 데이터 개수 구하기

size 프로퍼티를 이용해 데이터의 개수를 구할 수 있다.

```js
console.log(userId.size); // 2
```

### 데이터 추가하기, 읽기, 확인, 삭제

> - **set(key,value)** 메소드를 사용해서 데이터를 추가할 수 있다.

- **get(key)** 메소드를 사용해 데이터를 읽을 수 있다.
- **has(key)** 메소드를 사용해 데이터가 있는지 확인 가능하다.
- **delete(key)** 메소드를 사용해 데이터를 삭제할 수 있다.
- **clear()** 메소드를 사용하면 모든 데이터를 삭제할 수 있다.

```js
userId.set('Jane', 'jane123');
console.log(userId); // Map(3) {"doum" => "asdf123", "gildong" => "qwer321", "Jane" => "jane123"}

console.log(userId.get('Jane')); // 'jane123'

console.log(userId.has('Jane')); //true

userId.delete('Jane');
console.log(userId); // Map(2) {"doum" => "asdf123", "gildong" => "qwer321"}

userId.clear();
```

### 모든 키, 값, 데이터의 열거

>

- 키를 열거하고 싶을 때는 keys() 메소드를 사용
- 값을 열거하고 싶을 때는 values() 메소드를 사용
- 데이터를 열거하고 싶을 때는 entries() 메소드를 사용

```js
const iter = userId.entries();
for (let [key, value] of iter) console.log(key, value);
//doum asdf123
// gildong qwer321
```

### 모든 데이터를 함수로 처리하기

> forEach 메소드를 사용해서 콜백함수를 모든 데이터에 적용할 수 있다. 콜백함수의 인수는 다음과 같다.

- value : 현재 처리하는 데이터 값
- key : 현재 처리하는 데이터 키
- map : 처리 중인 Map 객체

```js
userId.forEach((value, key, map) => {
	console.log(`${key} => ${value}`);
});
// doum => asdf123
// gildong => qwer321
```

> #### 참조
>
> 모던 자바스크립트 입문
