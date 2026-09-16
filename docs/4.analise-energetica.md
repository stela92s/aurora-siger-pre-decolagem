# 🚀 AURORA SIGER

---

# 4. Análise Energética

---

## 4.1 Objetivo

A análise energética tem como objetivo determinar a energia efetivamente disponível e estimar a autonomia energética inicial da nave Aurora Siger com base nos parâmetros disponíveis de seu sistema de energia.

Essa análise será utilizada para verificar se a energia armazenada é suficiente para atender aos requisitos energéticos previstos para a operação, especialmente durante a etapa de pré-decolagem e decolagem.

---

## 4.2 Parâmetros Considerados

Para a realização dos cálculos, serão considerados quatro parâmetros principais:

* capacidade total de armazenamento de energia;
* nível atual de carga;
* consumo energético estimado para a operação;
* perdas energéticas do sistema.

> Os resultados obtidos servirão como subsídio para o sistema de validação das condições de pré-decolagem

---

## 4.3 Parâmetros

| ID          | Parâmetro                         | Unidade  |
| ----------- | --------------------------------- | -------- |
| `CAP_TOTAL` | Capacidade total de armazenamento | kWh      |
| `CAR_ATUAL` | Carga atual do sistema            | %        |
| `CONS_EST`  | Consumo estimado da operação      | kW / kWh |
| `PER_ENERG` | Perdas energéticas                | %        |

> O consumo deve ser representado em kW quando utilizado para determinar autonomia em função do tempo. Quando o objetivo for representar uma quantidade total de energia consumida durante uma operação específica, deve ser utilizado kWh.

---

## 4.4 Descrição dos Parâmetros Energéticos

---

### 4.4.1 Capacidade Total

A capacidade total corresponde à quantidade máxima de energia que o sistema de armazenamento da nave é capaz de armazenar.

Esse parâmetro será expresso em quilowatt-hora (kWh) e representa a capacidade energética nominal do sistema quando este se encontra completamente carregado.

A capacidade total será utilizada como referência para determinar a quantidade de energia atualmente armazenada a partir do nível de carga informado.

---

### 4.4.2 Carga Atual

A carga atual representa o percentual de energia armazenada no sistema no momento em que a análise é realizada.

A partir da `capacidade_total` e do percentual de carga, será possível determinar a quantidade de energia atualmente disponível no sistema.

O cálculo será realizado por meio da seguinte relação:

```text
Energia disponível = Capacidade total × (Carga atual / 100)
```

Onde:

* Energia disponível é expressa em kWh;
* Capacidade total é expressa em kWh;
* Carga atual é expressa em porcentagem.

Dessa forma, o percentual de carga é convertido em uma quantidade absoluta de energia armazenada.

Esse valor representa a energia disponível antes da aplicação do fator correspondente às perdas energéticas do sistema.

---

### 4.4.3 Consumo Estimado na Decolagem

O `consumo_estimado` representa a demanda energética necessária para executar a operação planejada, com especial atenção à etapa de decolagem.

E será utilizado para determinar a demanda energética da operação e verificar se a energia útil disponível é suficiente para atendê-la.

É importante distinguir energia de potência:

* Energia (kWh): representa a quantidade de energia consumida ou armazenada;
* Potência (kW): representa a taxa de consumo ou fornecimento de energia.

Quando o objetivo for calcular a autonomia em função do tempo, o consumo deverá ser representado como uma potência média ou taxa de consumo, em kW.

Nesse caso, a relação entre energia disponível e potência consumida permitirá determinar o tempo estimado de autonomia.

---

### 4.4.4  Perdas Energéticas

As `perdas_energéticas` representam a parcela da energia armazenada que não estará efetivamente disponível para utilização devido às perdas ocorridas durante os processos de armazenamento, conversão, transmissão e distribuição.

Para fins de cálculo, as perdas poderão ser representadas como um percentual da energia disponível.

O cálculo será realizado por meio da seguinte relação:

```text
Perdas = Energia disponível × (Percentual de perdas / 100)
```

A energia efetivamente disponível para a operação será então determinada por:

