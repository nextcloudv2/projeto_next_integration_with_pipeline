# 🚀 Nextcloudv2 - AWS ECS Deployment

Este projeto é uma versão containerizada do Nextcloud, preparada para ser implantada em AWS ECS utilizando uma pipeline de CI/CD que envia as imagens para o ECR.

🛠️ Fluxo de Deploy

O deploy do projeto é feito em etapas, desde o desenvolvimento local até o deploy em produção na AWS:



# 💻 1. Desenvolvimento Local

Arquivos principais:

Dockerfile – define a imagem do Nextcloud.

compose.yml – orquestra os serviços para desenvolvimento local.

.env.example – arquivo de exemplo com variáveis de ambiente.

Teste local:

docker-compose -f compose.yml up

#  🏗️ 2. Construção e Versionamento da Imagem

O buildspec.yml define as etapas da pipeline:

Instalação de dependências.

Build da imagem Docker.

Login no AWS ECR.

Push da imagem para o repositório ECR.

Pipeline disparada por commits no repositório.

#  📦 3. Repositório no ECR

Imagens Docker são armazenadas no Amazon Elastic Container Registry (ECR).

Fluxo:

Pipeline faz login no ECR.

Tag da imagem baseada no commit ou branch.

Push da imagem para o repositório.

 #  🚢 4. Deploy no ECS

AWS ECS gerencia os containers:

Cluster ECS → hospeda os serviços.

Service → garante containers ativos.

Task Definition → especifica imagem, variáveis e rede.

Arquivos úteis:

ECS_DEPLOY.md – detalhes do deploy no ECS.

envio_ecr.sh – script de envio da imagem.

#  🗄️ 5. Banco de Dados

Integração com RDS (MySQL ou PostgreSQL):

RDS_SETUP.md → instruções de setup.

Variáveis de conexão no .env ou Secrets Manager.
 
#  💾 6. Backup e Restore

Scripts disponíveis:

backup_restore_exemplo.sh – exemplo de backup e restore do Nextcloud.

#  🔄 7. Fluxo Resumido da Pipeline

Commit no repositório → pipeline acionada.

Build da imagem Docker (Dockerfile).

Login no ECR e push da imagem.

ECS detecta nova imagem → atualiza serviço.

Novo container do Nextcloud iniciado com sucesso.
