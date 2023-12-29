# PROVISIONAMENTO DE AMBIENTE COM PHP, POSTGRES E REDIS

## UTILIZAÇÃO

Fazer uma cópia do arquivo ```.env.exemplo``` para ```.env``` e editar. **Não funcionará sem esse arquivo.**

### Comando para iniciar os containeres:

```bash
$ docker compose up -d
```

**Caso alguma dessas portas: 80, 443, 6379, esteja sendo utilizada no host, o arquivo ```.env``` deverá ser editado.**

### Comando para parar os containeres:

```bash
$ docker compose down
```

**Caso sejam feitas alterações nas configurações das imagens, ou seja, em qualquer arquivo da pasta docker, as imagens precisam ser reconstruídas:**

```bash
$ docker compose up --build
```

Esse último procedimento pode demorar mas não precissa ser realizado com frequência.

### Comando para acesssar o shell dos containeres

```bash
# bash em app (php)
$ docker compose exec app "/bin/bash"

# bash em db
$ docker compose exec db "/bin/bash"

# bash em redis
$ docker compose exec redis "/bin/bash"
```

### Comando para acessar o prompt de comando psql em db

```bash
#      app: é o nome do usuário que consta em .env
# postgres: é o nome do banco de dados que será conectado
$ docker compose exec db psql -U app postgres
```

## PHP

O arquivo ```Dockerfile``` apresenta as principais configurações como ```php.ini``` de *dev.* e *prod.*, ```conf.d``` (*php*) e módulos.

Para tornar o módulo disponível no ambiente, basta descomentar a linha com o comando ```RUN``` dentro do arquivo ```Dockerfile```.

O arquivo ```php.ini``` pode ser personalizado para o ambiente de desenvolvimento e de produção. O objetivo é saber as configurações que foram feitas no ```php.ini``` ao longo do projeto.

Também é possível carregar informações de configuração do *php* através de arquivos ```.ini``` dentro da pasta ```conf.d```.

Os arquivos de configurações básicas de *virtualhost* do *Apache* estão na pasta ```vhosts```. As chaves *SSL* do *vhost* são criadas durante a *build* da imagem.

Nas configurações da imagem de desenvolvimento foi consta a instalação do *Composer*, *Node* e *Yarn*.

## POSTGRESQL

O arquivo ```Dockerfile``` apresenta a instalação padrão da última versão do Postgresql.

Está disponível, através da remoção de comentários no arquivo ```Dockerfile``` a possibilidade de instalação de dois módulo do *Postgresql*: *Postgis* e *FDW*.

Na pasta ```arquivos``` existe o exemplo de arquivos com comandos para criação e manipulação de bancos de dados na imagem.

## REDIS

O arquivo ```Dockerfile``` apresenta a instalação padrão da última versão do Redis.

O arquivo de configuração está disponível para ajustes.

