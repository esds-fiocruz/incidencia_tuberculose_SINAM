# 🦠 Incidência de Tuberculose (SINAN/DataSUS)

Este projeto contém um script em Python (Jupyter Notebook) desenvolvido para automatizar a extração de dados do Sistema de Informação de Agravos de Notificação (SINAN) e calcular o **Coeficiente de Incidência de Casos Novos de Tuberculose por 100 mil habitantes**, agrupado por Unidade Federativa (UF) do Brasil.

## 🎯 Objetivo

Facilitar a obtenção e o processamento de dados epidemiológicos públicos, integrando os registros de Tuberculose do DataSUS com as projeções populacionais do IBGE, gerando uma planilha final pronta para análise e visualização de dados.

## ✨ Funcionalidades

*   **Extração Automatizada:** Download direto dos arquivos `.dbc` (convertidos para `.parquet` e depois `.csv`) da base do SINAN utilizando a biblioteca `PySUS`.
*   **Filtro Histórico:** Obtenção nativa dos dados dos anos de 2019 a 2023.
*   **Limpeza e Processamento:** Filtro específico para "Casos Novos" (considerando os códigos de tratamento `1` - Caso Novo, `4` - Não Sabe, e `6` - Pós-óbito).
*   **Cálculo Epidemiológico:** Cruzamento dos casos confirmados com os dados populacionais do IBGE para cálculo exato da incidência por 100 mil habitantes (`(Casos / População) * 100.000`).
*   **Exportação Organizada:** Geração de um arquivo Excel consolidado (`TUB_CN_GERAL.xlsx`), contendo uma aba (sheet) dedicada para cada ano analisado.

## 🛠️ Tecnologias e Bibliotecas Utilizadas

*   `Python 3`
*   `pandas` (Manipulação e análise de dados)
*   `numpy` (Operações numéricas)
*   `PySUS` (Interface para os dados do DataSUS/SINAN)
*   `openpyxl` (Criação e manipulação de planilhas Excel)

## 🚀 Como Utilizar

### 1. Pré-requisitos
O notebook foi estruturado considerando o ambiente do **Google Colab** (utilizando caminhos como `/content/`). Para rodar o código, você precisará instalar as dependências principais:

```bash
pip install pysus
pip install --upgrade openpyxl pandas numpy
```

### 2. Arquivos Necessários
Para que o cruzamento de dados funcione corretamente, é **obrigatório** ter o arquivo com a projeção populacional do IBGE no diretório raiz de execução (`/content/` no Colab):
*   📄 `dados_ibge_projecao_tab_net_2022.xlsx` (Deve conter as colunas `CODIGO_UF` e `POP_ANT`).

### 3. Execução
Basta executar todas as células do notebook sequencialmente. O script fará o download dos arquivos (que podem demorar alguns minutos dependendo do tamanho), criará a estrutura de pastas e consolidará as informações.

Para rodar a função principal com os parâmetros padrão (todos os anos de 2019 a 2023 e todas as UFs), execute:

```python
cria_df()
```

*(Opcional)* Você pode passar anos ou UFs específicas como parâmetros caso a função seja adaptada futuramente.

## 📁 Estrutura de Diretórios Gerada

Após a execução bem-sucedida, o script criará a seguinte estrutura no seu ambiente:

```text
/content/
│
├── dados_ibge_projecao_tab_net_2022.xlsx  (Input manual necessário)
│
└── TUB_CN/
    ├── 2019/
    │   └── TUB_CN_2019.csv
    ├── 2020/
    │   └── TUB_CN_2020.csv
    ├── ...
    └── TUB_CN_GERAL.xlsx                  (Output Final Consolidado)
```

## ⚠️ Observações Importantes

*   **Padrão de Dados do SINAN:** Os dados do DataSUS são atualizados periodicamente. O tamanho dos arquivos e a disponibilidade podem variar conforme a data de execução do script.
*   **Dicionário de Variáveis:** O mapeamento dos estados foi feito convertendo os códigos numéricos do IBGE (ex: `33`) para as siglas correspondentes (ex: `RJ`).
