<!DOCTYPE html>  
<html>  
<head>  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Mii Creator Ultimate+</title>  
  
<style>  
body {  
  margin:0;  
  font-family: Arial;  
  background:#dfe6ee;  
  text-align:center;  
}  
  
canvas {  
  background:white;  
  border-radius:50%;  
  border:3px solid black;  
  touch-action:none;  
}  
  
.panel {  
  background:#fff;  
  padding:10px;  
  max-width:420px;  
  margin:auto;  
  box-shadow:0 0 10px rgba(0,0,0,0.2);  
}  
  
button, select, input {  
  margin:5px;  
  padding:6px;  
}  
</style>  
</head>  
  
<body>  
  
<h3>Mii Creator Ultimate+</h3>  
  
<canvas id="c" width="320" height="420"></canvas>  
  
<div class="panel">  
  
<!-- FACE -->  
<div>  
Skin <input type="color" id="skin" value="#f5c6a5">  
Hair  
<select id="hair">  
<option value="0">None</option>  
<option value="1">Short</option>  
<option value="2">Top</option>  
</select>  
</div>  
  
<!-- EXPRESSION -->  
<div>  
Expression  
<select id="expression">  
<option value="neutral">Neutral</option>  
<option value="happy">Happy</option>  
<option value="sad">Sad</option>  
<option value="angry">Angry</option>  
<option value="surprised">Surprised</option>  
</select>  
</div>  
  
<!-- BODY -->  
<div>  
Height  
<input type="range" id="height" min="0.8" max="1.4" step="0.05" value="1">  
  
Shirt  
<input type="color" id="shirt" value="#4a90e2">  
</div>  
  
<!-- PERSONAL -->  
<div>  
<input id="name" placeholder="Name">  
<input id="personality" placeholder="Personality">  
</div>  
  
<div>  
<button onclick="saveSlot()">Save Slot</button>  
<button onclick="loadSlot()">Load Slot</button>  
<button onclick="speak()">Speak</button>  
</div>  
  
<div id="slots"></div>  
  
</div>  
  
<script>  
const c=document.getElementById("c");  
const ctx=c.getContext("2d");  
  
let features={  
  leftEye:{x:110,y:130},  
  rightEye:{x:210,y:130},  
  mouth:{x:160,y:210}  
};  
  
let currentSlot=0;  
let slotCount=5;  
  
// DRAW  
function draw(){  
  ctx.clearRect(0,0,320,420);  
  
  let h=height.value;  
  
  // BODY  
  ctx.fillStyle=shirt.value;  
  ctx.fillRect(110,260,100,120*h);  
  
  // HEAD  
  ctx.fillStyle=skin.value;  
  ctx.beginPath();  
  ctx.ellipse(160,150,110,130,0,0,Math.PI*2);  
  ctx.fill();  
  
  // HAIR  
  ctx.fillStyle="#222";  
  if(hair.value==1) ctx.fillRect(70,40,180,60);  
  if(hair.value==2) ctx.fillRect(100,20,120,80);  
  
  // EXPRESSION MODIFIERS  
  let ex=expression.value;  
  
  let eyeY=130;  
  let mouthY=210;  
  
  if(ex==="sad") mouthY=230;  
  if(ex==="angry") eyeY=120;  
  if(ex==="surprised") eyeY=120;  
  
  // EYES  
  ctx.fillStyle="black";  
  ctx.beginPath();  
  ctx.arc(features.leftEye.x,eyeY,10,0,Math.PI*2);  
  ctx.arc(features.rightEye.x,eyeY,10,0,Math.PI*2);  
  ctx.fill();  
  
  // MOUTH  
  ctx.strokeStyle="black";  
  ctx.lineWidth=3;  
  
  if(ex==="happy"){  
    ctx.beginPath();  
    ctx.arc(160,mouthY,35,0,Math.PI);  
    ctx.stroke();  
  }  
  
  if(ex==="sad"){  
    ctx.beginPath();  
    ctx.arc(160,mouthY,35,Math.PI,Math.PI*2);  
    ctx.stroke();  
  }  
  
  if(ex==="neutral"){  
    ctx.beginPath();  
    ctx.moveTo(130,mouthY);  
    ctx.lineTo(190,mouthY);  
    ctx.stroke();  
  }  
  
  if(ex==="angry"){  
    ctx.beginPath();  
    ctx.moveTo(130,mouthY);  
    ctx.lineTo(190,mouthY-5);  
    ctx.stroke();  
  }  
  
  if(ex==="surprised"){  
    ctx.beginPath();  
    ctx.arc(160,mouthY,15,0,Math.PI*2);  
    ctx.stroke();  
  }  
}  
  
// SAVE SLOT  
function saveSlot(){  
  let data={  
    skin:skin.value,  
    hair:hair.value,  
    expression:expression.value,  
    height:height.value,  
    shirt:shirt.value,  
    name:name.value,  
    personality:personality.value  
  };  
  localStorage.setItem("mii_"+currentSlot,JSON.stringify(data));  
}  
  
// LOAD SLOT  
function loadSlot(){  
  let data=JSON.parse(localStorage.getItem("mii_"+currentSlot));  
  if(!data) return;  
  
  skin.value=data.skin;  
  hair.value=data.hair;  
  expression.value=data.expression;  
  height.value=data.height;  
  shirt.value=data.shirt;  
  name.value=data.name;  
  personality.value=data.personality;  
  
  draw();  
}  
  
// SPEECH  
function speak(){  
  let text = name.value + " feels " + expression.value + ". They are " + personality.value;  
  let u = new SpeechSynthesisUtterance(text);  
  speechSynthesis.speak(u);  
}  
  
// slots UI  
let slots=document.getElementById("slots");  
for(let i=0;i<slotCount;i++){  
  let b=document.createElement("button");  
  b.innerText="Slot "+(i+1);  
  b.onclick=()=>currentSlot=i;  
  slots.appendChild(b);  
}  
  
// update  
document.querySelectorAll("input,select").forEach(el=>{  
  el.addEventListener("input",draw);  
});  
  
draw();  
</script>  
  
</body>  
</html>  
