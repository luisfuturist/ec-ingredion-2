# ec-ingredion-2

> Este projeto faz parte do curso de **Inteligência Artificial** oferecido pela [FIAP](https://github.com/fiap) - Online 2024. Este repositório reúne os materiais relacionados ao **Enterprise Challenge - Ingredion**, correspondendo à **Sprint 2** do desafio.

- Video de Apresentação: [Youtube]()
- Notebook para Correção: [Jupyter Notebook](./src/ml.ipynb)

## Descrição

Este projeto desenvolve um modelo de aprendizado de máquina para previsão de produtividade agrícola na região de Manhuaçu (MG), substituindo métodos tradicionais de análise baseados em estimativas manuais e dados desconectados. Ao integrar imagens de satélite (índice de vegetação NDVI) e dados históricos de produção, o modelo identifica padrões sazonais e relações entre saúde vegetal e produtividade, gerando previsões precisas para auxiliar na tomada de decisões. A solução melhora a eficiência no planejamento agrícola, reduz perdas por fatores ambientais e otimiza a alocação de recursos, sendo adaptável a diferentes culturas e escalável para outras regiões.

## Estrutura de Arquivos

```txt
.
├── data - Arquivos de entrada e saída usados no processo
│   ├── PROCESSED
│   │   ├── manhuacu.csv
│   │   └── ndvi.csv
│   ├── GOOGLE_EARTH_ENGINE
│   │   └── ndvi_manhuacu.csv - Série NDVI (2000–2025): Google Earth Engine
│   └── SIDRA
│       └── tabela1613.xlsx - Dados de produção (1974–2023): IBGE/Tabela 1613
├── models
│   ├── lstm.pth - Pesos do modelo LSTM
│   └── mlp.pth - Pesos do modelo MLP
├── README.md - Este README
├── requirements.txt
├── scripts
│   └── extract-ndvi-manhuacu.ipynb - Jupyter Notebook para extração de dados NDVI de Manhuaçu, MG
│   └── prepare-data.ipynb - Jupyter Notebook para preparação de dados
├── src
│   └── eda.ipynb - Notebook de Análise Exploratória e Estatísticas Resultantes 
│   └── ml.ipynb - Notebook de Implementação dos Modelos de IA
└── TODO.md - Gestão do projeto
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

[png1] [png2]

### Processo de Preparação dos Dados

- Link para código e documentação: [Jupyter Notebook](./scripts/prepare-data.ipynb)

### Funcionamento do Código

#### Modelagem e Algoritmos

#### Abordagens Implementadas

Foram desenvolvidas e comparadas duas arquiteturas de redes neurais profundas, cada uma com características específicas para o problema de previsão de produtividade agrícola:

MLP (Multilayer Perceptron)	Rede neural densa para capturar padrões não lineares.	- Camadas ocultas: 32 → 16 neurônios
 - Função de ativação: ReLU + Tanh amplificada
 - Janela temporal: 5 observações

LSTM (Long Short-Term Memory)	Rede recorrente para dependências temporais de longo prazo.	- Camadas LSTM: 2
 - Neurônios ocultos: 32
 - Janela temporal: 20 observações

Critério de Escolha:
 - MLP: Simplicidade e eficiência para padrões anuais.
 - LSTM: Capacidade de memorizar variações sazonais complexas.

### Justificativa da Escolha das Variáveis

### Justificativa do Modelo e sua Lógica Preditiva

### Justificativa Técnica com Métricas e Gráficos Ilustrando os Resultados

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
