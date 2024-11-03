# Trabalho Ambientes Operacionais

Este repositório contém a descrição e códigos necessários para o trabalho aplicado da disciplina de Ambientes Operacionais.

Utilize o ambiente do curso "AWS Academy Learner Lab" para fazer o trabalho. Nele você recebeu 50$ para uso livre da AWS.

Este ambiente persiste até o fechamento do curso.

## Objetivo

Aplicar os conhecimentos adquiridos na disciplina de Ambientes Operacionais, provisionando recursos na AWS dentro de uma VPC e suas subredes públicas e privadas e criando regras de segurança par acesso aos recursos.

## Trabalho Individual

Cada aluno deve realizar suas entregas individualmente.

## Entregas

Cada parte deverá ser feita até a data especificada no cronograma (ver plano de ensino no classroom).
Edite o documento word ( .doc ) usando o MsOffice ou Google Docs e adicione evidências da conclusão das atividades

Quando solicitado por um DIAGRAMA, utilize https://app.diagrams.net para fazer o desenho da arquitetura e a cada parte, atualize o diagrama com a evolução do projeto.
Exemplo: 
![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/DrawIO.png?raw=true)

Quando solicitado por EVIDÊNCIAS, tire prints do console da AWS demonstrando a criação e/ou funcionamento do que foi solicitado. 

## Parte 1 - INFRAESTRUTURA

> Este conteúdo foi visto no módulo 05 e praticada no LAB 02.

1. Criar uma VPC com as seguintes características:
   1.1. A VPC deve ter a máscara de sub rede /16 
   1.2. Utilizando duas zonas de disponibilidade diferentes. 
        1.2.1 Criar Duas subredes pública ( uma em cada zona de disponibilidade )
	    1.2.2 Criar Duas subredes privadas ( uma em cada zona de disponibilidade )
        1.2.3  Cada sub rede deve ter máscara /24
    1.3 A VPC deve conter um NAT Gateway
    1.4 A VPC deve conter um Internet Gateway

2.    Criar 2 grupos de segurança (SECURITY GROUPS) na VPC criada anteriormente:
    2.1. Nome: ec2-sg. Deve permitir a conexão SSH e conexão HTTP de qualquer local
    2.2. Nome: bd-sg. Deve permitir a conexão Mysql e PostgreSQL somente se originada desta vpc.

Entregas - Parte 1:
    Entrega 1. Diagrama detalhando sua estrutura. 
    Entrega 2. Evidências da criação da VPC conforme solicitação
    Entrega 3. Evidências da criação das Sub redes conforme solicitação
    Entrega 4. Evidências da criação dos Grupos de segurança conforme solicitação
    Entrega 5. Evidências da liberação das portas nos grupos de segurança conforme solicitação

## Parte 2 - CRIAÇÃO DOS RECURSOS

> Este conteúdo foi em diferentes módulos: 
>    A parte sobre máquinas EC2 foi vista no módulo 06 e praticada no LAB 03.
>    A parte sobre Buckets S3 foi vista no módulo 07 e praticada no LAB 04.
>    A parte sobreBancos RDS foi vista no módulo 08 e praticada no LAB 05.

1. Criar um Bucket S3 com as seguintes características:
    1.1. Escolha e anote o nome único definido para seu bucket.
    1.2. Bucket deve permitir acesso público
    1.3. Bucket deve ser configurado para hospedar um site estático

2. Criar uma instância EC2 com as seguintes características:
    2.1. Sistema Operacional Amazon Linux
    2.2. Tipo da instância T3.micro
    2.3. Ela deve ser colocada na subrede pública da VPC criada na atividade anterior
    2.4. Atribuia a criação de IP público ou associe um IP elástico à esta máquina.
    2.5. Associe-o ao grupo de segurança ec2-sg criado na atividade anterior

3. Crie um servidor de banco de dados RDS com as seguintes características:
    3.1. Tipo Cluster Aurora compatível com postgresql ( ou arrisque-se com mysql )
    3.1. Modelo DEV/Test
    3.1. Escola os tipos de instância mais baratos ( família T normalmente )
    3.1. Defina e anote as informações de conexão ( usuário e senha da instalação )
    3.1. Ela deve ser colocada na subrede privada da VPC criada na atividade anterior
    3.1. Associe-o ao grupo de segurança bd-sg criado na atividade anterior

