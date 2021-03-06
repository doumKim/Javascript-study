# 이터레이터와 배열

```js
const array = [1, 2, 3, 4];

const iterator = (() => {
	let num = 1;

	return {
		next: () => {
			return num > 4 ? { done: true } : { done: false, value: num++ };
		},
	};
})();
/*
console.log(array); //[1, 2, 3, 4]
console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
console.log(iterator.next().value); // 4
*/
```

## 이터레이터와 배열의 차이

이터레이터의 경우 생성하면 기본적으로 next 함수 하나만 있다고 생각하면 된다.
next 함수에서는 done과 value 두 항목을 담은 객체를 반환한다.
done은 이터레이터가 끝이 났는지 아직 남은게 있는지를 의미한다.
value는 이터레이터가 아직 순회 중일 때 값을 반환한다.
next 함수 하나만을 지원하기 때문에 이전에 얻어온 value, 다음 value만을 가져올 수 있다.

반대로 배열의 경우 랜덤 액세스가 가능하다.( 인덱스를 이용해 값을 불러올 수 있다.)
배열의 요소의 개수도 바로 알 수 있다.
이터레이터는 배열의 부분집합이다. 배열은 이터레이터의 기능을 포함하기 때문에 이터레이터로 변환을 할 수 있다.
반대로 이터레이터가 배열로 변환을 하려면 계산하지 않고 두던 모든 값을 계산을 해야한다는 점에서 조금 다르다.

### 이터레이터를 사용하는 이유

1. More functionality does not mean "better".
2. Iterator can save memory uses.

일반적인 경우에는 배열이 이터레이터보다 무거울 수 밖에 없다.
그런데 이터레이터를 사용해도 되는 상황에서 배열을 사용한다면? 성능 상으로 좋지 못한 선택이다.
또한 코드 가독성도 떨어지는 단점이 발생한다. 그리고 가장 중요한 배열은 하지 못하나 이터레이터만이 할 수 있는 작업이 있다.
일반적으로 배열을 이용하려면 배열의 모든 요소들을 모두 메모리에 넣어야한다. 일정한 규칙이 존재하는 수열과 같은 데이터를 다루기 위해서는
당연하게도 이터레이터를 활용하는게 더 좋은 선택이 될것이다. 또한 외부데이터를 다루기 위한 수단으로도 많이 사용된다.
예를들어 이미지 분석을 위해 특정 디렉토리에 있는 이미지들을 불러와 미리 작성해둔 코드를 돌려가며 처리하는 작업이 있다고 하면
먼저 배열을 사용해서 한다고 생각하면 모든 이미지들을 다 불러와서 배열에 미리 불러다 놓아야한다. 하지만 이터레이터를 사용한다면
딱 현재 다루고 있는 이미지 하나만을 메모리에 올리면 된다. 개발자 입장에서는 배열이나 이터레이터나 상관없이 루프를 돌리는 작업으로 보이지만
시스템적으로는 엄청난 차이가 있다는 것이다.

> ### 정리
>
> 1.  제공하는 기능 기준으로 이터레이터는 배열의 부분집합이다.
>
> 2.  이터레이터를 이용하면 값을 모두 계산에서 보관할 필요가 없이 다음 값 호출을 받았을 때, 그때 필요한 값만 계산하는게 가능해진다.
>
> 3.  함수형 프로그래밍을 위한 map, reduce와 같은 메소드들은 이터레이터만 있어도 구현을 할 수 있다.
