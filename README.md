# HTML_game_making

웹에서 게임을 만들어 보겠습니다. 
js의 canvas를 사용하여서 하겠습니다(완벽한 설명이 아닐 수 있습니다!)


# 먼저 작업할 것은 캔버스에 동그라미를 그려보겠습니다.
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
이렇게 작업한 후에 drawBall함수를 실행시키면 캔버스에 원이 그려지는것을 볼 수 있을겁니다.

# 다음은 이 원을 움직이는 작업을 해보겠습니다.

```
1.먼저 원의 위치를 왼쪽 상단에 위치하게 하기 위해서 ctx.arc의 값을  20, 20, 20, 0, Math.PI*2 이렇게 설정합니다.

2.하지만 x와 y의 값을 20,20으로 고정을 했으니 원은 움직이지 않습니다. 변할수 있는 수, 즉 변수를 사용하여 x와 y의 값을 증가시키면 원은 움직일 것입니다.

3.먼저 변수 x,y를 선언합니다.
        var x = 20;
        var y = 20;
        
4.이렇게 선언한 x y값을 ctx.arc에 넣습니다. ctx.arc(x, y, 20, 0, Math.PI*2);

5.원을 그린 다음에 x와 y의 값을 증가시켜면 됩니다. 이때 dx,dy변수를 선언합니다 
        var dx = 2;
        var dy = 2;
        //dx,dy의 값은 x와 y를 더해주기 위한 변수입니다.. dx,dy의 값이 증가하면 공의 위치가 변하는 정도가 증가합니다.
       
6.이렇게 하면 총 완성되면 코드는 

        var x = 20;
        var y = 20;
        var dx = 2;
        var dy = 2;

        function draw() {
            ctx.beginPath();
            ctx.arc(x, y, 20, 0, Math.PI * 2);
            ctx.fillStyle = "#0095DD";
            ctx.fill();
            ctx.closePath();
            x += dx;
            y += dy;
            ctx.closePath();
        }

이렇게 완성이 됩니다

7.이 완성된 draw함수를 setInterval(draw,10);으로 10밀리초로 실행을 시켜주면 원이 쭈~욱 늘어나는 모습을 볼 수 있습니다. 

8.하지만 우리가 원하는 것은 이런것이 아닌 원이 하나만 나와주는 것입니다.. 그렇기 위해서는 원이 지나간 자리를 지워주는 무언가가 필요합니다.
ctx.clearRect(0, 0, canvas.width, canvas.height); 는 캔버스 전체를 지우는 역활을 합니다. 즉 draw함수 맨 윗줄에 작성을 하면 원이 이동하면 전에 있던 원은 삭제하게 됩니다.

9.이렇게 원이 움직이는것을 구현하였습니다. 다음은 원이 캔버스 밖에 나갔을때 예외를 처리해보겠습니다.
```

# 공 튕겨나감을 구현해보겠습니다.
```
1.먼저 원의 크기를 쉽게 조절하기 위해,계산을 쉽게 하기 위해 ctx.arc값에 반지름 값을 변수로 지정합시다.
var ballRadius = 10;
-> ctx.arc(x, y, ballRadius, 0, Math.PI * 2);

2.먼저 켄버스는 좌표평면이라는것을 알고 있어야합니다. 즉 x축 캔버스에서 0을 넘어선 경우,dx의 값에서 음수를 곱해서 반대로 튕겨나가게 합니다

3.그렇게 해서 조건문을 만들면 대충 
if (x + dx > canvas.width || x + dx < 0) { //x + dx가 x축 캔버스 범위를 벗어난 경우 
                dx = -dx;
}
if (y + dy > canvas.height || y + dy < 0) { //y + dy가 y축 캔버스를 벗어난 경우
                dy = -dy;
}
이런 형태가 됩니다. 

4.하지만 이렇게 해서 실행을 해보면 캔버스를 조금 오버해서 튕기는 현상이 발생합니다. 이는 원의 중심으로 예외를 처리해서 이런 오류가 발생합니다.
이를 해결하기 위해서 원의 중심이 아닌 원의 테두리가 닿으면 튕기게 만들어야 합니다.

5.if(x + dx > canvas.width-ballRadius || x + dx < ballRadius) {
    dx = -dx;
}
if(y + dy > canvas.height-ballRadius || y + dy < ballRadius) {
    dy = -dy;
}

6.이렇게 해서 원의 튕김을 구현해 보았습니다.
```
