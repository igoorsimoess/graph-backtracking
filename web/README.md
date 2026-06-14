# Backtracking: versão web/notebook (Quarto)

Versão publicável do artigo, em HTML, com **simulações animadas** geradas por código Python (matplotlib). Reaproveita o mesmo conteúdo da versão LaTeX.

## O que tem aqui

```
web/
├── _quarto.yml       # configuração do site (tema, sumário, numeração)
├── index.qmd         # o artigo completo + células de código das animações
├── styles.scss       # paleta consistente com o PDF
├── references.bib    # mesmas referências (ABNT)
├── requirements.txt  # dependências Python
└── README.md
```

Animações incluídas (rodam no HTML, com controles de play):

- **Explosão combinatória** (estática) · Seção "Por que o Backtracking Existe?"
- **Exploração do espaço de busca com poda** (animada) · Seção "Espaço de Busca"
- **Construção da solução parcial** (animada) · Seção "Soluções Parciais"
- **4 Rainhas resolvidas com Backtracking** (animada) · Seção "Resolvendo as 4 Rainhas"

## Pré-requisitos

1. **Quarto**: <https://quarto.org/docs/get-started/> (instalador para macOS).
2. **Python 3.10+** com as dependências:
   ```bash
   cd web
   python3 -m venv .venv && source .venv/bin/activate
   pip install -r requirements.txt
   ```

## Visualizar localmente

```bash
cd web
quarto preview        # abre no navegador e atualiza ao salvar
```

Para gerar o HTML final (pasta `_site/`):

```bash
quarto render
```

## Publicar (link compartilhável)

Opção mais simples, **Quarto Pub** (gratuito):

```bash
quarto publish quarto-pub
```

Ou **GitHub Pages**, se o projeto estiver em um repositório:

```bash
quarto publish gh-pages
```

## Observações

- As animações são geradas com `matplotlib.animation`, salvas como **GIF** (`writer="pillow"`) e embutidas no HTML via `<img>` em base64 (helper `gif_fig`). Assim tocam automaticamente em loop infinito, sem controles de play/pause (comportamento de GIF) e o HTML fica autossuficiente ao publicar. Os arquivos `.gif` são criados no render e ficam fora do Git (ver `.gitignore`).
- O código de cada animação aparece recolhido ("ver código"), mantendo o visual de artigo mas permitindo inspecionar a simulação (estilo notebook).
- Para citações no padrão ABNT, baixe um arquivo CSL da ABNT e adicione `csl: abnt.csl` ao `_quarto.yml`. Sem isso, o Quarto usa o estilo padrão.
