# Backtracking: resolvendo problemas através da exploração de possibilidades

Artigo didático sobre a técnica de Backtracking, produzido para a disciplina de Algoritmos em Grafos (PUC-SP). Autores: César José Santana da Silva e Igor Simões.

O projeto tem duas saídas a partir do mesmo conteúdo:

| Pasta | Saída | Como gerar |
|---|---|---|
| [`latex/`](latex/) | **PDF** em formato de artigo (Overleaf) | pdfLaTeX + biber. Ver [`latex/README.md`](latex/README.md) |
| [`web/`](web/) | **Site HTML** com simulações animadas | Quarto. Ver [`web/README.md`](web/README.md) |

- [`PLANO_EDICAO.md`](PLANO_EDICAO.md) documenta o plano de edição e as decisões tomadas.

## Versão web (publicação)

A versão web é um projeto [Quarto](https://quarto.org). Para visualizar localmente:

```bash
cd web
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
quarto preview
```

Para publicar no GitHub Pages (após enviar este repositório ao GitHub):

```bash
cd web
quarto publish gh-pages
```

O link final fica em `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.
