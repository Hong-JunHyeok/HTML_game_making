# HTML_game_making

웹에서 게임을 만들어 보겠습니다. 
js의 canvas를 사용하여서 하겠습니다

먼저 작업할 것은 캔버스에 동그라미를 그려보겠습니다.
```
1. html에 <canvas id="myCanvas" width="480" height="320"></canvas> 태그를 추가해줍니다

2. 그 다음에 js에 코드를 작성해 봅시다.

3. var canvas = document.getElementById("myCanvas"); html의 canvas의 ID값을 가져온 다음에 

4. var ctx = canvas.getContext("2d"); 처럼 변수 ctx에 2D rendering context 도구를 넣습니다.

5. 그 다음 원을 그려줄 drawBall()함수를 만들어 줍니다.

6. 함수 안에는 
function drawBall() {
            ctx.beginPath();
            ctx.arc(canvas.width / 2, canvas.height/2, 50, 0, Math.PI*2);
            ctx.fillStyle = "blue";
            ctx.fill();
            ctx.closePath();
        }
이런 내용이 들어갈 것 입니다.

코드의 설명을 해보겠습니다.

- ctx.beginPath()라는 부분과 ctx.closePath()라는 부분은 캔버스의 모든 명령어가 들어갈 자리입니다. 쉽게 말해서 캔버스를 위한 {}이라고 보면 되겠습니다.

- ctx.arc()는 처음 두개의 인자는 원의 중심인 x와 y의 값을 입력받습니다. 세번째 인자는 원의 반지름, 네번째는 원을 그릴 때 시작과 끝이되는 각도입니다.(즉 라디안 값)

- ctx.fillStyle이라는 속성은 ctx.fill()의 대한 속성인데 fillStyle의 속성값에 때라 fill()함수가 실행됩니다.

- fill함수는 원의 색을 칠해주는 역활을 합니다.
```
이렇게 작업하면 캔버스에 원이 그려지는것을 볼 수 있을겁니다.
