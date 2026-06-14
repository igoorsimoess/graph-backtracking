# Plano de Edição — Guia de Backtracking

> Documento de trabalho. Aqui descrevemos **o que** será feito e **como**, passo a passo, sem ainda executar nenhuma edição. O conteúdo do texto **não será alterado** (nada de adicionar ou remover ideias); o foco desta fase é **apresentação, estrutura e visualizações**.

---

## 0. Princípios e restrições (valem para tudo)

1. **Tudo em LaTeX**, organizado de forma **modular**, pronto para subir no Overleaf.
2. **Idioma: português** em todo o documento (texto, legendas, títulos, sumário).
3. **Nunca usar o travessão `—` (em dash)** em nenhum lugar. Em LaTeX, isso significa **nunca digitar `---`**. Onde houver necessidade de pausa, usar vírgula, dois-pontos, parênteses ou ponto. Onde o texto original já tiver `—`, será substituído por pontuação equivalente (isto é regra de estilo, não mudança de conteúdo).
4. **Não mudar o conteúdo**: as 13 seções, o resumo, as palavras-chave e as referências permanecem com o mesmo significado. Podemos mexer em **ordem de apresentação** e **forma**, não em ideias.
5. **Visualizações representacionais**: explicações que envolvem "processo" ou "matemática" ganham representações visuais (figuras passo a passo no PDF; GIFs/animações na versão web/notebook).
6. Esta fase entrega **apenas o plano**. As edições acontecem depois, juntos, seguindo as etapas abaixo.

---

## 1. Decisão de formato: como sair de "trabalho .docx" para "artigo de verdade"

Você pediu duas coisas que se complementam:

- um **projeto LaTeX no Overleaf** (saída PDF, com cara de artigo);
- uma **versão tipo notebook, publicável** (com GIFs/animações).

A tensão real: **GIF não roda em PDF**. Um PDF é estático. Por isso o plano trabalha com **duas saídas a partir de uma base comum**:

| Saída | Ferramenta | Onde vivem as animações | Uso |
|---|---|---|---|
| **PDF "artigo"** | LaTeX no Overleaf | Sequências de figuras passo a passo (TikZ) e, opcionalmente, animações embutidas com o pacote `animate` (rodam só no Adobe Reader) | Entrega acadêmica, impressão |
| **Web / notebook** | Ver Seção 8 deste plano | GIFs e/ou animações interativas de verdade | Publicação online, link compartilhável |

> **Recomendação:** manter o **LaTeX como fonte principal** (atende ao pedido do Overleaf) e gerar a versão web a partir dele. Na Seção 8 comparo as três rotas possíveis para a versão notebook e recomendo uma.

---

## 2. Estrutura modular do projeto LaTeX (Overleaf)

Boas práticas de Overleaf: um `main.tex` enxuto que só **inclui** arquivos, preâmbulo separado, uma seção por arquivo, figuras e bibliografia isoladas. Estrutura proposta:

```
backtracking/
├── main.tex                  # documento mestre: só \input / \include
├── preambulo/
│   ├── pacotes.tex           # todos os \usepackage
│   ├── estilo.tex            # cores, fontes, espaçamento, titlesec
│   └── comandos.tex          # comandos próprios + caixas (boxes) didáticas
├── frontmatter/
│   ├── capa.tex              # bloco de título estilo artigo (ver Seção 4)
│   ├── resumo.tex            # Resumo + palavras-chave
│   └── sumario.tex           # \tableofcontents (ver Seção 5)
├── secoes/
│   ├── 01-introducao.tex
│   ├── 02-por-que-existe.tex
│   ├── 03-o-que-e.tex
│   ├── 04-espaco-de-busca.tex
│   ├── 05-solucoes-parciais.tex
│   ├── 06-retrocesso.tex
│   ├── 07-poda.tex
│   ├── 08-aplicacoes.tex
│   ├── 09-quatro-rainhas.tex
│   ├── 10-resolvendo-rainhas.tex
│   ├── 11-arvore-rainhas.tex
│   ├── 12-vantagens-limitacoes.tex
│   └── 13-conclusao.tex
├── figuras/
│   ├── raster/               # as imagens atuais (image1..image7 renomeadas)
│   └── tikz/                 # figuras vetoriais novas (árvores, tabuleiro, poda)
├── referencias/
│   └── referencias.bib       # bibliografia (ver Seção 7)
└── README.md                 # como compilar no Overleaf
```

**Como `main.tex` ficará (esqueleto):**

