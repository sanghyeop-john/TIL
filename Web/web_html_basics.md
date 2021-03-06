# HTML Basics

> Tue Jul 5, 2022

---

[toc]

Eclipse > Dynamic Web Project 생성 > 프로젝트명: webApp > src > main > webapp 에 html 파일 생성



## Basics

### Index.html

기본적인 html 구성에 대해 배워봅시다.

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>John & MJ</title>
</head>
<body>
<!-- html 주석문 
	
	여러줄 주석 가능
-->
	John's Website
	첫번째 (pt. 기본=16px, cm, mm, in, em,...))
	홈페이지 
	만들기
	<h1 title="heading"> 헤더 태그 (글자크게, 진하게, 1줄 차지) 
		  -> h1, h2, h3, h4, h5, h6 </h1>
	<h2> 헤더 태그 (글자크게, 진하게, 1줄 차지) 
		  -> h1, h2, h3, h4, h5, h6 </h2>
		  태그 
		  테스트 
		  중
	<h6> 헤더 태그 (글자크게, 진하게, 1줄 차지) 
		  -> h1, h2, h3, h4, h5, h6 </h6>
	
	<!-- 
		</br> : 줄 바꾸기
		&nbsp; : 스페이스
		&lt;  &gt; : < >
		&copy; : ©
		
		b, strong 태그 : 진하게
		<del> </del> : 취소선
		<strike> </strike> : 취소선 
		
	 -->
	
	<div>
		<strong>뉴 M850i xDrive 쿠페 및 그란 쿠페</strong>에는 화려한 감각을 자랑하는 새로운 &nbsp;&nbsp;&nbsp; BMW 키드니 그릴이 장착된다.</br> 
		새 라디에이터 그릴은 프레임 안쪽에 U자형 바(bar)가 배치되어 있고, <b>BMW 아이코닉 글로우(Iconic Glow)</b>가 
		적용돼 그릴 내부 상단에서 &lt; 하단으로 &gt; 마치 폭포수가 쏟아지는 듯한 조명 효과를 낸다. </br></br></br> 또한, BMW 레이저 라이트가 
		탑재된 얇은 <del>헤드램프</del>와 <strike>새로운 디자인</strike>의 에어 인테이크 인레이를 적용한 전면 범퍼가 
		조화를 이뤄 한층 더 <i>강렬한 인상</i>을 자아낸다. &copy; </br>
		log<sub>10</sub>, x<sup>2</sup>
	</div>
	<pre>
		줄 바꿈이 
		되고
		공    백 문자도 적용        된다. 
		<b>html 태그도 적용된다.</b>
	</pre>
</body>
</html>
```



## Tag

### a href : 링크

a 태그를 활용하여 링크와 연결하는 방법을 알아봅시다.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Anchor Tag (앵커태그)</title>
</head>
<body>
<!-- 
	a 태그 : 링크, 파일다운로드
	
	href : 주소
	
	target : _blank : 새로운 창, _self : 현재창에
 -->
 <!-- 같은 페이지 다른위치로 이동하기 -->
 1. <a href="#a1">What is HTML?</a> <br/>
 2. <a href="#a2">What is JavaScript?</a> <br/>
 3. <a href="#a3">What is JQuery?</a> <br/>
 4. <a href="#a4">What is Ajax?</a> <br/>
 
 <hr/>
 
 <!-- 텍스트에 링크 걸기 -->
 <a href="../index.html">Home</a>
 <br/><br/>
 <a href="https://auto.nate.com/news/articleView.html?idxno=35669" target="_blank" title="Move to news link">News Link</a>

<!-- 이미지에 링크 걸기 -->
<br/><br/>
<a href="tag02_img.html"><img src="../img/02.png"/></a>><br/>


<!-- 다운로드 -->
 <br/><br/>
<a href="../downFile/mysql_demo.sql">Download demo.sql</a>
<br/><br/>
<a href="../img/01.JPG" download>Download bape nft image</a>
<hr/>
 1. <a id="a1">What is HTML? </a> <br/>
 	<p>Hyper Text Markerup Language.</p><p>Hyper Text Markerup Language.</p><p>Hyper Text Markerup Language.</p>
 2. <a id="a2">What is JavaScript? </a> <br/>
 	<p>동적인 웹프로그래밍</p><p>동적인 웹프로그래밍</p><p>동적인 웹프로그래밍</p>
 3. <a id="a3">What is JQuery?</a> <br/>
 	<p>자바스크립트 라이브러리</p><p>자바스크립트 라이브러리</p><p>자바스크립트 라이브러리</p>
 4. <a id="a4">What is Ajax? </a><br/>
 	<p>비동기식 전송가능</p><p>비동기식 전송가능</p><p>비동기식 전송가능</p>
</body>
</html>
```



### img src : 이미지

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<!-- 
	img 태그 : 웹페이지에 이미지 표시하기
	src 속성 : 사용할 이미지 파일명
	width 속성 : 폭 (px, %)
	height 속성 : 높이
 -->
 
 Bape NFT 
  <br/> 
 <img src="../img/01.JPG" width="200px" height="200px" title="Bape NFT"/>
 <br/>
 PlanetB NFT
 <br/>
 <img src="../img/02.png" width="30%" height="300px"/>
 <br/>
 <img src="../img/03.png" alt="leaf"/>

 

