# Análise e Tratamento de Dados — Autuações de Trânsito DF (2025)

Projeto final da disciplina de **Introdução à Ciência de Dados**, focado na extração, limpeza, padronização e análise exploratória de dados governamentais abertos sobre infrações de trânsito. O projeto está dividido em duas etapas principais: ETL (Tratamento) e Visualização (Análise).

**Integrantes do Grupo:**
- Gabriel Queiroz — gabriel.sabatino@sempreceub.com
- Cauan Bastos — cauan.br@sempreceub.com
- Joao Tarik — joao.tarik@sempreceub.com
- Enzo Machado — enzo.machado@sempreceub.com

## 🌐 Apresentação Interativa

Os resultados da análise foram compilados em uma página web interativa (dashboard) rodando no GitHub Pages.
**[Acessar Apresentação: Infrações DF 2025](https://kauan9r7.github.io/Ciencias_de_Dados_projetos/trabalho-final.html)**

---
## Estrutura da Pasta

Esta pasta contém os seguintes arquivos e diretórios:

- `README.md`: Este documento.
- `tratamento_dodos.ipynb`: Notebook focado em extrair, limpar e unificar os dados (ETL).
- `analise.ipynb`: Notebook focado em análise exploratória de dados (EDA) e geração de gráficos.
- `dados/codigos_valores_multas.csv`: Tabela auxiliar montada manualmente com valores das multas.
- `dados/dados_2025.parquet`: A base de dados final, gerada pelo primeiro notebook e consumida pelo segundo.
- `docs/`: Pasta contendo a exportação em HTML e os arquivos de dados (JSON) que alimentam a apresentação interativa.

## Fontes e Bases de Dados

As bases utilizadas neste projeto são totalmente públicas e abertas:

1. **Dados de Infrações do DF (Base Principal):** Extraídos do [Portal de Dados Abertos do Distrito Federal](https://www.dados.df.gov.br/dataset/infracoes-transito). O notebook faz o download e a consolidação diretamente via URL.
2. **Valores das Multas (Base Secundária):** Baseado na [Portaria SENATRAN n.º 354/2022 (Anexo IV)](https://www.gov.br/transportes/pt-br/assuntos/transito/arquivos-senatran/portarias/2022/Portaria3542022AnexoN4.pdf), para correlacionar o código da infração ao valor pago.

## Parte 1: Processo de Limpeza (`tratamento_dodos.ipynb`)

Este notebook é responsável por preparar a base:

1. **Coleta e Consolidação**: Lê os CSVs mensais dos links da transparência do DF.
2. **Padronização de Texto**: Converte categorias para minúsculo e remove acentuação/espaços.
3. **Limpeza e Tratamento de Nulos**: Preenche dados vazios e remove colunas irrelevantes.
4. **Conversão de Datas (Features)**: Transforma colunas de data em tipos nativos (`datetime`, `timedelta`) e extrai o dia da semana.
5. **Cruzamento (Valores)**: Faz um `LEFT JOIN` com `dados/codigos_valores_multas.csv` para incluir o valor da infração em Reais.
6. **Exportação Otimizada**: Salva o arquivo final no formato `.parquet` para manter as tipagens do Pandas e garantir alta velocidade na próxima etapa.

## Parte 2: Análise Exploratória (`analise.ipynb`)

Este notebook consome a base pré-processada (`dados/dados_2025.parquet`) para responder perguntas-chave sobre as infrações no Distrito Federal através de gráficos:

1. **Onde ocorrem?** (Top rodovias autuadoras)
2. **Quando ocorrem?** (Distribuição por mês, dias da semana e hora do dia)
3. **Quais são os principais motivos?** (Excesso de velocidade, invasão de faixas, uso de celular)
4. **Qual a gravidade e valor?** (Análise da distribuição de multas médias e gravíssimas e arrecadação)
5. **Quais veículos mais cometem infrações?** (Automóveis, caminhonetes, motos, etc.)

Os insights e os dados tratados neste notebook foram exportados e integram o **Dashboard Interativo** hospedado no GitHub Pages (link acima).

## Como utilizar

Para reproduzir o projeto, siga a ordem dos notebooks:
1. Rode todas as células de `tratamento_dodos.ipynb` para gerar a base parquet dentro da pasta `dados/`.
2. Rode `analise.ipynb` para ler a base e visualizar as distribuições estatísticas.
