# 1.5 Análise assistida por IA

Nesta etapa, é utilizada uma Inteligência Artificial para auxiliar na interpretação dos dados de **telemetria** e **energia** da nave *Aurora Siger*.

A IA recebe os dados previamente estruturados em formato JSON e realiza uma análise baseada exclusivamente nas informações fornecidas. O objetivo é obter:

* **Classificação dos dados;**
* **Identificação de possíveis anomalias;**
* **Sugestões de risco.**

A análise possui caráter **preventivo e auxiliar**, não substituindo a validação dos dados ou a tomada de decisão por parte do responsável pelo sistema.

---

## 1.5.1 Preparação dos dados

Antes de enviar as informações para o modelo de IA, os dados são convertidos para o formato JSON.

```python
dados_formatados = json.dumps(
    dados_ia,
    ensure_ascii=False,
    indent=2
)
```

A utilização do `json.dumps()` permite transformar a estrutura `dados_ia` em uma representação textual organizada.

O parâmetro `ensure_ascii=False` permite preservar caracteres especiais, como os utilizados na língua portuguesa, enquanto `indent=2` melhora a organização e a legibilidade dos dados.

Dessa forma, a IA recebe os dados em uma estrutura padronizada e de fácil interpretação.

---

## 1.5.2 Dados utilizados pela análise

A análise considera principalmente duas áreas:

### Telemetria

Os dados de telemetria utilizados pelo sistema incluem:

| Parâmetro              | Unidade |
| ---------------------- | ------- |
| Temperatura interna    | °C      |
| Temperatura externa    | °C      |
| Integridade estrutural | —       |
| Nível de energia       | %       |
| Pressão dos tanques    | —       |
| Módulos críticos       | —       |
| Status do sistema      | —       |
| Falhas registradas     | —       |

Esses dados são apresentados inicialmente em uma tabela utilizando o `pandas.DataFrame`.

```python
tabela_telemetria = pd.DataFrame([
    ["Temperatura interna", dados_ia["telemetria"]["temperatura_interna"], "°C"],
    ["Temperatura externa", dados_ia["telemetria"]["temperatura_externa"], "°C"],
    ["Integridade estrutural", dados_ia["telemetria"]["integridade_estrutural"], ""],
    ["Nível de energia", dados_ia["telemetria"]["nivel_energia"], "%"],
    ["Pressão dos tanques", dados_ia["telemetria"]["pressao_tanques"], ""],
    ["Módulos críticos", dados_ia["telemetria"]["modulos_criticos"], ""],
    ["Status do sistema", dados_ia["telemetria"]["status_sistema"], ""],
], columns=["Parâmetro", "Valor", "Unidade"])
```

Além da análise realizada pela IA, o próprio código possui uma verificação inicial do estado da telemetria:

```python
if dados_ia["telemetria"]["status_sistema"] == "OK":
    print("O sistema de telemetria não apresenta falhas identificadas.")
else:
    print("Foram identificadas condições que exigem atenção.")
```

Caso existam falhas registradas, elas também são apresentadas ao utilizador.

---

## 1.5.3 Análise energética

A segunda área analisada corresponde às informações relacionadas à energia da nave.

São considerados:

| Parâmetro          | Unidade |
| ------------------ | ------- |
| Energia disponível | kWh     |
| Perdas energéticas | kWh     |
| Energia útil       | kWh     |
| Autonomia estimada | h       |
| Autonomia mínima   | h       |
| Status energético  | —       |

Esses dados são organizados através de um `DataFrame`:

```python
tabela_energia = pd.DataFrame([
    ["Energia disponível", dados_ia["energia"]["energia_disponivel"], "kWh"],
    ["Perdas energéticas", dados_ia["energia"]["perdas"], "kWh"],
    ["Energia útil", dados_ia["energia"]["energia_util"], "kWh"],
    ["Autonomia estimada", dados_ia["energia"]["autonomia"], "h"],
    ["Autonomia mínima", dados_ia["energia"]["autonomia_minima"], "h"],
    ["Status energético", dados_ia["energia"]["status_energia"], ""],
], columns=["Parâmetro", "Valor", "Unidade"])
```

O código também realiza uma verificação direta do estado energético:

```python
if dados_ia["energia"]["status_energia"] == "OK":
    print("A condição energética está adequada para a operação.")
else:
    print("A condição energética apresenta insuficiência de autonomia.")
```

Essa verificação serve como uma primeira avaliação antes da análise realizada pelo modelo de IA.

---

# 1.5.4 Classificação dos dados

A primeira tarefa solicitada à IA é classificar a situação geral dos dados.

O modelo recebe três categorias possíveis:

* **NORMAL**
* **ATENÇÃO**
* **CRÍTICO**

A classificação deve ser acompanhada de uma breve explicação baseada nos dados fornecidos.

A instrução enviada ao modelo estabelece explicitamente que a classificação deve ser realizada utilizando somente os dados disponíveis:

```text
Sua análise deve ser baseada SOMENTE nos dados recebidos.
Não invente valores.
Não altere os valores.
Não crie falhas que não estejam relacionadas aos dados.
```

Dessa forma, o modelo é orientado a não criar informações que não estejam presentes no conjunto de dados.

---

# 1.5.5 Identificação de possíveis anomalias

A segunda etapa consiste na identificação de possíveis anomalias.

A IA deve analisar os parâmetros de telemetria e energia e identificar aqueles que:

* estejam fora das condições esperadas;
* apresentem valores que mereçam atenção;
* possam representar uma condição anormal;
* estejam relacionados a algum indicador de risco.

Para cada possível anomalia, o modelo deve apresentar uma justificativa.

A instrução utilizada no código é:

```text
IDENTIFICAÇÃO DE POSSÍVEIS ANOMALIAS

Identifique os parâmetros que estejam fora das condições esperadas
ou que mereçam atenção.

Explique o motivo de cada possível anomalia.
```

É importante destacar que o resultado é denominado **possível anomalia**. A IA não deve considerar automaticamente que um determinado valor representa uma falha real.

A confirmação deve ser realizada posteriormente com base nos critérios técnicos e nas regras do sistema.

---

# 1.5.6 Sugestões de risco

Na terceira etapa, a IA utiliza os resultados da análise para apresentar possíveis riscos relacionados aos dados observados.

As sugestões devem possuir caráter:

* preventivo;
* técnico;
* relacionado aos dados fornecidos.

O prompt determina que a IA não deve criar falhas sem relação com os dados:

```text
SUGESTÕES DE RISCO

Apresente riscos potenciais relacionados aos dados encontrados.

As sugestões devem ser preventivas e técnicas.
Não invente falhas que não possam ser relacionadas aos dados.
```

Assim, caso um parâmetro apresente uma condição que mereça atenção, a IA pode indicar um possível risco associado e sugerir que o parâmetro seja acompanhado ou verificado.

---

# 1.5.7 Prompt utilizado pela IA

A análise é controlada por duas mensagens.

A primeira define o comportamento esperado do modelo:

```python
{
    "role": "system",
    "content": """
    Você é a inteligência artificial de análise da nave espacial Aurora Siger.

    Analise os dados de telemetria e energia fornecidos.

    Sua análise deve ser baseada SOMENTE nos dados recebidos.
    Não invente valores.
    Não altere os valores.
    Não crie falhas que não estejam relacionadas aos dados.

    Divida sua resposta obrigatoriamente em três partes:

    CLASSIFICAÇÃO DOS DADOS
    ...

    IDENTIFICAÇÃO DE POSSÍVEIS ANOMALIAS
    ...

    SUGESTÕES DE RISCO
    ...
    """
}
```

A segunda mensagem fornece os dados que serão analisados:

```python
{
    "role": "user",
    "content": f"""
    Analise os dados atuais da nave Aurora Siger:

    {dados_formatados}
    """
}
```

Essa separação permite definir primeiro as regras da análise e, posteriormente, enviar os dados reais para o modelo.

---

# 1.5.8 Execução do modelo

Após a construção das mensagens, o código utiliza o `tokenizer` para preparar o texto para o modelo:

```python
texto = tokenizer.apply_chat_template(
    mensagens,
    tokenize=False,
    add_generation_prompt=True
)
```

Em seguida, o texto é convertido em tensores:

```python
entradas = tokenizer(
    texto,
    return_tensors="pt"
).to(model.device)
```

