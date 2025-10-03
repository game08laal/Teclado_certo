<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>MathMota</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="https://cdn.socket.io/4.5.4/socket.io.min.js"></script>
  <script src="https://unpkg.com/@lottiefiles/dotlottie-wc" type="module"></script>

   <!-- Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.2/dist/confetti.browser.min.js"></script>
  <style>
    #loadingScreen {
  display: none; /* fica oculto por padrão */
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  background: rgba(0,0,0,0.7); /* fundo escuro semi-transparente */
}

#loadingScreen.active {
  display: flex;
}

.loading-wrapper h1 {
  color: white;
  font-size: 2em;
  font-family: sans-serif;
  text-align: center;
}

/* Pontinhos animados */
.dots {
  display: inline-block;
  position: relative;
  width: 60px;
  height: 12px;
  margin-left: 10px;
}

.dot {
  position: absolute;
  width: 10px;
  height: 10px;
  background: #fff;
  border-radius: 50%;
  animation: move 1.5s infinite ease-in-out;
}

.dot:nth-child(1) { left: 0;   animation-delay: 0s; }
.dot:nth-child(2) { left: 20px; animation-delay: 0.2s; }
.dot:nth-child(3) { left: 40px; animation-delay: 0.4s; }

@keyframes move {
  0%   { transform: translateY(0); opacity: 0.5; }
  25%  { transform: translateY(-10px); opacity: 1; }
  50%  { transform: translateY(0); opacity: 0.5; }
  75%  { transform: translateY(10px); opacity: 1; }
  100% { transform: translateY(0); opacity: 0.5; }
}

    /* Tela de parabéns */
#rewardScreen {
  background: #FFD700; /* amarelo ouro no fundo */
  color: #000; /* texto preto para contraste */
}

/* Caixa do texto */
#rewardScreen .caixa {
  background: #FFF8B0; /* amarelo clarinho */
  padding: 20px;        /* menos espaçamento interno */
  border-radius: 20px; 
  box-shadow: 0px 4px 10px rgba(0,0,0,0.2);
  max-width: 5000px;     /* menor largura */
  margin: 400px auto 0; /* centraliza horizontalmente e empurra pra baixo */
  text-align: center;   /* mantém o texto centralizado */
}
.dots {
  display: inline-block;
  margin-left: 10px;
  position: relative;
  width: 60px; /* espaço para o movimento */
  height: 12px;
}

.dot {
  position: absolute;
  width: 10px;
  height: 10px;
  background: #fff;
  border-radius: 50%;
  animation: move 1.5s infinite ease-in-out;
}

.dot:nth-child(1) { left: 0;   animation-delay: 0s; }
.dot:nth-child(2) { left: 20px; animation-delay: 0.2s; }
.dot:nth-child(3) { left: 40px; animation-delay: 0.4s; }

@keyframes move {
  0%   { transform: translateX(0); opacity: 0.5; }
  25%  { transform: translateX(10px); opacity: 1; }
  50%  { transform: translateX(0); opacity: 0.5; }
  75%  { transform: translateX(-10px); opacity: 1; }
  100% { transform: translateX(0); opacity: 0.5; }
}
.btn-aluno {
  background-color: #4CAF50; /* verde chamativo */
  color: white;
  font-size: 1.9em;
  padding: 30px 60px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  margin: 15px;
  transition: 0.3s;
}
.btn-aluno:hover {
  background-color: #45a049;
  transform: scale(1.05);
}

/* Botão do Professor - singelo */
.btn-professor {
  background-color: transparent;
  color: #f7f6f6;
  font-size: 1.2em;
  border: none;
  cursor: pointer;
  margin: 10px;
}
.btn-professor:hover {
  text-decoration: underline;
}

.btn-entrar {
  background-color: #4CAF50; /* verde chamativo */
  color: white;
  font-size: 1.2em;
  padding: 12px 25px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  margin-right: 10px;
  transition: 0.3s;
}
.btn-entrar:hover {
  background-color: #45a049;
  transform: scale(1.05);
}

.btn-cancelar {
  background-color: #e74c3c; /* vermelho */
  color: white;
  font-size: 1.2em;
  padding: 12px 25px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.3s;
}
.btn-cancelar:hover {
  background-color: #c0392b;
  transform: scale(1.05);
}

.anos-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  margin: 20px 0;
}

.anos-container button {
  background-color: #3498db; /* azul */
  color: white;
  font-size: 1.3em;
  padding: 20px 40px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  transition: 0.3s;
}

