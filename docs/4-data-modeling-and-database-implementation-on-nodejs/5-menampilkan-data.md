---
sidebar_position: 5
---

# 5. Fetch Data Table

import useBaseUrl from '@docusaurus/useBaseUrl';

Pada tahap ini, kita akan mencoba menampilkan seluruh data dari tabel `blog`.

Tambahkan code berikut pada file main.go (root)

## Mengambil koneksi database
Hal pertama yang perlu dilakukan untuk fetching data dari database adalah melakukan koneksi ke database

```go {6} title="main.go"
// continuation this code same like before

func main() {
	route := mux.NewRouter()

	connection.DatabaseConnect()

	// static folder
	route.PathPrefix("/public/").Handler(http.StripPrefix("/public/", http.FileServer(http.Dir("./public/"))))

	// routing
	route.HandleFunc("/", helloWorld).Methods("GET")
	route.HandleFunc("/home", home).Methods("GET").Name("home")
	route.HandleFunc("/blog", blogs).Methods("GET")
	route.HandleFunc("/blog/{id}", blogDetail).Methods("GET")
	route.HandleFunc("/add-blog", formBlog).Methods("GET")
	route.HandleFunc("/blog", addBlog).Methods("POST")
	route.HandleFunc("/delete-blog/{id}", deleteBlog).Methods("GET")
	route.HandleFunc("/contact-me", contactMe).Methods("GET")

	fmt.Println("Server running on port 5000")
	http.ListenAndServe("localhost:5000", route)
}

// continuation this code same like before
```

## Mengambil data dan mengirim data ke file Handlebars

Kemudian kita mengeksekusi script `SELECT * FROM tb_blog` untuk mengambil data dari database. Data yang dikembalikan oleh script tersebut akan tersimpan didalam parameter `rows` dan kita simpan kedalam variable `Blog`. 

Pertama kita harus membuat sebuahn struct yang nantinya akan menyimpan seluruh data blog yang kita dapatkan dari database

<br />

```go {4-12} title="main.go"
// continuation this code same like before
// this code below var Data = map[string]interface{}{

type Blog struct {
	Id          int
	Title       string
	Image       string
	Post_date   time.Time
	Format_date string
	Author      string
	Content     string
}

// continuation this code same like before
```

selanjutnya kita mulai melakukan fetching data dari database dan kemua kita melakukan manipulasi property pada object data blog, yaitu menambahkan data `post_date` dan `author` yang tidak kita dapatkan dari database.

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day4-2-fetch-data-table/main.go">
Contoh code
</a>

<br />
<br />

```go {14-35} title="main.go"
// continuation this code same like before
// this code below func home(w http.ResponseWriter, r *http.Request) {

func blogs(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")

	var tmpl, err = template.ParseFiles("views/blog.html")
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte("message : " + err.Error()))
		return
	}

	rows, _ := connection.Conn.Query(context.Background(), "SELECT id, title, image, content, post_date FROM tb_blog ORDER BY id DESC")

	var result []Blog
	for rows.Next() {
		var each = Blog{}

		var err = rows.Scan(&each.Id, &each.Title, &each.Image, &each.Content, &each.Post_date)
		if err != nil {
			fmt.Println(err.Error())
			return
		}

		each.Author = "Ilham Fathullah"
		each.Format_date = each.Post_date.Format("2 January 2006")

		result = append(result, each)
	}

	respData := map[string]interface{}{
		"Data":  Data,
		"Blogs": result,
	}

	w.WriteHeader(http.StatusOK)
	tmpl.Execute(w, respData)
}

// continuation this code same like before
```

## Menampilkan data

Tambahkan code berikut pada bagian daftar blog pada halaman `blog`

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day4-2-fetch-data-table/views/blog.html">
Contoh code
</a>

<br />
<br />

```html {3,40,44,46,55,60,62,65,67,70} title="blog.html"
<html>
  <head>
    <title>{{.Data.Title}}</title>
    <link rel="stylesheet" href="/public/style.css" />
    <!-- linking boostrap css cdn  -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3"
      crossorigin="anonymous"
    />
  </head>

  <body>
    <!-- NavBar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-lg">
        <a class="navbar-brand me-5" href="/home">
          <img src="/public/assets/logo.png" alt="logo" />
        </a>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" href="/home">Home</a>
            </li>
            <li class="nav-item">
              <a href="/blog" class="nav-link list-active">Blog</a>
            </li>
          </ul>
        </div>
        <div class="d-flex contact-me">
          <a href="/contact-me"> Contact Me </a>
        </div>
      </div>
    </nav>

    <!-- Blog list -->
    <div id="contents" class="blog-list">
      <!-- conditional post blog -->
      {{if .Data.IsLogin}}
      <div class="button-group w-100">
        <a href="/add-blog" class="btn-post">Add New Blog</a>
      </div>
      {{end}}
      <!-- dynamic content would be here -->
      {{range $index, $data := .Blogs}}
      <div class="blog-list-item">
        <div class="blog-image">
          <img
            src="/public/assets/blog-img.png"
            alt="Pasar Coding di Indonesia Dinilai Masih Menjanjikan"
          />
        </div>
        <div class="blog-content">
          {{if $.Data.IsLogin}}
          <div class="button-group">
            <a class="btn-edit">Edit Post</a>
            <a class="btn-post" href="/delete-blog/{{$index}}">Delete Blog</a>
          </div>
          {{end}}
          <h1>
            <a href="/blog/{{$index}}" target="_blank"> {{$data.Title}} </a>
          </h1>
          <div class="detail-blog-content">
            {{$data.Post_date}} | {{$data.Author}}
          </div>
          <p>{{$data.Content}}</p>
        </div>
      </div>
      {{end}}
    </div>
  </body>
</html>
```

<img alt="image1" src={useBaseUrl('img/docs/image-4-50.png')} height="350px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://personal-web-chapter-2.herokuapp.com/blog">
Demo
</a>
</div>
