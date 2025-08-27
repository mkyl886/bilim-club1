# bilim-club1[bilim_kulubu_kolay.html](https://github.com/user-attachments/files/22013288/bilim_kulubu_kolay.html)
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bilim Kulübü</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f5f5f5; }
    header { background: #004d7a; color: white; padding: 1rem; text-align: center; }
    nav { background: #006699; padding: 0.5rem; text-align: center; }
    nav a { color: white; margin: 0 10px; text-decoration: none; }
    main { max-width: 800px; margin: 2rem auto; padding: 1rem; background: white; border-radius: 8px; }
    article { border-bottom: 1px solid #ddd; padding: 1rem 0; }
    h2 { margin: 0; }
    .admin-panel { display: none; margin-top: 2rem; }
    .hidden { display: none; }
    footer { text-align: center; padding: 1rem; background: #eee; margin-top: 2rem; }
    input, textarea { width: 100%; padding: 8px; margin: 5px 0; }
    button { padding: 8px 16px; margin-top: 10px; background: #004d7a; color: white; border: none; border-radius: 4px; cursor: pointer; }
  </style>
</head>
<body>
  <header>
    <h1>Bilim Kulübü</h1>
  </header>
  <nav>
    <a href="#" onclick="showPosts()">Anasayfa</a>
    <a href="#" onclick="showAdmin()">Admin Paneli</a>
  </nav>
  <main id="content">
    <h2>Yazılar</h2>
    <div id="posts"></div>
  </main>

  <div class="admin-panel" id="adminPanel">
    <h2>Yeni Yazı Ekle</h2>
    <input type="text" id="title" placeholder="Başlık">
    <textarea id="contentInput" placeholder="Yazı içeriği"></textarea>
    <button onclick="addPost()">Ekle</button>
  </div>

  <footer>
    <p>© 2025 Bilim Kulübü</p>
  </footer>

  <script>
    let posts = JSON.parse(localStorage.getItem("posts")) || [];

    function renderPosts() {
      const postsDiv = document.getElementById("posts");
      postsDiv.innerHTML = "";
      posts.forEach((post, index) => {
        const article = document.createElement("article");
        article.innerHTML = `<h2>${post.title}</h2><p>${post.content}</p>
          <button onclick="deletePost(${index})">Sil</button>`;
        postsDiv.appendChild(article);
      });
    }

    function addPost() {
      const title = document.getElementById("title").value;
      const content = document.getElementById("contentInput").value;
      if (title && content) {
        posts.push({ title, content });
        localStorage.setItem("posts", JSON.stringify(posts));
        renderPosts();
        document.getElementById("title").value = "";
        document.getElementById("contentInput").value = "";
      } else {
        alert("Lütfen başlık ve içerik girin!");
      }
    }

    function deletePost(index) {
      posts.splice(index, 1);
      localStorage.setItem("posts", JSON.stringify(posts));
      renderPosts();
    }

    function showAdmin() {
      document.getElementById("adminPanel").style.display = "block";
      document.getElementById("content").style.display = "none";
    }

    function showPosts() {
      document.getElementById("adminPanel").style.display = "none";
      document.getElementById("content").style.display = "block";
      renderPosts();
    }

    renderPosts();
  </script>
</body>
</html>
