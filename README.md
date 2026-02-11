# FOR-XIOMI
SHE IS MY GIRL
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Nuestra Historia - Netflix Romance</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&family=Playfair+Display:wght@600&display=swap" rel="stylesheet">

<style>

body{
 margin:0;
 font-family:'Poppins',sans-serif;
 background:black;
 color:white;
 overflow:hidden;
}

/* NETFLIX DARK FADE */
#fadeLayer{
 position:fixed;
 inset:0;
 background:black;
 opacity:0;
 pointer-events:none;
 transition:opacity 1s;
 z-index:50;
}

/* BACKGROUND SLIDESHOW GLOBAL */
#bgSlideshow{
 position:fixed;
 inset:0;
 z-index:-2;
}

.bgImg{
 position:absolute;
 inset:0;
 width:100%;
 height:100%;
 object-fit:cover;
 opacity:0;
 transition:opacity 3s ease;
 filter:brightness(.35);
}

.bgImg.active{
 opacity:1;
}

/* CINEMA OVERLAY */
#cinemaOverlay{
 position:fixed;
 inset:0;
 background:radial-gradient(circle at center, transparent 55%, rgba(0,0,0,.85));
 pointer-events:none;
 z-index:2;
}

.scene{
 position:absolute;
 inset:0;
 display:flex;
 flex-direction:column;
 justify-content:center;
 align-items:center;
 text-align:center;
 opacity:0;
 transform:scale(1.08);
 transition:all 1.2s ease;
 padding:40px;
 box-sizing:border-box;
}

.scene.active{
 opacity:1;
 transform:scale(1);
 z-index:10;
}

h1{
 font-family:'Playfair Display',serif;
 font-size:clamp(2rem,4vw,3.2rem);
 text-shadow:0 0 25px rgba(255,255,255,.25);
}

p{
 font-size:clamp(1rem,2.2vw,1.3rem);
 max-width:700px;
}

