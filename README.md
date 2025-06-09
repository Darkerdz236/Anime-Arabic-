<!DOCTYPE html><html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>منتدى المانجا والأنمي والكوميكس</title>
  <style>
    body { font-family: 'Tahoma', sans-serif; background-color: #111; color: #fff; margin: 0; padding: 0; }
    header { background: #222; padding: 20px; text-align: center; font-size: 24px; color: #f97316; }
    main { padding: 20px; max-width: 800px; margin: auto; }
    .post { background: #1e1e1e; padding: 15px; margin-bottom: 20px; border-radius: 10px; }
    .post img { max-width: 100%; border-radius: 8px; margin-top: 10px; }
    .comments { margin-top: 15px; border-top: 1px solid #333; padding-top: 10px; }
    .comment { margin-bottom: 10px; }
    input, textarea, button { width: 100%; padding: 10px; margin-top: 10px; border: none; border-radius: 5px; }
    input, textarea { background: #2a2a2a; color: #fff; }
    button { background: #f97316; color: white; cursor: pointer; }
    button:hover { background: #fb923c; }
  </style>
</head>
<body>
  <header>
    منتدى نقاشات الأنمي والمانجا والكوميكس
  </header>
  <main>
    <section class="new-post">
      <h2>انشر نظرية أو نقاش جديد</h2>
      <input type="text" id="title" placeholder="عنوان النقاش">
      <textarea id="content" rows="4" placeholder="محتوى النظرية أو النقاش..."></textarea>
      <input type="file" id="image">
      <button onclick="createPost()">نشر</button>
    </section><section id="posts"></section>

  </main>  <script>
    const postsContainer = document.getElementById("posts");

    function createPost() {
      const title = document.getElementById("title").value;
      const content = document.getElementById("content").value;
      const imageInput = document.getElementById("image");
      const file = imageInput.files[0];

      const reader = new FileReader();
      reader.onload = function(e) {
        const post = document.createElement("div");
        post.className = "post";
        post.innerHTML = `
          <h3>${title}</h3>
          <p>${content}</p>
          ${file ? `<img src="${e.target.result}">` : ""}
          <div class="comments">
            <h4>التعليقات</h4>
            <div class="comment-list"></div>
            <input type="text" placeholder="اكتب تعليقك..." class="comment-input">
            <button onclick="addComment(this)">إضافة تعليق</button>
          </div>
        `;
        postsContainer.prepend(post);
      };
      if (file) reader.readAsDataURL(file);
      else reader.onload({ target: { result: "" } });
    }

    function addComment(button) {
      const container = button.closest(".comments");
      const input = container.querySelector(".comment-input");
      const list = container.querySelector(".comment-list");
      const comment = document.createElement("div");
      comment.className = "comment";
      comment.textContent = input.value;
      list.appendChild(comment);
      input.value = "";
    }
  </script></body>
</html>
