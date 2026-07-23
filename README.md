## End-to-End Data Pipeline: Gestão de Estoque e Analytics para E-commerce

## Sobre o Projeto
Este projeto consiste em uma arquitetura completa de dados (End-to-End) desenvolvida para automatizar a gestão de estoque e a análise financeira de um e-commerce de joias e semijoias. 

O pipeline substitui o controle manual isolado por um fluxo automatizado na nuvem, permitindo o rastreamento histórico de flutuação de produtos, análises de Business Intelligence e previsão de reposição de estoque (Curva ABC).

## Arquitetura e Tecnologias
O projeto foi construído utilizando os conceitos de Engenharia de Dados (ETL) e Analytics Engineering:

* **Origem dos Dados (Extract):** Google Sheets API (Input operacional diário).
* **Processamento (Transform):** Python (Pandas) no Google Colab. 
  * Limpeza de strings (moedas, caracteres especiais).
  * Conversão de tipagem de dados.
  * Inserção de temporalidade (`data_carga`) para construção de histórico diário.
* **Armazenamento (Load):** Google BigQuery (GCP). Carga incremental (`append`) gerenciada via código para empilhamento de dados sem duplicidade.
* **Segurança e IAM:** Proteção de credenciais (Service Account JSON) utilizando o cofre de segredos nativo do ambiente de desenvolvimento.
* **Visualização (BI):** Microsoft Power BI.
  * Conexão direta com o BigQuery.
  * Modelagem dimensional e criação de métricas com DAX (Ex: Filtro dinâmico de "Última Carga", Valor Investido em Estoque).

## Como Executar o Pipeline
1. Clone este repositório.
2. Configure uma Service Account no Google Cloud Platform com acessos às APIs do Google Drive, Google Sheets e BigQuery.
3. Insira o JSON da Service Account nas variáveis de ambiente (Secrets).
4. Execute o notebook `pipeline_estoque_bq.ipynb` para realizar a carga dos dados.
5. Atualize o relatório `.pbix` no Power BI para consumir os novos dados inseridos.

## 📈 Impacto para o Negócio
* **Visibilidade Financeira:** Transformação de dados brutos de quantidade em valor financeiro real investido em tempo real.
* **Histórico de Dados:** Criação de uma base sólida para futuras implementações de Machine Learning (previsão de demanda), saindo de uma visão "estática" para uma visão "temporal" do estoque.
* **Automação:** Redução de horas manuais de compilação de dados e eliminação de erros humanos na geração de relatórios.
