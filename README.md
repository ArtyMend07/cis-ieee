# CIS IEEE — Resolução de Desafios de Machine Learning e Data Science

Este repositório é dedicado à estruturação e resolução dos desafios práticos de Machine Learning, Engenharia de Recursos e Análise de Dados desenvolvidos para a etapa de seleção e capacitação do CIS IEEE.

---

## Estrutura de Diretórios e Desafios

O repositório está organizado de forma modular, permitindo a separação limpa das etapas de processamento, dados brutos e processados, além das modelagens estatísticas de cada semana.

```text
/ (raiz do projeto)
├── desafio_introdutorio/     ← Modelagem inicial de nivelamento.
├── desafio1/                 ← Primeira modelagem preditiva e engenharia de recursos.
├── desafio2/                 ← Otimização de hiperparâmetros e deep learning baseada em PyTorch.
├── requirements.in           ← Dependências brutas do projeto.
└── requirements.txt          ← Dependências compiladas de forma determinística com hashes.
```

### Detalhamento dos Desafios Semanais

1. **[Desafio da Semana Introdutória](./desafio_introdutorio/)**
   - **Objetivo**: Resolução estruturada de nivelamento analítico, manipulação básica de conjuntos de dados e entendimento de pipelines iniciais.
   - **Solução Desenvolvida**: Notebook de análise exploratória e modelagem, localizado em [Artur_Arruda_solution.ipynb](./desafio_introdutorio/notebooks/Artur_Arruda_solution.ipynb).

2. **[Desafio da Semana 1](./desafio1/)**
   - **Objetivo**: Aplicação de engenharia de atributos estruturada, pré-processamento de variáveis categóricas e numéricas e validação cruzada inicial.
   - **Solução Desenvolvida**: Pipeline de modelagem completo, localizado em [solucao.ipynb](./desafio1/notebooks/solucao.ipynb).

3. **[Desafio da Semana 2](./desafio2/)**
   - **Objetivo**: Implementação de fluxos de treinamento para modelos tradicionais de Machine Learning e arquiteturas profundas baseadas em PyTorch, onde toda a calibração de hiperparâmetros e monitoramento de métricas por época são catalogados localmente por meio de logs nativos no MLflow.
   - **Guia Técnico**: Documentação de modelagem estruturada em [desafio2/README.md](./desafio2/README.md).
   - **Solução Desenvolvida**: Notebook estruturado em [solucao_desafio2.ipynb](./desafio2/notebooks/solucao_desafio2.ipynb).

---

## Gerenciamento de Dependências do Ambiente

Para garantir a reprodutibilidade dos experimentos, o projeto utiliza o `pip-tools` para travar versões exatas de dependências do Python. As definições de alto nível residem no arquivo [requirements.in](./requirements.in).

Para atualizar ou compilar o arquivo de requisitos de forma determinística, garantindo as hashes de integridade, execute na raiz do projeto com o ambiente virtual ativo:

```powershell
.\venv\Scripts\pip-compile requirements.in --generate-hashes
```

Para sincronizar o ambiente virtual do projeto de acordo com a árvore travada de dependências em [requirements.txt](./requirements.txt), execute:

```powershell
.\venv\Scripts\pip-sync requirements.txt
```

---
## Histórico de Versões
| Versão | Descrição | Autor(es) | Data | Revisor(es) | Data de Revisão |
|--------|-----------|-----------|------|-------------|-----------------|
| 1.0 | Reestruturação geral do README do repositório principal com inclusão dos caminhos relativos corretos e mapeamento dos desafios semanais. | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 22/05/2026 |
