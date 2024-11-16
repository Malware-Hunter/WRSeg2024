# Viés Avaliativo e Generalização Comprometida: O Impacto de Amostras Idênticas em Datasets de Malware Android

Neste trabalho, analisamos *datasets* públicos utilizados na detecção de *malwares* Android, investigando como amostras idênticas e os grupos que elas formam impactam o desempenho e a capacidade de generalização dos modelos de aprendizado de máquina. Nossos testes em seis cenários mostram que amostras idênticas elevam artificialmente as métricas de desempenho, criando uma impressão equivocada de eficácia. Além disso, em conjuntos com poucas amostras únicas, observamos que os modelos enfrentam dificuldades para generalizar em novos dados. Concluímos que é fundamental garantir amostras exclusivas no conjunto de testes para avaliações precisas e evitar conclusões enganosas sobre a capacidade dos classificadores.

Neste repositório, apresentamos os resultados completos do artigo.

### Tabela: Resumo de informações dos *datasets*

Neste estudo, foram utilizados sete (7) *datasets*, cujas dimensões e características estão detalhadas na tabela a seguir:

|**Dataset**            | **Características** | **A. únicas** | **A. idênticas** | **Total** |
|------------------------|----------------------|----------------|------------------|-----------|
|                       | **Qtde.** | **Tipos** | **Mal.** | **Ben.** | **Mal.** | **Ben.** |           |
| Adroit                | 166       | P        | 133      | 992      | 3285     | 7066     | 11476     |
| AndroCrawl            | 141       | A(26), I(8), P(84), O(23) | 7436 | 44860 | 2734 | 41714 | 96744 |
| Android Permissions   | 151       | P        | 1443     | 976      | 16344    | 8101     | 26864     |
| DefenseDroid PRS     | 2877      | P(1489), I(1388) | 4620 | 2595 | 1380 | 3380 | 11975 |
| Drebin-215           | 215       | A(73), P(113), S(6), I(23) | 1116 | 3870 | 4439 | 5606 | 15031 |
| KronoDroid Emulator   | 276       | P(145), A(123), O(8) | 8401 | 14136 | 20344 | 21110 | 63991 |
| KronoDroid Real       | 286       | P(146), A(100), O(40) | 14555 | 16908 | 26827 | 19847 | 78137 |

**Legenda:**  
- [P] Permissões  
- [A] Chamadas de API  
- [I] Intenções  
- [S] Comandos do Sistema  
- [O] Outros

### Testes realizados

Foram realizados cinco testes:

**Teste 1:** Todas as amostras idênticas foram excluídas do conjunto de dados.  
*Objetivo:* Avaliar o impacto da remoção completa de amostras duplicadas na capacidade de generalização dos modelos.

**Teste 2:** Remoção do maior grupo de amostras idênticas, ou seja, instâncias com as mesmas características, independentemente de pertencerem à mesma classe ou não.  
*Objetivo:* Analisar como a remoção de um grupo significativo de amostras idênticas afeta a performance dos modelos, utilizando o restante dos dados para treinamento.

**Teste 3:** Conjunto de teste composto exclusivamente por amostras únicas.  
*Objetivo:* Avaliar a eficácia dos modelos treinados com dados contendo amostras idênticas ao serem testados exclusivamente com amostras distintas.

**Teste 4:** Utilização de conjuntos de dados sem amostras idênticas, onde, para cada grupo, foi mantida apenas uma instância. Esse teste foi realizado em dois cenários:
- **Teste 4.1:** A classe foi definida como benigna.
- **Teste 4.2:** A classe foi definida como *malware*.  
*Objetivo:* Avaliar o comportamento dos classificadores em cenários sem dados sobrepostos, com uma única amostra representando cada grupo idêntico.

**Teste 5:** Conjunto de dados completo, com todas as amostras idênticas presentes.  
*Objetivo:* Servir como referência comparativa para os outros testes, mostrando o impacto das amostras duplicadas no desempenho dos modelos.

### Resultados para o dataset Adroit
| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 1.0000   | 0.0167  | 0.1174  |
|          | RF     | 0.1143   | 0.0667  | -0.0548 |
|          | KNN    | 0.2647   | 0.1500  | 0.0776  |
| Teste 2  | SVM    | 0.3030   | 0.1504  | 0.1429  |
|          | RF     | 0.3077   | 0.1203  | 0.1292  |
|          | KNN    | 0.1707   | 0.1579  | 0.0570  |
| Teste 3  | SVM    | 0.4248   | 0.1611  | 0.1753  |
|          | RF     | 0.5000   | 0.1946  | 0.2313  |
|          | KNN    | 0.3393   | 0.1913  | 0.1431  |
| Teste 4.1| SVM    | 0.0000   | 0.0000  | 0.0000  |
|          | RF     | 0.1667   | 0.0323  | 0.0322  |
|          | KNN    | 0.0000   | 0.0000  | -0.0457 |
| Teste 4.2| SVM    | 0.5000   | 0.3043  | 0.1519  |
|          | RF     | 0.4111   | 0.3217  | 0.0633  |
|          | KNN    | 0.3395   | 0.4783  | -0.0495 |
| Teste 5  | SVM    | 0.9512   | 0.7131  | 0.7629  |
|          | RF     | 0.9346   | 0.7834  | 0.8003  |
|          | KNN    | 0.8700   | 0.8003  | 0.7649  |

