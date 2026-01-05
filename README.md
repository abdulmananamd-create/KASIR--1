# KASIR--1
KASIR 1
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Kasir - Sistem Point of Sale</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f7fa;
            color: #333;
            display: flex;
            min-height: 100vh;
        }

        /* Sidebar Menu */
        .sidebar {
            width: 250px;
            background: linear-gradient(to bottom, #2c3e50, #34495e);
            color: white;
            height: 100vh;
            position: fixed;
            overflow-y: auto;
            transition: all 0.3s;
            box-shadow: 3px 0 10px rgba(0, 0, 0, 0.1);
            z-index: 1000;
        }

        .logo {
            padding: 20px 15px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .logo h2 {
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .logo h2 i {
            margin-right: 10px;
            color: #3498db;
        }

        .menu {
            padding: 20px 0;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 15px 20px;
            color: #ecf0f1;
            text-decoration: none;
            transition: all 0.3s;
            border-left: 4px solid transparent;
        }

        .menu-item:hover {
            background-color: rgba(255, 255, 255, 0.1);
            border-left-color: #3498db;
            color: white;
        }

        .menu-item.active {
            background-color: rgba(52, 152, 219, 0.2);
            border-left-color: #3498db;
            color: white;
        }

        .menu-item i {
            width: 30px;
            font-size: 1.2rem;
        }

        /* Konten utama */
        .main-content {
            flex: 1;
            margin-left: 250px;
            transition: margin-left 0.3s;
            padding-bottom: 20px;
        }

        /* Header */
        .header {
            background-color: white;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header h1 {
            font-size: 1.8rem;
            color: #2c3e50;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #3498db;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }

        /* Container halaman */
        .page-container {
            padding: 30px;
        }

        /* Card */
        .card {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 30px;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid #eee;
            padding-bottom: 15px;
        }

        .card-header h2 {
            font-size: 1.5rem;
            color: #2c3e50;
        }

        /* Tabel */
        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        table th, table td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        table th {
            background-color: #f8f9fa;
            font-weight: 600;
            color: #2c3e50;
        }

        table tr:hover {
            background-color: #f8f9fa;
        }

        /* Form */
        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #2c3e50;
        }

        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
            transition: border 0.3s;
        }

        .form-control:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        /* Tombol */
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background-color: #3498db;
            color: white;
        }

        .btn-primary:hover {
            background-color: #2980b9;
        }

        .btn-success {
            background-color: #2ecc71;
            color: white;
        }

        .btn-success:hover {
            background-color: #27ae60;
        }

        .btn-warning {
            background-color: #f39c12;
            color: white;
        }

        .btn-warning:hover {
            background-color: #d35400;
        }

        .btn-danger {
            background-color: #e74c3c;
            color: white;
        }

        .btn-danger:hover {
            background-color: #c0392b;
        }

        /* Baris aksi */
        .action-buttons {
            display: flex;
            gap: 10px;
        }

        /* Grid untuk produk */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }

        .product-card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .product-image {
            width: 100%;
            height: 150px;
            background-color: #f8f9fa;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 15px;
            color: #7f8c8d;
            font-size: 3rem;
        }

        .product-info h3 {
            font-size: 1.2rem;
            margin-bottom: 10px;
            color: #2c3e50;
        }

        .product-price {
            font-size: 1.3rem;
            font-weight: 700;
            color: #2ecc71;
        }

        .product-stock {
            color: #7f8c8d;
            font-size: 0.9rem;
        }

        /* Search bar */
        .search-container {
            position: relative;
            margin-bottom: 20px;
        }

        .search-input {
            width: 100%;
            padding: 12px 15px 12px 45px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
        }

        .search-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #7f8c8d;
        }

        /* Tampilan kasir */
        .cashier-container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 30px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid #eee;
        }

        .cart-item-info h4 {
            margin-bottom: 5px;
        }

        .cart-item-actions {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .quantity-control {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #f8f9fa;
            cursor: pointer;
        }

        /* Dashboard stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .stat-icon {
            width: 60px;
            height: 60px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            color: white;
        }

        .stat-info h3 {
            font-size: 1.8rem;
            margin-bottom: 5px;
        }

        .stat-info p {
            color: #7f8c8d;
        }

        /* Tombol export */
        .export-buttons {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        /* Responsif */
        @media (max-width: 992px) {
            .sidebar {
                width: 80px;
            }

            .sidebar .menu-item span {
                display: none;
            }

            .main-content {
                margin-left: 80px;
            }

            .logo h2 span {
                display: none;
            }

            .cashier-container {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }

            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            }
        }
    </style>
</head>
<body>
    <!-- Sidebar Menu -->
    <div class="sidebar">
        <div class="logo">
            <h2><i class="fas fa-cash-register"></i> <span>Kasir Pro</span></h2>
        </div>
        <div class="menu">
            <a href="#" class="menu-item active" data-page="dashboard">
                <i class="fas fa-home"></i> <span>Dashboard</span>
            </a>
            <a href="#" class="menu-item" data-page="kasir">
                <i class="fas fa-shopping-cart"></i> <span>Kasir</span>
            </a>
            <a href="#" class="menu-item" data-page="produk">
                <i class="fas fa-box-open"></i> <span>Produk & Stok</span>
            </a>
            <a href="#" class="menu-item" data-page="laporan">
                <i class="fas fa-chart-bar"></i> <span>Laporan</span>
            </a>
            <a href="#" class="menu-item" data-page="riwayat">
                <i class="fas fa-history"></i> <span>Riwayat</span>
            </a>
            <a href="#" class="menu-item" data-page="pengaturan">
                <i class="fas fa-cog"></i> <span>Pengaturan</span>
            </a>
        </div>
    </div>

    <!-- Konten Utama -->
    <div class="main-content">
        <!-- Header -->
        <div class="header">
            <h1 id="page-title">Dashboard</h1>
            <div class="user-info">
                <div class="user-avatar">AD</div>
                <div>
                    <h4>Admin</h4>
                    <p style="font-size: 0.9rem; color: #7f8c8d;">Super Admin</p>
                </div>
            </div>
        </div>

        <!-- Container Halaman -->
        <div class="page-container">
            <!-- Dashboard -->
            <div id="dashboard-page" class="page-content active">
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-icon" style="background-color: #3498db;">
                            <i class="fas fa-dollar-sign"></i>
                        </div>
                        <div class="stat-info">
                            <h3>Rp 12.450.000</h3>
                            <p>Pendapatan Hari Ini</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background-color: #2ecc71;">
                            <i class="fas fa-shopping-cart"></i>
                        </div>
                        <div class="stat-info">
                            <h3>48</h3>
                            <p>Transaksi Hari Ini</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background-color: #f39c12;">
                            <i class="fas fa-box-open"></i>
                        </div>
                        <div class="stat-info">
                            <h3>156</h3>
                            <p>Total Produk</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background-color: #e74c3c;">
                            <i class="fas fa-exclamation-triangle"></i>
                        </div>
                        <div class="stat-info">
                            <h3>12</h3>
                            <p>Stok Menipis</p>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h2>Aktivitas Terbaru</h2>
                        <button class="btn btn-primary">Lihat Semua</button>
                    </div>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Waktu</th>
                                    <th>Transaksi</th>
                                    <th>Pelanggan</th>
                                    <th>Total</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>14:30</td>
                                    <td>TRX-001245</td>
                                    <td>Budi Santoso</td>
                                    <td>Rp 325.000</td>
                                    <td><span style="color: #2ecc71; font-weight: bold;">Selesai</span></td>
                                </tr>
                                <tr>
                                    <td>13:15</td>
                                    <td>TRX-001244</td>
                                    <td>Ani Wijaya</td>
                                    <td>Rp 150.000</td>
                                    <td><span style="color: #2ecc71; font-weight: bold;">Selesai</span></td>
                                </tr>
                                <tr>
                                    <td>11:45</td>
                                    <td>TRX-001243</td>
                                    <td>CV Makmur Jaya</td>
                                    <td>Rp 1.250.000</td>
                                    <td><span style="color: #2ecc71; font-weight: bold;">Selesai</span></td>
                                </tr>
                                <tr>
                                    <td>10:20</td>
                                    <td>TRX-001242</td>
                                    <td>Siti Rahayu</td>
                                    <td>Rp 85.000</td>
                                    <td><span style="color: #2ecc71; font-weight: bold;">Selesai</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Kasir -->
            <div id="kasir-page" class="page-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Transaksi Kasir</h2>
                    </div>
                    
                    <div class="cashier-container">
                        <div>
                            <div class="search-container">
                                <i class="fas fa-search search-icon"></i>
                                <input type="text" class="search-input" id="product-search" placeholder="Cari produk berdasarkan nama atau kode...">
                            </div>
                            
                            <div class="products-grid" id="product-list">
                                <!-- Produk akan dimuat di sini oleh JavaScript -->
                            </div>
                        </div>
                        
                        <div>
                            <div class="card">
                                <div class="card-header">
                                    <h2>Keranjang Belanja</h2>
                                </div>
                                <div id="cart-items">
                                    <!-- Item keranjang akan dimuat di sini -->
                                    <p style="text-align: center; color: #7f8c8d; padding: 20px;">Keranjang kosong</p>
                                </div>
                                
                                <div style="margin-top: 20px; border-top: 1px solid #eee; padding-top: 20px;">
                                    <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                                        <span>Subtotal:</span>
                                        <span id="subtotal">Rp 0</span>
                                    </div>
                                    <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                                        <span>Pajak (10%):</span>
                                        <span id="tax">Rp 0</span>
                                    </div>
                                    <div style="display: flex; justify-content: space-between; font-size: 1.2rem; font-weight: bold; margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee;">
                                        <span>Total:</span>
                                        <span id="total">Rp 0</span>
                                    </div>
                                    
                                    <div style="margin-top: 25px;">
                                        <button class="btn btn-success" style="width: 100%; padding: 15px; font-size: 1.1rem;" id="checkout-btn">
                                            <i class="fas fa-check"></i> Proses Pembayaran
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Produk & Stok -->
            <div id="produk-page" class="page-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Daftar Produk</h2>
                        <button class="btn btn-primary" id="add-product-btn">
                            <i class="fas fa-plus"></i> Tambah Produk
                        </button>
                    </div>
                    
                    <div class="search-container">
                        <i class="fas fa-search search-icon"></i>
                        <input type="text" class="search-input" id="product-list-search" placeholder="Cari produk...">
                    </div>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Kode</th>
                                    <th>Nama Produk</th>
                                    <th>Kategori</th>
                                    <th>Harga</th>
                                    <th>Stok</th>
                                    <th>Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="product-table">
                                <!-- Data produk akan dimuat di sini oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Laporan -->
            <div id="laporan-page" class="page-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Laporan Penjualan</h2>
                        <div class="export-buttons">
                            <button class="btn btn-success" id="export-csv">
                                <i class="fas fa-file-csv"></i> Export CSV
                            </button>
                            <button class="btn btn-success" id="export-excel">
                                <i class="fas fa-file-excel"></i> Export Excel
                            </button>
                        </div>
                    </div>
                    
                    <div class="form-group" style="display: flex; gap: 15px; margin-bottom: 20px;">
                        <div style="flex: 1;">
                            <label>Dari Tanggal</label>
                            <input type="date" class="form-control" id="start-date" value="2023-10-01">
                        </div>
                        <div style="flex: 1;">
                            <label>Sampai Tanggal</label>
                            <input type="date" class="form-control" id="end-date" value="2023-10-31">
                        </div>
                        <div style="display: flex; align-items: flex-end;">
                            <button class="btn btn-primary" id="filter-report">
                                <i class="fas fa-filter"></i> Filter
                            </button>
                        </div>
                    </div>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Tanggal</th>
                                    <th>No. Transaksi</th>
                                    <th>Produk</th>
                                    <th>Jumlah</th>
                                    <th>Harga</th>
                                    <th>Total</th>
                                </tr>
                            </thead>
                            <tbody id="report-table">
                                <!-- Data laporan akan dimuat di sini -->
                            </tbody>
                        </table>
                    </div>
                    
                    <div style="display: flex; justify-content: space-between; margin-top: 20px; padding-top: 20px; border-top: 1px solid #eee;">
                        <div>
                            <h3>Total Pendapatan:</h3>
                            <p style="font-size: 1.5rem; color: #2ecc71; font-weight: bold;" id="total-income">Rp 0</p>
                        </div>
                        <div>
                            <h3>Jumlah Transaksi:</h3>
                            <p style="font-size: 1.5rem; color: #3498db; font-weight: bold;" id="total-transactions">0</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Riwayat -->
            <div id="riwayat-page" class="page-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Riwayat Transaksi</h2>
                    </div>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Tanggal/Waktu</th>
                                    <th>No. Transaksi</th>
                                    <th>Pelanggan</th>
                                    <th>Items</th>
                                    <th>Total</th>
                                    <th>Kasir</th>
                                    <th>Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="history-table">
                                <!-- Data riwayat akan dimuat di sini -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Pengaturan -->
            <div id="pengaturan-page" class="page-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Pengaturan Aplikasi</h2>
                    </div>
                    
                    <div style="max-width: 600px;">
                        <div class="form-group">
                            <label>Nama Toko</label>
                            <input type="text" class="form-control" id="store-name" value="Toko Makmur Jaya">
                        </div>
                        
                        <div class="form-group">
                            <label>Alamat Toko</label>
                            <textarea class="form-control" id="store-address" rows="3">Jl. Merdeka No. 123, Jakarta Pusat</textarea>
                        </div>
                        
                        <div class="form-group">
                            <label>Telepon</label>
                            <input type="text" class="form-control" id="store-phone" value="021-1234567">
                        </div>
                        
                        <div class="form-group">
                            <label>Pajak (%)</label>
                            <input type="number" class="form-control" id="tax-rate" value="10" min="0" max="100">
                        </div>
                        
                        <div class="form-group">
                            <label>Nota Footer</label>
                            <textarea class="form-control" id="receipt-footer" rows="2">Terima kasih telah berbelanja di toko kami</textarea>
                        </div>
                        
                        <div style="margin-top: 30px;">
                            <button class="btn btn-primary" id="save-settings">
                                <i class="fas fa-save"></i> Simpan Pengaturan
                            </button>
                            <button class="btn btn-warning" id="reset-settings" style="margin-left: 10px;">
                                <i class="fas fa-undo"></i> Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Data produk contoh
        const sampleProducts = [
            { id: 1, code: "P001", name: "Indomie Goreng", category: "Makanan", price: 3500, stock: 45 },
            { id: 2, code: "P002", name: "Aqua 600ml", category: "Minuman", price: 3000, stock: 120 },
            { id: 3, code: "P003", name: "Roti Tawar", category: "Makanan", price: 15000, stock: 25 },
            { id: 4, code: "P004", name: "Susu Ultra", category: "Minuman", price: 6000, stock: 60 },
            { id: 5, code: "P005", name: "Kopi Sachet", category: "Minuman", price: 2000, stock: 200 },
            { id: 6, code: "P006", name: "Shampoo Clear", category: "Perawatan", price: 18000, stock: 30 },
            { id: 7, code: "P007", name: "Sabun Lifebuoy", category: "Perawatan", price: 5000, stock: 75 },
            { id: 8, code: "P008", name: "Pensil 2B", category: "Alat Tulis", price: 2500, stock: 150 },
            { id: 9, code: "P009", name: "Buku Tulis", category: "Alat Tulis", price: 5000, stock: 80 },
            { id: 10, code: "P010", name: "Sikat Gigi", category: "Perawatan", price: 8000, stock: 40 }
        ];

        // Data transaksi contoh
        const sampleTransactions = [
            { id: 1, date: "2023-10-25 14:30", code: "TRX-001245", customer: "Budi Santoso", items: 3, total: 325000, cashier: "Admin" },
            { id: 2, date: "2023-10-25 13:15", code: "TRX-001244", customer: "Ani Wijaya", items: 2, total: 150000, cashier: "Admin" },
            { id: 3, date: "2023-10-25 11:45", code: "TRX-001243", customer: "CV Makmur Jaya", items: 5, total: 1250000, cashier: "Admin" },
            { id: 4, date: "2023-10-25 10:20", code: "TRX-001242", customer: "Siti Rahayu", items: 1, total: 85000, cashier: "Admin" },
            { id: 5, date: "2023-10-24 16:45", code: "TRX-001241", customer: "Joko Prasetyo", items: 4, total: 220000, cashier: "Admin" }
        ];

        // Data laporan contoh
        const sampleReportData = [
            { date: "2023-10-25", code: "TRX-001245", product: "Indomie Goreng", quantity: 5, price: 3500, total: 17500 },
            { date: "2023-10-25", code: "TRX-001245", product: "Aqua 600ml", quantity: 10, price: 3000, total: 30000 },
            { date: "2023-10-25", code: "TRX-001245", product: "Roti Tawar", quantity: 2, price: 15000, total: 30000 },
            { date: "2023-10-25", code: "TRX-001244", product: "Susu Ultra", quantity: 4, price: 6000, total: 24000 },
            { date: "2023-10-25", code: "TRX-001244", product: "Kopi Sachet", quantity: 20, price: 2000, total: 40000 }
        ];

        // Variabel global
        let cart = [];
        let currentPage = "dashboard";

        // Inisialisasi aplikasi
        document.addEventListener('DOMContentLoaded', function() {
            // Setup menu navigasi
            setupNavigation();
            
            // Load data awal
            loadDashboard();
            loadProducts();
            loadProductTable();
            loadReport();
            loadHistory();
            
            // Setup event listeners
            setupEventListeners();
        });

        // Setup navigasi menu
        function setupNavigation() {
            const menuItems = document.querySelectorAll('.menu-item');
            
            menuItems.forEach(item => {
                item.addEventListener('click', function(e) {
                    e.preventDefault();
                    
                    // Hapus class active dari semua menu
                    menuItems.forEach(i => i.classList.remove('active'));
                    
                    // Tambah class active ke menu yang diklik
                    this.classList.add('active');
                    
                    // Dapatkan halaman yang akan ditampilkan
                    const pageId = this.getAttribute('data-page');
                    
                    // Tampilkan halaman yang sesuai
                    showPage(pageId);
                });
            });
        }

        // Tampilkan halaman berdasarkan ID
        function showPage(pageId) {
            // Sembunyikan semua halaman
            const pages = document.querySelectorAll('.page-content');
            pages.forEach(page => page.classList.remove('active'));
            
            // Tampilkan halaman yang dipilih
            const activePage = document.getElementById(`${pageId}-page`);
            if (activePage) {
                activePage.classList.add('active');
            }
            
            // Update judul halaman
            const pageTitle = document.getElementById('page-title');
            const pageTitles = {
                dashboard: "Dashboard",
                kasir: "Kasir",
                produk: "Produk & Stok",
                laporan: "Laporan",
                riwayat: "Riwayat",
                pengaturan: "Pengaturan"
            };
            
            pageTitle.textContent = pageTitles[pageId] || "Dashboard";
            currentPage = pageId;
            
            // Refresh data halaman jika diperlukan
            if (pageId === 'dashboard') loadDashboard();
            if (pageId === 'kasir') loadProducts();
            if (pageId === 'produk') loadProductTable();
            if (pageId === 'laporan') loadReport();
            if (pageId === 'riwayat') loadHistory();
        }

        // Setup event listeners
        function setupEventListeners() {
            // Search bar untuk produk di halaman kasir
            const productSearch = document.getElementById('product-search');
            if (productSearch) {
                productSearch.addEventListener('input', function() {
                    filterProducts(this.value);
                });
            }
            
            // Search bar untuk produk di halaman daftar produk
            const productListSearch = document.getElementById('product-list-search');
            if (productListSearch) {
                productListSearch.addEventListener('input', function() {
                    filterProductTable(this.value);
                });
            }
            
            // Tombol checkout
            const checkoutBtn = document.getElementById('checkout-btn');
            if (checkoutBtn) {
                checkoutBtn.addEventListener('click', processCheckout);
            }
            
            // Tombol tambah produk
            const addProductBtn = document.getElementById('add-product-btn');
            if (addProductBtn) {
                addProductBtn.addEventListener('click', addNewProduct);
            }
            
            // Tombol export
            const exportCsvBtn = document.getElementById('export-csv');
            if (exportCsvBtn) {
                exportCsvBtn.addEventListener('click', exportToCSV);
            }
            
            const exportExcelBtn = document.getElementById('export-excel');
            if (exportExcelBtn) {
                exportExcelBtn.addEventListener('click', exportToExcel);
            }
            
            // Tombol filter laporan
            const filterReportBtn = document.getElementById('filter-report');
            if (filterReportBtn) {
                filterReportBtn.addEventListener('click', loadReport);
            }
            
            // Tombol simpan pengaturan
            const saveSettingsBtn = document.getElementById('save-settings');
            if (saveSettingsBtn) {
                saveSettingsBtn.addEventListener('click', saveSettings);
            }
            
            // Tombol reset pengaturan
            const resetSettingsBtn = document.getElementById('reset-settings');
            if (resetSettingsBtn) {
                resetSettingsBtn.addEventListener('click', resetSettings);
            }
        }

        // Load dashboard
        function loadDashboard() {
            // Dashboard sudah diisi dengan konten statis
            // Dalam implementasi nyata, di sini akan ada panggilan API
        }

        // Load produk untuk halaman kasir
        function loadProducts() {
            const productList = document.getElementById('product-list');
            if (!productList) return;
            
            productList.innerHTML = '';
            
            sampleProducts.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                productCard.setAttribute('data-id', product.id);
                productCard.innerHTML = `
                    <div class="product-image">
                        <i class="fas fa-box"></i>
                    </div>
                    <div class="product-info">
                        <h3>${product.name}</h3>
                        <p class="product-price">Rp ${product.price.toLocaleString('id-ID')}</p>
                        <p class="product-stock">Stok: ${product.stock} | Kode: ${product.code}</p>
                    </div>
                `;
                
                productCard.addEventListener('click', () => addToCart(product));
                productList.appendChild(productCard);
            });
        }

        // Filter produk di halaman kasir
        function filterProducts(searchTerm) {
            const productCards = document.querySelectorAll('.product-card');
            const term = searchTerm.toLowerCase();
            
            productCards.forEach(card => {
                const productName = card.querySelector('h3').textContent.toLowerCase();
                const productCode = card.querySelector('.product-stock').textContent.toLowerCase();
                
                if (productName.includes(term) || productCode.includes(term)) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // Tambah produk ke keranjang
        function addToCart(product) {
            // Cek apakah produk sudah ada di keranjang
            const existingItem = cart.find(item => item.id === product.id);
            
            if (existingItem) {
                // Jika sudah ada, tambah jumlah
                if (existingItem.quantity < product.stock) {
                    existingItem.quantity++;
                } else {
                    alert(`Stok ${product.name} tidak mencukupi!`);
                    return;
                }
            } else {
                // Jika belum ada, tambah item baru
                if (product.stock > 0) {
                    cart.push({
                        id: product.id,
                        name: product.name,
                        price: product.price,
                        quantity: 1,
                        stock: product.stock
                    });
                } else {
                    alert(`Stok ${product.name} habis!`);
                    return;
                }
            }
            
            // Update tampilan keranjang
            updateCartDisplay();
            
            // Tampilkan notifikasi
            showNotification(`${product.name} ditambahkan ke keranjang`);
        }

        // Update tampilan keranjang
        function updateCartDisplay() {
            const cartItems = document.getElementById('cart-items');
            const subtotalElement = document.getElementById('subtotal');
            const taxElement = document.getElementById('tax');
            const totalElement = document.getElementById('total');
            
            if (cart.length === 0) {
                cartItems.innerHTML = '<p style="text-align: center; color: #7f8c8d; padding: 20px;">Keranjang kosong</p>';
                subtotalElement.textContent = 'Rp 0';
                taxElement.textContent = 'Rp 0';
                totalElement.textContent = 'Rp 0';
                return;
            }
            
            // Hitung subtotal
            let subtotal = 0;
            cart.forEach(item => {
                subtotal += item.price * item.quantity;
            });
            
            // Hitung pajak (10%)
            const taxRate = 0.1;
            const tax = subtotal * taxRate;
            
            // Hitung total
            const total = subtotal + tax;
            
            // Update elemen
            subtotalElement.textContent = `Rp ${subtotal.toLocaleString('id-ID')}`;
            taxElement.textContent = `Rp ${tax.toLocaleString('id-ID')}`;
            totalElement.textContent = `Rp ${total.toLocaleString('id-ID')}`;
            
            // Tampilkan item keranjang
            cartItems.innerHTML = '';
            cart.forEach(item => {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div class="cart-item-info">
                        <h4>${item.name}</h4>
                        <p>Rp ${item.price.toLocaleString('id-ID')}</p>
                    </div>
                    <div class="cart-item-actions">
                        <div class="quantity-control">
                            <div class="quantity-btn minus" data-id="${item.id}">
                                <i class="fas fa-minus"></i>
                            </div>
                            <span style="font-weight: bold;">${item.quantity}</span>
                            <div class="quantity-btn plus" data-id="${item.id}">
                                <i class="fas fa-plus"></i>
                            </div>
                        </div>
                        <div style="font-weight: bold; min-width: 100px; text-align: right;">
                            Rp ${(item.price * item.quantity).toLocaleString('id-ID')}
                        </div>
                        <div class="quantity-btn remove" data-id="${item.id}" style="background-color: #ffeaea; color: #e74c3c;">
                            <i class="fas fa-trash"></i>
                        </div>
                    </div>
                `;
                
                cartItems.appendChild(cartItem);
            });
            
            // Tambah event listeners untuk tombol di keranjang
            document.querySelectorAll('.quantity-btn.minus').forEach(btn => {
                btn.addEventListener('click', function() {
                    const productId = parseInt(this.getAttribute('data-id'));
                    decreaseQuantity(productId);
                });
            });
            
            document.querySelectorAll('.quantity-btn.plus').forEach(btn => {
                btn.addEventListener('click', function() {
                    const productId = parseInt(this.getAttribute('data-id'));
                    increaseQuantity(productId);
                });
            });
            
            document.querySelectorAll('.quantity-btn.remove').forEach(btn => {
                btn.addEventListener('click', function() {
                    const productId = parseInt(this.getAttribute('data-id'));
                    removeFromCart(productId);
                });
            });
        }

        // Kurangi jumlah produk di keranjang
        function decreaseQuantity(productId) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                if (item.quantity > 1) {
                    item.quantity--;
                } else {
                    // Jika jumlah menjadi 0, hapus dari keranjang
                    cart = cart.filter(item => item.id !== productId);
                }
                updateCartDisplay();
            }
        }

        // Tambah jumlah produk di keranjang
        function increaseQuantity(productId) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                const product = sampleProducts.find(p => p.id === productId);
                if (item.quantity < product.stock) {
                    item.quantity++;
                    updateCartDisplay();
                } else {
                    alert(`Stok ${product.name} tidak mencukupi!`);
                }
            }
        }

        // Hapus produk dari keranjang
        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartDisplay();
            showNotification("Produk dihapus dari keranjang");
        }

        // Proses checkout
        function processCheckout() {
            if (cart.length === 0) {
                alert("Keranjang belanja kosong!");
                return;
            }
            
            // Tampilkan dialog konfirmasi
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const tax = subtotal * 0.1;
            const total = subtotal + tax;
            
            const confirmMessage = `Total belanja: Rp ${total.toLocaleString('id-ID')}\n\nLanjutkan proses pembayaran?`;
            
            if (confirm(confirmMessage)) {
                // Generate nomor transaksi
                const transactionCode = `TRX-${Date.now().toString().slice(-6)}`;
                
                // Simpan transaksi
                const transaction = {
                    id: sampleTransactions.length + 1,
                    date: new Date().toLocaleString('id-ID'),
                    code: transactionCode,
                    customer: "Pelanggan",
                    items: cart.reduce((sum, item) => sum + item.quantity, 0),
                    total: total,
                    cashier: "Admin"
                };
                
                // Dalam implementasi nyata, di sini akan ada penyimpanan ke database
                sampleTransactions.unshift(transaction);
                
                // Kurangi stok produk
                cart.forEach(cartItem => {
                    const product = sampleProducts.find(p => p.id === cartItem.id);
                    if (product) {
                        product.stock -= cartItem.quantity;
                    }
                });
                
                // Reset keranjang
                cart = [];
                updateCartDisplay();
                
                // Tampilkan notifikasi
                showNotification(`Transaksi ${transactionCode} berhasil!`, 'success');
                
                // Update tampilan produk
                loadProducts();
                loadProductTable();
                
                // Tampilkan halaman riwayat
                showPage('riwayat');
            }
        }

        // Load daftar produk untuk halaman produk & stok
        function loadProductTable(filter = '') {
            const productTable = document.getElementById('product-table');
            if (!productTable) return;
            
            productTable.innerHTML = '';
            
            let filteredProducts = sampleProducts;
            if (filter) {
                const term = filter.toLowerCase();
                filteredProducts = sampleProducts.filter(product => 
                    product.name.toLowerCase().includes(term) || 
                    product.code.toLowerCase().includes(term) ||
                    product.category.toLowerCase().includes(term)
                );
            }
            
            filteredProducts.forEach(product => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${product.code}</td>
                    <td>${product.name}</td>
                    <td>${product.category}</td>
                    <td>Rp ${product.price.toLocaleString('id-ID')}</td>
                    <td>
                        <span class="${product.stock < 10 ? 'low-stock' : ''}">
                            ${product.stock}
                        </span>
                    </td>
                    <td>
                        <div class="action-buttons">
                            <button class="btn btn-warning btn-sm edit-product" data-id="${product.id}">
                                <i class="fas fa-edit"></i>
                            </button>
                            <button class="btn btn-danger btn-sm delete-product" data-id="${product.id}">
                                <i class="fas fa-trash"></i>
                            </button>
                        </div>
                    </td>
                `;
                
                // Tambah class untuk stok rendah
                if (product.stock < 10) {
                    row.querySelector('.low-stock').style.color = '#e74c3c';
                    row.querySelector('.low-stock').style.fontWeight = 'bold';
                }
                
                productTable.appendChild(row);
            });
            
            // Tambah event listeners untuk tombol edit dan hapus
            document.querySelectorAll('.edit-product').forEach(btn => {
                btn.addEventListener('click', function() {
                    const productId = parseInt(this.getAttribute('data-id'));
                    editProduct(productId);
                });
            });
            
            document.querySelectorAll('.delete-product').forEach(btn => {
                btn.addEventListener('click', function() {
                    const productId = parseInt(this.getAttribute('data-id'));
                    deleteProduct(productId);
                });
            });
        }

        // Filter daftar produk
        function filterProductTable(searchTerm) {
            loadProductTable(searchTerm);
        }

        // Tambah produk baru
        function addNewProduct() {
            alert("Fitur tambah produk akan diimplementasikan di sini.\n\nDalam aplikasi lengkap, akan muncul form modal untuk menambahkan produk baru.");
            
            // Contoh produk baru
            const newProduct = {
                id: sampleProducts.length + 1,
                code: `P${(sampleProducts.length + 1).toString().padStart(3, '0')}`,
                name: "Produk Baru",
                category: "Lainnya",
                price: 10000,
                stock: 50
            };
            
            sampleProducts.push(newProduct);
            loadProductTable();
            loadProducts();
            
            showNotification("Produk berhasil ditambahkan", 'success');
        }

        // Edit produk
        function editProduct(productId) {
            alert(`Fitur edit produk ID ${productId} akan diimplementasikan di sini.\n\nDalam aplikasi lengkap, akan muncul form modal untuk mengedit produk.`);
        }

        // Hapus produk
        function deleteProduct(productId) {
            if (confirm("Apakah Anda yakin ingin menghapus produk ini?")) {
                const index = sampleProducts.findIndex(p => p.id === productId);
                if (index !== -1) {
                    sampleProducts.splice(index, 1);
                    loadProductTable();
                    loadProducts();
                    showNotification("Produk berhasil dihapus", 'success');
                }
            }
        }

        // Load laporan
        function loadReport() {
            const reportTable = document.getElementById('report-table');
            const totalIncome = document.getElementById('total-income');
            const totalTransactions = document.getElementById('total-transactions');
            
            if (!reportTable) return;
            
            // Filter berdasarkan tanggal
            const startDate = document.getElementById('start-date')?.value || '2023-10-01';
            const endDate = document.getElementById('end-date')?.value || '2023-10-31';
            
            // Dalam implementasi nyata, di sini akan ada filter berdasarkan tanggal
            // Untuk contoh, kita gunakan data contoh
            reportTable.innerHTML = '';
            
            let total = 0;
            let transactionCount = 0;
            let currentTransaction = '';
            
            sampleReportData.forEach(item => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${item.date}</td>
                    <td>${item.code}</td>
                    <td>${item.product}</td>
                    <td>${item.quantity}</td>
                    <td>Rp ${item.price.toLocaleString('id-ID')}</td>
                    <td>Rp ${item.total.toLocaleString('id-ID')}</td>
                `;
                reportTable.appendChild(row);
                
                total += item.total;
                if (item.code !== currentTransaction) {
                    transactionCount++;
                    currentTransaction = item.code;
                }
            });
            
            totalIncome.textContent = `Rp ${total.toLocaleString('id-ID')}`;
            totalTransactions.textContent = transactionCount;
        }

        // Load riwayat transaksi
        function loadHistory() {
            const historyTable = document.getElementById('history-table');
            if (!historyTable) return;
            
            historyTable.innerHTML = '';
            
            sampleTransactions.forEach(transaction => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${transaction.date}</td>
                    <td>${transaction.code}</td>
                    <td>${transaction.customer}</td>
                    <td>${transaction.items} item</td>
                    <td>Rp ${transaction.total.toLocaleString('id-ID')}</td>
                    <td>${transaction.cashier}</td>
                    <td>
                        <div class="action-buttons">
                            <button class="btn btn-primary btn-sm view-transaction" data-id="${transaction.id}">
                                <i class="fas fa-eye"></i>
                            </button>
                            <button class="btn btn-success btn-sm print-receipt" data-id="${transaction.id}">
                                <i class="fas fa-print"></i>
                            </button>
                        </div>
                    </td>
                `;
                
                historyTable.appendChild(row);
            });
            
            // Tambah event listeners untuk tombol
            document.querySelectorAll('.view-transaction').forEach(btn => {
                btn.addEventListener('click', function() {
                    const transactionId = parseInt(this.getAttribute('data-id'));
                    viewTransaction(transactionId);
                });
            });
            
            document.querySelectorAll('.print-receipt').forEach(btn => {
                btn.addEventListener('click', function() {
                    const transactionId = parseInt(this.getAttribute('data-id'));
                    printReceipt(transactionId);
                });
            });
        }

        // Lihat detail transaksi
        function viewTransaction(transactionId) {
            alert(`Fitur lihat detail transaksi ID ${transactionId} akan diimplementasikan di sini.\n\nDalam aplikasi lengkap, akan muncul modal dengan detail transaksi.`);
        }

        // Cetak struk
        function printReceipt(transactionId) {
            alert(`Fitur cetak struk untuk transaksi ID ${transactionId} akan diimplementasikan di sini.\n\nDalam aplikasi lengkap, akan muncul preview struk untuk dicetak.`);
        }

        // Export ke CSV
        function exportToCSV() {
            // Dalam implementasi nyata, di sini akan ada logika untuk export ke CSV
            alert("Data laporan berhasil diexport ke format CSV!");
            showNotification("File CSV berhasil diunduh", 'success');
        }

        // Export ke Excel
        function exportToExcel() {
            // Dalam implementasi nyata, di sini akan ada logika untuk export ke Excel
            alert("Data laporan berhasil diexport ke format Excel!");
            showNotification("File Excel berhasil diunduh", 'success');
        }

        // Simpan pengaturan
        function saveSettings() {
            // Dalam implementasi nyata, di sini akan ada penyimpanan ke database/localStorage
            alert("Pengaturan berhasil disimpan!");
            showNotification("Pengaturan berhasil disimpan", 'success');
        }

        // Reset pengaturan
        function resetSettings() {
            if (confirm("Apakah Anda yakin ingin mengembalikan pengaturan ke nilai default?")) {
                document.getElementById('store-name').value = "Toko Makmur Jaya";
                document.getElementById('store-address').value = "Jl. Merdeka No. 123, Jakarta Pusat";
                document.getElementById('store-phone').value = "021-1234567";
                document.getElementById('tax-rate').value = "10";
                document.getElementById('receipt-footer').value = "Terima kasih telah berbelanja di toko kami";
                
                showNotification("Pengaturan berhasil direset", 'success');
            }
        }

        // Tampilkan notifikasi
        function showNotification(message, type = 'info') {
            // Buat elemen notifikasi
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                padding: 15px 20px;
                background-color: ${type === 'success' ? '#2ecc71' : '#3498db'};
                color: white;
                border-radius: 6px;
                box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
                z-index: 9999;
                animation: slideIn 0.3s ease;
                max-width: 300px;
            `;
            
            notification.innerHTML = `
                <div style="display: flex; align-items: center; gap: 10px;">
                    <i class="fas fa-${type === 'success' ? 'check-circle' : 'info-circle'}"></i>
                    <span>${message}</span>
                </div>
            `;
            
            document.body.appendChild(notification);
            
            // Hapus notifikasi setelah 3 detik
            setTimeout(() => {
                notification.style.animation = 'slideOut 0.3s ease';
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
            
            // Tambah style animasi
            const style = document.createElement('style');
            style.textContent = `
                @keyframes slideIn {
                    from { transform: translateX(100%); opacity: 0; }
                    to { transform: translateX(0); opacity: 1; }
                }
                @keyframes slideOut {
                    from { transform: translateX(0); opacity: 1; }
                    to { transform: translateX(100%); opacity: 0; }
                }
            `;
            
            if (!document.querySelector('#notification-styles')) {
                style.id = 'notification-styles';
                document.head.appendChild(style);
            }
        }
    </script>
</body>
</html>
