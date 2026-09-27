# Previsão de Preços de Imóveis — Airbnb São Paulo

Projeto final da disciplina **Aprendizado de Máquina Supervisionado**, MBA em Ciência de Dados — UNIFOR.
Professor: Caio Ponte | Turma: 11

## Objetivo

Prever o **preço da diária** (`price`) de anúncios do Airbnb em São Paulo a partir de suas características
físicas, de localização, do anfitrião e de avaliações — um problema de **regressão** aplicado a dados reais
de mercado.

## Fonte dos dados

[InsideAirbnb](https://insideairbnb.com/) — scrape público de São Paulo (20/06/2026).
Dataset original: 42.354 anúncios, 90 colunas.

## Como executar

1. Baixe o arquivo `listings.csv` (descompactado) do InsideAirbnb para a mesma pasta deste notebook.
2. Abra `notebook_airbnb_sp_completo.ipynb` no Jupyter ou VS Code.
3. Execute todas as células em ordem (Kernel → Restart & Run All).
4. **Atenção:** a célula de ajuste de hiperparâmetros do Random Forest (Etapa 4.6) pode levar alguns
   minutos, dependendo do processador.

**Bibliotecas necessárias:** pandas, numpy, matplotlib, scikit-learn.

## Estrutura do projeto

| Etapa | Conteúdo |
|---|---|
| 1. Definição do Problema | Contexto, dicionário de dados, carregamento |
| 2. Análise Exploratória (EDA) | Distribuição, estatísticas, outliers, correlação, mapa geográfico, PCA/t-SNE |
| 3. Pré-processamento | Tratamento de nulos, outliers, encoding categórico, NLP (amenities + TF-IDF), split e normalização |
| 4. Treinamento | Ridge, Random Forest e KNN — baseline e ajuste de hiperparâmetros |
| 5. Avaliação e Conclusão | Benchmark final, análise de resíduos, discussão e conclusão |

## Resultados finais (dados de teste)

| Modelo | R² | MAE | RMSE |
|---|---|---|---|
| Ridge Regression | 0,401 | R$ 121,62 | R$ 204,32 |
| KNN | 0,475 | R$ 106,16 | R$ 191,52 |
| **Random Forest** | **0,552** | **R$ 95,86** | **R$ 176,71** |

**Modelo final escolhido:** Random Forest, por liderar em todas as métricas de avaliação.

## Principais decisões técnicas

- **Capping de outliers** em `bedrooms`, `bathrooms`, `beds`, `minimum_nights` e no `price` (percentil 99)
- **Flag `sem_reviews`** para anúncios sem avaliação, em vez de imputação simples nas notas
- **Agrupamento de categorias raras** em `property_type` e bairro antes do One-Hot Encoding
- **NLP:** binarização das 20 comodidades mais comuns + TF-IDF (30 termos) na descrição
- **Normalização** ajustada apenas no conjunto de treino, evitando vazamento de dados (data leakage)

## Arquivos do repositório

- `notebook_airbnb_sp_completo.ipynb` — notebook completo com todo o pipeline
- `apresentacao_airbnb.pptx` — slides utilizados na apresentação em vídeo

## Autor

Luan — MBA em Ciência de Dados, UNIFOR