.anos-container button:hover {
  background-color: #2980b9;
  transform: scale(1.05);
}


    body {
      margin: 0;
      font-family: Arial, sans-serif;
      text-align: center;
      background: linear-gradient(135deg, #6a11cb, #2575fc);
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      height: 100vh;
      overflow: hidden;
    }

    .keyboard-open {
  margin-bottom: 300px; /* ou a altura aproximada do teclado */
  transition: margin-bottom 0.3s;
}

     
   h1, h2 { 
  margin-bottom: 20px; 
}
.screen {
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  animation: fadeIn 0.5s;
}

/* Estilo específico para a pergunta */
#pergunta {
  font-size: 2.5em; /* aumenta apenas o texto da pergunta */
  text-align: center;
  margin: 20px;
  line-height: 1.3;
}
    .active { display: flex; }
    input, select, button {
      font-size: 1.2em;
      padding: 10px;
      margin: 10px;
      border-radius: 8px;
      border: none;
    }
    .options button {
  padding: 40px 0;        /* altura maior do botão */
  font-size: 2.5em;       /* aumenta o tamanho do texto/número */
  border-radius: 20px;
  cursor: pointer;
  width: 100%;             /* ocupa toda a coluna da grid */
  max-width: 400px;        /* não fica maior que 400px */
  transition: background 0.3s;
  color: #fff;
}
    .options button:hover, .options button:active { background: #2ecc71; }
    .selected { background: #e006a2 !important; }
    #timer { font-size: 2.5em; margin: 20px; }
    
   #grafico {
  max-width: 400px;
  max-height: 400px;
  background: #fff;
  border-radius: 10px;
  padding: 10px;
}
  .progresso {
  text-align: center;           /* centraliza o texto */
  color: gold;                  /* dourado */
  font-size: 1.8em;             /* aumenta o tamanho */
  font-weight: bold;            /* deixa destacado */
  text-shadow: 2px 2px 5px rgba(0,0,0,0.5); /* sombra para destacar */
  margin-bottom: 15px;
}

    .opcao-vermelho { background: #e74c3c; }
    .opcao-azul    { background: #3498db; }
    .opcao-amarelo { background: #f1c40f; color: #000; }
    .opcao-verde   { background: #2ecc71; }
    .correta { background: #35ba6c !important; color: #fff !important; }
    .errada  { background: #c0392b !important; color: #fff !important; }
    .options {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      width: 90%;
      max-width: 600px;
    }
    .options button {
  padding: 50px;     /* aumenta o tamanho do botão */
  font-size: 2.5em;  /* deixa os números maiores */
  border-radius: 20px;
  cursor: pointer;
    }
    .desativado { background: #aec0c2 !important; color: #010101 !important; }
 
    .menu-buttons {
  display: flex;
  flex-direction: column;
  gap: 20px;
  align-items: center;
  margin-top: 40px;
}

/* Botão do JOGO em destaque */
.btn-jogo {
  padding: 20px 50px;
  font-size: 1.8em;
  border-radius: 15px;
  background: linear-gradient(135deg, #4CAF50, #2E7D32);
  color: white;
  border: none;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
}

.btn-jogo:hover {
  transform: scale(1.08);
  box-shadow: 0 6px 16px rgba(0,0,0,0.4);
}

/* Botão do PROFESSOR mais discreto */
.btn-professor {
  padding: 12px 30px;
  font-size: 1.2em;
  border-radius: 10px;
  background: rgba(255,255,255,0.2);
  color: white;
  border: 1px solid rgba(255,255,255,0.4);
  cursor: pointer;
  transition: transform 0.2s, background 0.2s;
}

.btn-professor:hover {
  background: rgba(255,255,255,0.35);
  transform: scale(1.05);
}
#screen1 {
  background: linear-gradient(135deg, #6a11cb, #2575fc);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

/* Cabeça do robô */
.robo {
  width: 60vw;
  height: 70vh;
  background: #0b3d91; /* azul escuro */
  border-radius: 200px; /* quase oval */
  position: relative;
  box-shadow: 0 8px 25px rgba(0,0,0,0.3);
  animation: flutuar 2s ease-in-out infinite; /* movimento mais rápido */
}

@keyframes flutuar {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); } /* sobe um pouco mais */
}

/* olhos */
.olho {
  width: 22vh;   /* olhos maiores */
  height: 22vh;
  background: #87cefa; /* azul claro */
  border-radius: 50%;
  position: absolute;
  top: 23%;
  animation: piscar 3s infinite; /* piscar mais rápido */
}
.olho.esq { left: 17%; }
.olho.dir { right: 17%; }

@keyframes piscar {
  0%, 90%, 100% { transform: scaleY(1); }
  95% { transform: scaleY(0.1); }
}

/* sorriso preenchido */
.boca {
  width: 160px;
  height: 80px;
  background: #87cefa; /* azul claro */
  border-radius: 0 0 120px 120px; /* curva suave */
  position: absolute;
  bottom: 18%;
  left: 50%;
  transform: translateX(-50%);
}

/* Robô só na tela de acerto */
#feedbackScreen .acerto {
  width: 60vw;
  height: 70vh;
  background: #064d00; /* verde escuro */
  border-radius: 200px;
  position: relative;
  box-shadow: 0 8px 25px rgba(0,0,0,0.3);
  animation: flutuar 2s ease-in-out infinite, concordar 2.5s ease-in-out infinite;
}

/* Olhos do robô */
#feedbackScreen .acerto .olho {
  width: 22vh;
  height: 22vh;
  background: #7CFC00; /* verde claro */
  border-radius: 50%;
  position: absolute;
  top: 23%;
  animation: piscar 3s infinite, fecharOlhos 2.5s ease-in-out infinite;
}
#feedbackScreen .acerto .olho.esq { left: 17%; }
#feedbackScreen .acerto .olho.dir { right: 17%; }

/* Boca do robô */
#feedbackScreen .acerto .boca {
  width: 180px;
  height: 90px;
  background: #7CFC00;
  border-radius: 0 0 120px 120px;
  position: absolute;
  bottom: 18%;
  left: 50%;
  transform: translateX(-50%);
}

/* Animações */
@keyframes flutuar {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-4px); }
}

@keyframes concordar {
  0%, 5%   { transform: translateY(0); }
  10%      { transform: translateY(-15px); }
  15%      { transform: translateY(15px); }
  20%      { transform: translateY(-15px); }
  25%      { transform: translateY(0); }
  50%      { transform: translateY(0); }
  55%      { transform: translateY(-15px); }
  60%      { transform: translateY(15px); }
  65%      { transform: translateY(-15px); }
  70%      { transform: translateY(0); }
  100%     { transform: translateY(0); }
}

@keyframes fecharOlhos {
  0%, 5%   { transform: scaleY(1); }
  10%, 20% { transform: scaleY(0.6); }
  25%      { transform: scaleY(1); }
  55%, 65% { transform: scaleY(0.6); }
  70%      { transform: scaleY(1); }
  100%     { transform: scaleY(1); }
}

@keyframes piscar {
  0%, 90%, 100% { transform: scaleY(1); }
  95% { transform: scaleY(0.1); }
}


/* 1. ESTILIZAÇÃO DO ROBO (CONTINUA EM COLUNA) */
#feedbackScreen .erro .robo {
  width: 60vw;
  height: 70vh;
  background: #cc0000;
  border-radius: 200px;
  position: relative;
  box-shadow: 0 8px 25px rgba(0,0,0,0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/* Olhos do robô na tela de erro */
#feedbackScreen .erro .olho {
  width: 22vh;
  height: 22vh;
  background: #e07f72; /* vermelho */
  border-radius: 50%;
  animation: piscar 3s infinite; /* mantém o piscar */
}

#feedbackScreen .erro .olho.esq { margin-right: 5%; }
#feedbackScreen .erro .olho.dir { margin-left: 5%; }

#feedbackScreen .erro .boca {
  width: 180px;
  height: 90px;
  background: #e07f72;
  border-radius: 120px 120px 0 0; /* curva para baixo */
  position: absolute;
  top: 65%;      /* posiciona abaixo dos olhos */
  left: 50%;
  transform: translateX(-50%); /* centraliza horizontalmente */
}



    #pinKeyboard {
  display: none; /* começa oculto */
}
  /* Teclado Virtual - mais harmonioso com a tela do aluno */
#keyboard {
  display: none;
  padding: 5px;
  background: rgba(255,255,255,0.1); /* mais transparente */
  border-radius: 15px;
  position: fixed;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  flex-direction: column;
  gap: 5px;
  z-index: 1000;
  box-shadow: 0 6px 20px rgba(0,0,0,0.3);
}

