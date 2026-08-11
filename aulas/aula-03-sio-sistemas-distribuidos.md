---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Revisão ENADE — SIO & Sistemas Distribuídos

## Sistemas de Informação nas organizações + computação distribuída

Tópicos Especiais II — ENADE · CC e SI · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## Como funciona esta revisão

<div class="cols">

<div>

**Bloco A — SIO**
- Sistemas de Informação **nas organizações**.
- Recaptura + 🔥 Esquenta.

</div>

<div>

**Bloco B — Sistemas Distribuídos**
- Computação **distribuída** e nuvem.
- Recaptura + 🔥 Esquenta.

</div>

</div>

<div class="dica">💡 São dois temas do componente específico do ENADE — leia o contexto e decida pela análise.</div>

---

<!-- _class: secao -->

# Bloco A — SIO
### Sistemas de Informações Organizacionais

---

## Informação e conhecimento

- **Dado × Informação × Conhecimento** (Davenport):
  - **Dado** = fato bruto, sem contexto (ex.: "1500").
  - **Informação** = dado com **relevância e propósito** (ex.: "vendas de maio = R$ 1500").
  - **Conhecimento** = informação + experiência/contexto para **decidir**.
- **Ciclo de vida da informação:** criação → armazenamento → transporte → uso → descarte.
- **Qualidade da informação** e **valor da TI**; "informação é poder".

---

## Tipos de SI por nível organizacional

<div class="cols">

<div>

**Pirâmide de decisão**
- **Estratégico** → **SAE/EIS/ESS** (decisões **não estruturadas**).
- **Tático/gerencial** → **SIG/MIS** e **SAD/DSS** (relatórios, simulação de cenários).
- **Operacional** → **SPT/TPS** (processa **transações**; missão crítica).

</div>

<div>

**Sistemas integrados**
- **ERP** — integra os módulos da empresa.
- **CRM** — relacionamento com o cliente.
- **SCM** — cadeia de suprimentos.
- **BI / DW / Data Mining / Big Data** — apoio à decisão.

</div>

</div>

---

## TI, infraestrutura e vantagem competitiva

- **TI como vantagem competitiva** (Porter — **cadeia de valor**): a informação diferencia a empresa dos concorrentes de forma **duradoura**.
- **Infraestrutura:** arquitetura de **Von Neumann**; **cliente-servidor** (2 e 3 camadas); **virtualização**; **computação em nuvem**; Data Center.
- **Redes:** modelo de camadas **OSI / TCP-IP**; protocolos de aplicação (HTTP, SMTP, FTP…).

<div class="dica">💡 <strong>Data Mining</strong>, <strong>BI</strong> e <strong>Big Data</strong> <strong>não são sinônimos</strong> — cada um resolve um problema diferente (voltamos a isso na Q3).</div>

---

<!-- _class: secao -->

# Bloco A — 🔥 Esquenta SIO
### Questões estilo ENADE (A–D)

---

## Q1 · SIO — Dado × Informação

Um sistema registra a leitura "**38**" de um sensor. Sozinho, esse número **não orienta nenhuma decisão**; já a frase "**temperatura do paciente = 38 °C, acima do normal**" permite ao médico agir.

A diferença entre os dois é que o segundo é:

A) apenas um dado, pois contém um número.
B) **informação — dado com contexto e propósito, que apoia a decisão.**
C) conhecimento tácito, impossível de registrar.
D) um ruído, sem valor para a organização.

---

## Q1 · Gabarito: **B**

**Relembrando (Unidade 1):** **dado** é o fato bruto ("38"); **informação** é o dado com **contexto e relevância** ("38 °C, acima do normal") que **apoia a decisão**.

- **Conhecimento** iria além: a experiência do médico para **interpretar e agir**. O dado isolado não é ruído — falta-lhe **contexto**.

---

## Q2 · SIO — Níveis de sistema

A diretoria de uma rede varejista precisa de um sistema para **analisar cenários de longo prazo** (abrir novas lojas, entrar em novos mercados) — decisões **não estruturadas** e estratégicas.

Que tipo de sistema atende melhor a essa necessidade?

A) SPT/TPS — processamento de transações.
B) SIG/MIS — relatórios gerenciais de rotina.
C) **SAE/EIS — sistema de apoio ao executivo (nível estratégico).**
D) Sistema de automação de escritório.

---

## Q2 · Gabarito: **C**

