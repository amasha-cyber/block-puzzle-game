<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tetris Enhanced</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{background:linear-gradient(160deg,#0b0020,#0a1040);color:#fff;font-family:Arial,sans-serif;display:flex;flex-direction:column;align-items:center;min-height:100vh;padding:10px;overflow-x:hidden}
h3{font-size:1.6em;margin:8px 0;text-shadow:0 0 20px rgba(100,200,255,0.8);letter-spacing:2px}
#hud{display:flex;gap:14px;margin-bottom:8px;flex-wrap:wrap;justify-content:center}
.hud-box{background:rgba(255,255,255,0.1);border:1px solid rgba(255,255,255,0.2);border-radius:10px;padding:5px 16px;text-align:center;min-width:80px}
.hud-label{color:#aaa;font-size:10px;text-transform:uppercase;letter-spacing:1px}
.hud-val{color:#fff;font-size:1.3em;font-weight:bold}
#game-wrap{position:relative}
canvas{display:block;background:#0a0a1a;border:2px solid rgba(100,150,255,0.3);border-radius:8px;box-shadow:0 0 30px rgba(80,120,255,0.2)}
.controls{display:flex;gap:8px;margin-top:10px;flex-wrap:wrap;justify-content:center}
.controls button{padding:12px 18px;font-size:20px;border-radius:12px;border:1px solid rgba(255,255,255,0.2);background:rgba(255,255,255,0.1);color:white;cursor:pointer;transition:all 0.15s;backdrop-filter:blur(4px)}
.controls button:active{transform:scale(0.92);background:rgba(255,255,255,0.25)}
.spark{position:fixed;border-radius:50%;pointer-events:none;z-index:9999;animation:sparkFly 0.7s ease-out forwards}
@keyframes sparkFly{0%{opacity:1;transform:translate(0,0) scale(1)}100%{opacity:0;transform:translate(var(--tx),var(--ty)) scale(0)}}
#float-msg{position:absolute;top:40%;left:50%;transform:translate(-50%,-50%);pointer-events:none;z-index:50;font-weight:900;font-size:1.4em;white-space:nowrap;font-family:Arial Black,Arial,sans-serif;opacity:0}
#float-msg.show{animation:floatPop 1.2s ease forwards}
@keyframes floatPop{0%{opacity:1;transform:translate(-50%,-50%) scale(0.5)}20%{transform:translate(-50%,-50%) scale(1.2)}60%{transform:translate(-50%,-70%) scale(1);opacity:1}100%{transform:translate(-50%,-120%) scale(0.9);opacity:0}}
</style>
</head>
<body>
<h3>🎮 Tetris Blast</h3>
<div id="hud">
  <div class="hud-box"><div class="hud-label">Score</div><div class="hud-val" id="score">0</div></div>
  <div class="hud-box"><div class="hud-label">Level</div><div class="hud-val" id="level">1</div></div>
  <div class="hud-box"><div class="hud-label">Lines</div><div class="hud-val" id="lines">0</div></div>
  <div class="hud-box"><div class="hud-label">Next</div><canvas id="next-canvas" width="80" height="80"></canvas></div>
</div>
<div id="game-wrap">
  <canvas id="game"></canvas>
  <div id="float-msg"></div>
</div>
<div class="controls">
  <button onclick="move(-1)">⬅️</button>
  <button onclick="rotatePiece()">🔄</button>
  <button onclick="move(1)">➡️</button>
  <button onclick="hardDrop()">⬇️⬇️</button>
  <button onclick="softDrop()">⬇️</button>
</div>

<script>
// ── Canvas & Sizing ───────────────────────────────────────────────────────────
var canvas=document.getElementById('game');
var ctx=canvas.getContext('2d');
var nextCanvas=document.getElementById('next-canvas');
var nCtx=nextCanvas.getContext('2d');
var COLS=10,ROWS=20,SIZE=30;

function resize(){
  var maxW=Math.min(window.innerWidth*0.95,360);
  var maxH=window.innerHeight*0.62;
  SIZE=Math.floor(Math.min(maxW/COLS,maxH/ROWS));
  canvas.width=SIZE*COLS;canvas.height=SIZE*ROWS;
}
window.addEventListener('resize',function(){resize();draw();});
resize();

// ── Audio ─────────────────────────────────────────────────────────────────────
var AC=null;
function getAC(){if(!AC)AC=new(window.AudioContext||window.webkitAudioContext)();return AC;}
function playTone(freq,dur,type,vol){
  try{var ac=getAC(),o=ac.createOscillator(),g=ac.createGain();o.connect(g);g.connect(ac.destination);o.type=type||'sine';o.frequency.value=freq;g.gain.setValueAtTime(vol||0.15,ac.currentTime);g.gain.exponentialRampToValueAtTime(0.001,ac.currentTime+dur);o.start();o.stop(ac.currentTime+dur);}catch(e){}
}
function sfxMove(){playTone(300,0.06,'sine',0.08);}
function sfxRotate(){playTone(440,0.08,'triangle',0.1);setTimeout(function(){playTone(550,0.08,'triangle',0.08);},60);}
function sfxLock(){playTone(180,0.12,'sawtooth',0.12);setTimeout(function(){playTone(140,0.1,'sawtooth',0.1);},80);}
function sfxLine1(){playTone(660,0.1,'triangle',0.18);setTimeout(function(){playTone(784,0.15,'triangle',0.16);},90);setTimeout(function(){playTone(880,0.2,'triangle',0.14);},180);}
function sfxLine2(){playTone(523,0.1,'triangle',0.2);setTimeout(function(){playTone(659,0.1,'triangle',0.2);},70);setTimeout(function(){playTone(784,0.1,'triangle',0.2);},140);setTimeout(function(){playTone(1047,0.25,'triangle',0.18);},210);}
function sfxTetris(){
  var n=[523,659,784,1047,1319,1568];
  for(var i=0;i<n.length;i++){(function(f,i){setTimeout(function(){playTone(f,0.2,'triangle',0.22);},i*80);})(n[i],i);}
  setTimeout(function(){playTone(2093,0.4,'sine',0.18);},560);
}
function sfxCelebration(){
  var m=[523,659,784,659,784,1047,784,1047,1319];
  for(var i=0;i<m.length;i++){(function(f,i){setTimeout(function(){playTone(f,0.22,'triangle',0.2);},i*110);})(m[i],i);}
  for(var i=0;i<5;i++){(function(i){setTimeout(function(){playTone(80+i*12,0.1,'sawtooth',0.12);},i*220);})(i);}
}
function sfxGameOver(){
  var n=[440,392,349,330,294,262];
  for(var i=0;i<n.length;i++){(function(f,i){setTimeout(function(){playTone(f,0.25,'sawtooth',0.18);},i*140);})(n[i],i);}
}

// ── Colors ────────────────────────────────────────────────────────────────────
// Each piece gets a vibrant gradient pair [light, dark]
var PIECE_COLORS=[
  ['#00ffff','#007a8a'],  // I - cyan
  ['#ffd700','#8a6e00'],  // O - gold
  ['#cc44ff','#5c00a8'],  // T - purple
  ['#ff6622','#8a2e00'],  // L - orange
  ['#4488ff','#0033aa'],  // J - blue
  ['#44ff88','#008840'],  // S - green
  ['#ff4466','#880020'],  // Z - red
];

var SHAPES=[
  [[1,1,1,1]],           // I
  [[1,1],[1,1]],         // O
  [[0,1,0],[1,1,1]],     // T
  [[1,0,0],[1,1,1]],     // L
  [[0,0,1],[1,1,1]],     // J
  [[0,1,1],[1,1,0]],     // S
  [[1,1,0],[0,1,1]]      // Z
];

// ── Game State ────────────────────────────────────────────────────────────────
var grid,piece,nextPiece,score,level,lines,gameRunning,gameOver,dropInterval,lastTime;

function init(){
  grid=Array.from({length:ROWS},function(){return Array(COLS).fill(0);});
  score=0;level=1;lines=0;gameRunning=true;gameOver=false;
  dropInterval=600;lastTime=0;
  piece=spawnPiece();
  nextPiece=spawnPiece();
  updateHUD();
  drawNext();
}

function spawnPiece(){
  var idx=Math.floor(Math.random()*SHAPES.length);
  return{
    shape:JSON.parse(JSON.stringify(SHAPES[idx])),
    colorIdx:idx,
    x:Math.floor(COLS/2)-1,
    y:0
  };
}

// ── Drawing ───────────────────────────────────────────────────────────────────
function drawBlock(context,x,y,colorIdx,sz,alpha){
  var light=PIECE_COLORS[colorIdx][0];
  var dark=PIECE_COLORS[colorIdx][1];
  var s=sz||SIZE,a=alpha||1;
  context.globalAlpha=a;
  // main gradient fill
  var grd=context.createLinearGradient(x*s,y*s,(x+1)*s,(y+1)*s);
  grd.addColorStop(0,light);grd.addColorStop(1,dark);
  context.fillStyle=grd;
  context.fillRect(x*s+1,y*s+1,s-2,s-2);
  // shine top-left
  context.fillStyle='rgba(255,255,255,0.3)';
  context.fillRect(x*s+2,y*s+2,s*0.4,3);
  context.fillRect(x*s+2,y*s+2,3,s*0.4);
  // border glow
  context.strokeStyle=light;
  context.lineWidth=1;
  context.globalAlpha=a*0.6;
  context.strokeRect(x*s+1,y*s+1,s-2,s-2);
  context.globalAlpha=1;
}

function drawGhost(){
  var ghost={x:piece.x,y:piece.y,shape:piece.shape,colorIdx:piece.colorIdx};
  while(!collide(ghost.x,ghost.y+1,ghost.shape))ghost.y++;
  ghost.shape.forEach(function(row,ry){
    row.forEach(function(v,rx){
      if(v)drawBlock(ctx,ghost.x+rx,ghost.y+ry,ghost.colorIdx,SIZE,0.18);
    });
  });
}

function draw(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  // grid lines
  ctx.strokeStyle='rgba(255,255,255,0.04)';ctx.lineWidth=1;
  for(var r=0;r<ROWS;r++){ctx.beginPath();ctx.moveTo(0,r*SIZE);ctx.lineTo(canvas.width,r*SIZE);ctx.stroke();}
  for(var c=0;c<COLS;c++){ctx.beginPath();ctx.moveTo(c*SIZE,0);ctx.lineTo(c*SIZE,canvas.height);ctx.stroke();}
  // locked cells
  for(var y=0;y<ROWS;y++)for(var x=0;x<COLS;x++)if(grid[y][x])drawBlock(ctx,x,y,grid[y][x]-1);
  // ghost
  if(piece)drawGhost();
  // active piece
  if(piece)piece.shape.forEach(function(row,ry){row.forEach(function(v,rx){if(v)drawBlock(ctx,piece.x+rx,piece.y+ry,piece.colorIdx);});});
}

function drawNext(){
  nCtx.clearRect(0,0,80,80);
  if(!nextPiece)return;
  var ns=18,offX=Math.floor((4-nextPiece.shape[0].length)/2),offY=Math.floor((4-nextPiece.shape.length)/2);
  nextPiece.shape.forEach(function(row,ry){row.forEach(function(v,rx){if(v)drawBlock(nCtx,offX+rx,offY+ry,nextPiece.colorIdx,ns);});});
}

// ── Particles ─────────────────────────────────────────────────────────────────
var SPARK_COLORS=['#ff4444','#ff8800','#ffdd00','#44ff88','#44aaff','#cc44ff','#ffffff','#ff44cc','#00ffff'];
function spawnParticles(cx,cy,count,colors){
  for(var i=0;i<(count||8);i++){
    var s=document.createElement('div');s.className='spark';
    var angle=Math.random()*Math.PI*2,dist=40+Math.random()*80;
    var col=colors?colors[Math.floor(Math.random()*colors.length)]:SPARK_COLORS[Math.floor(Math.random()*SPARK_COLORS.length)];
    s.style.cssText='left:'+cx+'px;top:'+cy+'px;background:'+col+';--tx:'+(Math.cos(angle)*dist)+'px;--ty:'+(Math.sin(angle)*dist)+'px;width:'+(5+Math.random()*6)+'px;height:'+(5+Math.random()*6)+'px;animation-duration:'+(0.4+Math.random()*0.5)+'s';
    document.body.appendChild(s);
    setTimeout(function(el){return function(){if(el.parentNode)el.parentNode.removeChild(el);};}(s),900);
  }
}

function lineClearParticles(rows){
  var rect=canvas.getBoundingClientRect();
  rows.forEach(function(r){
    for(var x=0;x<COLS;x+=2){
      var cx=rect.left+x*SIZE+SIZE/2,cy=rect.top+r*SIZE+SIZE/2;
      spawnParticles(cx,cy,5);
    }
  });
}

function showFloatMsg(txt,color){
  var el=document.getElementById('float-msg');
  el.textContent=txt;el.style.color=color||'#ffd700';
  el.style.textShadow='0 0 20px '+( color||'#ffd700')+',0 2px 4px rgba(0,0,0,0.8)';
  el.className='';void el.offsetWidth;el.className='show';
}

// ── Collision ─────────────────────────────────────────────────────────────────
function collide(px,py,shape){
  return shape.some(function(row,ry){
    return row.some(function(v,rx){
      if(!v)return false;
      var nx=px+rx,ny=py+ry;
      return nx<0||nx>=COLS||ny>=ROWS||(ny>=0&&grid[ny][nx]);
    });
  });
}

// ── Mechanics ─────────────────────────────────────────────────────────────────
function merge(){
  piece.shape.forEach(function(row,ry){
    row.forEach(function(v,rx){
      if(v)grid[piece.y+ry][piece.x+rx]=piece.colorIdx+1;
    });
  });
}

var LINE_MSGS=[
  ['Single! 👍','#44ff88'],
  ['DOUBLE! 🔥','#ffd700'],
  ['TRIPLE! ⚡⚡','#ff8800'],
  ['TETRIS!!! 🌈💥','#ff44cc']
];
var MOTIVATE=['Keep going! 💪','Nice move! 😎','You\'re on fire! 🔥','Smooth! ✨','Sharp! 🎯','Unstoppable! 🚀'];
var motivateTimer=null;

function clearLines(){
  var cleared=[],y=ROWS-1;
  while(y>=0){
    if(grid[y].every(function(v){return v;})){
      cleared.push(y);
      grid.splice(y,1);
      grid.unshift(Array(COLS).fill(0));
    } else y--;
  }
  if(cleared.length){
    lineClearParticles(cleared);
    var pts=[0,100,300,600,1000][cleared.length]*level;
    score+=pts;lines+=cleared.length;
    // Sound
    if(cleared.length>=4)sfxTetris();
    else if(cleared.length>=2)sfxLine2();
    else sfxLine1();
    // Message
    var msgData=LINE_MSGS[cleared.length-1];
    showFloatMsg(msgData[0]+(cleared.length>=4?' +'+pts:''),msgData[1]);
    // Level up every 10 lines
    var newLevel=Math.floor(lines/10)+1;
    if(newLevel>level){level=newLevel;dropInterval=Math.max(80,600-level*55);onLevelUp();}
    updateHUD();
  }
}

function onLevelUp(){
  sfxCelebration();
  showLevelUpScreen(level);
  // particles burst
  var rect=canvas.getBoundingClientRect();
  for(var i=0;i<20;i++){
    (function(i){setTimeout(function(){
      spawnParticles(rect.left+Math.random()*canvas.width,rect.top+Math.random()*canvas.height,10);
    },i*80);})(i);
  }
}

function lock(){
  sfxLock();
  merge();clearLines();
  piece=nextPiece;nextPiece=spawnPiece();drawNext();
  if(collide(piece.x,piece.y,piece.shape)){doGameOver();return;}
  // random motivation every ~5 pieces
  if(Math.random()<0.25){
    clearTimeout(motivateTimer);
    motivateTimer=setTimeout(function(){showFloatMsg(MOTIVATE[Math.floor(Math.random()*MOTIVATE.length)],'#aaddff');},300);
  }
}

function doGameOver(){
  gameRunning=false;gameOver=true;
  sfxGameOver();
  showLevelUpScreen(null);
}

function step(){
  if(!gameRunning)return;
  if(!collide(piece.x,piece.y+1,piece.shape)){piece.y++;}
  else lock();
}

function softDrop(){if(!gameRunning)return;step();score+=1;updateHUD();}
function hardDrop(){
  if(!gameRunning)return;
  var dropped=0;
  while(!collide(piece.x,piece.y+1,piece.shape)){piece.y++;dropped++;}
  score+=dropped*2;updateHUD();
  // impact particles
  var rect=canvas.getBoundingClientRect();
  spawnParticles(rect.left+(piece.x+piece.shape[0].length/2)*SIZE,rect.top+(piece.y+piece.shape.length)*SIZE,12);
  lock();
}
function move(dir){if(!gameRunning)return;if(!collide(piece.x+dir,piece.y,piece.shape)){piece.x+=dir;sfxMove();}}
function rotatePiece(){
  if(!gameRunning)return;
  var rot=piece.shape[0].map(function(_,i){return piece.shape.map(function(r){return r[i];}).reverse();});
  if(!collide(piece.x,piece.y,rot)){piece.shape=rot;sfxRotate();}
  else if(!collide(piece.x+1,piece.y,rot)){piece.x++;piece.shape=rot;sfxRotate();}
  else if(!collide(piece.x-1,piece.y,rot)){piece.x--;piece.shape=rot;sfxRotate();}
}

function updateHUD(){
  document.getElementById('score').textContent=score;
  document.getElementById('level').textContent=level;
  document.getElementById('lines').textContent=lines;
}

// ── Level Up / Game Over Screen ───────────────────────────────────────────────
function showLevelUpScreen(newLevel){
  var existing=document.getElementById('celebration-overlay');
  if(existing)existing.parentNode.removeChild(existing);
  var ov=document.createElement('div');
  ov.id='celebration-overlay';
  var isGO=newLevel===null;
  ov.style.cssText='position:fixed;inset:0;z-index:9999;display:flex;flex-direction:column;align-items:center;justify-content:center;background:rgba(5,0,20,0.9);animation:lvFadeIn 0.4s ease;overflow:hidden';
  ov.innerHTML='<style>@keyframes lvFadeIn{from{opacity:0}to{opacity:1}}@keyframes lvFadeOut{from{opacity:1}to{opacity:0}}@keyframes titleDrop{0%{transform:translateY(-70px) scale(0.5);opacity:0}60%{transform:translateY(8px) scale(1.06)}100%{transform:translateY(0) scale(1);opacity:1}}@keyframes numPop{0%{transform:scale(0) rotate(-15deg);opacity:0}60%{transform:scale(1.3) rotate(4deg)}100%{transform:scale(1) rotate(0deg);opacity:1}}@keyframes shimmer{0%,100%{text-shadow:0 0 20px #ffd700,0 0 40px #ff8800}50%{text-shadow:0 0 40px #fff,0 0 80px #ffd700}}@keyframes subRise{0%{transform:translateY(50px);opacity:0}100%{transform:translateY(0);opacity:1}}@keyframes btnPulse{0%,100%{transform:scale(1);box-shadow:0 0 16px rgba(255,215,0,0.4)}50%{transform:scale(1.06);box-shadow:0 0 36px rgba(255,215,0,0.8)}}@keyframes confettiFall{0%{transform:translateY(-20px) rotate(0deg);opacity:1}100%{transform:translateY(100vh) rotate(720deg);opacity:0}}</style>'+
  '<div id="cel-confetti" style="position:absolute;inset:0;pointer-events:none;overflow:hidden"></div>'+
  '<div style="text-align:center;position:relative;z-index:2;padding:20px">'+
  (isGO?
    '<div style="font-size:3em;animation:titleDrop 0.6s ease forwards">💀</div>'+
    '<div style="font-family:Arial Black,Arial;font-size:2em;font-weight:900;color:#ff4444;letter-spacing:3px;text-transform:uppercase;animation:titleDrop 0.7s 0.1s both;margin:8px 0">Game Over</div>'+
    '<div style="font-size:1.1em;color:#fff;animation:subRise 0.6s 0.4s ease both;margin-bottom:6px">Score: <span style="color:#ffd700;font-weight:bold">'+score+'</span></div>'+
    '<div style="font-size:1em;color:#ccc;animation:subRise 0.6s 0.5s ease both;margin-bottom:20px">Level: <span style="color:#ffd700">'+level+'</span> &nbsp;|&nbsp; Lines: <span style="color:#ffd700">'+lines+'</span></div>'+
    '<button onclick="restartGame()" style="padding:12px 40px;border-radius:26px;border:none;background:linear-gradient(135deg,#ffd700,#ff6600);color:#1a0020;font-size:1.1em;font-weight:bold;cursor:pointer;animation:subRise 0.5s 0.7s ease both,btnPulse 1.5s 1.2s infinite">Play Again 🔄</button>'
  :
    '<div style="font-size:3em;animation:titleDrop 0.6s ease forwards">🏆</div>'+
    '<div style="font-family:Arial Black,Arial;font-size:1.8em;font-weight:900;color:#ffd700;letter-spacing:3px;text-transform:uppercase;animation:titleDrop 0.7s 0.1s both,shimmer 2s 0.8s infinite;margin:8px 0">Level Up!</div>'+
    '<div style="font-size:1em;color:#fff;letter-spacing:2px;animation:subRise 0.5s 0.4s ease both;margin-bottom:8px">Welcome to</div>'+
    '<div style="font-family:Arial Black,Arial;font-size:5em;font-weight:900;color:#ffd700;line-height:1;animation:numPop 0.7s 0.55s both,shimmer 1.5s 1.2s infinite;margin-bottom:16px">'+newLevel+'</div>'+
    '<div style="color:#aaa;font-size:0.9em;animation:subRise 0.5s 0.8s ease both;margin-bottom:20px">Speed increased! ⚡ Score: <span style="color:#ffd700">'+score+'</span></div>'+
    '<button onclick="dismissCelebration()" style="padding:12px 40px;border-radius:26px;border:none;background:linear-gradient(135deg,#ffd700,#ff6600);color:#1a0020;font-size:1.1em;font-weight:bold;cursor:pointer;animation:subRise 0.5s 0.9s ease both,btnPulse 1.5s 1.4s infinite">Let\'s Go! 🚀</button>'
  )+
  '</div>';
  document.body.appendChild(ov);
  if(!isGO){spawnCelebrationConfetti();setTimeout(function(){if(document.getElementById('celebration-overlay'))dismissCelebration();},5000);}
}

function spawnCelebrationConfetti(){
  var container=document.getElementById('cel-confetti');if(!container)return;
  var colors=['#ffd700','#ff4444','#44ff88','#44aaff','#ff44cc','#fff','#ff8800','#cc44ff'];
  for(var i=0;i<55;i++){
    (function(i){setTimeout(function(){
      if(!document.getElementById('cel-confetti'))return;
      var c=document.createElement('div'),sz=6+Math.random()*10,rect=Math.random()>0.5;
      c.style.cssText='position:absolute;left:'+(Math.random()*100)+'%;top:-20px;width:'+sz+'px;height:'+(rect?sz*0.4:sz)+'px;background:'+colors[Math.floor(Math.random()*colors.length)]+';border-radius:'+(rect?'2px':'50%')+';animation:confettiFall '+(1.5+Math.random()*2.5)+'s '+(Math.random()*0.4)+'s ease-in forwards';
      container.appendChild(c);
    },i*65);})(i);
  }
  // extra spark burst
  var rect=canvas.getBoundingClientRect();
  for(var i=0;i<15;i++){
    (function(i){setTimeout(function(){spawnParticles(rect.left+Math.random()*canvas.width,rect.top+Math.random()*canvas.height,8);},i*70);})(i);
  }
}

function dismissCelebration(){
  var ov=document.getElementById('celebration-overlay');if(!ov)return;
  ov.style.animation='lvFadeOut 0.4s ease forwards';
  setTimeout(function(){if(ov&&ov.parentNode)ov.parentNode.removeChild(ov);},400);
}

function restartGame(){
  var ov=document.getElementById('celebration-overlay');if(ov&&ov.parentNode)ov.parentNode.removeChild(ov);
  init();
}

// ── Keyboard ──────────────────────────────────────────────────────────────────
document.addEventListener('keydown',function(e){
  if(e.key==='ArrowLeft')move(-1);
  else if(e.key==='ArrowRight')move(1);
  else if(e.key==='ArrowDown')softDrop();
  else if(e.key==='ArrowUp'||e.key==='x'||e.key==='X')rotatePiece();
  else if(e.key===' '){e.preventDefault();hardDrop();}
});

// ── Game Loop ─────────────────────────────────────────────────────────────────
function loop(time){
  if(time===undefined)time=0;
  if(gameRunning&&time-lastTime>dropInterval){step();lastTime=time;}
  draw();
  requestAnimationFrame(loop);
}

init();
loop();
</script>
</body>
</html>
