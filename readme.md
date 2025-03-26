# docker_postgres
projeto para criar um container docker usando postgres e colocar na sua rede para uso com qualquer outra aplicação se necessário para estudos pessoais e integrações em caso de desenvolvimento.

## arquitetura do projeto
```
|_envs
|__> postgres.env (environments)
|_data (persistencia: habilitar no arquivo docker-compose.yaml)
```

### persistencia
podemos habilitar 2 tipos de persistencia:
1. na pasta do projeto configurando o volume no docker-compose.yaml
2. internamente no docker

ambos vao deixar acessivel pela rede para outras aplicações interagirem

```
## dados de acesso

host: postgres
port: 5432

# usuario padrão
user: root
pass: root

# usuario admin
user: postgre
pass: root
```


### gerenciamento de container
acessar a pasta do projeto para rodar esses comandos

```Shell
# comando que executa o arquivo compose e remove orphans (limpeza na execução)
# a cada alteração no arquivo docker-compose.yaml, pode executar esse comando novamente
docker compose -f './docker-compose.yaml' up -d --build --remove-orphans

docker compose -f './docker-compose.yaml' down --remove-orphans

# outro comando "vagabundo"
alias docker-restart="docker compose -f './docker-compose.yaml' down && docker compose -f './docker-compose.yaml' up -d --build --remove-orphans"
```

### comandos importantes
```shell
# comando para remover redes nao usadas (limpeza de espaço em disco)
docker network prune --force

# comando para remover imagens não usadas
docker image prune --force

# comando para remover volumes não usados
docker volume prune --force

# comando "vagabundo" para executar tudo através de um alias (apelido)
alias docker-clean="docker network prune --force && docker image prune --force && docker volume prune --force"

# agora ja pode executar (temporariamente)
docker-clean
```