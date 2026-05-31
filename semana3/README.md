# Semana 3 — Retrieval-Augmented Generation (RAG)

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
    └── opcional.ipynb      <- RAG denso com FAISS e sentence-transformers
```

---

## Atividade Obrigatória — RAG Lexical (BM25)

Pipeline de recuperação baseado em relevância lexical (TF-IDF ponderado) via algoritmo BM25Okapi:

1. Aquisição de 5.000 documentos da Wikipédia PT via streaming
2. Segmentação em chunks de 300 tokens com sobreposição de 50
3. Indexação via `rank-bm25`
4. Recuperação top-5 por consulta
5. Avaliação e exportação de métricas

---

## Atividade Opcional — RAG Denso (FAISS + Embeddings)

Pipeline de recuperação semântica via similaridade de cosseno em espaço vetorial:

1. Aquisição de 2.000 documentos (subset menor para viabilidade de embedding)
2. Segmentação em chunks de 200 tokens com sobreposição de 30
3. Geração de embeddings multilinguais com `paraphrase-multilingual-MiniLM-L12-v2`
4. Indexação via `faiss.IndexFlatIP` com normalização L2
5. Recuperação top-5 por consulta
6. Avaliação comparativa e exportação de métricas

---

## Dependências

Gerenciadas via `pip-tools` na raiz do projeto:

```bash
pip install -r requirements.txt
```

Pacotes relevantes para esta semana: `datasets`, `sentence-transformers`, `faiss-cpu`, `rank-bm25`.

---

## Histórico de Versões

| Versão | Descrição | Autor(es) | Data | Revisor(es) | Data de Revisão |
|--------|-----------|-----------|------|-------------|-----------------|
| 1.0 | Criação dos notebooks de RAG lexical e denso com corpus TucanoBR/wikipedia-PT. | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 | [artur mendonça arruda](https://github.com/ArtyMend07) | 31/05/2026 |
