<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>shaboot - لعبة الثعبان</title>
<style>
  body { display:flex; justify-content:center; align-items:center; height:100vh; background:#000; margin:0; }
  canvas { background:#111; display:block; }
</style>
</head>
<body>
<canvas id="game" width="400" height="400"></canvas>
<script>
const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');
const CELL = 20;
let snake = [{x:10,y:10}], food={x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)};
let dx=0, dy=0;

document.addEventListener('keydown', e => {
  if(e.key==="ArrowUp" && dy===0){dx=0;dy=-1;}
  if(e.key==="ArrowDown" && dy===0){dx=0;dy=1;}
  if(e.key==="ArrowLeft" && dx===0){dx=-1;dy=0;}
  if(e.key==="ArrowRight" && dx===0){dx=1;dy=0;}
});

function update(){
  const head = {x:snake[0].x+dx, y:snake[0].y+dy};
  if(head.x<0||head.x>=20||head.y<0||head.y>=20||snake.some(s=>s.x===head.x&&s.y===head.y)){
    alert("انتهت اللعبة!");
    snake=[{x:10,y:10}]; dx=dy=0;
    return;
  }
  snake.unshift(head);
  if(head.x===food.x && head.y===food.y){
    food = {x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)};
  } else snake.pop();
}

function draw(){
  ctx.fillStyle="#111"; ctx.fillRect(0,0,400,400);
  ctx.fillStyle="lime"; snake.forEach(s=>ctx.fillRect(s.x*CELL,s.y*CELL,CELL-2,CELL-2));
  ctx.fillStyle="red"; ctx.fillRect(food.x*CELL,food.y*CELL,CELL-2,CELL-2);
}

function loop(){ update(); draw(); setTimeout(loop,100); }
loop();
</script>
</body>
</html>