Entregas - Parte 2:
    Entrega 1. Diagrama atualizado da estrutura. 
    Entrega 2. Evidências da criação do Bucket S3 conforme solicitação
    Entrega 3. Evidências da criação da máquina EC2 conforme solicitação
    Entrega 4. Evidências da criação do servidor RDS conforme solicitação




1. Criar uma VPC com as seguintes características:

    1.1. A VPC deve ter 1024 endereços de IPv4 disponíveis 

    1.2. Duas subredes públicas

    1.3. Duas subredes privadas.

    1.4. Cada subrede deve conter 27 endereços de IPv4 disponíveis
    
    1.5. Utilizar duas zonas de disponibilidade diferentes. Uma subrede pública e uma privada deve estar em cada zona de disponibilidade

    1.6 A VPC deve conter um NAT Gateway

    1.7 A VPC deve conter um Internet Gateway

    1.8 A VPC deve conter as tabelas de rotas e associações apropriadas para as subredes

2. Criar 2 grupos de segurança na VPC criada anteriormente:

    2.1. Nome: ec2-sg. Deve permitir a conexão SSH e conexão HTTP de qualquer local

    2.2. Nome: bd-sg. Deve permitir a conexão PostgreSQL somente para o grupo de segurança anterior
    
    
3. Criar um bucket S3 com as seguintes características:

    3.1. O bucket deve ser configurado permitir acesso público

    3.2 O bucket deve ser configurado para hospedar um site estático

    3.3 O bucket deve ter a seguinte política de segurança. Troque **NOME_BUCKET** pelo nome do seu bucket:

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::NOME_BUCKET/*"
            }
        ]
    }
    ```

    3.4 Coloque no bucket o conteúdo da pasta html deste repositório (https://github.com/fesousa/ambientes-operacionais-bd-trabalho/tree/main/html)

    3.5. Procure pelo endpoint de site do bucket e abra no seu navegador para testar. Você deve ver a seguinte tela:

    <img src="https://github.com/fesousa/ambientes-operacionais-bd-trabalho/raw/main/img/s3.png" />

    
4. Criar uma instância EC2 com seguintes características:

    4.1. Nome: flask-app

    4.2. Imagem: Amazon Linux

    4.3. Tipo de Instância: t2.micro

    4.4. Par de chaves: vockey

    4.4 Utilizar a VPC criada neste trabalho

    4.5 Colocar a instância em uma subrede pública

    4.6. Habilitar atribuição automática de IP Público

    4.7 Vincular o grupo de segurança ec2-sg

    4.8 Utilizar o seguinte código em user data (Dados do usuário):

    https://github.com/fesousa/ambientes-operacionais-bd-trabalho/blob/3822d09faca1f11c160cae658a951bd93673d66c/flask-ec2.sh#L1-L26


    Obs: Cuidado que ao copiar o código ele insere um espaço antes de cada comando, fazendo com que o ambiente não seja criado corretamente. Remova o espaço no início de cada comando, se houver.

5. Criar um grupo de sub-redes de banco de dados no RDS

    5.1. Deve estar na VPC criada neste projeto

    5.2. Deve conter apenas as subredes privadas da VPC

6. Criar um cluster RDS Aurora:

    6.1. Compatível com PostgreSQL

    6.2. Modelo de Dev/Test

    6.3. Defina um nome de usuário, senha e nome do banco de dados inicial. O Nome do banco de dados náo é o identificador. O nome do banco é configurado em configuração adicional.

    6.4. Escolha uma Classe de intância t (mais barata)

    6.5. Coloque o cluster RDS na VPC criada e na subnet privada

    6.6. Selecione o grupo de subredes criado anteriormente

    6.7. Associe o grupo de segurança bd-sg. Somente este grupo de segurança deve estar associado.

7. Para testar a solução:

    7.1. Procure pelo endpoint de site do bucket e abra no seu navegador

    7.2. Clique em configurações

    7.3. Configure os campos:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a. Endereço IPv4 público EC2: IP público da instãncia EC2 criada

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b. Host Banco de Dados: Endpoint do cluster RDS

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c. Banco de dados: nome do banco de dados criado (não é o identificador da instância)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;d. Usuário: usuário do banco de dados

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e. Senha: senha do banco de dados

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;f. Clique em Salvar

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;g. Clique em Voltar
    
&nbsp;&nbsp;&nbsp;&nbsp;7.4. Clique em SQL

&nbsp;&nbsp;&nbsp;&nbsp;7.5. Escreva comandos SQL do tipo `CREATE TABLE`, `INSERT` e `SELECT` para testar
