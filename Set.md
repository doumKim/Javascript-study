# Set

ES6 이전에는 키와 값을 연결하려면 객체를 이용했다. 하지만 단순 객체를 사용한다면 아래의 단점이 발생한다.

>

1. 프로토타입 체인으로 의도하지 않은 연결이 발생.
2. 객체 안에 프로퍼티의 수를 쉽게 알아내기 힘들다.
3. 객체는 프로퍼티 순서를 보장하지 않는다.
4. 키는 반드시 문자열 또는 심볼만 사용해야한다.

이러한 문제점들을 해결하기 위해 이전에 설명한 Map과 이번에 설명할 Set을 사용하면 된다.

## Set 객체의 특징

> Set객체는 중복을 허용하지 않는 값을 모아놓은 즉 유일한 데이터를 수집하여 활용하기 위한 객체이다.
> Set객체는 데이터 값의 단순 집합으로 간주한다.
> Set 객체는 외부에서 키를 사용하여 데이터 값을 추가, 삭제, 검색 할 수 있다.
> 값의 데이터 타입에 제한이 없다.

### Set 객체의 생성

**new Set(iterable)**
이터러블 객체(일반적으로 배열)를 전달받으면 그 안의 값을 복사해 셋에 넣어준다.

```js
const set = new Set();
console.log(set); // Set {}

const set2 = new Set(['Kim', 'Lee']);

//제너레이터 함수를 이용
function* makeUser() {
	yield 'Kim';
	yield 'Lee';
}

const users = makeUser();
const usersSet = new Set(users);
console.log(UserSet); // Set {"Kim","Lee"}
```

### 데이터 추가, 삭제, 확인

add, delete, has 메소드를 통해 데이터의 추가, 삭제, 확인을 할 수 있다.

```js
const users = new Set(['Kim', 'Lee']);
users.add('Choi');
console.log(users); //Set {"Kim","Lee","Choi"}

users.delete('Choi');
console.log(users); //Set {"Kim","Lee"}

console.log(users.has('Choi')); // false
```

### 전체 데이터 값의 열거, 함수 처리

```js
const users = new Set(['Kim', 'Lee']);
const iterKeys = users.keys();
for (let v of iterKeys) console.log(v); //Kim  Lee

const iterEntries = users.entries();
for (let v of iterEntries) console.log(v); // ['Kim','Kim']   ['Lee','Lee']

for (let v of users) console.log(v); //Kim  Lee

users.forEach((user1, user2) => {
	console.log(`${user1} => ${user2}`); // Kim => Kim   Lee => Lee
});
```