button{
 margin-top:25px;
 padding:14px 34px;
 border:none;
 border-radius:40px;
 font-size:1.1rem;
 cursor:pointer;
 background:linear-gradient(45deg,#ff2e88,#ff6ec7);
 color:white;
 transition:.35s;
}

button:hover{
 transform:scale(1.08);
 box-shadow:0 0 25px rgba(255,0,120,.8);
}

input{
 width:260px;
 padding:14px;
 border-radius:30px;
 border:none;
 text-align:center;
 font-size:1rem;
}

iframe{
 width:min(360px,90vw);
 height:min(220px,50vw);
 border-radius:14px;
}

.heart{
 position:absolute;
 font-size:22px;
 animation:fall 5s linear infinite;
}

@keyframes fall{
 0%{transform:translateY(-100px)}
 100%{transform:translateY(100vh)}
}

</style>
</head>

<body>

<div id="fadeLayer"></div>
<div id="bgSlideshow"></div>
<div id="cinemaOverlay"></div>

<audio id="clickSound" src="https://assets.mixkit.co/active_storage/sfx/2568/2568-preview.mp3"></audio>

<!-- INTRO -->
<div class="scene active" id="intro">
<h1>Una bonita historia de amor 💘</h1>
<button onclick="go('song')">Comenzar</button>
</div>

<!-- SONG -->
<div class="scene" id="song">
<h1>Espero que con esta canción tengas un bonito inicio de día 💘</h1>
<br>
<iframe frameborder="no" allow="autoplay"
 src="https://audiomack.com/embed/branstadel/song/xiom"></iframe>
<button onclick="go('password')">Continuar</button>
</div>

<!-- PASSWORD -->
<div class="scene" id="password">
<h1>Acceso especial</h1>
<p>Pista: Es el nombre de la chica que hace latir mi corazón 💘</p>
<input id="pass" placeholder="Ingresa la clave">
<button onclick="checkPass()">Descifrar</button>
<p id="status"></p>
</div>

<!-- LETTER -->
<div class="scene" id="letter">
<h1>Una historia que no tendrá final...</h1>
<p>
Desde el primer momento supe que había algo diferente en ti.
Te elegiría en todas mis vidas.
</p>
<button onclick="go('question')">Continuar</button>
</div>

<!-- QUESTION -->
<div class="scene" id="question">
<h1>Xiomara... ¿Me darías el honor de ser mi San Valentín?</h1>
<button onclick="acceptLove()">Sí, acepto 💘</button>
<button id="noBtn" onmouseover="moveNo()">No</button>
</div>

<!-- FINAL -->
<div class="scene" id="final">
<h1>Sabía que dirías que sí 💘</h1>
<p id="teamo"></p>
<button onclick="go('intro')">Reiniciar historia</button>
</div>

<script>

/* DRIVE IMAGES GLOBAL NETFLIX BACKGROUND */
const images=[
"https://drive.google.com/uc?export=view&id=1nxJmYMiIW7tlg-NR5XaRX5HM1sarzoCF",
"https://drive.google.com/uc?export=view&id=12gpQrfIXnN3_YBmIxiMTYtXYBfs8nFe7",
"https://drive.google.com/uc?export=view&id=1oVonA-INOWMhpAm0C_pVTls3NokwT1eP",
"https://drive.google.com/uc?export=view&id=1MZWO5py81gVUkJbYzUOrZWgA-QJq4-Iw",
"https://drive.google.com/uc?export=view&id=1orwHa-bTMxrfOV2kybHChMlYi8kRGWHR",
"https://drive.google.com/uc?export=view&id=1VOLIXCNi7gPocjmhV463LBWe2BwjTQuR",
"https://drive.google.com/uc?export=view&id=1zGztDwRIRq-mW0ksSq6mI3hZqGIxVLj_",
"https://drive.google.com/uc?export=view&id=12r0dBFxcAbcWPfBDc5CsV9WEY8TaN5ae",
"https://drive.google.com/uc?export=view&id=1eyfeHkKGGlg1xVQYUxdwN-VLOvgSnKdw",
"https://drive.google.com/uc?export=view&id=1vYgJ6sVLTNz0KKyWQYeRmFTBE2rJFWDA",
"https://drive.google.com/uc?export=view&id=12JmCswIItNHIVji_2PezfNU2yGR7UIbH",
"https://drive.google.com/uc?export=view&id=1teqVaC0noaEU7ALdPUaPH-Cip-HZ1W9Y",
"https://drive.google.com/uc?export=view&id=1OeAvhsJZ6lo-4FX9Ezmka-p6YEj2-7cp",
"https://drive.google.com/uc?export=view&id=1KotLoetlJICDvr_N3PoV9B87wbZW2pdQ",
"https://drive.google.com/uc?export=view&id=1QXwWxylraGikdpgA_2Tlz4CedJZAOdyp"
];

const bg=document.getElementById('bgSlideshow');
images.forEach(src=>{
 let img=document.createElement('img');
 img.src=src;
 img.className='bgImg';
 bg.appendChild(img);
});

let bgIndex=0;
const bgImgs=document.querySelectorAll('.bgImg');
function cycleBg(){
 bgImgs.forEach(i=>i.classList.remove('active'));
 bgImgs[bgIndex].classList.add('active');
 bgIndex=(bgIndex+1)%bgImgs.length;
}
setInterval(cycleBg,4000);
cycleBg();

/* NARRADOR HOMBRE ESPAÑOL */
const narraciones={
 intro:'Toda gran historia comienza con un momento especial...',
 song:'Escucha esta canción con el corazón...',
 password:'Solo alguien especial conoce esta clave...',
 letter:'Hay historias que no tienen final...',
 question:'Ha llegado el momento de la gran pregunta...',
 final:'Este es solo el comienzo de algo hermoso...'
};

function narrarEscena(id){
 if(!narraciones[id]) return;
 let speech=new SpeechSynthesisUtterance(narraciones[id]);
 speech.rate=.9;
 speech.pitch=.85;
 speech.lang='es-ES';

 let voices=speechSynthesis.getVoices();
 let male=voices.find(v=>v.name.toLowerCase().includes('male') || v.name.toLowerCase().includes('hombre'));
 if(male) speech.voice=male;

 speechSynthesis.cancel();
 speechSynthesis.speak(speech);
}

function sonidoClick(){
 document.getElementById('clickSound').currentTime=0;
 document.getElementById('clickSound').play();
}

function fadeTransition(cb){
 let fade=document.getElementById('fadeLayer');
 fade.style.opacity=1;
 setTimeout(()=>{
 cb();
 fade.style.opacity=0;
 },900);
}

function go(id){
 sonidoClick();
 fadeTransition(()=>{
 document.querySelectorAll('.scene').forEach(s=>s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
 narrarEscena(id);
 });
}

function checkPass(){
 sonidoClick();
 let val=document.getElementById('pass').value.toLowerCase();
 let status=document.getElementById('status');
 if(val==='xiomara'){
 status.innerText='Descifrando código...';
 setTimeout(()=>{ status.innerText='Contraseña correcta'; setTimeout(()=> go('letter'),1200); },2000);
 }else status.innerText='Acceso denegado';
}

function moveNo(){
 let btn=document.getElementById('noBtn');
 btn.style.position='absolute';
 btn.style.left=Math.random()*80+'%';
 btn.style.top=Math.random()*80+'%';
}

function acceptLove(){
 sonidoClick();
 go('final');
 setTimeout(rainHearts,600);
 setTimeout(showTeAmo,600);
}

function rainHearts(){
 setInterval(()=>{
 let h=document.createElement('div');
 h.className='heart';
 h.innerHTML='💘';
 h.style.left=Math.random()*100+'%';
 document.body.appendChild(h);
 setTimeout(()=>h.remove(),5000);
 },320);
}

function showTeAmo(){
 const list=[
 'Te amo','Te amo mi vida','Te amo muchísimo','Te amo con todo mi corazón','Te amo para siempre',
 'Te amo hoy','Te amo mañana','Te amo cada día','Te amo más y más','Te amo infinito'
 ];
 let i=0;
 setInterval(()=>{ document.getElementById('teamo').innerText=list[i%list.length]; i++; },1200);
}

</script>

</body>
</html>
