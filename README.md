# Movie App 2019

React JS fundamentals Course (2019 Update)

## features

## lecture contents

### 2.0 Creating your first React component

* component ; HTML을 반환하는 함수

    - js와 HTML file의 조함 : jsx
    - src/index.js에서 react application은 하나의 component만을 rendering 해야 한다.

    --> 따라서 다른 component 들을 이용하는 경우 ?
    src/App.js안에 다른 component 들을 넣어서 사용하는 방법을 이용할 수 있다.

ex. src/Potato.js 생성하여 이용하는 경우

1. Potato.js file 생성
* React에서 html~js 위해서 import React from "react"는 필수이다.

* 다른 곳에서 이용하기 위해 export default Potato; 정의한듯 하다.

```
import React from "react";

function Potato() {
    return <h3>I love potato</h3>;
}

export default Potato;
```

2. App.js에서 import 한후, 아래와 같은 형식으로 이용 가능
```
import React from 'react';
import Potato from "./Potato"

function App() {
  return (
    <div>
      <h1>Hello!!</h1>
      <Potato />
      </div>
  );
}

export default App;

//<Potato />와 같은 방식으로 이용 가능

```

<br>
<br>


### 2.1 Reusable Components with JSX + Props

* component-component, children component로 정보 보내는 방법

1. Food component에 kimchi라는 value로 prop name을 줌
```
<Food fav="kimchi" />
<Food fav="ramen" />
<Food fav="samgiopsal" />
<Food fav="chukumi" />
```

2. Food component는 fav를 통해 받은 prop으로 함수 사용가능

```
(ex.1)
function Food({ fav }) {
  return <h1>I like {fav}</h1>
}

(ex.2)
function Food(props) {
  return <h1>I like {props.fav}</h1>
}

```

--> 재사용이 가능하다. 따라서 김치, 라면, 삼겹살, 쭈꾸미를 fav로 보내면 각각 Food라는 함수를 사용하여 그에 맞는 문구가 출력된다.


<br>
<br>

### 2.2 Dynamic Component Generation


* 동적 데이터를 추가하는 방법 (ex. array , API에서 가져오는 경우) --> map 사용

<br>

* map ?
array의 각 item에서 function을 실행하는 array를 가지는 JavaScript function이고 그 function의 result를 갖는 array를 준다.

(ex) foodILike이라는 배열의 요소들을 Food component에 넣고 싶은 경우

```
function App() {
  return (
    <div>
      {foodILike.map(dish => <Food name ={dish.name} picture ={dish.image}/>)}
      </div>
  );
}



function Food({ name, picture }) {
  return <div>
    <h2>I like {name}</h2>
    <img src={picture} />
  </div>
}
```


<br>
<br>


### 2.3 map Recap

* map : 각각 object 별로 함수 호출함


props key가 달라야 하는 경우가 종종 발생한다. 
따라서, 배열에 id값을 각각 요소별로 다르게 저장해주고, Food component를 호출할 때 key 값을 주는 것을 생성해준다.

```
function App() {
  return (
    <div>
      {foodILike.map(dish => (
        <Food key={dish.id} name={dish.name} picture={dish.image} />
        ))}
      </div>
  );
}
```

<br>
<br>


### 2.4 Protection with PropTypes


<br>
<br>