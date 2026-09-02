---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2 · [☰ Sumário](../index.html)'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Aulão de Banco de Dados
## Agrupar e agregar — pensar em conjuntos

**Tópicos Especiais II** · ENADE · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## A pergunta de hoje

Você já escreve `SELECT`, `WHERE` e `JOIN`. Aí chega esta pergunta simples:

<div class="dica">🧾 "Temos uma tabela com <strong>uma venda por linha</strong>. Quanto <strong>cada loja</strong> faturou?"</div>

- A consulta **linha a linha** não responde: ela devolve **as vendas**, não **o total por loja**.
- Falta uma ferramenta para **resumir muitos registros em poucos**.

<div class="aviso">🎯 Hoje a gente monta essa ferramenta do zero: <code>GROUP BY</code>, funções de agregação, <code>HAVING</code> e <code>ORDER BY</code>.</div>

---

## A virada de chave

<div class="cols">
<div>

**Jeito procedural** (de quem programa)
Percorrer **uma linha de cada vez** e ir somando numa variável.
`for venda in vendas: total[loja] += venda`

</div>
<div>

**Jeito do SQL** (declarativo)
Você **não percorre** nada. Descreve **grupos** e o que quer de **cada grupo**.
"Para **cada loja**, a **soma** dos valores."

</div>
</div>

<div class="dica">💡 A ideia-mãe: a tabela é um <strong>monte de linhas</strong> → você as separa em <strong>baldes</strong> (grupos) → e pede <strong>um número por balde</strong>. Pensar em <strong>conjuntos</strong>, não em laços.</div>

---

## Nossa tabela de exemplo — `VENDAS`

<div class="cols">
<div>

| loja | vendedor | valor |
|--|--|--|
| Norte | Ana | 100 |
| Norte | Bia | 50 |
| Sul | Caio | 200 |
| Sul | Duda | 80 |
| Leste | Edu | 30 |

</div>
<div>

**Uma venda por linha.**
Cinco linhas, três lojas.

Vamos responder, passo a passo:
1. quanto faturou **no total**?
2. quanto faturou **cada loja**?
3. e **só** as lojas grandes?
4. da **maior** para a menor?

</div>
</div>

---

## Passo 1 — resumir a tabela inteira

Uma **função de agregação** engole **muitas linhas** e devolve **uma**:

```sql
SELECT SUM(valor), COUNT(*), AVG(valor) FROM VENDAS;
```

| SUM(valor) | COUNT(*) | AVG(valor) |
|--|--|--|
| 460 | 5 | 92 |

<div class="dica">💡 Sem <code>GROUP BY</code>, a tabela toda é <strong>um único grupo</strong> → uma linha de resposta. <code>SUM</code> soma, <code>COUNT</code> conta, <code>AVG</code> tira a média, <code>MIN</code>/<code>MAX</code> pegam extremos.</div>

---

## Passo 2 — `GROUP BY`: um resumo por grupo

`GROUP BY loja` separa as linhas em **baldes** e aplica a função em **cada um**:

<div class="cols">
<div>

**Entram (agrupadas por cor)**
<table style="font-size:15px">
<tr><th>loja</th><th>valor</th></tr>
<tr style="background:#e7effa"><td>Norte</td><td>100</td></tr>
<tr style="background:#e7effa"><td>Norte</td><td>50</td></tr>
<tr style="background:#fdeccf"><td>Sul</td><td>200</td></tr>
<tr style="background:#fdeccf"><td>Sul</td><td>80</td></tr>
<tr style="background:#d7f4df"><td>Leste</td><td>30</td></tr>
</table>

</div>
<div>

**Saem** — `GROUP BY loja` + `SUM`
<table style="font-size:15px">
<tr><th>loja</th><th>SUM(valor)</th></tr>
<tr style="background:#e7eeff"><td>Norte</td><td><strong>150</strong></td></tr>
<tr style="background:#fdeccf"><td>Sul</td><td><strong>280</strong></td></tr>
<tr style="background:#d7f4df"><td>Leste</td><td><strong>30</strong></td></tr>
</table>

</div>
</div>

