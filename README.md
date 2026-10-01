# Energia renovável e Machine Learning com dados abertos

## Objetivo
Aplicar classificação e regressão a dados de energia renovável: classificar a fonte de geração de empreendimentos da ANEEL (Solar, Eólica ou Hidráulica) e estimar a radiação solar horária em Petrolina (PE).

## Fontes e período dos dados
- Classificação: cadastro de empreendimentos de geração da ANEEL (https://dadosabertos.aneel.gov.br/api/3/action/datastore_search), 3876 registros, com potência (kW), latitude e longitude. Arquivo: aneel_classificacao_orange.csv
- Regressão: API Open-Meteo, Petrolina (PE), de 01/04/2025 a 30/06/2025, das 7h às 17h, 1001 registros horários com temperatura, umidade, nuvens, vento, hora e radiação (W/m²). Arquivo: meteo_regressao_orange.csv

## Como executar o notebook
1. Abra Aula_APIs_Energia_Renovavel_ML.ipynb no Google Colab (ou Jupyter).
2. Envie os dois arquivos CSV para a pasta /content (ou ajuste o caminho nas células de leitura).
3. Execute todas as células em ordem (Ambiente de execução > Executar tudo).

## Resumo dos resultados
### Classificação (média macro, 20% de teste, divisão estratificada)
| Modelo | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| KNN | 0,965 | 0,966 | 0,964 | 0,965 |
| Regressão Logística | 0,825 | 0,828 | 0,821 | 0,820 |
| Random Forest | 0,976 | 0,977 | 0,974 | 0,975 |

O Random Forest foi o melhor modelo. Os erros se concentram na classe Solar.

### Regressão (80% iniciais para treino, 20% finais para teste, sem embaralhar)
| Modelo | MAE (W/m²) | MSE ((W/m²)²) | R² |
|---|---|---|---|
| Regressão Linear | 145,2 | 30034,2 | 0,360 |
| KNN | 68,3 | 7608,0 | 0,838 |
| Random Forest | 66,7 | 7278,1 | 0,845 |

O Random Forest foi o melhor modelo. A hora do dia é a variável mais importante.

## Autor
Felipe Mello - RM 569237