`Energia útil = Energia disponível − Perdas`

Ou, de forma equivalente:

```test
Energia útil = Energia disponível × (1 − Percentual de perdas / 100)
```

A energia útil será utilizada como referência para os cálculos de autonomia e para a validação da condição energética da nave.

---

### 4.5 Cálculo da Autonomia Inicial

Após a determinação da energia útil disponível, será realizado o cálculo da autonomia energética inicial da Aurora Siger.

A autonomia representa o período estimado durante o qual a energia útil disponível é capaz de sustentar uma determinada demanda energética.

Quando o consumo for representado por uma potência média, a autonomia poderá ser calculada por meio da seguinte relação:

Autonomia = Energia útil / Potência de consumo

Considerando:

energia útil em kWh;
potência de consumo em kW;

o resultado será obtido em horas (h).

A autonomia poderá posteriormente ser convertida para minutos:

Autonomia (min) = Autonomia (h) × 60

Exemplo conceitual

Considerando uma energia útil de 80 kWh e uma potência média de consumo de 20 kW:

Autonomia = 80 / 20 = 4 h

Portanto, nessas condições, a autonomia energética estimada seria de 4 horas.

O valor de autonomia representa uma estimativa baseada na potência de consumo considerada. Alterações na demanda energética durante a operação resultarão em uma autonomia diferente.

---

## 4.6. Integração com o Sistema de Pré-Decolagem

A análise energética será posteriormente integrada ao sistema de validação das condições de pré-decolagem da Aurora Siger.

O resultado dos cálculos poderá ser utilizado como um dos parâmetros responsáveis pela determinação da condição energética da nave antes do início da operação.

A lógica de validação será baseada na comparação entre a energia útil disponível e a energia necessária para a operação planejada.

Condição energética

Energia útil suficiente
↓
Condição energética: OK

Energia útil insuficiente
↓
Condição energética: NOK

Caso a energia útil disponível ou a autonomia calculada não atendam aos requisitos mínimos definidos para a operação, o sistema deverá registrar uma condição energética inadequada.

Essa condição será posteriormente analisada em conjunto com os demais parâmetros de telemetria e critérios de validação, contribuindo para a determinação do estado geral da nave antes da decolagem.

---

## 4.7. Variáveis da Análise

Para a implementação posterior em Python, a análise energética deverá utilizar as seguintes variáveis:

| Variável             | Descrição                                       | Unidade  |
| -------------------- | ----------------------------------------------- | -------- |
| `capacidade_total`   | Capacidade máxima de armazenamento de energia   | kWh      |
| `carga_atual`        | Percentual de energia armazenada                | %        |
| `energia_disponivel` | Energia armazenada correspondente à carga atual | kWh      |
| `consumo`            | Potência média ou energia consumida na operação | kW / kWh |
| `perdas_energeticas` | Percentual de perdas do sistema                 | %        |
| `energia_util`       | Energia efetivamente disponível após as perdas  | kWh      |
| `autonomia`          | Tempo estimado de disponibilidade energética    | h        |


Essas variáveis formarão a base para o desenvolvimento do código responsável pelo cálculo energético da nave.

---

## 4.8 Implementação da Análise Energética em Python

A análise energética da Aurora Siger será implementada em Python com o objetivo de automatizar a obtenção dos dados, os cálculos de energia disponível, as perdas energéticas, a energia útil e a autonomia estimada da nave.

O código foi estruturado em diferentes funções, permitindo separar a geração dos dados, a apresentação das informações, os cálculos energéticos e a tomada de decisão.

### 4.8.1 Geração dos Dados Energéticos

Inicialmente, o programa utiliza a biblioteca `random` para gerar valores simulados dos parâmetros energéticos da nave. Essa abordagem permite realizar testes do sistema sem a necessidade de utilizar dados reais de telemetria.

```python
import random

def dados_energia():
    return {
        "capacidade_total": round(random.uniform(50, 100), 2),
        "carga_atual": round(random.uniform(50, 100), 2),
        "consumo": round(random.uniform(15, 40), 2),
        "perdas_energeticas": round(random.uniform(5, 15), 2)
    }
```

