# MapBox & React-Map-Gl

### 

### 1. Install using React Maps

---

```java
npm install react-map-gl
npm install @mapbox/mapbox-sdk
```

> React에서 Mapbox와 Map-Gl 사용하기 위해 필요한 API



#### #List

----

​	|  + client 

​		|  - src 

​		  | - components

​			| 1. MapApp.js    

​			| 2. Map.js

​			| 3. mapbox.js

​			| 4. PlacesList.js

​			| 5. index.js

​			| 6. AddPlaceForm.js

​			| 7. styles.css

---



### 2. MapApp.js

---

```java
# MapApp.js
const initialPlaces = [
  {
    id: 1,
    name: "Berlin, Germany",
    lngLat: [13.383309, 52.516806]
  },
  {
    id: 2,
    name: "Roma, Rome, Italy",
    lngLat: [12.485855, 41.909468]
  },
  {
    id: 3,
    name: "Barcelona, Barcelona, Spain",
    lngLat: [2.177657, 41.401487]
  }
];
```

> 방문목록을 만들때 Add new place로 추가한 저장한 값을  ```initialPlaces```라는 변수를 만들어 저장한다.

---

```java
# MapApp.js
async function getPlaces() {
  return new Promise((resolve) => {
    setTimeout(() => resolve(initialPlaces), 500);
  });
}
```

> ```Promise((resolve)```를 사용해 실행중인 코드가 완료될 때까지 기다리지 않고 다음 코드를 수행 할수 있게 비동기 객체를 선언했고 추가적으로 서버에서 데이터를 받아오기 전에 오류를 줄여주기 위해서도 있다.

  ```java
  # MapApp.js
  useEffect(() => {
      setLoading(true);
      (async () => {
        const places = await getPlaces();
        setPlaces(places);
        setCenter(places[1].lngLat);
        setLoading(false);
      })();
    }, []);
  ```

> promise를 이용해서 서버에 대한 ```setPlaces, setCenter, setLoading```에 대한 변수들에 데이터 로드 호출을 처리해준다.

---

```
# MapApp.js
function onSubmit(place) {
    if (places.find((x) => x.name === place.name)) {
      alert("Place already existing");
      return;
    }
    const newPlace = {
      ...place,
      id: places[places.length - 1].id + 1
    };
    setPlaces([...places, newPlace]);
    setCenter(place.lngLat);
  }
```

> Places를 추가할때 중복에 대한 추가값을 확인 해주는 부분이다.

---

```java
# MapApp.js
    return (
    <div className="app">
      <div className="sidebar">
        {isLoading ? (
          <p>Loading...</p>
        ) : (
          <>
            <PlacesList
              places={places}
              onPlaceClick={onPlaceClick}
              onPlaceRemove={onPlaceRemove}
            />
            <AddPlaceForm onSubmit={onSubmit} />{" "}
          </>
        )}
      </div>
      <Map center={center} places={places} />
    </div>
  );
}
```

> sidebar에 대한 정의로 ```List , Add , Click, Remove```기능을 추가 해주는 부분이다.

---



### 3. Map.js

