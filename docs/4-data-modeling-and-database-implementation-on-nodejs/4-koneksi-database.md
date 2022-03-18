---
sidebar_position: 4
---

# 4. Database Connection

import useBaseUrl from '@docusaurus/useBaseUrl';

Pada tahap ini, kita akan mencoba menghubungkan database `PostgreSQL` dengan aplikasi web yang kita buat dengan `NodeJs`.

- Instal package `pg`, package ini akan membantu kita untuk melakukan koneksi, mengirim perintah/script, dan mengirim data ke database.

  ```shell
  npm i pg
  ```

- Buatlah sebuah folder dengan nama `connection` dan didalam folder tersebut buatlah sebuah file dengan nama `db.js`

  ```text {1-2}
  +-- connection
      +-- db.js
  +-- public
  +-- views
  +-- package-lock.json
  +-- package.json
  +-- index.js
  ```

- Kemudian tambahkan code berikut pada file `db.js`

  <a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day4-1.database-connection">
  Contoh code
  </a>

  <br />
  <br />

Buatlah kondisi jika sudah di deploy menggunakan koneksi yang isProduction, jika tidak menggunakan koneksi local 

  ```js title=db.js
  const { Pool } = require('pg')

  const isProduction = process.env.NODE_ENV === "production";
  let pool

  if (isProduction) {
    pool = new Pool({
        connectionString: process.env.DATABASE_URL,
        ssl: {
            rejectUnauthorized: false,
        },
    });
  } else {

    pool = new Pool({
        database: process.env.PG_DATABASE,
        port: process.env.PG_PORT,
        user: process.env.PG_USER,
        password: process.env.PG_PASSWORD
    })

  }
  module.exports = pool
  ```

  Pada code diatas, kita memanggil package `pg` dan melakukan konfigurasi untuk koneksi database.
