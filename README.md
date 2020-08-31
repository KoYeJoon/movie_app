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


