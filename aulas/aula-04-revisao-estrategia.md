---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Revisão final & Estratégia de prova

## Reta final para o ENADE

Tópicos Especiais II — ENADE · CC e SI · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## O que faremos hoje

<div class="cols">

<div>

**1. Estratégia de prova**
- Estrutura, tempo, discursivas, quando chutar.

</div>

<div>

**2. Revisão relâmpago + Esquenta**
- As frentes (BD, SIO, SD, Análise de Dados) e um Esquenta misto.

</div>

</div>

<div class="aviso">⚠️ Véspera do Simulado 2 — hoje é para <strong>afinar a estratégia</strong> e revisar o essencial.</div>

---

<!-- _class: secao -->

# Parte 1
### Estratégia de prova ENADE

---

## Como a prova é organizada

- **40 questões · 4 horas.**
- **Formação Geral (10):** 8 objetivas + 2 discursivas — comum a todos os cursos.
- **Componente Específico (30):** 27 objetivas + 3 discursivas — da sua área.
- **Peso:** Formação Geral **25%** · Componente Específico **75%**.
- **Questionário do estudante** (obrigatório) e questionário de percepção da prova.

<div class="dica">💡 São <strong>5 discursivas</strong> no total — elas pesam e não podem ficar em branco.</div>

---

## Gestão do tempo

- **~6 minutos por questão**, em média — mas **reserve tempo** para as **discursivas**.
- **Não empaque:** marque a questão difícil, siga em frente e **volte depois**.
- Faça primeiro o que **domina** (garante pontos), depois o resto.
- **Controle o relógio:** um "checkpoint" na metade da prova.

---

## Discursivas: como pontuar

- **Leia o comando** e responda **exatamente o que se pede** (verbo: "explique", "compare", "justifique").
- **Estruture:** ideia central → desenvolvimento → fechamento curto.
- Use **termos técnicos corretos** e **exemplos** quando couber.
- **Clareza e legibilidade** contam — nada de responder "por cima".
- Melhor **responder parcialmente** do que **deixar em branco**.

---

## Objetivas: quando (e como) chutar

- **Elimine distratores** — quase sempre dá para descartar 1 ou 2.
- Desconfie de **"sempre", "nunca", "apenas", "somente"** — costumam indicar alternativa falsa.
- Atenção a comandos **negativos**: "assinale a **INCORRETA**".
- **Leia todas** as alternativas antes de marcar.
- **Nunca deixe em branco** — no ENADE objetivo, errar **não** penaliza.

---

## No dia da prova

- Leve **documento oficial com foto**; chegue **cedo**.
- **Leia o texto-base com calma** — a resposta está na **análise** do contexto.
- Respire, **gerencie a ansiedade**, confie na sua preparação.
- **Preencha o questionário do estudante** — faz parte da avaliação.

<div class="dica">💡 Sua participação é <strong>coletiva</strong>: o resultado reflete e valoriza todo o curso.</div>

---

<!-- _class: secao -->

# Parte 2
### Revisão relâmpago das frentes

---

## As 4 frentes em um slide

<div class="cols">

<div>

**🗄️ Banco de Dados**
- Normalização (parcial→2FN, transitiva→3FN); `WHERE`×`HAVING`; ACID/anomalias; 2PL/deadlock; WAL; CAP/NoSQL.

**📊 Análise de Dados**
- Média×mediana (outliers); correlação≠causalidade; overfitting; precisão/revocação; *data leakage*.

</div>

<div>

**🏢 SIO**
- Dado×informação; níveis (SPT/SIG/SAD/EIS); ERP/CRM/SCM; BI×Data Mining×Big Data; virtualização/nuvem.

**🌐 Sistemas Distribuídos**
- Transparência; falha parcial; escalabilidade horizontal×vertical; cluster×grid; IaaS/PaaS/SaaS.

</div>

</div>

---

<!-- _class: secao -->

# 🗄️ Banco de Dados
### Frente 1 — revisão essencial

---

## BD — modelo relacional e normalização

