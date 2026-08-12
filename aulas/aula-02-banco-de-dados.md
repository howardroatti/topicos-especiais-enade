---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Revisão ENADE — Banco de Dados

## Do modelo relacional ao NoSQL

Tópicos Especiais II — ENADE · CC e SI · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## Como funciona esta revisão

<div class="cols">

<div>

**1. Recaptura relâmpago**
- Os conceitos-chave de **cada unidade**, em uma passada rápida.
- Foco no que o **ENADE cobra**.

</div>

<div>

**2. 🔥 Esquenta**
- Questões **estilo ENADE** (situação-problema → A–D).
- Responda **antes** do gabarito comentado.

</div>

</div>

<div class="dica">💡 A prova cobra <strong>análise</strong>, não decoreba: leia o contexto, elimine distratores, decida.</div>

---

<!-- _class: secao -->

# Parte 1
### Recaptura relâmpago por unidade

---

## Arquitetura ANSI-SPARC (3 níveis)

<div class="cols">

<div>

- **Externo (views):** o que **cada usuário/app** enxerga — recortes dos dados.
- **Conceitual (lógico):** o **esquema global** — tabelas, colunas, chaves, relacionamentos, regras.
- **Interno (físico):** como está **gravado** — arquivos, páginas, **índices**, ordenação.

</div>

<div>

**Independência de dados**
- **Física:** mudar índices/armazenamento **sem** mexer no conceitual nem nas apps.
- **Lógica:** mudar o **conceitual** (ex.: nova coluna) sem quebrar as **views** — mais difícil de garantir.

</div>

</div>

<div class="dica">💡 ENADE: "reorganizou físico/índices sem afetar apps" = independência <strong>física</strong>.</div>

---

## ANSI-SPARC — visão em camadas

<svg viewBox="0 0 1000 420" role="img" style="width:100%;max-width:900px;display:block;margin:12px auto 0;font-family:'Segoe UI',Arial,sans-serif">
 <rect x="150" y="10" width="700" height="90" rx="12" fill="#dbeafe" stroke="#12437f" stroke-width="2"/>
 <text x="500" y="45" text-anchor="middle" font-size="24" font-weight="700" fill="#0d2b57">NÍVEL EXTERNO</text>
 <text x="500" y="78" text-anchor="middle" font-size="19" fill="#1f2937">Views — o recorte que cada usuário/app enxerga</text>
 <text x="500" y="140" text-anchor="middle" font-size="18" font-style="italic" fill="#12437f">&#8597; independência lógica</text>
 <rect x="150" y="160" width="700" height="90" rx="12" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="500" y="195" text-anchor="middle" font-size="24" font-weight="700" fill="#0d2b57">NÍVEL CONCEITUAL</text>
 <text x="500" y="228" text-anchor="middle" font-size="19" fill="#1f2937">Esquema lógico global — tabelas, chaves, relacionamentos</text>
 <text x="500" y="290" text-anchor="middle" font-size="18" font-style="italic" fill="#12437f">&#8597; independência física</text>
 <rect x="150" y="310" width="700" height="90" rx="12" fill="#e2e8f0" stroke="#12437f" stroke-width="2"/>
 <text x="500" y="345" text-anchor="middle" font-size="24" font-weight="700" fill="#0d2b57">NÍVEL INTERNO</text>
 <text x="500" y="378" text-anchor="middle" font-size="19" fill="#1f2937">Físico — arquivos, páginas, índices, ordenação</text>
</svg>

---

## Modelo Relacional (Codd)

<div class="cols">

<div>

- Dados em **relações (tabelas)**: linha = **tupla**, coluna = **atributo**, valores válidos = **domínio**.
- **Chaves:** *superchave* (identifica) ⊇ *candidata* (mínima) → uma vira **primária (PK)**, as outras **alternativas**; **estrangeira (FK)** referencia a PK de outra.

</div>

<div>

