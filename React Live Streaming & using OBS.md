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

> 실시간 라이브 방을 만들고 라이브가 끝나면 지울수 있는 정의를 하였다.

> ###### 참조링크 : https://feel5ny.github.io/2017/12/23/log_002/

---

```java
#StreamShow.js
const { id } = this.props.match.params;
    this.player = flv.createPlayer({
      type: 'flv',
      url: `http://localhost:8000/live/${id}.flv`
    });
    this.player.attachMediaElement(this.videoRef.current);
    this.player.load();
```

> 플래시 비디오를 열었을 경우 ```url``` 끝부분에는 방 고유 번호를 생성 하고 ```url {id}``` 에 값이 들어간다.
>
> id는 방이 만들어지는 순서대로 번호가 생기는데 ```{ id }``` 번호를 넣으면 원하는 방으로 들어가진다. 

```java
#StramShow.js
    if (!this.props.stream) {
      return <div>Loading...</div>;
    }
```

> 스트리밍이 시작 하지 않았을 경우 Loading... 을 표시해준다.

----

```java
#StramShow.js
const { title, description } = this.props.stream;
    return (
      <div>
        <video ref={this.videoRef} style={{ width: '100%' }} controls />
        <h1>{title}</h1>
        <h5>{description}</h5>
      </div>
    );
  }
```

> 스트리밍 비디오를 사용하기 위해 ```.videoRef```를 사용하여 쉽게 접근할수 있게 설정해준다.

> style를 최대치로 하고 창을 줄이면 크기를 컨트롤 해주는 부분이다.

---

```java
const mapStateToProps = (state, ownProps) => {
  return { stream: state.streams[ownProps.match.params.id] };
};
```

> ```mapStateToProps``` 상태 조회해서 어떤 것들을 조회해서 ```ownProps```로 넣을지 정의 해준다.

> ```strams```을 불러와서 ```match```함과 동시에 호출후 ```mapStateToProps```에 넣어준다.

---

### 2. StreamEdit.js

```java
class StreamEdit extends React.Component {
  componentDidMount() {
    this.props.fetchStream(this.props.match.params.id);
  }
    
  onSubmit = formValues => {
    this.props.editStream(this.props.match.params.id, formValues);
  };
```

> ```fetchStream(this.props.match.params.id);```사용자의 데이터인 ```id``` 불러와서 ```math```와 후출하여 서버에 담아준다.

> ```this.props.editStream(this.props.match.params.id, formValues);```방 생성 구간에서 수정하고 싶다면 사용자의 데이터인 id 불러와서 생성할때  데이터를 ```formValues```에 담아준다.