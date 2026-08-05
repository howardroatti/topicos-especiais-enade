---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Tópicos Especiais II — ENADE

## Aula 1 — Boas-vindas & Esquenta

Revisão para o ENADE · Ciência da Computação e Sistemas de Informação
Prof. M.Sc. Howard Cruz Roatti · 2026/2

---

## Roteiro de hoje

<div class="cols">

<div>

**Parte 1 — Sobre o ENADE**
- O que é e como funciona
- Por que ele importa (para você e para o curso)
- Cuidados na hora da prova

</div>

<div>

**Parte 2 — 🔥 Esquenta**
- Questões objetivas **estilo ENADE** (A–D)
- **10 de Banco de Dados + 10 de Análise de Dados**
- Responda **antes** de ver o gabarito comentado

</div>

</div>

<div class="dica">💡 A ideia é treinar o <strong>jeito ENADE de pensar</strong>: ler o contexto, analisar e decidir.</div>

---

<!-- _class: secao -->

# Parte 1
### O que é o ENADE?

---

## O que é o ENADE

- **E**xame **N**acional de **D**esempenho dos **E**studantes, aplicado pelo **INEP**.
- É um dos pilares do **SINAES** (Sistema Nacional de Avaliação da Educação Superior).
- Avalia o **desempenho dos concluintes** em relação às **competências, habilidades e conteúdos** previstos nas **Diretrizes Curriculares Nacionais (DCN)** do curso.
- **Periodicidade trienal** por área — Computação (CC e SI) foi avaliada em **2023**; a próxima é **2026**.
- **Prova (4h):** **Formação Geral** (comum a todas as áreas) + **Componente Específico** da área — questões **objetivas e discursivas**.

---

## Por que o ENADE importa

<div class="cols">

<div>

**Para você, estudante**
- A **participação regular** é **condição para colar grau** (consta no histórico).
- Mostra o quanto você **integra** o que aprendeu ao longo do curso.
- Treino valioso para **concursos** e **processos seletivos**.

</div>

<div>

**Para o curso e a FAESA**
- Gera o **Conceito ENADE**, o **CPC** e alimenta o **IGC**.
- Impacta **reconhecimento, reputação** e a **renovação** do curso.
- **O valor do seu diploma** também depende desses conceitos.

</div>

</div>

<div class="aviso">⚠️ O desempenho é <strong>coletivo</strong>: "zerar de propósito" ou não levar a sério prejudica todo o curso — inclusive quem já se formou.</div>

---

## Cuidados na hora da prova

- **Leve a sério.** Não é "só mais uma prova": ela mede — e é registrada.
- **Leia o texto-base com atenção.** As questões são **contextualizadas** (situação-problema, tabela, gráfico, código). A resposta está na análise, não na memória.
- **Gerencie o tempo.** São 4h para Formação Geral + Específico, incluindo **discursivas**.
- **Não deixe em branco** e **responda o questionário do estudante**.
- **Cuidado com distratores.** As alternativas erradas costumam ser **plausíveis** — elimine com critério.

---

## O que vamos revisar

Nas próximas aulas, vamos **revisar em profundidade** três disciplinas do componente específico:

<div class="cols">

<div>

- 🗄️ **Banco de Dados**
- 📊 **Análise de Dados Aplicada à Computação**
- 🌐 **Sistemas Distribuídos**

</div>

<div>

Hoje começamos com um **Esquenta** de **Banco de Dados** e **Análise de Dados**. 🔥
*(Sistemas Distribuídos entra nas próximas aulas.)*

</div>

</div>

---

<!-- _class: secao -->

# Parte 2 — 🔥 Esquenta
### 20 questões estilo ENADE · alternativas A a D
#### 10 de Banco de Dados · 10 de Análise de Dados — responda antes de virar o slide!

---

## Q1 · Banco de Dados

Uma coordenação de curso utiliza um sistema acadêmico cujo esquema relacional inclui `Aluno(Matricula, Nome, IdCurso)` e `Curso(IdCurso, NomeCurso)`. Para organizar uma atividade de integração, a secretaria precisa emitir uma lista contendo **somente os nomes** dos alunos matriculados no curso de **Sistemas de Informação** — sem os demais dados.

Assinale a expressão de **álgebra relacional** que produz corretamente essa lista.

