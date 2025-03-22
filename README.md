# 9SOAT-G63-MC-KING
## Tech Challenge FIAP - 9SOAT - Grupo 63

## Pipeline Status

[![Liquibase Migration](https://github.com/renaneustaquio/FiapTech-Challenge-Fiap-mcking-liquibase-Fase3/actions/workflows/liquibase.yml/badge.svg)](https://github.com/renaneustaquio/FiapTech-Challenge-Fiap-mcking-liquibase-Fase3/actions/workflows/liquibase.yml)

### Participantes:
- **Mayara Manzi** - RM359734 

mayaramanzi@hotmail.com

- **Renan Eustaquio Claudiano Martins** - RM359737

renan.ecm@outlook.com



## Objetivo
Este projeto visa implementar um sistema de autoatendimento para uma lanchonete de bairro que está em expansão devido ao seu grande sucesso. O objetivo é melhorar o atendimento aos clientes e garantir a precisão dos pedidos, minimizando confusões e atrasos.

### Benefícios esperados:
- **Melhorar a eficiência do atendimento:** Reduzir o tempo de espera dos clientes e garantir a precisão dos pedidos.
- **Aumentar a satisfação dos clientes:** Oferecer uma experiência de atendimento moderna e eficiente.

## Entregáveis - Fase 3
Dando continuidade ao desenvolvimento do software para a lanchonete, teremos as seguintes melhorias e alterações:

1. **Implementação de API Gateway e Function Serverless para autenticação via CPF:**
   - Integração ao sistema de autenticação para identificar o cliente.
2. **Implementação de CI/CD segregado por repositórios:**
   - **1 repositório** para o Lambda.
   - **1 repositório** para infraestrutura VPC via Terraform.
   - **1 repositório** para infraestrutura Kubernetes via Terraform.
   - **1 repositório** para infraestrutura de banco de dados gerenciáveis via Terraform.
   - **1 repositório** para a aplicação executada no Kubernetes.
   - **1 repositório** para versionamento do banco com Liquibase.
3. **Deploy automatizado via Actions:**
   - As branches `master` serão protegidas.
   - Os commits diretos serão bloqueados, exigindo o uso de Pull Requests.
4. **Melhoria da estrutura do banco de dados:**
   - Documentação seguindo padrões de modelagem de dados.
   - Justificativa da escolha do banco de dados.
5. **Uso obrigatório de serviços serverless:**
   - **Functions:** AWS Lambda, Azure Functions ou Google Functions.
   - **Banco de dados gerenciáveis:** AWS RDS, Banco de Dados do Azure ou Cloud SQL no GCP.
   - **Sistema de autenticação:** AWS Cognito, Microsoft AD ou Google Identity Platform.

## Principais Tecnologias Utilizadas
- **Visual Studio 2022**
- **.NET - 8.0**
- **Postgres - 16.4**
- **AWS EKS**
- **AWS RDS**
- **AWS VPC**
- **AWS Secrets Manager**
- **Cognito**
- **Liquibase**

## Guia de Setup - Versionamento de Banco com Liquibase
Este repositório gerencia o versionamento da base de dados da aplicação McKing utilizando Liquibase, com execução via Kubernetes (EKS).

### Pré-requisitos
Para que o Liquibase funcione corretamente, é necessário que os seguintes repositórios de infraestrutura Terraform já estejam aplicados:
- Infraestrutura **VPC**.
- Infraestrutura **Kubernetes (EKS)**.
- Infraestrutura do **banco de dados (RDS)**.

### Executando Liquibase via GitHub Actions
O pipeline executa um Job Kubernetes no EKS que:
- Extrai a URL do banco via AWS Secrets Manager.
- Monta os arquivos changelog via ConfigMap.
- Executa o Liquibase automaticamente.

### Rodando Manualmente com Docker
Os dados de conexão (URL, usuário e senha) podem ser obtidos de forma segura através do AWS Secrets Manager, conforme configurado na infraestrutura.

```bash
docker run --rm \
  -v $(pwd)/liquibase/changelog:/liquibase/changelog \
  liquibase/liquibase \
  --url="jdbc:postgresql://<host>:5432/<db>?user=<user>&password=<pass>" \
  --changeLogFile=changelog/db.changelog-master.xml \
  update
```

