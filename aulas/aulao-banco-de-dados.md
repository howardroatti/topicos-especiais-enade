---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2 · [☰ Sumário](../index.html)'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Aulão de Banco de Dados
## ENADE — a partir do Simulado 2026-1

**Tópicos Especiais II** · ENADE · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## O diagnóstico, em uma frase

Banco de Dados caiu **só em SI e ADS** (3 itens cada) — e os dois estão em velocidades muito diferentes:

<div class="cols">
<div>

**SI — 83,3%**
Conceito de pé. Faltam **pontos finos**.

</div>
<div>

**ADS — 47,1%**
Um **buraco** claro, concentrado.

</div>
</div>

<div class="dica">💡 O eixo do aulão sai limpo dos dados: <strong>o problema não é junção nem subconsulta — é agregação e agrupamento</strong> (<code>GROUP BY</code>, <code>SUM</code>, <code>AVG</code>).</div>

---

## Abertura — votem no ar 🖐️

Banco de eleição: `Candidato(numero, nome)`, `Partido(numero, nome, sigla)`, `Votacao(partido, votos, estado)`. Queremos **o total de votos de cada partido/candidato**. Todas partem da **mesma base** — muda só o destacado:

```sql
SELECT c.nome, p.nome, «AGREGADO»  FROM Partido p, Candidato c, Votacao v
WHERE c.numero = p.numero AND v.partido = c.numero  «AGRUPAMENTO»;
```

| | «AGREGADO» | «AGRUPAMENTO» |
|--|--|--|
| **A** | `COUNT(v.votos)` | `GROUP BY c.nome, p.nome` |
| **B** | `SUM(v.votos)` | `GROUP BY c.nome, p.nome` |
| **C** | `SUM(v.votos)` | *(sem `GROUP BY`)* |
| **D** | `SUM(v.votos)` | `GROUP BY c.nome, p.nome, v.votos` |

<div class="aviso">🖐️ <strong>A, B, C ou D?</strong> Guardem a resposta. Voltamos a ela em 3 minutos.</div>

---

## O contraste que orienta a aula

<div class="cols">
<div>

**SI · Q14 — subconsulta IN tripla**
`SELECT ... WHERE idMoto IN (SELECT ... IN (SELECT ...))`
### 100% de acerto
Três níveis aninhados **não derrubaram ninguém**.

</div>
<div>

**ADS · Q16 — SUM com GROUP BY**
A consulta de agregação da abertura.
### 6% de acerto
**1 acerto em 17.** 12 na mesma errada.

</div>
</div>

<div class="dica">💡 Por que o "mais difícil" foi o mais fácil? <strong>Subconsulta é procedural</strong> — resolve de dentro para fora, como código. <strong>Agregação é declarativa</strong> — exige pensar em <strong>conjuntos</strong>. É aí que a intuição de quem programa falha.</div>

---

## Roteiro de hoje

| # | Item | Assunto | Tempo |
|--|--|--|--|
| 1 | ADS Q16 | `SUM` com `GROUP BY` | 15 min |
| 2 | ADS Q17 | `AVG`, `GROUP BY` e `ORDER BY` | 12 min |
| 3 | SI Q15 | `JOIN` com apelidos e coluna ambígua | 8 min |
| 4 | ADS Q19 | Modelo ER e chave candidata | 7 min |
| 5 | SI Q13 | `RIGHT` × `LEFT` × `INNER JOIN` | 6 min |
| 6 | ADS Q23 | Diagrama de classes e multiplicidade | 3 min |

<div class="dica">💡 Núcleo em <strong>agregação</strong> (segura ADS); junção e modelagem entram como <strong>revisão rápida</strong> (para SI).</div>

---

<!-- _class: secao -->

# 1 · ADS Q16
### `SUM` com `GROUP BY` — vamos rodar as duas

---

## Q16 — rode as duas à mão

Seis linhas de `Votacao` e a saída de **cada** consulta:

<div class="cols">
<div>

**Dados (`Votacao`)**
| partido | votos |
|--|--|
| Alfa | 100 |
| Alfa | 50 |
| Alfa | 30 |
| Beta | 200 |
| Beta | 20 |

</div>
<div>

**B — `GROUP BY c.nome, p.nome`** ✅
| candidato | partido | SUM |
|--|--|--|
| Ana | Alfa | **180** |
| Bruno | Beta | **220** |

**D — `... , v.votos`** ❌
| candidato | partido | SUM |
|--|--|--|
| Ana | Alfa | 100 |
| Ana | Alfa | 50 |
| … | … | … |

</div>
</div>