**As 3 integridades**
- **Entidade:** PK **não nula** e única.
- **Referencial:** FK **existe** na tabela referenciada **ou** é nula.
- **Domínio:** valor dentro do tipo/regra da coluna.

</div>

</div>

<div class="aviso">⚠️ Violar integridade referencial = FK apontando para uma linha que não existe.</div>

---

## Álgebra relacional (a base do SELECT)

<div class="cols">

<div>

- **σ** seleção → **filtra linhas** (condição).
- **π** projeção → **escolhe colunas** (elimina duplicatas).
- **⋈** junção → combina tabelas pela condição/chave.
- **×** produto cartesiano → **todas** as combinações.

</div>

<div>

- **∪** união · **∩** interseção · **−** diferença (exigem tabelas **compatíveis**).
- **÷** divisão → ideia de "**para todos**" (ex.: quem cursou **todas** as disciplinas).

</div>

</div>

<div class="dica">💡 Ordem típica: junta (⋈) → filtra (σ) → projeta (π). <strong>σ = linhas</strong>, <strong>π = colunas</strong>.</div>

---

## MER e mapeamento para tabelas

<div class="cols">

<div>

- **Atributos:** simples, **composto**, **multivalorado**, **derivado**.
- **Relacionamento + cardinalidade** (1:1, 1:N, N:N).
- **Generalização/especialização:** total×parcial, **disjunta×sobreposta**.
- **Entidade associativa** resolve **N:N**.

</div>

<div>

**Regras MER → relacional**
- **1:N:** a chave do lado **1** vira **FK** no lado **N**.
- **N:N:** cria **tabela associativa** com as duas FKs (**PK composta**).
- **1:1:** FK no lado de **participação total**.

</div>

</div>

<div class="dica">💡 A "tabela associativa" do N:N é exatamente o que cai na modelagem da C1.</div>

---

## Mapeamento N:N — a tabela associativa

<svg viewBox="0 0 1000 280" role="img" style="width:100%;max-width:940px;display:block;margin:16px auto 0;font-family:'Segoe UI',Arial,sans-serif">
 <line x1="260" y1="140" x2="390" y2="140" stroke="#12437f" stroke-width="2"/>
 <line x1="610" y1="140" x2="740" y2="140" stroke="#12437f" stroke-width="2"/>
 <text x="285" y="128" text-anchor="middle" font-size="18" font-weight="700" fill="#12437f">1</text>
 <text x="365" y="128" text-anchor="middle" font-size="18" font-weight="700" fill="#12437f">N</text>
 <text x="635" y="128" text-anchor="middle" font-size="18" font-weight="700" fill="#12437f">N</text>
 <text x="715" y="128" text-anchor="middle" font-size="18" font-weight="700" fill="#12437f">1</text>
 <rect x="40" y="100" width="220" height="80" rx="10" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="150" y="135" text-anchor="middle" font-size="22" font-weight="700" fill="#0d2b57">ALUNO</text>
 <text x="150" y="162" text-anchor="middle" font-size="15" fill="#1f2937">PK matricula</text>
 <rect x="390" y="83" width="220" height="114" rx="10" fill="#fff8e1" stroke="#f0c36d" stroke-width="2"/>
 <text x="500" y="116" text-anchor="middle" font-size="20" font-weight="700" fill="#0d2b57">CURSA</text>
 <text x="500" y="143" text-anchor="middle" font-size="14" fill="#1f2937">PK (matricula, cod)</text>
 <text x="500" y="167" text-anchor="middle" font-size="14" fill="#1f2937">FK ALUNO · FK DISCIPLINA</text>
 <rect x="740" y="100" width="220" height="80" rx="10" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="850" y="135" text-anchor="middle" font-size="21" font-weight="700" fill="#0d2b57">DISCIPLINA</text>
 <text x="850" y="162" text-anchor="middle" font-size="15" fill="#1f2937">PK cod</text>
 <text x="500" y="250" text-anchor="middle" font-size="18" font-style="italic" fill="#1f2937">O N:N vira duas relações 1:N ligadas pela tabela associativa (PK composta = as 2 FKs)</text>
