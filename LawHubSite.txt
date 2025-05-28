LawHubSite/
├── <!DOCTYPE html>
<html>
<head>
  <title>LawHub</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <h1>Welcome to LawHub</h1>
  <nav>
    <a href="research.html">Research Papers</a> |
    <a href="caselaws.html">Case Laws</a> |
    <a href="blog.html">Blog</a>
  </nav>
</body>
</html>
├── <!DOCTYPE html>
<html>
<head>
  <title>Research Papers</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <h1>Research Papers</h1>
  <ul id="research-list"></ul>
  <script src="js/dynamic.js"></script>
</body>
</html>
├── <!DOCTYPE html>
<html>
<head>
  <title>Case Laws</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <h1>Case Laws</h1>
  <ul id="caselaws-list"></ul>
  <script src="js/dynamic.js"></script>
</body>
</html>
├── <!DOCTYPE html>
<html>
<head>
  <title>Blog</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <h1>Blog</h1>
  <div id="blog-posts"></div>
  <script src="js/dynamic.js"></script>
</body>
</html>
├── /uploads
│   ├── /research
│   └── /caselaws
├── /_posts
├── /admin
│   ├── <!DOCTYPE html>
<html>
<head><title>Admin Panel</title></head>
<body>
  <script src="https://unpkg.com/netlify-cms@latest/dist/netlify-cms.js"></script>
</body>
</html>
│   └── backend:
  name: git-gateway
  branch: main

media_folder: "uploads"
public_folder: "/uploads"

collections:
  - name: "research"
    label: "Research Papers"
    folder: "uploads/research"
    create: true
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "File", name: "file", widget: "file" }

  - name: "caselaws"
    label: "Case Laws"
    folder: "uploads/caselaws"
    create: true
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "File", name: "file", widget: "file" }

  - name: "blog"
    label: "Blog Posts"
    folder: "_posts"
    create: true
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    fields:
      - { label: "Title", name: "title", widget: "string" }
      - { label: "Body", name: "body", widget: "markdown" }
├── /css
│   └── /* Reset some default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f5f5f5;
  color: #333;
  line-height: 1.6;
}

header {
  background-color: #0073e6;
  color: #fff;
  padding: 20px;
  text-align: center;
}

header h1 {
  font-size: 2rem;
}

nav {
  background-color: #005bb5;
  display: flex;
  justify-content: center;
  padding: 10px;
}

nav a {
  color: #fff;
  text-decoration: none;
  padding: 10px 20px;
  transition: background-color 0.3s ease;
}

nav a:hover {
  background-color: #004494;
}

.container {
  max-width: 1000px;
  margin: 20px auto;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
  margin-bottom: 10px;
  color: #0073e6;
}

p {
  margin-bottom: 15px;
}

ul {
  list-style: disc;
  margin-left: 20px;
}

a.button {
  display: inline-block;
  background-color: #0073e6;
  color: #fff;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

a.button:hover {
  background-color: #004494;
}

footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 15px;
  position: fixed;
  bottom: 0;
  width: 100%;
}

.upload-section {
  margin: 20px 0;
}

.upload-section label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.upload-section input[type="file"] {
  margin-bottom: 10px;
}

.upload-section button {
  background-color: #0073e6;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

.upload-section button:hover {
  background-color: #004494;
}
└── /js
    └── // Fetch Research PDFs
if(document.getElementById('research-list')){
  fetch('/uploads/research/')
  .then(r=>r.text()).then(d=>{
    const parser = new DOMParser();
    const doc = parser.parseFromString(d, 'text/html');
    doc.querySelectorAll('a').forEach(a=>{
      if(a.href.endsWith('.pdf')){
        let li=document.createElement('li');
        li.innerHTML=`<a href="${a.href}" target="_blank">${a.text} 📄</a>`;
        research-list.appendChild(li);
      }
    });
  });
}

// Fetch Case Laws PDFs
if(document.getElementById('caselaws-list')){
  fetch('/uploads/caselaws/')
  .then(r=>r.text()).then(d=>{
    const parser = new DOMParser();
    const doc = parser.parseFromString(d, 'text/html');
    doc.querySelectorAll('a').forEach(a=>{
      if(a.href.endsWith('.pdf')){
        let li=document.createElement('li');
        li.innerHTML=`<a href="${a.href}" target="_blank">${a.text} 📄</a>`;
        caselaws-list.appendChild(li);
      }
    });
  });
}

// Fetch Blog Posts
if(document.getElementById('blog-posts')){
  fetch('/_posts')
  .then(r=>r.text()).then(d=>{
    const parser = new DOMParser();
    const doc = parser.parseFromString(d, 'text/html');
    doc.querySelectorAll('a').forEach(a=>{
      if(a.href.endsWith('.md')){
        let div=document.createElement('div');
        div.innerHTML=`<a href="${a.href}" target="_blank">${a.text} 📝</a>`;
        blog-posts.appendChild(div);
      }
    });
  });
}
