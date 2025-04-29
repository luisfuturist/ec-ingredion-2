## Roteiro para Vídeo Demonstrativo (3 minutos)

**Título:** Previsão de Produtividade Agrícola com Machine Learning

**Objetivo:** Demonstrar o fluxo completo da solução de Machine Learning, desde a coleta e pré-processamento dos dados até a avaliação dos modelos.

**Estrutura:**

**[0:00 - 0:15] Introdução e Contexto (15 segundos)**

*   **Imagem:** Logo da FIAP, título do desafio, nome do grupo.
*   **Narração:** "Olá! Bem-vindos a esta demonstração da nossa solução para o Challenge Ingredion! Nosso grupo desenvolveu um sistema de Machine Learning para prever a produtividade agrícola, combinando dados de satélite e históricos de produção. Acompanhe a solução!"
*   **Imagem:** Breve animação mostrando um campo agrícola e dados sendo sobrepostos.

**[0:15 - 0:45] Coleta e Pré-processamento de Dados (30 segundos)**

*   **Imagem:** Snippet de código mostrando a importação das bibliotecas essenciais (Pandas, NumPy, Matplotlib, PyTorch, etc.).
*   **Narração:** "Começamos importando as bibliotecas necessárias. Em seguida, coletamos dados de duas fontes principais: imagens de satélite NDVI, que refletem a saúde da vegetação, e dados históricos de produção agrícola."
*   **Imagem:** Rapidamente, mostrar o início e o fim da execução da célula com a coleta de dados via API do Google Earth Engine (mostrar o gráfico gerado).
*   **Imagem:** Snippet de código mostrando a leitura dos dados (NDVI e produção) com Pandas.
*   **Narração:** "Com os dados em mãos, realizamos um pré-processamento crucial: padronização das datas em representações cíclicas para preservar a sazonalidade, normalização dos valores para otimizar o treinamento dos modelos e organização em janelas temporais para capturar dependências ao longo do tempo."

**[0:45 - 1:30] Criação e Treinamento dos Modelos (45 segundos)**

*   **Imagem:** Snippet de código mostrando a definição das arquiteturas dos modelos: MLP (Multilayer Perceptron) e LSTM (Long Short-Term Memory).
*   **Narração:** "Implementamos dois modelos de Machine Learning para abordar diferentes aspectos da previsão. O MLP, com sua arquitetura mais simples, foca em padrões anuais, enquanto o LSTM, uma rede recorrente, captura dependências temporais de longo prazo."
*   **Imagem:** Mostrar brevemente o início e o fim da execução das células com o treinamento dos modelos (mostrar o progresso da otimização e os gráficos de perda/erro).
*   **Narração:** "O treinamento dos modelos envolveu a utilização de conjuntos de dados divididos para treino, validação e teste, otimização com o algoritmo Adam e monitoramento contínuo para evitar overfitting."

**[1:30 - 2:15] Avaliação e Resultados (45 segundos)**

*   **Imagem:** Snippet de código mostrando a avaliação dos modelos no conjunto de teste.
*   **Narração:** "Após o treinamento, avaliamos o desempenho dos modelos no conjunto de teste para verificar sua capacidade de generalização para dados novos."
*   **Imagem:** Gráfico comparando as previsões do modelo MLP com os dados reais da produção.
*   **Narração:** "Os resultados mostraram um MSE de 0.2540 para o MLP e de 0.3796 para o LSTM no conjunto de teste."
*   **Imagem:** Gráfico comparando as previsões do modelo LSTM com os dados reais da produção.

**[2:15 - 2:45] Discussão e Conclusões (30 segundos)**

*   **Imagem:** Slide com bullet points listando as principais conclusões e possíveis melhorias.
*   **Narração:** "Em resumo, nossa solução demonstrou o potencial do Machine Learning para prever a produtividade agrícola, integrando dados de diferentes fontes e utilizando modelos adequados para capturar padrões complexos. No entanto, existem oportunidades para aprimorar ainda mais a solução, explorando janelas temporais mais longas, técnicas de regularização mais avançadas e a combinação dos dois modelos."

**[2:45 - 3:00] Encerramento e Agradecimentos (15 segundos)**

*   **Imagem:** Slide com os nomes dos membros do grupo.
*   **Narração:** "Agradecemos a atenção e esperamos que este vídeo tenha demonstrado o funcionamento da nossa solução de forma clara e concisa. Obrigada!"

**Dicas:**

*   Mantenha a linguagem simples e evite jargões técnicos excessivos.
*   Utilize recursos visuais atraentes para ilustrar os conceitos.
*   Realize cortes estratégicos no vídeo para agilizar a demonstração e evitar tempos de espera longos.
*   Use música de fundo suave e agradável.
*   Mantenha o ritmo do vídeo dinâmico e envolvente.
