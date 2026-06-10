# Medidas e Visualizacoes - Bolsa Familia

Exercicios praticos da disciplina **Introducao a Ciencia de Dados** com foco em metricas descritivas e visualizacoes graficas a partir dos dados abertos do programa **Bolsa Familia**.

Esta pasta contem dois notebooks complementares:

- `README.md`
- `Exercicio_1_BolsaFamilia_Metricas.ipynb`
- `Exercicio_2_BolsaFamilia_Visualizacoes.ipynb`

## Base de dados

Os dois notebooks usam a mesma base, disponivel no Google Drive e carregada via `gdown`:

```python
import gdown
import tempfile, os, uuid
import pandas as pd

temp_path = os.path.join(tempfile.gettempdir(), f"dataset_{uuid.uuid4().hex}.parquet")
gdown.download(id='13KRdiYnQikDx3pxPKGUTeejOz1fLHjzm', output=temp_path, quiet=True)
df = pd.read_parquet(temp_path)
```

O dataset contem registros de beneficiarios do Bolsa Familia com colunas como `UF`, `NOME MUNICIPIO`, `NOME FAVORECIDO`, `VALOR PARCELA` e `MES REFERENCIA`.

## Exercicio 1 - Metricas com Pandas

Lista de 15 questoes respondidas com operacoes basicas do `pandas`, sem graficos.

### O que o notebook responde

1. Quantas linhas existem no `df`?
2. Quantas colunas existem no `df`?
3. Quantos registros tem `cpf_favorecido` preenchido?
4. Quantos valores distintos existem em `cpf_favorecido`?
5. Quantos `nis_favorecido` distintos existem?
6. Quantos municipios distintos aparecem em `nome_municipio`?
7. Quantas UFs distintas aparecem?
8. Qual e a media de `valor_parcela`?
9. Qual e a mediana de `valor_parcela`?
10. Qual e o valor minimo de `valor_parcela`?
11. Qual e o valor maximo de `valor_parcela`?
12. Contagem de registros por UF - qual e a maior?
13. Media de `valor_parcela` por UF - qual e a maior?
14. Mediana de `valor_parcela` por municipio - qual e a maior?
15. Maximo de `valor_parcela` por `mes_referencia` - qual e o maior?

## Exercicio 2 - Visualizacoes com Matplotlib

Lista de 15 questoes respondidas com graficos gerados via `matplotlib` e `seaborn`. O notebook roda o Exercicio 1 internamente via `%run` para reutilizar o DataFrame ja limpo.

### O que o notebook responde

1. Grafico de barras da contagem de registros por UF.
2. Grafico de barras horizontal com os 10 municipios com mais registros.
3. Grafico de linha com a soma de `valor_parcela` por `mes_referencia`.
4. Grafico de linha com a soma total paga por mes (questao com funcao reutilizavel).
5. Grafico de linha com a contagem de registros por mes.
6. Histograma de `valor_parcela` com `bins=8`.
7. Histograma com linhas de media e mediana destacadas.
8. Boxplot geral de `valor_parcela` com Q1, mediana e Q3.
9. Boxplot por UF (top 5 UFs com mais registros).
10. Grafico de dispersao de `mes_referencia` x `valor_parcela` com correlacao de Pearson.
11. Grafico de barras com a contagem de nomes distintos por UF.
12. Grafico de pizza com a participacao da soma de `valor_parcela` por UF (top 5 + Outros).
13. Grafico de barras da media de `valor_parcela` por municipio (apenas municipios com 2+ registros).
14. Heatmap (UF x mes) com contagem de registros usando `imshow`.
15. Grafico de linha acumulado da soma de `valor_parcela` por mes.

## Observacoes sobre a base

- A coluna `MES REFERENCIA` foi convertida de inteiro (`202601`) para `datetime` no inicio do Exercicio 2.
- A coluna `VALOR PARCELA` foi convertida de string (com virgula) para `float` no Exercicio 1.
- Linhas com valores nulos foram removidas antes das analises.
- O Exercicio 2 importa o Exercicio 1 via `%run` para evitar duplicacao de codigo.
