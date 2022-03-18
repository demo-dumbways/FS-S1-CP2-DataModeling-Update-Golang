---
sidebar_position: 4
---

# 4. Creating Blog Table

import useBaseUrl from '@docusaurus/useBaseUrl';

Jika sebelumnya kita telah membuat tabel `user`, kali ini kita akan melanjutkan membuat tabel `blog`.

<img alt="image414" src={useBaseUrl('img/docs/image-4-14.png')} max="50%"/>

- Klik kanan pada `Tables` → `Create` → `Table...`

  <img alt="image415" src={useBaseUrl('img/docs/image-4-15.png')} max="70%"/>

- Pada menu `General`, silahkan isi nama tabel, yaitu `tb_blog`.

  <img alt="image416" src={useBaseUrl('img/docs/image-4-16.png')} max="70%"/>

- Pada menu `Columns`, silahkan tambahkan columns/fields pada tabel `blog` dengan cara menekan tanda `+`. Kemudian isi sesuai dengan kebutuhan tabel, sebagai berikut:

  - **id** → `Data type: serial`, `Not NULL: True`, `Primary key: True`
  - **author_id** → `Data type: integer`
  - **title** → `Data type: character varying`, `Length: 255`, `Not NULL: True`
  - **image** → `Data type: character varying`, `Length: 255`, `Not NULL: True`
  - **content** → `Data type: text`, `Not NULL: True`
  - **post_data** → `Data type: timestamp with time zone`, `Not NULL: True`, `Default: now()`

  <img alt="image417" src={useBaseUrl('img/docs/image-4-17.png')} max="70%"/>

  Kemudian klik `Save`.

- Kita telah berhasil membuat tabel `blog`.

  <img alt="image418" src={useBaseUrl('img/docs/image-4-18.png')} max="70%"/>
