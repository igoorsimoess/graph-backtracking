# Backtracking: projeto LaTeX (artigo)

Projeto modular do artigo "Backtracking: resolvendo problemas através da exploração de possibilidades".

## Como compilar (Overleaf)

1. Subir a pasta `latex/` inteira para um projeto novo no Overleaf.
2. Definir o documento principal como `main.tex`.
3. Compilador: **pdfLaTeX**. Bibliografia: **biber** (Menu → Settings → Compiler: pdfLaTeX; Bibliography: biber). O Overleaf roda a sequência automaticamente.

Localmente:

```bash
cd latex
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

## Estrutura

```
latex/
├── main.tex              # documento mestre (so \input); ordem das secoes ja reordenada
├── preambulo/
│   ├── pacotes.tex       # \usepackage
│   ├── estilo.tex        # cores, titulos, espacamento
│   └── comandos.tex      # caixas didaticas + \figuraplaceholder
├── frontmatter/
│   ├── capa.tex          # cabecalho de artigo (STUB)
│   ├── resumo.tex        # quadro-resumo + Resumo + palavras-chave (STUB)
│   └── sumario.tex       # \tableofcontents
├── secoes/               # 13 secoes, uma por arquivo
├── figuras/tikz/         # 10 figuras vetoriais (TikZ)
└── referencias/referencias.bib
```

## Estado atual

- Artigo completo e compilável: capa, resumo, quadro-resumo, sumário, 13 seções e bibliografia ABNT.
- As 10 figuras estão finalizadas em **TikZ** (em `figuras/tikz/`), inseridas via `\figura{rótulo}{legenda}{caminho}`.

## Convenções de estilo

- **Nunca usar `---` (travessão / em dash).** Usar vírgula, dois-pontos, parênteses ou ponto.
- Paleta fixa (em `estilo.tex`): azul = decisão, verde = válido, vermelho = podado/inválido, cinza = não explorado.
- Caixas didáticas disponíveis: `ideiachave`, `passos`, `atencao`, `quadroresumo`.

Plano completo: ver `../PLANO_EDICAO.md`.
