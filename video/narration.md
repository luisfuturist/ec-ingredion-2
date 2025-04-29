## Narrações Contextualizadas para Vídeo (3 minutos)

**[0:00 - 0:15] Introdução e Contexto (15 segundos)**

"Olá! Bem-vindos a esta demonstração da nossa solução para o Challenge Ingredion! Nosso grupo desenvolveu um sistema de Machine Learning para prever a produtividade agrícola, combinando dados de satélite e históricos de produção. Acompanhe a solução!"

**[0:15 - 0:45] Coleta e Pré-processamento de Dados (30 segundos)**

"Começamos importando as bibliotecas necessárias para manipular dados, visualizar e construir os modelos preditivos. Em seguida, coletamos dados de duas fontes principais: imagens de satélite NDVI, que refletem a saúde da vegetação e dados históricos de produção agrícola. Os dados de NDVI foram coletados através da API do Google Earth Engine."

"Com os dados em mãos, realizamos um pré-processamento crucial: transformamos as datas em representações cíclicas para preservar a sazonalidade, normalizamos os valores para otimizar o treinamento dos modelos e organizamos os dados em janelas temporais para capturar dependências ao longo do tempo."

**[0:45 - 1:30] Criação e Treinamento dos Modelos (45 segundos)**

"Implementamos dois modelos de Machine Learning para abordar diferentes aspectos da previsão. O MLP, com sua arquitetura mais simples, foca em padrões anuais, enquanto o LSTM, uma rede recorrente, captura dependências temporais de longo prazo."

"O treinamento dos modelos envolveu a utilização de conjuntos de dados divididos para treino, validação e teste, otimização com o algoritmo Adam e monitoramento contínuo do erro no conjunto de validação para evitar overfitting, uma situação onde o modelo aprende muito bem o conjunto de treino e mal o conjunto de validação."

**[1:30 - 2:15] Avaliação e Resultados (45 segundos)**

"Após o treinamento, avaliamos o desempenho dos modelos no conjunto de teste para verificar sua capacidade de generalização para dados novos."

"Os resultados mostraram um erro médio quadrado (MSE) de 0.2540 para o MLP e de 0.3796 para o LSTM no conjunto de teste. Isso indica que os modelos conseguiram aprender padrões importantes."

**[2:15 - 2:45] Discussão e Conclusões (30 segundos)**

"Em resumo, nossa solução demonstrou o potencial do Machine Learning para prever a produtividade agrícola, integrando dados de diferentes fontes e utilizando modelos adequados para capturar padrões complexos. No entanto, existem oportunidades para aprimorar ainda mais a solução, explorando janelas temporais mais longas, técnicas de regularização mais avançadas e a combinação dos dois modelos."

**[2:45 - 3:00] Encerramento e Agradecimentos (15 segundos)**

"Agradecemos a atenção e esperamos que este vídeo tenha demonstrado o funcionamento da nossa solução de forma clara e concisa. Obrigada!"