<div class="aviso">⚠️ Agrupar <strong>também</strong> por <code>v.votos</code> cria <strong>um grupo para cada valor de voto</strong> → a soma vira o próprio valor. A totalização <strong>some</strong>, mas o banco aceita e devolve linhas.</div>

---

## Q16 — a regra (só agora) + gabarito **B**

<div class="dica">💡 <strong>Agrupa-se pelo que NÃO está agregado.</strong> As colunas do <code>SELECT</code> que não entram numa função (<code>SUM</code>, <code>AVG</code>…) vão <strong>todas</strong>, e só elas, no <code>GROUP BY</code>.</div>

- **B** ✅ — `SUM(v.votos)` totaliza; `GROUP BY c.nome, p.nome` dá o total por partido/candidato.
- **D** ❌ (12 alunos) — agrupar por `v.votos` anula a soma (o erro campeão).
- **A** ❌ — usa `COUNT` (conta linhas, não soma votos).
- **C** ❌ — `SUM` **sem** `GROUP BY` com colunas não agregadas → consulta inválida.

<div class="aviso">📌 O que o erro revela: quem marca D acha que <code>GROUP BY</code> "lista as colunas do <code>SELECT</code>". Enquanto essa ideia estiver de pé, <strong>toda</strong> totalização sai errada.</div>

---

<!-- _class: secao -->

# 2 · ADS Q17
### `AVG`, `GROUP BY` e `ORDER BY`

---

## Q17 — primeiro, em português

Banco bancário: `CLIENTE`, `CONTA`, `HISTORICO_MOVIMENTACAO`. Queremos **o nome de cada cliente e o valor médio movimentado por ele, do maior para o menor**.

<div class="aviso">🗣️ Antes de qualquer SQL: qual a diferença entre <strong>"o valor movimentado"</strong> e <strong>"a média por cliente"</strong>? Quem não enuncia isso não escreve o <code>GROUP BY</code> — por mais sintaxe que decore.</div>

<div class="cols">
<div>

**Sem agregar** (erro B, 4 alunos)
| cliente | valor |
|--|--|
| Bruno | 50 |
| Ana | 100 |
| Bruno | 150 |
| Ana | 200 |

</div>
<div>

**`AVG ... GROUP BY cliente`** ✅
| cliente | média |
|--|--|
| Ana | **150** |
| Bruno | **100** |

</div>
</div>

---

## Q17 — gabarito **A**

```sql
SELECT CL.NOME, AVG(HM.VAL_MOVIMENTADO)
FROM CLIENTE CL
  JOIN CONTA CO ON CL.COD_CLIENTE = CO.COD_CLIENTE
  JOIN HISTORICO_MOVIMENTACAO HM ON CO.NUM_CONTA = HM.NUM_CONTA
GROUP BY CL.COD_CLIENTE, CL.NOME
ORDER BY AVG(HM.VAL_MOVIMENTADO) DESC;   -- ordena pela própria agregação
```

- **A** ✅ — `AVG` + `GROUP BY` por cliente + `ORDER BY AVG(...) DESC`.
- **B** ❌ — lista os valores **individuais** (sem `AVG`, sem agrupar).
- **C** ❌ — `AVG` **sem** `GROUP BY`.
- **D** ❌ — junções erradas (colunas trocadas).

<div class="dica">💡 Sete dos dez erros de ADS foram de agregação — <strong>não</strong> de junção. E o item ainda cobra o passo seguinte: <strong>ordenar pela função de agregação</strong>.</div>

---

<!-- _class: secao -->

# 3 · SI Q15
### `JOIN`, apelidos e coluna ambígua

---

## Q15 — o conceito está de pé, faltam os finos

`Peca(CodPeca, NomePeca, ...)` e `Embarque(CodPeca, CodFornecedor, QuantidadeEmbarque)`. Queremos `CodPeca` e `NomePeca` das peças com `QuantidadeEmbarque > 100`.

```sql
-- A (correta)
SELECT P.CodPeca, P.NomePeca
FROM Peca P JOIN Embarque E ON P.CodPeca = E.CodPeca
WHERE E.QuantidadeEmbarque > 100;
```

<div class="aviso">🗣️ Pergunta que resolve as duas pegadinhas: por que <code>WHERE QuantidadeEmbarque > 100</code> <strong>sem qualificar</strong> às vezes funciona e às vezes não? (Obriga a pensar no <strong>esquema</strong>, não na consulta.)</div>

