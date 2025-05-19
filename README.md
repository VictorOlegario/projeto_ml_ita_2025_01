# projeto_ml_ita_2025_01

Este repositório contém o modelo desenvolvido para o trabalho da disciplina de Machine Learning do curso de pós-graduação do ITA — turma 2025.1.

Intregrantes do Grupo 

- Felipe Gomes
- Lennon Falcao
- Luiz Vitor Tozi
- Victor Hugo Reis Olegario

## Introdução

O tema do projeto aborda a **Falha por Fadiga e Curvas S-N**, fenômeno importante na análise de componentes sujeitos a carregamentos cíclicos. A falha por fadiga ocorre quando microtrincas se formam e crescem ao longo do tempo, mesmo que as tensões aplicadas estejam abaixo do limite de resistência do material.

### Pontos-chave:
- **Falha por fadiga**: processo de degradação progressiva causado por cargas repetidas.
- **Curvas S-N**: relacionam tensão aplicada (S) ao número de ciclos até falha (N), sendo fundamentais na estimativa de vida útil.
- **Fatores influentes**: incluem tensões locais, geometrias com entalhes, condições ambientais e histórico de carga.
- **Aplicação prática**: utilizada em projetos de engenharia aeronáutica, civil e automotiva para garantir segurança estrutural.

---

## Descrição do Problema

Aplicar o conceito de fadiga à aviação é essencial, pois aeronaves passam por ciclos repetitivos de pressurização, turbulência e pousos, que afetam diretamente sua estrutura.

### Como a fadiga afeta aviões:
- **Ciclos de voo** (pressurização/despressurização) geram esforços cíclicos.
- **Componentes críticos**: asas, fuselagem (rebites e junções), trem de pouso, motores, superfícies de controle.

### Curvas S-N na prática:
- Ajudam engenheiros a estimar quantos ciclos uma peça pode resistir antes de falhar.
- Base para definir intervalos de manutenção e substituição preventiva.

### Caso histórico:
- **De Havilland Comet (1950s)**: primeiros jatos comerciais. Sofreram falhas catastróficas por trincas de fadiga iniciadas em cantos quadrados das janelas, agravadas pelos ciclos de voo.

### Técnicas de mitigação:
- Uso de **cantos arredondados** para reduzir concentração de tensões.
- **Materiais resistentes à fadiga** (ex: ligas de titânio).
- **Inspeções não destrutivas** periódicas (END).
- **Controle de ciclos de voo** de cada peça (Life Cycle Management).

## Base de Dados

A base simula resultados estruturais de uma fuselagem submetida a diferentes situações operacionais. Os atributos incluem:

1. `EID`: identificador do componente  
2. `type`: tipo do componente (painel ou reforçador)  
3. `material`: tipo da liga metálica (1, 2 ou 3)  
4. `stress_landing`: esforço durante o pouso  
5. `stress_taxi`: esforço durante taxiamento  
6. `stress_vertical`: esforço com vento vertical  
7. `stress_lateral`: esforço com vento lateral  
8. `stress_pressurization`: esforço com pressurização  
9. `life`: número de ciclos até a falha  
10. `log_life`: logaritmo de `life` na base 10  
11. Arquivo: `aircraft_fatigue.csv`

![Curva SN exemplo](image.png)  
![Visualização de stress](image-1.png)

## Software e Ferramentas

