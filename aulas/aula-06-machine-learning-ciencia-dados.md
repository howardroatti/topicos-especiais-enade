---
marp: true
theme: faesa
paginate: true
footer: 'Prof. M.Sc. Howard Cruz Roatti · FAESA · Tópicos Especiais II — ENADE · 2026/2'
---

<!-- _class: capa -->
<!-- _paginate: false -->

# Revisão ENADE — Machine Learning & Ciência de Dados

## Do dado bruto ao modelo avaliado

Tópicos Especiais II — ENADE · CC e SI · 2026/2
Prof. M.Sc. Howard Cruz Roatti

---

## Como funciona esta revisão

<div class="cols">

<div>

**1. Recaptura relâmpago**
- Os conceitos-chave de **ML e Ciência de Dados** em uma passada rápida.
- Foco no que o **ENADE cobra**: tipos de aprendizado, avaliação de modelos, armadilhas.

</div>

<div>

**2. 🔥 Esquenta**
- **10 questões** estilo ENADE (situação-problema → A–D).
- Responda **antes** de virar o gabarito comentado.

</div>

</div>

<div class="dica">💡 O ENADE cobra <strong>análise</strong>, não fórmula decorada: leia o cenário, veja qual métrica/técnica responde ao problema, elimine distratores.</div>

---

<!-- _class: secao -->

# Parte 1
### Recaptura relâmpago

---

## Ciência de Dados × IA × Machine Learning

<div class="cols">

<div>

- **Ciência de Dados:** processo amplo de **extrair conhecimento** de dados (estatística + computação + domínio).
- **Inteligência Artificial:** campo que busca **comportamento inteligente**.
- **Machine Learning:** sub-área da IA — o modelo **aprende padrões a partir de exemplos**, em vez de regras escritas à mão.

</div>

<div>

**A ideia central do ML**
- Aprendizado por **indução**: do **particular** (exemplos) para o **geral** (modelo que generaliza).
- O objetivo não é **decorar** os dados de treino, e sim **acertar em dados novos** (generalização).

</div>

</div>

<div class="dica">💡 "Deep Learning" ⊂ "Machine Learning" ⊂ "Inteligência Artificial". LLMs (IA generativa) são redes neurais profundas treinadas em texto.</div>

---

## O ciclo de um projeto de dados (CRISP-DM)

<div class="cols">

<div>

1. **Entendimento do negócio** — qual é a pergunta?
2. **Entendimento dos dados** — o que temos, qualidade.
3. **Preparação dos dados** — limpeza, transformação (a etapa mais demorada).
4. **Modelagem** — treinar os algoritmos.

</div>

<div>

5. **Avaliação** — o modelo responde à pergunta do passo 1?
6. **Implantação (deployment)** — colocar em produção e monitorar.

</div>

</div>

<div class="aviso">📌 O ciclo é <strong>iterativo</strong>: a avaliação costuma mandar você voltar para a preparação ou a modelagem.</div>

---

## Tipos de aprendizado

| Tipo | Os dados têm rótulo? | Para que serve | Exemplos |
|---|---|---|---|
| **Supervisionado** | **Sim** (entrada → saída conhecida) | prever um rótulo/valor | classificação, regressão |
| **Não supervisionado** | **Não** | achar estrutura escondida | **agrupamento (clustering)**, associação, redução de dimensionalidade |
| **Por reforço** | recompensa por **ação** | aprender uma política por tentativa e erro | robôs, jogos |

<div class="dica">💡 Pergunta-chave: <strong>"existe uma resposta certa rotulada no histórico?"</strong> → sim = supervisionado; não = não supervisionado.</div>

---

## Supervisionado: classificação × regressão

<div class="cols">

<div>

**Classificação**
- A saída é uma **categoria** (discreta).
- Ex.: *spam/não-spam*, *fraude/legítima*, *dígito 0–9*.
- Algoritmos: k-NN, árvore de decisão, Naive Bayes, SVM, regressão **logística**, redes neurais.

</div>

<div>

**Regressão**
- A saída é um **número contínuo**.
- Ex.: *preço do imóvel*, *consumo de energia*, *nota prevista*.
- Algoritmos: regressão **linear**, árvores de regressão, redes neurais.

</div>

</div>

<div class="dica">💡 Olhe o <strong>alvo</strong>: rótulo/categoria → classificação; quantidade/valor → regressão.</div>

---

## O pecado capital: overfitting × underfitting

<div class="cols">

<div>

