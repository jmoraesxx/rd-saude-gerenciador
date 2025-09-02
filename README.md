<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Consulta de Acesso — RD Saúde</title>
  <meta name="description" content="Sistema de consulta de acesso RD Saúde por CPF." />

  <!-- Fonte Google Fonts Poppins -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet" />

  <style>
    :root {
      --verde-claro: #10b981;
      --verde: #059669;
      --verde-escuro: #047857;
      --verde-mais-escuro: #065f46;
      --branco-transparente: rgba(255,255,255,0.95);
      --radius: 18px;
      --shadow-light: 0 8px 24px rgba(5,150,105,0.15);
      --shadow-strong: 0 12px 36px rgba(5,150,105,0.3);
      --font: 'Poppins', sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: var(--font);
    }

    body {
      min-height: 100vh;
      background: linear-gradient(135deg, var(--verde-claro), var(--verde));
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      color: #222;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }

    .card {
      background: var(--branco-transparente);
      border-radius: var(--radius);
      padding: 48px 40px 56px 40px;
      width: 100%;
      max-width: 620px;
      box-shadow: var(--shadow-light);
      backdrop-filter: blur(14px);
      text-align: center;
      transition: transform 0.35s ease, box-shadow 0.35s ease;
    }

    .card:hover {
      transform: translateY(-8px);
      box-shadow: var(--shadow-strong);
    }

    h1 {
      font-size: 2.4rem;
      margin-bottom: 0.3rem;
      font-weight: 700;
      color: var(--verde-mais-escuro);
      text-transform: uppercase;
      letter-spacing: 2px;
      text-shadow: 0 1px 2px rgba(0,0,0,0.1);
    }

    h2 {
      font-size: 2.8rem;
      margin-bottom: 1.6rem;
      font-weight: 800;
      color: var(--verde-escuro);
      text-transform: uppercase;
      letter-spacing: 3px;
      text-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }

    p {
      font-size: 1.25rem;
      margin-bottom: 2.6rem;
      opacity: 0.9;
      color: #333;
      font-weight: 500;
    }

    input {
      width: 100%;
      padding: 18px;
      border-radius: var(--radius);
      border: 2px solid #a7f3d0;
      margin-bottom: 1.8rem;
      font-size: 1.15rem;
      text-align: center;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
      font-weight: 500;
      color: #065f46;
      background: #d1fae5;
      box-shadow: inset 0 1px 3px rgba(0,0,0,0.05);
    }

    input::placeholder {
      color: #4ade80;
      font-weight: 400;
    }

    input:focus {
      outline: none;
      border-color: var(--verde-escuro);
      box-shadow: 0 0 12px rgba(5,150,105,0.6);
      background: #ffffff;
      color: #065f46;
    }

    button {
      width: 100%;
      padding: 20px;
      background: var(--verde);
      border: none;
      border-radius: var(--radius);
      font-size: 1.25rem;
      font-weight: 700;
      cursor: pointer;
      color: #fff;
      transition: background 0.35s ease, transform 0.25s ease, box-shadow 0.35s ease;
      box-shadow: 0 6px 18px rgba(5,150,105,0.35);
      user-select: none;
    }

    button:hover {
      background: var(--verde-escuro);
      transform: scale(1.07);
      box-shadow: 0 10px 28px rgba(5,150,105,0.55);
    }

    .result {
      margin-top: 2.2rem;
      font-size: 1.15rem;
      text-align: left;
      background: #fefefe;
      padding: 26px 28px;
      border-radius: var(--radius);
      border: 1.5px solid #a7f3d0;
      display: none;
      color: #065f46;
      line-height: 1.75;
      box-shadow: inset 0 3px 10px rgba(5,150,105,0.1);
      user-select: text;
      font-weight: 500;
    }

    /* Seção QR Code e botão lado a lado */
    .qr-section {
      margin-top: 36px;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 40px;
      flex-wrap: wrap;
    }

    #qrcode {
      background: white;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 8px 24px rgba(5,150,105,0.25);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
      flex-shrink: 0;
      width: 190px;
      height: 190px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #qrcode:hover {
      transform: scale(1.1);
      box-shadow: 0 12px 36px rgba(5,150,105,0.4);
    }

    .btn-link {
      background: var(--verde-escuro);
      border-radius: var(--radius);
      color: white;
      font-weight: 700;
      font-size: 1.3rem;
      border: none;
      cursor: pointer;
      box-shadow: 0 6px 20px rgba(4,120,87,0.5);
      transition: background 0.35s ease, transform 0.25s ease, box-shadow 0.35s ease;
      text-align: center;
      text-decoration: none;
      user-select: none;
      padding: 0 40px;
      height: 60px;
      flex-shrink: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      min-width: 220px;
    }

    .btn-link:hover {
      background: var(--verde-mais-escuro);
      transform: scale(1.1);
      box-shadow: 0 10px 28px rgba(6,95,70,0.7);
    }

    @media (max-width: 600px) {
      .qr-section {
        flex-direction: column;
        gap: 24px;
      }
      #qrcode, .btn-link {
        width: 100%;
        max-width: 320px;
        height: auto;
        padding: 20px;
      }
      .btn-link {
        height: 50px;
        font-size: 1.1rem;
        padding: 0 20px;
      }
    }
  </style>

  <!-- Biblioteca para gerar QR Code -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
