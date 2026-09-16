# 🚀 AURORA SIGER

---

# 4. Análise Energética

---

## 4.1 Análise Energética

A análise energética tem como objetivo determinar a autonomia inicial da nave Aurora Siger a partir das informações disponíveis sobre seu sistema de energia. Essa análise será utilizada para verificar se a quantidade de energia disponível é suficiente para atender ao consumo previsto durante a operação.

Para realizar esse cálculo, serão considerados quatro fatores principais: capacidade total de energia, carga atual, consumo estimado na decolagem e perdas energéticas.

---

## 4.2 Objetivo
Essa etapa é importante para verificar se a energia disponível é suficiente para atender aos requisitos da operação. O resultado da análise pode ser utilizado como um dos critérios para a tomada de decisão do sistema de pré-decolagem.

---

## 4.3 Parâmetros Monitorados

|ID| Parâmetro | unidade| 
|CAP_TOTAL| Capacidade total| kwh |
|CAR_ATUAL| Carga atual| % |
|CONS_EST| Consumo estimado na decolagem| kwh|
|PER_ENERG| Perdas energéticas| kWh |

---

## 4.4 Descrição dos parametros de energia

---

### 4.4.1 Capacidade Total

A capacidade total corresponde à quantidade máxima de energia que o sistema de armazenamento da nave é capaz de armazenar.

Esse valor será expresso em quilowatt-hora (kWh) e representa a capacidade energética nominal disponível quando o sistema está completamente carregado.

A capacidade total será utilizada como referência para determinar a quantidade de energia efetivamente disponível de acordo com o nível atual de carga.

---

### 4.4.2 Carga Atual

A carga atual representa o percentual de energia disponível no sistema no momento da análise.

A partir da capacidade total e da porcentagem de carga, será possível determinar a quantidade de energia armazenada atualmente.

O cálculo será realizado pela relação:

Energia disponível = Capacidade total × (Carga atual / 100)

Dessa forma, a porcentagem de carga será convertida em uma quantidade de energia expressa em kWh.

Esse valor representa a energia armazenada antes de serem consideradas as perdas energéticas do sistema.

---

### 4.4.3 Consumo Estimado na Decolagem

O consumo estimado na decolagem representa a quantidade de energia necessária para executar a etapa de decolagem da nave.

Esse parâmetro deverá considerar o consumo dos sistemas envolvidos na operação, incluindo os sistemas de propulsão, controle, computadores de bordo, sensores, comunicação e demais equipamentos necessários para o funcionamento da nave.

O consumo será utilizado para determinar quanto da energia disponível será utilizada durante a decolagem e para calcular a autonomia energética do sistema.

É importante diferenciar energia consumida, expressa em kWh, de potência, expressa em kW. Para o cálculo da autonomia em tempo, o consumo deverá ser definido como uma taxa de consumo, permitindo relacionar a energia disponível ao consumo por unidade de tempo.

---

### 4.4.4  Perdas Energéticas

As perdas energéticas representam a parcela da energia que não estará efetivamente disponível para utilização devido às perdas ocorridas durante o armazenamento, conversão e distribuição da energia.

Essas perdas podem estar relacionadas à eficiência dos sistemas elétricos, conversores, cabos, baterias e outros componentes envolvidos no fornecimento de energia.

As perdas serão consideradas como um percentual da energia disponível.

O cálculo poderá ser representado por:

Perdas = Energia disponível × (Percentual de perdas / 100)

A energia efetivamente disponível para a operação será então determinada pela diferença entre a energia armazenada e as perdas:

Energia útil = Energia disponível - Perdas

Esse valor será utilizado como base para o cálculo da autonomia.

---

### 4.5 Cálculo da Autonomia Inicial

Após determinar a energia útil disponível, será realizado o cálculo da autonomia inicial da nave.

A autonomia representa o período durante o qual a energia disponível é capaz de sustentar o consumo previsto do sistema.

Quando o consumo for representado como uma taxa de potência, a autonomia poderá ser determinada pela relação:

Autonomia = Energia útil / Consumo

Nesse caso, considerando a energia em kWh e o consumo em kW, o resultado será obtido em horas.

A partir desse resultado, também será possível converter a autonomia para outras unidades de tempo, como minutos, caso necessário.

---

## 4.6. Integração com o Sistema de Pré-Decolagem

A análise energética será posteriormente integrada ao sistema de validação da Aurora Siger.

O resultado do cálculo poderá ser utilizado como mais um parâmetro de segurança durante a verificação das condições de pré-decolagem.

A lógica geral será baseada na comparação entre a energia útil disponível e a energia necessária para a operação planejada.

Energia disponível suficiente
        ↓
Condição energética: OK

Energia disponível insuficiente
        ↓
Condição energética: NOK

Caso a autonomia calculada não atenda ao requisito mínimo estabelecido para a operação, o sistema deverá registrar uma condição de falha. Essa informação será posteriormente considerada junto aos demais parâmetros de telemetria na determinação do estado final da nave.

---

## 4.7. Variáveis da Análise

Para a implementação posterior em Python, a análise energética deverá trabalhar com as seguintes variáveis:

Variável	Descrição	Unidade
Capacidade total	Capacidade máxima de armazenamento de energia	kWh
Carga atual	Percentual de energia disponível	%
Energia disponível	Energia armazenada de acordo com a carga atual	kWh
Consumo	Energia ou potência utilizada durante a operação	kWh / kW
Perdas energéticas	Percentual de energia perdida no sistema	%
Energia útil	Energia efetivamente disponível após as perdas	kWh
Autonomia	Tempo estimado de disponibilidade energética	h

Essas variáveis formarão a base para o desenvolvimento do código responsável pelo cálculo energético da nave.

---

## 4.8 Conclusão

A análise energética permitirá determinar a quantidade de energia efetivamente disponível para a Aurora Siger e estimar sua autonomia inicial antes da decolagem.

O processo considera a capacidade total do sistema de armazenamento, o nível atual de carga, o consumo previsto durante a operação e as perdas energéticas existentes no sistema.

A partir desses dados, será possível determinar a energia útil disponível e calcular a autonomia energética. Posteriormente, esses resultados serão incorporados ao sistema desenvolvido em Python, permitindo utilizar a condição energética como parte dos critérios de validação da pré-decolagem.

Dessa forma, a análise energética complementará os demais parâmetros de telemetria do projeto, contribuindo para uma avaliação integrada das condições necessárias para a execução segura da operação.