/* Linhas de teclas */
#keyboard .row {
  display: flex;
  justify-content: center;
  gap: 5px;
}

/* Teclas */
#keyboard .key {
  padding: 10px 12px;
  font-size: 1.2em;
  border-radius: 8px;
  background: rgba(255,255,255,0.2); /* leve transparência para combinar */
  border: 1px solid rgba(255,255,255,0.3);
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.2s, background 0.2s;
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}

/* Hover das teclas */
#keyboard .key:hover {
  transform: scale(1.08);
  background: rgba(255,255,255,0.35);
}

/* Tecla larga (espaço ou backspace) */
.key-wide {
  flex: 1;
  text-align: center;
  background: rgba(255,255,255,0.25);
  color: #fff;
  font-weight: bold;
}

/* Opcional: cores mais suaves para alternar */
#keyboard .key:nth-child(odd) {
  background: rgba(255,255,255,0.25);
}
#keyboard .key:nth-child(even) {
  background: rgba(255,255,255,0.15);
}

/* Hover divertido */
#keyboard .key:hover {
  transform: scale(1.15);
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
}

/* Barra de espaço colorida */
.key-wide[data-action="space"] {
  background: #adf10f !important; /* amarelo */
  color: #000;
}


/* Teclado PIN */
#pinKeyboard {
  display: none; /* só mostra quando abrir */
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
}

.pin-row {
  display: flex;
  gap: 12px;
}

.pin-key {
  width: 70px;
  height: 70px;
  font-size: 1.5em;
  border-radius: 12px;
  background: rgba(255,255,255,0.2);
  border: 1px solid rgba(255,255,255,0.4);
  color: #fff;
  cursor: pointer;
  transition: transform 0.2s, background 0.2s;
}

.pin-key:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.35);
}


/* Linhas do teclado */
#keyboard .row {
    display: flex;
    justify-content: center; /* centraliza as teclas */
    gap: 8px;
}

/* Teclas */
#keyboard .key {
    padding: 20px 25px;
    font-size: 1.8em;
    border-radius: 12px;
    background: rgba(255,255,255,0.15); /* leve transparência */
    border: 1px solid rgba(255,255,255,0.3);
    color: #fff;
    cursor: pointer;
    transition: transform 0.2s, background 0.2s;
}

#keyboard .key:hover {
    transform: scale(1.1);
    background: rgba(255,255,255,0.3);
}

.key-wide {
    flex: 1;
    text-align: center;
}


    @keyframes fadeIn { from {opacity:0} to {opacity:1} }
  </style>
</head>
<body>

<!-- Tela 1 -->
<div class="screen active" id="screen1">
 <div class="robo">
    <div class="olho esq"></div>
    <div class="olho dir"></div>
    <div class="boca"></div>
  </div>
  </div>
<!-- Tela 1.5: Menu -->
<div class="screen" id="menuScreen">
  <h1>Bem-vindo ao MathMota</h1>
  <div class="menu-buttons">
    <button class="btn-jogo" onclick="trocarTela('screen2')">🎮 Iniciar Jogo</button>
    <button class="btn-professor" onclick="trocarTela('screenSenha')">👨‍🏫 Professor</button>
  </div>
</div>

 <script>
  const tela1 = document.getElementById("screen1");

  tela1.addEventListener("click", () => {
  socket.emit('reset');
    trocarTela("menuScreen");
  });

  function irProfessor() {
    // aqui você redireciona para a tela da senha do professor
    trocarTela("screenSenha"); 
  }
</script>
</div>
<!-- Tela de senha -->
<div class="screen" id="screenSenha">
  <h1>Área do Orientador</h1>
  <p>Digite a senha para acessar os participantes</p>
  <input type="password" id="senhaProfessor" placeholder="Senha" readonly 
         style="font-size:2em; text-align:center; width:150px; margin-bottom:20px;">
  
  <!-- Teclado PIN -->
  <div id="pinKeyboard">
    <div class="pin-row">
      <button class="pin-key">1</button>
      <button class="pin-key">2</button>
      <button class="pin-key">3</button>
    </div>
    <div class="pin-row">
      <button class="pin-key">4</button>
      <button class="pin-key">5</button>
      <button class="pin-key">6</button>
    </div>
    <div class="pin-row">
      <button class="pin-key">7</button>
      <button class="pin-key">8</button>
      <button class="pin-key">9</button>
    </div>
    <div class="pin-row">
      <button class="pin-key" data-action="clear">🗑</button>
      <button class="pin-key">0</button>
      <button class="pin-key" data-action="backspace">⌫</button>
    </div>

    <!-- Botões de ação -->
    <div style="margin-top:15px; display:flex; gap:10px;">
      <button class="btn-entrar" onclick="entrarProfessor()">Entrar</button>
      <button class="btn-cancelar" onclick="trocarTela('menuScreen')">Cancelar</button>
    </div>
  </div>
</div>



 <div class="screen" id="participantes"> </div>

<!-- Tela de seleção de ano (terceira tela do professor) -->
<div class="screen" id="screenProfessor">
  <h1>Selecione o ano do aluno</h1>
  <div class="options">
    <button onclick="selecionarAnoProfessor('3º ano')">3º ano</button>
    <button onclick="selecionarAnoProfessor('4º ano')">4º ano</button>
    <button onclick="selecionarAnoProfessor('5º ano')">5º ano</button>
    <button onclick="selecionarAnoProfessor('6º ano')">6º ano</button>
    <button onclick="selecionarAnoProfessor('2º ano técnico')">2º ano técnico</button>
  </div>
  <button class="btn-cancelar" onclick="trocarTela('menuScreen')">Voltar</button>
