<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jennaira Group - Sistem Kasir Pro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f8f9fa;
            color: #333;
            display: flex;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* SIDEBAR MENU - TIDAK IKUT SCROLL */
        .sidebar {
            width: 260px;
            background: linear-gradient(180deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            height: 100vh;
            position: fixed;
            overflow-y: auto;
            overflow-x: hidden;
            transition: all 0.3s;
            box-shadow: 3px 0 15px rgba(0, 0, 0, 0.1);
            z-index: 1000;
        }

        .sidebar::-webkit-scrollbar {
            width: 6px;
        }

        .sidebar::-webkit-scrollbar-thumb {
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: 3px;
        }

        .logo-container {
            padding: 25px 20px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            background-color: rgba(0, 0, 0, 0.1);
        }

        .logo-container h1 {
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 5px;
        }

        .logo-container h1 i {
            margin-right: 12px;
            color: #4dabf7;
        }

        .logo-container p {
            font-size: 0.9rem;
            opacity: 0.8;
            margin-top: 5px;
        }

        .date-time {
            padding: 15px 20px;
            text-align: center;
            background-color: rgba(0, 0, 0, 0.15);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }

        .menu {
            padding: 20px 0;
        }

        .menu-item {
            display: flex;
            align-items: center;
            padding: 16px 25px;
            color: #e9ecef;
            text-decoration: none;
            transition: all 0.3s;
            border-left: 5px solid transparent;
            margin-bottom: 2px;
        }

        .menu-item:hover {
            background-color: rgba(255, 255, 255, 0.1);
            border-left-color: #4dabf7;
            color: white;
            padding-left: 30px;
        }

        .menu-item.active {
            background-color: rgba(77, 171, 247, 0.2);
            border-left-color: #4dabf7;
            color: white;
            font-weight: 600;
        }

        .menu-item i {
            width: 25px;
            font-size: 1.2rem;
            margin-right: 15px;
        }

        /* KONTEN UTAMA */
        .main-content {
            flex: 1;
            margin-left: 260px;
            transition: margin-left 0.3s;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* HEADER */
        .header {
            background-color: white;
            padding: 18px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            position: sticky;
            top: 0;
            z-index: 100;
            flex-shrink: 0;
        }

        .header h2 {
            font-size: 1.6rem;
            color: #1e3c72;
            font-weight: 600;
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-avatar {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 1.1rem;
        }

        /* CONTAINER UTAMA */
        .content-container {
            padding: 30px;
            flex-grow: 1;
            overflow-y: auto;
        }

        /* SEARCH BAR */
        .search-container {
            position: relative;
            margin-bottom: 25px;
            max-width: 500px;
        }

        .search-bar {
            width: 100%;
            padding: 14px 20px 14px 50px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 1rem;
            background-color: white;
            transition: all 0.3s;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
        }

        .search-bar:focus {
            outline: none;
            border-color: #4dabf7;
            box-shadow: 0 3px 15px rgba(77, 171, 247, 0.2);
        }

        .search-icon {
            position: absolute;
            left: 18px;
            top: 50%;
            transform: translateY(-50%);
            color: #6c757d;
            font-size: 1.1rem;
        }

        /* CARD */
        .card {
            background-color: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            margin-bottom: 30px;
            border: 1px solid rgba(0, 0, 0, 0.03);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .card-header h3 {
            font-size: 1.4rem;
            color: #1e3c72;
            font-weight: 600;
        }

        /* PRODUK */
        .products-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }

        .product-card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.07);
            transition: all 0.3s;
            cursor: pointer;
            border: 1px solid #f1f3f4;
            display: flex;
            flex-direction: column;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
            border-color: #4dabf7;
        }

        .product-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 15px;
        }

        .product-name {
            font-size: 1.2rem;
            font-weight: 600;
            color: #1e3c72;
            line-height: 1.3;
        }

        .product-code {
            font-size: 0.85rem;
            color: #6c757d;
            background-color: #f8f9fa;
            padding: 3px 8px;
            border-radius: 4px;
        }

        .product-price {
            font-size: 1.4rem;
            font-weight: 700;
            color: #2ecc71;
            margin: 10px 0;
        }

        .product-category {
            display: inline-block;
            font-size: 0.85rem;
            color: #6c757d;
            background-color: #f1f3f4;
            padding: 4px 10px;
            border-radius: 20px;
            margin-bottom: 15px;
        }

        .product-stats {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px dashed #eee;
            font-size: 0.9rem;
        }

        .stock {
            color: #6c757d;
        }

        .stock.low {
            color: #e74c3c;
            font-weight: 600;
        }

        .sold {
            color: #3498db;
        }

        /* STATS DASHBOARD */
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.07);
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

        .stat-info h4 {
            font-size: 1.8rem;
            margin-bottom: 5px;
            color: #1e3c72;
        }

        .stat-info p {
            color: #6c757d;
            font-size: 0.95rem;
        }

        /* TABEL */
        .table-container {
            overflow-x: auto;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: white;
        }

        table thead {
            background-color: #1e3c72;
            color: white;
        }

        table th {
            padding: 16px 15px;
            text-align: left;
            font-weight: 600;
            font-size: 0.95rem;
        }

        table td {
            padding: 14px 15px;
            border-bottom: 1px solid #eee;
            color: #495057;
        }

        table tbody tr:hover {
            background-color: #f8f9fa;
        }

        /* TOMBOL */
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
            font-size: 0.95rem;
        }

        .btn-primary {
            background-color: #4dabf7;
            color: white;
        }

        .btn-primary:hover {
            background-color: #339af0;
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
            background-color: #e67e22;
        }

        .btn-danger {
            background-color: #e74c3c;
            color: white;
        }

        .btn-danger:hover {
            background-color: #c0392b;
        }

        /* KASIR INTERFACE */
        .cashier-container {
            display: grid;
            grid-template-columns: 1fr 400px;
            gap: 30px;
        }

        .cart-container {
            background-color: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            height: fit-content;
            position: sticky;
            top: 100px;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .cart-items {
            max-height: 400px;
            overflow-y: auto;
            margin-bottom: 20px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid #f8f9fa;
        }

        .cart-item-info h4 {
            margin-bottom: 5px;
            color: #1e3c72;
        }

        .cart-item-price {
            color: #6c757d;
            font-size: 0.95rem;
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
            background-color: #f8f9fa;
            padding: 5px 10px;
            border-radius: 6px;
        }

        .quantity-btn {
            width: 28px;
            height: 28px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #e9ecef;
            cursor: pointer;
            font-weight: bold;
        }

        .cart-summary {
            border-top: 2px solid #eee;
            padding-top: 20px;
            margin-top: 20px;
        }

        .summary-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 12px;
            color: #6c757d;
        }

        .summary-total {
            display: flex;
            justify-content: space-between;
            font-size: 1.3rem;
            font-weight: 700;
            color: #1e3c72;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px dashed #ddd;
        }

        /* NOTIFIKASI */
        .notification {
            position: fixed;
            bottom: 30px;
            right: 30px;
            padding: 15px 25px;
            background-color: #2ecc71;
            color: white;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 12px;
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.4s;
        }

        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }

        /* RESPONSIF */
        @media (max-width: 1200px) {
            .cashier-container {
                grid-template-columns: 1fr;
            }
            
            .cart-container {
                position: static;
            }
        }

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
            
            .logo-container h1 span {
                display: none;
            }
            
            .logo-container p {
                display: none;
            }
            
            .date-time {
                font-size: 0.8rem;
                padding: 10px;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
                padding: 15px;
            }
            
            .header-actions {
                width: 100%;
                justify-content: space-between;
            }
            
            .content-container {
                padding: 20px;
            }
            
            .stats-container {
                grid-template-columns: 1fr;
            }
            
            .products-container {
                grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            }
        }

        @media (max-width: 576px) {
            .sidebar {
                transform: translateX(-100%);
                width: 280px;
            }
            
            .sidebar.active {
                transform: translateX(0);
            }
            
            .main-content {
                margin-left: 0;
            }
            
            .menu-toggle {
                display: block;
            }
            
            .products-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- SIDEBAR MENU (TIDAK IKUT SCROLL) -->
    <div class="sidebar">
        <div class="logo-container">
            <h1><i class="fas fa-cash-register"></i> <span>KASIR PRO</span></h1>
            <p>Sistem Kasir Lengkap untuk UMKM</p>
        </div>
        
        <div class="date-time" id="currentDateTime">
            <!-- Waktu akan diisi oleh JavaScript -->
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
                <i class="fas fa-history"></i> <span>Riwayat Transaksi</span>
            </a>
            <a href="#" class="menu-item" data-page="pengaturan">
                <i class="fas fa-cog"></i> <span>Pengaturan</span>
            </a>
        </div>
    </div>

    <!-- KONTEN UTAMA -->
    <div class="main-content">
        <!-- HEADER -->
        <div class="header">
            <h2 id="pageTitle">Dashboard</h2>
            <div class="header-actions">
                <div class="search-container">
                    <i class="fas fa-search search-icon"></i>
                    <input type="text" class="search-bar" id="globalSearch" placeholder="Cari produk, transaksi, laporan...">
                </div>
                <div class="user-info">
                    <div class="user-avatar">AD</div>
                    <div>
                        <h4 style="font-size: 1rem; color: #1e3c72;">Admin</h4>
                        <p style="font-size: 0.85rem; color: #6c757d;">Super Admin</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- CONTAINER KONTEN -->
        <div class="content-container">
            <!-- DASHBOARD -->
            <div id="dashboardPage" class="page active">
                <div class="stats-container">
                    <div class="stat-card">
                        <div class="stat-icon" style="background: linear-gradient(135deg, #4dabf7, #339af0);">
                            <i class="fas fa-dollar-sign"></i>
                        </div>
                        <div class="stat-info">
                            <h4 id="totalSales">Rp 12.450.000</h4>
                            <p>Total Penjualan</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background: linear-gradient(135deg, #2ecc71, #27ae60);">
                            <i class="fas fa-shopping-cart"></i>
                        </div>
                        <div class="stat-info">
                            <h4 id="totalTransactions">48</h4>
                            <p>Jumlah Transaksi</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background: linear-gradient(135deg, #f39c12, #e67e22);">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <div class="stat-info">
                            <h4 id="avgTransaction">Rp 259.375</h4>
                            <p>Rata-rata per Transaksi</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon" style="background: linear-gradient(135deg, #e74c3c, #c0392b);">
                            <i class="fas fa-box"></i>
                        </div>
                        <div class="stat-info">
                            <h4 id="totalItemsSold">1.594</h4>
                            <p>Item Terjual</p>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3>Aktivitas Terbaru</h3>
                        <button class="btn btn-primary">Lihat Semua</button>
                    </div>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Tanggal</th>
                                    <th>No. Transaksi</th>
                                    <th>Produk</th>
                                    <th>Qty</th>
                                    <th>Total</th>
                                    <th>Kasir</th>
                                </tr>
                            </thead>
                            <tbody id="recentActivities">
                                <!-- Data akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- KASIR -->
            <div id="kasirPage" class="page">
                <div class="cashier-container">
                    <div>
                        <div class="search-container">
                            <i class="fas fa-search search-icon"></i>
                            <input type="text" class="search-bar" id="productSearch" placeholder="Cari produk berdasarkan nama, kode, atau kategori...">
                        </div>
                        
                        <div class="products-container" id="productList">
                            <!-- Produk akan diisi oleh JavaScript -->
                        </div>
                    </div>
                    
                    <div class="cart-container">
                        <div class="cart-header">
                            <h3>Keranjang Belanja</h3>
                            <button class="btn btn-danger btn-sm" id="clearCart">Kosongkan</button>
                        </div>
                        
                        <div class="cart-items" id="cartItems">
                            <!-- Item keranjang akan diisi oleh JavaScript -->
                            <p style="text-align: center; color: #6c757d; padding: 30px 0;">Keranjang belanja kosong</p>
                        </div>
                        
                        <div class="cart-summary">
                            <div class="summary-row">
                                <span>Subtotal:</span>
                                <span id="cartSubtotal">Rp 0</span>
                            </div>
                            <div class="summary-row">
                                <span>Pajak (10%):</span>
                                <span id="cartTax">Rp 0</span>
                            </div>
                            <div class="summary-total">
                                <span>Total:</span>
                                <span id="cartTotal">Rp 0</span>
                            </div>
                            
                            <div style="margin-top: 25px;">
                                <button class="btn btn-success" style="width: 100%; padding: 15px; font-size: 1.1rem;" id="checkoutBtn">
                                    <i class="fas fa-check-circle"></i> Proses Pembayaran
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- PRODUK & STOK -->
            <div id="produkPage" class="page">
                <div class="card">
                    <div class="card-header">
                        <h3>Manajemen Produk & Stok</h3>
                        <button class="btn btn-primary" id="addProductBtn">
                            <i class="fas fa-plus"></i> Tambah Produk
                        </button>
                    </div>
                    
                    <div class="search-container">
                        <i class="fas fa-search search-icon"></i>
                        <input type="text" class="search-bar" id="productListSearch" placeholder="Cari produk berdasarkan nama, kode, atau kategori...">
                    </div>
                    
                    <div class="products-container" id="productManagementList">
                        <!-- Produk akan diisi oleh JavaScript -->
                    </div>
                </div>
            </div>

            <!-- LAPORAN -->
            <div id="laporanPage" class="page">
                <div class="card">
                    <div class="card-header">
                        <h3>Laporan Penjualan</h3>
                        <div>
                            <button class="btn btn-success" id="exportCsv">
                                <i class="fas fa-file-csv"></i> Export CSV
                            </button>
                            <button class="btn btn-success" id="exportExcel">
                                <i class="fas fa-file-excel"></i> Export Excel
                            </button>
                        </div>
                    </div>
                    
                    <div style="display: flex; gap: 15px; margin-bottom: 25px; flex-wrap: wrap;">
                        <div style="flex: 1; min-width: 200px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Dari Tanggal</label>
                            <input type="date" class="search-bar" style="padding: 12px 15px;" id="startDate" value="2023-10-01">
                        </div>
                        <div style="flex: 1; min-width: 200px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Sampai Tanggal</label>
                            <input type="date" class="search-bar" style="padding: 12px 15px;" id="endDate" value="2023-10-31">
                        </div>
                        <div style="display: flex; align-items: flex-end;">
                            <button class="btn btn-primary" id="filterReport">
                                <i class="fas fa-filter"></i> Filter Laporan
                            </button>
                        </div>
                    </div>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>No</th>
                                    <th>Tanggal</th>
                                    <th>No. Transaksi</th>
                                    <th>Produk</th>
                                    <th>Qty</th>
                                    <th>Total</th>
                                    <th>Kasir</th>
                                </tr>
                            </thead>
                            <tbody id="reportTable">
                                <!-- Data laporan akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- RIWAYAT TRANSAKSI -->
            <div id="riwayatPage" class="page">
                <div class="card">
                    <div class="card-header">
                        <h3>Riwayat Transaksi</h3>
                        <button class="btn btn-primary">Refresh</button>
                    </div>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>No</th>
                                    <th>Tanggal</th>
                                    <th>ID Transaksi</th>
                                    <th>Items</th>
                                    <th>Total</th>
                                    <th>Bayar</th>
                                    <th>Kembali</th>
                                    <th>Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="historyTable">
                                <!-- Data riwayat akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- PENGATURAN -->
            <div id="pengaturanPage" class="page">
                <div class="card">
                    <div class="card-header">
                        <h3>Pengaturan Aplikasi</h3>
                    </div>
                    
                    <div style="max-width: 600px;">
                        <div style="margin-bottom: 20px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Nama Toko</label>
                            <input type="text" class="search-bar" style="padding: 12px 15px;" id="storeName" value="Jennaira Group">
                        </div>
                        
                        <div style="margin-bottom: 20px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Alamat Toko</label>
                            <textarea class="search-bar" style="padding: 12px 15px; min-height: 100px; resize: vertical;" id="storeAddress">Jl. Raya Contoh No. 123, Jakarta Selatan</textarea>
                        </div>
                        
                        <div style="margin-bottom: 20px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Telepon</label>
                            <input type="text" class="search-bar" style="padding: 12px 15px;" id="storePhone" value="021-12345678">
                        </div>
                        
                        <div style="margin-bottom: 20px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Pajak (%)</label>
                            <input type="number" class="search-bar" style="padding: 12px 15px;" id="taxRate" value="10" min="0" max="100">
                        </div>
                        
                        <div style="margin-bottom: 20px;">
                            <label style="display: block; margin-bottom: 8px; color: #495057; font-weight: 500;">Nota Footer</label>
                            <textarea class="search-bar" style="padding: 12px 15px; min-height: 80px; resize: vertical;" id="receiptFooter">Terima kasih telah berbelanja di Jennaira Group</textarea>
                        </div>
                        
                        <div style="margin-top: 30px;">
                            <button class="btn btn-primary" id="saveSettings">
                                <i class="fas fa-save"></i> Simpan Pengaturan
                            </button>
                            <button class="btn btn-warning" id="resetSettings" style="margin-left: 10px;">
                                <i class="fas fa-undo"></i> Reset
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- NOTIFIKASI -->
    <div class="notification" id="notification">
        <i class="fas fa-check-circle"></i>
        <span id="notificationMessage">Pesan notifikasi</span>
    </div>

    <script>
        // Data produk berdasarkan URL yang diberikan
        const products = [
            { id: 1, code: "BR001", name: "Beras 5kg", category: "Sembako • pack", price: 60000, stock: 45, sold: 125 },
            { id: 2, code: "MG002", name: "Minyak Goreng 2L", category: "Sembako • botol", price: 35000, stock: 28, sold: 89 },
            { id: 3, code: "GP003", name: "Gula Pasir 1kg", category: "Sembako • kg", price: 15000, stock: 12, sold: 156 },
            { id: 4, code: "TL004", name: "Telur 1kg", category: "Sembako • kg", price: 28000, stock: 8, sold: 67 },
            { id: 5, code: "SB005", name: "Sabun Mandi", category: "Kebersihan • pcs", price: 5000, stock: 120, sold: 234 },
            { id: 6, code: "SP006", name: "Shampoo", category: "Kebersihan • botol", price: 12000, stock: 35, sold: 78 },
            { id: 7, code: "AM007", name: "Air Mineral 600ml", category: "Minuman • botol", price: 3000, stock: 150, sold: 345 },
            { id: 8, code: "KS008", name: "Kopi Sachet", category: "Minuman • pcs", price: 2000, stock: 89, sold: 289 },
            { id: 9, code: "TC009", name: "Teh Celup", category: "Minuman • pcs", price: 1500, stock: 65, sold: 167 },
            { id: 10, code: "BS010", name: "Biskuit", category: "Snack • pack", price: 8000, stock: 42, sold: 134 }
        ];

        // Data transaksi contoh
        const transactions = [
            { id: 1, date: "2023-10-25 14:30", code: "TRX-001245", items: 3, total: 325000, payment: 350000, change: 25000, cashier: "Admin" },
            { id: 2, date: "2023-10-25 13:15", code: "TRX-001244", items: 2, total: 150000, payment: 200000, change: 50000, cashier: "Admin" },
            { id: 3, date: "2023-10-25 11:45", code: "TRX-001243", items: 5, total: 1250000, payment: 1500000, change: 250000, cashier: "Admin" },
            { id: 4, date: "2023-10-25 10:20", code: "TRX-001242", items: 1, total: 85000, payment: 100000, change: 15000, cashier: "Admin" },
            { id: 5, date: "2023-10-24 16:45", code: "TRX-001241", items: 4, total: 220000, payment: 250000, change: 30000, cashier: "Admin" }
        ];

        // Data laporan contoh
        const reportData = [
            { id: 1, date: "2023-10-25", code: "TRX-001245", product: "Beras 5kg", quantity: 2, total: 120000, cashier: "Admin" },
            { id: 2, date: "2023-10-25", code: "TRX-001245", product: "Minyak Goreng 2L", quantity: 1, total: 35000, cashier: "Admin" },
            { id: 3, date: "2023-10-25", code: "TRX-001245", product: "Gula Pasir 1kg", quantity: 3, total: 45000, cashier: "Admin" },
            { id: 4, date: "2023-10-25", code: "TRX-001244", product: "Shampoo", quantity: 2, total: 24000, cashier: "Admin" },
            { id: 5, date: "2023-10-25", code: "TRX-001244", product: "Sabun Mandi", quantity: 5, total: 25000, cashier: "Admin" }
        ];

        // Data aktivitas terbaru
        const recentActivities = [
            { date: "2023-10-25 14:30", code: "TRX-001245", product: "Beras 5kg, Minyak Goreng, Gula", quantity: 6, total: 200000, cashier: "Admin" },
            { date: "2023-10-25 13:15", code: "TRX-001244", product: "Shampoo, Sabun Mandi", quantity: 7, total: 49000, cashier: "Admin" },
            { date: "2023-10-25 11:45", code: "TRX-001243", product: "Beras 5kg, Telur, Minyak", quantity: 10, total: 450000, cashier: "Admin" },
            { date: "2023-10-25 10:20", code: "TRX-001242", product: "Air Mineral", quantity: 15, total: 45000, cashier: "Admin" },
            { date: "2023-10-24 16:45", code: "TRX-001241", product: "Kopi, Teh, Biskuit", quantity: 12, total: 42000, cashier: "Admin" }
        ];

        // Variabel global
        let cart = [];
        let currentPage = "dashboard";

        // Inisialisasi aplikasi
        document.addEventListener('DOMContentLoaded', function() {
            // Update waktu
            updateDateTime();
            setInterval(updateDateTime, 1000);
            
            // Setup menu navigasi
            setupNavigation();
            
            // Load data awal
            loadDashboard();
            loadProducts();
            loadProductManagement();
            loadReport();
            loadHistory();
            
            // Setup event listeners
            setupEventListeners();
        });

        // Update waktu dan tanggal
        function updateDateTime() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            };
            const dateStr = now.toLocaleDateString('id-ID', options);
            const timeStr = now.toLocaleTimeString('id-ID');
            
            document.getElementById('currentDateTime').innerHTML = `
                <div>${dateStr}</div>
                <div style="font-weight: bold; margin-top: 5px;">${timeStr}</div>
            `;
        }

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
            const pages = document.querySelectorAll('.page');
            pages.forEach(page => page.classList.remove('active'));
            
            // Tampilkan halaman yang dipilih
            const activePage = document.getElementById(`${pageId}Page`);
            if (activePage) {
                activePage.classList.add('active');
            }
            
            // Update judul halaman
            const pageTitle = document.getElementById('pageTitle');
            const pageTitles = {
                dashboard: "Dashboard",
                kasir: "Kasir",
                produk: "Produk & Stok",
                laporan: "Laporan",
                riwayat: "Riwayat Transaksi",
                pengaturan: "Pengaturan"
            };
            
            pageTitle.textContent = pageTitles[pageId] || "Dashboard";
            currentPage = pageId;
            
            // Refresh data halaman jika diperlukan
            if (pageId === 'dashboard') loadDashboard();
            if (pageId === 'kasir') loadProducts();
            if (pageId === 'produk') loadProductManagement();
            if (pageId === 'laporan') loadReport();
            if (pageId === 'riwayat') loadHistory();
        }

        // Setup event listeners
        function setupEventListeners() {
            // Search bar global
            const globalSearch = document.getElementById('globalSearch');
            if (globalSearch) {
                globalSearch.addEventListener('input', function() {
                    performGlobalSearch(this.value);
                });
            }
            
            // Search bar untuk produk di halaman kasir
            const productSearch = document.getElementById('productSearch');
            if (productSearch) {
                productSearch.addEventListener('input', function() {
                    filterProducts(this.value);
                });
            }
            
            // Search bar untuk produk di halaman daftar produk
            const productListSearch = document.getElementById('productListSearch');
            if (productListSearch) {
                productListSearch.addEventListener('input', function() {
                    filterProductManagement(this.value);
                });
            }
            
            // Tombol checkout
            const checkoutBtn = document.getElementById('checkoutBtn');
            if (checkoutBtn) {
                checkoutBtn.addEventListener('click', processCheckout);
            }
            
            // Tombol kosongkan keranjang
            const clearCartBtn = document.getElementById('clearCart');
            if (clearCartBtn) {
                clearCartBtn.addEventListener('click', clearCart);
            }
            
            // Tombol tambah produk
            const addProductBtn = document.getElementById('addProductBtn');
            if (addProductBtn) {
                addProductBtn.addEventListener('click', addNewProduct);
            }
            
            // Tombol export
            const exportCsvBtn = document.getElementById('exportCsv');
            if (exportCsvBtn) {
                exportCsvBtn.addEventListener('click', exportToCSV);
            }
            
            const exportExcelBtn = document.getElementById('exportExcel');
            if (exportExcelBtn) {
                exportExcelBtn.addEventListener('click', exportToExcel);
            }
            
            // Tombol filter laporan
            const filterReportBtn = document.getElementById('filterReport');
            if (filterReportBtn) {
                filterReportBtn.addEventListener('click', loadReport);
            }
            
            // Tombol simpan pengaturan
            const saveSettingsBtn = document.getElementById('saveSettings');
            if (saveSettingsBtn) {
                saveSettingsBtn.addEventListener('click', saveSettings);
            }
            
            // Tombol reset pengaturan
            const resetSettingsBtn = document.getElementById('resetSettings');
            if (resetSettingsBtn) {
                resetSettingsBtn.addEventListener('click', resetSettings);
            }
        }

        // Search global
        function performGlobalSearch(searchTerm) {
            const term = searchTerm.toLowerCase().trim();
            
            if (term.length === 0) {
                // Jika search kosong, tampilkan halaman normal
                showPage(currentPage);
                return;
            }
            
            // Cari di produk
            const filteredProducts = products.filter(product => 
                product.name.toLowerCase().includes(term) || 
                product.code.toLowerCase().includes(term) ||
                product.category.toLowerCase().includes(term)
            );
            
            // Cari di transaksi
            const filteredTransactions = transactions.filter(transaction => 
                transaction.code.toLowerCase().includes(term)
            );
            
            // Tampilkan hasil pencarian
            showSearchResults(filteredProducts, filteredTransactions, term);
        }

        // Tampilkan hasil pencarian
        function showSearchResults(productsResult, transactionsResult, searchTerm) {
            // Sembunyikan semua halaman
            const pages = document.querySelectorAll('.page');
            pages.forEach(page => page.classList.remove('active'));
            
            // Buat halaman hasil pencarian
            let searchResultsPage = document.getElementById('searchResultsPage');
            if (!searchResultsPage) {
                searchResultsPage = document.createElement('div');
                searchResultsPage.id = 'searchResultsPage';
                searchResultsPage.className = 'page';
                document.querySelector('.content-container').appendChild(searchResultsPage);
            }
            
            searchResultsPage.innerHTML = '';
            searchResultsPage.classList.add('active');
            
            // Update judul halaman
            document.getElementById('pageTitle').textContent = `Hasil Pencarian: "${searchTerm}"`;
            
            // Tampilkan hasil produk
            if (productsResult.length > 0) {
                const productsSection = document.createElement('div');
                productsSection.className = 'card';
                productsSection.innerHTML = `
                    <div class="card-header">
                        <h3>Produk (${productsResult.length} ditemukan)</h3>
                    </div>
                    <div class="products-container" id="searchProductResults">
                    </div>
                `;
                searchResultsPage.appendChild(productsSection);
                
                const productsContainer = productsSection.querySelector('#searchProductResults');
                productsResult.forEach(product => {
                    const productCard = createProductCard(product, false);
                    productsContainer.appendChild(productCard);
                });
            }
            
            // Tampilkan hasil transaksi
            if (transactionsResult.length > 0) {
                const transactionsSection = document.createElement('div');
                transactionsSection.className = 'card';
                transactionsSection.innerHTML = `
                    <div class="card-header">
                        <h3>Transaksi (${transactionsResult.length} ditemukan)</h3>
                    </div>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Tanggal</th>
                                    <th>ID Transaksi</th>
                                    <th>Items</th>
                                    <th>Total</th>
                                    <th>Kasir</th>
                                </tr>
                            </thead>
                            <tbody id="searchTransactionResults">
                            </tbody>
                        </table>
                    </div>
                `;
                searchResultsPage.appendChild(transactionsSection);
                
                const transactionsContainer = transactionsSection.querySelector('#searchTransactionResults');
                transactionsResult.forEach((transaction, index) => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${transaction.date}</td>
                        <td>${transaction.code}</td>
                        <td>${transaction.items} item</td>
                        <td>Rp ${transaction.total.toLocaleString('id-ID')}</td>
                        <td>${transaction.cashier}</td>
                    `;
                    transactionsContainer.appendChild(row);
                });
            }
            
            // Jika tidak ada hasil
            if (productsResult.length === 0 && transactionsResult.length === 0) {
                const noResultsSection = document.createElement('div');
                noResultsSection.className = 'card';
                noResultsSection.innerHTML = `
                    <div style="text-align: center; padding: 40px 20px;">
                        <i class="fas fa-search" style="font-size: 3rem; color: #6c757d; margin-bottom: 20px;"></i>
                        <h3 style="color: #6c757d; margin-bottom: 10px;">Tidak ada hasil ditemukan</h3>
                        <p style="color: #6c757d;">Tidak ada produk atau transaksi yang sesuai dengan pencarian "${searchTerm}"</p>
                    </div>
                `;
                searchResultsPage.appendChild(noResultsSection);
            }
        }

        // Load dashboard
        function loadDashboard() {
            // Hitung total penjualan dari transaksi
            const totalSales = transactions.reduce((sum, transaction) => sum + transaction.total, 0);
            const totalTransactions = transactions.length;
            const avgTransaction = totalTransactions > 0 ? totalSales / totalTransactions : 0;
            
            // Hitung total item terjual dari produk
            const totalItemsSold = products.reduce((sum, product) => sum + product.sold, 0);
            
            // Update statistik
            document.getElementById('totalSales').textContent = `Rp ${totalSales.toLocaleString('id-ID')}`;
            document.getElementById('totalTransactions').textContent = totalTransactions;
            document.getElementById('avgTransaction').textContent = `Rp ${Math.round(avgTransaction).toLocaleString('id-ID')}`;
            document.getElementById('totalItemsSold').textContent = totalItemsSold.toLocaleString('id-ID');
            
            // Load aktivitas terbaru
            const recentActivitiesTable = document.getElementById('recentActivities');
            if (recentActivitiesTable) {
                recentActivitiesTable.innerHTML = '';
                
                recentActivities.forEach(activity => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${activity.date}</td>
                        <td>${activity.code}</td>
                        <td>${activity.product}</td>
                        <td>${activity.quantity}</td>
                        <td>Rp ${activity.total.toLocaleString('id-ID')}</td>
                        <td>${activity.cashier}</td>
                    `;
                    recentActivitiesTable.appendChild(row);
                });
            }
        }

        // Buat kartu produk
        function createProductCard(product, isForKasir = true) {
            const productCard = document.createElement('div');
            productCard.className = 'product-card';
            productCard.setAttribute('data-id', product.id);
            
            const stockClass = product.stock < 10 ? 'stock low' : 'stock';
            
            productCard.innerHTML = `
                <div class="product-header">
                    <div class="product-name">${product.name}</div>
                    <div class="product-code">${product.code}</div>
                </div>
                <div class="product-price">Rp ${product.price.toLocaleString('id-ID')}</div>
                <div class="product-category">${product.category}</div>
                <div class="product-stats">
                    <div class="${stockClass}">Stok: ${product.stock}</div>
                    <div class="sold">Terjual: ${product.sold}</div>
                </div>
            `;
            
            if (isForKasir) {
                productCard.addEventListener('click', () => addToCart(product));
            } else {
                // Untuk halaman manajemen produk, tambahkan tombol aksi
                const actionDiv = document.createElement('div');
                actionDiv.style.marginTop = '15px';
                actionDiv.style.display = 'flex';
                actionDiv.style.gap = '10px';
                actionDiv.innerHTML = `
                    <button class="btn btn-warning btn-sm edit-product-btn" data-id="${product.id}" style="padding: 8px 12px; font-size: 0.85rem;">
                        <i class="fas fa-edit"></i> Edit
                    </button>
                    <button class="btn btn-danger btn-sm delete-product-btn" data-id="${product.id}" style="padding: 8px 12px; font-size: 0.85rem;">
                        <i class="fas fa-trash"></i> Hapus
                    </button>
                `;
                productCard.appendChild(actionDiv);
                
                // Tambahkan event listener untuk tombol edit dan hapus
                productCard.querySelector('.edit-product-btn').addEventListener('click', (e) => {
                    e.stopPropagation();
                    editProduct(product.id);
                });
                
                productCard.querySelector('.delete-product-btn').addEventListener('click', (e) => {
                    e.stopPropagation();
                    deleteProduct(product.id);
                });
            }
            
            return productCard;
        }

        // Load produk untuk halaman kasir
        function loadProducts() {
            const productList = document.getElementById('productList');
            if (!productList) return;
            
            productList.innerHTML = '';
            
            products.forEach(product => {
                const productCard = createProductCard(product, true);
                productList.appendChild(productCard);
            });
        }

        // Filter produk di halaman kasir
        function filterProducts(searchTerm) {
            const productList = document.getElementById('productList');
            if (!productList) return;
            
            productList.innerHTML = '';
            
            const term = searchTerm.toLowerCase();
            let filteredProducts = products;
            
            if (term) {
                filteredProducts = products.filter(product => 
                    product.name.toLowerCase().includes(term) || 
                    product.code.toLowerCase().includes(term) ||
                    product.category.toLowerCase().includes(term)
                );
            }
            
            if (filteredProducts.length === 0) {
                productList.innerHTML = `
                    <div style="grid-column: 1 / -1; text-align: center; padding: 40px 20px;">
                        <i class="fas fa-search" style="font-size: 3rem; color: #6c757d; margin-bottom: 20px;"></i>
                        <h3 style="color: #6c757d; margin-bottom: 10px;">Tidak ada produk ditemukan</h3>
                        <p style="color: #6c757d;">Tidak ada produk yang sesuai dengan pencarian "${searchTerm}"</p>
                    </div>
                `;
                return;
            }
            
            filteredProducts.forEach(product => {
                const productCard = createProductCard(product, true);
                productList.appendChild(productCard);
            });
        }

        // Load produk untuk halaman manajemen produk
        function loadProductManagement() {
            const productManagementList = document.getElementById('productManagementList');
            if (!productManagementList) return;
            
            productManagementList.innerHTML = '';
            
            products.forEach(product => {
                const productCard = createProductCard(product, false);
                productManagementList.appendChild(productCard);
            });
        }

        // Filter produk di halaman manajemen
        function filterProductManagement(searchTerm) {
            const productManagementList = document.getElementById('productManagementList');
            if (!productManagementList) return;
            
            productManagementList.innerHTML = '';
            
            const term = searchTerm.toLowerCase();
            let filteredProducts = products;
            
            if (term) {
                filteredProducts = products.filter(product => 
                    product.name.toLowerCase().includes(term) || 
                    product.code.toLowerCase().includes(term) ||
                    product.category.toLowerCase().includes(term)
                );
            }
            
            if (filteredProducts.length === 0) {
                productManagementList.innerHTML = `
                    <div style="grid-column: 1 / -1; text-align: center; padding: 40px 20px;">
                        <i class="fas fa-search" style="font-size: 3rem; color: #6c757d; margin-bottom: 20px;"></i>
                        <h3 style="color: #6c757d; margin-bottom: 10px;">Tidak ada produk ditemukan</h3>
                        <p style="color: #6c757d;">Tidak ada produk yang sesuai dengan pencarian "${searchTerm}"</p>
                    </div>
                `;
                return;
            }
            
            filteredProducts.forEach(product => {
                const productCard = createProductCard(product, false);
                productManagementList.appendChild(productCard);
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
                    showNotification(`Stok ${product.name} tidak mencukupi!`, 'error');
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
                        code: product.code
                    });
                } else {
                    showNotification(`Stok ${product.name} habis!`, 'error');
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
            const cartItems = document.getElementById('cartItems');
            const cartSubtotal = document.getElementById('cartSubtotal');
            const cartTax = document.getElementById('cartTax');
            const cartTotal = document.getElementById('cartTotal');
            
            if (cart.length === 0) {
                cartItems.innerHTML = '<p style="text-align: center; color: #6c757d; padding: 30px 0;">Keranjang belanja kosong</p>';
                cartSubtotal.textContent = 'Rp 0';
                cartTax.textContent = 'Rp 0';
                cartTotal.textContent = 'Rp 0';
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
            cartSubtotal.textContent = `Rp ${subtotal.toLocaleString('id-ID')}`;
            cartTax.textContent = `Rp ${tax.toLocaleString('id-ID')}`;
            cartTotal.textContent = `Rp ${total.toLocaleString('id-ID')}`;
            
            // Tampilkan item keranjang
            cartItems.innerHTML = '';
            cart.forEach(item => {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div class="cart-item-info">
                        <h4>${item.name}</h4>
                        <div class="cart-item-price">Rp ${item.price.toLocaleString('id-ID')} × ${item.quantity}</div>
                    </div>
                    <div class="cart-item-actions">
                        <div class="quantity-control">
                            <div class="quantity-btn minus" data-id="${item.id}">
                                <i class="fas fa-minus"></i>
                            </div>
                            <span style="font-weight: bold; min-width: 30px; text-align: center;">${item.quantity}</span>
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
                const product = products.find(p => p.id === productId);
                if (item.quantity < product.stock) {
                    item.quantity++;
                    updateCartDisplay();
                } else {
                    showNotification(`Stok ${product.name} tidak mencukupi!`, 'error');
                }
            }
        }

        // Hapus produk dari keranjang
        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartDisplay();
            showNotification("Produk dihapus dari keranjang");
        }

        // Kosongkan keranjang
        function clearCart() {
            if (cart.length === 0) return;
            
            if (confirm("Apakah Anda yakin ingin mengosongkan keranjang belanja?")) {
                cart = [];
                updateCartDisplay();
                showNotification("Keranjang belanja dikosongkan");
            }
        }

        // Proses checkout
        function processCheckout() {
            if (cart.length === 0) {
                showNotification("Keranjang belanja kosong!", 'error');
                return;
            }
            
            // Hitung total
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const tax = subtotal * 0.1;
            const total = subtotal + tax;
            
            // Tampilkan dialog pembayaran
            const payment = prompt(`Total belanja: Rp ${total.toLocaleString('id-ID')}\n\nMasukkan jumlah uang yang dibayarkan:`, total);
            
            if (payment === null) return;
            
            const paymentAmount = parseFloat(payment.replace(/[^0-9]/g, ''));
            
            if (isNaN(paymentAmount) || paymentAmount < total) {
                showNotification("Jumlah pembayaran tidak valid atau kurang!", 'error');
                return;
            }
            
            const change = paymentAmount - total;
            
            // Generate nomor transaksi
            const transactionCode = `TRX-${Date.now().toString().slice(-6)}`;
            
            // Simpan transaksi
            const transaction = {
                id: transactions.length + 1,
                date: new Date().toLocaleString('id-ID'),
                code: transactionCode,
                items: cart.reduce((sum, item) => sum + item.quantity, 0),
                total: total,
                payment: paymentAmount,
                change: change,
                cashier: "Admin"
            };
            
            transactions.unshift(transaction);
            
            // Kurangi stok produk
            cart.forEach(cartItem => {
                const product = products.find(p => p.id === cartItem.id);
                if (product) {
                    product.stock -= cartItem.quantity;
                    product.sold += cartItem.quantity;
                }
            });
            
            // Tambahkan ke laporan
            cart.forEach(cartItem => {
                const product = products.find(p => p.id === cartItem.id);
                reportData.unshift({
                    id: reportData.length + 1,
                    date: new Date().toISOString().split('T')[0],
                    code: transactionCode,
                    product: product.name,
                    quantity: cartItem.quantity,
                    total: cartItem.price * cartItem.quantity,
                    cashier: "Admin"
                });
            });
            
            // Tambahkan ke aktivitas terbaru
            const productNames = cart.map(item => item.name).join(', ');
            recentActivities.unshift({
                date: new Date().toLocaleString('id-ID'),
                code: transactionCode,
                product: productNames.length > 50 ? productNames.substring(0, 47) + '...' : productNames,
                quantity: cart.reduce((sum, item) => sum + item.quantity, 0),
                total: total,
                cashier: "Admin"
            });
            
            // Reset keranjang
            cart = [];
            updateCartDisplay();
            
            // Tampilkan notifikasi
            showNotification(`Transaksi ${transactionCode} berhasil! Kembalian: Rp ${change.toLocaleString('id-ID')}`, 'success');
            
            // Update dashboard
            loadDashboard();
            
            // Tampilkan struk
            showReceipt(transaction, cart);
        }

        // Tampilkan struk
        function showReceipt(transaction, cartItems) {
            const receiptWindow = window.open('', '_blank', 'width=400,height=600');
            
            const receiptContent = `
                <!DOCTYPE html>
                <html>
                <head>
                    <title>Struk #${transaction.code}</title>
                    <style>
                        body { font-family: 'Courier New', monospace; padding: 20px; }
                        .receipt { max-width: 300px; margin: 0 auto; }
                        .header { text-align: center; margin-bottom: 20px; border-bottom: 1px dashed #000; padding-bottom: 10px; }
                        .store-name { font-size: 18px; font-weight: bold; }
                        .transaction-info { margin: 15px 0; }
                        .items { width: 100%; border-collapse: collapse; margin: 15px 0; }
                        .items th { border-bottom: 1px dashed #000; padding: 5px 0; text-align: left; }
                        .items td { padding: 5px 0; }
                        .total { border-top: 2px solid #000; padding-top: 10px; margin-top: 10px; }
                        .footer { text-align: center; margin-top: 20px; font-size: 12px; }
                    </style>
                </head>
                <body>
                    <div class="receipt">
                        <div class="header">
                            <div class="store-name">${document.getElementById('storeName').value || 'Jennaira Group'}</div>
                            <div>${document.getElementById('storeAddress').value || 'Jl. Raya Contoh No. 123, Jakarta Selatan'}</div>
                            <div>Telp: ${document.getElementById('storePhone').value || '021-12345678'}</div>
                        </div>
                        <div class="transaction-info">
                            <div>No: ${transaction.code}</div>
                            <div>Tanggal: ${transaction.date}</div>
                            <div>Kasir: ${transaction.cashier}</div>
                        </div>
                        <table class="items">
                            <thead>
                                <tr>
                                    <th>Item</th>
                                    <th>Qty</th>
                                    <th>Total</th>
                                </tr>
                            </thead>
                            <tbody>
                                ${cartItems.map(item => `
                                    <tr>
                                        <td>${item.name}</td>
                                        <td>${item.quantity}</td>
                                        <td>Rp ${(item.price * item.quantity).toLocaleString('id-ID')}</td>
                                    </tr>
                                `).join('')}
                            </tbody>
                        </table>
                        <div class="total">
                            <div style="display: flex; justify-content: space-between;">
                                <span>Subtotal:</span>
                                <span>Rp ${(transaction.total / 1.1).toLocaleString('id-ID')}</span>
                            </div>
                            <div style="display: flex; justify-content: space-between;">
                                <span>Pajak (10%):</span>
                                <span>Rp ${(transaction.total * 0.1).toLocaleString('id-ID')}</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; font-weight: bold; margin-top: 5px;">
                                <span>Total:</span>
                                <span>Rp ${transaction.total.toLocaleString('id-ID')}</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; margin-top: 10px;">
                                <span>Bayar:</span>
                                <span>Rp ${transaction.payment.toLocaleString('id-ID')}</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; font-weight: bold;">
                                <span>Kembali:</span>
                                <span>Rp ${transaction.change.toLocaleString('id-ID')}</span>
                            </div>
                        </div>
                        <div class="footer">
                            ${document.getElementById('receiptFooter').value || 'Terima kasih telah berbelanja di Jennaira Group'}
                        </div>
                    </div>
                </body>
                </html>
            `;
            
            receiptWindow.document.write(receiptContent);
            receiptWindow.document.close();
            
            // Auto print
            setTimeout(() => {
                receiptWindow.print();
            }, 500);
        }

        // Load laporan
        function loadReport() {
            const reportTable = document.getElementById('reportTable');
            if (!reportTable) return;
            
            // Filter berdasarkan tanggal
            const startDate = document.getElementById('startDate')?.value || '2023-10-01';
            const endDate = document.getElementById('endDate')?.value || '2023-10-31';
            
            // Dalam implementasi nyata, di sini akan ada filter berdasarkan tanggal
            // Untuk contoh, kita gunakan data contoh
            reportTable.innerHTML = '';
            
            reportData.forEach((item, index) => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${item.date}</td>
                    <td>${item.code}</td>
                    <td>${item.product}</td>
                    <td>${item.quantity}</td>
                    <td>Rp ${item.total.toLocaleString('id-ID')}</td>
                    <td>${item.cashier}</td>
                `;
                reportTable.appendChild(row);
            });
        }

        // Load riwayat transaksi
        function loadHistory() {
            const historyTable = document.getElementById('historyTable');
            if (!historyTable) return;
            
            historyTable.innerHTML = '';
            
            transactions.forEach((transaction, index) => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${transaction.date}</td>
                    <td>${transaction.code}</td>
                    <td>${transaction.items} item</td>
                    <td>Rp ${transaction.total.toLocaleString('id-ID')}</td>
                    <td>Rp ${transaction.payment.toLocaleString('id-ID')}</td>
                    <td>Rp ${transaction.change.toLocaleString('id-ID')}</td>
                    <td>
                        <div style="display: flex; gap: 5px;">
                            <button class="btn btn-primary btn-sm view-history-btn" data-id="${transaction.id}" style="padding: 5px 10px; font-size: 0.8rem;">
                                <i class="fas fa-eye"></i>
                            </button>
                            <button class="btn btn-success btn-sm print-history-btn" data-id="${transaction.id}" style="padding: 5px 10px; font-size: 0.8rem;">
                                <i class="fas fa-print"></i>
                            </button>
                        </div>
                    </td>
                `;
                
                historyTable.appendChild(row);
            });
            
            // Tambah event listeners untuk tombol
            document.querySelectorAll('.view-history-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const transactionId = parseInt(this.getAttribute('data-id'));
                    viewTransactionHistory(transactionId);
                });
            });
            
            document.querySelectorAll('.print-history-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const transactionId = parseInt(this.getAttribute('data-id'));
                    printTransactionHistory(transactionId);
                });
            });
        }

        // Lihat detail transaksi riwayat
        function viewTransactionHistory(transactionId) {
            const transaction = transactions.find(t => t.id === transactionId);
            if (transaction) {
                alert(`Detail Transaksi:\n\nID: ${transaction.code}\nTanggal: ${transaction.date}\nItems: ${transaction.items}\nTotal: Rp ${transaction.total.toLocaleString('id-ID')}\nBayar: Rp ${transaction.payment.toLocaleString('id-ID')}\nKembali: Rp ${transaction.change.toLocaleString('id-ID')}\nKasir: ${transaction.cashier}`);
            }
        }

        // Cetak ulang transaksi riwayat
        function printTransactionHistory(transactionId) {
            const transaction = transactions.find(t => t.id === transactionId);
            if (transaction) {
                // Untuk contoh, kita buat struk sederhana
                const receiptWindow = window.open('', '_blank', 'width=400,height=500');
                
                const receiptContent = `
                    <!DOCTYPE html>
                    <html>
                    <head>
                        <title>Struk Ulang #${transaction.code}</title>
                        <style>
                            body { font-family: 'Courier New', monospace; padding: 20px; }
                            .receipt { max-width: 300px; margin: 0 auto; }
                            .header { text-align: center; margin-bottom: 20px; border-bottom: 1px dashed #000; padding-bottom: 10px; }
                            .store-name { font-size: 18px; font-weight: bold; }
                            .transaction-info { margin: 15px 0; }
                            .total { border-top: 2px solid #000; padding-top: 10px; margin-top: 10px; }
                            .footer { text-align: center; margin-top: 20px; font-size: 12px; }
                            .note { font-size: 12px; color: #666; margin-top: 10px; }
                        </style>
                    </head>
                    <body>
                        <div class="receipt">
                            <div class="header">
                                <div class="store-name">${document.getElementById('storeName').value || 'Jennaira Group'}</div>
                                <div>${document.getElementById('storeAddress').value || 'Jl. Raya Contoh No. 123, Jakarta Selatan'}</div>
                            </div>
                            <div class="transaction-info">
                                <div><strong>STRUK ULANG</strong></div>
                                <div>No: ${transaction.code}</div>
                                <div>Tanggal: ${transaction.date}</div>
                                <div>Kasir: ${transaction.cashier}</div>
                            </div>
                            <div class="total">
                                <div style="display: flex; justify-content: space-between; font-weight: bold;">
                                    <span>Total:</span>
                                    <span>Rp ${transaction.total.toLocaleString('id-ID')}</span>
                                </div>
                                <div style="display: flex; justify-content: space-between; margin-top: 5px;">
                                    <span>Bayar:</span>
                                    <span>Rp ${transaction.payment.toLocaleString('id-ID')}</span>
                                </div>
                                <div style="display: flex; justify-content: space-between; font-weight: bold;">
                                    <span>Kembali:</span>
                                    <span>Rp ${transaction.change.toLocaleString('id-ID')}</span>
                                </div>
                            </div>
                            <div class="note">
                                * Struk ulang untuk arsip *
                            </div>
                            <div class="footer">
                                ${document.getElementById('receiptFooter').value || 'Terima kasih telah berbelanja di Jennaira Group'}
                            </div>
                        </div>
                    </body>
                    </html>
                `;
                
                receiptWindow.document.write(receiptContent);
                receiptWindow.document.close();
                
                // Auto print
                setTimeout(() => {
                    receiptWindow.print();
                }, 500);
            }
        }

        // Tambah produk baru
        function addNewProduct() {
            const name = prompt("Masukkan nama produk:");
            if (!name) return;
            
            const price = parseFloat(prompt("Masukkan harga produk:"));
            if (isNaN(price) || price <= 0) {
                showNotification("Harga tidak valid!", 'error');
                return;
            }
            
            const stock = parseInt(prompt("Masukkan stok awal produk:"));
            if (isNaN(stock) || stock < 0) {
                showNotification("Stok tidak valid!", 'error');
                return;
            }
            
            const category = prompt("Masukkan kategori produk (contoh: Sembako • pack):", "Lainnya");
            
            // Generate kode produk
            const nextId = products.length + 1;
            const code = `P${nextId.toString().padStart(3, '0')}`;
            
            const newProduct = {
                id: nextId,
                code: code,
                name: name,
                category: category || "Lainnya",
                price: price,
                stock: stock,
                sold: 0
            };
            
            products.push(newProduct);
            loadProductManagement();
            loadProducts();
            
            showNotification(`Produk "${name}" berhasil ditambahkan`, 'success');
        }

        // Edit produk
        function editProduct(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            const newName = prompt("Edit nama produk:", product.name);
            if (!newName) return;
            
            const newPrice = parseFloat(prompt("Edit harga produk:", product.price));
            if (isNaN(newPrice) || newPrice <= 0) {
                showNotification("Harga tidak valid!", 'error');
                return;
            }
            
            const newStock = parseInt(prompt("Edit stok produk:", product.stock));
            if (isNaN(newStock) || newStock < 0) {
                showNotification("Stok tidak valid!", 'error');
                return;
            }
            
            const newCategory = prompt("Edit kategori produk:", product.category);
            
            // Update produk
            product.name = newName;
            product.price = newPrice;
            product.stock = newStock;
            product.category = newCategory || product.category;
            
            loadProductManagement();
            loadProducts();
            
            showNotification(`Produk "${newName}" berhasil diperbarui`, 'success');
        }

        // Hapus produk
        function deleteProduct(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            if (confirm(`Apakah Anda yakin ingin menghapus produk "${product.name}"?`)) {
                const index = products.findIndex(p => p.id === productId);
                if (index !== -1) {
                    products.splice(index, 1);
                    loadProductManagement();
                    loadProducts();
                    showNotification(`Produk "${product.name}" berhasil dihapus`, 'success');
                }
            }
        }

        // Export ke CSV
        function exportToCSV() {
            // Buat data CSV
            let csvContent = "Tanggal,No. Transaksi,Produk,Qty,Total,Kasir\n";
            
            reportData.forEach(item => {
                csvContent += `${item.date},${item.code},${item.product},${item.quantity},${item.total},${item.cashier}\n`;
            });
            
            // Buat blob dan download
            const blob = new Blob([csvContent], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `laporan_penjualan_${new Date().toISOString().split('T')[0]}.csv`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            
            showNotification("File CSV berhasil diunduh", 'success');
        }

        // Export ke Excel
        function exportToExcel() {
            // Dalam implementasi nyata, bisa menggunakan library seperti SheetJS
            // Untuk contoh, kita gunakan CSV dengan ekstensi .xls
            let excelContent = "<table><tr><th>Tanggal</th><th>No. Transaksi</th><th>Produk</th><th>Qty</th><th>Total</th><th>Kasir</th></tr>";
            
            reportData.forEach(item => {
                excelContent += `<tr><td>${item.date}</td><td>${item.code}</td><td>${item.product}</td><td>${item.quantity}</td><td>${item.total}</td><td>${item.cashier}</td></tr>`;
            });
            
            excelContent += "</table>";
            
            // Buat blob dan download
            const blob = new Blob([excelContent], { type: 'application/vnd.ms-excel' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `laporan_penjualan_${new Date().toISOString().split('T')[0]}.xls`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            
            showNotification("File Excel berhasil diunduh", 'success');
        }

        // Simpan pengaturan
        function saveSettings() {
            // Dalam implementasi nyata, di sini akan ada penyimpanan ke localStorage atau database
            showNotification("Pengaturan berhasil disimpan", 'success');
        }

        // Reset pengaturan
        function resetSettings() {
            if (confirm("Apakah Anda yakin ingin mengembalikan pengaturan ke nilai default?")) {
                document.getElementById('storeName').value = "Jennaira Group";
                document.getElementById('storeAddress').value = "Jl. Raya Contoh No. 123, Jakarta Selatan";
                document.getElementById('storePhone').value = "021-12345678";
                document.getElementById('taxRate').value = "10";
                document.getElementById('receiptFooter').value = "Terima kasih telah berbelanja di Jennaira Group";
                
                showNotification("Pengaturan berhasil direset", 'success');
            }
        }

        // Tampilkan notifikasi
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            const notificationMessage = document.getElementById('notificationMessage');
            
            // Set pesan dan warna
            notificationMessage.textContent = message;
            
            if (type === 'error') {
                notification.style.backgroundColor = '#e74c3c';
            } else if (type === 'warning') {
                notification.style.backgroundColor = '#f39c12';
            } else {
                notification.style.backgroundColor = '#2ecc71';
            }
            
            // Tampilkan notifikasi
            notification.classList.add('show');
            
            // Sembunyikan setelah 3 detik
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
    </script>
</body>
</html>
