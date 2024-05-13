# Backup e restore postgres com zstd

### Executar dump com zstd
```bash

DATE="$(date "+%Y-%m-%d_%H-%M")"
DATABASE="banco"
DUMP_NAME="/tmp/${DATABASE}_${DATE}.sql"

pg_dump -U postgres -C "${DATABASE}" | zstd --rm -o "${DUMP_NAME}.zst"
```

### Restaurar dump compactado com zstd
```bash
zstd -cdk --no-progress arquivo_dump.sql.zst | psql -U postgres -W -h localhost postgres
```