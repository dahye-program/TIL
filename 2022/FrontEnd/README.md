# FrontEnd

## 서버 사이드 렌더링 vs 클라이언트 사이드 렌더링

모바일의 시대가 도래하며, 모바일 환경에 맞춰진 웹페이지 즉 모바일 웹에 대한 니즈가 폭발적으로 증가했고 그에 따른 성능 이슈도 함께 거론됨

전통적인 웹 방식(서버 사이드 렌더링)은 성능문제를 보임

→ 요청시마다 새로고침이 일어나면서 페이지를 로딩할 때마다 서버로부터 리소스를 전달받아 해석하고 화면에 렌더링하는 방식이였기 때문

데스크탑에 비해 성능이 낮은 모바일, 스마트폰을 통해 웹페이지를 출력하기 위해서는 기존 방식과 다른 접근이 필요했고 그에 따라 **SPA(Single Page web Application) 기법**이 등장

SPA는 브라우저에 로드되고 난 후에 페이지 전체를 서버에 요청하는 것이 아닌 **최초 한번 페이지 전체를 로딩한 후 이후부터는 데이터만 변경하여 사용**할 수 있는 웹 애플리케이션을 의미

(어떤 요소를 클릭하거나 스크롤 시, 상호작용하기 위한 최소한의 요소만 변경

페이지 변경처럼 보이는 것 → 최초 로드된 js 통해 미리 브라우저에 올라간 템플릿만 교환 되는 것)

SPA는 **트래픽을 감소**시키고 **사용자에게 더 나은 경험을 제공**

서버는 단지 JSON 파일만 보내주는 역할, HTML을 그리는 역할은 클라이언트 측에서 자바스크립트가 수행 ⇒ 클라이언트 사이드 렌더링

Angular JS, Backbone JS같은 Single Page를 생성하기 쉬운 JS 프레임워크들이 등장했고 특히 Angular JS는 러닝커브를 제외한 많은 장점들 덕분에 큰 호응을 얻음(느리지만)

클라이언트쪽이 점점 무거워지자 이에 반대로 View만 관리하자는 철학으로 리액트 등장

### 클라이언트 사이드 렌더링

**장점**

- 사용자의 행동에 따라 필요한 부분만 다시 읽어들이기 때문에 서버 측에서 렌더링하여 전체 페이지를 다시 읽어들이는 것보다 **빠른 인터랙션 기대 가능**
- 서버 사이드 렌더링을 한다고 하더라도 Ajax 기능을 위해 클라이언트 렌더링 요소가 포함될 수 밖에 없음
- 서버 사이드 렌더링이 따로 필요하지 않기 때문에 일관성 있는 코드 작성 가능

**단점**

- 페이지를 읽어들이는 시간, JS를 읽어들이는 시간, JS가 화면을 그리는 시간까지 모두 마쳐야 콘텐츠가 사용자에게 보여짐 + 웹 서버에서 콘텐츠 데이터라도 가져와야 한다면 그 시간은 더 길어짐 ⇒ **초기 구동 속도가 느림**
- **검색 엔진 최적화의 문제**(대부분의 웹크롤러, 봇들이 JS 파일을 실행시키지 못하기 때문에 HTML에서만 콘텐츠를 수집하게되고 클라이언트 사이드 렌더링되는 페이지를 빈 페이지로 인식하게됨, 추가적으로 보안문제 발생)
- 기존 서버 사이드 렌더링에서는 사용자에 대한 정보를 서버측에서 세션으로 관리, 그러나 클라이언트 측에는 쿠키말고 사용자에 대한 정보를 저장할 공간이 마땅치 않음

### 서버 사이드 렌더링

**장점**

- 유저가 처음으로 컨텐츠를 접하는 시점을 당길 수 있음
- 서버 따로, 클라이언트 따로 작성하던 코드가 하나로 합쳐짐
- SEO 적용 문제 없음

**단점**

- 사용자와 인터랙션 하는 부분에서 매번 서버에 request 요청을 통해 해결해야함
- DOM 조작에서도 요청하는 과정이나 엄청난 탐색 비용으로 애를 먹음

## axios 와 fetch

### axios

- Promise based HTTP client for the browser and node.js
- node.js와 브라우저를 위한 HTTP 통신 라이브러리
- 비동기로 HTTP 통신을 가능하게 해주며 return 을 Promise 객체로 해주기 때문에 response 데이터를 다루기도 쉬움

**axios의 post method**

```jsx
axios({
  method: 'post',
  url: '/',
  data: {
    name: 'dahye',
    number: '1234',
  },
});
```

### fetch

- ES6부터 Javascript의 내장 라이브러리
- Promise 기반
- 내장 라이브러리라는 장점으로 편리

**fetch의 post method**

```jsx
const url = 'url주소'
const option = {
	method: 'POST',
	header:{
		'Accept': 'application/json',
		'Content-Type': 'application/json';
	},
	body:JSON.stringfy({
		name: 'dahye',
		age: '24'
	})}
fetch(url, options)
	.then(reponse => console.log(response))
```

## 캐싱

- 웹 사이트와 애플리케이션의 성능은 이전에 가져온 리소스들을 재사용함으로써 현저하게 향상될 수 있음
- 웹 캐시는 레이턴시와 네트워크 트래픽을 줄여줌으로써 리소스를 보여주는 데에 필요한 시간을 줄여줌
- **캐싱은 주어진 리소스의 복사본을 저장하고 있다가 요청 시에 그것을 제공하는 기술**
- 웹 캐시가 자신의 저장소 내에 요청된 리소스를 가지고 있다면, 요청을 가로채 원래의 서버로부터 리소스를 다시 다운로드하는 대신 리소스의 복사본을 반환
  - 모든 클라이언트를 서비스할 필요가 없어지므로 서버의 부하를 완화
  - (캐시가 원래 서버에 비해서) 클라이언트에 더 가까이에 있으므로 성능이 향상됨
  - 리소스를 회신하는데 더 적은 시간이 들게됨
- 캐시는 `private 캐시`와 `shared 캐시` 존재
  - `shared 캐시` 는 한명 이상의 사용자가 재사용할 수 있도록 응답을 저장하는 캐시
  - `private 캐시` 는 한명의 사용자만 사용하는 캐시
