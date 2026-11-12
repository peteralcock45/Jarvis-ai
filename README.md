
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#020817">
<title>JARVIS AI</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;min-height:100vh;text-align:center;
 background:radial-gradient(circle,#103d70,#020817 75%);
 color:#42caff;font-family:Arial,sans-serif;
 padding:20px 12px
}
h1{font-size:38px;letter-spacing:7px;text-shadow:0 0 20px #00aaff}
.status{font-size:12px;letter-spacing:3px;color:#9bdfff}
.core{
 width:220px;height:220px;margin:40px auto;
 border:3px solid #32caff;border-radius:50%;
 display:grid;place-items:center;
 box-shadow:0 0 30px #009dff,inset 0 0 30px #009dff;
 animation:glow 3s infinite
}
@keyframes glow{50%{box-shadow:0 0 55px #00aaff,inset 0 0 40px #008cff}}
.inner{
 width:160px;height:160px;border:2px solid #8beaff;
 border-radius:50%;display:grid;place-items:center;font-size:55px
}
#output{
 background:#04172c;border:1px solid #1689c5;
 border-radius:15px;padding:20px;margin:20px auto;
 max-width:500px;min-height:90px;color:white
}
button{
 background:#07385d;color:#62dfff;border:1px solid #32caff;
 border-radius:30px;padding:15px 22px;margin:7px;font-size:15px
}
input{
 background:#04172c;border:1px solid #1689c5;
 color:white;padding:14px;border-radius:25px;width:65%
}
</style>
</head>
<body>
<h1>J.A.R.V.I.S.</h1>
<div class="status">PERSONAL AI SYSTEM</div>
<div class="status" id="status">SYSTEM ONLINE</div>
<div class="core"><div class="inner">J</div></div>
<div id="output">Good day, sir. JARVIS is online. How may I assist?</div>
<button onclick="listen()">🎙 SPEAK TO JARVIS</button>
<br>
<input id="question" placeholder="Type a command">
<button onclick="send()">SEND</button>
<br>
<button onclick="speak('All systems are operational, sir.')">SYSTEM CHECK</button>
<script>
function speak(t){
 document.getElementById('output').textContent=t;
 let s=new SpeechSynthesisUtterance(t);
 s.rate=.88;s.pitch=.75;
 speechSynthesis.cancel();speechSynthesis.speak(s);
}
function reply(t){
 let q=t.toLowerCase(),a="I'm listening, sir.";
 if(q.includes('hello'))a="Good day, sir. JARVIS at your service.";
 else if(q.includes('time'))a="The time is "+new Date().toLocaleTimeString();
 else if(q.includes('date'))a="Today is "+new Date().toLocaleDateString();
 else if(q.includes('name'))a="I am JARVIS, your personal assistant.";
 else if(q.includes('website'))a="I can help you create a website. What would you like?";
 else if(q.includes('app'))a="Let's plan and build your app, sir.";
 else if(q.includes('joke'))a="Why did the computer get cold? It left its Windows open.";
 speak(a);
}
function send(){
 let i=document.getElementById('question'),v=i.value.trim();
 if(v){i.value='';reply(v);}
}
function listen(){
 let R=window.SpeechRecognition||window.webkitSpeechRecognition;
 if(!R){speak('Please use Chrome for voice recognition.');return;}
 let r=new R();r.lang='en-AU';
 document.getElementById('status').textContent='LISTENING';
 r.onresult=e=>reply(e.results[0][0].transcript);
 r.onerror=()=>document.getElementById('status').textContent='VOICE ERROR';
 r.onend=()=>document.getElementById('status').textContent='SYSTEM ONLINE';
 r.start();
}
</script>
</body>
</html>