<div class="cols">

<div>

**Chaves**
- **Superchave** identifica; **candidata** é mínima; **primária (PK)** é a escolhida; **estrangeira (FK)** aponta para a PK de outra tabela.
- **Integridade:** de entidade (PK única/não nula) · referencial (FK existe ou é nula) · de domínio (tipo/valor).

</div>

<div>

**Normalização (pela dependência)**
- **1FN:** valores **atômicos** (sem grupos repetidos).
- **2FN:** 1FN + sem **dependência parcial** da chave composta.
- **3FN:** 2FN + sem **dependência transitiva** (não-chave dependendo de não-chave).

</div>

</div>

<div class="dica">💡 Bizu: <strong>2FN</strong> mata a dependência <strong>parcial</strong>; <strong>3FN</strong> mata a <strong>transitiva</strong>. BCNF: todo determinante é chave candidata.</div>

---

## BD — SQL, transações e pegadinhas

<div class="cols">

<div>

**SQL**
- `WHERE` filtra **linhas antes** do `GROUP BY`; `HAVING` filtra **grupos depois** da agregação.
- **JOINs:** `INNER` (só o que casa) · `LEFT` (tudo da esquerda) · `FULL` (ambos, com NULLs).

**NoSQL & CAP**
- Tipos: chave-valor, documento, coluna, grafo. Sob **partição**, escolhe **C ou A**.

</div>

<div>

**Transações — ACID**
- **A**tomicidade · **C**onsistência · **I**solamento · **D**urabilidade.
- Anomalias: *dirty read*, *non-repeatable read*, *phantom* → **níveis de isolamento**.
- **2PL** evita conflito mas pode dar **deadlock**; **WAL** (log antes do dado) garante recuperação.

</div>

</div>

<div class="aviso">⚠️ Pegadinha da FK: <code>CASCADE</code> apaga os filhos · <code>RESTRICT/NO ACTION</code> bloqueia · <code>SET NULL</code> deixa órfão.</div>

---

<!-- _class: secao -->

# 📊 Análise de Dados
### Frente 2 — revisão essencial

---

## Análise — estatística e aprendizado

<div class="cols">

<div>

**Descritiva**
- **Média** sofre com **outliers**; **mediana** resiste → distribuição assimétrica pede **mediana**.
- **Desvio padrão** = dispersão em torno da média.

**Tipos de aprendizado**
- **Supervisionado** (rótulo): classificação/regressão.
- **Não supervisionado**: agrupamento (*clustering*).
- **Reforço**: aprende por recompensa.

</div>

<div>

**Viés × variância**
- **Underfitting** = viés alto: erra **treino e teste**.
- **Overfitting** = variância alta: acerta o treino, **falha no teste**.
- Corrige com **mais dados, regularização, validação cruzada**.

</div>

</div>

<div class="dica">💡 O <strong>vão</strong> entre acurácia de treino e teste é a assinatura do <strong>overfitting</strong>.</div>

---

## Análise — métricas e armadilhas

<div class="cols">

<div>

**Matriz de confusão**
- **Precisão** = dos previstos positivos, quantos acertei — VP/(VP+FP).
- **Revocação (recall)** = dos positivos reais, quantos peguei — VP/(VP+FN).
- **F1** = média harmônica de precisão e recall.

</div>

<div>

**Pegadinhas clássicas**
- **Acurácia engana** em classes **desbalanceadas** (99% prevendo "não-fraude") → olhe precisão/recall/F1.
- **Correlação ≠ causalidade** (variável de confusão).
- **Data leakage**: `fit` **só no treino**; no teste, só `transform`.

</div>

</div>

<div class="aviso">⚠️ Normalizar treino+teste juntos = vazamento → métricas infladas que somem em produção.</div>

---

<!-- _class: secao -->

# 🏢 SIO
### Frente 3 — revisão essencial

---

## SIO — dado, informação e a pirâmide

- **Dado** (bruto) → **Informação** (contextualizada) → **Conhecimento** (aplicável à decisão).

<div class="cols">