A função `dados_energia()` retorna um conjunto de dados contendo:

* `capacidade_total`: capacidade máxima de armazenamento, em kWh;
* `carga_atual`: percentual de carga armazenada;
* `consumo`: potência média de consumo, em kW;
* `perdas_energeticas`: percentual estimado de perdas do sistema.

Os valores são gerados dentro de intervalos definidos previamente para possibilitar a simulação de diferentes condições energéticas.

### 4.8.2 Exibição dos Dados

Após a geração dos parâmetros, a função `exibir_energia()` apresenta os dados energéticos no terminal.

```python
def exibir_energia(dados):

    print("==================================================")
    print("2. DADOS ENERGÉTICOS")
    print("==================================================")

    print(f"Capacidade total:       {dados['capacidade_total']} kWh")
    print(f"Carga atual:            {dados['carga_atual']} %")
    print(f"Consumo médio:          {dados['consumo']} kW")
    print(f"Perdas energéticas:     {dados['perdas_energeticas']} %")
```

Essa função tem como finalidade facilitar a visualização dos parâmetros utilizados na análise.

### 4.8.3 Cálculo da Energia Disponível e da Energia Útil

A função `validar_parametros()` é responsável pela realização dos cálculos energéticos.

```python
def validar_parametros(dados):

    capacidade_total = dados["capacidade_total"]
    carga_atual = dados["carga_atual"]
    consumo = dados["consumo"]
    perdas_percentual = dados["perdas_energeticas"]

    energia_disponivel = capacidade_total * (carga_atual / 100)

    perdas = energia_disponivel * (perdas_percentual / 100)

    energia_util = energia_disponivel - perdas

    autonomia = energia_util / consumo

    autonomia_minutos = autonomia * 60

    return {
        "energia_disponivel": round(energia_disponivel, 2),
        "perdas": round(perdas, 2),
        "energia_util": round(energia_util, 2),
        "autonomia": round(autonomia, 2),
        "autonomia_minutos": round(autonomia_minutos, 2)
    }
```

Primeiramente, o programa calcula a energia disponível a partir da capacidade total e do percentual de carga:

```text
Energia disponível = Capacidade total × (Carga atual / 100)
```

Em seguida, são calculadas as perdas energéticas:

```text
Perdas = Energia disponível × (Perdas / 100)
```

A energia útil é obtida pela diferença entre a energia disponível e as perdas:

```text
Energia útil = Energia disponível − Perdas
```

Por fim, o programa determina a autonomia estimada dividindo a energia útil pela potência média de consumo:

```text
Autonomia = Energia útil / Consumo
```

Como a energia está representada em kWh e o consumo em kW, o resultado da divisão é obtido em horas. Esse valor também é convertido para minutos para facilitar sua interpretação.

### 4.8.4 Apresentação da Análise Energética

Após a realização dos cálculos, a função `imprimir_analise()` apresenta os resultados no terminal.

```python
def imprimir_analise(analise):

    print("==================================================")
    print("3. ANÁLISE ENERGÉTICA")
    print("==================================================")

    print(f"Energia disponível:    {analise['energia_disponivel']} kWh")
    print(f"Perdas energéticas:    {analise['perdas']} kWh")
    print(f"Energia útil:           {analise['energia_util']} kWh")
    print(f"Autonomia estimada:     {analise['autonomia']} h")
    print(f"Autonomia estimada:     {analise['autonomia_minutos']} min")
```

Dessa forma, o operador consegue visualizar os principais resultados da análise energética antes da tomada de decisão.

### 4.8.5 Validação da Condição Energética

Para determinar se a nave apresenta condições energéticas adequadas para a operação, foi definido um valor mínimo de autonomia de 2 horas.

```python
AUTONOMIA_MINIMA = 2.0
```

A função `gerar_resultado()` compara a autonomia calculada com esse valor mínimo.

