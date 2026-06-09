# Replicação Experimental: Análise de Sentimentos e Mineração de Tópicos em Avaliações de Medicamentos.

> 📖 **Artigo Base Utilizado:** [Clique aqui para acessar o PDF do artigo original](./s12874-021-01347-1.pdf)

Este repositório contém o desenvolvimento do trabalho final da disciplina de Processamento de Linguagem Natural (PLN). O projeto consiste na **reprodução experimental** do artigo científico "Machine learning in medicine: a practical introduction to natural language processing" focado na extração de insights, análise de sentimentos através de abordagens baseadas em léxico e aprendizado supervisionado a partir de revisões textuais de pacientes sobre medicamentos.

## 📋 Modalidade do Trabalho
* **Modalidade 1:** Reprodução experimental da abordagem apresentada no artigo original, utilizando a mesma base de dados, porém adaptando e expandindo o pipeline experimental para o ecossistema Python.

---

## 🧠 Fundamentação Teórica e Metodologia

O projeto replica e analisa a metodologia de processamento de texto aplicada sobre o dataset público **UCI `drugsCom` (KUC Hackathon Winter 2018)**. O pipeline de PLN foi estruturado nas seguintes etapas fundamentais:

1.  **Pré-processamento de Texto:**
    * Expansão de contrações da língua inglesa (biblioteca `contractions`).
    * Remoção de caracteres especiais, números e pontuações via Expressões Regulares (Regex).
    * Conversão de texto para minúsculas.
    * Tokenização e filtragem de *Stop Words* usando o `NLTK`.
    * Stemming utilizando o algoritmo `PorterStemmer` para normalização morfológica.

2.  **Análise de Sentimento Baseada em Léxico (BING):**
    * Utilização do léxico de opinião de *Bing Liu* para computar scores de termos positivos e negativos em medicamentos selecionados (*Levothyroxine, Viagra, Oseltamivir, Apixaban*) para validar as métricas de sensibilidade e inclinação do artigo original.

3.  **Modelagem de Tópicos (LDA):**
    * Aplicação do algoritmo *Latent Dirichlet Allocation* (LDA) através da biblioteca `Gensim` para descobrir os tópicos latentes discutidos nas avaliações médicas e avaliar sua perplexidade com diferentes parâmetros de $k$.

4.  **Aprendizado Supervisionado (Classificação de Sentimentos):**
    * Treinamento e validação de modelos preditivos para classificar a satisfação do paciente com base no texto das revisões, utilizando métricas robustas como Acurácia, AUC (Área sob a curva ROC) e Especificidade.

---

## 📊 Principais Resultados Obtidos

* **Validação do Léxico BING:** A replicação em Python capturou tendências semelhantes às do artigo original para medicamentos específicos (como taxas de positividade elevadas para o *Viagra* e moderadas para o *Levothyroxine*).
* **Modelagem de Tópicos:** O modelo LDA identificou agrupamentos semânticos claros associados a condições de saúde como *Controle de Natalidade (Birth Control)*, *Ansiedade/TDAH* e *Gastroenterologia/Metabolismo*. O teste com $k=4$ mostrou-se superior a $k=3$ (perplexidade de 752.90 vs 776.84).
* **Desempenho Supervisionado:** A implementação em Python superou os benchmarks originais do artigo em todas as métricas principais:
    * **Acurácia:** Ganho de +4 a +11 pontos percentuais.
    * **AUC:** Ganho de +8 a +17 pontos percentuais.
    * **Especificidade:** Evolução expressiva de +12 a +53 pontos percentuais, gerando modelos muito mais equilibrados entre Sensibilidade e Especificidade.

---

## 🛠️ Tecnologias e Dependências

O projeto foi desenvolvido inteiramente em **Python 3** utilizando o ambiente **Google Colab**. As seguintes bibliotecas são necessárias para a execução:

```bash
pip install contractions imbalanced-learn gensim kagglehub pandas numpy nltk matplotlib