### Resultados para o dataset Androcrawl

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.9546   | 0.8887  | 0.9090  |
|          | RF     | 0.9415   | 0.9006  | 0.9085  |
|          | KNN    | 0.9488   | 0.8488  | 0.8822  |
| Teste 2  | SVM    | 0.9110   | 0.9110  | 0.9005  |
|          | RF     | 0.9250   | 0.9159  | 0.9111  |
|          | KNN    | 0.9059   | 0.8751  | 0.8777  |
| Teste 3  | SVM    | 0.9381   | 0.8984  | 0.9051  |
|          | RF     | 0.9418   | 0.8995  | 0.9079  |
|          | KNN    | 0.9383   | 0.8676  | 0.8872  |
| Teste 4.1| SVM    | 0.9546   | 0.8692  | 0.8992  |
|          | RF     | 0.9537   | 0.8386  | 0.8807  |
|          | KNN    | 0.9582   | 0.7185  | 0.8105  |
| Teste 4.2| SVM    | 0.9802   | 0.8761  | 0.9034  |
|          | RF     | 0.7782   | 0.8736  | 0.7583  |
|          | KNN    | 0.5461   | 0.8746  | 0.5505  |
| Teste 5  | SVM    | 0.9392   | 0.9207  | 0.9220  |
|          | RF     | 0.9480   | 0.9212  | 0.9272  |
|          | KNN    | 0.9428   | 0.8828  | 0.9028  |

### Resultados para o dataset Android Permissions

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.5797   | 0.8896  | 0.0155  |
|          | RF     | 0.4730   | 0.4968  | -0.2609 |
|          | KNN    | 0.5315   | 0.5189  | -0.1043 |
| Teste 2  | SVM    | 0.6105   | 0.9134  | 0.0819  |
|          | RF     | 0.6224   | 0.8385  | 0.1068  |
|          | KNN    | 0.6074   | 0.7152  | 0.0341  |
| Teste 3  | SVM    | 0.5950   | 0.9038  | 0.0995  |
|          | RF     | 0.6132   | 0.8318  | 0.1406  |
|          | KNN    | 0.6041   | 0.7830  | 0.0961  |
| Teste 4.1| SVM    | 0.5366   | 0.1728  | 0.1066  |
|          | RF     | 0.4397   | 0.2670  | 0.0449  |
|          | KNN    | 0.4127   | 0.2042  | 0.0120  |
| Teste 4.2| SVM    | 0.7026   | 0.9910  | 0.0820  |
|          | RF     | 0.7135   | 0.9248  | 0.1050  |
|          | KNN    | 0.7094   | 0.8992  | 0.0698  |
| Teste 5  | SVM    | 0.6799   | 0.9621  | 0.1432  |
|          | RF     | 0.6904   | 0.9011  | 0.1497  |
|          | KNN    | 0.7051   | 0.8002  | 0.1573  |

### Resultados para o dataset DefenseDroid PRS

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.9250   | 0.9063  | 0.8059  |
|          | RF     | 0.9208   | 0.9013  | 0.7954  |
|          | KNN    | 0.9059   | 0.9013  | 0.7758  |
| Teste 2  | SVM    | 0.9457   | 0.8918  | 0.8393  |
|          | RF     | 0.9306   | 0.8993  | 0.8297  |
|          | KNN    | 0.9088   | 0.8775  | 0.7862  |
| Teste 3  | SVM    | 0.9620   | 0.9033  | 0.8484  |
|          | RF     | 0.9598   | 0.9025  | 0.8448  |
|          | KNN    | 0.9402   | 0.8924  | 0.8102  |
| Teste 4.1| SVM    | 0.9365   | 0.9062  | 0.8337  |
|          | RF     | 0.9327   | 0.8664  | 0.7921  |
|          | KNN    | 0.9276   | 0.8416  | 0.7639  |
| Teste 4.2| SVM    | 0.8745   | 0.9578  | 0.6928  |
|          | RF     | 0.8606   | 0.9553  | 0.6570  |
|          | KNN    | 0.8241   | 0.9619  | 0.5762  |
| Teste 5  | SVM    | 0.9404   | 0.8898  | 0.8358  |
|          | RF     | 0.9294   | 0.9075  | 0.8399  |
|          | KNN    | 0.8945   | 0.9058  | 0.8005  |

