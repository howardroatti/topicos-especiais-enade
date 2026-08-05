# Tópicos Especiais II — ENADE · FAESA

Material didático da disciplina **Tópicos Especiais II — ENADE** (revisão para o ENADE dos cursos de **Ciência da Computação** e **Sistemas de Informação**), do Prof. M.Sc. **Howard Cruz Roatti** — FAESA Centro Universitário · 2026/2.

🌐 **Sumário (vivo):** https://howardroatti.github.io/topicos-especiais-enade/

Cada aula traz um **Esquenta** com questões no estilo do ENADE (situação-problema → alternativas → gabarito comentado) e a revisão de conteúdos do componente específico. As áreas de revisão são **Banco de Dados**, **Análise de Dados Aplicada à Computação** e **Sistemas Distribuídos**.

## Estrutura

```
aulas/    slides das aulas (Marp): .md (fonte), .html e .pdf
themes/   tema visual FAESA (faesa.css)
index.html   sumário vivo (cresce a cada aula)
build.sh     renderiza os decks (.md → .html) com o tema FAESA
```

## Como gerar os slides

Requer [`@marp-team/marp-cli`](https://github.com/marp-team/marp-cli) (e, opcionalmente, `@mermaid-js/mermaid-cli` para diagramas).

```bash
./build.sh                       # renderiza todos os decks em aulas/
./build.sh aulas/aula-01-....md  # renderiza um deck específico
```

## Licença

Conteúdo sob [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.pt-br).