A) π<sub>Nome</sub>( σ<sub>NomeCurso='Sistemas de Informação'</sub>( Aluno ⋈ Curso ) )
B) π<sub>Nome</sub>( Aluno ⋈ Curso )
C) σ<sub>NomeCurso='Sistemas de Informação'</sub>( Aluno ⋈ Curso )
D) π<sub>NomeCurso</sub>( σ<sub>Nome='Sistemas de Informação'</sub>( Aluno ⋈ Curso ) )

---

## Q1 · Resposta: **A**

**Relembrando (Unidade 3 — Álgebra Relacional):** a **seleção (σ)** filtra **linhas** por um predicado; a **projeção (π)** escolhe **colunas**. A **junção (⋈)** combina `Aluno` e `Curso` pela chave `IdCurso`.

- O pedido "**apenas os nomes** dos alunos de SI" → junta as tabelas, **filtra** pelo curso (σ) e **projeta** só o `Nome` (π). ✅
- **B** não filtra o curso (traz todos); **C** filtra certo, mas **sem projeção** devolve a tupla inteira — não "só os nomes"; **D** projeta e filtra pelos **atributos errados**.

<div class="dica">💡 σ antes ou depois da junção dá o mesmo resultado — mas a projeção do <code>Nome</code> é obrigatória.</div>

---

## Q2 · Banco de Dados

Uma loja virtual registra suas vendas em `Cliente(id, nome)`, `Pedido(id, id_cliente)` e `Item(id_pedido, qtd, valor)`. Para uma campanha de fidelidade, o marketing quer identificar os **clientes de maior valor**: aqueles cujo **total gasto** — a soma de `qtd*valor` considerando **todos os itens de todos os seus pedidos** — **ultrapassa R$ 1.000,00**.

Qual consulta SQL atende corretamente a esse requisito?

A) usa `WHERE SUM(qtd*valor) > 1000` com `GROUP BY nome`.
B) junta as três tabelas, agrupa por cliente e usa `HAVING SUM(qtd*valor) > 1000`.
C) agrupa por cliente e usa `HAVING qtd*valor > 1000`.
D) usa `WHERE valor > 1000`, filtrando item a item.

---

## Q2 · Resposta: **B**

**Relembrando (Unidade 5 — SQL):** `WHERE` filtra **linhas antes** de agrupar e **não aceita** funções de agregação; `HAVING` filtra **grupos depois** do `GROUP BY`.

- O critério é sobre um **total por cliente** (soma) → precisa `GROUP BY cliente` + **`HAVING SUM(qtd*valor) > 1000`**. ✅
- **A** usa `SUM` no `WHERE` (erro clássico); **C** compara **item a item**, não o total; **D** filtra itens caros, não clientes que **gastaram muito no conjunto**.

---

## Q3 · Banco de Dados

Ao projetar o banco de um sistema acadêmico, um analista modelou a tabela `R(Aluno, Disciplina, Professor)`, cuja chave primária é o par `(Aluno, Disciplina)`. Pela regra de negócio, **cada disciplina é ministrada por um único professor** (`Disciplina → Professor`). Na revisão, nota-se **redundância**: o professor de uma disciplina se repete em toda matrícula, e trocá-lo exigiria alterar **várias linhas** (anomalia de atualização).

Sobre a normalização de `R`, é correto afirmar que ela **viola** a:

A) 1FN, por conter um atributo multivalorado.
B) 3FN, por uma dependência transitiva entre atributos não-chave.
C) 2FN, pois um atributo não-chave depende apenas de **parte** da chave.
D) Nenhuma; a relação já está na 3FN.

---

## Q3 · Resposta: **C**

**Relembrando (Unidade 4 — Normalização):** 1FN = atributos **atômicos**; 2FN = sem **dependência parcial** (não-chave dependendo de **parte** de uma chave composta); 3FN = sem **dependência transitiva**.

- Chave = `(Aluno, Disciplina)`; como **`Disciplina → Professor`**, o `Professor` depende só de **parte** da chave → **dependência parcial** → viola a **2FN** (origem da redundância descrita). ✅
- Não é transitiva (isso seria 3FN) nem atomicidade (1FN).

<div class="dica">💡 Correção: decompor em <code>Turma(Disciplina, Professor)</code> e <code>Matricula(Aluno, Disciplina)</code>.</div>

