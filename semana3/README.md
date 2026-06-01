# Semana 3: Retrieval-Augmented Generation (RAG)

Implementação de pipelines de Recuperação Aumentada por Geração (RAG) sobre o corpus da Wikipédia em português, via dataset `TucanoBR/wikipedia-PT` do Hugging Face.

---

## Estrutura

```
semana3/
├── data/
│   ├── raw/           <- Corpus bruto salvo localmente após primeira execução
│   └── processed/     <- Chunks, índices e resultados de avaliação
└── notebooks/
    ├── obrigatorio.ipynb   <- RAG lexical com BM25
    └── opcional.ipynb      <- RAG com FAISS e sentence-transformers
```

---

## Dataset

O corpus utilizado é o `TucanoBR/wikipedia-PT`, disponível no Hugging Face. O dataset expõe uma única coluna `text`, contendo o corpo integral de artigos da Wikipédia em português, sem campo de título separado. Essa característica influencia diretamente a estratégia de chunking adotada, onde os documentos são segmentados por tokens, sem ter referência a metadados estruturais.

---

## Atividade Obrigatória: RAG Lexical (BM25)

Pipeline de recuperação baseado em relevância lexical (TF-IDF ponderado) via algoritmo BM25Okapi:

1. Aquisição de 5.000 documentos da Wikipédia PT via streaming
2. Segmentação em chunks de 300 tokens com sobreposição de 50
3. Indexação via `rank-bm25`
4. Recuperação top-5 por consulta
5. Avaliação e exportação de métricas
6. Geração de respostas baseadas no contexto via `google/flan-t5-small`

---

## Atividade Opcional: RAG Denso com FAISS e Embeddings

Pipeline de recuperação semântica via similaridade de cosseno em espaço vetorial:

1. Aquisição de 2.000 documentos (subset menor para viabilidade de embedding)
2. Segmentação em chunks com sobreposição e teste de impacto do tamanho (ex: 200 vs 500 tokens) na qualidade do vetor
3. Geração de embeddings multilinguais com `paraphrase-multilingual-MiniLM-L12-v2`
4. Indexação via `faiss.IndexFlatIP` com normalização L2
5. Recuperação top-5 por consulta
6. Geração de respostas diretas utilizando o LLM `google/flan-t5-small` baseado no contexto
7. Avaliação comparativa e exportação de métricas

O modelo `paraphrase-multilingual-MiniLM-L12-v2` foi escolhido por ser leve, suportar nativamente o português e apresentar boa relação entre qualidade semântica e custo computacional, adequado para o volume de chunks processados sem GPU.

Para a geração, incorporamos o modelo open-source `google/flan-t5-small` (escolhido no lugar da versão `base`, pois estava dando falta de memória bruta no kernel do jupyter). Alimentando o LLM com o contexto recuperado, as respostas geradas demonstraram ser diretas e restritas aos fatos indexados, onde a injeção de contexto evitou alucinações comuns em respostas sem contexto (livro fechada ou book-closed).

---

## Resultados

### BM25 (Lexical)

| Consulta | Pontuação BM25 (top-1) | Contexto recuperado relevante? |
|---|---|---|
| O que é astronomia? | 14.83 | Não, retornou artigo de fonética |
| Quem foi Albert Einstein? | 10.94 | Parcial, artigo sobre Nobélio com menção a Albert |
| Como funciona a fotossíntese? | 16.46 | Não, retornou artigo sobre obras urbanas |
| O que é inteligência artificial? | 23.80 | Sim |
| Qual é a história do Brasil? | 22.72 | Sim |

### FAISS + Embeddings (Denso)

| Consulta | Similaridade de Cosseno (top-1) | Contexto recuperado relevante? |
|---|---|---|
| O que é astronomia? | 0.829 | Sim, artigo direto de Astronomia |
| Quem foi Albert Einstein? | 0.591 | Sim, física quântica com menção a Einstein |
| Como funciona a fotossíntese? | 0.547 | Sim, fotossíntese em liquens |
| O que é inteligência artificial? | 0.927 | Sim, artigo direto de IA |
| Qual é a história do Brasil? | 0.731 | Sim, Guerra de Canudos e interior do Brasil |

---

## Análise Comparativa

O BM25 falhou em 3 das 5 consultas, recuperando documentos com sobreposição lexical acidental, o clássico problema de vocabulário desalinhado entre consulta e corpus. A abordagem densa via FAISS acertou semanticamente todas as consultas, mesmo com um corpus quatro vezes menor (2k vs 5k documentos).

A diferença de desempenho evidencia a limitação fundamental da recuperação lexical, que é justamente a dependência de correspondência exata de termos. Em domínios com vocabulário rico e variado como a Wikipédia, embeddings semânticos são consistentemente superiores, ao custo de maior tempo de indexação e dependência de um modelo pré-treinado.

---

## Como Executar

```bash
pip install datasets sentence-transformers faiss-cpu rank-bm25 transformers "pyarrow>=14"
```

Abra o Jupyter e execute os notebooks na seguinte ordem:

1. `obrigatorio.ipynb`: baixa o corpus e constrói o índice BM25
2. `opcional.ipynb`: reutiliza parte do corpus, gera os embeddings e executa o LLM para geração

Na primeira execução, o corpus é baixado via streaming e salvo em `data/raw/` para reruns sem download adicional.

---

## Dependências

Gerenciadas via `pip-tools` na raiz do projeto. Pacotes relevantes para esta semana: `datasets`, `sentence-transformers`, `faiss-cpu`, `rank-bm25`, `transformers`, `pyarrow>=14`.

---

## Histórico de Versões

| Versão | Descrição | Autor(es) | Data | Revisor(es) | Data de Revisão |
|--------|-----------|-----------|------|-------------|-----------------|
| 1.0 | Criação e edição do README. | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 |
| 1.1 | Adição de resultados, análise comparativa, contexto do dataset e instruções de execução. | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 |
| 1.2 | Análise do impacto do chunk. | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 |
