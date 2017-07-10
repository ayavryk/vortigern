# Vortigern with custom render
issue: https://github.com/barbar/vortigern/issues/126

#### Change:
1. add /src/index.html
2. change /src/server.tsx

2.1 add lines for coping index.html to directory  /build 

  const fs = require('fs');
  fs
    .createReadStream(path.join(__dirname, '../src/index.html'))
    .pipe(fs.createWriteStream(path.join(__dirname, 'index.html')));
 
2.2 add lines for optional render server/index.html 

    app.get('*', (req, res) => {

      if (appConfig.staticRender) {
          res.sendFile(path.join(__dirname, 'index.html'));
          return;
      }

    ..........
3. add line option staticRender in  /config/main.js

var config = {
  staticRender: true,
  ...................