```latex
\documentclass[12pt,a4paper]{article}
\input{preambulo/pacotes}
\input{preambulo/estilo}
\input{preambulo/comandos}

\begin{document}
  \input{frontmatter/capa}
  \input{frontmatter/resumo}
  \input{frontmatter/sumario}

  \input{secoes/01-introducao}
  \input{secoes/02-por-que-existe}
  % ... demais seções ...
  \input{secoes/13-conclusao}

  \printbibliography   % ou \bibliography{...} conforme a Seção 7
\end{document}
```

**Pacotes previstos (`pacotes.tex`):**

- Base/idioma: `inputenc`/`fontenc` (ou compilar com LuaLaTeX/XeLaTeX e `fontspec`), `babel` com `brazil`.
- Tipografia: `microtype`, fonte limpa (ex.: `libertinus` ou `lmodern`).
- Layout: `geometry`, `titlesec` (títulos de seção com cara de artigo), `parskip` (opcional), `setspace`.
- Cor e caixas didáticas: `xcolor`, `tcolorbox` (caixas de "Ideia-chave", "Passo a passo", "Atenção").
- Figuras: `graphicx`, `tikz` (+ bibliotecas `trees`, `positioning`, `arrows.meta`, `shapes`), `subcaption`, `float`.
- Domínio do tema: `chessboard`/`xskak` (tabuleiro das rainhas), `sudoku` (grade de Sudoku), `algorithm2e` ou `algpseudocode` (se quisermos pseudocódigo, sem inventar conteúdo novo).
- Animação no PDF (opcional): `animate`.
- Links e bibliografia: `hyperref` (com `hidelinks`), `biblatex` (estilo ABNT) ou `bibtex`.

> ✅ **Definido:** classe `article` moderna com `titlesec` (ver Seção 9).

---

## 3. Identidade visual e regras de estilo (`estilo.tex` + `comandos.tex`)

Para "subir de nível" e parecer artigo:

- **Paleta de cores** consistente, reutilizada em todas as figuras TikZ (ex.: um azul para "decisão", verde para "válido", vermelho para "podado/inválido", cinza para "não explorado"). Isso conecta visualmente todas as ilustrações.
- **Títulos de seção** estilizados com `titlesec` (numeração discreta, fonte de peso forte, regra fina).
- **Caixas didáticas** com `tcolorbox`, usadas de forma recorrente (sem alterar texto, apenas realçando trechos que já existem):
  - `\ideiachave{...}` para a frase central de cada conceito;
  - `\passos{...}` para listas de etapas (ex.: as 4 etapas da Seção 3, a sequência "Escolhe/Testa/Avança/Erra/Volta" da Seção 6);
  - `\atencao{...}` para limitações.
- **Legendas de figura** padronizadas em português, mantendo o texto das legendas atuais ("Figura 1 ...", etc.).
- **Regra do travessão**: comando de revisão para garantir que nenhum `---` exista no fonte.

---

## 4. Capa em formato de artigo (`capa.tex`)

Hoje a primeira página é uma **folha de rosto acadêmica** (PUC-SP, disciplina, alunos, professora, cidade, ano). Você pediu para **formatar a capa como artigo**. Proposta:

- Substituir a folha de rosto por um **cabeçalho de artigo**:
  - **Título** em destaque + **subtítulo** ("Resolvendo problemas através da exploração de possibilidades").
  - Linha de **autores** (César José Santana da Silva; segundo autor a confirmar) com RA em nota de rodapé.
  - **Afiliação**: PUC-SP, Ciência da Computação, disciplina Algoritmos em Grafos, Profa. Lisbete Madsen Barbosa.
  - Logo da PUC-SP (`image2.png`) discreto no topo, não dominando a página.
  - Data (2026).
- O **Resumo** e as **Palavras-chave** entram logo abaixo do bloco de título, como em artigos (não em página separada).

> **Observação:** todos esses dados **já existem** no documento; estamos só reorganizando a apresentação, não inventando informação. O segundo aluno está em branco no original (campos "Aluno 2 / RA" vazios), então deixaremos um marcador até você preencher.

> ✅ **Definido:** cabeçalho de artigo, sem folha de rosto ABNT tradicional (ver Seção 9).

---

## 5. Sumário ("summary")

Decisão tomada: **os dois**. Plano:

- **Sumário/índice:** inserir `\tableofcontents` logo após o resumo (arquivo `sumario.tex`), gerado automaticamente a partir dos títulos de seção.
- **Quadro-resumo executivo:** uma caixa `tcolorbox` em destaque, resumindo o artigo em poucas linhas, **construída a partir de frases que já existem no texto** (Resumo + Conclusão), sem inventar conteúdo novo.
- Opcional (deixa com cara de artigo de revista): uma pequena infografia de **"mapa do artigo"** em TikZ, mostrando o fluxo Intuição → Conceitos → Exemplo prático → Conclusão. É elemento visual, não texto novo.

---

## 6. Visualizações: o coração do "próximo nível"

Princípio: **toda explicação de processo ou de matemática ganha uma representação visual**.

**Decisão (2026-06-13):** as imagens atuais do `.docx` **não serão reaproveitadas** (genéricas demais). Em vez disso, cada figura entra como um **placeholder descritivo** no LaTeX, isto é, uma caixa visível que descreve a imagem/fluxograma desejado e reserva o espaço com a legenda correta. As figuras finais (estáticas para o PDF e GIFs para a web) são produzidas em fase posterior.

O placeholder é gerado pelo comando `\figuraplaceholder{rótulo}{legenda}{descrição do que a figura deve mostrar}` (definido em `comandos.tex`).

| # | Seção | O que a figura final deve mostrar (descrição do placeholder) | Animação (web) |
|---|---|---|---|
| V1 | 1. Introdução | Labirinto com um ponto de decisão destacado e um beco sem saída, com seta de retorno ao último ponto de bifurcação | GIF percorrendo o labirinto e recuando no beco |
| V2 | 2. Por que existe | **Explosão combinatória**: árvore ramificando + contagem crescente, destacando `3×3×3×3 = 81` e `10⁸` | Animação contando ramos crescendo |
| V3 | 3. O que é | Fluxograma cíclico das 4 etapas: escolher → validar → avançar → voltar | GIF do ciclo girando |
| V4 | 4. Espaço de busca | Árvore de decisões limpa: nós = decisões, ramos = escolhas, com um caminho destacado | GIF percorrendo a árvore em profundidade |
| V5 | 5. Soluções parciais | Sequência de 4 quadros mostrando `(3) → (3,1) → (3,1,4) → (3,1,4,2)` sendo construída | GIF montando a sequência |
| V6 | 6. Retrocesso | Mini-árvore com um ramo inválido e a seta de retorno ("Erra → Volta → Tenta de novo") destacada | GIF do recuo na árvore |
| V7 | 7. Poda | Árvore com ramos viáveis (verde), inviáveis (vermelho) e não explorados (cinza); ícone de tesoura cortando uma subárvore | GIF cortando o ramo e sumindo a subárvore |
| V8 | 8. Aplicações | Grade de Sudoku com uma célula em conflito destacada e a correção indicada | GIF preenchendo e corrigindo uma célula |
| V9 | 10. Resolvendo 4 Rainhas | Tabuleiro 4×4 com a solução `V=(3,1,4,2)` e as anotações coluna→linha | GIF posicionando rainha a rainha |
| V10 | 11. Árvore das 4 Rainhas | Árvore de busca das 4 Rainhas marcando ramos podados (vermelho) e a solução (verde) | GIF expandindo a árvore com recuos |

Notas:
- **Paleta consistente** entre todas as figuras (azul = decisão, verde = válido, vermelho = podado/inválido, cinza = não explorado), definida em `estilo.tex`.
- **Animação no PDF (opcional):** o pacote `animate` consegue embutir sequências como animação que roda no Adobe Reader. Por padrão, no PDF entregamos a **sequência de quadros lado a lado**; a animação "de verdade" fica na versão web.
- Nada disso muda o **texto**; são ilustrações do que o texto já descreve.

---

## 7. Referências e citações

- Migrar as 5 referências (GeeksforGeeks, NEPS Academy, MIT OCW ×2, Wikipedia) para um arquivo `referencias.bib`.
- Usar `biblatex` com estilo **ABNT** (`biblatex-abnt`) para citações e lista final no padrão brasileiro, **mantendo exatamente os mesmos dados** (autor/instituição, título, URL, data de acesso).
- `hyperref` deixa os links clicáveis no PDF e na versão web.

---

## 8. Versão "notebook" publicável (resposta à sua pergunta)

Sim, dá. Três rotas, da mais alinhada ao seu pedido para a menos:

1. **Quarto (recomendado).** Fonte única `.qmd` que entende LaTeX/Markdown e gera **PDF (via LaTeX, para o Overleaf/impressão)** *e* **HTML publicável** com GIFs e até animações interativas. Tem cara de notebook, publica fácil (GitHub Pages, Quarto Pub, Netlify). Vantagem: um só conteúdo, duas saídas, math em LaTeX preservada.
2. **LaTeX puro → HTML.** Manter o projeto LaTeX e converter para web com `make4ht`/`LaTeXML`. Bom para fidelidade ao PDF, porém animações ficam limitadas (entram como GIF embutido).
3. **Jupyter Book.** Estilo notebook nativo, ótimo para web, mas o PDF fica menos "artigo" e exige reescrever a fonte fora do padrão LaTeX que você quer no Overleaf.

> ✅ **Definido: Quarto.** Começar pelo **LaTeX no Overleaf** (entrega principal) e, em paralelo, manter uma versão **Quarto** que reaproveita o mesmo texto e as mesmas figuras, adicionando os GIFs só na saída HTML. Assim você tem o artigo em PDF e um link publicável com as animações.

---

## 9. Decisões (resolvidas em 2026-06-13)

- **A. Estilo do documento:** ✅ **`article` moderno e limpo** com `titlesec`, tipografia refinada (cara de artigo de revista).
- **B. Capa/ABNT:** ✅ decorrência de A — **cabeçalho de artigo** (sem folha de rosto ABNT tradicional). Ver Seção 4.
- **C. "Summary":** ✅ **Os dois** — `\tableofcontents` (Sumário/índice) **e** um quadro-resumo executivo em destaque. Ver Seção 5.
- **D. Versão web:** ✅ **Quarto** — fonte que gera PDF (via LaTeX) e HTML publicável com GIFs.
- **E. Recriar figuras em TikZ:** recriar vetorialmente V4, V7, V10; criar novas V2, V3, V5, V6, V9; manter raster V1, V8. (Confirmar pontualmente durante a execução.)
- **F. Reordenação:** ✅ **Aplicar** — ver Seção 10 (fluxo `1→2→3→4→5→6→7→9→10→11→8→12→13`).
- **G. Segundo autor:** ✅ resolvido — **RA não é necessário**. Usar apenas nomes dos autores no cabeçalho.
- **H. Imagens:** ✅ **não reaproveitar as imagens atuais** (genéricas demais). Cada figura vira um **placeholder descritivo** (uma caixa com a descrição da imagem/fluxograma desejado), a ser produzido depois. Ver Seção 6.

---

## 10. Sugestão de reordenação (opcional)

A ordem atual já é boa e didática. Uma única melhora de narrativa que sugiro:

- **Mover a Seção 8 (Aplicações Práticas / Sudoku) para depois da Seção 11** (depois do exemplo completo das 4 Rainhas).
- Racional: o leitor primeiro **constrói a intuição** (1–7), depois vê **um exemplo completo de ponta a ponta** (9–11, as 4 Rainhas), e só então **amplia para onde mais se usa** (Sudoku e demais aplicações). Fecha com vantagens/limitações (12) e conclusão (13).
- Fluxo final sugerido: `1 → 2 → 3 → 4 → 5 → 6 → 7 → 9 → 10 → 11 → 8 → 12 → 13`.
- Isso é só **ordem de apresentação**; nenhum conteúdo é alterado. Mantém-se totalmente opcional: se preferir, ficamos com a ordem original.

---

## 11. Ordem de execução proposta (passo a passo, fase seguinte)

1. **(este passo)** Criar o esqueleto do projeto (Seção 2) e definir `pacotes/estilo/comandos`, incluindo o comando `\figuraplaceholder`.
2. Montar capa (4), resumo, sumário e quadro-resumo (5).
3. Transcrever as 13 seções para os arquivos modulares, **idênticas em conteúdo**, aplicando estilo, caixas e a regra do travessão, na ordem reordenada (Seção 10).
4. Inserir os **placeholders de figura** (V1–V10) com legendas em português nos pontos certos.
5. Montar a bibliografia (7).
6. Compilar e revisar o PDF no Overleaf.
7. Produzir as figuras finais (estáticas) e substituir os placeholders, uma a uma.
8. Gerar a versão web/notebook em Quarto (8) reaproveitando texto e figuras, adicionando GIFs.

---

### Observação sobre as imagens do `.docx`
- As imagens originais (extraídas em `unpacked/word/media/`) **não serão usadas** no projeto final. Servem apenas como referência histórica do que cada figura tentava ilustrar. As figuras finais serão produzidas do zero (placeholders por enquanto).