A geração da resposta ocorre sem cálculo de gradientes:

```python
with torch.no_grad():
    saida = model.generate(
        **entradas,
        max_new_tokens=500,
        temperature=0.2,
        do_sample=True,
        top_p=0.9
    )
```

### Parâmetros utilizados

| Parâmetro        |  Valor | Função                                                   |
| ---------------- | -----: | -------------------------------------------------------- |
| `max_new_tokens` |  `500` | Limita o tamanho máximo da resposta gerada               |
| `temperature`    |  `0.2` | Mantém a geração mais controlada                         |
| `do_sample`      | `True` | Permite amostragem durante a geração                     |
| `top_p`          |  `0.9` | Controla o conjunto de tokens considerados na amostragem |

Por fim, a resposta produzida pelo modelo é convertida novamente para texto:

```python
resposta = tokenizer.decode(
    saida[0][entradas["input_ids"].shape[1]:],
    skip_special_tokens=True
)
```

---

# 1.5.9 Resultado da análise

O resultado final é apresentado no terminal:

```python
print("=" * 60)
print("12. ANÁLISE DA INTELIGÊNCIA ARTIFICIAL")
print("=" * 60)

print(resposta)
```

A resposta da IA deve seguir obrigatoriamente a estrutura:

```text
CLASSIFICAÇÃO DOS DADOS

[Classificação: NORMAL, ATENÇÃO ou CRÍTICO]

[Justificativa]

IDENTIFICAÇÃO DE POSSÍVEIS ANOMALIAS

[Parâmetros que merecem atenção]

[Justificativas]

SUGESTÕES DE RISCO

[Riscos potenciais e sugestões preventivas]
```

---

# 1.5.10 Fluxo da análise assistida por IA

O processo completo pode ser representado pelo seguinte fluxo:

```text
             DADOS DA AURORA SIGER
                      │
                      ▼
             ┌─────────────────┐
             │ Preparação dos  │
             │     dados       │
             └────────┬────────┘
                      │
                      ▼
              Formato JSON
                      │
             ┌────────┴────────┐
             │                 │
             ▼                 ▼
       TELEMETRIA           ENERGIA
             │                 │
             └────────┬────────┘
                      │
                      ▼
                Modelo de IA
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
    Classificação  Anomalias   Sugestões
       dos dados   possíveis    de risco
          │           │           │
          └───────────┼───────────┘
                      ▼
              Resultado textual
                      │
                      ▼
                Análise humana
```

---

# 1.5.11 Limitações e cuidados

A análise realizada pela IA deve ser considerada uma **ferramenta de apoio**.

O modelo recebe os dados fornecidos pelo sistema e produz uma interpretação baseada nas instruções definidas no prompt. Portanto, a qualidade da análise depende da qualidade, completude e consistência dos dados de entrada.

Além disso:

* A IA não substitui as verificações programadas no sistema;
* Uma possível anomalia não representa necessariamente uma falha;
* Uma sugestão de risco não representa uma confirmação de risco;
* Os resultados devem ser confrontados com os valores e regras técnicas do sistema;
* O modelo é instruído a não inventar valores ou falhas que não estejam relacionadas aos dados recebidos.

Dessa forma, a IA funciona como uma camada adicional de interpretação sobre a telemetria e os dados energéticos da *Aurora Siger*.

---

## 1.5.12 Resumo

A implementação desenvolvida utiliza Inteligência Artificial para complementar o diagnóstico da nave *Aurora Siger*.

O processo é dividido em três objetivos principais:

| Objetivo                                 | Descrição                                                                           |
| ---------------------------------------- | ----------------------------------------------------------------------------------- |
| **Classificação dos dados**              | Determina se a situação geral é `NORMAL`, `ATENÇÃO` ou `CRÍTICO`                    |
| **Identificação de possíveis anomalias** | Localiza parâmetros que estejam fora das condições esperadas ou que mereçam atenção |
| **Sugestões de risco**                   | Apresenta possíveis riscos e orientações preventivas relacionadas aos dados         |

A abordagem permite combinar as verificações programadas em Python com uma análise textual realizada por IA, proporcionando uma visão complementar do estado da telemetria e da disponibilidade energética do sistema.
