# Movie App 2019

React JS fundamentals Course (2019 Update)

## features

## lecture contents

### 1 SETUP

[How to use react?]

1. 원하는 폴더에 가서

```
npx create-react-app {이름}
```

으로 파일 생성

2. terminal에서 해당 폴더에 가서

```
npm start 
```

3. refresh가 필요한 경우

```
npm i
```

<br>
<br>


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

* prop-types : 내가 전달받은 Props가 내가 원하는 props인지를 확인하는 것
무조건 이름은 Food.propsType과 같이 정의해야 함 . propsType 이름을 바꿀 수 없음

ex. image 에 잘못된 정보를 보내는 경우 같은거 잡아냄
    * isRequired: 무조건 있어야 하는 경우 추가되는 조건

1. propsType 검사기 설치

터미널에 아래와 같은 명령어 작성

```
npm i prop-types
```

2. 검사 방법 정의 :componenet.propTypes 형식

```
Food.propTypes = {
  name : PropTypes.string.isRequired,
  picture : PropTypes.string.isRequired,
  rating : PropTypes.number
};
```

<br>
<br>


### 3.0 Class Components and State

* class App 정의 : class App은 react component라는 뜻


  * class App 는 function이 아니므로, return을 안하고 render method를 가지고 있다.

  *  react는 자동적으로 모든 class componnet의 render method를 실행하고자 한다.

  * state : 보통 우리가 동적데이터와 함께 작업할 때 만들어진다. 사라지고 생기는 데이터와 같이 바뀌는 데이터를 state안에 넣는다.

  * class component는 state를 가지고 state는 object이다. component의 data를 넣은 공간으로써, data는 변하므로 state를 이용한다.


```
class App extends React.Component{
  state = {
    count : 0
  };

  add = () => {
    console.log("add");
  };
  minus = () => {
    console.log("minus");
  };

  render(){
    return <div>
      <h1>The number is:  {this.state.count}</h1>
      <button onClick = {this.add}>Add</button>
      <button onClick = {this.minus}>Minus</button>
      </div>
  }
}
```

<br>
<br>

### 3.1 All you need to know about State

* state는 직접적으로 변경이 불가능하다. 
ex. this.state= 1 불가능


-> 이유 : react는 render function을 Refresh하지 않는다.
=> 따라서 state의 상태를 변경할때 마다 render를 호출해야 한다. `setState` 이용해야 한다. setState를 통해 react는 virtual DOM을 통해 변경된 부분만 다시 칠한다.

(1) setState 활용 1 : 이쁜방법은 아니다.

```
this.setState({count : this.state.count + 1});
```

(2) setState 활용 2
```
this.setState(current => ({count : current.count + 1})); 
```

<br>


* 매우 중요한 사실

``setState를 호출할때마다 react는 state와 함께 다시 render를 호출한다.``


<br>
<br>

### 3.2 Component Life Cycle

react component에서 사용하는 유일한 function은 render function이다.

* life cycle method : react가 component를 생성하고 없애는 방법이다.

  * component가 생성될 때, 생성되기 전과 생성된 후에 호출되는 다른 function 존재한다. 


```
1. mounting "태어나는 것"
constructor : javascript에서 class 만들 때 호출되는 것 
-> super(props);를 호출해야함
-> screen에 표시될 때 호출됨
  * getDrivedStateFromProps () : 잘 사용 안함
  * render() : 컴포넌트 생성시 호출됨.
  * ComponentDidMount() : Mount 되고 실행되는 듯


2. updating : 상태 변경 (setState할 때마다 render 호출)
  * getDrivedStateFromProps() : 사용안함
  * shouldComponentUpdate() : update할지 말지 결정하는 것인데 여기서 다루지 않음
  * componentDidUpdate() : update된후 실행되는 듯


3. unmounting "component가 죽음" ->page 바꿀 때 등 발생
  * componentWillUnmount() : component가 떠날때 호출됨.

```
<br>
<br>

### 3.3 Planning the Movie Component

* class App extends React.component 에서 componentDidMount() , 즉 mount 된 직후 실행되는 함수에서 6초 뒤에 준비되었다는 문구를 출력하고 싶은 경우

```
componentDidMount() {
    setTimeout(() => {
      this.setState({isLoading : false});
    }, 6000);
  }

  render(){
    const { isLoading } = this.state;

    return <div>
      {isLoading ? "Loading..." : "we are ready"}
      </div>;
  }
```


<br>
<br>


### 4.0 Fetching Movies from API

* axios : fetch위에 있는 작은 layer   npm install axios을 통해 설치한 후, 

```
import axios from "axios";
```
을 통해 import한다. 


* async ~ await : 비동기, 기다려라
데이터받아오는데 시간이 걸려서 좀 기다려야하는 경우에 사용한다.

```
getMovies = async() => {
    const movies = await  axios.get("https://yts-proxy.now.sh/list_movies.json");
  }

```

<br>
<br>


### 4.1 Rendering the Movies


<br>
<br>