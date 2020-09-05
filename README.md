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

1. console.log로 movies의 형태를 보면 data-data-movie 이렇게 접근이 가능하다는 것을 알 수 있음

2. (1)movies.data.data.movie  or (2){data : {data : movies}} 로 표현 가능

(2)를 적용한 예시
```
const {
      data : {
        data : { movies }
      }
    } = await axios.get("https://yts-proxy.now.sh/list_movies.json");

```

<br>

(1) this.setState({movies : movies}); 
(1)movies 좌항 : state에서 옴
(1)movies 우항 : axios에서 옴
or (2)this.setState({movies})

* component가 state가 필요 없을 때에는 class component로 정의하지 않아도 됨 -> Movie.js는 class component로 정의하지 않아도 됨

(Movie.js)
```
import React from "react";
import PropTypes from "prop-types";

function Movie({ id, year, title, summary, poster }) {
  return <h4>{title}</h4>;
}

Movie.propTypes = {
  id: PropTypes.number.isRequired,
  year: PropTypes.number.isRequired,
  title: PropTypes.string.isRequired,
  summary: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired
};

export default Movie;
```

(App.js)

```
render(){
    const { isLoading,movies } = this.state;

    return (
      <div>
        {isLoading
          ? "Loading..."
          : movies.map(movie => (
              <Movie
                key={movie.id}
                id={movie.id}
                year={movie.year}
                title={movie.title}
                summary={movie.summary}
                poster={movie.medium_cover_image}
              />
            ))}
      </div>
    );
  }

```

<br>
<br>

### 4.2 Styling the Movies

* styling을 위해 App.css와 Movie.css를 만들고 이를 활용하는 js file에서 import 해준다.

```
(ex)
import "./App.css";
```


<br>

1. Styling을 위해 div 대신 section으로 구분해주고, render 함수에서 return 하는 부분을 여러개의 class로 나누어줌

(App.js)
```
render(){
    const { isLoading,movies } = this.state;

    return (
      <section class="container">
      {isLoading ? (
        <div class="loader">
          <span class="loader__text">Loading...</span>
        </div>
      ) : (
        <div class="movies">
          {movies.map(movie => (
            <Movie
              key={movie.id}
              id={movie.id}
              year={movie.year}
              title={movie.title}
              summary={movie.summary}
              poster={movie.medium_cover_image}
            />
          ))}           
            </div>
          )}   
      </section>
    );
  }
```


2. Movie component 역시, styling을 위해서 return하는 것을 여러 개의 class로 분할해줌. 

```
function Movie({ id, year, title, summary, poster }) {
  return (<div class="movie">
      <img src={poster} alt={title} title={title} />
      <div class="movie__data">
      <h3 class="movie__title" >{title}</h3>
      <h5 class ="movie__year">{year}</h5>
      <p class="movie__summary">{summary}</p>
      </div>
      </div>
      );
```

<br>
<br>


### 4.3 Adding Genres

* javaScript에서는 div class 와 같이 이용하는 경우 className이라고 정의해야함.
  * 이유  : class로 묶는 객체와 혼란을 겪기 때문에


* map을 사용하는 경우, key 값 필요(item, index)


(Movie.js)
```
<ul className="genres">
          {genres.map((genre, index) => (
            <li key={index} className="genres__genre">
              {genre}
            </li>
          ))}
        </ul>
```


<br>
<br>

### 4.4 Styles Timelapse

* 몰랐던 css 문법


  * box-sizing -> 박스의 크기를 화면에 표시하는 방식을 변경하는 속성
    1. content-box : 기본값으로 너비, 높이는 content 영역만을 의미함(border, padding, margin 제외)
    2. border-box : 너비, 높이 계산 시 content, padding, border를 포함함(margin 제외)

  <br>

  * justify-content -> 콘텐츠의 좌우 관계 정렬 상태를 정의

  ```
  justify-content : flex-start | flex-end | center | space-between | space-around | inherit;
  ```

    1. flex-start : 요소의 정렬상태를 왼쪽(기본)으로 설정
    2. flex-end : 요소의 좌우 정렬 상태를 오른쪽 끝점으로 설정
    3. center : 요소의 좌우 정렬 상태를 가운데로 설정
    4. space-between : 요소와 요소사이의 간격을 왼쪽과 오른쪽을 기준으로 설정
    5. space-around : 요소와 요소 사이의 간격을 가운데를 기준으로 설정
    6. inherit : justify-content의 속성 값을 상위요소한테 상속받음

  
  <br>

  * flex-wrap : 나열된 요소들의 총 넓이가 부모 넓이보다 클 때, 다음 줄에 이어서 나열해주는 기능

    1. nowrap : 부모 넓이에 맞게 요소들의 넓이를 강제 축소
    2. wrap : 부모 넓이보다 요소들의 총 넓이가 크다면 나머지 요소들은 다음줄로 줄 바꿈
    3. wrap-reverse : 줄바꿈하는 요소들을 역순으로 배열
    4. initial : 기본 값 (nowrap)
    5. inherit : 부모 요소의 설정 값을 사용

  <br>

  * box-shadow : 박스 요소에 그림자를 넣는 속성

    1. none : 기본값 , 그림자가 표시되지 않음
    2. h-shadow : 필수지정, 수평 그림자 위치
        양수 값 지정 : 박스 오른쪽에 그림자가 생김
        음수 값 지정 : 박스 왼쪽에 그림자가 생김
    3. v-shadow : 필수지정, 수직 그림자 위치
        양수 값 지정 : 박스 위쪽에 그림자가 생김
        음수 값 지정 : 박스 아래쪽에 그림자가 생김
    4. blur : 선택지정, 그림자의 흐림 정도
        0 : 그림자가 진함
        ++ : 점점 그림자가 흐릿해짐 ( 양수값만 허용)
    5. spread : 선택지정 , 그림자가 드리워지는 정도
        양수 값 지정 : 그림자가 커짐
        음수 값 지정 : 그림자가 작아짐

  <br>

  * rgba(x,y,z,w) : (적색, 녹색, 청색, 투명도)
    * w : 0.0(투명)~1.0(불투명)


  <br>

  * position

  ```
  position: static | relative | absolute | fixed | sticky
  ```
    1. static : 요소를 문서 흐름에 맞추어 배치
    2. relative : 이전 요소(주로 부모 요소)에 자연스럽게 연결하여 위치 지정
    3. absolute : 원하는 위치를 지정해 배치
    4. fixed : 지정한 위치에 고정하여 배치
    5. sticky : 위치에 따라서 동작방식이 달라짐. 요소가 임게점 (scroll 박스 기준) 이전에는 relative와 같이 동작하고, 그 이후에는 fixed와 같이 동작

