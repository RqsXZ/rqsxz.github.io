<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Print QR Code</title>

  <!-- QR Code library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

  <style>
    @page {
      size: auto;
      margin: 0;
    }

    body {
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: Arial, sans-serif;
    }

    .label {
      width: 80mm;
      height: 50mm;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      border: 1px solid #000;
      box-sizing: border-box;
    }

    #qrcode {
      margin-bottom: 8px;
    }

    .code-text {
      font-size: 12px;
      font-weight: bold;
      text-align: center;
      word-break: break-all;
    }
  </style>
</head>
<body>

  <div class="label">
    <div id="qrcode"></div>
    <div class="code-text" id="codeText"></div>
  </div>

  <script>
    const params = new URLSearchParams(window.location.search);
    const value = params.get('value');

    if (!value) {
      document.body.innerHTML = '<h2>QR Code inválido</h2>';
      throw new Error('Missing QR value');
    }

    document.getElementById('codeText').innerText = value;

    new QRCode(document.getElementById('qrcode'), {
      text: value,
      width: 200,
      height: 200,
      correctLevel: QRCode.CorrectLevel.H
    });

    // Abre automaticamente o diálogo de impressão
    window.onload = () => {
      setTimeout(() => window.print(), 500);
    };
  </script>

</body>
</html>
