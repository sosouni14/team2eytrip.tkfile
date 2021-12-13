# React File Upload & Like & Subscription

#### 

### 1. Install using React App

---



```
	 -------- Server/package.json  --------
	 
	"bcrypt": "^3.0.6",
    "body-parser": "^1.18.3",
    "cookie-parser": "^1.4.3",
    "cors": "^2.8.5",
    "debug": "^4.1.1",
    "express": "^4.17.1",
    "fluent-ffmpeg": "^2.1.2",
    "jsonwebtoken": "^8.5.1",
    "moment": "^2.24.0",
    "mongoose": "^5.4.20",
    "multer": "^1.4.3",
    "react-map-gl": "^6.1.17",
    "react-map-gl-geocoder": "^2.2.0",
    "react-redux": "^5.0.7",
    "saslprep": "^1.0.3",
    "supports-color": "^7.1.0"
    
    -------- Client/package.json --------
    
     "antd": "^3.24.1",
    "axios": "^0.19.2",
    "core-js": "^3.6.4",
    "formik": "^1.5.8",
    "moment": "^2.24.0",
    "react": "^16.8.6",
    "react-app-polyfill": "^1.0.6",
    "react-dom": "^16.8.6",
    "react-dropzone": "^11.4.2",
    "react-icons": "^3.7.0",
    "react-map-gl": "^6.1.17",
    "react-map-gl-geocoder": "^2.2.0",
    "react-redux": "^7.1.0-rc.1",
    "react-router-dom": "^5.0.1",
    "react-scripts": "3.4.1",
    "redux": "^4.0.0",
    "redux-promise": "^0.6.0",
    "redux-thunk": "^2.3.0",
    "yup": "^0.27.0"
```



#### #List #Client

---

​	| + client 

​		| - src

​			| - components

​			|        | + views

​			|		| - LandingPage

​			|		| - LoginPage

​			|		| - Navbar

​			|		| - RehisterPage

​			|		| - SubscriptionPage

​			|		| - VideoDetailPage

​			|			| - Sections

​			|		| - VideoUploadPage

​			|  1. App.js

---



#### #List #Server

---

​	| + server

​		| - config

​		| - middleware

​		| - models

​		| - routes

​		| 1. index.js

​	| + uploads

​		| - thumbnails

---



### 1. Components>VideoDetail.js

```java
function VideoDetailPage(props) {
  const videoId = props.match.params.videoId;
  const variable = { videoId: videoId };
```



> 랜딩페이지에 있는 ```videoId```를 ```props```로 불러와서 사용하기 위한 정의

---

```java
#VideoDetail.js 
useEffect(() => {
    Axios.post('/api/video/getVideoDetail', variable).then((response) => {
      if (response.data.success) {
        console.log(response.data);
        setVideoDetail(response.data.videoDetail);
      } else {
        alert('비디오 정보를 가져오길 실패했습니다.');
      }
    });
  }, []);
```

> ```Axios```를 이용하여 ```post ```로 서버```/getVideoDetail```에 있는 ```db``` 에서 비디오 정보를 ```response```를 보내서 받아온다

---

```java
#VideoDetail.js
if (VideoDetail.writer) {
    const subscribeButton = VideoDetail.writer._id !==
      localStorage.getItem('userId') && (
      <Subscribe
        userTo={VideoDetail.writer._id}
        userFrom={localStorage.getItem('userId')}
      /> 
```

> 페이지의 동영상이 업로드한 사람이 볼때 구독 버튼이 안보이게 ```userId```를 비교해서 구독 버튼이 사라지게 만들어준다.

---

```java
#VideoDeatil.js
return (
      <Row gutter={(16, 16)}>
        <Col lg={18} xs={24}>
          <div style={{ width: '100%', padding: '3rem 4rem' }}>
            <video
              style={{ width: '100%' }}
              src={`http://localhost:5000/${VideoDetail.filePath}`}
              controls
            />
```

> 동영상의 스타일을 정의 해주면서 동영상의 ```filePath```를 정의 해주는 부분이다.

```java
<List.Item actions={[<Subscribe userTo={VideoDetail.writer._id} userFrom={localStorage.getItem('userId')}/>,]} >
              <List.Item.Meta
                avatar={<Avatar src={VideoDetail.writer.image} />}
                title={VideoDetail.writer.name}
                description={VideoDetail.description}
              />
            </List.Item>
```

> 구독 버튼이 활성화 될때 구독을 눌르면  ```userId```키를 ```localStorage.getItem```를 사용해 전달해준다. 

> 각 ```thumbnails, title, description```을 정의 해주는 부분이다.