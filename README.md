# controle_estacionamento_Django
projeto de controle de estacionamento simples com endpoints em python e django








## Dados do docker

iniciar docker:
entre em ./data/

### instalação do conteiner

só na primeira vez para criar os conteiners

 - primeira vez , para instalar e baixar os pacotes necessarios:
```bash
sudo docker-compose run web django-admin startproject web_django .
```
 - para dar permissões dentro do diretorio do projeto
```bash
sudo chown -R $USER:$USER web_django
```



### inicialização dos conteiners

para depois que estiver instalado, é só iniciar que sobe tudo

 - para iniciar o docker:
```bash
docker-compose up
```

 - ou para iniciar com o console liberado
```bash
docker-compose up -d
```

 - para construir o conteiner
```bash
docker-compose build
```

 - para iniciar o projeto:
```bash
docker-compose run web python manage.py makemigrations
  docker-compose run web python manage.py migrate
```

## Credenciais de acesso do projeto

 - dados para usar o modelo deste projeto:
  - web_django: ports:  '8000:8000'
  - mysql: ports: '3306:3306'
  - MYSQL_DATABASE: 'db_django'
  - MYSQL_USER: 'root'
  - MYSQL_PASSWORD: 'password'
  - MYSQL_ROOT_PASSWORD: 'password'


## Configurações

### MYSQL




criando as tabelas

 - primeiro, criar a tabela do cliente
```sql
CREATE TABLE db_django.TB_CUSTOMER (
	ID INT auto_increment  NOT NULL PRIMARY KEY,
	NAME varchar(50) NULL
)
ENGINE=InnoDB
DEFAULT CHARSET=utf8
COLLATE=utf8_general_ci;
```


 - segundo, a criar a tabela do veiculo
```sql
CREATE TABLE db_django.TB_CUSTOMER_VEHICLES (
	ID INT auto_increment  NOT NULL PRIMARY KEY,
	PLATE varchar(10)  NULL,
	KIND INT  NULL,
	CONSTRAINT CUSTOMER_ID FOREIGN KEY (ID) REFERENCES db_django.TB_CUSTOMER(ID)
)
ENGINE=InnoDB
DEFAULT CHARSET=utf8
COLLATE=utf8_general_ci;
```

 - e por ultimo criar a tabela do registro do estacionamento
```sql
CREATE TABLE db_django.TB_PARKMOVEMENT (
	ID INT auto_increment NOT NULL PRIMARY KEY,
	ENTRY_DATE DATETIME NULL,
	EXIT_DATE DATETIME NULL,
	VALIDATE_DATE DATETIME NULL,
	VALUE REAL NULL,
	PLATE varchar(50) NULL,
	CONSTRAINT VEHICLE_ID FOREIGN KEY (ID) REFERENCES db_django.TB_CUSTOMER_VEHICLES(ID)
)
ENGINE=InnoDB
DEFAULT CHARSET=utf8
COLLATE=utf8_general_ci;
```


## API Django

### Rotas do endpoints

 - é necessário criar as Rotas:
  - customer
  - vehicle
  - movement
  - movement_exit




## Fontes de pesquisa:

 - https://dev.to/foadlind/dockerizing-a-django-mysql-project-g4m
 - https://medium.com/@minghz42/docker-setup-for-django-on-mysql-1f063c9d16a0
 - https://skonik.me/setup-django-with-mysql-using/
 - https://roytuts.com/docker-compose-dockerizing-django-mysql-app/
 - https://docs.docker.com/samples/django/

 - https://www.youtube.com/watch?v=qa7SWCozY_A&ab_channel=Maransatto
 - https://tech-pt.netlify.app/articles/pt519912/index.html
 - https://cursos.alura.com.br/forum/topico-error-ao-executar-docker-compose-run-web-python-manage-py-makemigrations-105642
 - https://groups.google.com/g/python-brasil/c/uKe2kvDOYZQ?pli=1
 - https://www.digitalocean.com/community/tutorials/how-to-scale-and-secure-a-django-application-with-docker-nginx-and-let-s-encrypt-pt
 - https://johnfercher.medium.com/mysql-docker-7ff6d50d6cf1
 - https://pt.stackoverflow.com/questions/532461/como-fazer-o-docker-compose-exportar-a-porta-do-postgres-para-o-host
 - https://fernandofreitasalves.com/criando-um-container-docker-para-um-projeto-django-existente/

 - https://stack.desenvolvedor.expert/appendix/docker/comandos.html
 - https://www.certificacaolinux.com.br/comandos-docker/
 - https://medium.com/xp-inc/principais-comandos-docker-f9b02e6944cd

 - https://www.codegrepper.com/code-examples/sql/dbeaver+mysql+set+primary+key
