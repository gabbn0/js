# js
//variavelbolinha
let xBolinha = 100;
let yBolinha = 150;
let diametro = 20;
let raio = diametro / 2
let velocidadexBolinha = 8;
let velocidadeyBolinha = 8;

//variavelraquete
let xRaquete = 5;
let yRaquete = 150;
let cRaquete = 10;
let aRaquete = 98;

//variavel raquete oponente
let xOponente = 585
let yOponente = 150
let velocidadeyOponente;

// variavel placar
let meuspontos = 0;
let pontosOponente = 0; 

// variavel sons
let raquetada;
let ponto;
let trilha;
 
function setup() {
  createCanvas(600, 400);
  trilha.loop();
  
}
  


function draw() {
  background("black");
  mostrabolinha();
  movimentabolinha();
  verificaborda();
  mostraRaquete(xRaquete, yRaquete);
  movimentaRaquete();
  verificaRaquete(xRaquete, yRaquete);
  mostraRaquete(xOponente, yOponente);
  movimentaOponente(); 
  verificaRaquete(xOponente, yOponente);
  incluiplacar();
  marcarpontos();
}
  
 
// funcoes a bolinha 

function mostrabolinha(){
  circle(xBolinha, yBolinha, diametro);
}

function movimentabolinha(){
  xBolinha += velocidadexBolinha;
  yBolinha += velocidadeyBolinha;
}

function bolinhaNaoFicaPresa(){
    if (XBolinha - raio < 0){
    XBolinha = 23
    }
}

function verificaborda(){
  if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadexBolinha *= -1;
 }
  if (yBolinha + raio > height || yBolinha - raio < 0) {
    velocidadeyBolinha *= -1;
  }
}

//funcoes da raquete

function mostraRaquete(x, y){
  rect(x, y, cRaquete, aRaquete)
}

function movimentaRaquete(){
  if (keyIsDown (UP_ARROW)){
    yRaquete -= 10;
  }
  if (keyIsDown (DOWN_ARROW)){
    yRaquete += 10;
  }
}

function verificaRaquete(x,y){
  colidiu = collideRectCircle(x, y, cRaquete, aRaquete, xBolinha, yBolinha, raio);
    if (colidiu) {
        velocidadexBolinha *= -1;
      raquetada.play();
    }
}


// Funcoes do oponente 

function movimentaOponente(){
  if (keyIsDown (87)){
    yOponente -= 10;
  } 
  if (keyIsDown (83)){
    yOponente += 10;
  }
}
 
// funcoes do placar 

function incluiplacar(){
  stroke(255);
  textSize(16);
  textAlign(CENTER);
  fill(color(255,20,147));
  rect (150, 10, 40, 20);
  fill (255)
  text(meuspontos, 170, 26)
  fill(color(255,20,147));
  rect (450, 10, 40, 20);
  fill (255)
  text(pontosOponente, 470, 26)
}

function marcarpontos(){
if (xBolinha > 590){ 
  meuspontos += 1;
  ponto.play();
}
  if (xBolinha < 10){
    pontosOponente += 1
    ponto.play();
  }
}

//funcoes sons 

function preload() {
    trilha = loadSound("trilha.mp3");
    ponto = loadSound("ponto.mp3");
    raquetada = loadSound("raquetada.mp3");
}
