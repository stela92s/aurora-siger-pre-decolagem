# 🚀 AURORA SIGER

---

# 4. Análise Energética

---

## 4.1 Objetivo

A análise energética tem como objetivo determinar a energia efetivamente disponível e estimar a autonomia energética inicial da nave Aurora Siger com base nos parâmetros disponíveis de seu sistema de energia.

Essa análise será utilizada para verificar se a energia armazenada é suficiente para atender aos requisitos energéticos previstos para a operação, especialmente durante a etapa de pré-decolagem e decolagem.

---

## 4.2 Parâmetros

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

A partir da `capacidade total` e do `percentual de carga`, será possível determinar a quantidade de energia atualmente disponível no sistema.

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

O `consumo estimado` representa a demanda energética necessária para executar a operação planejada, com especial atenção à etapa de decolagem.

Esse parâmetro deverá considerar o consumo dos principais sistemas envolvidos na operação da nave, incluindo, quando aplicável:

* sistemas de propulsão;
* sistemas de controle;
* computadores de bordo;
* sensores;
* sistemas de comunicação;
* sistemas de navegação;
* sistemas de gerenciamento de energia;
* demais equipamentos necessários à operação.

O `consumo estimado` será utilizado para determinar a demanda energética da operação e verificar se a energia útil disponível é suficiente para atendê-la.

É importante distinguir energia de potência:

* Energia (kWh): representa a quantidade de energia consumida ou armazenada;
* Potência (kW): representa a taxa de consumo ou fornecimento de energia.

Quando o objetivo for calcular a autonomia em função do tempo, o consumo deverá ser representado como uma potência média ou taxa de consumo, em kW.

Nesse caso, a relação entre energia disponível e potência consumida permitirá determinar o tempo estimado de autonomia.

---

### 4.4.4  Perdas Energéticas

As `perdas energéticas` representam a parcela da energia armazenada que não estará efetivamente disponível para utilização devido às perdas ocorridas durante os processos de armazenamento, conversão, transmissão e distribuição.

Essas perdas podem estar associadas à eficiência de componentes como:

* baterias;
* conversores;
* inversores;
* cabos;
* sistemas de distribuição;
* circuitos eletrônicos;
* demais componentes do sistema elétrico.

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

## 4.8 Critérios de Validação

Para permitir a integração da análise energética ao sistema de pré-decolagem, recomenda-se estabelecer critérios objetivos de validação.

A condição energética poderá ser determinada a partir da comparação entre a energia útil disponível e os requisitos energéticos da operação.

De forma conceitual:

Energia útil ≥ Energia requerida
→ Condição energética: OK

Energia útil < Energia requerida
→ Condição energética: NOK

Quando a validação for baseada em autonomia:

Autonomia calculada ≥ Autonomia mínima requerida
→ Condição energética: OK

Autonomia calculada < Autonomia mínima requerida
→ Condição energética: NOK

Os valores mínimos deverão ser definidos de acordo com os requisitos operacionais estabelecidos para a missão.

---

## 4.9 Conclusão

A análise energética permitirá determinar a quantidade de energia efetivamente disponível para a Aurora Siger e estimar sua autonomia energética antes do início da operação.

O processo considera a capacidade total do sistema de armazenamento, o nível atual de carga, o consumo energético previsto e as perdas associadas ao sistema elétrico.

A partir desses parâmetros, será possível determinar a energia disponível, aplicar as perdas energéticas, obter a energia útil e, quando aplicável, calcular a autonomia estimada da nave.

Os resultados serão posteriormente incorporados ao sistema desenvolvido em Python, permitindo utilizar a condição energética como um dos critérios de validação do processo de pré-decolagem.

Dessa forma, a análise energética complementará os demais parâmetros de telemetria da Aurora Siger, proporcionando uma avaliação estruturada das condições energéticas necessárias para o início da operação.
