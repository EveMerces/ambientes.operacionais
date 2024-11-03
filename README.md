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

Exemplo:

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/VPC.png)

-----

## Parte 1 - INFRAESTRUTURA

>Este conteúdo foi visto no módulo 05 e praticada no LAB 02.

1. Criar uma VPC com as seguintes características:

   1.1. A VPC deve ter a máscara de sub rede /16 

   1.2. Utilizando duas zonas de disponibilidade diferentes. 

	1.2.1 Criar Duas subredes pública ( uma em cada zona de disponibilidade )

   	1.2.2 Criar Duas subredes privadas ( uma em cada zona de disponibilidade )
   
   	1.2.3  Cada sub rede deve ter máscara /24

    1.3 A VPC deve conter um NAT Gateway

    1.4 A VPC deve conter um Internet Gateway

2. Criar 2 grupos de segurança (SECURITY GROUPS) na VPC criada anteriormente:

    2.1. Nome: ec2-sg. Deve permitir a conexão SSH e conexão HTTP de qualquer local
 
    2.2. Nome: bd-sg. Deve permitir a conexão Mysql e PostgreSQL somente se originada desta vpc.

Entregas - Parte 1:
    
    Entrega 1. Diagrama detalhando sua estrutura. 
    
    Entrega 2. Evidências da criação da VPC conforme solicitação
    
    Entrega 3. Evidências da criação das Sub redes conforme solicitação
    
    Entrega 4. Evidências da criação dos Grupos de segurança conforme solicitação

    Entrega 5. Evidências da liberação das portas nos grupos de segurança conforme solicitação

-----

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

    2.3. Par de chaves vockey

    2.4. Ela deve ser colocada na subrede pública da VPC criada na atividade anterior

    2.5. Atribuia a criação de IP público ou associe um IP elástico à esta máquina.

    2.6. Associe-o ao grupo de segurança ec2-sg criado na atividade anterior

4. Crie um servidor de banco de dados RDS com as seguintes características:

    3.1. Tipo Cluster Aurora compatível com postgresql ( ou arrisque-se com mysql )

    3.2. Modelo DEV/Test

    3.3. Escola os tipos de instância mais baratos ( família T normalmente )

    3.4. Defina e anote as informações de conexão ( usuário e senha da instalação )

    3.5. Ela deve ser colocada na subrede privada da VPC criada na atividade anterior

    3.6. Associe-o ao grupo de segurança bd-sg criado na atividade anterior

Entregas - Parte 2:
    
    Entrega 1. Diagrama atualizado da estrutura. 
    
    Entrega 2. Evidências da criação do Bucket S3 conforme solicitação
    
    Entrega 3. Evidências da criação da máquina EC2 conforme solicitação

    Entrega 4. Evidências da criação do servidor RDS conforme solicitação

-----

## Parte 3 - IMPLEMENTAÇÃO DA SOLUÇÃO

> Concluindo as configurações do Bucket S3

1. Edite seu Bucket S3 e em Permissões adicione a seguinte política do bucket:

Troque **NOME_BUCKET** pelo nome do seu bucket:


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

2. Coloque no bucket o conteúdo da pasta html deste repositório (https://github.com/gbmaia/ambientes.operacionais/tree/main/html)

3. Procure pelo endpoint de site do bucket e abra no seu navegador para testar. Você deve ver a seguinte tela:

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/website.png)

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/s3.png)

-----

> Concluindo as configurações do Bucket EC2

-----

4. Conecte-se na Instância EC2 usando o menu padrão de conexão da AWS.

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/ec2connect.png)

5. No console copie e cole sem formatação o seguinte código:

https://github.com/gbmaia/ambientes.operacionais/blob/15b2aabce22043e47ec2903bb56d8b264f8279b3/flask-ec2.sh#L1-L26

Exemplo:

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/ec2.png)

Detalhe: Esta ação poderia ter sido otimizada ao incluir este mesmo código em "Dados de Usuário" na criação da máquina EC2.

-----

> Concluindo as configurações do Solução

-----

6. Acesse o endpoint coletado anteriormente ( item 3 ), depois clique em CONFIGURAÇÕES

    6.1. Inclua seus dados de configuração:

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/configuracao.png)

-----

> Testando a Solução

-----

7. Clique em VOLTAR ou Acesse novamente o endpoint coletado anteriormente ( item 3 ), depois clique em SQL

    7.1. Inclua um código SQL que será executado em seu servidor RDS e depois clique em EXECUTAR:

![alt text](https://github.com/gbmaia/ambientes.operacionais/blob/main/img/testes.png)


Entregas - Parte 3:
    
    Entrega 1. Diagrama atualizado da estrutura. 
    
    Entrega 2. Evidências da edição do Bucket S3 e a inclusão das políticas do Bucket
    
    Entrega 3. Evidências da instalação/execução na máquina EC2 do código solicitado

    Entrega 4. Evidências da execução de um código SQL qualquer na tela final da solução.

-----

## Parte 4 - CONCLUSÃO

Opcionalmente, utilize um pgadmin ou DBeaver para se conctar em seu banco RDS e confirmar a execução do código.

Não se esqueça de realizar todas as entregas nos prazos propostos e de dar um feedback ao professor sobre a atividade.