</div>

<div class="screen" id="screenJogador" style="display:none;">
  <button onclick="voltarParticipantes()">← Voltar</button>
  <h1 id="tituloJogador"></h1>
  <p id="dadosJogador"></p>
</div>
<script>function abrirTelaJogador(jogador) {
    // Esconde lista de participantes
    document.getElementById('screenParticipantes').style.display = 'none';

    // Mostra tela do jogador
    const tela = document.getElementById('screenJogador');
    tela.style.display = 'block';

    // Preenche dados
    document.getElementById('tituloJogador').textContent = jogador.nome;
    document.getElementById('dadosJogador').textContent = 
        `Ano: ${jogador.ano || "Não informado"} | ID: ${jogador.id || "N/A"}`;
}

function voltarParticipantes() {
    trocarTela('screenParticipantes');
}

</script>
<script>
function selecionarAnoProfessor(ano) {
    trocarTela('screenParticipantes');

    // Atualiza o título
    document.getElementById('tituloParticipantes').textContent = `Alunos do ${ano}`;

    // Busca participantes do ano selecionado
    fetch(`/participantes/${encodeURIComponent(ano)}`)
        .then(res => res.json())
        .then(data => {
            const lista = document.getElementById('listaParticipantesAno');
            lista.innerHTML = '';
            if (data.length === 0) {
                lista.innerHTML = "<p>Nenhum participante encontrado.</p>";
            } else {
                const ul = document.createElement('ul');
                data.forEach(jogador => {
    const button = document.createElement('button');
    button.textContent = jogador.nome;
    button.style.margin = "10px";
    button.style.padding = "15px 25px";
    button.style.fontSize = "1.2em";
    button.style.borderRadius = "10px";
    button.style.cursor = "pointer";

    // Quando clicar no botão, abre a tela do jogador
     button.addEventListener("click", () => {
        window.location.href = `/relatorio/${jogador.id}`;
    });

    ul.appendChild(button);
});
                lista.appendChild(ul);
            }
        })
        .catch(err => console.error("Erro ao buscar participantes:", err));
}
function voltarTelaAno() {
    trocarTela("screenProfessor");
}





</script>

<div class="screen" id="screenParticipantes" style="display:none;">
  <button onclick="voltarTelaAno()">← Voltar</button>
  <h1 id="tituloParticipantes"></h1>
  <div id="listaParticipantesAno"></div> <!-- ID único -->
</div>


  
<!-- Tela 2: Nome e Ano -->
<div class="screen" id="screen2">
  <h1>Digite seu nome e selecione o ano escolar</h1>
  <input type="text" id="nome" placeholder="Seu nome" readonly>
  <select id="ano">
    <option value="">Escolha o ano</option>
    <option value="3º ano">3º ano</option>
    <option value="4º ano">4º ano</option>
    <option value="5º ano">5º ano</option>
    <option value="6º ano">6º ano</option>
    <option value="2º ano">2º ano técnico</option>
  </select>
  <button onclick="iniciarQuiz();  salvarParticipante()">Continuar</button>
</div>
<script>

    window.jogadorId = null;

    function salvarParticipante() {
    const nome = document.getElementById('nome').value;
    const ano = document.getElementById('ano').value;

    if (!nome || !ano) {
        alert("Digite seu nome e selecione o ano!");
        return;
    }

    fetch('/salvar_jogador', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ nome, ano })
    })
    .then(res => res.json())
    .then(data => {
        console.log("Jogador salvo:", data);
        // Salva o ID do jogador no JS
        window.jogadorId = data.id;

        // Aqui emitimos para o Python que o jogador foi criado
        socket.emit("jogador_salvo", { jogador_id: window.jogadorId, nome, ano });

        // Só agora iniciamos o quiz
        iniciarQuiz();
        reset();
    })
    .catch(err => console.error("Erro ao salvar jogador:", err));
}

</script>
 
<!-- Outras Telas -->
<div class="screen" id="loadingScreen">
  <div class="loading-wrapper">
    <h1>
      Preparando para as perguntas
      <span class="dots">
        <span class="dot"></span>
        <span class="dot"></span>
        <span class="dot"></span>
      </span>
    </h1>
  </div>
  </div>

<div class = "screen" id="questionScreen">
<h3 id="progressoPergunta"></h3>
  <h2 id="pergunta"></h2>
  <div class="options">
    <button onclick="responder(0)" id="opt0" class="opcao-vermelho"></button>
    <button onclick="responder(1)" id="opt1" class="opcao-azul"></button>
    <button onclick="responder(2)" id="opt2" class="opcao-amarelo"></button>
    <button onclick="responder(3)" id="opt3" class="opcao-verde"></button>
  </div>
  

  <!-- Barra de tempo rosa -->
  <div id="timerBar" style="width: 80%; height: 20px; background: #ddd; border-radius: 15px; margin: 20px auto;">
    <div id="preenchimentoBarra" style="width: 100%; height: 100%; background: #ff69b4; border-radius: 15px;"></div>
  </div>
  </div>
  



<div class="screen" id="feedbackScreen">
  <h1 id="feedbackMsg"></h1>
   <div id="imgErro" class="erro">
  <div class="robo">
    <div class="olhos-container">
      <div class="olho esq" id="olhoEsq"></div>
      <div class="olho dir" id="olhoDir"></div>
    </div>
    <div class="boca"></div>
  </div>
</div>


   <div id="imgAcerto" class="acerto">
   <div class="olho esq"></div>
   <div class="olho dir"></div> 
   <div class="boca"></div> 
   </div>
   </div>

   <script>
  const feedbackScreen = document.getElementById('feedbackScreen');

// Adiciona o listener
feedbackScreen.addEventListener('click', () => {
  proximaPergunta();
});
</script>

