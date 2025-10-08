<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Vendas</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f0f2f5;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px 0;
            margin: 0;
        }
        .calculadora-container {
            background-color: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            box-sizing: border-box;
        }
        h1 {
            color: #1e3a8a;
            text-align: center;
            margin-bottom: 25px;
        }
        .input-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #555;
        }
        input, select, button {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #ccc;
            box-sizing: border-box;
            font-size: 16px;
        }
        button {
            background-color: #2563eb;
            color: white;
            font-weight: 700;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #1e40af;
        }
        .resultado {
            margin-top: 30px;
            background-color: #eef2ff;
            padding: 20px;
            border-radius: 8px;
        }
        .resultado h2 {
            margin-top: 0;
            color: #1e3a8a;
            text-align: center;
            margin-bottom: 20px;
        }
        .resultado p {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            font-size: 16px;
        }
        .resultado span {
            font-weight: 700;
        }
        .resultado .total-cliente {
            font-weight: 700;
            border-top: 1px solid #ccc;
            padding-top: 10px;
        }
        .resultado .liquido {
            font-size: 18px;
            color: #16a34a;
            font-weight: 700;
            margin-top: 15px;
            border-top: 1px solid #ccc;
            padding-top: 15px;
        }
    </style>
</head>
<body>
    <div class="calculadora-container">
        <h1>Simulador de Venda</h1>
        
        <div class="input-group">
            <label for="valorVenda">Valor original do produto</label>
            <input type="number" id="valorVenda" placeholder="Ex: 150.50">
        </div>
        
        <div class="input-group">
            <label for="numParcelas">Em quantas parcelas?</label>
            <select id="numParcelas">
                <option value="1">1x (Crédito à vista)</option>
                <option value="2">2x</option>
                <option value="3">3x</option>
                <option value="4">4x</option>
                <option value="5">5x</option>
                <option value="6">6x</option>
                <option value="7">7x</option>
                <option value="8">8x</option>
                <option value="9">9x</option>
                <option value="10">10x</option>
                <option value="11">11x</option>
                <option value="12">12x</option>
            </select>
        </div>
        
        <button onclick="calcular()">Calcular Venda</button>
        
        <div class="resultado" id="areaResultado" style="display:none;">
            <h2>Resumo da Simulação</h2>
            <p>Valor original do produto: <span id="resultadoValorOriginal"></span></p>
            <p>Acréscimo (parcelamento): <span id="resultadoAcrescimo"></span></p>
            <p class="total-cliente">Valor Final (Cliente Paga): <span id="resultadoValorCliente"></span></p>
            <p>Parcela do Cliente: <span id="resultadoParcelaCliente"></span></p>
            <hr>
            <p>Taxa da Máquina: <span id="resultadoTaxa"></span></p>
            <p>Desconto (baseado no valor original): <span id="resultadoDesconto"></span></p>
            <p class="liquido">VOCÊ RECEBE (LÍQUIDO): <span id="resultadoLiquido"></span></p>
        </div>
    </div>

    <script>
        const taxas_por_parcela = {
            1: 0.0379, 2: 0.0589, 3: 0.0689, 4: 0.0789, 5: 0.0880,
            6: 0.0997, 7: 0.1289, 8: 0.1372, 9: 0.1505, 10: 0.1586,
            11: 0.1674, 12: 0.1746,
        };

        function formatarMoeda(valor) {
            return `R$ ${valor.toFixed(2).replace('.', ',')}`;
        }

        function calcular() {
            // 1. Pegar os valores dos campos de input
            const valorVendaOriginal = parseFloat(document.getElementById('valorVenda').value);
            const numParcelas = parseInt(document.getElementById('numParcelas').value);

            if (isNaN(valorVendaOriginal) || valorVendaOriginal <= 0) {
                alert("Por favor, insira um valor de venda válido.");
                return;
            }

            let acrescimo = 0;
            // 2. Aplicar a regra de negócio do acréscimo
            if (numParcelas > 5) {
                const parcelasExtras = numParcelas - 5;
                acrescimo = (valorVendaOriginal > 500) ? parcelasExtras * 20 : parcelasExtras * 10;
            }
            
            const valorBrutoAjustado = valorVendaOriginal + acrescimo;
            
            // 3. Realizar os cálculos com a NOVA LÓGICA
            const taxaAplicada = taxas_por_parcela[numParcelas];
            
            // *** MUDANÇA PRINCIPAL: A taxa agora incide sobre o valor ORIGINAL ***
            const valorDescontoTaxa = valorVendaOriginal * taxaAplicada;
            
            // O valor líquido é o que o cliente paga (total) menos o que a máquina desconta.
            const valorLiquido = valorBrutoAjustado - valorDescontoTaxa;
            
            const valorParcelaCliente = valorBrutoAjustado / numParcelas;
            
            // 4. Exibir os resultados na página com a NOVA ESTRUTURA
            document.getElementById('areaResultado').style.display = 'block';

            // Detalhamento para o cliente
            document.getElementById('resultadoValorOriginal').innerText = formatarMoeda(valorVendaOriginal);
            document.getElementById('resultadoAcrescimo').innerText = `+ ${formatarMoeda(acrescimo)}`;
            document.getElementById('resultadoValorCliente').innerText = formatarMoeda(valorBrutoAjustado);
            document.getElementById('resultadoParcelaCliente').innerText = `${numParcelas}x de ${formatarMoeda(valorParcelaCliente)}`;
            
            // Detalhamento para o vendedor
            document.getElementById('resultadoTaxa').innerText = `${(taxaAplicada * 100).toFixed(2)}%`.replace('.', ',');
            document.getElementById('resultadoDesconto').innerText = `- ${formatarMoeda(valorDescontoTaxa)}`;
            document.getElementById('resultadoLiquido').innerText = formatarMoeda(valorLiquido);
        }
    </script>
</body>
</html>
