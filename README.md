# Mini Estudo 2: Simulação de Sistemas Estocásticos (Fila M/M/1) 🚀

Este repositório contém a implementação, análise e relatórios de um simulador de eventos discretos para uma **Fila M/M/1**, desenvolvido para a disciplina de **Avaliação de Desempenho** do Instituto de Computação (IComp) da UFAM.

O objetivo do estudo divide-se em avaliar o impacto de diferentes regras de parada na precisão estatística do sistema e mitigar o viés de inicialização provocado pelo estado transiente do modelo simulado.

---

## 📂 Organização do Repositório

O projeto está dividido em dois notebooks principais, organizados de acordo com o escopo dos experimentos:

* **`MiniEstudo2_LuisNegreiros.ipynb`**: Contém a base do simulador e os **Exercícios 1, 2 e 3**, focados em regimes de horizonte finito e critérios de parada estatística (Chow e Robbins, Precisão Relativa).
* **`MiniEstudo2_exercicios4-6.ipynb`**: Contém os **Exercícios 4, 5 e 6**, focados estritamente na detecção, análise e eliminação do **Estado Transiente** utilizando heurísticas avançadas.

---

## 🛠️ Tecnologias e Otimizações

Para garantir a viabilidade computacional de simulações massivas (na casa de **1 bilhão de iterações**), o projeto empregou soluções avançadas de engenharia de software:

* **Python 3 & Jupyter Notebook**: Ambiente principal de desenvolvimento.
* **Numba (Just-In-Time Compilation)**: Utilização do decorador `@jit(nopython=True)` para compilar funções críticas em código de máquina nativo, reduzindo o tempo de processamento de horas para segundos.
* **Transformada Inversa**: Método matemático para geração precisa de Variáveis Aleatórias Exponenciais (tempo entre chegadas e tempo de serviço).
* **Algoritmo de Welford**: Implementação para cálculo incremental da média e da variância em tempo real, evitando estouro de memória RAM.

---

## 📊 Estrutura dos Experimentos

### Parte 1: Regras de Parada e Fronteiras de Coleta (`MiniEstudo2_LuisNegreiros.ipynb`)
* **Exercício 1 (Horizonte Finito)**: Análise de convergência variando o tamanho da amostra ($n = 10^3$ a $10^9$). Demonstração prática da Lei dos Grandes Números aproximando-se do valor analítico.
* **Exercício 2 (Regra de Chow e Robbins)**: Critério de parada baseado em limites absolutos de erro do Intervalo de Confiança ($d = 1.0, 0.5, 0.1, 0.05$).
* **Exercício 3 (Precisão Relativa)**: Critério de parada inteligente baseado no tamanho do Intervalo de Confiança ($\gamma = 5\%$), otimizando o número de amostras necessárias para alcançar a estabilidade estatística.

### Parte 2: Análise do Estado Transiente (`MiniEstudo2_exercicios4-6.ipynb`)
* **Exercício 4 (O Problema do Transiente)**: Avaliação do impacto do viés de inicialização (sistema começando vazio) em replicações finitas, evidenciando a subestimação sistemática do tempo médio de espera.
* **Exercício 5 (Heurísticas Clássicas de Truncagem)**: Implementação e comparação das regras de descarte de **Conway** e **Fishman (k=7)** para isolar o período de aquecimento (*warm-up*).
* **Exercício 6 (MSER-5Y e Horizonte Infinito)**: Implementação do algoritmo *Mitigation of Start-up Transients in Simulation Output* (MSER-5Y) integrado a uma simulação de horizonte infinito com técnica de médias de lotes (*Batch Means*).

---

## 🏃 Como Executar

### Pré-requisitos
Certifique-se de ter o Python e o gerenciador de pacotes `pip` instalados. É necessária a instalação das bibliotecas de computação científica e otimização:

```bash
pip install numba numpy matplotlib scipy
```