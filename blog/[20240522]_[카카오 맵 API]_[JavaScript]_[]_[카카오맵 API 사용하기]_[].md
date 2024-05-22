# 11일차-프로젝트

작성일시: 2024년 5월 22일 오후 2:48
복습: No
최종 편집 일시: 2024년 5월 22일 오후 2:49
최종 편집자: 이상윤

# 13일차 - 프로젝트

## 카카오 지도 api 불러오기

![지도가 들어갈 자리](img/240522/0.png)

         지도가 들어갈 자리

1. *[카카오 개발자사이트](https://developers.kakao.com/)* (https://developers.kakao.com) 접속

2. 개발자 등록 및 앱 생성

![Untitled](img/240522/1.png)

![Untitled](img/240522/2.png)

![Untitled](img/240522/3.png)

3. 웹 플랫폼 추가: 앱 선택 – [플랫폼] – [Web 플랫폼 등록] – 사이트 도메인 등록

![Untitled](img/240522/4.png)

4. 사이트 도메인 등록: [웹] 플랫폼을 선택하고, [사이트 도메인] 을 등록합니다. (예: [http://localhost:8080](http://localhost:8080/))

![경로를 제외한 프로토콜, 도메인 이름, 포트만 포함될 수 있습니다.](img/240522/5.png)

경로를 제외한 프로토콜, 도메인 이름, 포트만 포함될 수 있습니다. 
(O) [https://example.com](https://example.com/)             (X) [https://example.com/](https://example.com/)

5. 페이지 상단의 [JavaScript 키]를 지도 API의 appkey로 사용합니다.

![Untitled](img/240522/6.png)

1. <body> 안에 지도를 넣을 영역 만들기

```jsx
<div id="map" style="width:500px;height:400px;"></div>
```

1. 실제 지도를 그리는 Javascript API를 불러오기

```jsx
<script 
	type="text/javascript" 
	src="//dapi.kakao.com/v2/maps/sdk.js?appkey=발급받은 APP KEY를 넣으시면 됩니다."
></script>
```

![Untitled](img/240522/6.png)

1. 지도를 띄우는 코드 작성

```jsx
var container = document.getElementById('map'); //지도를 담을 영역의 DOM 레퍼런스
var options = { //지도를 생성할 때 필요한 기본 옵션
	center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
	level: 3 //지도의 레벨(확대, 축소 정도)
};

var map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
```

전체코드

```html
<!DOCTYPE html><html>
<head>
	<meta charset="utf-8"/>
	<title>Kakao 지도 시작하기</title>
</head>
<body>
	<div id="map" style="width:500px;height:400px;"></div>
	<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=발급받은 APP KEY를 넣으시면 됩니다."></script>
	<script>
var container= document.getElementById('map');
var options= {
			center:new kakao.maps.LatLng(33.450701, 126.570667),
			level: 3
		};

var map=new kakao.maps.Map(container, options);
	</script>
</body>
</html>
```

## 지도 내부 그리드 Radius 제거

**problem**

![Untitled](img/240522/7.png)

원인

모든 이미지에 대한 스타일이 적용 되어있을 경우 지도에는 저렇게 나타나게 된다. 

지도를 나타낼 때 작은 이미지들을 여러개 불러와서 지도를 나타내는 것이기 때문

**solution**

모든 이미지에 적용되는 radius와 shadow를 map과 따로 분리시켜서 저장.