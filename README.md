<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Dias</title>
</head>
<body>
  <div class="container">
    <h1>Calculadora de dias corridos / úteis</h1>
    
    <form action="#" method="post">
        <label for="data_inicio">Data de Início:</label>
        <input type="date" id="data_inicio" name="data_inicio" required>
        
        <label for="data_fim">Data de Fim:</label>
        <input type="date" id="data_fim" name="data_fim" required>
        
        <button type="submit">Calcular</button>
    </form>
<div class="result">


<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $data_inicio = isset($_POST["data_inicio"]) ? $_POST["data_inicio"] : null;
    $data_fim = isset($_POST["data_fim"]) ? $_POST["data_fim"] : null;

    if ($data_inicio && $data_fim) {
        // Converter as datas para objetos DateTime
        $data_inicio_obj = new DateTime($data_inicio);
        $data_fim_obj = new DateTime($data_fim);

        // Calcular dias corridos
        $diferenca_dias_corridos = $data_inicio_obj->diff($data_fim_obj)->days + 1;

        // Calcular dias úteis
        $dias_uteis = contarDiasUteis($data_inicio_obj, $data_fim_obj);

        // Exibir resultados
        echo "<p>Dias corridos: $diferenca_dias_corridos</p><hr>";
        echo "<p>Dias úteis: $dias_uteis * </p><br> <strong>*</strong> Não considera feriados (Nac/Es/Mun).";
    } else {
        echo "<p>Por favor, forneça ambas as datas.</p>";
    }
}

function contarDiasUteis($data_inicio, $data_fim) {
    $intervalo = new DateInterval('P1D'); // Intervalo de 1 dia
    $periodo = new DatePeriod($data_inicio, $intervalo, $data_fim);

    $dias_uteis = 0;
    foreach ($periodo as $data) {
        // Verifica se não é sábado (0) ou domingo (6)
        if ($data->format('N') < 6) {
            $dias_uteis++;
        }
    }

    return $dias_uteis;
}
?></div>

</div>  
</body>
</html>

<style>
    body{
        margin: 0;
        background-color:  #fff;
    }
.container{
    
    display: block;
    text-align: center;
}
form{
    display: block;
    border: 1px solid blue;
    width: 600px;
    height: 200px;
    margin: 0 auto;
    padding: 20px;
    font-size: 1.8rem;
    background-color: #3333ff;
    border-radius: 15px;
    margin-bottom: 20px;
    color: white;
}
input{
    display: block;
    margin: 0 auto;
    margin-top: 10px;
    margin-bottom: 15px;
    font-size: 1.3rem;
}
button{
    font-size: 1.3rem;
}
button:hover{
    background-color: gray;
    color: #fff;
    font-size: 1.5rem;
}
.result{
    
    display: block;
    margin-top: 20px;
    width: 400px;
    height: 180px;
    margin: 0 auto;
    padding: 10px;
    font-size: 1.3rem;
    background-color: blue;
    border-radius: 15px;
    color: white;
}
footer{
    width: 100%;
    text-align: center;
}
</style>
<footer>
<p>By Alessandro Antunes - v1.0</p>
<?php
$dataAtual = date('d/m/Y');
echo "$dataAtual";
?>
</footer>
