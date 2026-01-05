<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KASIR</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: #f5f7fa;
            color: #333;
            min-height: 100vh;
        }

        .container {
            display: flex;
            min-height: 100vh;
        }

        /* SIDEBAR */
        .sidebar {
            width: 250px;
            background: #2d3748;
            color: white;
            padding: 25px 0;
            box-shadow: 3px 0 15px rgba(0, 0, 0, 0.1);
        }

        .logo {
            display: flex;
            align-items: center;
            padding: 0 25px;
            margin-bottom: 40px;
        }

        .logo i {
            font-size: 28px;
            color: #4299e1;
            margin-right: 12px;
        }

        .logo h1 {
            font-size: 22px;
            font-weight: 700;
            color: white;
        }

        .logo p {
            font-size: 11px;
            color: #cbd5e0;
            margin-top: 3px;
        }

        .nav-menu {
            list-style: none;
        }

        .nav-item {
            padding: 15px 25px;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s;
            border-left: 4px solid transparent;
        }

        .nav-item:hover {
            background: #4a5568;
            border-left: 4px solid #4299e1;
        }

        .nav-item.active {
            background: #4a5568;
            border-left: 4px solid #4299e1;
        }

        .nav-item i {
            font-size: 18px;
            margin-right: 12px;
            width: 24px;
            text-align: center;
            color: #cbd5e0;
        }

        .nav-item.active i {
            color: #4299e1;
        }

        .nav-item span {
            font-size: 15px;
            font-weight: 500;
        }

        /* MAIN CONTENT */
        .main-content {
            flex: 1;
            padding: 0;
            overflow: hidden;
        }

        /* HEADER */
        .header {
            background: white;
            padding: 18px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            border-bottom: 1px solid #e2e8f0;
        }

        .header-left h2 {
            font-size: 20px;
            font-weight: 600;
            color: #2d3748;
        }

        .header-left p {
            font-size: 13px;
            color: #718096;
            margin-top: 3px;
        }

        .header-right {
            display: flex;
            align-items: center;
            gap: 25px;
        }

        .datetime {
            text-align: right;
        }

        .datetime .date {
            font-size: 14px;
            color: #4a5568;
            font-weight: 500;
        }

        .datetime .time {
            font-size: 18px;
            font-weight: 700;
            color: #2d3748;
            margin-top: 3px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 12px;
            background: #edf2f7;
            padding: 8px 15px;
            border-radius: 30px;
            cursor: pointer;
        }

        .user-profile img {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid #4299e1;
        }

        .user-info h4 {
            font-size: 14px;
            font-weight: 600;
            color: #2d3748;
        }

        .user-info p {
            font-size: 12px;
            color: #718096;
        }

        /* CONTENT AREA */
        .content-area {
            padding: 25px;
            height: calc(100vh - 82px);
            overflow-y: auto;
        }

        /* PRODUCTS SECTION */
        .products-section {
            background: white;
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border: 1px solid #e2e8f0;
        }

        .section-title {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #edf2f7;
        }

        .section-title i {
            font-size: 20px;
            color: #4299e1;
            margin-right: 10px;
        }

        .section-title h3 {
            font-size: 18px;
            font-weight: 600;
            color: #2d3748;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 20px;
        }

        .product-card {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 10px;
            padding: 18px;
            transition: all 0.3s;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
            border-color: #4299e1;
        }

        .product-card.selected {
            border-color: #4299e1;
            background: linear-gradient(135deg, #f0f9ff, #e6f7ff);
        }

        .product-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }

        .product-name {
            font-weight: 600;
            font-size: 15px;
            color: #2d3748;
        }

        .product-code {
            background: #4299e1;
            color: white;
            padding: 3px 10px;
            border-radius: 15px;
            font-size: 11px;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        .product-price {
            color: #2d6a4f;
            font-weight: 700;
            font-size: 17px;
            margin-bottom: 8px;
        }

        .product-category {
            display: inline-block;
            background: #e2e8f0;
            color: #4a5568;
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 12px;
            margin-bottom: 15px;
        }

        .product-stats {
            display: flex;
            justify-content: space-between;
            font-size: 13px;
            color: #718096;
        }

        .stock {
            color: #38a169;
            font-weight: 600;
        }

        .sold {
            color: #e53e3e;
            font-weight: 600;
        }

        /* SALES REPORT */
        .sales-report {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border: 1px solid #e2e8f0;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: #f8fafc;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            border-top: 4px solid #4299e1;
            transition: all 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.08);
        }

        .stat-card:nth-child(1) {
            border-top-color: #38a169;
        }

        .stat-card:nth-child(2) {
            border-top-color: #4299e1;
        }

        .stat-card:nth-child(3) {
            border-top-color: #d69e2e;
        }

        .stat-card:nth-child(4) {
            border-top-color: #e53e3e;
        }

        .stat-value {
            font-size: 26px;
            font-weight: 700;
            color: #2d3748;
            margin-bottom: 8px;
        }

        .stat-label {
            font-size: 14px;
            color: #718096;
            font-weight: 500;
        }

        /* SALES HISTORY TABLE */
        .history-table-container {
            border: 1px solid #e2e8f0;
            border-radius: 10px;
            overflow: hidden;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        thead {
            background: #edf2f7;
        }

        th {
            padding: 16px 20px;
            text-align: left;
            font-weight: 600;
            color: #2d3748;
            font-size: 14px;
            border-bottom: 1px solid #e2e8f0;
        }

        td {
            padding: 16px 20px;
            border-bottom: 1px solid #e2e8f0;
            font-size: 14px;
            color: #4a5568;
        }

        tbody tr:hover {
            background: #f7fafc;
        }

        /* TRANSACTION PANEL */
        .transaction-panel {
            position: fixed;
            top: 82px;
            right: 0;
            width: 450px;
            height: calc(100vh - 82px);
            background: white;
            box-shadow: -5px 0 20px rgba(0, 0, 0, 0.1);
            padding: 25px;
            overflow-y: auto;
            z-index: 100;
        }

        .cart-items-container {
            max-height: 320px;
            overflow-y: auto;
            margin-bottom: 25px;
            border: 1px solid #e2e8f0;
            border-radius: 10px;
        }

        .empty-cart {
            text-align: center;
            padding: 50px 20px;
            color: #a0aec0;
        }

        .empty-cart i {
            font-size: 48px;
            margin-bottom: 15px;
            opacity: 0.5;
        }

        .empty-cart p {
            font-size: 14px;
            margin-bottom: 5px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 18px;
            border-bottom: 1px solid #e2e8f0;
            background: #f8fafc;
        }

        .cart-item:last-child {
            border-bottom: none;
        }

        .cart-item-info h4 {
            font-weight: 600;
            font-size: 15px;
            margin-bottom: 5px;
            color: #2d3748;
        }

        .cart-item-info .price {
            color: #2d6a4f;
            font-weight: 600;
            font-size: 14px;
        }

        .cart-item-controls {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .quantity-controls {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .quantity-btn {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background: #e2e8f0;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-weight: bold;
            color: #4a5568;
            font-size: 16px;
            transition: all 0.2s;
        }

        .quantity-btn:hover {
            background: #4299e1;
            color: white;
        }

        .quantity {
            font-weight: 700;
            min-width: 30px;
            text-align: center;
            font-size: 15px;
            color: #2d3748;
        }

        .item-total {
            font-weight: 700;
            color: #2d6a4f;
            min-width: 100px;
            text-align: right;
            font-size: 15px;
        }

        .remove-item {
            background: none;
            border: none;
            color: #e53e3e;
            cursor: pointer;
            font-size: 17px;
            transition: all 0.2s;
        }

        .remove-item:hover {
            transform: scale(1.1);
        }

        /* TRANSACTION SUMMARY */
        .transaction-summary {
            background: #f8fafc;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 25px;
            border: 1px solid #e2e8f0;
        }

        .summary-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 12px;
            font-size: 15px;
            color: #4a5568;
        }

        .summary-row.total {
            font-size: 20px;
            font-weight: 700;
            color: #2d3748;
            border-top: 2px solid #e2e8f0;
            padding-top: 15px;
            margin-top: 10px;
        }

        /* PAYMENT SECTION */
        .payment-section {
            margin-bottom: 25px;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2d3748;
            font-size: 15px;
        }

        .input-group input {
            width: 100%;
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 17px;
            font-weight: 600;
            text-align: right;
            color: #2d3748;
            transition: all 0.3s;
        }

        .input-group input:focus {
            outline: none;
            border-color: #4299e1;
            box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.1);
        }

        .change-display {
            background: linear-gradient(135deg, #38a169, #2d6a4f);
            color: white;
            padding: 18px;
            border-radius: 8px;
            text-align: center;
            font-weight: 700;
            font-size: 18px;
            display: none;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ACTION BUTTONS */
        .action-buttons {
            display: flex;
            gap: 15px;
        }

        .btn {
            flex: 1;
            padding: 17px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            transition: all 0.3s;
        }

        .btn-clear {
            background: #e2e8f0;
            color: #4a5568;
        }

        .btn-clear:hover {
            background: #cbd5e0;
            transform: translateY(-2px);
        }

        .btn-checkout {
            background: linear-gradient(135deg, #4299e1, #3182ce);
            color: white;
        }

        .btn-checkout:hover {
            background: linear-gradient(135deg, #3182ce, #2c5282);
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(49, 130, 206, 0.3);
        }

        /* RESPONSIVE */
        @media (max-width: 1200px) {
            .transaction-panel {
                width: 400px;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 992px) {
            .container {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
                padding: 15px 0;
            }
            
            .nav-menu {
                display: flex;
                overflow-x: auto;
                padding: 0 15px;
            }
            
            .nav-item {
                padding: 12px 20px;
                white-space: nowrap;
                border-left: none;
                border-bottom: 3px solid transparent;
            }
            
            .nav-item.active,
            .nav-item:hover {
                border-left: none;
                border-bottom: 3px solid #4299e1;
            }
            
            .transaction-panel {
                position: relative;
                top: 0;
                width: 100%;
                height: auto;
                margin-top: 25px;
            }
            
            .main-content {
                padding-bottom: 400px;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            
            .header-right {
                width: 100%;
                justify-content: space-between;
            }
            
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .action-buttons {
                flex-direction: column;
            }
        }

        @media (max-width: 480px) {
            .content-area {
                padding: 15px;
            }
            
            .products-grid {
                grid-template-columns: 1fr;
            }
            
            .transaction-panel {
                padding: 20px;
            }
            
            .cart-item {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .cart-item-controls {
                width: 100%;
                justify-content: space-between;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- SIDEBAR -->
        <div class="sidebar">
            <div class="logo">
                <i class="fas fa-cash-register"></i>
                <div>
                    <h1>KASIR</h1>
                    <p>Sistem Kasir Lengkap</p>
                </div>
            </div>
            
            <ul class="nav-menu">
                <li class="nav-item active">
                    <i class="fas fa-home"></i>
                    <span>Dashboard</span>
                </li>
                <li class="nav-item">
                    <i class="fas fa-box"></i>
                    <span>Produk</span>
                </li>
                <li class="nav-item">
                    <i class="fas fa-shopping-cart"></i>
                    <span>Transaksi</span>
                </li>
                <li class="nav-item">
                    <i class="fas fa-chart-bar"></i>
                    <span>Laporan</span>
                </li>
                <li class="nav-item">
                    <i class="fas fa-users"></i>
                    <span>Pelanggan</span>
                </li>
                <li class="nav-item">
                    <i class="fas fa-cog"></i>
                    <span>Pengaturan</span>
                </li>
            </ul>
        </div>

        <!-- MAIN CONTENT -->
        <div class="main-content">
            <!-- HEADER -->
            <div class="header">
                <div class="header-left">
                    <h2>Dashboard Kasir</h2>
                    <p>Kelola penjualan dan transaksi dengan mudah</p>
                </div>
                
                <div class="header-right">
                    <div class="datetime">
                        <div class="date" id="currentDate">Senin, 5 Januari 2026</div>
                        <div class="time" id="currentTime">16:44:30</div>
                    </div>
                    
                    <div class="user-profile">
                        <img src="https://ui-avatars.com/api/?name=Kasir+Admin&background=4299e1&color=fff&size=100" alt="User">
                        <div class="user-info">
                            <h4>Kasir Admin</h4>
                            <p>Super Admin</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- CONTENT AREA -->
            <div class="content-area">
                <!-- PRODUCTS SECTION -->
                <div class="products-section">
                    <div class="section-title">
                        <i class="fas fa-boxes"></i>
                        <h3>Manajemen Produk & Stok</h3>
                    </div>
                    
                    <div class="products-grid" id="productsGrid">
                        <!-- Product cards will be loaded here -->
                    </div>
                </div>

                <!-- SALES REPORT -->
                <div class="sales-report">
                    <div class="section-title">
                        <i class="fas fa-chart-line"></i>
                        <h3>Laporan Penjualan</h3>
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-value" id="totalSales">Rp 0</div>
                            <div class="stat-label">Total Penjualan</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="transactionCount">0</div>
                            <div class="stat-label">Jumlah Transaksi</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="avgTransaction">Rp 0</div>
                            <div class="stat-label">Rata-rata per Transaksi</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="itemsSold">0</div>
                            <div class="stat-label">Item Terjual</div>
                        </div>
                    </div>
                    
                    <div class="section-title" style="margin-top: 30px;">
                        <i class="fas fa-history"></i>
                        <h3>Riwayat Transaksi</h3>
                    </div>
                    
                    <div class="history-table-container">
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
                                </tr>
                            </thead>
                            <tbody id="salesHistory">
                                <!-- Sales history will be loaded here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TRANSACTION PANEL (RIGHT SIDEBAR) -->
            <div class="transaction-panel">
                <div class="section-title">
                    <i class="fas fa-shopping-cart"></i>
                    <h3>Transaksi Aktif</h3>
                </div>
                
                <!-- CART ITEMS -->
                <div class="cart-items-container" id="cartContainer">
                    <div class="empty-cart" id="emptyCart">
                        <i class="fas fa-shopping-basket"></i>
                        <p>Keranjang belanja kosong</p>
                        <p>Pilih produk dari daftar produk</p>
                    </div>
                    <!-- Cart items will be loaded here -->
                </div>

                <!-- TRANSACTION SUMMARY -->
                <div class="transaction-summary">
                    <div class="summary-row">
                        <span>Subtotal</span>
                        <span id="subtotal">Rp 0</span>
                    </div>
                    <div class="summary-row">
                        <span>Pajak (10%)</span>
                        <span id="tax">Rp 0</span>
                    </div>
                    <div class="summary-row total">
                        <span>TOTAL</span>
                        <span id="total">Rp 0</span>
                    </div>
                </div>

                <!-- PAYMENT SECTION -->
                <div class="payment-section">
                    <div class="input-group">
                        <label for="cashAmount">
                            <i class="fas fa-money-bill-wave"></i>
                            Uang Diterima (Cash)
                        </label>
                        <input type="number" id="cashAmount" placeholder="0" min="0" value="0">
                    </div>
                    <div class="change-display" id="changeDisplay">
                        Kembalian: <span id="changeAmount">Rp 0</span>
                    </div>
                </div>

                <!-- ACTION BUTTONS -->
                <div class="action-buttons">
                    <button class="btn btn-clear" id="clearCartBtn">
                        <i class="fas fa-trash-alt"></i>
                        Kosongkan
                    </button>
                    <button class="btn btn-checkout" id="checkoutBtn">
                        <i class="fas fa-receipt"></i>
                        Selesaikan Transaksi
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Data produk sesuai dengan URL
        const products = [
            { id: 1, name: "Beras 5kg", code: "BR001", price: 60000, category: "Sembako", unit: "pack", stock: 45, sold: 125 },
            { id: 2, name: "Minyak Goreng 2L", code: "MG002", price: 35000, category: "Sembako", unit: "botol", stock: 28, sold: 89 },
            { id: 3, name: "Gula Pasir 1kg", code: "GP003", price: 15000, category: "Sembako", unit: "kg", stock: 12, sold: 156 },
            { id: 4, name: "Telur 1kg", code: "TL004", price: 28000, category: "Sembako", unit: "kg", stock: 8, sold: 67 },
            { id: 5, name: "Sabun Mandi", code: "SB005", price: 5000, category: "Kebersihan", unit: "pcs", stock: 120, sold: 234 },
            { id: 6, name: "Shampoo", code: "SP006", price: 12000, category: "Kebersihan", unit: "botol", stock: 35, sold: 78 },
            { id: 7, name: "Air Mineral 600ml", code: "AM007", price: 3000, category: "Minuman", unit: "botol", stock: 150, sold: 345 },
            { id: 8, name: "Kopi Sachet", code: "KS008", price: 2000, category: "Minuman", unit: "pcs", stock: 89, sold: 289 },
            { id: 9, name: "Teh Celup", code: "TC009", price: 1500, category: "Minuman", unit: "pcs", stock: 65, sold: 167 },
            { id: 10, name: "Biskuit", code: "BS010", price: 8000, category: "Snack", unit: "pack", stock: 42, sold: 134 }
        ];

        // Data awal
        let cart = [];
        let salesHistory = [];
        let salesStats = {
            totalSales: 192500,
            transactionCount: 2,
            totalItemsSold: 11
        };

        // DOM Elements
        const productsGrid = document.getElementById('productsGrid');
        const cartContainer = document.getElementById('cartContainer');
        const emptyCart = document.getElementById('emptyCart');
        const subtotalElement = document.getElementById('subtotal');
        const taxElement = document.getElementById('tax');
        const totalElement = document.getElementById('total');
        const cashAmountInput = document.getElementById('cashAmount');
        const changeDisplay = document.getElementById('changeDisplay');
        const changeAmountElement = document.getElementById('changeAmount');
        const clearCartBtn = document.getElementById('clearCartBtn');
        const checkoutBtn = document.getElementById('checkoutBtn');
        const salesHistoryTbody = document.getElementById('salesHistory');
        
        // Statistik elements
        const totalSalesElement = document.getElementById('totalSales');
        const transactionCountElement = document.getElementById('transactionCount');
        const avgTransactionElement = document.getElementById('avgTransaction');
        const itemsSoldElement = document.getElementById('itemsSold');

        // Format Rupiah
        function formatRupiah(amount) {
            return `Rp ${amount.toLocaleString('id-ID')}`;
        }

        // Update waktu
        function updateDateTime() {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const dateString = now.toLocaleDateString('id-ID', options);
            const timeString = now.toLocaleTimeString('id-ID');
            
            document.getElementById('currentDate').textContent = dateString;
            document.getElementById('currentTime').textContent = timeString;
        }

        // Load produk
        function loadProducts() {
            productsGrid.innerHTML = '';
            
            products.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                productCard.dataset.id = product.id;
                
                productCard.innerHTML = `
                    <div class="product-header">
                        <div class="product-name">${product.name}</div>
                        <div class="product-code">${product.code}</div>
                    </div>
                    <div class="product-price">${formatRupiah(product.price)}</div>
                    <div class="product-category">${product.category} • ${product.unit}</div>
                    <div class="product-stats">
                        <div class="stock">Stok: ${product.stock}</div>
                        <div class="sold">Terjual: ${product.sold}</div>
                    </div>
                `;
                
                productCard.addEventListener('click', () => addToCart(product.id));
                productsGrid.appendChild(productCard);
            });
        }

        // Tambah ke keranjang
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                if (existingItem.quantity < product.stock) {
                    existingItem.quantity++;
                } else {
                    alert(`Stok ${product.name} tidak cukup! Stok tersisa: ${product.stock}`);
                    return;
                }
            } else {
                if (product.stock > 0) {
                    cart.push({
                        id: product.id,
                        name: product.name,
                        price: product.price,
                        quantity: 1,
                        code: product.code
                    });
                } else {
                    alert(`Stok ${product.name} habis!`);
                    return;
                }
            }
            
            updateCartDisplay();
        }

        // Update tampilan keranjang
        function updateCartDisplay() {
            cartContainer.innerHTML = '';
            
            if (cart.length === 0) {
                cartContainer.appendChild(emptyCart);
                emptyCart.style.display = 'block';
            } else {
                emptyCart.style.display = 'none';
                
                let subtotal = 0;
                
                cart.forEach((item, index) => {
                    const itemTotal = item.price * item.quantity;
                    subtotal += itemTotal;
                    
                    const cartItem = document.createElement('div');
                    cartItem.className = 'cart-item';
                    
                    cartItem.innerHTML = `
                        <div class="cart-item-info">
                            <h4>${item.name} (${item.code})</h4>
                            <div class="price">${formatRupiah(item.price)}</div>
                        </div>
                        <div class="cart-item-controls">
                            <div class="quantity-controls">
                                <button class="quantity-btn" onclick="decreaseQuantity(${index})">-</button>
                                <div class="quantity">${item.quantity}</div>
                                <button class="quantity-btn" onclick="increaseQuantity(${index})">+</button>
                            </div>
                            <div class="item-total">${formatRupiah(itemTotal)}</div>
                            <button class="remove-item" onclick="removeFromCart(${index})">
                                <i class="fas fa-times"></i>
                            </button>
                        </div>
                    `;
                    
                    cartContainer.appendChild(cartItem);
                });
                
                const tax = subtotal * 0.1;
                const total = subtotal + tax;
                
                subtotalElement.textContent = formatRupiah(subtotal);
                taxElement.textContent = formatRupiah(tax);
                totalElement.textContent = formatRupiah(total);
                
                // Update statistik item terjual
                const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
                itemsSoldElement.textContent = totalItems;
            }
            
            calculateChange();
        }

        // Fungsi untuk kuantitas
        window.decreaseQuantity = function(index) {
            if (cart[index].quantity > 1) {
                cart[index].quantity--;
            } else {
                cart.splice(index, 1);
            }
            updateCartDisplay();
        };

        window.increaseQuantity = function(index) {
            const productId = cart[index].id;
            const product = products.find(p => p.id === productId);
            
            if (cart[index].quantity < product.stock) {
                cart[index].quantity++;
            } else {
                alert(`Stok ${product.name} tidak cukup! Stok tersisa: ${product.stock}`);
            }
            
            updateCartDisplay();
        };

        window.removeFromCart = function(index) {
            cart.splice(index, 1);
            updateCartDisplay();
        };

        // Kosongkan keranjang
        clearCartBtn.addEventListener('click', function() {
            if (cart.length === 0) {
                alert('Keranjang sudah kosong!');
                return;
            }
            
            if (confirm('Apakah Anda yakin ingin mengosongkan keranjang?')) {
                cart = [];
                updateCartDisplay();
                cashAmountInput.value = '0';
                calculateChange();
            }
        });

        // Hitung kembalian
        function calculateChange() {
            const cashAmount = parseFloat(cashAmountInput.value) || 0;
            const totalText = totalElement.textContent.replace('Rp ', '').replace(/\./g, '');
            const total = parseFloat(totalText) || 0;
            
            if (cashAmount >= total && total > 0) {
                const change = cashAmount - total;
                changeAmountElement.textContent = formatRupiah(change);
                changeDisplay.style.display = 'block';
            } else {
                changeDisplay.style.display = 'none';
            }
        }

        // Checkout
        checkoutBtn.addEventListener('click', function() {
            if (cart.length === 0) {
                alert('Keranjang belanja kosong!');
                return;
            }
            
            const cashAmount = parseFloat(cashAmountInput.value) || 0;
            const totalText = totalElement.textContent.replace('Rp ', '').replace(/\./g, '');
            const total = parseFloat(totalText);
            
            if (cashAmount < total) {
                alert(`Uang tidak cukup! Total: ${formatRupiah(total)}\nDiterima: ${formatRupiah(cashAmount)}`);
                return;
            }
            
            // Generate ID transaksi
            const transactionId = 'TRX' + Date.now().toString().slice(-6);
            const now = new Date();
            const dateString = now.toLocaleDateString('id-ID');
            const timeString = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
            
            // Hitung total item
            let totalItems = 0;
            let itemsList = [];
            
            cart.forEach(item => {
                totalItems += item.quantity;
                itemsList.push(`${item.name} (${item.quantity}x)`);
                
                // Update stok produk
                const productIndex = products.findIndex(p => p.id === item.id);
                if (productIndex !== -1) {
                    products[productIndex].stock -= item.quantity;
                    products[productIndex].sold += item.quantity;
                }
            });
            
            // Update statistik
            salesStats.totalSales += total;
            salesStats.transactionCount += 1;
            salesStats.totalItemsSold += totalItems;
            
            // Simpan transaksi
            const transaction = {
                id: transactionId,
                date: `${dateString} ${timeString}`,
                items: itemsList.join(', '),
                total: total,
                cash: cashAmount,
                change: cashAmount - total
            };
            
            salesHistory.unshift(transaction);
            
            // Update tampilan
            updateSalesStats();
            updateSalesHistory();
            loadProducts();
            
            // Tampilkan struk
            const receiptWindow = window.open('', 'Receipt', 'width=400,height=600');
            receiptWindow.document.write(`
                <html>
                <head>
                    <title>Struk Transaksi</title>
                    <style>
                        body { font-family: Arial, sans-serif; padding: 20px; }
                        .receipt { border: 1px solid #000; padding: 20px; }
                        .header { text-align: center; margin-bottom: 20px; }
                        .header h2 { margin: 0; }
                        .info { margin-bottom: 20px; }
                        .items { width: 100%; border-collapse: collapse; margin-bottom: 20px; }
                        .items th, .items td { padding: 8px; text-align: left; border-bottom: 1px solid #ddd; }
                        .total { text-align: right; font-weight: bold; margin-top: 20px; }
                        .footer { text-align: center; margin-top: 30px; font-size: 12px; }
                    </style>
                </head>
                <body>
                    <div class="receipt">
                        <div class="header">
                            <h2>KASIR STORE</h2>
                            <p>Jl. Contoh No. 123, Jakarta</p>
                            <p>Telp: 021-12345678</p>
                        </div>
                        <div class="info">
                            <p><strong>ID Transaksi:</strong> ${transactionId}</p>
                            <p><strong>Tanggal:</strong> ${dateString} ${timeString}</p>
                            <p><strong>Kasir:</strong> Admin</p>
                        </div>
                        <table class="items">
                            <thead>
                                <tr>
                                    <th>Item</th>
                                    <th>Qty</th>
                                    <th>Harga</th>
                                    <th>Subtotal</th>
                                </tr>
                            </thead>
                            <tbody>
                                ${cart.map(item => `
                                    <tr>
                                        <td>${item.name}</td>
                                        <td>${item.quantity}</td>
                                        <td>${formatRupiah(item.price)}</td>
                                        <td>${formatRupiah(item.price * item.quantity)}</td>
                                    </tr>
                                `).join('')}
                            </tbody>
                        </table>
                        <div class="total">
                            <p>Subtotal: ${formatRupiah(total - (total * 0.1))}</p>
                            <p>Pajak (10%): ${formatRupiah(total * 0.1)}</p>
                            <p><strong>TOTAL: ${formatRupiah(total)}</strong></p>
                            <p>Bayar: ${formatRupiah(cashAmount)}</p>
                            <p>Kembali: ${formatRupiah(cashAmount - total)}</p>
                        </div>
                        <div class="footer">
                            <p>Terima kasih telah berbelanja!</p>
                            <p>Barang yang sudah dibeli tidak dapat dikembalikan</p>
                        </div>
                    </div>
                    <script>
                        window.onload = function() {
                            window.print();
                            setTimeout(function() {
                                window.close();
                            }, 1000);
                        };
                    </script>
                </body>
                </html>
            `);
            
            // Reset
            cart = [];
            updateCartDisplay();
            cashAmountInput.value = '0';
            calculateChange();
        });

        // Update statistik
        function updateSalesStats() {
            totalSalesElement.textContent = formatRupiah(salesStats.totalSales);
            transactionCountElement.textContent = salesStats.transactionCount;
            
            const avg = salesStats.transactionCount > 0 
                ? salesStats.totalSales / salesStats.transactionCount 
                : 0;
            avgTransactionElement.textContent = formatRupiah(Math.round(avg));
            
            itemsSoldElement.textContent = salesStats.totalItemsSold;
        }

        // Update riwayat transaksi
        function updateSalesHistory() {
            salesHistoryTbody.innerHTML = '';
            
            // Tambah data contoh
            const exampleHistory = [
                {
                    id: 'TRX202601001',
                    date: '05/01/2026 14:30',
                    items: 'Beras 5kg (2x), Minyak Goreng 2L (1x)',
                    total: 155000,
                    cash: 200000,
                    change: 45000
                },
                {
                    id: 'TRX202601002',
                    date: '05/01/2026 15:15',
                    items: 'Sabun Mandi (3x), Shampoo (1x), Teh Celup (5x)',
                    total: 37500,
                    cash: 50000,
                    change: 12500
                }
            ];
            
            const allHistory = [...salesHistory, ...exampleHistory].slice(0, 10);
            
            allHistory.forEach((transaction, index) => {
                const row = document.createElement('tr');
                
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${transaction.date}</td>
                    <td>${transaction.id}</td>
                    <td title="${transaction.items}">${transaction.items.length > 30 ? transaction.items.substring(0, 30) + '...' : transaction.items}</td>
                    <td>${formatRupiah(transaction.total)}</td>
                    <td>${formatRupiah(transaction.cash)}</td>
                    <td>${formatRupiah(transaction.change)}</td>
                `;
                
                salesHistoryTbody.appendChild(row);
            });
        }

        // Inisialisasi
        function initializeApp() {
            updateDateTime();
            setInterval(updateDateTime, 1000);
            
            loadProducts();
            updateCartDisplay();
            updateSalesStats();
            updateSalesHistory();
            
            // Event listener untuk input uang
            cashAmountInput.addEventListener('input', calculateChange);
            
            // Event listener untuk Enter key
            cashAmountInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    checkoutBtn.click();
                }
            });
            
            // Navigation menu
            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', function() {
                    document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
                    this.classList.add('active');
                    
                    // Simple navigation effect
                    const title = this.querySelector('span').textContent;
                    document.querySelector('.header-left h2').textContent = title;
                });
            });
        }

        // Jalankan aplikasi
        document.addEventListener('DOMContentLoaded', initializeApp);
    </script>
</body>
</html>