- **Underfitting (sub-ajuste):** modelo **simples demais** — erra no treino **e** no teste (alto **viés**).
- **Overfitting (sobre-ajuste):** modelo **complexo demais** — **decora** o treino (inclui o ruído), vai **muito bem no treino** e **mal em dados novos** (alta **variância**).

</div>

<div>

**Como combater o overfitting**
- **Mais dados**; menos complexidade.
- **Regularização** (penaliza coeficientes grandes).
- **Validação cruzada** para escolher hiperparâmetros.
- *Early stopping*, *dropout* (redes neurais).

</div>

</div>

<div class="aviso">📌 Sintoma clássico de <strong>overfitting</strong>: acurácia alta no treino e <strong>queda forte</strong> no teste. É o caso mais cobrado no ENADE.</div>

---

## Treino, validação e teste

<div class="cols">

<div>

- **Treino:** o modelo **aprende** os parâmetros.
- **Validação:** ajuste de **hiperparâmetros** e escolha do modelo.
- **Teste:** estimativa **final e imparcial** do desempenho — usado **uma vez**, no fim.

</div>

<div>

**Validação cruzada (k-fold)**
- Divide os dados em **k partes**; treina em k−1 e testa na que sobrou; repete k vezes e **faz a média**.
- Usa melhor os dados e dá uma estimativa **mais estável** que um único *holdout*.

</div>

</div>

<div class="dica">⚠️ <strong>Vazamento de dados (data leakage):</strong> normalizar/ajustar usando o conjunto de teste contamina a avaliação. <strong>Separe primeiro</strong>, transforme depois (ajuste só no treino).</div>

---

## Avaliação de classificação: a matriz de confusão

<div class="cols">

<div>

|  | **Previu Positivo** | **Previu Negativo** |
|---|---|---|
| **Real Positivo** | VP (acerto) | FN (erro: deixou passar) |
| **Real Negativo** | FP (alarme falso) | VN (acerto) |

</div>

<div>

- **Acurácia** = (VP+VN) / total
- **Precisão** = VP / (VP+FP) — *dos que eu marquei, quantos eram mesmo?*
- **Revocação (recall)** = VP / (VP+FN) — *dos que eram, quantos eu peguei?*
- **F1** = média harmônica de precisão e recall.

</div>

</div>

<div class="aviso">📌 Em base <strong>desbalanceada</strong> (ex.: 99% legítimas), a <strong>acurácia engana</strong>: um modelo que chuta sempre "classe maior" acerta 99% e não serve. Olhe <strong>recall/precisão/F1</strong> da classe rara.</div>

---

## Avaliação de regressão & pré-processamento

<div class="cols">

<div>

**Métricas de regressão**
- **MAE** — erro absoluto médio.
- **MSE / RMSE** — penaliza **mais** os erros grandes.
- **R²** — fração da variância explicada (1 = perfeito; 0 = igual à média).

</div>

<div>

**Pré-processamento (preparação)**
- **Dados faltantes:** remover ou imputar (média/mediana/modelo).
- **Escala:** normalização/padronização (importa p/ k-NN, SVM, redes).
- **Categóricos:** *one-hot / label encoding*.
- **Desbalanceamento:** reamostragem (*over/under-sampling*, SMOTE).

</div>

</div>

<div class="dica">💡 <strong>Correlação não é causação:</strong> duas variáveis andarem juntas não prova que uma causa a outra (pode haver um fator oculto).</div>

---

<!-- _class: secao -->

# Parte 2
### 🔥 Esquenta — 10 questões estilo ENADE
Leia a situação · **responda** · só então vire o gabarito comentado.

---

## Q1 — Qual é o tipo de aprendizado?

Uma operadora quer **segmentar** a base de clientes em grupos de perfil **semelhante** para campanhas de marketing. **Não existe** um rótulo prévio dizendo a que grupo cada cliente pertence; os grupos devem **emergir dos próprios dados**.

Esse problema é de aprendizado:

A) Supervisionado de classificação.
B) Supervisionado de regressão.
C) Não supervisionado (agrupamento).
D) Por reforço.

---

## Q1 — Gabarito: **C**

**Como pensar:** a frase "**não existe rótulo prévio**" e "os grupos **emergem dos dados**" é a assinatura do **aprendizado não supervisionado** — especificamente **clustering** (ex.: *k-means*).

- **A/B** exigiriam um alvo **rotulado** no histórico (categoria ou número) — não há.
- **D** envolve um agente tomando **ações** e recebendo **recompensas**, que não é o caso.

<div class="dica">💡 Segmentar/agrupar sem resposta certa conhecida = <strong>clustering</strong>.</div>

---

## Q2 — O modelo que decorou