</div>
<div class="screen" id="reportScreen">
  <h2 id="resumo"></h2>
  <canvas id="grafico"></canvas>
  <button id="btnSurpresa" onclick="mostrarRecompensa()">Ver Surpresa</button>
  <button id="btnReiniciar" onclick="reiniciarJogo()" style="display:none;">🔄 Iniciar Novamente</button>
</div>
<div class="screen" id="rewardScreen">
  <div class="caixa">
    <h1>Parabéns, <span id="userName"></span>! 🎉</h1>
    <p>Você acertou tudinho! Aqui está sua surpresa: 🎁</p>
     <button id="btnReiniciarReward" class="btn-jogo" onclick="reiniciarJogo()">🔄 Iniciar Novamente</button>
  </div>
</div>

<div id="keyboard">
    <div class="row">
      <span class="key">Q</span><span class="key">W</span><span class="key">E</span><span class="key">R</span><span class="key">T</span>
      <span class="key">Y</span><span class="key">U</span><span class="key">I</span><span class="key">O</span><span class="key">P</span>
    </div>
    <div class="row">
      <span class="key">A</span><span class="key">S</span><span class="key">D</span><span class="key">F</span><span class="key">G</span>
      <span class="key">H</span><span class="key">J</span><span class="key">K</span><span class="key">L</span>
    </div>
    <div class="row">
      <span class="key">Z</span><span class="key">X</span><span class="key">C</span><span class="key">V</span><span class="key">B</span>
      <span class="key">N</span><span class="key">M</span>
      <span class="key key-wide" data-action="backspace">⌫</span>
    </div>
    <div class="row">
      <span class="key key-wide" data-action="space">Espaço</span>
    </div>
  </div>


<script>
  const perguntas3 = [
    { q: "5 + 7 = ?", options: ["10", "12", "13", "14"], correct: 1, category: "Soma"},
    { q: "15 - 8 = ?", options: ["6", "7", "8", "5"], correct: 1, category: "Subtração" },
    { q: "9 + 4 = ?", options: ["12", "14", "13", "15"], correct: 2, category: "Soma" },
    { q: "18 - 6 = ?", options: ["12", "11", "10", "13"], correct: 0, category: "Subtração" },
    { q: "7 + 7 = ?", options: ["12", "15", "13", "14"], correct: 3, category: "Soma" },
    { q: "20 - 9 = ?", options: ["10", "12", "11", "9"], correct: 2, category: "Subtração" },
    { q: "6 + 8 = ?", options: ["12", "14", "13", "15"], correct: 1, category: "Soma" },
    { q: "20 - 9 = ?", options: ["10", "12", "11", "9"], correct: 2, category: "Subtração" }
  ];

  const perguntas4 = [
    { q: "6 x 7 = ?", options: ["42", "36", "40", "48"], correct: 0, category: "Multiplicação" },
    { q: "56 ÷ 8 = ?", options: ["6", "8", "7", "9"], correct: 2, category: "Divisão" },
    { q: "9 x 5 = ?", options: ["45", "40", "35", "50"], correct: 0, category: "Multiplicação" },
    { q: "72 ÷ 9 = ?", options: ["6", "9", "8", "7"], correct: 2, category: "Divisão" },
    { q: "8 x 8 = ?", options: ["64", "72", "56", "60"], correct: 0, category: "Multiplicação" },
    { q: "63 ÷ 7 = ?", options: ["8", "9", "7", "10"], correct: 1, category: "Divisão" },
    { q: "12 x 4 = ?", options: ["48", "36", "40", "44"], correct: 0, category: "Multiplicação" },
    { q: "63 ÷ 7 = ?", options: ["8", "9", "7", "10"], correct: 1, category: "Divisão" }
  ];

  const perguntas5 = [
    { q: "João comprou 3 cadernos por R$12 cada. Quanto gastou?", options: ["R$36", "R$30", "R$24", "R$40"], correct: 0, category: "Multiplicação" },
    { q: "Um ônibus transporta 45 pessoas. Quantas pessoas em 6 ônibus?", options: ["270", "300", "280", "250"], correct: 0, category: "Multiplicação" },
    { q: "Se uma pizza custa R$48 e é dividida em 8 fatias, quanto custa cada fatia?", options: ["R$6", "R$8", "R$5", "R$7"], correct: 0, category: "Divisão" },
    { q: "Um aluno leu 120 páginas em 4 dias. Quantas páginas por dia?", options: ["25", "30", "40", "35"], correct: 1, category: "Divisão" },
    { q: "Se 5 caixas têm 125 balas no total, quantas balas em cada caixa?", options: ["30", "20", "25", "15"], correct: 2, category: "Divisão" },
    { q: "Um produto de R$200 teve desconto de R$50. Quanto custa agora?", options: ["R$150", "R$160", "R$140", "R$130"], correct: 0, category: "Multiplicação" },
    { q: "Qual o resultado de 120 ÷ 5?", options: ["25", "24", "22", "20"], correct: 1, category: "Divisão"},
    { q: "João comprou 3 cadernos por R$12 cada. Quanto gastou?", options: ["R$36", "R$30", "R$24", "R$40"], correct: 0, category: "Multiplicação" }
  ];

  const perguntas6 = [
    { q: "Qual é 1/2 de 3/4?", options: ["3/8", "3/4", "2/4", "1/8"], correct: 0, category: "Fração" },
    { q: "Resolva: 2x = 10. Quanto vale x?", options: ["4", "5", "10", "2"], correct: 1, category: "Equação" },
    { q: "Quanto é 3/5 + 1/5?", options: ["4/5", "3/10", "5/10", "5/5"], correct: 0, category: "Fração" },
    { q: "Resolva: 12 ÷ (3 + 1)", options: ["3", "4", "2", "6"], correct: 0, category: "Equação" },
    { q: "Qual fração representa metade?", options: ["1/4", "1/2", "2/4", "2/3"], correct: 1, category: "Fração" },
    { q: "Resolva: x + 7 = 12", options: ["4", "5", "6", "3"], correct: 1, category: "Equação" },
    { q: "Se uma barra de chocolate tem 12 pedaços e você come 3, qual fração foi comida?", options: ["1/4", "1/2", "1/3", "1/6"], correct: 0, category: "Fração" },
    { q: "Resolva: 2x = 10. Quanto vale x?", options: ["4", "5", "10", "2"], correct: 1, category: "Equação" }
  ];

 const perguntas2 = [
  { q: "Quanto vale cos(0°)?", options: ["0", "1/2", "90", "1"], correct: 3, category: "Trigonometria" },
  { q: "Qual é a soma dos ângulos internos de um quadrilátero?", options: ["180°", "270°", "360°", "540°"], correct: 2, category: "Polígonos" },
  { q: "Quanto vale sin(30°)?", options: ["0", "1/2", "1", "30"], correct: 1, category: "Trigonometria" },
  { q: "Um hexágono regular tem todos os ângulos iguais. Qual é a medida de cada ângulo interno?", options: ["100°", "120°", "135°", "140°"], correct: 1, category: "Polígonos" },
  { q: "Quanto vale sin(0°)?", options: ["1/2", "0", "1", "3/4"], correct: 1, category: "Trigonometria" },
  { q: "Quantos diagonais tem um pentágono?", options: ["31", "5", "70", "1"], correct: 1, category: "Polígonos" },
  { q: "Se cos(θ) = 1/2 e θ está no primeiro quadrante, qual é o valor de θ?", options: ["30°", "45°", "60°", "90°"], correct: 0, category: "Trigonometria" },
  { q: "Seja um triângulo retângulo em que um dos ângulos agudos mede 30° e a hipotenusa mede 10. Qual é o valor do cateto oposto a esse ângulo de 30°?", options: ["3", "4", "5", "6"], correct: 2, category: "Trigonometria" }
];


  let perguntas = []; 
  let resultados = [];
  let nome = "";
  let ano = "";
  let indice = 0;
  let acertos = 0;
  let tempo = 10;
  let timerInterval = null; 

  const socket = io('http://localhost:5001');
  
 const input = document.getElementById("nome");