</svg>

---

## Normalização — dependências funcionais

- **DF `X → Y`:** o valor de `X` **determina** `Y` (ex.: `CPF → Nome`); `X` é o **determinante**.

<div class="cols">

<div>

- **Parcial:** não-chave depende de **parte** de chave composta.
- **Transitiva:** não-chave depende de **outro não-chave**.
- **1FN:** atributos **atômicos**.

</div>

<div>

- **2FN:** 1FN + **sem dependência parcial**.
- **3FN:** 2FN + **sem dependência transitiva**.
- **BCNF:** todo **determinante** é chave candidata.

</div>

</div>

<div class="dica">💡 <strong>Parcial → 2FN</strong> · <strong>Transitiva → 3FN</strong>.</div>

---

## Normalização — exemplo passo a passo

**Desnormalizada:** `Matricula(Aluno, Disciplina, Professor, Depto_Prof)` — chave `(Aluno, Disciplina)`; regras `Disciplina → Professor` e `Professor → Depto_Prof`.

<div class="cols">

<div>

- **Parcial:** `Professor` depende só de `Disciplina` (parte da chave) → fere a **2FN**.
- **Transitiva:** `Depto_Prof` depende de `Professor` (não-chave) → fere a **3FN**.

</div>

<div>

**Resultado em 3FN**
- `Matricula(Aluno, Disciplina)`
- `Turma(Disciplina, Professor)`
- `Professor_Info(Professor, Depto_Prof)`

</div>

</div>

<div class="aviso">⚠️ Sem normalizar, o depto se repete em toda matrícula → anomalias de inserção, atualização e exclusão.</div>

---

## Normalização — a decomposição (visual)

<svg viewBox="0 0 1000 320" role="img" style="width:100%;max-width:940px;display:block;margin:6px auto 0;font-family:'Segoe UI',Arial,sans-serif">
 <rect x="215" y="6" width="570" height="66" rx="10" fill="#fde2e1" stroke="#c0392b" stroke-width="2"/>
 <text x="500" y="34" text-anchor="middle" font-size="17" font-weight="700" fill="#7b241c">Matricula(Aluno, Disciplina, Professor, Depto_Prof)</text>
 <text x="500" y="58" text-anchor="middle" font-size="14" fill="#7b241c">1 tabela — com dependência parcial e transitiva</text>
 <text x="500" y="108" text-anchor="middle" font-size="18" font-weight="700" fill="#12437f">decompõe até a 3FN  &#8595;</text>
 <rect x="30" y="138" width="290" height="86" rx="10" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="175" y="174" text-anchor="middle" font-size="16" font-weight="700" fill="#0d2b57">Matricula</text>
 <text x="175" y="198" text-anchor="middle" font-size="14" fill="#1f2937">(Aluno, Disciplina)</text>
 <rect x="355" y="138" width="290" height="86" rx="10" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="500" y="174" text-anchor="middle" font-size="16" font-weight="700" fill="#0d2b57">Turma</text>
 <text x="500" y="198" text-anchor="middle" font-size="14" fill="#1f2937">(Disciplina, Professor)</text>
 <rect x="680" y="138" width="290" height="86" rx="10" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="825" y="174" text-anchor="middle" font-size="16" font-weight="700" fill="#0d2b57">Professor_Info</text>
 <text x="825" y="198" text-anchor="middle" font-size="14" fill="#1f2937">(Professor, Depto_Prof)</text>
 <text x="500" y="278" text-anchor="middle" font-size="17" font-style="italic" fill="#1f2937">cada fato num só lugar → sem anomalias de inserção/atualização/exclusão</text>
</svg>

---

## SQL — o que cai e a ordem lógica

<div class="cols">

<div>