---

## Q4 · Banco de Dados

No modelo conceitual de um sistema de cadastro, a entidade `Pessoa` foi especializada em `PessoaFisica` (CPF) e `PessoaJuridica` (CNPJ). A especialização é **total** (todo cadastro é PF **ou** PJ) e **disjunta** (nenhum é os dois). Ao mapear para o modelo relacional, a equipe quer **evitar colunas frequentemente nulas** e **impedir** que um mesmo cadastro seja classificado como PF e PJ ao mesmo tempo.

Qual estratégia de mapeamento atende melhor a esses requisitos?

A) Uma única tabela `Pessoa` com todas as colunas (CPF e CNPJ), a maioria nula.
B) `Pessoa` + subtabelas por FK, permitindo ser física **e** jurídica ao mesmo tempo.
C) Uma tabela `Pessoa` com listas de CPF/CNPJ separadas por vírgula.
D) Uma tabela por subtipo, cada uma com os atributos comuns de `Pessoa`.

---

## Q4 · Resposta: **D**

**Relembrando (Unidade 4 — Generalização/Especialização):** *total* = todo supertipo é **algum** subtipo; *disjunta* = é **exatamente um**. Há 3 estratégias de mapeamento; a escolha depende dessas restrições.

- Para **total + disjunta**, "**uma tabela por subtipo**" (sem tabela do supertipo) **elimina os nulos** e preserva a exclusividade. ✅
- **A** gera muitas colunas **nulas**; **B** permitiria **sobreposição** (fere a disjunção); **C** fere a **1FN**.

---

## Q5 · Banco de Dados

Em um sistema bancário, a transação `T1` consulta o **saldo** de uma conta para exibi-lo na tela. Antes de `T1` concluir, a transação `T2` **credita um valor e confirma (commit)**. Quando `T1`, ainda em andamento, **consulta novamente** o saldo da **mesma conta**, obtém um **valor diferente** do lido inicialmente.

A anomalia de controle de concorrência caracterizada nessa situação é a:

A) Leitura não repetível (*non-repeatable read*).
B) Leitura suja (*dirty read*).
C) Perda de atualização (*lost update*).
D) Situação normal, sem anomalia.

---

## Q5 · Resposta: **A**

**Relembrando (Unidade 6 — Transações):** a "escada" de anomalias de concorrência —
- **Dirty read:** ler dado **não confirmado**.
- **Non-repeatable read:** reler a **mesma linha** e achar valor diferente (update **confirmado** no meio). ✅ *(é o caso)*
- **Phantom:** **novas linhas** aparecem num filtro relido.
- **Lost update:** duas escritas se sobrepõem.

Evita-se a leitura não repetível a partir do isolamento **`REPEATABLE READ`**.

---

## Q6 · Banco de Dados

Em um SGBD com bloqueio de duas fases (2PL), duas transações executam em paralelo. `T1` obtém bloqueio sobre o registro `A` e `T2` sobre o registro `B`. Em seguida, `T1` solicita bloqueio sobre `B` (retido por `T2`) e `T2` solicita bloqueio sobre `A` (retido por `T1`). Ambas ficam **paradas indefinidamente**, cada uma esperando um recurso que a outra detém.

Sobre a situação descrita, assinale a alternativa correta.

A) O 2PL **garante** que deadlocks nunca ocorram.
B) Ocorre **deadlock**; o SGBD detecta, escolhe uma **vítima** e faz **rollback**.
C) As duas transações concluem sem qualquer espera.
D) O fenômeno observado é uma **leitura fantasma**.

---

## Q6 · Resposta: **B**

**Relembrando (Unidade 6 — Concorrência):** o **2PL** garante **serialização** (transações crescem e depois só liberam bloqueios), mas **não evita deadlock**.

- `T1` espera `B` (com `T2`) e `T2` espera `A` (com `T1`) → **espera circular** = **deadlock**. ✅
- O SGBD mantém um **grafo de espera**, detecta o ciclo, **aborta uma vítima** e faz **rollback**; a outra prossegue.

<div class="dica">💡 Prevenção alternativa por timestamp: <em>esperar-morrer</em> (wait-die) / <em>ferir-esperar</em> (wound-wait).</div>

---

## Q7 · Banco de Dados

