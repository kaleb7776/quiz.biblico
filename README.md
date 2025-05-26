<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Quem Postou Isso? - Quiz Bíblico</title>

  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet" />

  <style>
    :root {
      --color-bg-dark: #0f2027;
      --color-bg-dark2: #203a43;
      --color-bg-dark3: #2c5364;
      --color-primary: #00bcd4;
      --color-primary-dark: #007c91;
      --color-accent: #4caf50;
      --color-error: #f44336;
      --color-text-light: #e0f7fa;
      --color-text-muted: #78909c;
      --color-progress-bg: #004d40;
      --color-progress-fill: #00bcd4;
      --color-shadow: rgba(0, 188, 212, 0.8);

      --font-family: 'Montserrat', sans-serif;
      --border-radius: 12px;
      --transition-speed: 0.3s;
      --btn-padding: 15px;
    }

    /* THEMES */
    body[data-theme='dark'] {
      background: linear-gradient(135deg, var(--color-bg-dark), var(--color-bg-dark2), var(--color-bg-dark3));
      color: var(--color-text-light);
    }

    body[data-theme='light'] {
      background: #f0f4f8;
      color: #333;
    }

    body[data-theme='neon'] {
      background: #000;
      color: #39ff14;
      text-shadow: 0 0 5px #39ff14;
    }

    body[data-theme='pink'] {
      background: #ffe4f0;
      color: #c2185b;
    }

    /* GLOBAL RESET */
    * {
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-family);
      margin: 0;
      padding: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      user-select: none;
      transition: background-color var(--transition-speed), color var(--transition-speed);
    }

    .container {
      background: rgba(10, 25, 35, 0.9);
      padding: 30px 40px;
      border-radius: 20px;
      box-shadow: 0 0 20px var(--color-shadow);
      max-width: 650px;
      width: 100%;
      text-align: center;
      position: relative;
      overflow: hidden;
      color: inherit;
      transition: background-color var(--transition-speed), color var(--transition-speed);
    }

    body[data-theme='light'] .container {
      background: #fff;
      color: #222;
      box-shadow: 0 0 20px #999999aa;
    }

    body[data-theme='neon'] .container {
      background: #111;
      box-shadow: 0 0 30px #39ff14aa;
      color: #39ff14;
    }

    body[data-theme='pink'] .container {
      background: #fff0f6;
      color: #c2185b;
      box-shadow: 0 0 20px #f06292aa;
    }

    h1 {
      font-weight: 700;
      font-size: 2.5rem;
      margin-bottom: 20px;
      letter-spacing: 2px;
      color: var(--color-primary);
      user-select: text;
      transition: color var(--transition-speed);
    }

    body[data-theme='light'] h1 {
      color: #d81b60;
    }

    body[data-theme='neon'] h1 {
      color: #39ff14;
      text-shadow: 0 0 10px #39ff14;
    }

    body[data-theme='pink'] h1 {
      color: #c2185b;
    }

    .progress-bar {
      width: 100%;
      height: 14px;
      background: var(--color-progress-bg);
      border-radius: 7px;
      overflow: hidden;
      margin-bottom: 25px;
      box-shadow: inset 0 0 8px #00796baa;
    }

    .progress-fill {
      height: 100%;
      background: var(--color-progress-fill);
      width: 0%;
      border-radius: 7px;
      transition: width 0.5s ease;
      box-shadow: 0 0 8px var(--color-progress-fill);
    }

    .question {
      font-size: 1.5rem;
      margin-bottom: 25px;
      min-height: 100px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      user-select: text;
    }

    .options {
      display: flex;
      flex-direction: column;
      gap: 15px;
      margin-bottom: 20px;
    }

    button.option-btn {
      background: var(--color-primary-dark);
      border: none;
      padding: var(--btn-padding);
      font-size: 1.1rem;
      border-radius: var(--border-radius);
      cursor: pointer;
      color: var(--color-text-light);
      font-weight: 600;
      box-shadow: 0 5px 10px #004d40aa;
      transition: background-color var(--transition-speed), transform 0.2s, box-shadow var(--transition-speed);
      user-select: none;
      position: relative;
      overflow: hidden;
    }

    button.option-btn:hover:not(:disabled) {
      background-color: var(--color-primary);
      transform: translateY(-4px);
      box-shadow: 0 8px 15px var(--color-shadow);
    }

    button.option-btn:disabled {
      cursor: default;
      background-color: #004d40;
      box-shadow: none;
      color: var(--color-text-muted);
    }

    button.option-btn.correct {
      background-color: var(--color-accent);
      box-shadow: 0 0 12px #4caf5088;
    }

    button.option-btn.incorrect {
      background-color: var(--color-error);
      box-shadow: 0 0 12px #f4433688;
    }

    #resultado {
      font-size: 1.3rem;
      font-weight: 700;
      min-height: 50px;
      letter-spacing: 1.2px;
      margin-bottom: 10px;
      user-select: text;
    }

    .final-message {
      font-size: 1.6rem;
      font-weight: 700;
      color: #00e676;
      margin-top: 20px;
      user-select: text;
      text-shadow: 0 0 5px #00e676aa;
      animation: glow 2s infinite alternate;
    }

    @keyframes glow {
      from {
        text-shadow: 0 0 5px #00e676aa, 0 0 10px #00e676aa;
      }
      to {
        text-shadow: 0 0 20px #00e676ff, 0 0 30px #00e676ff;
      }
    }

    .history {
      margin-top: 20px;
      max-height: 180px;
      overflow-y: auto;
      text-align: left;
      background: rgba(0,0,0,0.2);
      border-radius: 12px;
      padding: 10px;
      font-size: 0.9rem;
      line-height: 1.3;
      user-select: text;
    }

    .history-item.correct {
      color: var(--color-accent);
    }

    .history-item.incorrect {
      color: var(--color-error);
    }

    /* Medalhas */
    .medalhas {
      margin-top: 25px;
      display: flex;
      justify-content: center;
      gap: 25px;
      user-select: none;
    }

    .medalha {
      display: flex;
      flex-direction: column;
      align-items: center;
      font-weight: 700;
      color: #fff;
      text-shadow: 0 0 5px #000;
    }

    .medalha img {
      width: 80px;
      height: 80px;
      margin-bottom: 8px;
      filter: drop-shadow(0 0 4px #000);
      animation: pulse 2.5s infinite alternate;
    }

    @keyframes pulse {
      from {
        transform: scale(1);
      }
      to {
        transform: scale(1.1);
      }
    }

    /* Tema selector */
    .theme-selector {
      position: absolute;
      top: 15px;
      right: 15px;
      display: flex;
      gap: 10px;
      user-select: none;
      z-index: 10;
    }

    .theme-btn {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      border: 2px solid transparent;
      cursor: pointer;
      transition: border-color 0.3s;
    }

    .theme-btn:hover {
      border-color: var(--color-primary);
    }

    .theme-btn[data-theme='dark'] {
      background: linear-gradient(135deg, var(--color-bg-dark), var(--color-bg-dark3));
    }

    .theme-btn[data-theme='light'] {
      background: #f0f4f8;
      border-color: #ccc;
    }

    .theme-btn[data-theme='neon'] {
      background: #39ff14;
      box-shadow: 0 0 8px #39ff14;
    }

    .theme-btn[data-theme='pink'] {
      background: #f06292;
    }

    /* Timer */
    .timer {
      font-weight: 700;
      font-size: 1.2rem;
      margin-bottom: 20px;
      user-select: none;
      color: var(--color-primary);
      transition: color var(--transition-speed);
    }

    body[data-theme='light'] .timer {
      color: #d81b60;
    }

    body[data-theme='neon'] .timer {
      color: #39ff14;
      text-shadow: 0 0 8px #39ff14;
    }

    body[data-theme='pink'] .timer {
      color: #c2185b;
    }

    /* Share button */
    .share-btn {
      margin-top: 20px;
      background-color: var(--color-primary);
      color: #fff;
      border: none;
      padding: 12px 25px;
      font-weight: 700;
      border-radius: var(--border-radius);
      cursor: pointer;
      box-shadow: 0 5px 15px var(--color-shadow);
      transition: background-color 0.3s ease;
      user-select: none;
    }

    .share-btn:hover {
      background-color: var(--color-primary-dark);
    }

    /* Responsive */
    @media (max-width: 480px) {
      .container {
        padding: 20px 25px;
      }
      h1 {
        font-size: 1.8rem;
      }
      button.option-btn {
        font-size: 1rem;
        padding: 12px;
      }
      .timer {
        font-size: 1rem;
      }
      .medalha img {
        width: 60px;
        height: 60px;
      }
    }
  </style>
</head>
<body data-theme="dark">

  <div class="container" role="main" aria-live="polite">

    <h1>Quem Postou Isso?</h1>

    <!-- Theme Selector -->
    <div class="theme-selector" aria-label="Selecionar tema">
      <button class="theme-btn" data-theme="dark" title="Tema Escuro" aria-pressed="true"></button>
      <button class="theme-btn" data-theme="light" title="Tema Claro" aria-pressed="false"></button>
      <button class="theme-btn" data-theme="neon" title="Tema Neon" aria-pressed="false"></button>
      <button class="theme-btn" data-theme="pink" title="Tema Rosa" aria-pressed="false"></button>
    </div>

    <div class="progress-bar" aria-label="Progresso do quiz">
      <div class="progress-fill" style="width: 0%"></div>
    </div>

    <div class="timer" aria-live="assertive" aria-atomic="true" id="timer">Tempo: 15s</div>

    <div class="question" id="question">Carregando pergunta...</div>

    <div class="options" id="options" role="list"></div>

    <div id="resultado" aria-live="assertive"></div>

    <button id="next-btn" style="display:none; margin-top:10px; padding: 12px 20px; font-weight:700; font-size:1.1rem; border-radius: var(--border-radius); cursor:pointer; border:none; background: var(--color-primary); color:#fff; box-shadow: 0 5px 10px var(--color-shadow); user-select:none;">
      Próxima
    </button>

    <div class="history" id="history" aria-label="Histórico de respostas"></div>

    <div class="medalhas" id="medalhas" aria-live="polite" aria-atomic="true"></div>

    <button class="share-btn" id="share-btn" style="display:none;" aria-label="Compartilhar resultado no WhatsApp, Facebook ou Twitter">
      Compartilhar resultado
    </button>

  </div>

  <!-- Sons -->
  <audio id="sound-correct" src="https://cdn.jsdelivr.net/gh/freesoundorg/samples/320/320653__inspectorj__correct-answer.wav"></audio>
  <audio id="sound-wrong" src="https://cdn.jsdelivr.net/gh/freesoundorg/samples/94/94070__noisecollector__wrong.wav"></audio>
  <audio id="sound-click" src="https://cdn.jsdelivr.net/gh/freesoundorg/samples/237/237354__unfa__click.wav"></audio>
  <audio id="sound-timeup" src="https://cdn.jsdelivr.net/gh/freesoundorg/samples/216/216090__blublubs__alert-short.wav"></audio>

  <script>
    (() => {
      'use strict';

      // Perguntas, respostas e explicações
      const quizData = [
        {
          question: "Quem postou: 'Eu sou o caminho, a verdade e a vida'?",
          options: ["Moisés", "Davi", "Jesus", "Pedro"],
          answer: 2,
          explanation: "Jesus disse isso em João 14:6."
        },
        {
          question: "Quem postou: 'Confia no Senhor de todo o teu coração'?",
          options: ["Salomão", "Provérbios", "Eclesiastes", "Jó"],
          answer: 1,
          explanation: "Este versículo está no livro de Provérbios 3:5."
        },
        {
          question: "Quem postou: 'Eu sou o bom pastor'?",
          options: ["Jesus", "Paulo", "Pedro", "João Batista"],
          answer: 0,
          explanation: "Jesus usou esta metáfora em João 10:11."
        },
        {
          question: "Quem postou: 'Não temas, porque eu sou contigo'?",
          options: ["Isaías", "Jeremias", "Ezequiel", "Daniel"],
          answer: 0,
          explanation: "Isaías disse isso em Isaías 41:10."
        },
        {
          question: "Quem postou: 'O Senhor é meu pastor, nada me faltará'?",
          options: ["Davi", "Samuel", "Elias", "Eliseu"],
          answer: 0,
          explanation: "Este salmo é o Salmo 23, atribuído a Davi."
        },
        {
          question: "Quem postou: 'Tudo posso naquele que me fortalece'?",
          options: ["Paulo", "Pedro", "João", "Tiago"],
          answer: 0,
          explanation: "Paulo escreveu isso em Filipenses 4:13."
        },
        {
          question: "Quem postou: 'Amarás o teu próximo como a ti mesmo'?",
          options: ["Moisés", "Jesus", "Paulo", "Pedro"],
          answer: 1,
          explanation: "Jesus ensinou isso em Mateus 22:39."
        },
        {
          question: "Quem postou: 'A fé sem obras é morta'?",
          options: ["Tiago", "Paulo", "Pedro", "João"],
          answer: 0,
          explanation: "Tiago escreveu isso em Tiago 2:26."
        },
        {
          question: "Quem postou: 'No princípio Deus criou os céus e a terra'?",
          options: ["Moisés", "Gênesis", "Jesus", "Salomão"],
          answer: 1,
          explanation: "Esta frase é a abertura do livro de Gênesis 1:1."
        },
        {
          question: "Quem postou: 'O Senhor é a minha luz e a minha salvação'?",
          options: ["Davi", "Samuel", "Salomão", "Paulo"],
          answer: 0,
          explanation: "Davi disse isso no Salmo 27:1."
        }
      ];

      // Easter eggs nomes especiais
      const easterEggs = {
        "kaleb": "alma gêmea",
        "cecilia": "alma gêmea",
        "rafael": 0,
        "rafael e cecilia": 0,
        "rafael & cecilia": 0
      };

      const progressFill = document.querySelector(".progress-fill");
      const questionEl = document.getElementById("question");
      const optionsEl = document.getElementById("options");
      const resultadoEl = document.getElementById("resultado");
      const nextBtn = document.getElementById("next-btn");
      const historyEl = document.getElementById("history");
      const medalhasEl = document.getElementById("medalhas");
      const shareBtn = document.getElementById("share-btn");
      const timerEl = document.getElementById("timer");

      const soundCorrect = document.getElementById("sound-correct");
      const soundWrong = document.getElementById("sound-wrong");
      const soundClick = document.getElementById("sound-click");
      const soundTimeup = document.getElementById("sound-timeup");

      // Variáveis de controle
      let currentIndex = 0;
      let score = 0;
      let timer = 15;
      let timerInterval = null;
      let history = [];

      // Tema
      const themeButtons = document.querySelectorAll(".theme-btn");
      themeButtons.forEach(btn => {
        btn.addEventListener("click", () => {
          const theme = btn.dataset.theme;
          document.body.setAttribute("data-theme", theme);
          themeButtons.forEach(b => b.setAttribute("aria-pressed", "false"));
          btn.setAttribute("aria-pressed", "true");
          soundClick.play();
        });
      });

      // Função pra limpar opções
      function clearOptions() {
        optionsEl.innerHTML = "";
        resultadoEl.textContent = "";
        nextBtn.style.display = "none";
      }

      // Atualizar barra de progresso
      function updateProgress() {
        const percent = ((currentIndex) / quizData.length) * 100;
        progressFill.style.width = percent + "%";
      }

      // Mostrar pergunta
      function showQuestion() {
        clearOptions();
        updateProgress();
        timer = 15;
        timerEl.textContent = `Tempo: ${timer}s`;

        if (timerInterval) clearInterval(timerInterval);
        timerInterval = setInterval(() => {
          timer--;
          timerEl.textContent = `Tempo: ${timer}s`;
          if (timer <= 5) {
            timerEl.style.color = "var(--color-error)";
            if (document.body.getAttribute("data-theme") === "light") {
              timerEl.style.color = "#b71c1c";
            } else if (document.body.getAttribute("data-theme") === "neon") {
              timerEl.style.color = "#f44336";
              timerEl.style.textShadow = "0 0 12px #f44336";
            } else if (document.body.getAttribute("data-theme") === "pink") {
              timerEl.style.color = "#c2185b";
            }
          } else {
            timerEl.style.color = "var(--color-primary)";
          }

          if (timer <= 0) {
            clearInterval(timerInterval);
            handleTimeOut();
          }
        }, 1000);

        const q = quizData[currentIndex];
        questionEl.textContent = q.question;

        q.options.forEach((opt, i) => {
          const btn = document.createElement("button");
          btn.className = "option-btn";
          btn.textContent = opt;
          btn.setAttribute("role", "listitem");
          btn.addEventListener("click", () => selectAnswer(i));
          optionsEl.appendChild(btn);
        });
      }

      // Quando o tempo acaba
      function handleTimeOut() {
        // Desabilitar botões
        Array.from(optionsEl.children).forEach(btn => btn.disabled = true);
        resultadoEl.textContent = "Tempo esgotado! Resposta correta destacada.";
        resultadoEl.style.color = "var(--color-error)";
        if (document.body.getAttribute("data-theme") === "light") {
          resultadoEl.style.color = "#b71c1c";
        } else if (document.body.getAttribute("data-theme") === "neon") {
          resultadoEl.style.color = "#f44336";
          resultadoEl.style.textShadow = "0 0 12px #f44336";
        } else if (document.body.getAttribute("data-theme") === "pink") {
          resultadoEl.style.color = "#c2185b";
        }
        soundTimeup.play();

        // Destacar correta
        const correctIndex = quizData[currentIndex].answer;
        optionsEl.children[correctIndex].style.backgroundColor = "var(--color-correct)";
        nextBtn.style.display = "inline-block";

        // Armazenar no histórico
        history.push({
          question: quizData[currentIndex].question,
          answer: null,
          correctAnswer: quizData[currentIndex].options[correctIndex],
          correct: false
        });
        updateHistory();
      }

      // Selecionar resposta
      function selectAnswer(selectedIndex) {
        clearInterval(timerInterval);
        Array.from(optionsEl.children).forEach(btn => btn.disabled = true);

        const correctIndex = quizData[currentIndex].answer;
        if (selectedIndex === correctIndex) {
          score++;
          resultadoEl.textContent = "Resposta correta! " + quizData[currentIndex].explanation;
          resultadoEl.style.color = "var(--color-correct)";
          soundCorrect.play();
          optionsEl.children[selectedIndex].style.backgroundColor = "var(--color-correct)";
        } else {
          resultadoEl.textContent = "Resposta errada! " + quizData[currentIndex].explanation;
          resultadoEl.style.color = "var(--color-error)";
          soundWrong.play();
          optionsEl.children[selectedIndex].style.backgroundColor = "var(--color-error)";
          optionsEl.children[correctIndex].style.backgroundColor = "var(--color-correct)";
        }

        nextBtn.style.display = "inline-block";

        // Armazenar no histórico
        history.push({
          question: quizData[currentIndex].question,
          answer: quizData[currentIndex].options[selectedIndex],
          correctAnswer: quizData[currentIndex].options[correctIndex],
          correct: selectedIndex === correctIndex
        });
        updateHistory();
      }

      // Atualizar histórico
      function updateHistory() {
        historyEl.innerHTML = "<h3>Histórico de respostas:</h3>";
        history.forEach((item, idx) => {
          const div = document.createElement("div");
          div.textContent = `${idx + 1}. ${item.question} - Resposta: ${item.answer || "Nenhuma"} - Correta: ${item.correctAnswer}`;
          div.style.color = item.correct ? "var(--color-correct)" : "var(--color-error)";
          historyEl.appendChild(div);
        });
      }

      // Mostrar medalhas conforme pontuação
      function showMedals() {
        medalhasEl.innerHTML = "<h3>Medalhas:</h3>";
        let medalhaHTML = "";
        if (score === quizData.length) {
          medalhaHTML = "🏅 Medalha de Ouro - Perfeito!";
        } else if (score >= quizData.length * 0.8) {
          medalhaHTML = "🥈 Medalha de Prata - Excelente!";
        } else if (score >= quizData.length * 0.5) {
          medalhaHTML = "🥉 Medalha de Bronze - Bom!";
        } else {
          medalhaHTML = "💔 Sem medalha, tente novamente.";
        }
        medalhasEl.innerHTML += `<p>${medalhaHTML}</p>`;
      }

      // Próxima pergunta
      nextBtn.addEventListener("click", () => {
        soundClick.play();
        currentIndex++;
        if (currentIndex < quizData.length) {
          showQuestion();
        } else {
          // Fim do quiz
          questionEl.textContent = "Fim do quiz! Você acertou " + score + " de " + quizData.length;
          optionsEl.innerHTML = "";
          nextBtn.style.display = "none";
          timerEl.style.display = "none";
          progressFill.style.width = "100%";
          showMedals();
          shareBtn.style.display = "inline-block";
        }
      });

      // Compartilhar resultado
      shareBtn.addEventListener("click", () => {
        soundClick.play();
        const shareText = `Meu resultado no quiz bíblico: ${score} de ${quizData.length} acertos! Tente você também!`;
        const shareUrl = encodeURIComponent(window.location.href);
        const whatsappUrl = `https://api.whatsapp.com/send?text=${encodeURIComponent(shareText + " " + shareUrl)}`;
        const facebookUrl = `https://www.facebook.com/sharer/sharer.php?u=${shareUrl}`;
        const twitterUrl = `https://twitter.com/intent/tweet?text=${encodeURIComponent(shareText)}&url=${shareUrl}`;

        const shareWindow = window.open("", "Compartilhar resultado", "width=600,height=400");
        shareWindow.document.write(`
          <p>Compartilhe seu resultado:</p>
          <ul>
            <li><a href="${whatsappUrl}" target="_blank" rel="noopener noreferrer">WhatsApp</a></li>
            <li><a href="${facebookUrl}" target="_blank" rel="noopener noreferrer">Facebook</a></li>
            <li><a href="${twitterUrl}" target="_blank" rel="noopener noreferrer">Twitter</a></li>
          </ul>
        `);
      });

      // Pedir nome para easter egg
      function askName() {
        let name = prompt("Digite seu nome para ver sua amizade especial:");
        if (!name) {
          name = "Anônimo";
        }
        const lowerName = name.toLowerCase();

        // Verificar easter eggs
        if (easterEggs.hasOwnProperty(lowerName)) {
          if (typeof easterEggs[lowerName] === "number") {
            alert(`Resultado especial para ${name}: ${easterEggs[lowerName]}% de amizade.`);
            score = easterEggs[lowerName];
          } else {
            alert(`Resultado especial para ${name}: ${easterEggs[lowerName]}.`);
            // Aqui você pode manipular o score ou qualquer outra coisa para este caso
          }
        }
      }

      // Inicialização
      askName();
      showQuestion();

    })();
  </script>

</body>
</html>