- **DDL** `CREATE/ALTER/DROP` · **DML** `INSERT/UPDATE/DELETE` · **DQL** `SELECT`.
- **Ordem lógica:** `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`.
- **`WHERE`** filtra **linhas** (antes de agrupar); **`HAVING`** filtra **grupos** (aceita `SUM/COUNT`).

</div>

<div>

**JOINs**
- **INNER:** só o que **casa** nos dois lados.
- **LEFT:** **tudo** da esquerda (+ NULLs à direita).
- **FULL:** tudo dos **dois** lados.

</div>

</div>

<div class="dica">💡 "Total do grupo passa de X" = `GROUP BY` + `HAVING` — nunca `WHERE SUM(...)`.</div>

---

## SQL — índices, views e FK

<div class="cols">

<div>

- **Índice:** acelera busca **seletiva** (poucas linhas). Em coluna de **baixa seletividade** (ex.: booleana que traz metade), o otimizador prefere **varredura** — o índice só onera escrita/espaço.
- **View:** consulta nomeada (tabela virtual) — abstrai e protege o esquema.

</div>

<div>

**FK — ações ao excluir o pai**
- `CASCADE`: apaga os **filhos** junto.
- `RESTRICT/NO ACTION`: **bloqueia** a exclusão.
- `SET NULL`: deixa a FK **órfã** (nula).

</div>

</div>

---

## Transações — ACID e níveis de isolamento

- **ACID:** **A**tomicidade · **C**onsistência · **I**solamento · **D**urabilidade.

| Nível de isolamento | Dirty read | Non-repeatable | Phantom |
|---|:---:|:---:|:---:|
| READ UNCOMMITTED | pode | pode | pode |
| READ COMMITTED | **não** | pode | pode |
| REPEATABLE READ | **não** | **não** | pode |
| SERIALIZABLE | **não** | **não** | **não** |

<div class="dica">💡 Mais isolamento → menos anomalia, porém <strong>menos concorrência</strong> (mais bloqueio).</div>

---

## Concorrência e recuperação

<div class="cols">

<div>

**2PL (bloqueio em 2 fases)**
- **Expansão** (só adquire locks) → **encolhimento** (só libera).
- Garante **serialização**, mas **não evita deadlock**.
- **Deadlock:** espera circular → o SGBD **detecta**, escolhe **vítima** e faz **rollback**. Prevenção por timestamp: *wait-die* / *wound-wait*.

</div>

<div>

**Recuperação (WAL)**
- Grava o **log antes** do dado.
- Confirmadas → **REDO** (durabilidade).
- Não-confirmadas → **UNDO** (atomicidade).
- **Checkpoint** limita o retrocesso do REDO.

</div>

</div>

---

## Deadlock — o ciclo de espera (visual)

<svg viewBox="0 0 460 260" role="img" style="width:100%;max-width:440px;display:block;margin:18px auto 0;font-family:'Segoe UI',Arial,sans-serif">
 <defs>
  <marker id="ahb" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L9,3 L0,6 Z" fill="#12437f"/></marker>
  <marker id="ahr" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L9,3 L0,6 Z" fill="#c0392b"/></marker>
 </defs>
 <path d="M140,105 L322,105" stroke="#12437f" stroke-width="2.5" fill="none" marker-end="url(#ahb)"/>
 <text x="231" y="94" text-anchor="middle" font-size="14" fill="#12437f">T1 espera recurso de T2</text>
 <path d="M322,158 L140,158" stroke="#c0392b" stroke-width="2.5" fill="none" marker-end="url(#ahr)"/>
 <text x="231" y="180" text-anchor="middle" font-size="14" fill="#c0392b">T2 espera recurso de T1</text>
 <circle cx="90" cy="130" r="46" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="90" y="139" text-anchor="middle" font-size="24" font-weight="700" fill="#0d2b57">T1</text>
 <circle cx="372" cy="130" r="46" fill="#eef4fb" stroke="#12437f" stroke-width="2"/>
 <text x="372" y="139" text-anchor="middle" font-size="24" font-weight="700" fill="#0d2b57">T2</text>
 <text x="231" y="238" text-anchor="middle" font-size="15" font-style="italic" fill="#1f2937">ciclo ⇒ deadlock → o SGBD escolhe vítima + rollback</text>