```python
def gerar_resultado(analise):

    autonomia = analise["autonomia"]

    if autonomia >= AUTONOMIA_MINIMA:
        status = "OK"
        mensagem = "Condição energética adequada para a operação."
    else:
        status = "NOK"
        mensagem = "Condição energética insuficiente para a operação."

    resultado = {
        "status": status,
        "mensagem": mensagem,
        "autonomia_minima": AUTONOMIA_MINIMA
    }

    return resultado
```

A lógica utilizada pode ser representada da seguinte forma:

```text
Autonomia calculada ≥ 2 horas
              ↓
      Condição energética OK
```

ou:

```text
Autonomia calculada < 2 horas
              ↓
      Condição energética NOK
```

O resultado `"OK"` indica que a autonomia calculada atende ao requisito mínimo definido para a simulação. Já o resultado `"NOK"` indica que a autonomia calculada está abaixo do requisito estabelecido.

### 4.8.6 Apresentação da Decisão Final

Por fim, a função `imprimir_resultado()` apresenta a decisão final da análise energética.

```python
def imprimir_resultado(resultado):

    print("==================================================")
    print("4. DECISÃO FINAL")
    print("==================================================")

    print(f"Autonomia mínima:      {resultado['autonomia_minima']} h")
    print(f"Condição energética:   {resultado['status']}")
    print(f"Status:                 {resultado['mensagem']}")
```

Essa etapa permite integrar a análise energética ao sistema de validação da pré-decolagem. O resultado obtido poderá posteriormente ser combinado com outros parâmetros de telemetria da Aurora Siger para determinar a condição geral da nave.

### 4.8.7 Fluxo de Funcionamento do Programa

O funcionamento da implementação pode ser resumido no seguinte fluxo:

```text
Geração dos dados energéticos
            ↓
Exibição dos parâmetros
            ↓
Cálculo da energia disponível
            ↓
Cálculo das perdas
            ↓
Cálculo da energia útil
            ↓
Cálculo da autonomia
            ↓
Comparação com autonomia mínima
            ↓
       ┌────┴────┐
       ↓         ↓
      OK        NOK
       ↓         ↓
Condição      Condição
adequada    insuficiente
```

A utilização de funções independentes permite organizar o código de forma modular, facilitando futuras alterações e a integração com dados reais de sensores ou sistemas de telemetria.

É importante destacar que, nesta etapa, os valores energéticos são simulados por meio da biblioteca `random`. Em uma implementação futura da Aurora Siger, esses valores poderão ser substituídos por informações provenientes de sensores, bancos de dados ou sistemas de telemetria.

---

## 4.9 Critérios de Validação

A validação energética será realizada a partir da comparação entre a autonomia calculada e a autonomia mínima estabelecida para a operação.

Para a implementação apresentada, foi adotada uma autonomia mínima de 2 horas como parâmetro de teste.

```text
Autonomia ≥ 2 h
→ Condição energética: OK

Autonomia < 2 h
→ Condição energética: NOK
```

Esse valor é utilizado como requisito da simulação e deverá ser substituído pelo valor definido nos requisitos reais da missão.

A validação permite que o resultado da análise energética seja utilizado como uma das condições do sistema de pré-decolagem.

---

## 4.10 Conclusão

A implementação em Python permite automatizar a análise energética da Aurora Siger, realizando desde a obtenção dos parâmetros até a determinação da condição energética final.

O programa calcula a energia disponível a partir da capacidade total e do nível de carga, determina as perdas energéticas, obtém a energia útil e calcula a autonomia estimada com base no consumo médio.

Posteriormente, a autonomia calculada é comparada com o requisito mínimo estabelecido, produzindo uma condição `"OK"` ou `"NOK"`.

A estrutura modular utilizada facilita a integração futura com outros componentes do sistema de controle e validação da Aurora Siger. Os dados atualmente utilizados são simulados, mas a mesma estrutura poderá ser adaptada para receber informações reais provenientes de sensores e sistemas de telemetria.

Dessa forma, a implementação em Python representa a aplicação prática da análise energética descrita neste trabalho, permitindo transformar os parâmetros energéticos em informações objetivas para auxiliar no processo de validação da pré-decolagem.
