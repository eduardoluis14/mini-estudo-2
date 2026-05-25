# Mini Estudo 2: Simulação de Sistemas Estocásticos (Fila M/M/1) 🚀

Este repositório contém a implementação e análise de um simulador de eventos discretos para uma **Fila $M/M/1$**, desenvolvido para a disciplina de **Avaliação de Desempenho** do Instituto de Computação (IComp) da UFAM.

O objetivo principal do estudo foi avaliar o impacto de diferentes regras de parada (horizonte finito, absoluto e relativo) na precisão estatística do tempo médio de espera na fila, confrontando os resultados experimentais com os modelos analíticos da Teoria de Filas.

---

## 🛠️ Tecnologias e Otimizações

Para garantir a viabilidade computacional de simulações massivas (na casa de **1 bilhão de iterações**), o projeto empregou soluções avançadas de engenharia de software:

* **Python 3 & Jupyter Notebook**: Ambiente principal de desenvolvimento.
* **Numba (Just-In-Time Compilation)**: Utilização do decorador `@jit(nopython=True)` para compilar funções críticas em código de máquina nativo, reduzindo o tempo de processamento de 10⁹ iterações de horas para apenas ~28 segundos.
* **Transformada Inversa**: Método matemático para geração precisa de Variáveis Aleatórias Exponenciais (tempo entre chegadas e tempo de serviço).
* **Algoritmo de Welford**: Implementação para cálculo incremental da média e da variância em tempo real, evitando estouro de memória RAM ao dispensar o armazenamento de vetores gigantescos.

---

## 📊 Estrutura dos Experimentos

O notebook está organizado em três exercícios fundamentais:

1. **Exercício 1 (Horizonte Finito)**: Análise de convergência variando o tamanho da amostra ($n = 10^3, 10^5, 10^7, 10^9$). Demonstração prática da Lei dos Grandes Números aproximando-se do valor analítico de $0.9\text{s}$.
2. **Exercício 2 (Regra de Chow e Robbins)**: Critério de parada baseado em limites absolutos de erro do Intervalo de Confiança ($d = 1.0, 0.5, 0.1, 0.05$).
3. **Exercício 3 (Precisão Relativa)**: Critério de parada inteligente baseado no tamanho relativo do Intervalo de Confiança ($\gamma = 5\%$), otimizando o número de amostras necessárias para alcançar a estabilidade estatística.

---

## 🏃 Como Executar

### Pré-requisitos
Certifique-se de ter o Python e o gerenciador de pacotes `pip` instalados. É necessária a instalação do `numba` para a otimização JIT.

```bash
pip install numba