</body>
</html>
```



### map & area : 지도에 링크걸기

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>1개의 이미지를 여러곳으로 링크 걸기</h1>
<img src="../img/jeju_map.jpeg" usemap="#jejuMap"/>
<pre>
	map tag, area tag
	shape : 링크 모양 (rect, circle, poly)
	coords : 좌표
	href : 이동할 페이지 
</pre>
<map name = "jejuMap">
			<!-- 사각형		   x1,y1,x2,y2 -->
	<area shape="rect" coords="170,115,300,160" 
		  href="https://www.airport.co.kr/jeju/index.do" 
		  target="_blank" title="제주국제공항"/>
		  	<!-- 원   		    x,y,r-->
	<area shape="circle" coords="330,260,50" 
		  href="https://visithalla.jeju.go.kr/main/main.do" 
		  target="_blank" title="한라산국립공원"/>
		  	<!-- 삼각   		    x1,y1,x2,y2,x3,y3...-->
	<area shape="circle" coords="70,210,160,240,100,270,10,265" 
		  href="https://www.visitjeju.net/kr/" 
		  target="_blank" title="협재해수욕장"/>
</map>
</body>
</html>
```



### ol 태그 : 순서가 있는 목록 태그

```html
<ol type="I" style="background: yellow">
	<li style="background:green"><b>Sunflower</b></li>
	<li>Iris</li>
	<li>Rose</li>
</ol>
```



### ul 태그 : 순서가 없는 목록 태그 **

가장 많이 사용되는 태그입니다.

```html
<!--
	type 속성
		disc (안이 채워진 원), circle (안이 비워진 원), square (안이 채워진 사각형)
 -->
<ul type="circle">
	<li>HTML</li>
	<li>CSS</li>
	<li>JavaScript</li>
	<li>Spring</li>
	<li><img src="../img/02.png" width="200"></li>
</ul>
```



### dl 태그 : 

```html
<dl>
	<dt>html</dt>
	<dd>hyper text markup language. hyper text markup language. hyper text markup language.</dd>
	<dt>html</dt>
	<dd>hyper text markup language. hyper text markup language. hyper text markup language.</dd>
	<dt>html</dt>
	<dd>hyper text markup language. hyper text markup language. hyper text markup language.</dd>
</dl>
```



### table : 테이블 만들기

```html
<body>
<table border="1" width="100%">
	<caption><h1 style='color:red'>Schedule</h1></caption>
	<colgroup>
		<col style="color:blue"/>
	</colgroup>
	<tr height="50">
		<th>Mon</th>
		<th>Tue</th>
		<th>Wed</th>
	</tr>
	<tr>
		<td>JavaScript</td>
		<td><img src="../img/02.png" width:"200"/></td>
		<td>Java</td>
	</tr>
	<tr>
		<td>Spring</td>
		<td>Mybatic</td>
		<td>MySQL</td>
	</tr>
	
</table>

</body>
```



### table: 행렬의 수가 다른 표만들기

```html
<body>
	<h1>행렬의 수가 다른 표만들기</h1>
	<!-- 
		colspan : 칸을 합친다
		rowspace : 줄을 합친다
	 -->
	<table border="1">
		<tr>
			<td>AAAAAA</td>
			<td>BBBBBB</td>
			<td colspan="2">CCCCCC</td>
		</tr>
		<tr>
			<td colspan="2">DDDDDD</td>
			<td>EEEEEE</td>
			<td>FFFFFF</td>
		</tr>
		<tr>
			<td>GGGGGG</td>
			<td rowspan="2">HHHHHH</td>
			<td rowspan="2">IIIIII</td>
			<td>JJJJJJ</td>
		</tr>
		<tr>
			<td>KKKKKK</td>
			<td>LLLLLL</td>
		</tr>
	</table>

</body>
```



### iframe 태그 이용하기

```html
<body>
<h1>iframe 태그 이용하기</h1>
<!--
	src: 파일명
	width, height
	frameborder: 구분선 
	scrolling : yes, no
 -->
<iframe src="https://www.nate.com" width="1300" height="300" frameborder="0"></iframe>
<img src="../img/02.png" height="300"/>
<iframe src="tag03_a_map.html" width="800" height="700" frameborder="0 scrolling="no"></iframe>
</body>
```



### meta 태그 : 페이지 설명 기술하기

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="description" content="이페이지에 대한 설명"/>
<meta name="keywords" content="컴퓨터, IT, AI"/>
<meta name="author" content="hong gildong"/>
<meta http-equiv="refresh" content="10"/>
<meta http-equiv="Refresh" content="5; tag07_iframe.html"/>
<title>Meta 태그</title>
</head>
<body>
<h1>meta 태그</h1>
<pre>
	name 속성
		description : 이 페이지에 대한 설명을 기술
		keywords : 검색엔진에 검색되는 단어들...
		author : 작성자
	http-equiv 속성	
		refresh : 새로고침
		Refresh : 
</pre>
<img src="../img/02.png"/>
</body>
</html>
```



### Audio  태그

```html
<body>
<h1>Audio 재생하기</h1>
<pre>
	src : 재생할 사운드파일
	controls : 컨트롤 바 표시
	autoplay : 자동재생
	loop : 반복
	preload : 전송완료 후 재
</pre>
<audio src="../audio_video/Kalimba.mp3" controls autoplay loop="2"></audio>

<audio controls>
	<source src="../audio_video/Kalimba.mp3" type="audio/mp3"/>
	<source src="../audio_video/Kalimba.ogg" type="audio/ogg"/>
</audio>
<img src="../img/02.png"/>
</body>
```



### Video 태그

```html
<title>Video</title>
</head>
<body>
<h1>Video 재생하기</h1>
<pre>
	src : 재생할 사운드파일
	controls : 컨트롤 바 표시
	autoplay : 자동재생
	loop : 반복
	preload : 전송완료 후 재
</pre>
<video controls width="1000" autoplay poster="../img/01.JPG">
	<source src="../audio_video/Wildlife.mp4"/>
</video>
</body>

```