- **B** ❌ — `FROM Peca Embarque` lê `Embarque` como **apelido** de `Peca`.
- **C** ❌ — `CodPeca` **sem qualificar** é **ambíguo** (existe nas duas tabelas).
- **D** ❌ — `Embarque` só existe na subconsulta; referenciá-la no `SELECT` externo é **fora de escopo**.

---

<!-- _class: secao -->

# 4 · ADS Q19
### Modelo ER e chave candidata — a ponte para o SQL

---

## Q19 — leia a cardinalidade em voz alta

`pessoa` **possui** `cavalo`: cada pessoa possui **exatamente um** cavalo `(1,1)`; cada cavalo pertence a **no máximo uma** pessoa `(0,1)`.

<div class="dica">💡 Traduza cada número: o <strong>primeiro é o mínimo</strong>, o <strong>segundo é o máximo</strong>. <code>(0,1)</code> = "de zero a um" → <strong>opcional</strong>.</div>

- **C** ✅ — o `rg` identifica unicamente cada pessoa → pode ser **chave candidata**.
- **D** ❌ (3 alunos) — leram o **mínimo 0** de `(0,1)` como **obrigatório**; confundem "no máximo uma" com "exatamente uma".
- **A** ❌ — `(1,1)` limita a **um** cavalo por pessoa.
- **B** ❌ — `raca`/`eBento` são descritivos; a PK de `cavalo` é `codigo`.

<div class="aviso">📌 O que muda no esquema quando o mínimo é <strong>0</strong>? É onde entra a <strong>chave estrangeira que aceita nulo</strong> — modelagem virando SQL.</div>

---

<!-- _class: secao -->

# 5 · SI Q13
### `RIGHT` × `LEFT` × `INNER` — 30 segundos por junção

---

## Q13 — junção é operação de conjunto

Queremos **todas as linhas de Tabela2** e as correspondentes de Tabela1.

<div class="cols">
<div>

- **INNER** — só a **interseção**
- **LEFT** — tudo da **esquerda** + interseção
- **RIGHT** — tudo da **direita** + interseção

</div>
<div>

```sql
-- A (correta)
SELECT *
FROM Tabela1 t1
RIGHT JOIN Tabela2 t2
  ON t1.id = t2.fk;
```

</div>
</div>

- **C** ❌ (2 alunos) — `LEFT` preserva **Tabela1**, não Tabela2 (lado trocado).
- **D** ❌ — `INNER` devolve só a interseção.

<div class="dica">💡 Bônus (quase ninguém conhece): <code>RIGHT JOIN ... WHERE t1.id IS NULL</code> é o idioma para "<strong>o que existe de um lado e não do outro</strong>".</div>

---

## 6 · ADS Q23 — multiplicidade UML (não gastar aula)

Estudante 1..* Matrícula; cada Matrícula liga-se a um Curso (via Turma); Turma tem Horário e Professor. **Gabarito A** — 94,1% de acerto (16/17).

<div class="dica">💡 Use como <strong>argumento com a própria turma</strong>: vocês <strong>modelam bem</strong> (UML, multiplicidade, ER). O que falta é <strong>traduzir o modelo em consulta</strong> — que é exatamente a agregação de hoje.</div>

<div class="aviso">🔗 Aprofundar modelagem → decks de BD: <strong>Modelagem Conceitual (ER)</strong> e <strong>Lógica (→ tabelas)</strong>, com os exercícios integradores.</div>

---

## Fecho — a regra e o que estudar por conta

<div class="dica">💡 <strong>A frase do aulão:</strong> em agregação, <strong>agrupa-se pelo que não está agregado</strong>; funções (<code>SUM</code>/<code>AVG</code>/<code>COUNT</code>) resumem cada grupo; <code>HAVING</code> filtra grupos; <code>ORDER BY</code> pode ordenar pela própria agregação.</div>

**O simulado NÃO mediu (e o ENADE cobra) — revise nos decks de BD:**

<div class="cols">
<div>

- **Normalização** (o mais recorrente!) → deck *Normalização*
- **Transações e ACID** → deck *Transações*
- **Concorrência / isolamento** → deck *Concorrência*

</div>
<div>

- **Índices e desempenho** → deck *Views, SQL e Indexação*
- **Álgebra relacional** → deck *Álgebra Relacional*
- **NoSQL e CAP** → deck *NoSQL*

</div>
</div>

---

<!-- _class: secao -->

# Bons estudos! 🎯
### howard.cruz@faesa.br

<a class="proximo" href="../index.html">☰ Índice<small>Tópicos Especiais II</small></a>
<a class="proximo" href="aula-02-banco-de-dados.html">Aula 2 · Banco de Dados<small>revisão completa</small></a>