<div class="dica">💡 Cada <strong>cor</strong> vira <strong>uma linha</strong>. Cinco linhas entraram, três saíram — uma por grupo.</div>

---

## A regra de ouro (ela nasce aqui)

No `SELECT`, **cada coluna** ou está no `GROUP BY`, ou está **dentro de uma função** de agregação.

```sql
SELECT loja, SUM(valor) FROM VENDAS GROUP BY loja;   -- ✅ loja agrupa, valor agrega
```

**E se eu jogar `valor` no `GROUP BY` também?**

```sql
SELECT loja, SUM(valor) FROM VENDAS GROUP BY loja, valor;   -- ⚠️
```

<div class="aviso">⚠️ Agora cada <strong>par (loja, valor)</strong> é um grupo → volta a <strong>uma linha por valor</strong>, e a soma vira o próprio valor. A totalização <strong>some</strong> — e o banco aceita numa boa. Por isso a regra: <strong>agrupa-se pelo que NÃO está agregado</strong>.</div>

---

## Vote no ar 🖐️ — contexto novo, mesma ideia

<div class="cols">
<div>

Nova tabela `GOLS(time, jogador, gols)`:
<table style="font-size:15px">
<tr><th>time</th><th>jogador</th><th>gols</th></tr>
<tr style="background:#e7effa"><td>Leões</td><td>Rui</td><td>2</td></tr>
<tr style="background:#e7effa"><td>Leões</td><td>Téo</td><td>1</td></tr>
<tr style="background:#fdeccf"><td>Tigres</td><td>Vin</td><td>3</td></tr>
<tr style="background:#fdeccf"><td>Tigres</td><td>Zeca</td><td>1</td></tr>
</table>

</div>
<div>

Qual dá o **total de gols por TIME**?

```sql
-- 1
SELECT time, SUM(gols)
FROM GOLS
GROUP BY time;
-- 2
SELECT time, SUM(gols)
FROM GOLS
GROUP BY time, jogador;
```

</div>
</div>

<div class="dica">🖐️ <strong>1 ou 2?</strong> Antes de decidir: <strong>o que é "um balde" aqui?</strong></div>

---

## Vote no ar 🖐️ — a resposta

<div class="cols">
<div>

**Consulta 1** — `GROUP BY time` ✅
<table style="font-size:15px">
<tr><th>time</th><th>SUM(gols)</th></tr>
<tr style="background:#e7eeff"><td>Leões</td><td><strong>3</strong></td></tr>
<tr style="background:#fdeccf"><td>Tigres</td><td><strong>4</strong></td></tr>
</table>

Um balde por <strong>time</strong> → total <strong>por time</strong>.

</div>
<div>

**Consulta 2** — `GROUP BY time, jogador` ❌
<table style="font-size:15px">
<tr><th>time</th><th>jogador</th><th>SUM</th></tr>
<tr style="background:#e7eeff"><td>Leões</td><td>Rui</td><td>2</td></tr>
<tr style="background:#e7eeff"><td>Leões</td><td>Téo</td><td>1</td></tr>
<tr style="background:#fdeccf"><td>Tigres</td><td>Vin</td><td>3</td></tr>
<tr style="background:#fdeccf"><td>Tigres</td><td>Zeca</td><td>1</td></tr>
</table>

</div>
</div>

<div class="dica">💡 Pôr <code>jogador</code> no <code>GROUP BY</code> <strong>muda o balde</strong> → total por jogador, não por time. A regra de novo: agrupa-se só pelo que <strong>não está agregado</strong> (aqui, só <code>time</code>).</div>

---

## Passo 3 — `WHERE` × `HAVING`

Os dois filtram — mas em **momentos diferentes**:

<div class="cols">
<div>

**`WHERE`** → filtra **LINHAS**
*antes* de agrupar.
`WHERE valor >= 50`
(descarta a venda de 30 **antes** da soma)

</div>
<div>

**`HAVING`** → filtra **GRUPOS**
*depois* de agrupar.
`HAVING SUM(valor) > 100`
(descarta a loja cujo **total** ≤ 100)

</div>
</div>

