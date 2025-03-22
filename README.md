# McKing Database Versioning

Este repositório é responsável pelo **versionamento da base de dados** da aplicação McKing, utilizando **Liquibase** para gerenciar as mudanças estruturais de forma segura e automatizada.

## 📁 Estrutura
- `liquibase/changelog/db.changelog-master.xml`: Arquivo mestre que organiza e referencia todos os changelogs.
- `liquibase/changelog/V1__init.sql`: Script inicial contendo a estrutura base do banco.

---

## 🐳 Executando Liquibase com Docker (local)
Você pode rodar o Liquibase localmente via Docker, da seguinte forma:

```bash
docker run --rm \
  -v $(pwd)/liquibase/changelog:/liquibase/changelog \
  liquibase/liquibase \
  --url="jdbc:postgresql://<host>:5432/<nome_db>?user=<usuario>&password=<senha>" \
  --changeLogFile=changelog/db.changelog-master.xml \
  update