Um SGBD utiliza log com **write-ahead logging (WAL)**. Uma **falha de energia** reinicia o servidor. Ao ler o log, a recuperação constata que a transação `T1` havia registrado `commit` **antes** da falha (embora suas páginas talvez não tenham ido ao disco), enquanto a transação `T2` estava **em andamento**, **sem** `commit`.

Para garantir a **atomicidade** e a **durabilidade**, o procedimento de recuperação deve aplicar:

A) UNDO em `T1` e REDO em `T2`.
B) REDO em ambas.
C) REDO em `T1` e UNDO em `T2`.
D) Nenhuma ação; o `commit` de `T1` dispensa recuperação.

---

## Q7 · Resposta: **C**

**Relembrando (Unidade 6 — Recuperação):** no **Write-Ahead Logging**, o **log** vai ao disco **antes** dos dados. Na recuperação:

- Transações **confirmadas** (mas talvez não gravadas) → **REDO** (refaz) → é o caso de `T1` (durabilidade).
- Transações **não confirmadas** → **UNDO** (desfaz) → é o caso de `T2` (atomicidade). ✅
- O **checkpoint** limita até onde o REDO precisa retroceder no log.

---

## Q8 · Banco de Dados

Uma equipe de banco de dados analisa consultas sobre uma tabela com **milhões de linhas** e decide onde criar índices, ponderando o **ganho na leitura** contra o **custo de manutenção** (escrita e espaço) de cada índice.

Em qual das situações a seguir a criação de um índice **tende a NÃO trazer ganho** de desempenho?

A) Coluna `cpf` **única**, usada em `WHERE cpf = ...`.
B) **Chave estrangeira** usada com frequência em `JOIN`.
C) Coluna de data usada em faixas (`BETWEEN`).
D) Coluna de **baixa seletividade** (poucos valores distintos) cujo filtro retorna **metade** das linhas.

---

## Q8 · Resposta: **D**

**Relembrando (Unidade 3 — Índices):** um índice compensa quando a busca é **seletiva** (retorna **poucas** linhas), evitando a **varredura completa**.

- Numa coluna de **baixa seletividade** (ex.: um booleano) cujo filtro devolve **metade** da tabela, o otimizador prefere o **full scan** — e o índice ainda **onera** escrita e espaço. ✅ *(NÃO ajuda)*
- Igualdade em coluna **única** (A), **FKs** em junções (B) e **faixas** de data (C) são justamente onde o índice **ajuda**.

---

## Q9 · Banco de Dados

Uma empresa de e-commerce global mantém o **carrinho de compras** de milhões de usuários em servidores espalhados por vários continentes. O requisito é que o carrinho **continue disponível e aceitando itens** mesmo durante **falhas de comunicação (partições) entre os data centers**, admitindo-se que, por breves instantes, réplicas fiquem **temporariamente inconsistentes**.

À luz do **Teorema CAP**, a arquitetura adequada a esse requisito é:

A) Sistema **AP** (disponibilidade + tolerância a partição) com **consistência eventual**.
B) Sistema **CA** que garante **as três** propriedades simultaneamente.
C) Banco relacional com **bloqueio global síncrono** entre todos os nós.
D) Sistema **CP** que **recusa escritas** durante a partição.

---

## Q9 · Resposta: **A**

**Relembrando (Unidade 7 — NoSQL / CAP):** sob **partição de rede** (P), é preciso escolher entre **Consistência (C)** e **Disponibilidade (A)** — ter as três ao mesmo tempo é **impossível**.

- O carrinho precisa **aceitar escritas** e **ficar disponível** → **AP**, reconciliando depois (**consistência eventual**, modelo **BASE**, típico de bancos de documento/chave-valor). ✅
- **B** é impossível sob partição; **D** (CP) recusaria escritas; **C** não escala globalmente.

---

## Q10 · Banco de Dados

Buscando desempenho, a equipe de infraestrutura de um SGBD **reorganiza o armazenamento físico** de uma tabela e **cria novos índices**. Após a mudança, constata-se que **nenhum programa de aplicação precisou ser alterado** e o **esquema conceitual** permaneceu o mesmo.

Na arquitetura de três níveis (**ANSI-SPARC**), essa situação ilustra a:

A) Independência **lógica** de dados.
B) Independência **física** de dados.
C) Ausência de independência de dados.
D) Independência **referencial**.