Um classificador atingiu **99% de acurácia no conjunto de treino**, mas apenas **62% no conjunto de teste**. O gráfico mostra o erro de treino caindo sempre, enquanto o erro de validação **volta a subir**.

O diagnóstico e uma medida corretiva adequada são:

A) Underfitting; aumentar a complexidade do modelo.
B) Overfitting; aplicar regularização / mais dados / validação cruzada.
C) Vazamento de dados; trocar a métrica de avaliação.
D) Desbalanceamento; usar acurácia em vez de F1.

---

## Q2 — Gabarito: **B**

**Como pensar:** **ótimo no treino + ruim no teste** e **erro de validação subindo** é o retrato do **overfitting** (o modelo decorou o ruído e não generaliza).

- **A** é o oposto (underfitting erra **nos dois**); aumentar a complexidade **pioraria**.
- **C/D** descrevem outros problemas; aqui o sintoma é claramente de **variância alta**.

<div class="aviso">📌 Regularização, mais dados e reduzir complexidade são as respostas padrão para overfitting.</div>

---

## Q3 — Matriz de confusão (conta rápida)

Um filtro de spam foi avaliado em 500 e-mails. Dos resultados: **VP = 70**, **FP = 10**, **FN = 30**, **VN = 390** (positivo = "spam").

Qual é a **precisão** do filtro?

A) 0,70
B) 0,875
C) 0,92
D) 0,14

---

## Q3 — Gabarito: **B**

**Como pensar:** **Precisão = VP / (VP + FP)** = *dos que marquei como spam, quantos eram mesmo spam?*

- Precisão = 70 / (70 + 10) = 70/80 = **0,875**. ✅
- **A** = 0,70 é a **revocação** (70/(70+30)); **C** = 0,92 é a **acurácia** ((70+390)/500); **D** troca numerador e denominador.

<div class="dica">💡 Precisão olha a <strong>coluna do "previu positivo"</strong>; revocação olha a <strong>linha do "real positivo"</strong>.</div>

---

## Q4 — Quando a acurácia mente

Um banco tem **1% de transações fraudulentas**. Um modelo classifica **todas** as transações como "legítimas" e, com isso, alcança **99% de acurácia**.

A melhor conclusão é:

A) O modelo é excelente, pois 99% é altíssimo.
B) A acurácia é a métrica ideal para esse problema.
C) A acurácia engana em base desbalanceada; deve-se olhar recall/precisão/F1 da classe fraude.
D) Basta aumentar o conjunto de treino para resolver.

---

## Q4 — Gabarito: **C**

**Como pensar:** o modelo **nunca detecta fraude** (recall da fraude = **0**), mas a acurácia fica alta só porque a classe "legítima" domina.

- Em dados **desbalanceados**, a métrica precisa focar na **classe rara**: **recall, precisão, F1** (ou AUC-ROC).
- **A/B** caem na armadilha; **D** não ataca a causa (métrica inadequada + desbalanceamento).

<div class="aviso">📌 Pergunta-chave em base rara: "<strong>quantos casos positivos o modelo realmente pegou?</strong>" → revocação.</div>

---

## Q5 — Por que validação cruzada?

Uma equipe tem **poucos dados** e percebe que, dependendo de **como** separa treino e teste, o desempenho medido **varia muito**.

A técnica que dá uma estimativa **mais estável** usando melhor os dados é:

A) Treinar e testar no mesmo conjunto.
B) Validação cruzada k-fold.
C) Aumentar o número de épocas de treino.
D) Remover o conjunto de teste.

---

## Q5 — Gabarito: **B**

**Como pensar:** a **validação cruzada k-fold** reparte os dados em *k* dobras, revezando qual é a de teste, e **faz a média** — reduzindo a sorte/azar de uma única divisão e aproveitando todos os dados.

- **A** mede o modelo nos dados que ele já viu → otimismo (overfitting não detectado).
- **C** não muda a forma de **avaliar**; **D** eliminaria a própria avaliação.

---

## Q6 — Classificação ou regressão?

Uma imobiliária quer um modelo que **estime o valor de venda** (em reais) de um imóvel a partir de área, bairro e número de quartos.

Trata-se de um problema de:

A) Regressão (saída contínua).
B) Classificação binária.
C) Agrupamento (clustering).
D) Regras de associação.

---

## Q6 — Gabarito: **A**

**Como pensar:** o alvo é um **número contínuo** (preço em reais) → **regressão**. Métricas típicas: **MAE, RMSE, R²**.

- **B** seria se a saída fosse uma **categoria** (ex.: "caro/barato"); **C** não tem alvo; **D** busca itens que ocorrem juntos ("quem compra X também compra Y").