<div>

**Níveis (pirâmide de decisão)**
- **SPT/TPS** — operacional: registra **transações** (alto volume, missão crítica).
- **SIG/MIS** — tático: **relatórios** de rotina.

</div>

<div>

- **SAD/DSS** — decisão: análise **ad hoc**, cenários "e se".
- **SAE/EIS** — estratégico: painéis da **alta direção** (não estruturado).

</div>

</div>

<div class="dica">💡 "Registrar venda" = SPT · "relatório mensal" = SIG · "simular cenário" = SAD · "painel do CEO" = EIS.</div>

---

## SIO — sistemas integrados e BI

<div class="cols">

<div>

**Integrados**
- **ERP** integra processos internos; **CRM** foca no **cliente**; **SCM** na **cadeia de suprimentos**; **SGC** no conhecimento.

**Transacional × analítico**
- **OLTP** (dia a dia) × **OLAP** (multidimensional, análise).

</div>

<div>

**BI & dados**
- **Data Warehouse** = base histórica integrada para **BI**.
- **Data Mining** descobre **padrões ocultos**.
- **Big Data** = **5 Vs** (volume, velocidade, variedade, veracidade, valor).

</div>

</div>

<div class="aviso">⚠️ <strong>BI</strong> analisa o passado p/ decidir · <strong>Data Mining</strong> garimpa padrões · <strong>Big Data</strong> é a escala/variedade.</div>

---

<!-- _class: secao -->

# 🌐 Sistemas Distribuídos
### Frente 4 — revisão essencial

---

## SD — conceitos e transparências

<div class="cols">

<div>

- **Definição:** máquinas independentes que cooperam pela rede e parecem **um sistema único**.
- **Transparências:** acesso, localização, replicação, concorrência, **falha**.
- **Falha parcial:** parte cai e o resto segue — a ausência de resposta é **ambígua** (caiu? lento? perdeu?).

</div>

<div>

**Arquiteturas**
- **Cliente-servidor:** simples, mas **ponto único de falha**.
- **P2P:** sem servidor central, porém exige **coordenação**.

**Escalabilidade**
- **Vertical** = mais recurso na mesma máquina (limite físico).
- **Horizontal** = mais máquinas (elástica, preferida na nuvem).

</div>

</div>

---

## SD — nuvem e CAP

<div class="cols">

<div>

**Modelos de serviço**
- **IaaS** (infra: VM, rede) · **PaaS** (plataforma de desenvolvimento) · **SaaS** (software pronto, ex.: e-mail web).
- **Implantação:** pública · privada · **híbrida** · comunitária.

</div>

<div>

**Cluster × Grid × Cloud**
- **Cluster:** nós próximos, um objetivo.
- **Grid:** disperso geograficamente.
- **Cloud:** sob demanda, elástico, pago pelo uso.

**CAP:** sob **partição (P)**, **CP** recusa p/ manter consistência; **AP** responde com **consistência eventual**.

</div>

</div>

<div class="dica">💡 "Escalar adicionando servidores" = horizontal · "Gmail" = SaaS · "VM na nuvem" = IaaS.</div>

---

<!-- _class: secao -->

# 🔥 Esquenta misto
### Uma de cada frente (A–D) — reta final

---

## Q1 · Análise de Dados — Sobreajuste

Um modelo de classificação acerta **99% no treino** e apenas **68% no teste**.

O diagnóstico e a correção são:

A) *underfitting*; reduzir os dados de treino.
B) **overfitting; regularizar, simplificar o modelo e usar validação cruzada.**
C) modelo ideal, pois acertou muito no treino.
D) erro de digitação; ignorar.

---

## Q1 · Gabarito: **B**

**Relembrando:** o **vão** entre treino (99%) e teste (68%) é a marca do **overfitting** — o modelo **memorizou** e não **generaliza** (alta variância).

- Corrige-se com **mais dados, regularização, menos complexidade e validação cruzada**. *Underfitting* seria erro **alto nos dois**.

---

