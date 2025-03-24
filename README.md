# snackbar-pipeline
---

# CI/CD Pipeline

Este repositório contém a configuração de pipeline de CI/CD responsável por automatizar o processo de build, testes, e deploy de nossa aplicação Snackbar. A pipeline foi configurada para garantir que a aplicação seja testada corretamente e implantada de forma eficiente usando infraestrura Cloud AWS e Atlas MongoDB.

## Propósito

O principal objetivo desta pipeline é automatizar as seguintes etapas:
- **Build**: Criação de builds consistentes para garantir que a aplicação esteja pronta para execução.
- **Testes**: Execução de testes unitários pata validar funcionalidade do código.
- **Deploy**: Implantação automática da aplicação em ambiente cloud, usando ferramentas como Terraform, Helm e Kubernetes.


## Funcionalidades

- **Construção da aplicação**: Gera a versão mais recente da aplicação.
- **Execução de testes**: Garante que as funcionalidades estão funcionando corretamente antes do deploy.
- **Deploy automatizado**: Implanta a aplicação no ambiente cloud.
- **Provisionamento de Infraestrutura automatizado**: Implanta a infraestrutura necessária para que a aplicacão funcione, como Kubernetes, Api Gateway, Lambda Functions e MongoDB. 

### Variáveis de Ambiente AWS

- **`AWS_ACCESS_KEY_ID`**: ID da chave de acesso programático da conta AWS, usado para autenticação ao provisionar recursos AWS.
- **`AWS_SECRET_ACCESS_KEY`**: Chave secreta vinculada ao `AWS_ACCESS_KEY_ID`, usada para autenticação segura com a AWS.
- **`AWS_SESSION_TOKEN`**: Token temporário de sessão usado para autenticação na AWS em cenários de acesso seguro (normalmente gerado ao usar funções IAM ou MFA).
- **`AWS_DEFAULT_REGION`**: Região AWS onde os serviços serão provisionados, como EC2, S3 e EKS (exemplo: `us-east-1`).

### Variáveis de Ambiente MongoDB Atlas

- **`MONGODBATLAS_ORG_PRIVATE_KEY`**: Chave privada da organização do MongoDB Atlas, usada para autenticação em APIs de gerenciamento de MongoDB Atlas.
- **`MONGODBATLAS_ORG_PUBLIC_KEY`**: Chave pública da organização do MongoDB Atlas, usada para autenticação em APIs de gerenciamento de MongoDB Atlas.
- **`ORG_ID`**: ID único da organização no MongoDB Atlas, usado para referenciar a organização nos scripts e automações.
- **`MONGO_HOST`**: Host (endereço) do cluster MongoDB que será provisionado, utilizado pela aplicação para se conectar ao banco de dados.

### Variáveis de Ambiente Docker

- **`DOCKER_USERNAME`**: Nome de usuário do Docker Hub, usado para autenticação ao fazer login e fazer push das imagens Docker.
- **`DOCKER_PASSWORD`**: Senha ou token de acesso do Docker Hub, usado em conjunto com o `DOCKER_USERNAME` para fazer login no Docker Hub.

### Variáveis de Ambiente JWT

- **`JWT_EXPIRES`**: Define o tempo de expiração dos tokens JWT usados pela aplicação para autenticação e autorização (geralmente em segundos).
- **`JWT_SECRET`**: Chave secreta usada para assinar e validar os tokens JWT gerados pela aplicação.

### Variáveis de Ambiente MongoDB para a Aplicação

- **`MONGODBATLAS_USERNAME`**: Nome de usuário root usado para acessar o cluster MongoDB Atlas, configurado para autenticação no banco de dados.
- **`MONGODBATLAS_PASSWORD`**: Senha associada ao `MONGODBATLAS_USERNAME`, usada para autenticação no MongoDB Atlas.
- **`MONGODB_USER`**: Nome de usuário do banco de dados MongoDB específico da aplicação, usado para acessar o banco de dados provisionado.
- **`MONGO_APP_DB`**: Nome do banco de dados dentro do MongoDB que a aplicação utilizará (exemplo: `snackbar`).

### Outras Variáveis de Ambiente

- **`SONAR_TOKEN`**: Token usado para autenticação no SonarQube, necessário para integrar e rodar análises de qualidade de código.
- **`BUCKET_S3`**: Nome do bucket S3 na AWS usado para salvar o tfstate usado no provisionamento da infraestrutura.


Certifique-se de que essas variáveis de ambiente estão configuradas corretamente para o funcionamento adequado da pipeline.

## Como Utilizar

Para executar a pipeline, você deve garantir que todos os pré-requisitos estão atendidos, como:
1. Credenciais AWS configuradas corretamente.
2. Credenciais MONGODB ATLAS configuradas corretamente.
3. As variáveis de ambiente mencionadas acima configuradas corretamente.

A pipeline irá rodar automaticamente em cada push ou merge nas branch main dos seguintes repositórios:
- https://github.com/fiap-9soat-snackbar/snackbar - repositório da aplicacão
- https://github.com/fiap-9soat-snackbar/snackbar-lambda - repositório de provisionamento lambda 
- https://github.com/fiap-9soat-snackbar/snackbar-database - repositório de provisionamento mongoDB Atlas.
- https://github.com/fiap-9soat-snackbar/eks - repositório de provisionamento Kubernetes, através do AWS EKS.
- https://github.com/fiap-9soat-snackbar/snackbar-api-gateway - repositório de provisionamento AWS API GATEWAY