const keyboard = document.getElementById("keyboard");
const screen2 = document.getElementById("screen2");

input.addEventListener("click", (e) => {
  e.stopPropagation();
  if (screen2.classList.contains("active")) {
    keyboard.style.display = "flex"; // mostra teclado do aluno
    screen2.classList.add("keyboard-open"); // empurra conteúdo pra cima
  }
});

document.addEventListener("click", () => {
  keyboard.style.display = "none";
  screen2.classList.remove("keyboard-open"); // volta ao normal
});


keyboard.addEventListener("click", (e) => e.stopPropagation());

document.addEventListener("click", () => {
  keyboard.style.display = "none";
});

document.querySelectorAll(".key").forEach(key => {
  key.addEventListener("click", () => {
    const action = key.dataset.action;
    if (action === "backspace") input.value = input.value.slice(0, -1);
    else if (action === "space") input.value += " ";
    else input.value += key.textContent;
  });
});


// --- Teclado do professor (PINKeyboard) ---
const inputSenha = document.getElementById("senhaProfessor");
const pinKeyboard = document.getElementById("pinKeyboard");

// Mostra teclado PIN ao clicar no input de senha
inputSenha.addEventListener("click", (e) => {
  e.stopPropagation();
  pinKeyboard.style.display = "flex";
});

// Evita fechar teclado ao clicar dentro dele
pinKeyboard.addEventListener("click", (e) => e.stopPropagation());

// Fecha teclado ao clicar fora
document.addEventListener("click", () => {
  pinKeyboard.style.display = "none";
});

// Função para preencher input com PIN
pinKeyboard.querySelectorAll(".pin-key").forEach(key => {
  key.addEventListener("click", () => {
    const action = key.dataset.action;
    if (action === "backspace") inputSenha.value = inputSenha.value.slice(0,-1);
    else if (action === "clear") inputSenha.value = "";
    else inputSenha.value += key.textContent;
  });
});




function mostrarTela2() {
    trocarTela('screen2'); // usa a função centralizada que oculta todas as telas
}


  function entrarProfessor() {
    const senha = document.getElementById('senhaProfessor').value;
    const senhaCorreta = "123"; // coloque a senha que quiser

    if(senha === senhaCorreta){
      console.log("senha correta");
        // aqui você pode mostrar a próxima tela do professor
        trocarTela('screenProfessor');
    } else {
        alert("Senha incorreta!");
    }
}



  function iniciarQuiz() {
    nome = document.getElementById('nome').value;
    ano = document.getElementById('ano').value;
    
    if (!nome || !ano) return alert("Preencha tudo!");

    if (ano === "3º ano") perguntas = perguntas3;
    if (ano === "4º ano") perguntas = perguntas4;
    if (ano === "5º ano") perguntas = perguntas5;
    if (ano === "6º ano") perguntas = perguntas6;
    if (ano === "2º ano técnico") perguntas = perguntas2;
    
    socket.emit("novo_jogador", { nome: nome, ano: ano });

    trocarTela('loadingScreen');
    setTimeout(() => {
      indice = 0;
      acertos = 0;
      mostrarPergunta();
    }, 2000);
  }

 function mostrarPergunta() {
  trocarTela('questionScreen');
  const p = perguntas[indice];
  document.getElementById('progressoPergunta').textContent = 
      `Pergunta ${indice + 1} de ${perguntas.length}`;
  document.getElementById('pergunta').textContent = p.q;

  p.options.forEach((op, i) => {
    const botao = document.getElementById(`opt${i}`);
    botao.textContent = op;
    botao.classList.remove('correta', 'errada', 'desativado');

    if (i === 0) botao.className = 'opcao-vermelho';
    if (i === 1) botao.className = 'opcao-azul';
    if (i === 2) botao.className = 'opcao-amarelo';
    if (i === 3) botao.className = 'opcao-verde';
  });

  // ===== Inicializa a barra =====
  clearInterval(timerInterval);
  let tempoTotal = 10000;          
  let tempoRestante = tempoTotal;
  let barra = document.getElementById('preenchimentoBarra');
  barra.style.width = '100%'; // começa cheia

  timerInterval = setInterval(() => {
    tempoRestante -= 20;
    if (tempoRestante < 0) tempoRestante = 0;

    let porcentagem = (tempoRestante / tempoTotal) * 100;
    barra.style.width = porcentagem + '%';

    // Gradiente verde -> amarelo -> vermelho
    let r, g, b;
    if (porcentagem > 50) {
      let t = (100 - porcentagem) / 50;
      r = Math.round(46 + t * (241 - 46));
      g = Math.round(204 + t * (196 - 204));
      b = Math.round(113 + t * (15 - 113));
    } else {
      let t = (50 - porcentagem) / 50;
      r = Math.round(241 + t * (231 - 241));
      g = Math.round(196 + t * (76 - 196));
      b = Math.round(15 + t * (60 - 15));
    }
    barra.style.background = `rgb(${r},${g},${b})`;

    if (tempoRestante <= 0) {
      clearInterval(timerInterval);
      verificarResposta(-1);
    }
  }, 20);
}

