# Configuração de ML Automatizado no Azure Machine Learning Studio

Este guia detalha as etapas para configurar um trabalho de ML automatizado no Azure Machine Learning Studio para prever o número de aluguéis de bicicletas.

---

## 1. Acessar a Página de ML Automatizado

No Azure Machine Learning Studio:
- Navegue até a página **ML Automatizado** em **Criação**.

---

## 2. Criar um Novo Trabalho de ML Automatizado

### Configurações Básicas
- **Nome do trabalho**: Utilize o nome gerado automaticamente.
- **Novo nome do experimento**: `mslearn-bike-rental`
- **Descrição**: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- **Tags**: Nenhuma

---

## 3. Tipo de Tarefa e Dados

### Tipo de Tarefa
- Selecione **Regressão**

### Selecionar Conjunto de Dados
Crie um novo conjunto de dados com as seguintes configurações:

- **Tipo de Dados**:
  - **Nome**: `bike-rentals`
  - **Descrição**: Historic bike rental data
  - **Tipo**: Tabela (`mltable`)

- **Fonte de Dados**:
  - Selecione **De arquivos locais**
  - **Tipo de armazenamento de destino**:
    - **Tipo de armazenamento de dados**: Azure Blob Storage
    - **Nome**: `workspaceblobstore`

- **Seleção de MLtable**:
  - **Pasta de Upload**: [Baixe e descompacte a pasta com os arquivos necessários](https://aka.ms/bike-rentals)
  - Selecione **Criar**.

Após a criação, selecione o conjunto de dados `bike-rentals` para continuar.

---

## 4. Configurações da Tarefa

### Tipo de Tarefa
- **Tipo de Tarefa**: Regressão
- **Conjunto de Dados**: aluguel de bicicletas
- **Coluna de Destino**: `aluguéis` (inteiro)

### Configurações Adicionais
- **Métrica Primária**: `NormalizedRootMeanSquaredError`
- **Explique o Melhor Modelo**: Não selecionado
- **Habilitar Empilhamento de Conjunto**: Não selecionado
- **Usar Todos os Modelos Suportados**: Não selecionado
- **Modelos Permitidos**: 
  - `RandomForest`
  - `LightGBM`

### Limites
- **Máximo de Ensaios**: `3`
- **Máximo de Ensaios Simultâneos**: `3`
- **Máximo de Nós**: `3`
- **Limite de Pontuação Métrica**: `0.085`
- **Tempo Limite do Experimento**: `15`
- **Tempo Limite de Iteração**: `15`
- **Habilitar Rescisão Antecipada**: Selecionado

### Validação e Teste
- **Tipo de Validação**: Divisão de validação de trem
- **Porcentagem de Dados de Validação**: `10`
- **Conjunto de Dados de Teste**: Nenhum

---

## 5. Cálculo

- **Tipo de Computação**: Sem servidor
- **Tipo de Máquina Virtual**: CPU
- **Camada de Máquina Virtual**: Dedicada
- **Tamanho da Máquina Virtual**: `Standard_DS3_V2`
- **Número de Instâncias**: `1`

---

## 6. Enviar o Trabalho de Treinamento

- Envie o trabalho de treinamento, que será iniciado automaticamente.
- **Tempo de Espera**: Pode levar um tempo considerável para finalizar.

---

## 7. Avaliar o Melhor Modelo

- Na guia **Visão Geral** do trabalho de ML automatizado:
  - Revise o **Melhor Resumo do Modelo**.
  - Clique em **Nome do Algoritmo** para visualizar os detalhes.

### Métricas e Gráficos
- Vá para a guia **Métricas**.
- Selecione os gráficos **Residuais** e **Prediction_True**:
  - **Gráfico de Resíduos**: Histograma das diferenças entre valores previstos e reais.
  - **Prediction_True**: Compara valores previstos com valores verdadeiros.

---

## 8. Implantar e Testar o Modelo

### Implantação do Modelo
Na guia **Modelo** para o melhor modelo treinado:
- Clique em **Implantar** e selecione **Ponto de Extremidade em Tempo Real**.
- **Configurações**:
  - **Máquina Virtual**: `Standard_DS3_V2`
  - **Contagem de Instâncias**: `3`
  - **Ponto de Extremidade**: Novo (use o nome padrão ou um exclusivo)
  - **Nome da Implantação**: Padrão
  - **Inferência de Coleta de Dados**: Desativado
  - **Modelo de Pacote**: Desativado

### Acompanhar a Implantação
- O status inicial será **Running**.
- Aguarde até que o status mude para **Succeeded** (5 a 10 minutos).

---

## 9. Testar o Serviço Implantado

- No **Azure Machine Learning Studio**, navegue até **Endpoints**.
- Abra o endpoint em tempo real `predict-rentals`.


