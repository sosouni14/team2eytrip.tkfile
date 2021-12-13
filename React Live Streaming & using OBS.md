# React Live Streaming & using OBS



### 2. StreamShow.js

---

```java
#StramShow.js
    class StreamShow extends React.Component {
  constructor(props) {
    super(props);
      this.videoRef = React.createRef();
  }
```

> 클래스 ```class StreamShow``` 를 ```React.Component```에 상속받아 ```constructor, super``` 호출 받고
>
> ```this.videoRef```가 리렌더링되어도 초기값이 되지않게 ```React.createRef();```를 선언해주었다.

----

```java
#StramShow.js 
componentDidMount() {
    const { id } = this.props.match.params;
    this.props.fetchStream(id);
    this.buildPlayer();
  }
```

> ```componentDidMount() ```를 값을 유지하기 위해 선언하였고 생성된 { id } 값을 유지해주고
>
> props를 사용해서 id값을 받아서 넘겨준다.

---

```java
#StreamShow.js
    componentDidUpdate() {
    this.buildPlayer();
  }

  componentWillUnmount() {
    this.player.destroy();
  }
```

> 방 생성 

[1]: https://feel5ny.github.io/2017/12/23/log_002/	"참조"



