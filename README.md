<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KASIR PRO - Jennaira Group</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, sans-serif;
        }

        :root {
            --primary: #2d6a4f;
            --primary-light: #40916c;
            --secondary: #ff9e00;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --gray-light: #e9ecef;
            --success: #28a745;
            --danger: #dc3545;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }

        body {
            background-color: #f5f7fa;
            color: var(--dark);
            min-height: 100vh;
        }

        .container {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* Header Styles */
        .header {
            background: linear-gradient(135deg, var(--primary), var(--primary-light));
            color: white;
            padding: 1.2rem 2rem;
            box-shadow: var(--shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo i {
            font-size: 2rem;
            color: var(--secondary);
        }

        .logo h1 {
            font-size: 1.8rem;
            font-weight: 700;
        }

        .logo p {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .datetime {
            text-align: right;
        }

        .datetime .date {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .datetime .time {
            font-size: 1.5rem;
            font-weight: 700;
            letter-spacing: 1px;
            color: var(--secondary);
        }

        /* Main Content */
        .main-content {
            display: flex;
            flex: 1;
            padding: 1.5rem;
            gap: 1.5rem;
        }

        .left-panel {
            flex: 7;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .right-panel {
            flex: 5;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        /* Panel Cards */
        .panel-card {
            background: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: var(--shadow);
        }

        .panel-card h2 {
            color: var(--primary);
            margin-bottom: 1.2rem;
            padding-bottom: 0.7rem;
            border-bottom: 2px solid var(--gray-light);
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.4rem;
        }

        .panel-card h2 i {
            color: var(--secondary);
        }

        /* Product Management */
        .products-section {
            height: 100%;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: 1.2rem;
            max-height: 520px;
            overflow-y: auto;
            padding-right: 5px;
        }

        .product-card {
            border: 1px solid var(--gray-light);
            border-radius: 10px;
            padding: 1.2rem;
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
            border-color: var(--primary-light);
        }

        .product-card.selected {
            border-color: var(--secondary);
            background-color: rgba(255, 158, 0, 0.05);
        }

        .product-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 0.8rem;
        }

        .product-name {
            font-weight: 700;
            font-size: 1.1rem;
            color: var(--dark);
        }

        .product-code {
            background-color: var(--primary-light);
            color: white;
            padding: 3px 8px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .product-price {
            color: var(--primary);
            font-weight: 800;
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
        }

        .product-category {
            display: inline-block;
            background-color: var(--gray-light);
            color: var(--gray);
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
            margin-bottom: 1rem;
        }

        .product-stats {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
            color: var(--gray);
        }

        .stock {
            color: var(--success);
            font-weight: 600;
        }

        .sold {
            color: var(--danger);
            font-weight: 600;
        }

        /* Sales Report */
        .sales-report {
            height: 100%;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1.2rem;
            margin-bottom: 1.5rem;
        }

        .stat-card {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 10px;
            padding: 1.2rem;
            text-align: center;
            border-left: 5px solid var(--primary);
        }

        .stat-card.total-sales {
            border-left-color: var(--success);
        }

        .stat-card.transactions {
            border-left-color: var(--primary);
        }

        .stat-card.avg-transaction {
            border-left-color: var(--secondary);
        }

        .stat-card.items-sold {
            border-left-color: var(--danger);
        }

        .stat-value {
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--dark);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
            font-weight: 600;
        }

        /* Sales History */
        .sales-history {
            flex: 1;
        }

        .history-table-container {
            max-height: 300px;
            overflow-y: auto;
            border: 1px solid var(--gray-light);
            border-radius: 8px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        thead {
            position: sticky;
            top: 0;
            background-color: var(--primary);
            color: white;
        }

        th, td {
            padding: 0.9rem 1rem;
            text-align: left;
            border-bottom: 1px solid var(--gray-light);
            font-size: 0.9rem;
        }

        th {
            font-weight: 600;
        }

        tbody tr:hover {
            background-color: rgba(45, 106, 79, 0.05);
        }

        /* Transaction Panel */
        .transaction-panel {
            height: 100%;
        }

        .cart-items-container {
            max-height: 350px;
            overflow-y: auto;
            margin-bottom: 1.5rem;
            border: 1px solid var(--gray-light);
            border-radius: 8px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem;
            border-bottom: 1px solid var(--gray-light);
        }

        .cart-item:last-child {
            border-bottom: none;
        }

        .cart-item-info h4 {
            font-weight: 600;
            margin-bottom: 5px;
        }

        .cart-item-info .price {
            color: var(--primary);
            font-weight: 700;
        }

        .cart-item-controls {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .quantity-controls {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background-color: var(--gray-light);
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-weight: bold;
            color: var(--dark);
        }

        .quantity-btn:hover {
            background-color: var(--primary-light);
            color: white;
        }

        .quantity {
            font-weight: 700;
            min-width: 30px;
            text-align: center;
        }

        .item-total {
            font-weight: 800;
            color: var(--primary);
            min-width: 100px;
            text-align: right;
        }

        .remove-item {
            background: none;
            border: none;
            color: var(--danger);
            cursor: pointer;
            font-size: 1.1rem;
            margin-left: 10px;
        }

        /* Transaction Summary */
        .transaction-summary {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .summary-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 0.8rem;
            font-size: 1rem;
        }

        .summary-row.total {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--primary);
            border-top: 2px solid var(--gray-light);
            padding-top: 0.8rem;
            margin-top: 0.8rem;
        }

        /* Payment Section */
        .payment-section {
            margin-bottom: 1.5rem;
        }

        .input-group {
            margin-bottom: 1rem;
        }

        .input-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--dark);
        }

        .input-group input {
            width: 100%;
            padding: 0.9rem;
            border: 1px solid var(--gray-light);
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            text-align: right;
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--primary);
        }

        .change-display {
            background-color: var(--success);
            color: white;
            padding: 1rem;
            border-radius: 8px;
            text-align: center;
            font-weight: 700;
            font-size: 1.3rem;
            margin-top: 1rem;
            display: none;
        }

        /* Action Buttons */
        .action-buttons {
            display: flex;
            gap: 1rem;
        }

        .btn {
            flex: 1;
            padding: 1rem;
            border: none;
            border-radius: 8px;
            font-weight: 700;
            font-size: 1.1rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: var(--primary-light);
            transform: translateY(-3px);
        }

        .btn-secondary {
            background-color: var(--gray-light);
            color: var(--dark);
        }

        .btn-secondary:hover {
            background-color: #dde0e4;
        }

        .btn-success {
            background-color: var(--success);
            color: white;
        }

        .btn-success:hover {
            background-color: #218838;
            transform: translateY(-3px);
        }

        /* Footer */
        .footer {
            background-color: var(--dark);
            color: white;
            text-align: center;
            padding: 1.2rem;
            font-size: 0.9rem;
            margin-top: auto;
        }

        /* Empty State */
        .empty-cart {
            text-align: center;
            padding: 3rem 1rem;
            color: var(--gray);
        }

        .empty-cart i {
            font-size: 3rem;
            margin-bottom: 1rem;
            opacity: 0.5;
        }

        /* Responsive */
        @media (max-width: 1200px) {
            .main-content {
                flex-direction: column;
            }
            
            .stats-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                text-align: center;
                gap: 1rem;
            }
            
            .datetime {
                text-align: center;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            }
            
            .action-buttons {
                flex-direction: column;
            }
        }

        @media (max-width: 480px) {
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .products-grid {
                grid-template-columns: 1fr;
            }
            
            .main-content {
                padding: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <div class="logo">
                <i class="fas fa-cash-register"></i>
                <div>
                    <h1>KASIR PRO</h1>
                    <p>Sistem Kasir Lengkap untuk UMKM</p>
                </div>
            </div>
            <div class="datetime">
                <div class="date" id="currentDate">Senin, 5 Januari 2026</div>
                <div class="time" id="currentTime">16:44:30</div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Left Panel -->
            <div class="left-panel">
                <!-- Product Management -->
                <section class="panel-card products-section">
                    <h2><i class="fas fa-boxes"></i> Manajemen Produk & Stok</h2>
                    <div class="products-grid" id="productsGrid">
                        <!-- Product cards will be dynamically inserted here -->
                    </div>
                </section>

                <!-- Sales Report -->
                <section class="panel-card sales-report">
                    <h2><i class="fas fa-chart-line"></i> Laporan Penjualan</h2>
                    <div class="stats-grid">
                        <div class="stat-card total-sales">
                            <div class="stat-value" id="totalSales">Rp 0</div>
                            <div class="stat-label">Total Penjualan</div>
                        </div>
                        <div class="stat-card transactions">
                            <div class="stat-value" id="transactionCount">0</div>
                            <div class="stat-label">Jumlah Transaksi</div>
                        </div>
                        <div class="stat-card avg-transaction">
                            <div class="stat-value" id="avgTransaction">Rp 0</div>
                            <div class="stat-label">Rata-rata per Transaksi</div>
                        </div>
                        <div class="stat-card items-sold">
                            <div class="stat-value" id="itemsSold">0</div>
                            <div class="stat-label">Item Terjual</div>
                        </div>
                    </div>
                    
                    <!-- Sales History Table -->
                    <h3 style="margin-top: 1.5rem; margin-bottom: 1rem; color: var(--primary);">Riwayat Transaksi</h3>
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
                                <!-- Sales history will be dynamically inserted here -->
                            </tbody>
                        </table>
                    </div>
                </section>
            </div>

            <!-- Right Panel - Transaction -->
            <div class="right-panel">
                <section class="panel-card transaction-panel">
                    <h2><i class="fas fa-shopping-cart"></i> Transaksi Aktif</h2>
                    
                    <!-- Cart Items -->
                    <div class="cart-items-container" id="cartContainer">
                        <div class="empty-cart" id="emptyCart">
                            <i class="fas fa-shopping-basket"></i>
                            <p>Keranjang belanja kosong</p>
                            <p>Pilih produk dari daftar di sebelah kiri</p>
                        </div>
                        <!-- Cart items will be dynamically inserted here -->
                    </div>

                    <!-- Transaction Summary -->
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

                    <!-- Payment Section -->
                    <div class="payment-section">
                        <div class="input-group">
                            <label for="cashAmount"><i class="fas fa-money-bill-wave"></i> Uang Diterima (Cash)</label>
                            <input type="number" id="cashAmount" placeholder="Masukkan jumlah uang" min="0" value="0">
                        </div>
                        <div class="change-display" id="changeDisplay">
                            Kembalian: <span id="changeAmount">Rp 0</span>
                        </div>
                    </div>

                    <!-- Action Buttons -->
                    <div class="action-buttons">
                        <button class="btn btn-secondary" id="clearCartBtn">
                            <i class="fas fa-trash-alt"></i> Kosongkan
                        </button>
                        <button class="btn btn-success" id="checkoutBtn">
                            <i class="fas fa-receipt"></i> Selesaikan Transaksi
                        </button>
                    </div>
                </section>
            </div>
        </main>

        <!-- Footer -->
        <footer class="footer">
            <p>© 2026 Jennaira Group • KASIR PRO • Sistem Kasir Lengkap untuk UMKM</p>
        </footer>
    </div>

    <script>
        // Data produk sesuai dengan URL
        const products = [
            { id: 1, name: "Beras 5kg", code: "BR001", price: 60000, category: "Sembako • pack", stock: 45, sold: 125 },
            { id: 2, name: "Minyak Goreng 2L", code: "MG002", price: 35000, category: "Sembako • botol", stock: 28, sold: 89 },
            { id: 3, name: "Gula Pasir 1kg", code: "GP003", price: 15000, category: "Sembako • kg", stock: 12, sold: 156 },
            { id: 4, name: "Telur 1kg", code: "TL004", price: 28000, category: "Sembako • kg", stock: 8, sold: 67 },
            { id: 5, name: "Sabun Mandi", code: "SB005", price: 5000, category: "Kebersihan • pcs", stock: 120, sold: 234 },
            { id: 6, name: "Shampoo", code: "SP006", price: 12000, category: "Kebersihan • botol", stock: 35, sold: 78 },
            { id: 7, name: "Air Mineral 600ml", code: "AM007", price: 3000, category: "Minuman • botol", stock: 150, sold: 345 },
            { id: 8, name: "Kopi Sachet", code: "KS008", price: 2000, category: "Minuman • pcs", stock: 89, sold: 289 },
            { id: 9, name: "Teh Celup", code: "TC009", price: 1500, category: "Minuman • pcs", stock: 65, sold: 167 },
            { id: 10, name: "Biskuit", code: "BS010", price: 8000, category: "Snack • pack", stock: 42, sold: 134 }
        ];

        // Data transaksi (riwayat)
        let salesHistory = [];
        
        // Keranjang belanja
        let cart = [];
        
        // Statistik penjualan
        let salesStats = {
            totalSales: 0,
            transactionCount: 0,
            totalItemsSold: 0
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

        // Fungsi format Rupiah
        function formatRupiah(amount) {
            return `Rp ${amount.toLocaleString('id-ID')}`;
        }

        // Fungsi update tanggal dan waktu
        function updateDateTime() {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const dateString = now.toLocaleDateString('id-ID', options);
            const timeString = now.toLocaleTimeString('id-ID');
            
            document.getElementById('currentDate').textContent = dateString;
            document.getElementById('currentTime').textContent = timeString;
        }

        // Inisialisasi produk
        function initializeProducts() {
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
                    <div class="product-category">${product.category}</div>
                    <div class="product-stats">
                        <div class="stock">Stok: <span>${product.stock}</span></div>
                        <div class="sold">Terjual: <span>${product.sold}</span></div>
                    </div>
                `;
                
                productCard.addEventListener('click', () => addToCart(product.id));
                productsGrid.appendChild(productCard);
            });
        }

        // Tambah produk ke keranjang
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            
            if (!product) return;
            
            // Cek apakah produk sudah ada di keranjang
            const existingItemIndex = cart.findIndex(item => item.id === productId);
            
            if (existingItemIndex !== -1) {
                // Jika produk sudah ada, tambah kuantitas
                if (cart[existingItemIndex].quantity < product.stock) {
                    cart[existingItemIndex].quantity += 1;
                } else {
                    alert(`Stok ${product.name} tidak mencukupi! Stok tersisa: ${product.stock}`);
                    return;
                }
            } else {
                // Jika produk belum ada, tambah item baru
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    quantity: 1,
                    code: product.code
                });
            }
            
            updateCartDisplay();
        }

        // Update tampilan keranjang
        function updateCartDisplay() {
            // Kosongkan container
            cartContainer.innerHTML = '';
            
            if (cart.length === 0) {
                // Tampilkan pesan keranjang kosong
                cartContainer.appendChild(emptyCart);
                emptyCart.style.display = 'block';
            } else {
                emptyCart.style.display = 'none';
                
                // Hitung total
                let subtotal = 0;
                let totalItems = 0;
                
                // Tampilkan setiap item di keranjang
                cart.forEach((item, index) => {
                    const itemTotal = item.price * item.quantity;
                    subtotal += itemTotal;
                    totalItems += item.quantity;
                    
                    const cartItem = document.createElement('div');
                    cartItem.className = 'cart-item';
                    
                    cartItem.innerHTML = `
                        <div class="cart-item-info">
                            <h4>${item.name} (${item.code})</h4>
                            <div class="price">${formatRupiah(item.price)}</div>
                        </div>
                        <div class="cart-item-controls">
                            <div class="quantity-controls">
                                <button class="quantity-btn decrease" data-index="${index}">-</button>
                                <div class="quantity">${item.quantity}</div>
                                <button class="quantity-btn increase" data-index="${index}">+</button>
                            </div>
                            <div class="item-total">${formatRupiah(itemTotal)}</div>
                            <button class="remove-item" data-index="${index}">
                                <i class="fas fa-times"></i>
                            </button>
                        </div>
                    `;
                    
                    cartContainer.appendChild(cartItem);
                });
                
                // Tambah event listeners untuk tombol kuantitas
                document.querySelectorAll('.decrease').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const index = parseInt(e.target.dataset.index);
                        decreaseQuantity(index);
                    });
                });
                
                document.querySelectorAll('.increase').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const index = parseInt(e.target.dataset.index);
                        increaseQuantity(index);
                    });
                });
                
                document.querySelectorAll('.remove-item').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const index = parseInt(e.currentTarget.dataset.index);
                        removeFromCart(index);
                    });
                });
                
                // Update ringkasan transaksi
                const tax = subtotal * 0.1;
                const total = subtotal + tax;
                
                subtotalElement.textContent = formatRupiah(subtotal);
                taxElement.textContent = formatRupiah(tax);
                totalElement.textContent = formatRupiah(total);
                
                // Update statistik item terjual
                itemsSoldElement.textContent = totalItems;
            }
            
            // Update tampilan kembalian
            calculateChange();
        }

        // Kurangi kuantitas item
        function decreaseQuantity(index) {
            if (cart[index].quantity > 1) {
                cart[index].quantity -= 1;
            } else {
                // Jika kuantitas 1, hapus item dari keranjang
                cart.splice(index, 1);
            }
            
            updateCartDisplay();
        }

        // Tambah kuantitas item
        function increaseQuantity(index) {
            const productId = cart[index].id;
            const product = products.find(p => p.id === productId);
            
            if (cart[index].quantity < product.stock) {
                cart[index].quantity += 1;
            } else {
                alert(`Stok ${product.name} tidak mencukupi! Stok tersisa: ${product.stock}`);
            }
            
            updateCartDisplay();
        }

        // Hapus item dari keranjang
        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartDisplay();
        }

        // Kosongkan keranjang
        function clearCart() {
            cart = [];
            updateCartDisplay();
        }

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

        // Proses checkout
        function checkout() {
            if (cart.length === 0) {
                alert('Keranjang belanja kosong! Tambahkan produk terlebih dahulu.');
                return;
            }
            
            const cashAmount = parseFloat(cashAmountInput.value) || 0;
            const totalText = totalElement.textContent.replace('Rp ', '').replace(/\./g, '');
            const total = parseFloat(totalText) || 0;
            
            if (cashAmount < total) {
                alert(`Uang yang diterima kurang! Total: ${formatRupiah(total)}, Diterima: ${formatRupiah(cashAmount)}`);
                return;
            }
            
            // Generate ID transaksi
            const transactionId = 'TRX' + Date.now().toString().slice(-8);
            const now = new Date();
            const dateString = now.toLocaleDateString('id-ID');
            const timeString = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
            
            // Hitung total item
            let totalItems = 0;
            cart.forEach(item => {
                totalItems += item.quantity;
                
                // Update stok produk
                const productIndex = products.findIndex(p => p.id === item.id);
                if (productIndex !== -1) {
                    products[productIndex].stock -= item.quantity;
                    products[productIndex].sold += item.quantity;
                }
            });
            
            // Update statistik penjualan
            salesStats.totalSales += total;
            salesStats.transactionCount += 1;
            salesStats.totalItemsSold += totalItems;
            
            // Simpan transaksi ke riwayat
            const transaction = {
                id: transactionId,
                date: dateString + ' ' + timeString,
                items: cart.map(item => `${item.name} (${item.quantity}x)`).join(', '),
                total: total,
                cash: cashAmount,
                change: cashAmount - total
            };
            
            salesHistory.unshift(transaction);
            
            // Update tampilan statistik
            updateSalesStats();
            
            // Update riwayat transaksi
            updateSalesHistory();
            
            // Update daftar produk
            initializeProducts();
            
            // Tampilkan struk
            alert(`Transaksi berhasil!\nID Transaksi: ${transactionId}\nTotal: ${formatRupiah(total)}\nBayar: ${formatRupiah(cashAmount)}\nKembali: ${formatRupiah(cashAmount - total)}`);
            
            // Reset keranjang dan form pembayaran
            clearCart();
            cashAmountInput.value = '0';
            calculateChange();
        }

        // Update statistik penjualan
        function updateSalesStats() {
            totalSalesElement.textContent = formatRupiah(salesStats.totalSales);
            transactionCountElement.textContent = salesStats.transactionCount;
            
            const avgTransaction = salesStats.transactionCount > 0 
                ? salesStats.totalSales / salesStats.transactionCount 
                : 0;
            avgTransactionElement.textContent = formatRupiah(Math.round(avgTransaction));
            
            itemsSoldElement.textContent = salesStats.totalItemsSold;
        }

        // Update riwayat penjualan
        function updateSalesHistory() {
            salesHistoryTbody.innerHTML = '';
            
            salesHistory.forEach((transaction, index) => {
                const row = document.createElement('tr');
                
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${transaction.date}</td>
                    <td>${transaction.id}</td>
                    <td>${transaction.items}</td>
                    <td>${formatRupiah(transaction.total)}</td>
                    <td>${formatRupiah(transaction.cash)}</td>
                    <td>${formatRupiah(transaction.change)}</td>
                `;
                
                salesHistoryTbody.appendChild(row);
            });
        }

        // Inisialisasi aplikasi
        function initializeApp() {
            // Update waktu
            updateDateTime();
            setInterval(updateDateTime, 1000);
            
            // Inisialisasi produk
            initializeProducts();
            
            // Inisialisasi keranjang
            updateCartDisplay();
            
            // Inisialisasi statistik
            updateSalesStats();
            
            // Inisialisasi riwayat transaksi
            updateSalesHistory();
            
            // Event listeners
            clearCartBtn.addEventListener('click', clearCart);
            checkoutBtn.addEventListener('click', checkout);
            cashAmountInput.addEventListener('input', calculateChange);
            
            // Contoh data riwayat awal
            salesHistory = [
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
            
            // Update statistik awal berdasarkan riwayat
            salesStats.totalSales = 192500;
            salesStats.transactionCount = 2;
            salesStats.totalItemsSold = 11;
            
            updateSalesStats();
            updateSalesHistory();
        }

        // Jalankan aplikasi ketika halaman dimuat
        document.addEventListener('DOMContentLoaded', initializeApp);
    </script>
</body>
</html>
