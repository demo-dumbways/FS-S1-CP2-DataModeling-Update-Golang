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

  ```js title=db.js
  const { Pool } = require("pg");

  const pgUser = "ctukurnlfjbcbe";
  const pgPassword =
    "9ee6611f11cdd4c2721313d5c479fc4d88ca7aadaa448edf4e40dcea29c16eb9";
  const pgHost = "ec2-35-175-68-90.compute-1.amazonaws.com";
  const pgPort = 5432;
  const pgDatabase = ctukurnlfjbcbe;

  const connectionString = `postgres://${pgUser}:${pgPassword}@${pgHost}:${pgPort}/${pgDatabase}`;

  const pool = new Pool({
    connectionString: connectionString,
    ssl: {
      rejectUnauthorized: false,
    },
  });

  module.exports = pool;
  ```

  Pada code diatas, kita memanggil package `pg` dan melakukan konfigurasi untuk koneksi database.
