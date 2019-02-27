### sql-migrate
---
https://github.com/rubenv/sql-migrate

```go
import "github.com/rubenv/sql-migtate"

migrations := &migrate.MemoryMigrationSource{
  Migrations: []*migrate.Migration{
    &migrate.Migration{
      Id: "123",
      Up: []string{"CREATE TABLE people (id int)"},
      Down: []string{"DROP TABLE people"},
    },
  },
}

migrations := &migrate.FileMigrationSource{
  Dir: "db/migrations",
}

migrations := &migrate.PackrMigrationSource{
  Box: packr.NewBox("./migrations"),
}

migrations := &migrate.AssetMigrationSource{
  Asset: Asset,
  AssetDir: AssetDir,
  Dir: "migrations",
}

db, err := sql.Open("sqlite3", filename)
if err != nil {
}
n, err := migrate.Exec(db, "sqlite3", migrations, migrate.Up)
if err != nil {
}
fmt.Printf("Applied %d migrations!\n", n)

migrations := &migrate.PackrMigrationSource{
  Box: packr.NewBox("./migrations"),
}

migrations := &migrate.PackrMigrationSource{
  Box: myBox,
  Dir: "./migrations",
}

migrations := &migrate.AssetMigrationSource{
  Asset: Asset,
  AssetDir: AssetDir,
  Dir: "db/migrations",
}

type MigrationSource interface {
  FindMigrations() ([]*Migration, error)
}

n, err := migrate.Exec(db.DB, "sqlite3", migrations, migrate.Up)

if err != nil {
}
```

```
go get -v github.com/rubyenv/sql-migrate/...
sql-migrate --help

sql-migrate up --help
sql-migrate status

go-bindata -pkg myapp -o bindata.go db/migrations/
```

```yml
development:
  dailect: sqlite3
  datasource: test.db
  dir: migrations/sqlite3
  
production: 
  dialect: postgres
  datasource: dbname=myapp sslmode=disable
  dir: migrations/postgres
  table: migrations

production:
  dialect: mysql
  datasource: root@/dbname?parseTime=true
  dir: migrations/mysql
  table: migrations
```

```sql
CREATE TABLE people (id int);

DROP TABLE people;

CREATE TABLE people (id int);

CREATE OR REPLACE FUNCTION do_something()
returns void AS $$
DECLARE
  create_query text;
BEGIN
END;
$$
language plpgsql;

DROP FUNCTION do_something();
DROP TABLE people;

CREATE UNIQUE INDEX people_unique_id_ids CONCURRENTLY ON people (id);

DROP INDEX people_unique_id_idx;
```