**Relembrando (Unidade 4 — pirâmide de decisão):** cada nível tem seu sistema.

- **Estratégico / não estruturado** → **SAE/EIS/ESS**. ✅
- **SPT** é **operacional** (transações); **SIG** é **tático** (relatórios de rotina); automação de escritório é do nível de **conhecimento**.

---

## Q3 · SIO — Data Mining × BI × Big Data

Uma empresa acumula **enormes volumes** de dados de diversas fontes, em alta **velocidade** e **variedade** (texto, cliques, sensores), e quer, entre outras coisas, **descobrir padrões ocultos** de compra.

Sobre os conceitos envolvidos, assinale a correta.

A) Big Data e Data Mining são sinônimos.
B) BI é a técnica de garimpar padrões em grandes bases.
C) Data Mining é o mesmo que Data Warehouse.
D) **Big Data descreve o desafio (volume, velocidade, variedade); Data Mining garimpa padrões; BI dá apoio à decisão.**

---

## Q3 · Gabarito: **D**

**Relembrando (Unidade 4):** são conceitos **complementares**, não sinônimos.

- **Big Data** = os **3 Vs** (volume, velocidade, variedade) — o desafio dos dados.
- **Data Mining** = **garimpar padrões** (mineração).
- **BI** = transformar dados em **apoio à decisão** (relatórios, dashboards). O **DW** é o repositório que os alimenta.

---

## Q4 · SIO — Sistemas integrados

Uma indústria quer **unificar** finanças, estoque, produção e RH em uma **base única**, eliminando planilhas isoladas e retrabalho entre setores.

O sistema mais adequado é o:

A) **ERP — integra os módulos/processos da empresa numa base única.**
B) CRM — foco no relacionamento com o cliente.
C) SCM — foco na cadeia de suprimentos externa.
D) SPT isolado por setor.

---

## Q4 · Gabarito: **A**

**Relembrando (Unidade 4):** o **ERP** (Enterprise Resource Planning) **integra os módulos** internos numa **base única** — fim das ilhas de informação.

- **CRM** cuida do **cliente**; **SCM** da **cadeia de suprimentos**; SPTs isolados **não** integram.

---

## Q5 · SIO — Infraestrutura de TI

Um provedor precisa **executar vários servidores lógicos** (web, banco, e-mail) sobre **um mesmo servidor físico**, aproveitando melhor o hardware e isolando os ambientes.

A tecnologia empregada é a:

A) computação de alto desempenho (HPC).
B) arquitetura cliente-servidor de 2 camadas.
C) **virtualização.**
D) topologia de rede em estrela.

---

## Q5 · Gabarito: **C**

**Relembrando (Unidade 3 — Infraestrutura):** **virtualização** cria **máquinas virtuais** sobre um mesmo hardware físico — melhor uso de recursos, **isolamento** e base para a **nuvem**.

- HPC é processamento intensivo; cliente-servidor é modelo de aplicação; estrela é topologia física.

---

<!-- _class: secao -->

# Bloco B — Sistemas Distribuídos
### Computação distribuída e nuvem

---

## Fundamentos de SD

- **Definição:** conjunto de **computadores independentes** que se apresenta ao usuário como um **sistema único e coerente**.
- **Transparência** (esconder a distribuição): de **acesso, localização, replicação, concorrência e falha**.
- **Falha parcial:** parte do sistema falha e o resto continua — a **ausência de resposta é ambígua** (caiu? lento? perdeu-se?). Trata-se com **timeouts** e repetição **idempotente**.
- **8 falácias:** "a rede é confiável / latência é zero / banda é infinita / a rede é segura / a topologia não muda / há um só administrador / custo de transporte é zero / a rede é homogênea".

---

## Arquiteturas, comunicação e nuvem

- **Modelos:** **cliente-servidor** (2/3 camadas; *thin* × *fat client*), **P2P** (estruturado com **DHT**), camadas, publish-subscribe.
- **Comunicação:** **Sockets** (TCP/UDP), **RPC/RMI**, **Middleware** (CORBA), **Web Services** (**SOAP** e **REST**), **SOA**, **microsserviços**.
- **Escalabilidade:** **vertical** (*scale-up*: nó mais potente) × **horizontal** (*scale-out*: mais nós).
- **Tolerância a falhas:** **replicação** (ativa × primário-backup); **CAP** (sob partição, C **ou** A).
- **Nuvem:** **IaaS · PaaS · SaaS**; pública / privada / híbrida; **elasticidade**.