- Linguagem: **Python**
- Bibliotecas: `pandas`, `scikit-learn`, `matplotlib`
- Repositório GitHub: [acessar repositório](https://github.com/VictorOlegario/projeto_ml_ita_2025_01)

## Etapas do Projeto

  1.Introdução e limpeza de dados
  2.Análise exploratória
  3.Visualização de outliers
  4.Pré-processamento
  5.Testes com KNN e Árvore de Decisão
  6.Avaliação com MSE e R²
  7.Gráficos comparativos


   4.Pré-processamento:
- Remoção da coluna `EID`
- Conversão da variável `type` para valor numérico (LabelEncoder)
- One-hot encoding da variável `material`
- Reescalonamento das variáveis de stress para o intervalo **[-1, 1]**
- Geração de duas versões da base:
  - Sem truncamento de `life`
  - Com truncamento para valores de `life` acima de \(10^5\)

### 5.Modelos testados:

 KNN (K-Nearest Neighbors):
  O KNN é um modelo de regressão baseado na média dos valores dos "K" vizinhos mais próximos de um ponto. Ele não cria uma equação ou estrutura fixa, apenas observa os dados ao redor e faz previsões com base na proximidade.  
É sensível a outliers e escalas diferentes nas variáveis.

Árvore de Decisão
  A Árvore de Decisão constrói uma estrutura de regras com base nos dados de entrada. Ela divide o espaço de dados em regiões e toma decisões com base em valores-limite. Lida bem com dados ruidosos, relações não lineares e é menos sensível a valores extremos.

Random Forest
  É um conjunto de várias árvores de decisão. O modelo constrói várias árvores diferentes e tira a média dos resultados para fazer a previsão final. é mais robusto que uma única árvore, reduz o risco de overfitting, alta precisão. contudo eé menos interpretável, pode ser mais lento em bases grandes.

SVM (Support Vector Machine)
  No caso de regressão (SVR), o SVM busca encontrar uma linha ou superfície que fique o mais próxima possível dos dados, mas dentro de uma margem de tolerância. A ideia é prever valores sem se deixar levar por outliers. eé bom para dados com margens bem definidas e problemas complexos. eé sensível ao escalonamento dos dados, difícil de ajustar e interpretar em problemas reais com ruído.

### Avaliação:

Erro Quadrático Médio (MSE)
  Mede o quão distantes, em média, as previsões estão dos valores reais.  
  Quanto menor o valor, melhor o desempenho do modelo.

Coeficiente de Determinação (R²)
  Indica o quanto da variação dos dados o modelo consegue explicar.  
  Varia entre -∞ e 1, onde 1 significa ajuste perfeito.

Erro Absoluto Médio (MAE)
    Mede a média dos erros absolutos entre os valores previstos e os reais.
    Mostra, em média, o quanto o modelo erra, sem penalizar erros maiores.
    Quanto menor o valor, melhor o desempenho do modelo.

Raiz do Erro Quadrático Médio (RMSE)
    É a raiz quadrada da média dos erros ao quadrado.
    Dá mais peso aos grandes erros, sendo útil para destacar desvios maiores.
    Quanto menor o valor, melhor a precisão do modelo.

## Metrica de avaliacao

Métrica         |	Melhor valor
MAE             | Menor
RMSE            | Menor
MSE             | Menor
R²	            | Maior

## Resultados dos Modelos




![alt text](image-2.png)



![alt text](image-3.png)


## Conclusões

A análise comparativa entre os modelos mostrou que a Árvore de Decisão foi a que apresentou o melhor desempenho para este estudo. Mesmo sem aplicar truncamento na variável life, o modelo conseguiu lidar bem com os dados, alcançando um R² próximo de 0,90. Após aplicar o truncamento (limitando life em 10⁵), o desempenho foi praticamente perfeito, com R² ≈ 0,999999.

O KNN teve desempenho significativamente inferior na versão sem truncamento, com MSE elevado e R² abaixo de 0,30. Com o truncamento, o modelo melhorou bastante, mas ainda ficou abaixo da Árvore de Decisão em termos de estabilidade e precisão.

Considerando todas as métricas (MSE, MAE, RMSE e R²), a Árvore de Decisão com truncamento se mostrou o modelo mais indicado para este caso. Foi mais consistente, menos sensível a valores extremos e se adaptou muito bem ao comportamento da base de fadiga estrutural.


**Autor:** Victor Olegario  
**Curso:** Pós-graduação em Engenharia de Computação – ITA (2025.1)  