</head>
<body>
  <div class="card" role="main" aria-label="Consulta de acesso RD Saúde">
    <h1>CONSULTA DE ACESSO</h1>
    <h2>RD SAÚDE</h2>
    <p>Digite o CPF para verificar suas informações</p>
    <input type="text" id="cpf" placeholder="Digite o CPF" aria-label="Campo para digitar CPF" />
    <button onclick="consultar()" aria-label="Botão para consultar CPF">Consultar</button>

    <div class="result" id="resultado" aria-live="polite"></div>

    <!-- Seção com QR Code à esquerda e botão à direita -->
    <div class="qr-section">
      <div id="qrcode" role="img" aria-label="QR Code para acesso ao serviço"></div>
      <button class="btn-link" onclick="window.open('https://centrord.service-now.com/esc?id=sc_cat_item&table=sc_cat_item&sys_id=cc9875551bc23050929b87bfe54bcb51&recordUrl=com.glideapp.servicecatalog_cat_item_view.do%3Fv%3D1&sysparm_id=cc9875551bc23050929b87bfe54bcb51', '_blank')" aria-label="Botão para acessar o serviço">Acessar Serviço</button>
    </div>
  </div>

  <script>
    function consultar() {
      const cpf = document.getElementById('cpf').value.trim();
      const resultado = document.getElementById('resultado');
      
      const dados = {
        "12345678900": { matricula: "001122", email: "funcionario1@rdsaude.com.br", cargo: "Atendente 1" },
        "98765432100": { matricula: "003344", email: "funcionario2@rdsaude.com.br", cargo: "Atendente 2" }
      };

      if (dados[cpf]) {
        const javaCodigo = Math.floor(1000 + Math.random() * 9000); // número 4 dígitos aleatório
        resultado.style.display = "block";
        resultado.innerHTML = `
          <strong>Matrícula:</strong> ${dados[cpf].matricula}<br/>
          <strong>Nome:</strong> Funcionário<br/>
          <strong>E-mail:</strong> ${dados[cpf].email}<br/>
          <strong>Cargo:</strong> ${dados[cpf].cargo}<br/>
          <strong>Java:</strong> ${javaCodigo}
        `;
      } else {
        resultado.style.display = "block";
        resultado.innerHTML = "CPF não encontrado no sistema.";
      }
    }

    // URL para o QR Code
    const urlQRCode = "https://centrord.service-now.com/esc?id=sc_cat_item&table=sc_cat_item&sys_id=cc9875551bc23050929b87bfe54bcb51&recordUrl=com.glideapp.servicecatalog_cat_item_view.do%3Fv%3D1&sysparm_id=cc9875551bc23050929b87bfe54bcb51";

    // Gerar QR Code no container 'qrcode'
    new QRCode(document.getElementById("qrcode"), {
      text: urlQRCode,
      width: 190,
      height: 190,
      colorDark : "#059669",
      colorLight : "#ffffff",
      correctLevel : QRCode.CorrectLevel.H
    });
  </script>
</body>
</html>