function trocarTela(id) {
  // Esconde todas as telas
  document.querySelectorAll('.screen').forEach(s => {
    s.classList.remove('active');
    s.style.display = "none";
  });

  // Mostra apenas a escolhida
  const tela = document.getElementById(id);
  if (tela) {
    tela.classList.add('active');
    tela.style.display = "flex"; // ou "block", depende do seu layout
  }

  // Sempre esconder os teclados ao trocar de tela
  document.getElementById("keyboard").style.display = "none";
  document.getElementById("pinKeyboard").style.display = "none";

  // 🔹 Se voltou para o menu ou tela inicial, limpar a senha do professor
  if (id === "menuScreen" || id === "screen1") {
    const senhaInput = document.getElementById("senhaProfessor");
    if (senhaInput) senhaInput.value = "";
  }
}


/*
 function trocarTela(id) {
  // Esconde todas as telas
  document.querySelectorAll('.screen').forEach(s => {
    s.classList.remove('active');
    s.style.display = "none";
  });

  // Mostra apenas a escolhida
  const tela = document.getElementById(id);
  if (tela) {
    tela.classList.add('active');
    tela.style.display = "flex"; // ou "block", depende do seu layout
  }

  // Sempre esconder os teclados ao trocar de tela
  document.getElementById("keyboard").style.display = "none";
  document.getElementById("pinKeyboard").style.display = "none";
}
*/

 
  function verificarResposta(i) {
    const correta = perguntas[indice].correct;
    const botoes = document.querySelectorAll('.options button');

    botoes.forEach(b => {
      b.classList.remove('correta', 'errada', 'desativado');
    });

    resultados.push({ categoria: perguntas[indice].category, acertou: i === correta });

    if (i === correta) {
    acertos++;
    if (window.jogadorId) {
    console.log("certo");
    socket.emit('acertou', { jogador_id: window.jogadorId, categoria: perguntas[indice].category });
}
// 🎉 Dispara o confete
    confetti({
      particleCount: 100,
      spread: 70,
      origin: { y: 0.6 }
    });
      botoes.forEach((b, index) => {
        if (index === correta) {
          b.classList.add('correta');
        } else {
          b.classList.add('desativado');
        }
      });
    } else {
       if (window.jogadorId) {
    socket.emit('errou', { jogador_id: window.jogadorId, categoria: perguntas[indice].category });
}
      botoes.forEach((b, index) => {
        if (index === i) {
          b.classList.add('errada');
        } else if (index === correta) {
          b.classList.add('correta');
        } else {
          b.classList.add('desativado');
        }
      });
    }
     setTimeout(() => {
      if (i === correta) {
        document.getElementById('feedbackMsg').textContent = "Acertou!";
        document.getElementById('imgErro').style.display = 'none';
        document.getElementById('imgAcerto').style.display = 'block';
      } else {
        document.getElementById('imgErro').style.display = "block"; 
        document.getElementById('imgAcerto').style.display = 'none';
        document.getElementById('feedbackMsg').textContent = "Essa foi uma boa tentativa! Vamos tentar de novo?";
      }
      trocarTela('feedbackScreen');
    }, 1000);
  }

  function proximaPergunta() {
    indice++;
    if (indice < perguntas.length) {
      mostrarPergunta();
    } else {
      mostrarRelatorio();
    }
  } function responder(i) {
    clearInterval(timerInterval);
    verificarResposta(i);
  }

 
    socket.on("jogador_salvo", (data) => {
        jogadorId = data.jogador_id;       // atualiza a variável local
  window.jogadorId = data.jogador_id; // opcional: mantém também no window
  console.log("Jogador salvo com ID:", jogadorId);
    });

