# Criando o arquivo HTML do site solicitado pelo usuário
html_code = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora de Gerenciamento</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
    }
    .container {
      max-width: 600px;
      margin: 50px auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      background-color: #007bff;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .results {
      margin-top: 20px;
      background: #e8f5e9;
      padding: 15px;
      border-radius: 5px;
      color: #2e7d32;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Calculadora de Metas</h1>
    <label for="banca">Banca Inicial ($):</label>
    <input type="number" id="banca" placeholder="Ex: 1000">

    <label for="risco">Risco por Operação (%):</label>
    <input type="number" id="risco" placeholder="Ex: 2">

    <label for="stopLoss">Stop Loss (em pips):</label>
    <input type="number" id="stopLoss" placeholder="Ex: 20">

    <label for="valorPip">Valor por Pip ($):</label>
    <input type="number" id="valorPip" placeholder="Ex: 0.1">

    <label for="metaLucro">Meta de Lucro (%):</label>
    <input type="number" id="metaLucro" placeholder="Ex: 5">

    <label for="metaPerda">Meta de Perda (%):</label>
    <input type="number" id="metaPerda" placeholder="Ex: 4">

    <button onclick="calcular()">Calcular</button>

    <div class="results" id="results" style="display: none;"></div>
  </div>

  <script>
    function calcular() {
      // Pegando valores do formulário
      const banca = parseFloat(document.getElementById('banca').value);
      const risco = parseFloat(document.getElementById('risco').value) / 100;
      const stopLoss = parseFloat(document.getElementById('stopLoss').value);
      const valorPip = parseFloat(document.getElementById('valorPip').value);
      const metaLucro = parseFloat(document.getElementById('metaLucro').value) / 100;
      const metaPerda = parseFloat(document.getElementById('metaPerda').value) / 100;

      // Cálculos
      const riscoPorOperacao = banca * risco;
      const tamanhoLote = riscoPorOperacao / (stopLoss * valorPip);
      const metaStopWin = banca * metaLucro;
      const metaStopLoss = banca * metaPerda;

      // Exibindo os resultados
      const resultsDiv = document.getElementById('results');
      resultsDiv.style.display = 'block';
      resultsDiv.innerHTML = `
        <h3>Resultados</h3>
        <p><strong>Risco por Operação:</strong> $${riscoPorOperacao.toFixed(2)}</p>
        <p><strong>Tamanho do Lote:</strong> ${tamanhoLote.toFixed(2)} lotes</p>
        <p><strong>Meta de Lucro (Stop Win):</strong> $${metaStopWin.toFixed(2)}</p>
        <p><strong>Meta de Perda (Stop Loss):</strong> $${metaStopLoss.toFixed(2)}</p>
      `;
    }
  </script>
</body>
</html>
"""

# Salvando o arquivo para enviar ao usuário
file_path = "/mnt/data/CalculadoraGerenciamento/index.html"
with open(file_path, "w") as file:
    file.write(html_code)

file_path
