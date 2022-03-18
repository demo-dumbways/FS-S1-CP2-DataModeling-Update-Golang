---
sidebar_position: 3
---

# 3. Creating User Table

import useBaseUrl from '@docusaurus/useBaseUrl';

Kali ini kita akan mulai membuat tabel `user`, sesuai dengan desain database pada tahap sebelumnya.

<img alt="image47" src={useBaseUrl('img/docs/image-4-8.png')} max="50%"/>

- Didalam database `personal-web`, klik `Schemas` → `public`.

  <img alt="image47" src={useBaseUrl('img/docs/image-4-9.png')} max="70%"/>

- Kemudian klik kanan pada `Tables` → `Create` → `Table...`

  <img alt="image47" src={useBaseUrl('img/docs/image-4-10.png')} max="70%"/>

- Pada menu `General`, silahkan isi nama tabel, yaitu `tb_user`.

  <img alt="image47" src={useBaseUrl('img/docs/image-4-11.png')} max="70%"/>

- Pada menu `Columns`, silahkan tambahkan columns/fields pada tabel `user` dengan cara menekan tanda `+`. Kemudian isi sesuai dengan kebutuhan tabel, sebagai berikut:

  - **id** → `Data type: serial`, `Not NULL: True`, `Primary key: True`
  - **name** → `Data type: character varying`, `Length: 255`, `Not NULL: True`
  - **email** → `Data type: character varying`, `Length: 255`, `Not NULL: True`
  - **password** → `Data type: character varying`, `Length: 255`, `Not NULL: True`

  <img alt="image47" src={useBaseUrl('img/docs/image-4-12.png')} max="70%"/>

  Kemudian klik `Save`.

- Kita telah berhasil membuat tabel `user`.

  <img alt="image47" src={useBaseUrl('img/docs/image-4-13.png')} max="70%"/>
