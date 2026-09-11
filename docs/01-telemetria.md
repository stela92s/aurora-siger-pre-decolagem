# Organização e descrição da telemetria

## 1. Introdução

A telemetria da nave **Aurora Siger** é composta por dados simulados provenientes de sensores responsáveis por monitorar as principais condições operacionais da nave antes da decolagem.

O objetivo da telemetria é fornecer informações que possam ser analisadas pelo sistema de verificação pré-decolagem. A partir desses dados, o sistema poderá identificar condições normais, situações de alerta e possíveis falhas que possam impedir a autorização da decolagem.

---

## 2. Parâmetros monitorados

O sistema monitora os seguintes parâmetros:

* 🌡️ **Temperatura interna**
* 🌡️ **Temperatura externa**
* 🏗️ **Integridade estrutural**
* ⚡ **Nível de energia**
* ⛽ **Pressão dos tanques**
* 🔧 **Status dos módulos críticos**

---

### 🌡️ 2.1 Temperatura interna

Representa a temperatura no interior da nave.

**Unidade:** `°C`

Faixa considerada segura

* **Mínimo:** `15 °C`
* **Máximo:** `30 °C`

> ⚠️ Valores entre 15 °C a 30 °C serão considerados dentro dos parâmetros normais.
> Valores fora dessa faixa serão classificados como condição de falha pelo algoritmo de verificação.

Exemplos

| Temperatura | Classificação |
| ----------: | ------------- |
|       22 °C | 🟢 OK         |
|       29 °C | 🟢 OK         |
|       10 °C | 🔴 FALHA      |

---

### 🌡️ 2.2 Temperatura externa

Representa a temperatura do ambiente externo à nave.

**Unidade:** `°C`

### Faixa considerada segura

*  **Mínimo:** `-50 °C`
*  **Máximo:** `50 °C`

 > ⚠️ Valores entre -50 °C a 50 °C serão considerados dentro dos parâmetros normais.
> Valores fora dessa faixa serão classificados como condição de falha pelo algoritmo de verificação.

Exemplos

| Temperatura | Classificação |
| ----------: | ------------- |
|       18 °C | 🟢 OK         |
|      -20 °C | 🟢 OK         |
|      -60 °C | 🔴 FALHA      |

---

### 🧱 2.3 Integridade estrutural

Representa o resultado de uma verificação da estrutura da nave.

### Valores possíveis

* `1` =  Estrutura íntegra
* `0` =  Falha estrutural

> ⚠️ Para que a decolagem possa ser autorizada, a integridade estrutural deverá apresentar o valor: `1`
Qualquer valor diferente de `1` será considerado uma condição de falha pelo algoritmo de verificação.

Exemplos

| Valor | Classificação |
| ----: | ------------- |
|   `1` | 🟢 OK         |
|   `0` | 🔴 FALHA      |

---

### ⚡ 2.4 Nível de energia

Representa a quantidade de energia disponível nos sistemas da nave.

**Unidade:** `%`

### Faixa considerada segura

* **Mínimo:** `80%`
* **Máximo:** `100%`

> ⚠️ Valores inferiores a **80%** serão considerados insuficientes para a autorização da decolagem.

Exemplos

| Energia | Classificação |
| ------: | ------------- |
|    100% | 🟢 OK         |
|     92% | 🟢 OK         |
|     65% | 🔴 FALHA      |

---

### ⛽ 2.5 Pressão dos tanques

Representa a pressão operacional dos tanques em relação ao valor nominal definido para a simulação.

**Unidade:** `PSI`

### Faixa considerada segura

*  **Mínimo:** `150`
*  **Máximo:** `300`

> ⚠️ Valores entre 150 a 300 serão considerados dentro dos parâmetros normais.
Valores fora dessa faixa serão classificados como condição de falha pelo algoritmo de verificação.

Exemplos

| Pressão | Classificação |
| ------: | ------------- |
| 200 PSI | 🟢 OK         |
|  250 PSI| 🟢 OK         |
| 100 PSI | 🔴 FALHA      |

---

### 🔧 2.6 Status dos módulos críticos

Representa o estado dos principais módulos necessários para a operação da nave.

Os módulos críticos podem apresentar três estados:

| Status   | Significado                 |
| -------- | --------------------------- |
|  🟢 OK     | Funcionamento normal        |
| 🟡 ALERTA | Condição que requer atenção |
| 🔴 FALHA  | Falha identificada          |


> ⚠️ Caso qualquer módulo crítico apresente o estado FALHA, a decolagem deverá ser abortada.

---

## 📋 3. Tabela geral de parâmetros

A tabela a seguir apresenta os principais parâmetros utilizados na verificação das condições operacionais da nave antes da decolagem.

| 📡 Parâmetro               |  Unidade |  Mínimo |  Máximo | 
| -------------------------- | ---------- | --------: | --------: |
| 🌡️ Temperatura interna    | °C         |        15 |        30 |
| 🌡️ Temperatura externa    | °C         |       -50 |        50 | 
| 🏗️ Integridade estrutural | 0/1        |         1 |         1 | 
| ⚡ Energia                  | %          |        80 |       100 | 
| ⛽ Pressão dos tanques      | PSI         |        150 |       300 | 
| 🔧 Módulos críticos        | Estado     |      `OK` |      `OK` | 





