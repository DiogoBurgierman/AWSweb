# Servidor Web AWS EC2 com RDS MariaDB

## Visão Geral

Esta solução configura um servidor web na AWS EC2 usando Amazon Linux, que se conecta a uma instância RDS MariaDB. O servidor executa uma aplicação PHP que interage com um banco de dados MariaDB para gerenciar dados de funcionários.

## Componentes

- **AWS EC2**: Servidor virtual executando Amazon Linux.
- **AWS RDS MariaDB**: Serviço gerenciado de banco de dados para MariaDB.
- **Aplicação PHP**: Script PHP simples para interagir com o banco de dados.

## Pré-requisitos

1. **Conta AWS**: Certifique-se de ter uma conta AWS.
2. **Instância EC2**: Lance uma instância Amazon Linux EC2.
3. **Instância RDS MariaDB**: Configure uma instância MariaDB no RDS.

## Instruções de Configuração

### 1. Configurar Instância EC2

1. Lance uma instância Amazon Linux EC2.
2. Acesse sua instância EC2 via SSH.
3. Atualize o sistema e instale os pacotes necessários:

    ```bash
    sudo yum update -y
    sudo yum install -y httpd php php-mysqlnd
    ```

4. Inicie e habilite o Apache:

    ```bash
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```

### 2. Configurar RDS MariaDB

1. Crie uma instância RDS MariaDB através do Console de Gerenciamento da AWS.
2. Anote o endpoint, nome de usuário e senha da sua instância RDS.

### 3. Configurar Conexão com o Banco de Dados

1. Na sua instância EC2, crie um diretório para sua aplicação web:

    ```bash
    sudo mkdir -p /var/www/html/myapp
    ```

2. Crie o arquivo `dbinfo.inc` com suas credenciais RDS em `/var/www/html/myapp/inc/dbinfo.inc`:

    ```php
    <?php
    define('DB_SERVER', 'seu-endpoint-rds');
    define('DB_USERNAME', 'seu-usuario');
    define('DB_PASSWORD', 'sua-senha');
    define('DB_DATABASE', 'nome-do-seu-banco-de-dados');
    ?>
    ```

3. Coloque o script PHP no diretório `/var/www/html/myapp`.

### 4. Atualizar Script PHP

1. Salve o código PHP fornecido como `index.php` em `/var/www/html/myapp`.

### 5. Configurar Grupos de Segurança

1. Certifique-se de que o grupo de segurança da sua instância EC2 permita tráfego HTTP (porta 80) e HTTPS (porta 443) de entrada.
2. Certifique-se de que o grupo de segurança da sua instância RDS permita tráfego de entrada da instância EC2 na porta do MySQL (3306).

### 6. Acessar a Aplicação

1. Abra um navegador web e acesse o endereço IP público da sua instância EC2. Você deverá ver a aplicação web em execução.

## Uso

- **Adicionar Funcionário**: Use o formulário de entrada para adicionar dados de funcionários ao banco de dados.
- **Ver Funcionários**: A tabela abaixo do formulário exibe a lista atual de funcionários do banco de dados.

## Solução de Problemas

- **Erros de Conexão**: Verifique o endpoint, nome de usuário e senha do RDS em `dbinfo.inc`.
- **Problemas com o Banco de Dados**: Certifique-se de que a instância MariaDB seja acessível a partir da sua instância EC2 e que os grupos de segurança estejam configurados corretamente.

## Acesso às tecnologias utilizadas

- [AWS EC2](https://aws.amazon.com/ec2/)
- [AWS RDS MariaDB](https://aws.amazon.com/rds/mariadb/)
- [PHP](https://www.php.net/)
