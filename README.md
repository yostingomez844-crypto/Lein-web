<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>León IA</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#0f2027;color:white}
.app{max-width:420px;margin:auto;height:100vh;display:flex;flex-direction:column;background:#111}
header{text-align:center;padding:15px;font-size:20px;background:#000}
.chat{flex:1;padding:10px;overflow:auto}
.msg{margin:8px;padding:10px;border-radius:10px;max-width:80%}
.user{background:#1e90ff;margin-left:auto}
.bot{background:#333}
.input{display:flex;padding:10px;background:#000}
input{flex:1;padding:10px;border:none;border-radius:5px}
button{margin-left:5px;padding:10px;border:none;border-radius:5px;background:#1e90ff;color:white}
</style>
</head>
<body>

<div class="app">
<header>🦁 León IA</header>
<div class="chat" id="chat"></div>
<div class="input">
<input id="txt" placeholder="Escribe o di Ok León">
<button onclick="send()">➤</button>
<button onclick="voice()">🎤</button>
</div>
</div>

<script>
const chat=document.getElementById("chat")
const txt=document.getElementById("txt")

function add(t,c){
let d=document.createElement("div")
d.className="msg "+c
d.innerText=t
chat.appendChild(d)
chat.scrollTop=chat.scrollHeight
}

function send(){
if(!txt.value)return
add(txt.value,"user")
txt.value=""
setTimeout(()=>add("🦁 León: Estoy activo.","bot"),500)
}

function voice(){
if(!('webkitSpeechRecognition'in window)){alert("No soportado");return}
let r=new webkitSpeechRecognition()
r.lang="es-ES"
r.start()
r.onresult=e=>{
let t=e.results[0][0].transcript
txt.value=t
if(t.toLowerCase().includes("ok león")||t.toLowerCase().includes("ok leon")){
add("Ok León","user")
add("🦁 León: Te escucho.","bot")
}}
}
</script>

</body>
</html>
