# Guia Técnico de Modelagem — Desafio da Semana 2

Este diretório contém os artefatos de classificação de objetos celestes baseados no conjunto de dados SDSS17, onde galáxias, quasares e estrelas são categorizados de forma supervisionada.

O fluxo de trabalho foi estruturado com base nas diretrizes de boas práticas científicas estabelecidas para o projeto, aplicando as etapas integradas de tratamento de dados, exploração estatística, seleção de algoritmos candidatos e calibração de parâmetros.

---

## Estrutura do Fluxo de Dados

A organização dos conjuntos de dados segue a separação metodológica recomendada para garantir a integridade dos dados brutos e a consistência do pipeline:

* **[data/raw/](./data/raw/)**: Armazena o conjunto de dados original de classificação estelar em seu estado bruto.
* **[data/processed/](./data/processed/)**: Centraliza as matrizes numéricas divididas em treino e teste após a filtragem de atributos e escalonamento.

O notebook executa a automação completa desses caminhos de forma dinâmica, criando os diretórios caso não existam e reorganizando o arquivo de dados de entrada para o local correto de leitura de maneira automática.

---

## Estrutura da Atividade Obrigatória

A modelagem de classificação multiclasse atende às seguintes definições de projeto:

### 1. Classificação Multiclasse com PyTorch
Como a classificação compreende três categorias distintas, o modelo foi construído com três neurônios de saída, utilizando o cálculo de entropia cruzada estruturada para computar o erro:

```python
modelo = RedeNeuralStellar(dimensao_entrada=10, dimensao_saida=3)
funcao_custo = nn.CrossEntropyLoss()
```

### 2. Estudo de Variabilidade da Rede
A arquitetura suporta a parametrização dinâmica de largura e profundidade, permitindo medir e comparar o comportamento de diferentes capacidades de rede.

### 3. Otimização e Regularização
O script oferece suporte para acoplamento de penalidade por Dropout nas camadas densas e decaimento de pesos nos otimizadores, permitindo auditar estratégias de atenuação de superajuste em otimizadores como Adam e SGD com Momentum.

### 4. Rastreamento Natico no MLflow
A plataforma é utilizada de forma integrada para gerenciar o ciclo de vida completo dos modelos, registrando parâmetros chaves e perdas contínuas a cada época de treino para diagnosticar comportamentos de subajuste ou superajuste.

---

## Estrutura da Atividade Opcional

Construção de uma rede neural rasa escrita puramente em Python e NumPy, com o objetivo de executar os processos internos de inicialização randômica, propagação de ativação por Sigmoid, cálculo de entropia com Softmax de saída e retropropagação analítica baseada na derivada das funções ativas.

---

## Execução do Painel de Experimentos

Para monitorar as perdas contínuas e analisar os gráficos comparativos, inicialize a interface visual rodando o seguinte comando na raiz do projeto:

```powershell
mlflow ui
```

O dashboard estará disponível no endereço `http://localhost:5000`.

---
## Histórico de Versões
| Versão | Descrição | Autor(es) | Data | Revisor(es) | Data de Revisão |
|--------|-----------|-----------|------|-------------|-----------------|
| 1.0 | Estruturação da documentação técnica do Desafio da Semana 2 com o mapeamento das rotinas de classificação estelar multiclasse e detalhamento das atividades obrigatórias e opcionais. | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 |
| 1.1 | Atualização da arquitetura de fluxo de dados, detalhando a separação de diretórios entre dados brutos e processados com automação de caminhos integrada. | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 |