</svg>

---

## NoSQL, CAP e BASE

<div class="cols">

<div>

**4 famílias (com uso típico)**
- **Chave-valor:** cache, sessão.
- **Documento:** JSON, catálogo.
- **Coluna:** analítico, escrita massiva.
- **Grafo:** relações, redes sociais.

</div>

<div>

**CAP** — sob **partição**, escolha **uma**
- **CP:** consistência, **recusa** em partição.
- **AP:** disponibilidade, **consistência eventual**.
- **CA:** só sem partição (irreal em rede distribuída).

</div>

</div>

<div class="dica">💡 Relacional = <strong>ACID</strong> (forte); muitos NoSQL = <strong>BASE</strong> (disponível, consistência eventual).</div>

---

## CAP — escolha 2 dos 3

<svg viewBox="-130 0 1080 400" role="img" style="width:100%;max-width:720px;display:block;margin:6px auto 0;font-family:'Segoe UI',Arial,sans-serif">
 <polygon points="410,34 90,350 730,350" fill="#eef4fb" stroke="#12437f" stroke-width="2.5"/>
 <circle cx="410" cy="34" r="7" fill="#0d2b57"/>
 <circle cx="90" cy="350" r="7" fill="#0d2b57"/>
 <circle cx="730" cy="350" r="7" fill="#0d2b57"/>
 <text x="410" y="22" text-anchor="middle" font-size="21" font-weight="700" fill="#0d2b57">C — Consistência</text>
 <text x="90" y="380" text-anchor="middle" font-size="21" font-weight="700" fill="#0d2b57">A — Disponibilidade</text>
 <text x="730" y="380" text-anchor="middle" font-size="21" font-weight="700" fill="#0d2b57">P — Tolerância a partição</text>
 <text x="222" y="200" text-anchor="middle" font-size="22" font-weight="700" fill="#c0392b">CA</text>
 <text x="598" y="200" text-anchor="middle" font-size="22" font-weight="700" fill="#12437f">CP</text>
 <text x="410" y="336" text-anchor="middle" font-size="22" font-weight="700" fill="#12437f">AP</text>
 <text x="410" y="250" text-anchor="middle" font-size="16" font-style="italic" fill="#1f2937">Sob partição (P): escolha CP ou AP.</text>
 <text x="410" y="274" text-anchor="middle" font-size="16" font-style="italic" fill="#1f2937">CA só quando não há partição.</text>
</svg>

---

<!-- _class: secao -->

# Parte 2 — 🔥 Esquenta
### Banco de Dados · questões estilo ENADE (A–D)
#### Responda antes de virar o slide!

---

## Q1 — Álgebra relacional

Uma secretaria acadêmica usa `Aluno(Matricula, Nome, IdCurso)` e `Curso(IdCurso, NomeCurso)`. É preciso emitir uma lista com **somente os nomes** dos alunos do curso de **Sistemas de Informação**.

Assinale a expressão de álgebra relacional correta.

A) π<sub>Nome</sub>( σ<sub>NomeCurso='Sistemas de Informação'</sub>( Aluno ⋈ Curso ) )
B) π<sub>Nome</sub>( Aluno ⋈ Curso )
C) σ<sub>NomeCurso='Sistemas de Informação'</sub>( Aluno ⋈ Curso )
D) π<sub>NomeCurso</sub>( σ<sub>Nome='Sistemas de Informação'</sub>( Aluno ⋈ Curso ) )

---

## Q1 — Gabarito: **A**

**Relembrando:** **σ** filtra **linhas**; **π** escolhe **colunas**; a junção casa `IdCurso`.

