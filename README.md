# Ambiente de estudos PHP com Docker Compose

Ambiente acadêmico para estudar aplicações PHP com Apache, MySQL e PostgreSQL. Inclui páginas de exemplo e ferramentas de administração dos bancos.

## Serviços configurados

| Serviço | Configuração no repositório | Acesso local |
| --- | --- | --- |
| PHP/Apache | Imagem construída em `php/Dockerfile` | http://localhost |
| MySQL | Imagem `mysql:5.7` | Porta 3306 |
| PostgreSQL | Imagem `postgres:12` | Porta 5432 |
| phpMyAdmin | Imagem construída em `phpmyadmin/` | http://localhost:8080 |
| pgAdmin | Imagem `dpage/pgadmin4` | http://localhost:8081 |

As versões acima descrevem o código atual. A imagem PHP utiliza a versão 7.4; atualizar dependências e validar compatibilidade é uma etapa futura, antes de considerar qualquer publicação.

## Estrutura

- `docker-compose.yaml`: serviços, rede e armazenamento.
- `php/Dockerfile`: PHP/Apache com extensões de acesso aos bancos.
- `phpmyadmin/Dockerfile`: imagem para administração do MySQL.
- `web/index.php`: exemplo de acesso ao MySQL e informações do ambiente.
- `web/pgsql.php`: página de exemplo para PostgreSQL.
- `web/config/`: conexões e funções auxiliares.
- `web/lamp-compose/`: cópia de arquivos de configuração existente no projeto, a revisar.

## Como iniciar para estudo local

Requisitos: Git, Docker e Docker Compose.

```bash
git clone https://github.com/rebecka-teodoro/lamp-compose.git
cd lamp-compose
docker compose up --build -d
docker compose ps
docker compose logs php mysql postgres
```

Consulte as páginas e portas da tabela acima. As consultas PHP dependem de que os bancos e tabelas esperados existam: a configuração Compose, por si só, não garante a criação de todo o esquema exigido pelas páginas.

Para parar os serviços:

```bash
docker compose down
```

O Compose utiliza diretórios locais `mysql/` e `postgres/` para os dados dos bancos. Não exclua esses diretórios se quiser preservar seus dados.

## Limites do ambiente

- Configuração destinada a estudo local, com credenciais de exemplo no Compose.
- Há portas de banco publicadas no host. Não exponha esse ambiente diretamente na internet.
- A página inicial chama `phpinfo()`, útil para estudo, mas inadequado para uma aplicação pública.
- A pasta `web/lamp-compose/` contém configuração duplicada que ainda precisa ser organizada.
- Esta revisão documentou os arquivos; não executou nem homologou os containers.

## Evolução sugerida

- Atualizar as imagens e validar as extensões necessárias.
- Documentar e versionar o esquema mínimo dos bancos.
- Separar configurações locais de produção.
- Organizar a duplicação de diretórios e incluir uma demonstração visual após validar a execução.