---

<!-- _class: secao -->

# Bloco B — 🔥 Esquenta SD
### Questões estilo ENADE (A–D)

---

## Q6 · SD — Transparência

Ao acessar um arquivo em um sistema distribuído, o usuário o utiliza **como se fosse local** e **não sabe em qual servidor** ele está fisicamente armazenado.

A propriedade que **esconde a localização física** do recurso é a transparência de:

A) concorrência.
B) falha.
C) **localização.**
D) replicação.

---

## Q6 · Gabarito: **C**

**Relembrando:** **transparência** é esconder a distribuição. Aqui, não saber **onde** está o dado = transparência de **localização**. ✅

- **Acesso** = usar recurso remoto como local; **replicação** = não perceber as cópias; **concorrência** = não perceber o compartilhamento; **falha** = não perceber panes.

---

## Q7 · SD — Falha parcial

Um serviço **A** envia uma requisição ao serviço **B** e **não recebe resposta** no tempo esperado.

Assinale a alternativa correta.

A) A pode concluir **com certeza** que B falhou.
B) **A não distingue, só pela ausência de resposta, se B caiu, está lento ou se a resposta se perdeu.**
C) O uso de TCP **elimina** essa incerteza.
D) A deve encerrar todo o sistema, pois é uma falha total.

---

## Q7 · Gabarito: **B**

**Relembrando:** é a **falha parcial** — a ausência de resposta é **ambígua**. O **TCP não elimina** o problema (B pode cair **depois** de receber). Trata-se com **timeout + repetição idempotente**. ✅

- As demais afirmam **certezas** que A não possui.

---

## Q8 · SD — Escalabilidade

Para atender à demanda crescente, uma equipe decide **acrescentar mais servidores** ao sistema para dividir a carga, em vez de depender de **uma única máquina cada vez maior**.

Essa estratégia é a escalabilidade:

A) vertical (*scale-up*).
B) de replicação.
C) transparente.
D) **horizontal (*scale-out*).**

---

## Q8 · Gabarito: **D**

**Relembrando:** **horizontal (*scale-out*)** = **mais nós** dividindo a carga — base dos SD e da nuvem. ✅

- **Vertical (*scale-up*)** = **um** servidor mais potente (tem limite físico e ponto único de falha). Replicação e transparência são outros conceitos.

---

## Q9 · SD — Cluster × Grid

Uma universidade une **máquinas heterogêneas** de **várias instituições parceiras**, com sistemas operacionais diferentes, para processar em conjunto um grande experimento científico.

Esse arranjo caracteriza um sistema de computação em:

A) **grade (*grid*) — recursos heterogêneos de organizações distintas.**
B) cluster — máquinas homogêneas dedicadas.
C) mainframe centralizado.
D) cliente-servidor de 2 camadas.

---

## Q9 · Gabarito: **A**

**Relembrando (Tipos de SD):** **grid** reúne recursos **heterogêneos** de **organizações diferentes** (parceria), com SOs distintos. ✅

- O **cluster** usa máquinas **homogêneas e dedicadas** para aumentar o processamento. Mainframe e cliente-servidor de 2 camadas não são o caso.

---

## Q10 · SD — Computação em nuvem

Uma startup quer **hospedar sua aplicação** sem gerenciar servidores físicos, pagando pelo uso e **escalando automaticamente** conforme a demanda. Ela contrata **máquinas virtuais e armazenamento** sob demanda, mantendo controle do sistema operacional.

Esse modelo de serviço de nuvem é o:

A) SaaS — software como serviço.
B) **IaaS — infraestrutura (VMs, armazenamento, rede) como serviço.**
C) PaaS — plataforma como serviço.
D) On-premise (local, sem nuvem).

---

## Q10 · Gabarito: **B**

**Relembrando (Nuvem):** contratar **VMs, armazenamento e rede** sob demanda, mantendo o **SO** sob seu controle = **IaaS**. ✅

- **PaaS** entrega a **plataforma** (você só publica o código); **SaaS** entrega o **software pronto** (ex.: e-mail web); *on-premise* não é nuvem.

---

<!-- _class: secao -->

# Fim da revisão — SIO & Sistemas Distribuídos 🌐
### Continue treinando com os Esquentas e o material das disciplinas.

**Gabarito:** 1B · 2C · 3D · 4A · 5C · 6C · 7B · 8D · 9A · 10B