- Precisa **filtrar** pelo curso (σ) e **projetar** só o `Nome` (π). ✅
- **B** não filtra (traz todos); **C** filtra mas **não projeta** (devolve a tupla inteira); **D** usa atributos trocados.

---

## Q2 — SQL com agregação

Em `Cliente(id, nome)`, `Pedido(id, id_cliente)`, `Item(id_pedido, qtd, valor)`, o marketing quer os **clientes cujo total gasto** (∑ `qtd*valor`) **passa de R$ 1.000**.

Qual consulta atende?

A) `WHERE SUM(qtd*valor) > 1000` com `GROUP BY nome`.
B) junta as três tabelas, agrupa por cliente e usa `HAVING SUM(qtd*valor) > 1000`.
C) agrupa por cliente e usa `HAVING qtd*valor > 1000`.
D) `WHERE valor > 1000`, item a item.

---

## Q2 — Gabarito: **B**

**Relembrando:** filtro sobre **agregado por grupo** → `GROUP BY` + **`HAVING`** (o `WHERE` não aceita `SUM`).

- **A** usa `SUM` no `WHERE` (inválido); **C** compara item a item, não o total; **D** filtra itens caros, não o **gasto total** do cliente. ✅ = **B**.

---

## Q3 — Normalização

Um analista modela `R(Aluno, Disciplina, Professor)` com chave `(Aluno, Disciplina)` e a regra **`Disciplina → Professor`**. Ele nota **redundância**: o professor se repete em cada matrícula.

A relação **viola** a:

A) 1FN, por atributo multivalorado.
B) 3FN, por dependência transitiva.
C) 2FN, por dependência parcial de `Professor` em relação à chave.
D) Nenhuma; já está na 3FN.

---

## Q3 — Gabarito: **C**

**Relembrando:** `Professor` depende só de **`Disciplina`** (parte da chave composta) → **dependência parcial** → fere a **2FN**. ✅

- Não é transitiva (3FN) nem atomicidade (1FN). **Correção:** `Turma(Disciplina, Professor)` + `Matricula(Aluno, Disciplina)`.

---

## Q4 — Mapeamento de generalização

`Pessoa` especializa-se em `PessoaFisica` (CPF) e `PessoaJuridica` (CNPJ), de forma **total e disjunta**. Deseja-se **evitar colunas nulas** e impedir que um cadastro seja PF e PJ.

Qual estratégia é a mais adequada?

A) Uma tabela `Pessoa` com CPF e CNPJ (a maioria nula).
B) Uma **tabela por subtipo**, cada uma com os atributos comuns.
C) `Pessoa` + subtabelas, permitindo ser PF **e** PJ.
D) `Pessoa` com listas de CPF/CNPJ por vírgula.

---

## Q4 — Gabarito: **B**

**Relembrando:** especialização **total + disjunta** → **uma tabela por subtipo** elimina nulos e garante a exclusividade. ✅

- **A** gera muitos nulos; **C** permitiria sobreposição; **D** fere a 1FN.

---

## Q5 — Isolamento

No sistema bancário, `T1` lê o saldo; antes de `T1` terminar, `T2` **credita e confirma**; ao **reler**, `T1` obtém **valor diferente**.

A anomalia é:

A) Leitura suja (*dirty read*).
B) Perda de atualização (*lost update*).
C) Leitura fantasma (*phantom*).
D) Leitura não repetível (*non-repeatable read*).

---

## Q5 — Gabarito: **D**

**Relembrando:** reler a **mesma linha** e achar valor diferente (por *update confirmado* no meio) = **leitura não repetível**. ✅

- *Dirty* = ler não-confirmado; *phantom* = novas linhas; *lost update* = escritas se sobrepõem. Evita-se com `REPEATABLE READ`.

---

## Q6 — Concorrência

Com 2PL, `T1` trava `A` e `T2` trava `B`; então `T1` pede `B` e `T2` pede `A`, ambas travadas.

