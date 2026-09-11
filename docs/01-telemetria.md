# 1. Organização e descrição da telemetria

## 1.1 Introdução

A telemetria da nave **Aurora Siger** é composta por dados simulados provenientes de sensores responsáveis por monitorar as principais condições operacionais da nave antes da decolagem.

O objetivo da telemetria é fornecer informações que possam ser analisadas pelo sistema de verificação pré-decolagem. A partir desses dados, o sistema poderá identificar condições normais, situações de alerta e possíveis falhas que possam impedir a autorização da decolagem.

> ⚠️ **Observação:** Os dados, valores, limites e condições utilizados neste projeto são fictícios e têm finalidade exclusivamente acadêmica. Eles não representam especificações reais de uma nave espacial ou de um sistema de lançamento.

### Parâmetros monitorados

- 🌡️ **Temperatura interna**
- 🌡️ **Temperatura externa**
- 🏗️ **Integridade estrutural**
- ⚡ **Nível de energia**
- ⛽ **Pressão dos tanques**
- 🔧 **Status dos módulos críticos**

---

## 🌡️ 1.2 Temperatura interna

Representa a temperatura no interior da nave.

**Unidade:** `°C`

### Faixa considerada segura

- Mínimo: **15 °C**
- Máximo: **30 °C**

Valores dentro dessa faixa serão considerados normais.

Valores fora dessa faixa serão considerados uma condição de falha.

### Exemplos

| Temperatura | Classificação |
|---:|---|
| 22 °C | 🟢 OK |
| 29 °C | 🟢 OK |
| 30 °C | 🟢 OK |
| 31 °C | 🔴 FALHA |
| 10 °C | 🔴 FALHA |

---

## 🌡️ 1.3 Temperatura externa

Representa a temperatura do ambiente externo à nave.

**Unidade:** `°C`

### Faixa considerada segura

- Mínimo: **-50 °C**
- Máximo: **50 °C**

### Exemplos

| Temperatura | Classificação |
|---:|---|
| 18 °C | 🟢 OK |
| -20 °C | 🟢 OK |
| 50 °C | 🟢 OK |
| 55 °C | 🔴 FALHA |
| -60 °C | 🔴 FALHA |

---

## 🏗️ 1.4 Integridade estrutural

Representa o resultado de uma verificação simplificada da estrutura da nave.

Neste projeto, a integridade estrutural será representada por um valor binário:

- `1` = estrutura íntegra
- `0` = falha estrutural

Para que a decolagem possa ser autorizada:

```text
integridade_estrutural = 1