## Q2 · Análise de Dados — Correlação e causa

Uma análise mostra **forte correlação** entre vendas de sorvete e casos de afogamento no verão.

A conclusão correta é:

A) sorvete causa afogamento.
B) afogamento causa consumo de sorvete.
C) **correlação não implica causalidade — há uma variável de confusão (o calor/verão).**
D) a correlação prova a causa entre as duas.

---

## Q2 · Gabarito: **C**

**Relembrando:** **correlação ≠ causalidade**. Uma **variável de confusão** (o **calor** do verão) eleva **as duas** coisas ao mesmo tempo.

- É um alerta clássico do ENADE: cuidado ao inferir **causa** a partir de **associação**.

---

## Q3 · Banco de Dados — Integridade referencial

Numa tabela `Pedido` com FK para `Cliente`, deseja-se **impedir** a exclusão de um cliente que **ainda possui pedidos**.

A cláusula adequada na definição da FK é:

A) **`ON DELETE RESTRICT` (ou `NO ACTION`).**
B) `ON DELETE CASCADE`.
C) `ON DELETE SET NULL`.
D) Nenhuma; o banco nunca impede exclusões.

---

## Q3 · Gabarito: **A**

**Relembrando (integridade referencial):** **`RESTRICT`/`NO ACTION`** **bloqueia** a exclusão do cliente enquanto houver pedidos referenciando-o. ✅

- **`CASCADE`** apagaria os pedidos junto; **`SET NULL`** deixaria os pedidos **órfãos** (FK nula).

---

## Q4 · SIO — Nível de sistema

O caixa de um supermercado registra **cada venda** em tempo real, dando baixa no estoque. Trata-se de um sistema **operacional**, de **alto volume** e **missão crítica**.

Esse é um exemplo de:

A) SAE/EIS — apoio ao executivo.
B) SAD/DSS — apoio à decisão.
C) SIG/MIS — relatórios gerenciais.
D) **SPT/TPS — processamento de transações.**

---

## Q4 · Gabarito: **D**

**Relembrando (pirâmide de decisão):** registrar **transações** no nível **operacional**, em alto volume e missão crítica = **SPT/TPS**. ✅

- SIG/SAD são **táticos** (relatórios/decisão); EIS é **estratégico** (não estruturado).

---

## Q5 · Sistemas Distribuídos — CAP

Um sistema distribuído global precisa **permanecer consistente** e, diante de uma **partição de rede**, prefere **recusar operações** a devolver dados divergentes.

Segundo o CAP, essa é uma escolha:

A) **CP — prioriza consistência e tolerância a partição, sacrificando disponibilidade.**
B) AP — prioriza disponibilidade.
C) CA — garante as três ao mesmo tempo.
D) indiferente; o CAP não se aplica.

---

## Q5 · Gabarito: **A**

**Relembrando (CAP):** sob **partição (P)**, escolhe-se **C ou A**. Preferir **consistência** e **recusar operações** durante a partição = **CP**. ✅

- **AP** manteria a disponibilidade com **consistência eventual**; **CA** simultâneo é **impossível** sob partição.

---

## Q6 · Análise de Dados — Vazamento de dados

Um estagiário **normaliza toda a base** (treino + teste) antes de dividi-la e obtém métricas **ótimas** que **não se repetem em produção**.

O problema é:

A) falta de dados de treino.
B) *underfitting*.
C) **vazamento de dados: o *scaler* usou estatísticas do teste; o certo é `fit` só no treino.**
D) excesso de regularização.

---

## Q6 · Gabarito: **C**

**Relembrando (pré-processamento):** ajustar o escalonamento sobre **treino + teste** deixa o teste **vazar** para o treino (***data leakage***) e **infla** as métricas.

- Regra: **`fit` só no treino**, **`transform`** no teste — de preferência via **`Pipeline`**.

---

<!-- _class: secao -->

# Boa prova! 🍀
### Confie na preparação · leia o contexto · não deixe em branco.

**Gabarito:** 1B · 2C · 3A · 4D · 5A · 6C
