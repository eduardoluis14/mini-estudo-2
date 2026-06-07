# Mini Estudo 2: Simulação de Sistemas Estocásticos (Fila M/M/1) 🚀

Este repositório contém a implementação, análise e relatórios de um simulador de eventos discretos para uma **Fila M/M/1**, desenvolvido para a disciplina de **Avaliação de Desempenho** do Instituto de Computação (IComp) da UFAM.

O objetivo do estudo divide-se em avaliar o impacto de diferentes regras de parada na precisão estatística do sistema, mitigar o viés de inicialização provocado pelo estado transiente e aplicar técnicas de agrupamento para anular a forte correlação de dados em cenários de alta carga computacional.

---

## 📂 Organização do Repositório

O projeto está dividido em três notebooks principais, organizados de acordo com o escopo dos experimentos:

* **`MiniEstudo2_LuisNegreiros.ipynb`**: Contém a base do simulador e os **Exercícios 1, 2 e 3**, focados em regimes de horizonte finito e critérios de parada estatística (Chow e Robbins, Precisão Relativa).
* **`MiniEstudo2_exercicios4-6.ipynb`**: Contém os **Exercícios 4, 5 e 6**, focados estritamente na detecção, análise e eliminação do **Estado Transiente** utilizando heurísticas avançadas.
* **`MiniEstudo2_exercicios7-12.ipynb`**: Contém os **Exercícios 7 ao 12**, abordando a mitigação de autocorrelação em filas de alta contenção utilizando técnicas de médias de blocos e testes de normalidade para séries temporais padronizadas.

---

## 🛠️ Tecnologias e Otimizações

Para garantir a viabilidade computacional de simulações massivas (com picos de milhões de iterações), o projeto empregou soluções de engenharia de software e análise de dados:

* **Python 3 & Jupyter Notebook**: Ambiente principal de desenvolvimento.
* **Numba (Just-In-Time Compilation)**: Utilização do decorador `@jit(nopython=True)` para compilar funções críticas em código de máquina nativo, reduzindo drasticamente o tempo de processamento.
* **SciPy & NumPy**: Implementação eficiente de testes de hipótese complexos (Rank von Neumann, Shapiro-Wilk) e transformações em array.
* **Transformada Inversa**: Método matemático para geração precisa de Variáveis Aleatórias Exponenciais (tempo entre chegadas e tempo de serviço).
* **Algoritmo de Welford**: Implementação para cálculo incremental da média e da variância em tempo real, evitando estouro de memória RAM.

---

## 📊 Estrutura dos Experimentos

### Parte 1: Regras de Parada e Fronteiras de Coleta (`MiniEstudo2_LuisNegreiros.ipynb`)
* **Exercício 1 (Horizonte Finito)**: Análise de convergência variando o tamanho da amostra ($n = 10^3$ a $10^9$). Demonstração prática da Lei dos Grandes Números.
* **Exercício 2 (Regra de Chow e Robbins)**: Critério de parada baseado em limites absolutos de erro do Intervalo de Confiança ($d = 1.0, 0.5, 0.1, 0.05$).
* **Exercício 3 (Precisão Relativa)**: Critério de parada inteligente baseado no tamanho do Intervalo de Confiança ($\gamma = 5\%$).

### Parte 2: Análise do Estado Transiente (`MiniEstudo2_exercicios4-6.ipynb`)
* **Exercício 4 (O Problema do Transiente)**: Avaliação do impacto do viés de inicialização em replicações finitas, evidenciando a subestimação sistemática do tempo médio de espera.
* **Exercício 5 (Heurísticas Clássicas de Truncagem)**: Implementação e comparação das regras de descarte de **Conway** e **Fishman (k=7)** para isolar o período de aquecimento (*warm-up*).
* **Exercício 6 (MSER-5Y e Horizonte Infinito)**: Algoritmo *Marginal Standard Error Rule* (MSER-5Y) integrado a uma simulação de horizonte infinito para um corte ótimo e dinâmico.

### Parte 3: Tratamento de Correlação e Estimação Estacionária (`MiniEstudo2_exercicios7-12.ipynb`)
* **Exercício 7 (NBM - Nonoverlapping Batch Means)**: Agrupamento em blocos independentes, validados matematicamente pela Versão Ranking do Teste de von Neumann (RVN).
* **Exercício 8 (SBM - Spaced Batch Means)**: Introdução de descartes de fronteira ($S=1$ e $S=M/10$) para forçar o isolamento estatístico entre lotes consecutivos.
* **Exercício 9 (OBM - Overlapping Batch Means)**: Maximização da extração de médias através de janelas deslizantes com diferentes taxas de sobreposição (100%, 50%, 25%).
* **Exercício 10 (STS/AREA)**: Abordagem de Séries Temporais Padronizadas, aplicando transformações sobre os dados para atingir normalidade assintótica (validada por teste de Shapiro-Wilk).
* **Exercício 11 (STS/CSUM)**: Aprimoramento do método STS, integrando a métrica de soma cumulativa para penalizar desvios em relação à variância global da amostra.
* **Exercício 12 (Análise Comparativa)**: Avaliação unificada do custo computacional vs. precisão estatística dos cinco métodos operando sob regime de estresse de recursos ($\lambda = 9.5$, $\rho = 95\%$).

---

## 🏃 Como Executar

### Pré-requisitos
Certifique-se de ter o Python e o gerenciador de pacotes `pip` instalados. É necessária a instalação das bibliotecas de computação científica e otimização:

```bash
pip install numba numpy matplotlib scipy
