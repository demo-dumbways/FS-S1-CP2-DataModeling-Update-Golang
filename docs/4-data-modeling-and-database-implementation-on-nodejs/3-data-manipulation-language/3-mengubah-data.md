---
sidebar_position: 3
---

# 3. Update Data Table

import useBaseUrl from '@docusaurus/useBaseUrl';

Pada tahap ini kita akan mencoba untuk mengubah data yang ada didalam tabel.

## 3.1 Tabel User

- `Klik kanan` pada tabel `user`, kemudian pilih `Scripts` → `UPDATE Script`

  <img alt="image438" src={useBaseUrl('img/docs/image-4-38.png')} max="70%"/>

- Maka kita akan melihat script untuk mengubah data tabel `user`

  <img alt="image439" src={useBaseUrl('img/docs/image-4-39.png')} max="70%"/>

- Misalnya kita ingin mengubah nama user yang sebelumnya `John Doe` menjadi `Leon Doe`, maka kita tinggal menambahkan script setelah `SET` yaitu `SET name = 'Leon Doe'`, dan jangan lupa untuk mengatur data mana yang ingin kita ganti dengan menambahkan `id` setelah `WHERE`, contohnya `WHERE id = 1`. Untuk `menjalankan/execute` script, kita harus klik sebuah tombol disebelah atas, dan kita akan mendapatkan data dari tabel `user`

  <img alt="image440" src={useBaseUrl('img/docs/image-4-40.png')} max="70%"/>

## 3.2 Tabel Blog

- `Klik kanan` pada tabel `blog`, kemudian pilih `Scripts` → `UPDATE Script`

  <img alt="image441" src={useBaseUrl('img/docs/image-4-41.png')} max="70%"/>

- Maka kita akan melihat script untuk mengubah data tabel `blog`

  <img alt="image442" src={useBaseUrl('img/docs/image-4-42.png')} max="70%"/>

- Misalnya kita ingin mengubah title blog yang sebelumnya `Apa itu Teknologi 5G` menjadi `Perkembangan Teknologi Internet`, maka kita tinggal menambahkan script setelah `SET` yaitu `SET title = 'Perkembangan Teknologi Internet'`, dan jangan lupa untuk mengatur data mana yang ingin kita ganti dengan menambahkan `id` setelah `WHERE`, contohnya `WHERE id = 1`. Untuk `menjalankan/execute` script, kita harus klik sebuah tombol disebelah atas, dan kita akan mendapatkan data dari tabel `user`

  <img alt="image443" src={useBaseUrl('img/docs/image-4-43.png')} max="70%"/>
