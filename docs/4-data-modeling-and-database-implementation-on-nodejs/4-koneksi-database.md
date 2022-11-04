---
sidebar_position: 4
---

# 4. Database Connection

import useBaseUrl from '@docusaurus/useBaseUrl';

Pada tahap ini, kita akan mencoba menghubungkan database `PostgreSQL` dengan aplikasi web yang kita buat dengan `Golang`.

- Instal package `pgx`, package ini akan membantu kita untuk melakukan koneksi, mengirim perintah/script, dan mengirim data ke database.

  ```shell
 go get -u github.com/jackc/pgx/v4
  ```

- Buatlah sebuah folder dengan nama `connection` dan didalam folder tersebut buatlah sebuah file dengan nama `db.js`

  ```text {1-2}
  +-- connection
      +-- postgre.go
  +-- public
  +-- views
  +-- go.mod
  +-- go.sum
  +-- main.go
  ```

- Kemudian tambahkan code berikut pada file `postgre.go`

  <a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day4-1-database-connection/connection/postgre.go">
  Contoh code
  </a>

  <br />
  <br /> 

```go title="postgre.go"
  package connection

  import (
    "context"
    "fmt"
    "os"

    "github.com/jackc/pgx/v4"
  )

  var Conn *pgx.Conn

  func DatabaseConnect() {
    var err error
    databaseUrl := "postgres://postgres:root@localhost:5432/db_blog"
    Conn, err = pgx.Connect(context.Background(), databaseUrl)
    if err != nil {
      fmt.Fprintf(os.Stderr, "Unable to connect to database: %v\n", err)
      os.Exit(1)
    }
    fmt.Println("Success connect to database")

  }
```

  Pada code diatas, kita memanggil package `pgx` dan melakukan konfigurasi untuk koneksi database.
