---
sidebar_position: 1
---

# 1. Insert Data

import useBaseUrl from '@docusaurus/useBaseUrl';

Kita akan mencoba memasukkan data ke dalam tabel, agar data tersebut dapat tersimpan dengan baik.

## 1.1 Tabel User

- `Klik kanan` pada tabel `user`, kemudian pilih `Scripts` → `INSERT Script`

  <img alt="image424" src={useBaseUrl('img/docs/image-4-24.png')} max="70%"/>

- Maka kita akan melihat script untuk memasukkan data ke tabel `user`

  <img alt="image425" src={useBaseUrl('img/docs/image-4-25.png')} max="70%"/>

- Kita menghilangkan `id` pada script karena data `id` secara otomatis akan dibuatkan oleh postgreSQL dan `Auto Increment` agar tidak ada `id` yang sama, kemudian setelah script `VALUES` kita ketik data yang ingin kita masukkan ke dalam tabel tersebut.

  <img alt="image426" src={useBaseUrl('img/docs/image-4-26.png')} max="70%"/>

- Untuk `menjalankan/execute` script kita harus klik sebuah tombol disebelah atas

  <img alt="image431" src={useBaseUrl('img/docs/image-4-31.png')} max="70%"/>

## 1.2 Tabel Blog

- `Klik kanan` pada tabel `blog`, kemudian pilih `Scripts` → `INSERT Script`

  <img alt="image427" src={useBaseUrl('img/docs/image-4-27.png')} max="70%"/>

- Maka kita akan melihat script untuk memasukkan data ke tabel `blog`

  <img alt="image428" src={useBaseUrl('img/docs/image-4-28.png')} max="70%"/>

- Kita menghilangkan `id`, `author_id` karena kita belum membuat relasi ke tabel `user`, `post_data` karena kita sudah mengatur nilai `Default`. Kemudian setelah script `VALUES` kita ketik data yang ingin kita masukkan ke dalam tabel tersebut.

  <img alt="image429" src={useBaseUrl('img/docs/image-4-29.png')} max="70%"/>

- Untuk `menjalankan/execute` script kita harus klik sebuah tombol disebelah atas

  <img alt="image430" src={useBaseUrl('img/docs/image-4-30.png')} max="70%"/>
