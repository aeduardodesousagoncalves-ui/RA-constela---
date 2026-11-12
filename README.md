
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Áries - Realidade Aumentada</title>

  <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/mind-ar@1.2.5/dist/mindar-image-aframe.prod.js"></script>

  <style>
    body {
      margin: 0;
      background: #020617;
      font-family: Arial;
      color: white;
    }

    #painel {
      position: fixed;
      z-index: 10;
      top: 15px;
      left: 0;
      width: 100%;
      text-align: center;
    }

    button {
      padding: 12px 25px;
      border: none;
      border-radius: 20px;
      background: #38bdf8;
      font-weight: bold;
      cursor: pointer;
    }

    a-scene {
      display: none;
    }
  </style>
</head>

<body>

<div id="painel">
  <h2>CONSTELAÇÃO DE ÁRIES</h2>
  <p id="status">Experiência de realidade aumentada</p>
  <button id="iniciar">Iniciar câmera</button>
</div>

<a-scene
  id="cena"
  mindar-image="imageTargetSrc: ./targets.mind; autoStart: false;"
  vr-mode-ui="enabled: false"
  device-orientation-permission-ui="enabled: false">

  <a-camera position="0 0 0"
            look-controls="enabled: false"></a-camera>

  <a-entity id="marcador"
            mindar-image-target="targetIndex: 0">

    <a-entity position="0 0 0.15">

      <!-- Linhas que conectam as estrelas -->

      <a-entity line="start: -0.35 0.12 0; end: 0 0 0;
        color: #38bdf8"></a-entity>

      <a-entity line="start: 0 0 0; end: 0.32 -0.18 0;
        color: #38bdf8"></a-entity>

      <!-- Estrela Hamal -->

      <a-sphere position="-0.35 0.12 0"
        radius="0.035"
        material="color: #ffffff; emissive: #38bdf8;
        emissiveIntensity: 2">
      </a-sphere>

      <!-- Estrela Sheratan -->

      <a-sphere position="0 0 0"
        radius="0.028"
        material="color: #ffffff; emissive: #38bdf8;
        emissiveIntensity: 2">
      </a-sphere>

      <!-- Estrela Mesarthim -->

      <a-sphere position="0.32 -0.18 0"
        radius="0.025"
        material="color: #ffffff; emissive: #38bdf8;
        emissiveIntensity: 2">
      </a-sphere>

      <!-- Nomes das estrelas -->

      <a-text value="HAMAL"
        position="-0.43 0.19 0.01"
        color="#ffffff"
        width="1.1">
      </a-text>

      <a-text value="SHERATAN"
        position="-0.08 -0.08 0.01"
        color="#ffffff"
        width="1.1">
      </a-text>

      <a-text value="MESARTHIM"
        position="0.22 -0.26 0.01"
        color="#ffffff"
        width="1.1">
      </a-text>

      <!-- Título -->

      <a-text value="CONSTELACAO DE ARIES"
        position="-0.35 0.35 0.01"
        color="#38bdf8"
        width="2">
      </a-text>

    </a-entity>
  </a-entity>

</a-scene>

<script>
  const cena = document.querySelector("#cena");
  const botao = document.querySelector("#iniciar");
  const status = document.querySelector("#status");
  const marcador = document.querySelector("#marcador");

  botao.addEventListener("click", async () => {
    cena.style.display = "block";

    try {
      await cena.systems["mindar-image-system"].start();
      status.textContent = "Aponte para o QR Code!";
      botao.style.display = "none";
    } catch (erro) {
      status.textContent = "Erro ao acessar a câmera.";
      cena.style.display = "none";
    }
  });

  marcador.addEventListener("targetFound", () => {
    status.textContent = "Áries reconhecida!";
  });

  marcador.addEventListener("targetLost", () => {
    status.textContent = "Procure novamente o marcador.";
  });
</script>

</body>
</html>