function mostrarRelatorio() {
  trocarTela('reportScreen');

 const total = resultados.length;
    const acertos = resultados.filter(r => r.acertou).length;
    const erros = total - acertos;

  // Atualizar resumo
  document.getElementById('resumo').textContent =
    `${nome} (${ano}) - Acertos: ${acertos}/${perguntas.length}`;

   

  // Calcular categorias
  const categorias = {};
    resultados.forEach(r => {
        const categoria = r.categoria;
        if (!categorias[categoria]) categorias[categoria] = { total: 0, acertos: 0, erros: 0 };
        categorias[categoria].total++;
        if (r.acertou) categorias[categoria].acertos++;
        else categorias[categoria].erros++;
    });
  // Função para criar painel
  function criarPainel(titulo, cor, dados, tipo) {
    let painel = `<div style="padding:10px;border-radius:20px;width:200px;margin:10px;">
                    <h3 style="margin:0;background-color:${cor};border-radius:15px;padding:5px;text-align:center;color:white;">${titulo}</h3>`;
    for (let cat in dados) {
      let porcento = ((tipo === 'acertos' ? dados[cat].acertos : dados[cat].erros) / dados[cat].total * 100).toFixed(1);
      painel += `<p>${cat}: ${porcento}%</p>`;
    }
    painel += `</div>`;
    return painel;
  }

  const painelAcertos = criarPainel('Acertos', '#3498db', categorias, 'acertos');
  const painelErros = criarPainel('Erros', '#e74c3c', categorias, 'erros');

  // Pior categoria
  let piorCategoria = null;
  let maiorErro = 0;
  for (let cat in categorias) {
    let porcentoErro = (categorias[cat].erros / categorias[cat].total) * 100;
    if (porcentoErro > maiorErro) {
      maiorErro = porcentoErro;
      piorCategoria = cat;
    }
  }

  const painelMelhoria = `<div style="padding:10px;border-radius:20px;width:300px;margin:10px;">
                            <h3 style="margin:0;background-color:#2ecc71;border-radius:15px;padding:5px;text-align:center;color:white;">Pontos de melhoria:</h3>
                            <p>O aluno <b>${nome}</b> apresentou mais dificuldades em <b>${piorCategoria}</b>, 
                            por consequência é indicado prestar apoio e mais atenção em atividades relacionadas a <b>${piorCategoria}</b>.</p>
                          </div>`;

  // Limpar conteúdo anterior e manter canvas e botão
  const report = document.getElementById('reportScreen');
  report.innerHTML = `<h2 id="resumo"></h2>
                      <div id="containerPrincipal" style="display:flex; justify-content:center; align-items:flex-start; gap:40px; margin-top:20px;"></div>
                      <canvas id="grafico"></canvas>
                      <button onclick="mostrarRecompensa()">Ver Surpresa</button>`;

  document.getElementById('resumo').textContent =
    `${nome} (${ano}) - Acertos: ${acertos}/${perguntas.length}`;

    const botao = document.querySelector('#reportScreen button');
    botao.style.display = (acertos >= 6 && acertos <= 8) ? 'inline-block' : 'none';

  // Criar container principal e colunas
  const containerPrincipal = document.getElementById('containerPrincipal');

  // Esquerda: Acertos e Erros empilhados
  const containerEsquerda = document.createElement('div');
  containerEsquerda.style.display = 'flex';
  containerEsquerda.style.flexDirection = 'column';
  containerEsquerda.style.gap = '20px';
  containerEsquerda.innerHTML = painelAcertos + painelErros;

  // Centro: gráfico
  const containerCentral = document.createElement('div');
  containerCentral.style.display = 'flex';
  containerCentral.style.justifyContent = 'center';
  containerCentral.style.alignItems = 'center';
  containerCentral.style.flexDirection = 'column';
  containerCentral.appendChild(document.getElementById('grafico'));

  // Direita: Pontos de melhoria
  const containerDireita = document.createElement('div');
  containerDireita.style.display = 'flex';
  containerDireita.style.flexDirection = 'column';
  containerDireita.style.gap = '20px';
  containerDireita.innerHTML = painelMelhoria;

  // Adicionar colunas ao container principal
  containerPrincipal.appendChild(containerEsquerda);
  containerPrincipal.appendChild(containerCentral);
  containerPrincipal.appendChild(containerDireita);

  // Criar gráfico
  const ctx = document.getElementById('grafico').getContext('2d');
  new Chart(ctx, {
    type: 'pie',
    data: {
      labels: ['Acertos', 'Erros'],
      datasets: [{
        data: [acertos, erros],
        backgroundColor: ['#3498db', '#e74c3c']
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { position: 'bottom' }
      }
    }
  });
  /*
  let btnSurpresa = document.getElementById('btnSurpresa');
    if (!btnSurpresa) {
        btnSurpresa = document.createElement('button');
        btnSurpresa.id = 'btnSurpresa';
        btnSurpresa.textContent = 'Ver Surpresa';
        btnSurpresa.onclick = mostrarRecompensa;
        report.appendChild(btnSurpresa);
    }*/

    let btnReiniciar = document.getElementById('btnReiniciar');
    if (!btnReiniciar) {
        btnReiniciar = document.createElement('button');
        btnReiniciar.id = 'btnReiniciar';
        btnReiniciar.textContent = '🔄 Iniciar Novamente';
        btnReiniciar.onclick = reiniciarJogo;
        report.appendChild(btnReiniciar);
    }

    // Mostrar ou esconder botão surpresa
    btnSurpresa.style.display = (acertos >= 6 && acertos <= 8) ? 'inline-block' : 'none';
    btnReiniciar.style.display = 'inline-block'; // sempre aparece
  }

  // Mostrar botão apenas se acertos >= 6
 /*const botao = document.querySelector('#reportScreen button');
const acertosCount = resultados.filter(r => r.acertou).length;
botao.style.display = (acertosCount >= 6 && acertosCount <= 8) ? 'inline-block' : 'none';
  /*
  resultados.forEach(r => {
            fetch('/salvar_resultado', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    jogador_id: window.jogadorId,  // agora usa a variável global correta
                    categoria: r.categoria,
                    acertou: r.acertou ? 1 : 0
                })
            })
            .then(res => res.json())
            .then(data => console.log("Resultado salvo:", data))
            .catch(err => console.error("Erro ao salvar:", err));
        });
}

*/


  function mostrarRecompensa() {
    const acertosCount = resultados.filter(r => r.acertou).length; // conta acertos
    if (acertosCount >= 6 && acertosCount <= 8) {
        socket.emit('recompensa');
        trocarTela('rewardScreen');
        document.getElementById('userName').textContent = nome;
    } else {
        alert("A recompensa só é liberada para quem acertou entre 6 e 8 questões!");
    }
}

  let jogadorId = null;


 function reiniciarJogo() {
  // Zera ID do jogador
  window.jogadorId = null;

  // Limpa nome e ano
  document.getElementById("nome").value = "";
  document.getElementById("ano").value = "";

  // Zera progresso do quiz
  if (window.resultados) window.resultados = [];
  if (window.perguntaAtual) window.perguntaAtual = 0;
  if (window.pontos) window.pontos = 0;

  // Esconde gráficos, feedback, etc
  const grafico = document.getElementById("grafico");
  if (grafico) grafico.getContext("2d").clearRect(0, 0, grafico.width, grafico.height);

  // Volta para o menu inicial
  trocarTela("menuScreen");
}

function reset() { 
  resultados = [];
   indice = 0;
 }

// Receber ID salvo do servidor
socket.on("jogador_salvo", (data) => {
  jogadorId = data.jogador_id;
  console.log("Jogador salvo com ID:", jogadorId);
});


  socket.on('botao', data => {
    console.log('Evento de botão recebido! Dados:', data);
    const botao = data.botao.replace('BTN','') - 1;
    responder(botao);
  });

</script>
</body>
</html>