---

## Q10 · Resposta: **B**

**Relembrando (Unidade 2 — Arquitetura ANSI-SPARC):** três níveis — **externo** (views), **conceitual** (esquema lógico) e **interno** (físico/armazenamento).

- Mudar o nível **interno** (índices, armazenamento) **sem afetar** o conceitual/aplicações = **independência física**. ✅
- A **independência lógica** seria mudar o **esquema conceitual** sem afetar as **views**/aplicações — não é o caso aqui.

---

## Q11 · Análise de Dados

Um analista de RH examina os salários (em R$) de uma pequena equipe: **2000, 2200, 2500, 2800 e 50000** — este último, de um sócio-diretor. Ele precisa reportar à diretoria um **valor que represente o salário típico** da equipe, evitando uma medida **distorcida pelo valor atípico**.

Assinale a alternativa correta.

A) A média (~11 900) é a melhor medida, pois usa todos os valores.
B) A moda é a única medida válida para dados numéricos.
C) A mediana (2500) representa melhor o típico, pois é robusta a *outliers*.
D) O valor extremo (50000) não afeta a média.

---

## Q11 · Resposta: **C**

**Relembrando (Estatística descritiva):** a **média** usa todos os valores e por isso é **sensível a *outliers***; a **mediana** (valor central) é **robusta**.

- O salário de 50000 puxa a **média** para ~11 900 — que **não representa** ninguém do grupo. A **mediana (2500)** descreve melhor o "típico". ✅
- Em distribuições **assimétricas**, prefira a mediana (é o que o **boxplot** evidencia).

---

## Q12 · Análise de Dados

Dois times de vendas têm o **mesmo faturamento médio** mensal. Ao inspecionar os dados, um analista percebe que, no **time A**, os valores mensais ficam **muito próximos da média**, enquanto no **time B** eles **oscilam bastante** (meses muito altos e muito baixos).

Sobre as medidas de dispersão aplicáveis a essa comparação, assinale a alternativa correta.

A) Desvio-padrão e IQR não têm relação com dispersão.
B) O IQR é sensível a *outliers*, por isso deve ser evitado.
C) Como as médias são iguais, o desvio-padrão também será.
D) O **time B** tem **maior desvio-padrão**; o **IQR** mede os 50% centrais e é robusto a *outliers*.

---

## Q12 · Resposta: **D**

**Relembrando (Medidas de variabilidade):** o **desvio-padrão** mede o espalhamento **em torno da média** — logo, **mesma média não significa mesma dispersão**.

- O **time B**, que oscila mais, tem **maior desvio-padrão**. ✅
- O **IQR** = Q3 − Q1 resume os **50% centrais** e é **robusto a *outliers*** (por isso o **boxplot** usa quartis). O desvio-padrão **nunca** é negativo.

---

## Q13 · Análise de Dados

Uma equipe de vendas prepara um relatório para mostrar à diretoria a **evolução do faturamento mensal** ao longo de um ano (de janeiro a dezembro), de modo a **evidenciar a tendência** de crescimento no período.

Qual tipo de gráfico é o **mais adequado** para representar esses dados?

A) Gráfico de **linhas**, que mostra a evolução de um valor ao longo do tempo.
B) Gráfico de **pizza**, indicado para comparar a evolução temporal.
C) **Histograma**, próprio para exibir séries temporais.
D) Gráfico de **dispersão** entre o mês e o nome do produto.

---

## Q13 · Resposta: **A**

**Relembrando (Análise Exploratória — Visualização):** cada tipo de gráfico responde a uma pergunta diferente sobre os dados.

- **Linhas** → evolução de um valor **ao longo do tempo** (tendência) → é exatamente o caso. ✅
- **Pizza** mostra a **proporção** de um todo (não evolução); o **histograma** exibe a **distribuição de frequências** de uma variável numérica; a **dispersão** relaciona **duas variáveis numéricas**.

<div class="dica">💡 Escolha o gráfico pela pergunta: comparar, evoluir (tempo), distribuir ou relacionar.</div>

---

## Q14 · Análise de Dados

Uma equipe de dados faz um **teste A/B** para saber se uma nova versão do site aumenta a conversão. Define a hipótese nula **H₀** (não há diferença) e adota nível de significância **α = 0,05**. Ao final do experimento, obtém **p-valor = 0,03**.

