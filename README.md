# ec-ingredion-2

> Este projeto faz parte do curso de **Inteligência Artificial** oferecido pela [FIAP](https://github.com/fiap) - Online 2024. Este repositório reúne os materiais relacionados ao **Enterprise Challenge - Ingredion**, correspondendo à **Sprint 2** do desafio.

- Video de Apresentação: [Youtube]()
- Notebook para Correção: [Jupyter Notebook](./src/ml.ipynb)

## Descrição

Este projeto desenvolve um modelo de Inteligência Artificial para prever a produtividade agrícola, focando na cultura do café na região de Manhuaçu (MG).  Substituímos abordagens tradicionais, que dependem de estimativas manuais e dados fragmentados, por uma solução que integra imagens de satélite (índice de vegetação NDVI) e dados históricos de produção. O modelo aprende a identificar padrões sazonais e as relações entre a saúde da vegetação e a produtividade, gerando previsões mais precisas para dar suporte à tomada de decisões.

A solução proposta visa:

*   **Otimizar o planejamento agrícola:** Fornecendo previsões de produtividade mais acuradas, auxiliando na alocação eficiente de recursos (fertilizantes, mão de obra, etc.).
*   **Reduzir perdas:** Identificando tendências e possíveis impactos de fatores ambientais (seca, pragas, etc.) na produção.
*   **Adaptabilidade e escalabilidade:** A solução é projetada para ser adaptada a diferentes culturas e escalável para outras regiões, aumentando seu valor estratégico.

## Estrutura de Arquivos

```py
├── data                  # Arquivos de entrada e saída usados no processo
│   ├── PROCESSED           # Dados pré-processados para os modelos
│   │   ├── manhuacu.csv  # Produção histórica (1974-2023) + NDVI anual médio
│   │   └── ndvi.csv      # Série temporal NDVI (2000-2023) com colunas cíclicas
│   ├── GOOGLE_EARTH_ENGINE # Dados NDVI extraídos do Google Earth Engine
│   │   └── ndvi_manhuacu.csv # Série NDVI (2000–2025): Google Earth Engine
│   └── SIDRA               # Dados de produção do IBGE
│       └── tabela1613.xlsx # Dados de produção (1974–2023): IBGE/Tabela 1613
├── models                # Arquivos de pesos dos modelos treinados
│   ├── lstm.pth        # Pesos do modelo LSTM
│   └── mlp.pth         # Pesos do modelo MLP
├── README.md             # Este README
├── requirements.txt      # Lista de dependências do projeto
├── scripts               # Notebooks para extração e preparação dos dados
│   └── extract-ndvi-manhuacu.ipynb # Extração NDVI de Manhuaçu, MG (Google Earth Engine)
│   └── prepare-data.ipynb           # Preparação e integração dos dados
├── src                   # Código fonte dos modelos e análise exploratória
│   └── eda.ipynb       # Análise Exploratória (EDA) e estatísticas
│   └── ml.ipynb        # Implementação e treinamento dos modelos de IA
└── TODO.md               # Gestão do projeto e tarefas pendentes
```

## Documentação

### Preparação do Ambiente

#### Instalar o Python  

1. Baixe e instale a versão mais recente do Python (recomendado 3.7 ou superior) no [site oficial do Python](https://www.python.org/).  
2. Durante a instalação, certifique-se de marcar a opção **"Add Python to PATH"**.  
3. Verifique as versões do Python e do `pip`  
   Certifique-se de que o Python e o `pip` foram instalados corretamente executando:  
    ```bash
    python --version
    pip --version
    ```

#### Criar um Ambiente Virtual (Opcional, mas Recomendado)  

Usar um ambiente virtual isola as dependências do projeto.

1. Abra um terminal ou prompt de comando.  
2. Navegue até a pasta do projeto.  
3. Execute o seguinte comando para criar um ambiente virtual:  
   ```bash
   python -m venv venv
   ```  
4. Ative o ambiente virtual:  
   - No Windows:  
     ```bash
     venv\Scripts\activate
     ```  
   - No macOS/Linux:  
     ```bash
     source venv/bin/activate
     ```

#### Instalar as Bibliotecas Necessárias

1. Instale o `pip` e o `setuptools` (se ainda não estiverem instalados)  
   Atualize o `pip` e o `setuptools` para a versão mais recente:  
    ```bash
    pip install --upgrade pip setuptools
    ```  
2. Instale as Bibliotecas  
   Use o `pip` para instalar as bibliotecas necessárias. Execute o comando:  
    ```bash
    pip install -r requirements.txt
    ```
   Mais detalhes sobre instalação do PyTorch: https://pytorch.org/get-started/locally/

### Prints da Análise Exploratória e Estatísticas Resultantes

Para equivalentes às prints da Análise Exploratória e Estatísticas Resultantes:

[EDA](./src/eda.ipynb)

### Processo de Preparação dos Dados

- Link para código e documentação: [Jupyter Notebook](./scripts/prepare-data.ipynb)

A coleta e preparação dos dados envolvem duas etapas principais: extração de dados brutos de produtividade agrícola (SIDRA/IBGE) e de vegetação (NDVI via Google Earth Engine), seguidas por um processo de transformação e consolidação em um formato estruturado para modelagem.

---

#### Coleta de Dados

**1. Dados de Produção Agrícola (SIDRA/IBGE):**

- Acesse o site do SIDRA: [Produção Agrícola Municipal - Culturas Permanentes](https://sidra.ibge.gov.br/tabela/1613)
- Selecione as seguintes opções:
  - **Variável:** Área plantada, Área colhida, Quantidade produzida, Rendimento médio da produção e Valor da produção.
  - **Produto:** Café (em grão) Total.
  - **Ano:** Todos os disponíveis (marcar a caixa "Selecionar todos").
  - **Unidade Territorial:**
     - **Unidade da Federação:** 31. Minas Gerais
     - **Mesoregião Geográfica:** 3112. Zona da Mata (MG)
     - **Município:** 3139409. Manhuaçu (MG)
- Faça o download em formato `.xlsx`.

**2. Dados de NDVI (Google Earth Engine):**

- A coleta dos dados de NDVI foi realizada programaticamente utilizando o Google Earth Engine (GEE) e a coleção MODIS/061/MOD13Q1.
- A região de interesse foi definida como um buffer de 1 km centrado em **Manhuaçu, Minas Gerais**, obtido via geocodificação (`geopy`).
- O período coletado abrange de **01/01/2000 a 31/12/2025**.
- As imagens foram filtradas espacial e temporalmente, com média regional de NDVI computada para cada data.
- Os valores foram normalizados para escala 0–1.
- Exportação final: `../data/GOOGLE_EARTH_ENGINE/ndvi_manhuacu.csv`.

> **Nota:** É necessário autenticar com o GEE e configurar o `.env` com `GOOGLE_EARTH_ENGINE_PROJECT_ID`.

---

#### Preparação dos Dados

**1. Processamento dos dados do SIDRA:**

- A partir do `.xlsx` baixado, duas planilhas foram utilizadas:
  - **"Quantidade produzida"**: filtrada apenas para **Manhuaçu (MG)**, transposta e renomeada por ano.
  - **"Área colhida"**: processo idêntico ao anterior, resultando em área em hectares por ano.
- As duas tabelas foram unificadas por ano, e foi calculada a **produtividade anual (kg/ha)**.
- Resultado final salvo em: `../data/PROCESSED/manhuacu.csv`.

**2. Processamento dos dados de NDVI:**

- O CSV coletado do GEE foi carregado com `pandas`.
- As colunas foram renomeadas (`date` → `Data`, `ndvi` → `NDVI`).
- Foi extraído o campo **ano** a partir da data para posterior agregação e análise.
- Resultado final salvo em: `../data/PROCESSED/ndvi.csv`.

Esses conjuntos de dados prontos servem como base de entrada para os modelos de previsão de produtividade agrícola utilizados neste projeto.

#### Análise Exploratória (EDA)

A análise exploratória foi crucial para entender os dados e direcionar o desenvolvimento dos modelos.

*   **Série Temporal NDVI:** Visualização da série temporal NDVI (2000-2025) para identificar padrões sazonais e anomalias.
    *   [Gráfico da série NDVI](./src/eda.ipynb)
*   **Correlação entre NDVI, Área e Produção:**  Análise da correlação entre as variáveis para identificar relações preditivas.
    *   [Gráfico de Correlação](./src/eda.ipynb)
*   **Distribuição das Variáveis:** Boxplots para identificar outliers e entender a distribuição dos dados.
    *   [Boxplots das Variáveis](./src/eda.ipynb)
*   **Dados Faltantes:**  Verificação da existência de dados faltantes e tratamento adequado.
    *   Não há dados faltantes nas variáveis utilizadas.
*   **Relação entre NDVI, Área e Produção:** Gráficos de dispersão 3D e contorno para visualizar a relação entre as três variáveis.
    *   [Gráfico 3D da relação](./src/eda.ipynb)

### Funcionamento do Código

*   Link para código e documentação: [Jupyter Notebook](./src/ml.ipynb)

Nosso projeto utiliza PyTorch para construir e treinar modelos de Machine Learning. O pipeline implementa pré-processamento avançado, modelagem com MLP e LSTM, e otimização para GPU via CUDA.

#### Abordagens Implementadas

Duas arquiteturas de redes neurais profundas foram implementadas e comparadas para a previsão de produtividade agrícola:

| Modelo                         | Descrição                                                                                     | Arquitetura                                                                                                                     | Justificativa                                                                                                               |
| :----------------------------- | :-------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------- |
| MLP (Multilayer Perceptron)    | Rede neural *feed-forward* para capturar padrões não lineares e relações diretas.            | 32 → 16 neurônios, ativação ReLU + Tanh amplificada, janela temporal de 5 observações.                                   | Simplicidade e eficiência para aprender padrões anuais de curto prazo.                                                      |
| LSTM (Long Short-Term Memory) | Rede recorrente para capturar dependências temporais de longo prazo e variações sazonais complexas. | 2 camadas LSTM com 32 unidades cada, janela temporal de 20 observações, *dropout* para evitar *overfitting*. | Capacidade de memorizar dependências temporais de longo prazo e modelar a evolução sazonal da vegetação. |

#### Hiperparâmetros

A escolha dos hiperparâmetros foi crucial para otimizar o desempenho dos modelos. Ajustamos os hiperparâmetros para otimizar o desempenho dos modelos MLP e LSTM. O MLP utiliza uma janela temporal menor (5 observações) focada em padrões anuais, taxa de aprendizado de 2e-3, 300 épocas e arquitetura 32→16 neurônios, enquanto o LSTM emprega janela ampliada (20 observações) para capturar dependências temporais longas, com 2 camadas recorrentes (32 neurônios cada), dropout de 20% para regularização, taxa de aprendizado menor (5e-5) e treinamento prolongado (1000 épocas), sendo que ambas arquiteturas demonstram resultados consistentes (loss de validação ~0.19 e ~0.21 respectivamente), com configurações otimizadas mantendo batch sizes específicos (4 para MLP, 16 para LSTM) para equilibrar eficiência computacional e estabilidade do treinamento.

##### MLP Hyperparameters
*   MLP\_WINDOW\_SIZE = 5
*   MLP\_BATCH\_SIZE = 4
*   MLP\_BASE\_HIDDEN\_SIZE = 32
*   MLP\_EPOCHS = 300
*   MLP\_LEARNING\_RATE = 2e-3

##### LSTM Hyperparameters
*   LSTM\_WINDOW\_SIZE = 20
*   LSTM\_HIDDEN\_SIZE = 32
*   LSTM\_NUM\_LAYERS = 2
*   LSTM\_DROPOUT = 0.2
*   LSTM\_EPOCHS = 1000
*   LSTM\_BATCH\_SIZE = 16
*   LSTM\_LEARNING\_RATE = 5e-5

### Justificativa da Escolha das Variáveis

As principais variáveis utilizadas são:

*   **NDVI (Normalized Difference Vegetation Index):** Indicador da saúde da vegetação, obtido a partir de imagens de satélite. Reflete a quantidade e qualidade da biomassa vegetal, sendo um bom indicador da atividade fotossintética e do potencial de crescimento da cultura.
*   **Dados Históricos de Produção:** Quantidade produzida e área cultivada, provenientes de dados do IBGE. Permitem ao modelo aprender padrões históricos de produtividade e suas relações com o NDVI.
*   **Seno e Cosseno da Data:** Representações cíclicas da data (dia do ano) que permitem ao modelo capturar a sazonalidade da cultura e seus efeitos na produtividade.
*   **Ano:** Permite ao modelo identificar tendências de longo prazo e possíveis efeitos de mudanças climáticas ou tecnológicas na produtividade.
*   **Área (ha):** Área colhida em hectares.

### Justificativa do Modelo e sua Lógica Preditiva

O objetivo é prever a produtividade agrícola utilizando dados históricos de NDVI e produção. A lógica preditiva se baseia em:

*   **Relação entre NDVI e Produtividade:** Um NDVI mais alto geralmente indica maior biomassa e atividade fotossintética, o que, em teoria, se traduz em maior produtividade.
*   **Padrões Sazonais:** A cultura do café tem um ciclo de crescimento sazonal bem definido, que é capturado pelas representações cíclicas da data.
*   **Tendências de Longo Prazo:** O modelo pode aprender tendências de aumento ou diminuição da produtividade ao longo dos anos.

#### Arquiteturas

*   **MLP:** Adequado para aprender relações não lineares diretas entre o NDVI e a produtividade em um determinado ano. Útil para capturar padrões anuais.
*   **LSTM:** Capaz de modelar dependências temporais de longo prazo, o que é crucial para entender como a evolução da vegetação ao longo do tempo afeta a produtividade.

A escolha entre MLP e LSTM (ou a combinação de ambos) depende da complexidade dos dados e da importância das dependências temporais.

### Justificativa Técnica com Métricas e Gráficos Ilustrando os Resultados

Tanto os modelos MLP quanto LSTM foram avaliados utilizando a métrica de Mean Squared Error (MSE), em dados normalizados.
O modelo MLP obteve uma métrica MSE de 0.3241, enquanto o modelo LSTM obteve uma métrica de 0.4573, indicando que o modelo MLP apresentou uma performance superior, dado o conjunto de dados utilizado.

Visualização das predições do modelo MLP:

[MLP Predictions](./src/ml.ipynb)

Visualização das predições do modelo LSTM:

[LSTM Predictions](./src/ml.ipynb)

## Equipe

### Membros

- Amandha Nery (RM560030) 
- Bruno Conterato (RM561048)
- Gustavo Castro (RM560831)
- Kild Fernandes (RM560615)
- Luis Emidio (RM559976)

### Professores

- Tutor: Leonardo Ruiz Orabona
- Coordenador: André Godoi

## Tecnologias Utilizadas

| Categoria             | Ferramentas                  |
|------------------------|-------------------------------|
| Linguagem              | Python 3.9+                   |
| Manipulação de Dados   | Pandas, NumPy                 |
| Visualização           | Matplotlib                    |
| Aprendizado Profundo   | PyTorch                       |
| Pré-processamento      | Scikit-learn (StandardScaler) |
| Ambiente               | Jupyter Notebook, CUDA (GPU)  |

## Contato

Se tiver alguma dúvida, sinta-se à vontade para entrar em contato. 🚀