### Resultados para o dataset Drebin-215

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.9754   | 0.9215  | 0.9327  |
|          | RF     | 0.9749   | 0.9041  | 0.9210  |
|          | KNN    | 0.9599   | 0.9041  | 0.9113  |
| Teste 2  | SVM    | 0.9689   | 0.9467  | 0.9102  |
|          | RF     | 0.9576   | 0.8880  | 0.9008  |
|          | KNN    | 0.8962   | 0.9017  | 0.8694  |
| Teste 3  | SVM    | 0.9534   | 0.9367  | 0.9272  |
|          | RF     | 0.9703   | 0.9259  | 0.9314  |
|          | KNN    | 0.9197   | 0.9259  | 0.8974  |
| Teste 4.1| SVM    | 0.9784   | 0.6099  | 0.7443  |
|          | RF     | 0.9836   | 0.5381  | 0.6972  |
|          | KNN    | 0.9044   | 0.5516  | 0.6694  |
| Teste 4.2| SVM    | 0.8623   | 0.9439  | 0.8105  |
|          | RF     | 0.7824   | 0.9453  | 0.7196  |
|          | KNN    | 0.7313   | 0.9365  | 0.6464  |
| Teste 5  | SVM    | 0.9905   | 0.9694  | 0.9689  |
|          | RF     | 0.9944   | 0.9851  | 0.9841  |
|          | KNN    | 0.9758   | 0.9740  | 0.9609  |

### Resultados para o dataset Kronodroid Emulator

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.9206   | 0.8813  | 0.8406  |
|          | RF     | 0.9296   | 0.9093  | 0.8695  |
|          | KNN    | 0.9060   | 0.8782  | 0.8257  |
| Teste 2  | SVM    | 0.8925   | 0.9012  | 0.8106  |
|          | RF     | 0.9277   | 0.9106  | 0.8532  |
|          | KNN    | 0.8654   | 0.8735  | 0.7603  |
| Teste 3  | SVM    | 0.8982   | 0.8929  | 0.8308  |
|          | RF     | 0.9336   | 0.9183  | 0.8804  |
|          | KNN    | 0.8757   | 0.8837  | 0.8043  |
| Teste 4.1| SVM    | 0.9277   | 0.7288  | 0.7629  |
|          | RF     | 0.9225   | 0.6625  | 0.7144  |
|          | KNN    | 0.8779   | 0.5749  | 0.6267  |
| Teste 4.2| SVM    | 0.9233   | 0.9089  | 0.8301  |
|          | RF     | 0.8252   | 0.9316  | 0.7344  |
|          | KNN    | 0.7388   | 0.9137  | 0.5980  |
| Teste 5  | SVM    | 0.9572   | 0.9410  | 0.9069  |
|          | RF     | 0.9771   | 0.9635  | 0.9457  |
|          | KNN    | 0.9571   | 0.9499  | 0.9146  |


### Resultados para o dataset KronoDroid Real

| Teste    | Modelo | Precisão | Recall  | MCC     |
|----------|--------|----------|---------|---------|
| Teste 1  | SVM    | 0.9533   | 0.9250  | 0.8869  |
|          | RF     | 0.9561   | 0.9405  | 0.9034  |
|          | KNN    | 0.9474   | 0.9155  | 0.8729  |
| Teste 2  | SVM    | 0.9342   | 0.9397  | 0.8676  |
|          | RF     | 0.9437   | 0.9468  | 0.8852  |
|          | KNN    | 0.9238   | 0.9208  | 0.8376  |
| Teste 3  | SVM    | 0.9489   | 0.9307  | 0.8872  |
|          | RF     | 0.9598   | 0.9412  | 0.9072  |
|          | KNN    | 0.9424   | 0.9192  | 0.8705  |
| Teste 4.1| SVM    | 0.9483   | 0.8544  | 0.8464  |
|          | RF     | 0.9507   | 0.7735  | 0.7886  |
|          | KNN    | 0.9263   | 0.6895  | 0.7095  |
| Teste 4.2| SVM    | 0.9448   | 0.9361  | 0.8632  |
|          | RF     | 0.8674   | 0.9514  | 0.7774  |
|          | KNN    | 0.7894   | 0.9385  | 0.6454  |
| Teste 5  | SVM    | 0.9767   | 0.9606  | 0.9331  |
|          | RF     | 0.9842   | 0.9727  | 0.9538  |
|          | KNN    | 0.9766   | 0.9610  | 0.9333  |