Com base nesse resultado, assinale a decisão e a interpretação corretas.

A) O p-valor é a **probabilidade de H₀ ser verdadeira**.
B) Como **p (0,03) < α (0,05)**, **rejeita-se H₀**; o p-valor é a probabilidade de um resultado tão ou mais extremo, **supondo H₀ verdadeira**.
C) Como p < α, **aceita-se H₀**.
D) Rejeitar H₀ sendo ela verdadeira é **erro tipo II**.

---

## Q14 · Resposta: **B**

**Relembrando (Testes de hipótese / experimentos estatísticos):** o **p-valor** mede quão extremos são os dados **supondo H₀ verdadeira** — **não** é "a probabilidade de H₀".

- Regra de decisão: **p < α ⇒ rejeita-se H₀**. Aqui 0,03 < 0,05 → rejeita. ✅
- **Erro tipo I** = rejeitar H₀ **verdadeira** (probabilidade = α); **erro tipo II** = **não** rejeitar H₀ **falsa**. Um p pequeno é **evidência contra H₀**, não "prova" de H₁.

---

## Q15 · Análise de Dados

Uma empresa ajusta um modelo de **regressão linear** entre o **investimento mensal em anúncios** (x) e as **vendas** (y). O modelo tem coeficiente **angular positivo** e **R² = 0,64**. A partir disso, um gerente conclui que "aumentar anúncios **causa** aumento de vendas".

Sobre a interpretação correta desses resultados, assinale a alternativa correta.

A) O R² = 0,64 **prova** que anúncios **causam** vendas.
B) Coeficiente angular positivo indica **correlação negativa**.
C) O **R² = 0,64** indica que **64% da variabilidade** das vendas é explicada pelo modelo; **correlação não implica causalidade**.
D) Correlação de 0,64 significa **64% de acurácia** de classificação.

---

## Q15 · Resposta: **C**

**Relembrando (Regressão):** o **R²** é a proporção da **variabilidade** de `y` **explicada** pelo modelo (0,64 = **64%**; o resto é erro/outros fatores).

- O coeficiente **angular** dá a variação de `y` por unidade de `x` (é **diferente** do R²). ✅
- Alerta clássico do ENADE: a conclusão do gerente é indevida — **correlação/regressão ≠ causalidade** (pode haver **variável de confusão**).

---

## Q16 · Análise de Dados

Um cientista de dados treina um classificador e observa **acurácia de 99% no conjunto de treino**, mas apenas **70% no conjunto de teste** (dados não vistos). Tudo indica que o modelo "**decorou**" os exemplos de treino.

Assinale o diagnóstico e a mitigação corretos.

A) *Underfitting*; aumentar a complexidade do modelo.
B) O modelo está ideal, pois errou pouco no treino.
C) Vazamento de dados, que garante boa generalização.
D) *Overfitting*; mitigar com mais dados, regularização, menor complexidade e validação cruzada.

---

## Q16 · Resposta: **D**

**Relembrando (Machine Learning — viés × variância):** um **vão** entre bom desempenho no **treino** e ruim no **teste** = **overfitting** — o modelo **memorizou** o treino (**alta variância**) e **não generaliza**.

- Mitigações: **mais dados**, **regularização**, **reduzir a complexidade** e **validação cruzada**. ✅
- **Underfitting** seria erro **alto nos dois** (modelo simples demais).

---

## Q17 · Análise de Dados

Em um sistema de **detecção de fraude**, apenas **1% das transações são fraudulentas** (99% legítimas). Um modelo simplório que classifica **toda** transação como "legítima" alcança **99% de acurácia**, mas **não detecta nenhuma fraude**.

Sobre a avaliação de desempenho nesse cenário desbalanceado, assinale a alternativa correta.

A) A **acurácia é enganosa**; **precisão, revocação e F1** avaliam melhor a classe minoritária.
B) A acurácia de 99% indica boa detecção de fraudes.
C) A revocação mede a proporção de **negativos** corretos.
D) O F1 ignora os **falsos negativos**.

---

## Q17 · Resposta: **A**

**Relembrando (Classificação — métricas):** em dados **desbalanceados**, a **acurácia engana**: "sempre legítima" acerta 99%, mas tem **revocação 0** para fraude — **inútil**.

