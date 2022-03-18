---
sidebar_position: 5
---

# 5. Fetch Data Table

import useBaseUrl from '@docusaurus/useBaseUrl';

Pada tahap ini, kita akan mencoba menampilkan seluruh data dari tabel `blog`.

Tambahkan code berikut pada file index.js (root)

## Mengambil koneksi database

```js
const db = require('../connection/db');
```

## Mengambil data dan mengirim data ke file Handlebars

Hal pertama yang perlu dilakukan untuk fetching data dari database adalah melakukan koneksi ke database, kemudian kita mengeksekusi script `SELECT * FROM tb_blog` untuk mengambil data dari database. Data yang dikembalikan oleh script tersebut akan tersimpan didalam parameter `result` dan kita simpan kedalam variable `data`. Kemudian kita melakukan manipulasi property pada object data blog, yaitu menambahkan `post_at`, `post_age`, dan `isLogin`.

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/blob/day4-2.fetch-data/api/index.js">
Contoh code
</a>

<br />
<br />

```js title=index.js {8-37}
app.get('/home', function (req, res) {
    setHeader(res)
    res.render('index')
})

const isLogin = true

app.get('/blog', function (req, res) {
    setHeader(res)

    db.connect((err, client, done) => {
        if (err) throw err

        client.query('SELECT * FROM tb_blog', (err, result) => {
            done()
            if (err) throw

            let data = result.rows

            data = data.map((blog) => {
                return {
                    ...blog,
                    post_at: getFullTime(blog.post_at),
                    post_age: getDistanceTime(blog.post_at),
                    isLogin: isLogin
                }
            })

            res.render(
                'blog',
                {
                    isLogin: isLogin,
                    blogs: data
                })
        })
    })
})

app.get('/blog/:id', function (req, res) {
    const blogId = req.params.id
    const blog = blogs.find((item) => item.id == blogId);
    setHeader(res)
    res.render('blog-detail', { blog });
})
```

## Menampilkan data

Tambahkan code berikut pada bagian daftar blog pada halaman `blog`

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/blob/day4-2.fetch-data/views/blog.hbs">
Contoh code
</a>

<br />
<br />

```html {2,8,15,18,20,22} title=blog.hbs
<div id="contents" class="blog-list">
  {{#each blogs}}
  <div class="blog-list-item">
    <div class="blog-image">
      <img src="/public/assets/blog-img.png" alt="" />
    </div>
    <div class="blog-content">
      {{#if this.isLogin}}
      <div class="btn-group">
        <a class="btn-edit" href="/">Edit Post</a>
        <a href="/delete-blog/{{this.id}}" class="btn-delete">Delete Blog</a>
      </div>
      {{/if}}
      <h1>
        <a href="/detail-blog/{{this.id}}" target="_blank">{{this.title}}</a>
      </h1>
      <div class="detail-blog-content">{{this.post_at}} | {{this.author}}</div>
      <p>{{this.content}}</p>
      <div style="text-align: right">
        <span style="font-size: 15px; color: grey">{{post_age}}</span>
      </div>
    </div>
  </div>
  {{/each}}
</div>
```

<img alt="image1" src={useBaseUrl('img/docs/image-5-1.png')} height="350px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://personal-web-chapter-2.herokuapp.com/blog">
Demo
</a>
</div>