```sql
SELECT loja, SUM(valor) FROM VENDAS
GROUP BY loja
HAVING SUM(valor) > 100;      -- só Norte (150) e Sul (280); Leste (30) cai
```

<div class="dica">💡 Regra prática: condição sobre <strong>coluna</strong> → <code>WHERE</code>;<br>condição sobre <strong>resultado de agregação</strong> (<code>SUM</code>, <code>COUNT</code>…) → <code>HAVING</code>.</div>

---

## Passo 4 — `ORDER BY` pela agregação

Dá para ordenar **pelo número que você calculou**:

```sql
SELECT loja, SUM(valor) AS total FROM VENDAS
GROUP BY loja
ORDER BY total DESC;          -- Sul 280, Norte 150, Leste 30
```

| loja | total |
|--|--|
| Sul | 280 |
| Norte | 150 |
| Leste | 30 |

<div class="dica">💡 <code>ORDER BY SUM(valor) DESC</code> ou <code>ORDER BY total DESC</code> (pelo apelido) — os dois funcionam.</div>

---

## A consulta inteira — ordem de escrita × de execução

```sql
SELECT   loja, SUM(valor) AS total     -- 5º: escolhe o que aparece
FROM     VENDAS                         -- 1º: de onde vêm as linhas
WHERE    valor >= 50                    -- 2º: filtra LINHAS
GROUP BY loja                           -- 3º: forma os GRUPOS
HAVING   SUM(valor) > 100               -- 4º: filtra GRUPOS
ORDER BY total DESC;                    -- 6º: ordena o resultado
```

<div class="aviso">📌 Você <strong>escreve</strong> nessa ordem, mas o banco <strong>executa</strong> assim: <code>FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY</code>. É por isso que o <code>HAVING</code> pode usar <code>SUM</code> e o <code>WHERE</code> não.</div>

---

<!-- _class: secao -->

# Agora vocês 🤝

---

## Desafios — em grupos

<div class="cols">
<div>

Tabela `VENDAS`:
<table style="font-size:15px">
<tr><th>loja</th><th>vendedor</th><th>valor</th></tr>
<tr style="background:#e7effa"><td>Norte</td><td>Ana</td><td>100</td></tr>
<tr style="background:#e7effa"><td>Norte</td><td>Bia</td><td>50</td></tr>
<tr style="background:#fdeccf"><td>Sul</td><td>Caio</td><td>200</td></tr>
<tr style="background:#fdeccf"><td>Sul</td><td>Duda</td><td>80</td></tr>
<tr style="background:#d7f4df"><td>Leste</td><td>Edu</td><td>30</td></tr>
</table>

</div>
<div>

Escrevam a consulta:

1. **Quantas vendas** cada vendedor fez? *(`COUNT`)*
2. **Faturamento por loja**, só as que passaram de **100**.
3. A **loja campeã** *(uma linha só)*.

</div>
</div>

<div class="dica">💡 Comecem pela pergunta "<strong>o que é um grupo aqui?</strong>" — é o que vai no <code>GROUP BY</code>.</div>

---

## Desafios — gabarito

```sql
-- 1) vendas por vendedor
SELECT vendedor, COUNT(*) FROM VENDAS GROUP BY vendedor;

-- 2) faturamento por loja, acima de 100
SELECT loja, SUM(valor) FROM VENDAS
GROUP BY loja HAVING SUM(valor) > 100;

-- 3) loja campeã
SELECT loja, SUM(valor) AS total FROM VENDAS
GROUP BY loja ORDER BY total DESC
LIMIT 1;                       -- (no Oracle: FETCH FIRST 1 ROW ONLY)
```

<div class="dica">💡 Reparem: <strong>o que muda</strong> entre eles é só o <code>GROUP BY</code> e o filtro/ordenação — a estrutura é a mesma.</div>

---

## Como isso cai no ENADE

Banco de eleição: `Partido(numero, nome)`, `Votacao(partido, votos, estado)`. Queremos o **total de votos por partido**. Assinale a consulta correta.