- **Revocação** = TP/(TP+FN): quantas fraudes **capturei**. **Precisão** = TP/(TP+FP). **F1** = média harmônica das duas. ✅
- Use **precisão/revocação/F1** (ou **AUC**) para a classe **rara**. *(Lembre da matriz de confusão.)*

---

## Q18 · Análise de Dados

Uma rede de varejo possui uma base de **clientes sem rótulos** (não há categoria previamente definida) e deseja **descobrir grupos** de clientes com comportamento de compra semelhante, para direcionar campanhas específicas a cada perfil.

Qual abordagem de aprendizado de máquina é adequada a esse objetivo?

A) Aprendizado **supervisionado** (classificação), pois há rótulos definidos.
B) Aprendizado **não supervisionado** (clusterização, ex.: *k-means*), que agrupa por similaridade.
C) **Regressão linear**, para prever o grupo.
D) É preciso **rotular manualmente** todos os clientes antes de qualquer análise.

---

## Q18 · Resposta: **B**

**Relembrando (Tipos de aprendizado):** **supervisionado** usa dados **rotulados** (`y` conhecido: classificação/regressão); **não supervisionado** **não tem rótulo** e busca **estrutura** nos dados.

- **Descobrir grupos** em clientes **sem rótulos** = **clusterização** (não supervisionado), ex.: **k-means**, que agrupa por **distância/similaridade**. ✅
- Sem `y`, não cabe classificação nem regressão.

---

## Q19 · Análise de Dados

Um analista usa a biblioteca **pandas** para resumir as vendas por região e executa o código a seguir:

```python
import pandas as pd
df = pd.DataFrame({'regiao': ['S','N','S','N'],
                   'venda':  [10, 20, 30, 40]})
r = df.groupby('regiao')['venda'].mean()
```

Assinale a alternativa que descreve corretamente o conteúdo de `r`.

A) Uma *Series* com a soma: S = 40, N = 60.
B) Um *DataFrame* com todas as linhas originais.
C) Uma *Series* com a média por região: S = 20.0 e N = 30.0.
D) Erro, pois `groupby` não aceita coluna categórica.

---

## Q19 · Resposta: **C**

**Relembrando (pandas — *split-apply-combine*):** `groupby('regiao')['venda'].mean()` **agrupa** pela região e calcula a **média** de `venda` em cada grupo.

- **S:** (10 + 30) / 2 = **20.0**; **N:** (20 + 40) / 2 = **30.0**. ✅
- O resultado é uma **Series** indexada pela `regiao` — não a soma, nem o primeiro valor, nem o DataFrame inteiro.

---

## Q20 · Análise de Dados

Ao preparar os dados de um modelo, um estagiário **normaliza (escalona) todo o conjunto** usando a média e o desvio calculados sobre **todos os registros** e, **em seguida**, separa em treino e teste. Na avaliação, o modelo apresenta métricas **excelentes** — que **não se confirmam em produção**.

Sobre o procedimento adotado, assinale a alternativa correta.

A) Não há problema; escalonar antes de dividir é a prática recomendada.
B) O correto é ajustar no teste e aplicar no treino.
C) Vazamento de dados melhora a generalização.
D) Há **vazamento de dados**: o *scaler* usou estatísticas do teste; o certo é ajustar (**fit**) só no treino e aplicar (**transform**) no teste.

---

## Q20 · Resposta: **D**

**Relembrando (Feature engineering / pré-processamento):** calcular média/desvio do escalonamento sobre **treino + teste** deixa informação do **teste vazar** para o treino (***data leakage***) e **infla** as métricas — que depois **não se confirmam** em produção.

- Regra de ouro: **`fit` só no treino**, **`transform`** no teste. ✅
- Um **`Pipeline`** + **`train_test_split`** (estratificado, em classificação) garante isso **automaticamente**.

---

<!-- _class: secao -->

# Fim do Esquenta 🔥
### Nas próximas aulas: revisão a fundo de BD, Análise de Dados e Sistemas Distribuídos.

**Gabarito:** 1A · 2B · 3C · 4D · 5A · 6B · 7C · 8D · 9A · 10B · 11C · 12D · 13A · 14B · 15C · 16D · 17A · 18B · 19C · 20D
