# Vortigern with custom render
issue: https://github.com/barbar/vortigern/issues/126

#### Change:
1. add /src/index.html

  <!DOCTYPE html>
  <html lang="en">
    <head>
      <title>Some title</title>
    </head>
    <body>
      <h1>Custom Render</h1>
      <main id="app"></main>
      <script src='/public/js/app.js'></script>
    </body>
  </html>

2. change /src/server.tsx

2.1 add coping index.html to directory  /build 

  const fs = require('fs');
  fs
    .createReadStream(path.join(__dirname, '../src/index.html'))
    .pipe(fs.createWriteStream(path.join(__dirname, 'index.html')));
 
2.2 add optional reading index.html 

    app.get('*', (req, res) => {

      if (appConfig.staticRender) {
          res.sendFile(path.join(__dirname, 'index.html'));
          return;
      }

    ..........
3. add option staticRender in  /config/main.js

var config = {
  staticRender: true,
  ...................
