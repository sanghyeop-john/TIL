

# JavaScript Ex2: 영화 슬라이더 만들기

> Wed Jul 13, 2022

---

[toc]

아래의 모양의 영화 슬라이더를 만들어보겠습니다.

자동으로 왼쪽과 오른쪽으로 이동하고 양옆의 화살표를 누르면 반대 방향으로 이동하도록 만들겠습니다.

우선 콘테이너의 크기를 1000px 로 지정하고 양 옆에 버튼 두개와

안에 슬라이더를 div 로 지정해보겠습니다.

![image-20220713132859833](web_javascript_ex_movie_slider.assets/image-20220713132859833.png) 

```javascript

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	#postMain{
		width: 1000px;
		height: 164px;
		margin: 0 auto;
		
	}
	#postMain>*{
		height:164px;
		float: left;
	}
	#postMain>div{
		width: 941px;
		overflow: hidden;
		position: relative;
	}
	#postList{
		width:2320px;
		height:164px;
		background: lightblue;
		position: absolute;
	}
</style>
<script>
	// 포스트 이미지 셋팅
	function setPostImage(){
		var imgTag = "";
		for(var i=1; i<=20; i++){
			imgTag += "<img src='m";
			if(i<10) imgTag += "0";
			imgTag += i + ".png'/>";
		}
		console.log(imgTag);
		document.getElementById("postList").innerHTML = imgTag;
		
	}
	// 포스트 이동하기
	var x = 0;
	var stepX = -5;
	var timer;
	function postMove(){
		x += stepX;
		document.getElementById("postList").style.left = x+"px";
		
		// 방향전환
		if(x<=-1379) stepX=5;
		if(x>=0) stepX=-5;
		
	}
	
</script>
</head>
<body onload = "setPostImage(); timer=setInterval('postMove()',200);">
	<div id="postMain">
		<input type="button" value="❮" onclick="stepX=-5"/>
		<div onmouseenter="clearInterval(timer)" onmouseleave="timer=setInterval('postMove()',200)">
			<div id="postList"></div>
		</div>
		<input type="button" value="❯" onclick="stepX=5"/>
	</div>
</body>
</html>
```