<div class="dica">💡 "Quanto?" → regressão. "Qual categoria?" → classificação.</div>

---

## Q7 — O parâmetro do k-means

Uma analista aplica o algoritmo **k-means** para agrupar clientes. Antes de rodar, ela precisa **definir previamente**:

A) Os rótulos corretos de cada cliente.
B) O número de grupos (k).
C) A variável-alvo a ser prevista.
D) A matriz de confusão.

---

## Q7 — Gabarito: **B**

**Como pensar:** o **k-means** é **não supervisionado** — não há rótulo nem alvo. O que o usuário precisa informar é **quantos grupos (k)** deseja formar.

- **A/C** pressupõem aprendizado **supervisionado** (que não existe aqui); **D** é ferramenta de **classificação**, não de clustering.

<div class="dica">💡 Escolher o *k*: métodos como o <strong>"cotovelo" (elbow)</strong> e a <strong>silhueta</strong> ajudam a decidir.</div>

---

## Q8 — O equilíbrio viés × variância

Ao aumentar a complexidade de um modelo, observa-se que o **viés diminui** mas a **variância aumenta**, e o erro em dados novos passa a **piorar** depois de certo ponto.

Esse fenômeno é descrito pelo:

A) Teorema de Bayes.
B) Compromisso (trade-off) entre viés e variância.
C) Princípio da independência condicional.
D) Teorema do limite central.

---

## Q8 — Gabarito: **B**

**Como pensar:** modelos **simples** → **viés alto** (underfitting); modelos **complexos** → **variância alta** (overfitting). O erro de generalização é minimizado em um **ponto de equilíbrio** — o **trade-off viés–variância**.

- **A/C** são da base do Naive Bayes; **D** é um resultado estatístico sobre distribuições de médias — nada disso descreve esse equilíbrio.

---

## Q9 — A ordem certa das etapas

Ao preparar os dados, um estudante **normalizou todo o conjunto** usando média e desvio **calculados sobre a base inteira** e **só depois** separou treino e teste.

A crítica correta é:

A) O procedimento está certo; normalizar antes sempre ajuda.
B) Houve vazamento de dados: a estatística deve ser ajustada só no treino e aplicada ao teste.
C) Normalização nunca deve ser usada em ML.
D) O erro foi não ter removido a variável-alvo.

---

## Q9 — Gabarito: **B**

**Como pensar:** usar o **conjunto de teste** para calcular média/desvio **contamina** a avaliação — o modelo "enxergou" informação do teste. Isso é **data leakage (vazamento)**.

- O correto: **separar primeiro**, **ajustar a transformação no treino** e **aplicá-la** ao teste com os mesmos parâmetros.
- **A** repete o erro; **C** é falso (normalizar é útil); **D** confunde o problema.

<div class="aviso">📌 Regra de ouro: nada do conjunto de teste pode influenciar o treino — nem a normalização.</div>

---

## Q10 — Correlação, causação e IA generativa

Dois achados de um time de dados:
(i) nos dados históricos, **vendas de sorvete** e **afogamentos** sobem juntos;
(ii) um **LLM** (IA generativa) afirmou, com texto fluente, que "sorvete causa afogamento".

A leitura tecnicamente correta é:

A) Como há correlação forte, está provada a causação.
B) O LLM é uma fonte infalível, pois foi treinado em muitos dados.
C) Correlação não implica causação (há um fator oculto — o calor); e saídas de LLM podem "alucinar" e precisam de verificação.
D) Afogamentos causam o consumo de sorvete.

---

## Q10 — Gabarito: **C**

**Como pensar:** sorvete e afogamento sobem juntos por causa de um **terceiro fator** (calor/verão) — **correlação ≠ causação**.

- Além disso, um **LLM** gera texto plausível mas pode **alucinar** (afirmar com confiança algo falso); suas respostas são **insumo a verificar**, não prova.
- **A/B/D** confundem associação com causa ou atribuem autoridade indevida ao modelo.

<div class="dica">💡 No ENADE recente, IA generativa aparece como ferramenta de apoio — cobra-se <strong>uso crítico</strong>, não fé cega.</div>

---

<!-- _class: secao -->

# Fim — ML & Ciência de Dados 🤖
### Errou alguma? Anote o **eixo**, não a questão.

**Gabarito:** 1C · 2B · 3B · 4C · 5B · 6A · 7B · 8B · 9B · 10C

<div class="dica">💡 Eixos para revisar: tipos de aprendizado · overfitting/viés–variância · matriz de confusão & métricas · validação cruzada · vazamento de dados · correlação ≠ causação.</div>
