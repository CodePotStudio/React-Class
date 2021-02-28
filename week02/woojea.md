# 2주차 Review

### 모던 Javascript

## Arrow Function
> 화살표 함수는 일반 함수와 기능은 같으면서도 코드를 좀 더 간결하게 쓸 수 있도록 도와준다.

- 원래 함수
```jsx
function multiply(x,y){
    return x*y;
}

multiply(1,2) // 2
```

- Arrow Function
```jsx
const multiply = (x,y) => {
  return x*y;
}
```

- 함수 내에서 바로 return 하는 경우에는 축약 가능
```jsx
const multiply = (x,y) => x*y;
```

- 매개변수가 하나일 때는 소괄호도 축약 가능
  
```jsx
// const square = (n) => n*n;
const square = n => n*n;
```

## 객체 구조분해 할당
> 일반적으로 객체 내에 있는 변수 값들을 외부로 꺼내려고 할 때, 가져와야하는 프라퍼티가 많아 질수록 코드의 중복이 많아지는 걸 간결해지도록 도와준다.

```jsx
const fruit = {
    name: "apple",
    color : "red"    
};

console.log(fruit.name, fruit["color"]); // apple red
```
- 주의할 사항으로는 반드시 객체 내에 있는 프라퍼티 명을 사용해야한다.

```jsx
const {name, color} = fruit;
console.log(name, color); // apple red
```


- 객체에서 정의된 이름 바꾸기

```jsx
const {name: fruitName} = fruit;
console.log(fruitName); // apple
```

- 배열 비구조 할당
```jsx
const fruits = ["banana", "kiwi"];

const [first, second] = fruits;
console.log(first, second); // banana kiwi
```
## map - 배열 내장 함수

```jsx
const movies = ["Call me by Your Name", "Dark Knight", "Memento"];

function listofMovie(movie){
    cosnole.log(movie);
}

movies.map(listofMovie); 
// Call me by Your Name
// Dark Knight
// Memento
```
- Arrow Funtion ver.

```jsx
movies.map((movie) => console.log(movie));
```
<br>

## Serverless
> 서버가 없는 백엔드가 아닌 백엔드인데 직접 관리하지 않아도 되는 것
- 예전에는 직접 서버의 하드웨어 부분을 사야했는데 구글,아마존, MS의 서버를 돈주고 빌려 그 큰 회사들이 서버 하드웨어 부분을 책임지고 관리해주는 시대가 도래했다. 하지만 그렇다고 해도 서버의 소프트웨어는 직접 관리해줘야하는 번거로움이 있다.
  
- 서버리스를 활용하면 백엔드를 작은 함수단으로 쪼개 직접 관리하지 않는 서버에 올리는 것이다. 서버리스는 금전적인 면에서도 더 사용한 만큼의 값만 치르기 때문에 효율적이고, 서비스가 증가할 수록 그 때 규모를 확장하면 되므로 합리적이다.
  
- 서버리스의 단점은 cold start 서버가 항상 켜져있는 건 아니므로 함수를 작동시키는데 조금이나마 느릴 수 있다. 두번째 단점은 서버 제공자에 너무 의지하게 된다는 점이다. 한 서버리스 서비스 회사를 이용하다가 다른 회사로 바꾸려고 하면 불편해진다.

- 서버리스는 사이드프로젝트를 하거나 최대한 빠르게 프로토타입을 출시하고 싶은 경우에 좋다. 서버관리 및 설정에 신경을 쓰지 않아도 되기 때문에 코드에만 집중할 수 있게 해준다.
  
