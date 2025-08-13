# Desafio Alura Store — Data Science

**Objetivo:** indicar **qual loja** o Sr. João deve vender a partir da análise de faturamento, categorias, avaliações, produtos e frete.

**Conclusão (TL;DR):** recomendar a **venda da _loja_4_** — é a que apresenta **menor faturamento total** e não se destaca nas demais métricas a ponto de compensar essa desvantagem.

---

## 1) Dados e Reprodutibilidade

- Fonte: 4 arquivos CSV (uma base por loja).
- Tamanho consolidado: **9.435** registros (~2,36k por loja).
- Leitura das datas: formato **dia/mês/ano** → usar `dayfirst=True` no `read_csv`.

**Como executar no Google Colab**
1. Abra o notebook `AluraStoreBr.ipynb` no Colab.
2. Execute a célula de **importação** (lê as 4 URLs/CSVs).
3. Execute a **preparação e unificação** (cria o DataFrame `base`):
   ```python
   def prepara(df, nome):
       df = df.copy()
       df["Data da Compra"] = pd.to_datetime(df["Data da Compra"], dayfirst=True, errors="coerce")
       for col in ["Preço","Frete","Avaliação da compra","Quantidade de parcelas","lat","lon"]:
           if col in df.columns: df[col] = pd.to_numeric(df[col], errors="coerce")
       df["loja"] = nome
       return df

   loja_1 = prepara(loja, "loja_1")
   loja_2 = prepara(loja2, "loja_2")
   loja_3 = prepara(loja3, "loja_3")
   loja_4 = prepara(loja4, "loja_4")
   base = pd.concat([loja_1, loja_2, loja_3, loja_4], ignore_index=True)
