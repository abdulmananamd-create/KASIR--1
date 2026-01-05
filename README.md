<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Kasir | Jennaira Frozen</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

<nav>
  <h1>JENNAIRA FROZEN</h1>
</nav>

<div class="container">
  <h2>Aplikasi Kasir</h2>

  <label>Nama Barang</label>
  <select id="barang">
    <option value="Nugget Ayam|25000">Nugget Ayam - 25.000</option>
    <option value="Sosis Frozen|20000">Sosis Frozen - 20.000</option>
    <option value="Kentang Frozen|30000">Kentang Frozen - 30.000</option>
  </select>

  <label>Jumlah</label>
  <input type="number" id="jumlah" value="1">

  <button onclick="tambah()">Tambah</button>

  <table>
    <thead>
      <tr>
        <th>Barang</th>
        <th>Harga</th>
        <th>Jumlah</th>
        <th>Subtotal</th>
      </tr>
    </thead>
    <tbody id="keranjang"></tbody>
  </table>

  <h3>Total: Rp <span id="total">0</span></h3>

  <label>Uang Bayar</label>
  <input type="number" id="bayar">

  <button onclick="hitung()">Bayar</button>

  <h3>Kembalian: Rp <span id="kembali">0</span></h3>

  <button onclick="printStruk()">Print Struk</button>
</div>

<script src="js/kasir.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  background: #eaf3ff;
  margin: 0;
}

nav {
  background: #007bff;
  color: white;
  padding: 15px;
  text-align: center;
}

.container {
  background: white;
  width: 80%;
  margin: 20px auto;
  padding: 20px;
  border-radius: 8px;
}

label {
  display: block;
  margin-top: 10px;
}

input, select, button {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
}

button {
  background: #007bff;
  color: white;
  border: none;
  margin-top: 15px;
  cursor: pointer;
}

button:hover {
  background: #0056b3;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 15px;
}

th, td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: center;
}
let total = 0;

function tambah() {
  let barang = document.getElementById("barang").value.split("|");
  let nama = barang[0];
  let harga = parseInt(barang[1]);
  let jumlah = parseInt(document.getElementById("jumlah").value);

  let subtotal = harga * jumlah;
  total += subtotal;

  let row = `
    <tr>
      <td>${nama}</td>
      <td>${harga}</td>
      <td>${jumlah}</td>
      <td>${subtotal}</td>
    </tr>
  `;

  document.getElementById("keranjang").innerHTML += row;
  document.getElementById("total").innerText = total;
}

function hitung() {
  let bayar = parseInt(document.getElementById("bayar").value);
  let kembali = bayar - total;
  document.getElementById("kembali").innerText = kembali;
}

function printStruk() {
  window.print();
}
