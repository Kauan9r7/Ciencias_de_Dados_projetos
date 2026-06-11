# Tratamento de Dados — Autuações de Trânsito DF (2025)

Projeto final ou parte da disciplina de **Introdução à Ciência de Dados**, focado na extração, limpeza, padronização e estruturação de dados governamentais abertos sobre infrações de trânsito.

Esta pasta contém os seguintes arquivos:

- `README.md`
- `tratamento_dodos.ipynb`: Notebook com todo o fluxo de ETL (Extract, Transform, Load).
- `codigos_valores_multas.csv`: Tabela auxiliar com os códigos de infração do CTB e seus respectivos valores em Reais (R$).
- `dados_2025.parquet`: A base de dados final, limpa, tipada e unificada, pronta para análise.

## Base de Dados Original

Os dados brutos são fornecidos mensalmente pelo **Portal de Dados Abertos do DF** (infrações de trânsito de 2025). O notebook é responsável por baixar os 12 arquivos mensais via URL (`pd.read_csv`) e unificá-los em um único *DataFrame* usando `pd.concat`.

## Processo de Limpeza (O que o notebook faz)

O notebook `tratamento_dodos.ipynb` está dividido nas seguintes etapas de processamento:

1. **Coleta e Consolidação**: Lê os CSVs mensais diretamente dos links da transparência do DF.
2. **Inspeção Inicial**: Exibição da contagem e tipos iniciais das variáveis (geralmente lidas como texto).
3. **Análise da Distribuição**: Identificação de inconsistências em colunas categóricas (como letras maiúsculas/minúsculas e acentos).
4. **Padronização de Texto e Nulos**: 
   - Converte todas as categorias para minúsculo, remove acentuação e espaços duplos.
   - Preenche valores em branco ou `NaN` com a string constante `"Não informado"`.
5. **Conversão de Datas e Criação de Features**:
   - `cometimento` convertido para o tipo `datetime`.
   - Criação da nova coluna `dia_da_semana` baseada na data real do calendário.
   - `hora_cometimento` formatada corretamente (adição de `:00` nos segundos) e convertida para o tipo nativo `timedelta`.
6. **Cruzamento de Dados (Valores das Multas)**:
   - Faz a leitura da tabela auxiliar `codigos_valores_multas.csv`.
   - Realiza um `LEFT JOIN` (merge) utilizando o código da infração (`tipo_infracao`) para trazer a coluna numérica `Valor_multa` para a base original.
7. **Exportação Otimizada**:
   - Salva o resultado final no formato `.parquet`.
   - Este formato foi escolhido por preservar as tipagens nativas do Pandas (`datetime`, `timedelta`, `float`) e por entregar alta performance de leitura.

## Como utilizar

Para seguir com as análises (seja criando gráficos ou gerando estatísticas), basta abrir um novo notebook e carregar a base pré-processada:

```python
import pandas as pd

df = pd.read_parquet('dados_2025.parquet')
df.info()
```
