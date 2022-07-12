# JavaScript: Scroll

> Tue Jul 12, 2022

---

[toc]



```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style>
	#content{
		width:1000px;
		background-color:#ddd;
		margin:0 auto;
	}
	#content>img{
		width:100%;
	}
</style>
<script>
	var timer;
	function moveScroll(){
		// 절대위치로 이동  x=left  y=top
		//window.scrollTo(100, 500);
		// 상대위치로 이동
		window.scrollBy(0, 10);
	}
	function scrollInfor(){
		// 현재스크롤의 위치
		console.log('y좌표', window.scrollY);
		console.log('x좌표', window.scrollX);
		console.log('y좌표', document.documentElement.scrollTop);
		
		console.log('높이', document.body.clientHeight);
		console.log('높이', document.body.scrollHeight);
	}
</script>
</head>
<body onload="scrollInfor(); setInterval('moveScroll()', 1000);">
<h1>스크롤바 이동하기</h1>
<div id="content" onmouseover="clearInterval(timer);" onmouseout="timer = setInterval('moveScroll()', 500)">
	<script>
		for(var i=1; i<=4; i++){
			document.write("<img src='../img/0"+i+".png' onmouseover='this.src=\"../img/shopping.png\"' onmouseout='this.src=\"../img/0"+i+".png\"'/>");
		}
	</script>
</div>

</body>
</html>


```