<br>
<br>


### 4.5 Cutting the summary

* summary가 긴 경우, 자르기

(javascript)
ex . const summary = "60글자"
summary.slice(0,10)
앞에서부터 10글자 반환해줌

(응용한 예시)

```
<p className="movie__summary">{summary.slice(0, 180)}...</p>
```

<br>
<br>


### 5.0 Deploying to Github Pages

* gh-pages 이용하기

gh-pages : 웹사이트를 github의 github page 도메인에 나타나게 해줌.

1. movie_app directory에서 gh-pages 설치 

```
$ npm i gh-pages
```

<br>

2. github에서 프로젝트 이름을 통해 가져온다.

(package.json)
```
"homepage" : "https://KoYeJoon.github.io/movie_app/"
```

<br>

3. npm run build를 통해 build 폴더를 제공받는다. 

```
$ npm run build
```

<br>

4. scripts 안에 deploy를 추가한다. deploy는 gh-pages를 호출하고, build 폴더를 업로드 한다.

(package.json)
```
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "deploy" : "gh-pages -d build ",
    "predeploy" : "npm run build"
  },
```

<br>

5. terminal 에서 build 한다.

```
$ npm run deploy
```
<br>

6. " https://KoYeJoon.github.io/movie_app/ "에 들어가서 확인해본다.


<br>
<br>

### 5.1 Are we done?

* react hook 덕분에 state를 갖기 위해 class component를 가질 필요가 없다. -> react hook 강의 참고


<br>
<br>

### 6.0 Getting Ready for the Router

* install react-router-dom

```
$npm install react-router-dom
```

* 첫번째 screen은 영화설명 , 두번째 screen은 about 페이지가 되도록 구성

* components 폴더에는 domain을 담고, routes 폴더에는 각화면 Home.js와 About.js에 관한 내용을 담도록 한 것 같다.   

--> App.js에 있던 내용을 home.js로 옮김


<br>
<br>

### 6.1 Building the Router

* router 
  * /home -> home.js
  * /about -> about.js
  로 이동하도록 함

* basic url을 우선적으로, rendering한다. 
두개 이상이 rendering 될 수 있으므로 exact = {true}라는 것을 통해 정확히 그 주소일 때만 랜더링되도록 한다.

```
function App() {
  return (
    <HashRouter>
      <Route path="/" exact={true} component={Home} />
      <Route path="/about" component={About} />
    </HashRouter>
  );
}
```

<br>
<br>


### 6.2 Building the Navigation

1. Navigation.css와 Navigation.js를 component 폴더에 만들어주기

(Navigation.js)
* Link : Home 혹은 about 버튼을 a href로 연결하였을 때는 전체화면이 새로고침되므로 이를 방지하기 위해 Link를 이용한다.

```
import React from "react";
import { Link } from "react-router-dom";
import "./Navigation.css";

function Navigation() {
  return (
    <div className="nav">
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </div>
  );
}

export default Navigation;
```



<br>

2. App.js에서 연결해주기

```
import Navigation from "./components/Navigation";

function App() {
  return (
    <HashRouter>
      <Navigation />
      <Route path="/" exact={true} component={Home} />
      <Route path="/about" component={About} />
    </HashRouter>
  );
}
```
* Link : router밖에서 사용불가
따라서 `<HashRouter>` 안에서 `<Navigation />`을 정의하여 사용하기

* HashRouter와 BrowserRouter 차이
  * HashRouter : /#/와 같은 것이 있으나 github page에 올리기 편함.
  * BrowserRouter : /#/와 같은 요상한 것이 없음 -> github page에 사용하기는 어려움.
<br>
<br>

### 6.3 Sharing Props Between Routes

* 모든 router는 props를 갖는다.
* `<Link>`에는 Props를 보낼 수 있다.


<br>
<br>

### 6.4 Redirecting

* redirect ; 이 코드에서는 location이 undifined 된 경우, home으로 보낸다.
-> url에 직접적으로 /movie-direct로 하면 redirect 되도록 함.

<br>
<br>


##### reference

니꼬쌤 github ; https://github.com/nomadcoders/movie_app_2019
네이버 블로그 : http://blog.naver.com/PostView.nhn?blogId=shinekjm&logNo=220894933361
네이버 블로그 : https://m.blog.naver.com/PostView.nhn?blogId=pjh445&logNo=221160742046&proxyReferer=https:%2F%2Fwww.google.com%2F
tistory 블로그 : https://engkimbs.tistory.com/922 [새로비]