```sql
-- A
SELECT p.nome, SUM(v.votos) FROM Partido p, Votacao v
WHERE v.partido = p.numero GROUP BY p.nome;
-- B
SELECT p.nome, SUM(v.votos) FROM Partido p, Votacao v
WHERE v.partido = p.numero GROUP BY p.nome, v.votos;
```

<div class="dica">💡 É a <strong>mesma ideia</strong> de hoje: <code>SUM</code> totaliza e o <code>GROUP BY</code> leva só as colunas <strong>não agregadas</strong>. Agrupar por <code>v.votos</code> (B) quebraria a soma → a correta é <strong>A</strong>.</div>

---

<!-- _class: secao -->

# Bloco 2 · Junção
### Combinar tabelas — pensar em conjuntos

---

## Junção como conjunto

Combinar linhas de **duas tabelas** pela condição de **casamento** (`ON`):

<div class="cols">
<div>

`CLIENTE`
| id | nome |
|--|--|
| 1 | Ana |
| 2 | Bruno |
| 3 | Caio |

</div>
<div>

`PEDIDO`
| id | id_cliente | valor |
|--|--|--|
| 10 | 1 | 150 |
| 11 | 1 | 80 |
| 12 | 2 | 200 |

</div>
</div>

<div class="dica">💡 <strong>Caio não pediu nada.</strong> É a diferença entre os dois tipos — vamos ver a saída de cada um.</div>

---

## Junção — as duas saídas

<div class="cols">
<div>

`INNER JOIN` — só quem **casa**
<table style="font-size:15px">
<tr><th>nome</th><th>pedido</th><th>valor</th></tr>
<tr><td>Ana</td><td>10</td><td>150</td></tr>
<tr><td>Ana</td><td>11</td><td>80</td></tr>
<tr><td>Bruno</td><td>12</td><td>200</td></tr>
</table>

Caio <strong>fica de fora</strong>.

</div>
<div>

`CLIENTE LEFT JOIN PEDIDO`
<table style="font-size:15px">
<tr><th>nome</th><th>pedido</th><th>valor</th></tr>
<tr><td>Ana</td><td>10</td><td>150</td></tr>
<tr><td>Ana</td><td>11</td><td>80</td></tr>
<tr><td>Bruno</td><td>12</td><td>200</td></tr>
<tr style="background:#fdeaea"><td>Caio</td><td>NULL</td><td>NULL</td></tr>
</table>

</div>
</div>

<div class="dica">💡 A diferença é <strong>só o Caio</strong>: o <code>LEFT</code> preserva quem <strong>não casou</strong>, preenchendo com <code>NULL</code>. (<code>RIGHT</code> é o mesmo, do outro lado.)</div>

---

## Agora vocês — junção 🤝

Novo caso — `AUTOR` e `LIVRO`:

<div class="cols">
<div>

`AUTOR`
| id | nome |
|--|--|
| 1 | Machado |
| 2 | Clarice |
| 3 | Rui |

</div>
<div>

`LIVRO`
| id | id_autor | titulo |
|--|--|--|
| 100 | 1 | Dom Casmurro |
| 101 | 1 | Quincas Borba |
| 102 | 2 | A Hora da Estrela |

</div>
</div>

**Escrevam:** 1) todos os autores e seus livros, **inclusive quem não publicou**; 2) autores **sem livro**; 3) **quantos livros** cada autor tem *(inclusive 0)*.

---

## Junção — gabarito

```sql
-- 1) todos os autores + livros (Rui aparece com NULL)
SELECT a.nome, l.titulo
FROM AUTOR a LEFT JOIN LIVRO l ON l.id_autor = a.id;

-- 2) autores sem livro → só Rui
SELECT a.nome
FROM AUTOR a LEFT JOIN LIVRO l ON l.id_autor = a.id
WHERE l.id IS NULL;

-- 3) quantos livros por autor (junção + agrupamento)
SELECT a.nome, COUNT(l.id) AS qtd
FROM AUTOR a LEFT JOIN LIVRO l ON l.id_autor = a.id
GROUP BY a.nome;
```