Assinale a correta.

A) O 2PL garante que deadlock nunca ocorra.
B) Ocorre **deadlock**; o SGBD detecta, escolhe vítima e faz rollback.
C) As duas concluem sem espera.
D) É uma leitura fantasma.

---

## Q6 — Gabarito: **B**

**Relembrando:** 2PL garante **serialização**, mas **não evita deadlock**. Espera circular → o SGBD **aborta uma vítima** (rollback) e a outra segue. ✅

<div class="dica">💡 Prevenção por timestamp: <em>wait-die</em> (esperar-morrer) / <em>wound-wait</em> (ferir-esperar).</div>

---

## Q7 — Recuperação (WAL)

Após falha de energia: `T1` deu `commit` **antes** da falha (páginas talvez não gravadas); `T2` estava **ativa** (sem commit).

A recuperação aplica:

A) UNDO em `T1`, REDO em `T2`.
B) REDO em ambas.
C) REDO em `T1`, UNDO em `T2`.
D) Nada; o commit de `T1` dispensa recuperação.

---

## Q7 — Gabarito: **C**

**Relembrando (WAL):** confirmadas → **REDO** (durabilidade, caso de `T1`); não-confirmadas → **UNDO** (atomicidade, caso de `T2`). ✅

- O **checkpoint** limita o quanto o REDO precisa retroceder.

---

## Q8 — Índices

Sobre uma tabela de **milhões de linhas**, a equipe decide onde criar índices. Em qual caso o índice **tende a NÃO ajudar**?

A) Coluna `cpf` única em `WHERE cpf = ...`.
B) FK usada em `JOIN`.
C) Coluna **booleana** cujo filtro retorna **metade** das linhas.
D) Coluna de data em faixas (`BETWEEN`).

---

## Q8 — Gabarito: **C**

**Relembrando:** índice compensa quando a busca é **seletiva**. Coluna de **baixa seletividade** que retorna metade da tabela → o otimizador prefere **varredura completa**; o índice só onera escrita/espaço. ✅

---

## Q9 — NoSQL e CAP

Um **carrinho de compras global** precisa ficar **disponível e aceitando escritas** mesmo com **partições de rede**, tolerando inconsistência **temporária**.

Segundo o CAP, a escolha adequada é:

A) **AP** com consistência eventual (ex.: banco de documentos distribuído).
B) **CA** garantindo as três propriedades.
C) Relacional com bloqueio global síncrono.
D) **CP**, recusando escritas durante a partição.

---

## Q9 — Gabarito: **A**

**Relembrando (CAP):** sob **partição**, escolhe-se **C ou A**. O carrinho quer **disponibilidade + escrita** → **AP** (modelo **BASE**, consistência eventual). ✅

- **B** é impossível sob partição; **D** recusaria escritas; **C** não escala.

---

## Q10 — Arquitetura

A equipe **reorganiza o armazenamento físico** e **cria índices** de uma tabela, **sem alterar** aplicações nem o esquema conceitual.

Na ANSI-SPARC, isso é:

A) Independência lógica.
B) Independência física.
C) Ausência de independência.
D) Independência referencial.

---

## Q10 — Gabarito: **B**

**Relembrando:** mudar o **nível interno** (físico/índices) sem afetar o conceitual/aplicações = **independência física**. ✅

- A **lógica** seria mudar o **esquema conceitual** sem afetar as **views** — não é o caso.

---

<!-- _class: secao -->

# Fim da revisão de Banco de Dados 🗄️
### Próximo: mais Esquentas e o Aulão de BD (23/09).

**Gabarito:** 1A · 2B · 3C · 4B · 5D · 6B · 7C · 8C · 9A · 10B

<div class="dica">💡 <strong>Aulão (23/09):</strong> resolveremos questões em <strong>grupos</strong> — traga suas dúvidas das unidades acima.</div>
