# 🚀 AURORA SIGER — Sistema de Pré-Decolagem

Sistema de monitoramento, validação e análise dos parâmetros operacionais da nave **Aurora Siger**, desenvolvido como projeto acadêmico.

O projeto integra **telemetria simulada, algoritmo de validação, programação em Python, análise energética e Inteligência Artificial**, permitindo analisar as condições da nave antes da decolagem.

---

## 📋 Índice

* [Sobre o projeto](#-sobre-o-projeto)
* [Objetivos](#-objetivos)
* [Arquitetura do projeto](#-arquitetura-do-projeto)
* [1. Telemetria e parâmetros operacionais](#1-telemetria-e-parâmetros-operacionais)
* [2. Algoritmo, pseudocódigo e fluxograma](#2-algoritmo-pseudocódigo-e-fluxograma)
* [3. Implementação em Python](#3-implementação-em-python)
* [4. Análise energética](#4-análise-energética)
* [5. Análise assistida por IA](#5-análise-assistida-por-ia)
* [6. Reflexão crítica](#6-reflexão-crítica)
* [▶️ Instruções de execução](#️-instruções-de-execução)
* [📁 Estrutura do projeto](#-estrutura-do-projeto)
* [🛠️ Tecnologias utilizadas](#️-tecnologias-utilizadas)
* [⚠️ Limitações](#️-limitações)
* [👨‍💻 Considerações finais](#-considerações-finais)

---

# 📖 Sobre o projeto

A **Aurora Siger** é um projeto acadêmico que simula um sistema de monitoramento das condições operacionais de uma nave espacial durante a etapa de preparação para a decolagem.

O sistema recebe dados simulados de telemetria, verifica os parâmetros de acordo com limites previamente estabelecidos, realiza uma análise energética e utiliza Inteligência Artificial como ferramenta complementar de interpretação.

A lógica principal do sistema determina dois estados possíveis:

```text
DECOLAR
```

quando todos os parâmetros obrigatórios atendem aos critérios definidos;

ou:

```text
ABORTAR
```

quando pelo menos um parâmetro apresenta uma condição classificada como `NOK`.

> **Importante:** este projeto possui finalidade acadêmica e utiliza dados simulados. Não representa um sistema real de controle ou autorização de lançamento.

---

# 🎯 Objetivos

O projeto tem como principais objetivos:

* simular dados de telemetria de uma nave;
* validar parâmetros operacionais;
* registrar possíveis falhas;
* determinar uma condição geral de pré-decolagem;
* realizar cálculos de disponibilidade energética;
* estimar a autonomia da nave;
* utilizar IA para classificação e identificação de possíveis anomalias;
* documentar a lógica por meio de algoritmo, pseudocódigo e fluxograma;
* refletir sobre aspectos éticos, sociais e ambientais relacionados à tecnologia.

---

# 🏗️ Arquitetura do projeto

O funcionamento geral pode ser representado pelo seguinte fluxo:

```text
                    AURORA SIGER
                         │
                         ▼
                ┌─────────────────┐
                │ Dados simulados │
                └────────┬────────┘
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
       ┌───────────┐           ┌───────────┐
       │ Telemetria│           │  Energia  │
       └─────┬─────┘           └─────┬─────┘
             │                       │
             ▼                       ▼
       Validação dos            Cálculos de
        parâmetros                energia
             │                       │
             └───────────┬───────────┘
                         ▼
                  Análise por IA
                         │
                         ▼
              Classificação / Anomalias
                         │
                         ▼
                  Resultado final
```

---

# 1. Telemetria e parâmetros operacionais

A telemetria é responsável pela coleta, transmissão e monitoramento dos dados operacionais da Aurora Siger.

No projeto, os dados são **simulados em Python** para representar informações que poderiam ser provenientes de sensores.

## Parâmetros monitorados

| ID      | Parâmetro                   | Unidade | Tipo       |
| ------- | --------------------------- | ------- | ---------- |
| `T_INT` | Temperatura interna         | °C      | Numérico   |
| `T_EXT` | Temperatura externa         | °C      | Numérico   |
| `STR`   | Integridade estrutural      | 0/1     | Binário    |
| `PWR`   | Nível de energia            | %       | Numérico   |
| `PRS`   | Pressão dos tanques         | PSI     | Numérico   |
| `MOD`   | Status dos módulos críticos | Estado  | Categórico |

## Critérios de validação

| Parâmetro              | Condição `OK`         | Condição `NOK`                |
| ---------------------- | --------------------- | ----------------------------- |
| Temperatura interna    | `15 ≤ T_INT ≤ 30 °C`  | `T_INT < 15` ou `T_INT > 30`  |
| Temperatura externa    | `-50 ≤ T_EXT ≤ 50 °C` | `T_EXT < -50` ou `T_EXT > 50` |
| Integridade estrutural | `STR = 1`             | `STR = 0`                     |
| Nível de energia       | `80 ≤ PWR ≤ 100 %`    | `PWR < 80` ou `PWR > 100`     |
| Pressão dos tanques    | `150 ≤ PRS ≤ 300 PSI` | `PRS < 150` ou `PRS > 300`    |
| Módulos críticos       | `MOD = "OK"`          | `MOD ≠ "OK"`                  |

Cada parâmetro é analisado individualmente.

Caso um parâmetro não atenda ao critério estabelecido, ele é classificado como `NOK` e registrado na lista de falhas.

---

# 2. Algoritmo, pseudocódigo e fluxograma

O algoritmo organiza a sequência de operações necessárias para analisar os dados da nave.

## Fluxo lógico

```text
INÍCIO
   ↓
Iniciar sistema
   ↓
Receber dados de telemetria
   ↓
Validar parâmetros
   ↓
Registrar falhas
   ↓
Existem falhas?
  ↙       ↘
SIM       NÃO
 ↓         ↓
ABORTAR   DECOLAR
 ↓         ↓
Exibir    Finalizar
falhas
   ↓
  FIM
```

## Regra de decisão

A decisão geral segue a seguinte lógica:

```text
SE todos os parâmetros forem OK
    → DECOLAR

SE pelo menos um parâmetro for NOK
    → ABORTAR
```

O algoritmo foi posteriormente transformado em uma implementação Python.

---

# 3. Implementação em Python

A implementação foi desenvolvida em um **Python Notebook (`.ipynb`)**, utilizando o **Google Colab**.

Notebook da implementação:

[3.aurora_siger.ipynb](https://colab.research.google.com/drive/1_5lYS3x3V2opyxogfLxEWqjQ3ZJSMu7g#scrollTo=sE1OGbn5_BFM)

## Organização do código

O programa foi dividido em funções para facilitar a organização e manutenção:

```text
Geração dos dados
       ↓
Exibição da telemetria
       ↓
Validação dos parâmetros
       ↓
Registro das falhas
       ↓
Decisão final
```

## Geração da telemetria

A função `dados_telemetria()` gera valores simulados:

```python
def dados_telemetria():
    return {
        "DATA": datetime.now().strftime("%d/%m/%Y"),
        "T_INT": round(random.uniform(10, 35), 2),
        "T_EXT": round(random.uniform(-60, 60), 2),
        "STR": random.randint(0, 1),
        "PWR": round(random.uniform(50, 100), 2),
        "PRS": round(random.uniform(100, 350), 2),
        "MOD": random.choice(["OK", "FALHA"])
    }
```

São utilizados:

* `random.uniform()` para valores decimais;
* `random.randint()` para valores inteiros;
* `random.choice()` para estados categóricos;
* `datetime.now()` para registrar a data da execução.

## Validação

Durante a validação são utilizadas duas estruturas principais:

```python
falhas = []
sistema_ok = True
```

A lista `falhas` armazena os parâmetros que apresentarem problemas.

A variável `sistema_ok` representa o estado geral da validação.

Quando uma falha é encontrada:

```python
sistema_ok = False
```

e o parâmetro correspondente é adicionado à lista:

```python
falhas.append("Pressão dos tanques")
```

## Decisão final

A decisão utiliza uma estrutura condicional:

```python
if sistema_ok == True:
    print("STATUS: DECOLAR")
else:
    print("STATUS: ABORTAR")
```

Quando ocorre `ABORTAR`, as falhas identificadas também são apresentadas.

---

# 4. Análise energética

A análise energética tem como objetivo determinar a energia efetivamente disponível e estimar a autonomia inicial da Aurora Siger.

## Parâmetros

| ID          | Parâmetro                         | Unidade  |
| ----------- | --------------------------------- | -------- |
| `CAP_TOTAL` | Capacidade total de armazenamento | kWh      |
| `CAR_ATUAL` | Carga atual                       | %        |
| `CONS_EST`  | Consumo estimado                  | kW / kWh |
| `PER_ENERG` | Perdas energéticas                | %        |

## Energia disponível

O cálculo utilizado é:

```text
Energia disponível =
Capacidade total × (Carga atual / 100)
```

## Perdas energéticas

As perdas são calculadas por:

```text
Perdas =
Energia disponível × (Percentual de perdas / 100)
```

## Energia útil

Depois das perdas:

```text
Energia útil =
Energia disponível − Perdas
```

## Autonomia

Considerando o consumo como potência média:

```text
Autonomia =
Energia útil / Potência de consumo
```

O resultado é obtido em horas.

Para converter para minutos:

```text
Autonomia (min) =
Autonomia (h) × 60
```

## Critério energético

Para a simulação, foi definido:

```python
AUTONOMIA_MINIMA = 2.0
```

Assim:

```text
Autonomia ≥ 2 h
        ↓
      OK
```

e:

```text
Autonomia < 2 h
        ↓
      NOK
```

> O valor de 2 horas é um requisito definido para a simulação acadêmica e não representa um requisito de uma missão espacial real.

---

# 5. Análise assistida por IA

O projeto utiliza Inteligência Artificial como uma camada complementar de análise dos dados de telemetria e energia.

Os dados são organizados em formato JSON:

```python
dados_formatados = json.dumps(
    dados_ia,
    ensure_ascii=False,
    indent=2
)
```

A IA recebe os dados e realiza três tarefas principais.

## 5.1 Classificação dos dados

A situação geral é classificada em uma das categorias:

```text
NORMAL
ATENÇÃO
CRÍTICO
```

A classificação deve ser acompanhada de uma justificativa baseada nos dados recebidos.

## 5.2 Identificação de possíveis anomalias

A IA procura parâmetros que:

* estejam fora das condições esperadas;
* mereçam atenção;
* apresentem comportamento anormal;
* estejam relacionados a algum indicador de risco.

Uma possível anomalia não representa automaticamente uma falha confirmada.

## 5.3 Sugestões de risco

A IA também apresenta possíveis riscos relacionados aos dados observados.

As sugestões possuem caráter:

* preventivo;
* técnico;
* relacionado aos dados fornecidos.

## Estrutura da análise

O resultado esperado é:

```text
CLASSIFICAÇÃO DOS DADOS

NORMAL / ATENÇÃO / CRÍTICO

Justificativa...


IDENTIFICAÇÃO DE POSSÍVEIS ANOMALIAS

Parâmetros identificados...

Justificativas...


SUGESTÕES DE RISCO

Riscos potenciais...

Sugestões preventivas...
```

## Limitações da IA

A IA é utilizada somente como ferramenta de apoio.

O modelo:

* não substitui as regras programadas;
* não confirma automaticamente uma falha;
* depende da qualidade dos dados recebidos;
* pode interpretar informações de maneira inadequada;
* deve ser utilizado em conjunto com as verificações do sistema.

---

# 6. Reflexão crítica

O desenvolvimento do projeto também aborda questões relacionadas à ética, responsabilidade, sustentabilidade e impacto social.

## Ética e responsabilidade

Sistemas automatizados para operações críticas exigem supervisão humana.

Erros de sensores, falhas de software ou dados incorretos podem influenciar o resultado de uma análise.

Por isso, o projeto considera a necessidade de:

* validação;
* supervisão;
* redundância;
* verificação dos dados;
* responsabilidade humana.

A Inteligência Artificial é apresentada como ferramenta auxiliar e não como responsável isolada pela autorização da decolagem.

## Impacto social

A exploração espacial pode contribuir para:

* desenvolvimento científico;
* desenvolvimento tecnológico;
* geração de conhecimento;
* cooperação científica.

Ao mesmo tempo, envolve questões relacionadas aos custos, distribuição dos benefícios tecnológicos e possíveis aplicações estratégicas das tecnologias desenvolvidas.

## Sustentabilidade

A exploração espacial também apresenta desafios ambientais e tecnológicos, como:

* consumo de energia;
* produção de resíduos;
* reutilização de equipamentos;
* lixo espacial.

A análise energética desenvolvida no projeto demonstra a importância de acompanhar o consumo, as perdas e a disponibilidade de energia.

---

# ▶️ Instruções de execução

## Pré-requisitos

Para executar o projeto, são necessários:

* acesso à internet;
* uma conta Google;
* navegador web;
* acesso ao Google Colab;
* Python 3.

A implementação foi preparada para execução em notebook Jupyter/Google Colab.

## 1. Abrir o notebook

Acesse o notebook:

[3.aurora_siger.ipynb](https://colab.research.google.com/drive/1_5lYS3x3V2opyxogfLxEWqjQ3ZJSMu7g#scrollTo=sE1OGbn5_BFM)

## 2. Executar o ambiente

No Google Colab, abra o notebook e aguarde a inicialização do ambiente Python.

## 3. Executar as células

Execute as células do notebook na ordem em que aparecem.

No Google Colab, isso pode ser feito pelo botão de execução de cada célula ou pela opção:

```text
Ambiente de execução
→ Executar tudo
```

## 4. Verificar os dados de telemetria

Após a execução, o programa irá gerar valores simulados para:

```text
Temperatura interna
Temperatura externa
Integridade estrutural
Nível de energia
Pressão dos tanques
Módulos críticos
```

## 5. Verificar a validação

O sistema irá comparar os valores gerados com os limites definidos.

O resultado poderá ser:

```text
STATUS: DECOLAR
```

ou:

```text
STATUS: ABORTAR
```

Caso ocorram falhas, elas serão apresentadas na saída do programa.

## 6. Verificar a análise energética

O programa também irá calcular:

```text
Energia disponível
Perdas energéticas
Energia útil
Autonomia em horas
Autonomia em minutos
```

Depois, a autonomia será comparada com:

```text
AUTONOMIA_MINIMA = 2.0 horas
```

## 7. Executar a análise por IA

Após a preparação dos dados, o notebook organiza as informações em JSON e envia os dados para o modelo utilizado pelo projeto.

O resultado apresenta:

```text
CLASSIFICAÇÃO DOS DADOS
IDENTIFICAÇÃO DE POSSÍVEIS ANOMALIAS
SUGESTÕES DE RISCO
```

> A execução da etapa de IA depende das configurações e do modelo disponibilizado no próprio notebook.

---

# 📁 Estrutura do projeto

Uma possível organização dos arquivos é:

```text
aurora-siger-pre-decolagem/
│
├── README.md
│
├── docs/
│   ├── 1.telemetria.md
│   ├── 2.algoritmo.md
│   ├── 3.python.md
│   ├── 4.analise-energetica.md
│   ├── 5.analise-ia.md
│   └── 6.reflexao-critica.md
│
└── notebook/
    └── 3.aurora_siger.ipynb
```

A estrutura pode ser adaptada conforme a organização final do repositório.

---

# 🛠️ Tecnologias utilizadas

| Tecnologia                  | Utilização                           |
| --------------------------- | ------------------------------------ |
| **Python**                  | Desenvolvimento do sistema           |
| **Google Colab**            | Execução do notebook                 |
| **Jupyter Notebook**        | Estrutura da implementação           |
| **Random**                  | Geração dos dados simulados          |
| **Datetime**                | Registro da data de execução         |
| **Pandas**                  | Organização dos dados em tabelas     |
| **JSON**                    | Estruturação dos dados enviados à IA |
| **PyTorch**                 | Execução do modelo de IA             |
| **Tokenizer**               | Preparação dos dados para o modelo   |
| **Mermaid**                 | Representação do fluxograma          |
| **Inteligência Artificial** | Análise complementar dos dados       |

---

# ⚠️ Limitações

O projeto possui caráter **acadêmico e experimental**.

Os principais parâmetros são simulados por meio de geração pseudoaleatória. Portanto, os valores não representam dados provenientes de uma nave real.

Além disso:

* os limites utilizados são definidos para o projeto;
* a autonomia mínima de 2 horas é um requisito da simulação;
* a análise energética utiliza valores estimados;
* a IA depende dos dados fornecidos ao modelo;
* uma possível anomalia não representa necessariamente uma falha;
* a análise por IA não substitui validações determinísticas;
* o sistema não deve ser utilizado para controlar ou autorizar operações reais.

---

# 🔄 Fluxo completo do projeto

O funcionamento integrado pode ser resumido da seguinte maneira:

```text
┌──────────────────────────────┐
│       INÍCIO DO SISTEMA      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   Geração dos dados          │
│   de telemetria              │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   Validação dos parâmetros   │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Registro das falhas       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Análise energética       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       Análise por IA         │
└──────────────┬───────────────┘
               │
               ▼
       ┌───────┴───────┐
       │               │
       ▼               ▼
   DECOLAR          ABORTAR
       │               │
       └───────┬───────┘
               ▼
┌──────────────────────────────┐
│            FIM               │
└──────────────────────────────┘
```

---

# 📊 Resumo dos módulos

| Módulo                 | Função                                        |
| ---------------------- | --------------------------------------------- |
| **Telemetria**         | Coleta e organização dos parâmetros           |
| **Algoritmo**          | Define a sequência lógica de validação        |
| **Python**             | Implementa o sistema                          |
| **Análise energética** | Calcula energia útil e autonomia              |
| **IA**                 | Auxilia na interpretação dos dados            |
| **Reflexão crítica**   | Analisa aspectos éticos, sociais e ambientais |

---

# 👨‍💻 Considerações finais

O projeto **Aurora Siger** integra conceitos de programação, algoritmos, análise de dados, energia e Inteligência Artificial em uma aplicação acadêmica voltada à simulação de um sistema de pré-decolagem.

A construção do projeto foi organizada em etapas, começando pela definição dos parâmetros de telemetria, passando pela elaboração do algoritmo, pseudocódigo e fluxograma, até chegar à implementação em Python.

A análise energética acrescenta uma segunda camada de avaliação, permitindo calcular a energia disponível, as perdas, a energia útil e a autonomia estimada.

Por fim, a utilização de Inteligência Artificial fornece uma análise complementar dos dados, permitindo classificar a situação, identificar possíveis anomalias e apresentar sugestões preventivas.

O projeto também considera que sistemas automatizados devem ser desenvolvidos com responsabilidade, especialmente quando aplicados a situações críticas. Dessa forma, a IA e os algoritmos são tratados como ferramentas de apoio, enquanto a validação e a supervisão permanecem componentes importantes do processo.

---

## 🚀 Resultado

Ao integrar todos os módulos, o projeto apresenta uma estrutura de sistema capaz de:

```text
✔ Simular dados de telemetria
✔ Validar parâmetros operacionais
✔ Registrar falhas
✔ Calcular disponibilidade energética
✔ Estimar autonomia
✔ Classificar condições energéticas
✔ Utilizar IA para análise complementar
✔ Identificar possíveis anomalias
✔ Sugerir riscos preventivos
✔ Documentar todo o processo de desenvolvimento
```

---

## 📚 Documentação

A documentação detalhada de cada etapa pode ser organizada nos arquivos presentes no diretório `docs/`.

O notebook contém a implementação prática utilizada para executar a simulação.

---

**Projeto acadêmico — Aurora Siger 🚀**