<div class="dica">💡 No item 3, use <code>COUNT(l.id)</code>, <strong>não</strong> <code>COUNT(*)</code>: a linha do Rui tem <code>l.id = NULL</code>, então <code>COUNT(*)</code> contaria <strong>1</strong> indevidamente. Junção + agregação juntas — é assim que cai.</div>

---

<!-- _class: secao -->

# Bloco 3 · Modelagem
### Da cardinalidade à chave estrangeira

---

## Cardinalidade vira chave estrangeira

`(mín, máx)`: o **primeiro** é o mínimo, o **segundo** o máximo.

- `(1,1)` = obrigatório e único
- `(0,1)` = **opcional** e único
- `(0,N)` / `(1,N)` = vários
- No **mínimo 0**, a FK **aceita nulo**; no mínimo 1, a FK é **NOT NULL**.

<div class="aviso">⚠️ Pegadinha clássica: ler o mínimo <strong>0</strong> de <code>(0,1)</code> como se fosse obrigatório. "No máximo uma" <strong>não</strong> é "exatamente uma".</div>

---

## Modelagem — exemplo resolvido

> "Um **PEDIDO** tem **exatamente um** cliente; um **CLIENTE** tem de **0 a N** pedidos."

1. Cardinalidade: **PEDIDO (1,1)** · **CLIENTE (0,N)** → é um **1:N**.
2. A FK vai no lado **N**: `PEDIDO.id_cliente`.
3. Mínimo **1** (todo pedido tem cliente) → a FK é **NOT NULL**.

<div class="dica">💡 Roteiro: leia as duas cardinalidades → ache o lado <strong>N</strong> (a FK entra lá) → veja o <strong>mínimo</strong> desse lado: <strong>0</strong> aceita nulo, <strong>1</strong> é <code>NOT NULL</code>.</div>

---

## Agora vocês — modelagem 🤝

Novo caso:

> "Cada **LIVRO** tem **no máximo uma** editora `(0,1)`; uma **EDITORA** publica de **0 a N** livros."

1. Cardinalidade `(mín, máx)` de **cada lado**?
2. Em **qual tabela** entra a **FK**?
3. Essa FK **aceita nulo**?

---

## Modelagem — gabarito

1. **LIVRO (0,1)** · **EDITORA (0,N)** → é um **1:N**.
2. A FK vai no lado **N**: `LIVRO.id_editora`.
3. **Sim** — mínimo **0** (um livro pode não ter editora) → a FK **aceita NULL**.

<div class="dica">💡 Compare com o resolvido: lá o mínimo era <strong>1</strong> (FK <code>NOT NULL</code>); aqui é <strong>0</strong> (FK <strong>aceita nulo</strong>). <strong>O mínimo é o que decide.</strong></div>

---

## Fecho — leve isto na prova

<div class="dica">💡 <strong>Agregação em uma frase:</strong> forme os grupos com <code>GROUP BY</code>, resuma cada um com uma função (<code>SUM</code>/<code>AVG</code>/<code>COUNT</code>), <strong>agrupe pelo que não está agregado</strong>, filtre grupos com <code>HAVING</code> e ordene com <code>ORDER BY</code>.</div>

**Para revisar por conta — decks de BD:**

<div class="cols">
<div>

- [**Normalização**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/04-modelagem/normalizacao.html) (muito recorrente!)
- [**Transações e ACID**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/06-transacoes/transacoes.html)
- [**Concorrência / isolamento**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/06-transacoes/concorrencia-recuperacao.html)

</div>
<div>

- [**Índices**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/03-relacional/views-sql-indexacao.html) (Views, SQL e Indexação)
- [**Álgebra relacional**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/03-relacional/algebra-relacional.html)
- [**NoSQL e CAP**](https://howardroatti.github.io/banco-de-dados-faesa/unidades/07-nosql/nosql-conceitos.html)

</div>
</div>

---

<!-- _class: secao -->

# Bons estudos! 🎯
### howard.cruz@faesa.br

<a class="proximo" href="../index.html">☰ Índice<small>Tópicos Especiais II</small></a>
<a class="proximo" href="aula-02-banco-de-dados.html">Aula 2 · Banco de Dados<small>revisão completa</small></a>
