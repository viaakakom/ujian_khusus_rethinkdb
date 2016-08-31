# ujian_khusus_rethinkdb

1. aplikasi ini dibangun menggunakan node.js, angular.js dan database rethinkDB
2. mengintall database rethinkDB dan node.js
3. membuat package json untuk menginstall modul 
   {
  "name": "crud-kalimat",
  "version": "0.0.2",
  "private": true,
  "dependencies": {
    "body-parser": "1.0.2",
    "express": "4.0.0",
    "rethinkdb": "^2.2.1"
  }
}

4. kemudian menginstall modul dengan masuk pada cmd administrator, Pastikan sudah masuk dalam folder dimana package.json yang dibuat tadi disimpan. Modul-modul ini digunakan mempermudah pembangunan aplikasi

5. membuat koneksi/menghubungkan ke database rethinkDB dan express pada config.js
   module.exports = {
    rethinkdb: {
        host: "localhost",
        port: 28015,
        authKey: "",
        db: "rethinkdb_ex"
    },
    express: {
        port: 3000
    }
}
//rethink db terdapat pada port 28015 dan express pada port 3000

6. Buat file app.js yang berisi setting server, routes dan fungsi crud
// Import modul express
var express = require('express');
var bodyParser = require('body-parser');
var app = express();

// Load file config.js
var config = require(__dirname+"/config.js");

var r = require('rethinkdb');

app.use(express.static(__dirname + '/public'));
app.use(bodyParser());

//membuat koneksi ke database
app.use(createConnection);

// Definisi main routes
app.route('/todo/get').get(get);
app.route('/todo/new').put(create);
app.route('/todo/update').post(update);
app.route('/todo/delete').post(del);

//membuat fungsi untuk mulai express dengan mengambil port express
function startExpress() {
    app.listen(config.express.port);
    console.log('Listening on port '+config.express.port);
}

7. Membuat halaman untuk index,  memanfaatkan angular.js sehingga aplikasi cepat tanpa ada reload/request ke server.
