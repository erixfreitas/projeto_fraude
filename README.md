
# 🔍 Detecção de Fraude em Transações

Este projeto é um aplicativo desenvolvido com **Streamlit** para prever se uma transação financeira é fraudulenta, utilizando um modelo de Regressão Logística.

---

## 📚 Índice

1. [Objetivo](#objetivo)  
2. [Como Executar](#como-executar)  
   - [Clonando o Repositório](#clonando-o-repositório)  
   - [Instalando as Dependências](#instalando-as-dependências)  
   - [Executando o App](#executando-o-app)  
3. [Explicação do Código](#explicação-do-código)  
4. [Glossário](#glossário)  
5. [Requisitos](#requisitos)  
6. [Autor](#autor)  

---

## 🎯 Objetivo

Criar uma aplicação web simples e interativa para detectar fraudes em transações com base em dados de entrada fornecidos pelo usuário.

---

## ▶️ Como Executar

### 📁 Clonando o Repositório

```bash
git clone https://github.com/seuusuario/projeto-fraude.git
cd projeto-fraude
```

### 📦 Instalando as Dependências

**Usando o arquivo requirements.txt:**

```bash
pip install -r requirements.txt
```

**Ou instalando os pacotes individualmente:**

```bash
pip install streamlit numpy scikit-learn
```

### 🚀 Executando o App

```bash
streamlit run app.py
```

---

## 🧠 Explicação do Código

### 🔹 Importação de Bibliotecas

```python
import streamlit as st
import pickle
import numpy as np
```

- `streamlit`: Framework para construção da interface web.  
- `pickle`: Carrega o modelo treinado.  
- `numpy`: Manipulação de arrays numéricos.  

### 🔹 Carregamento do Modelo

```python
with open('modelo_fraude.pkl', 'rb') as file:
    fraud_model = pickle.load(file)
```

Carrega o modelo de Regressão Logística treinado e salvo no arquivo `.pkl`.

### 🔹 Interface com o Usuário

```python
st.title("Detecção de Fraude em Transações")
st.header("Detalhes da Transação")
```

Define o título e as seções principais do app.

### 🔹 Entrada de Dados

```python
valor_transacao = st.number_input("Valor da Transação (em dólares)", ...)
tempo_conta = st.number_input("Tempo de Conta (em meses)", ...)
num_transacoes_ult_30d = st.number_input("Número de Transações nos Últimos 30 dias", ...)
```

Campos para entrada dos dados da transação.

```python
pais_origem_opcoes = {"Brasil": 0, "EUA": 1, "Outros": 2}
pais_origem_escolhido = st.selectbox("País de Origem", list(pais_origem_opcoes.keys()))
```

Codificação numérica do país de origem.

### 🔹 Predição

```python
if st.button("Verificar se é Fraude"):
    input_array = np.array([[valor_transacao, tempo_conta, num_transacoes_ult_30d, pais_origem]])
    pred = fraud_model.predict(input_array)
    proba = fraud_model.predict_proba(input_array)
```

Executa a predição e obtém as probabilidades associadas.

### 🔹 Exibição dos Resultados

```python
if pred[0] == 1:
    st.error("Alerta: Transação com ALTO risco de fraude.")
else:
    st.success("Transação aparentemente legítima.")

st.write(f"**Probabilidade de Não Fraude:** {proba[0][0]:.2f}")
st.write(f"**Probabilidade de Fraude:** {proba[0][1]:.2f}")
```

Exibe a classificação e as probabilidades de fraude.

---

## 📘 Glossário

| Termo                 | Definição                                                                 |
|----------------------|---------------------------------------------------------------------------|
| Streamlit            | Framework para criação de apps interativos em Python                      |
| Regressão Logística  | Algoritmo de ML para classificação binária                                |
| Pickle               | Módulo de serialização de objetos Python                                  |
| predict              | Método que retorna a classe prevista pelo modelo                          |
| predict_proba        | Método que retorna as probabilidades associadas às classes                |
| Tempo de Conta       | Idade da conta em meses                                                   |
| Número de Transações | Total de transações recentes registradas em um período específico         |

---

## 📦 Requisitos

- Python 3.7 ou superior  
- Bibliotecas:
  - streamlit
  - numpy
  - scikit-learn

---



