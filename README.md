
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>DARK STORE | NFT | ПОДАРКИ | АНОНИМНЫЕ НОМЕРА</title>
    
    <!-- Telegram WebApp SDK -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    
    <!-- TON Connect -->
    <script src="https://unpkg.com/tonconnect-ui@latest/dist/tonconnect-ui.umd.js"></script>
    <script src="https://unpkg.com/ton@latest/dist/ton.min.js"></script>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        :root {
            --bg-primary: #0a0a0a;
            --bg-secondary: #141414;
            --text-primary: #ffffff;
            --text-secondary: #a0a0a0;
            --accent: #8774e1;
            --accent-glow: rgba(135, 116, 225, 0.4);
            --success: #4caf50;
            --danger: #f44336;
            --card-bg: #1e1e1e;
            --border: #2a2a2a;
        }

        body {
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            padding: 16px;
        }

        /* АДАПТАЦИЯ ПОД ПК И ТЕЛЕФОН */
        .desktop-only {
            display: none;
        }

        .mobile-only {
            display: block;
        }

        @media (min-width: 1024px) {
            body {
                padding: 30px;
                background: radial-gradient(circle at 20% 30%, #1a1a2e, #0a0a0a);
            }

            .desktop-only {
                display: block;
            }

            .mobile-only {
                display: none;
            }

            .container {
                max-width: 1400px;
                margin: 0 auto;
                padding: 0 40px;
            }

            .products-grid {
                grid-template-columns: repeat(4, 1fr) !important;
                gap: 25px !important;
            }

            .product-card {
                transition: transform 0.3s, box-shadow 0.3s;
            }

            .product-card:hover {
                transform: translateY(-10px);
                box-shadow: 0 20px 40px var(--accent-glow);
            }
        }

        /* КОНТЕЙНЕР */
        .container {
            max-width: 600px;
            margin: 0 auto;
            position: relative;
        }

        /* ХЕДЕР С БАЛАНСОМ */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            animation: rotate 20s linear infinite;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
            position: relative;
            z-index: 2;
        }

        .avatar {
            width: 50px;
            height: 50px;
            border-radius: 25px;
            background: rgba(255,255,255,0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            font-weight: bold;
            backdrop-filter: blur(10px);
        }

        .user-details {
            flex: 1;
        }

        .user-name {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .user-level {
            font-size: 12px;
            opacity: 0.8;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .level-bar {
            width: 80px;
            height: 4px;
            background: rgba(255,255,255,0.3);
            border-radius: 2px;
            overflow: hidden;
        }

        .level-progress {
            width: 30%;
            height: 100%;
            background: white;
            border-radius: 2px;
        }

        /* БАЛАНС */
        .balance-section {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 20px;
            border: 1px solid var(--border);
        }

        .balance-label {
            color: var(--text-secondary);
            font-size: 14px;
            margin-bottom: 8px;
        }

        .balance-amount {
            font-size: 36px;
            font-weight: 700;
            color: var(--accent);
            margin-bottom: 15px;
            text-shadow: 0 0 20px var(--accent-glow);
        }

        .balance-actions {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .ton-connect-btn {
            background: #0088cc;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 14px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            flex: 1;
            justify-content: center;
        }

        /* КАТЕГОРИИ */
        .categories {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 10px 0;
            margin-bottom: 20px;
            scrollbar-width: none;
        }

        .categories::-webkit-scrollbar {
            display: none;
        }

        .category {
            background: var(--card-bg);
            border: 1px solid var(--border);
            padding: 12px 24px;
            border-radius: 30px;
            font-size: 14px;
            font-weight: 600;
            color: var(--text-secondary);
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.3s;
        }

        .category.active {
            background: var(--accent);
            color: white;
            border-color: var(--accent);
        }

        /* СЕКЦИИ ТОВАРОВ */
        .section-title {
            font-size: 24px;
            font-weight: 700;
            margin: 30px 0 20px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .products-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }

        .product-card {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 16px;
            position: relative;
            overflow: hidden;
        }

        .product-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 100px;
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
            z-index: 1;
        }

        .product-badge {
            position: absolute;
            top: 10px;
            right: 10px;
            background: var(--accent);
            color: white;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            z-index: 2;
        }

        .product-emoji {
            font-size: 40px;
            margin-bottom: 10px;
            position: relative;
            z-index: 2;
        }

        .product-title {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 5px;
            position: relative;
            z-index: 2;
        }

        .product-description {
            font-size: 12px;
            color: var(--text-secondary);
            margin-bottom: 15px;
            position: relative;
            z-index: 2;
        }

        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            z-index: 2;
        }

        .product-price {
            font-size: 18px;
            font-weight: 700;
            color: var(--accent);
        }

        .product-price small {
            font-size: 12px;
            color: var(--text-secondary);
            font-weight: normal;
        }

        .buy-btn {
            background: var(--accent);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 14px;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .buy-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px var(--accent-glow);
        }

        /* NFT СПЕЦИАЛЬНЫЙ СТИЛЬ */
        .nft-card {
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            border: 1px solid #4a4a8a;
        }

        .nft-badge {
            background: #ffd700;
            color: #000;
        }

        .nft-price {
            color: #ffd700;
        }

        /* АНОНИМНЫЕ НОМЕРА */
        .number-card {
            background: linear-gradient(135deg, #1e3c72, #2a5298);
        }

        /* ПОДАРКИ */
        .gift-card {
            background: linear-gradient(135deg, #711c91, #ea00d9);
        }

        /* КОРЗИНА */
        .cart-panel {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: var(--card-bg);
            border-top: 1px solid var(--border);
            padding: 20px;
            transform: translateY(100%);
            transition: transform 0.3s;
            z-index: 1000;
            max-height: 80vh;
            overflow-y: auto;
        }

        .cart-panel.active {
            transform: translateY(0);
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .cart-title {
            font-size: 20px;
            font-weight: 600;
        }

        .cart-close {
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
        }

        .cart-items {
            margin-bottom: 20px;
        }

        .cart-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px 0;
            border-bottom: 1px solid var(--border);
        }

        .cart-item-emoji {
            font-size: 24px;
        }

        .cart-item-info {
            flex: 1;
        }

        .cart-item-title {
            font-size: 14px;
            font-weight: 600;
        }

        .cart-item-price {
            font-size: 12px;
            color: var(--accent);
        }

        .cart-item-quantity {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .quantity-btn {
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 12px;
            cursor: pointer;
        }

        .cart-total {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 20px 0;
            font-size: 18px;
            font-weight: 600;
        }

        .cart-total-amount {
            color: var(--accent);
        }

        .checkout-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }

        .checkout-rub {
            background: var(--success);
            color: white;
            border: none;
            padding: 16px;
            border-radius: 16px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
        }

        .checkout-ton {
            background: #0088cc;
            color: white;
            border: none;
            padding: 16px;
            border-radius: 16px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .clear-cart {
            background: var(--danger);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 12px;
            font-size: 14px;
            cursor: pointer;
        }

        /* КНОПКА КОРЗИНЫ */
        .cart-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--accent);
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 4px 20px var(--accent-glow);
            border: none;
            z-index: 999;
        }

        .cart-count {
            position: absolute;
            top: -5px;
            right: -5px;
            background: var(--danger);
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 12px;
            font-size: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }

        /* МОДАЛКА ОПЛАТЫ */
        .payment-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.9);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            padding: 20px;
        }

        .payment-modal.active {
            display: flex;
        }

        .payment-content {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 30px;
            max-width: 400px;
            width: 100%;
            border: 1px solid var(--border);
        }

        .payment-title {
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 20px;
            text-align: center;
        }

        .payment-details {
            background: var(--bg-secondary);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .payment-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .payment-total {
            font-size: 20px;
            font-weight: 700;
            color: var(--accent);
            text-align: center;
            margin: 20px 0;
        }

        .payment-address {
            background: var(--bg-primary);
            padding: 12px;
            border-radius: 12px;
            font-family: monospace;
            word-break: break-all;
            margin-bottom: 20px;
        }

        .payment-status {
            text-align: center;
            padding: 10px;
            border-radius: 12px;
            margin-bottom: 20px;
        }

        .payment-status.pending {
            background: rgba(255, 193, 7, 0.2);
            color: #ffc107;
        }

        .payment-status.success {
            background: rgba(76, 175, 80, 0.2);
            color: #4caf50;
        }

        .payment-close {
            background: var(--accent);
            color: white;
            border: none;
            padding: 16px;
            border-radius: 16px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
        }

        /* ПК СПЕЦИАЛЬНЫЕ ЭЛЕМЕНТЫ */
        .desktop-stats {
            display: none;
        }

        @media (min-width: 1024px) {
            .desktop-stats {
                display: grid;
                grid-template-columns: repeat(3, 1fr);
                gap: 20px;
                margin-bottom: 30px;
            }

            .stat-card {
                background: var(--card-bg);
                border: 1px solid var(--border);
                border-radius: 20px;
                padding: 20px;
                text-align: center;
            }

            .stat-value {
                font-size: 32px;
                font-weight: 700;
                color: var(--accent);
                margin: 10px 0;
            }

            .stat-label {
                color: var(--text-secondary);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ХЕДЕР С ПОЛЬЗОВАТЕЛЕМ -->
        <div class="header">
            <div class="user-info">
                <div class="avatar" id="userAvatar">👤</div>
                <div class="user-details">
                    <div class="user-name" id="userName">Загрузка...</div>
                    <div class="user-level">
                        <span>Уровень 3</span>
                        <div class="level-bar">
                            <div class="level-progress" style="width: 45%"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- БАЛАНС -->
        <div class="balance-section">
            <div class="balance-label">Ваш баланс</div>
            <div class="balance-amount" id="userBalance">0 ₽</div>
            <div class="balance-actions">
                <button class="ton-connect-btn" id="connectWalletBtn">
                    <span>💰</span> ПОДКЛЮЧИТЬ КОШЕЛЕК
                </button>
            </div>
        </div>

        <!-- СТАТИСТИКА ДЛЯ ПК -->
        <div class="desktop-stats">
            <div class="stat-card">
                <div>🔥</div>
                <div class="stat-value">1,234</div>
                <div class="stat-label">Продано NFT</div>
            </div>
            <div class="stat-card">
                <div>📱</div>
                <div class="stat-value">567</div>
                <div class="stat-label">Анонимных номеров</div>
            </div>
            <div class="stat-card">
                <div>🎁</div>
                <div class="stat-value">890</div>
                <div class="stat-label">Подарков отправлено</div>
            </div>
        </div>

        <!-- КАТЕГОРИИ -->
        <div class="categories">
            <div class="category active" onclick="filterProducts('all')">ВСЕ</div>
            <div class="category" onclick="filterProducts('nft')">🎨 NFT</div>
            <div class="category" onclick="filterProducts('numbers')">📱 НОМЕРА</div>
            <div class="category" onclick="filterProducts('gifts')">🎁 ПОДАРКИ</div>
            <div class="category" onclick="filterProducts('premium')">⭐ PREMIUM</div>
        </div>

        <!-- NFT СЕКЦИЯ -->
        <div class="section-title">🎨 КОЛЛЕКЦИЯ NFT</div>
        <div class="products-grid" id="nftGrid"></div>

        <!-- АНОНИМНЫЕ НОМЕРА -->
        <div class="section-title">📱 АНОНИМНЫЕ НОМЕРА</div>
        <div class="products-grid" id="numbersGrid"></div>

        <!-- ПОДАРКИ -->
        <div class="section-title">🎁 ПОДАРКИ</div>
        <div class="products-grid" id="giftsGrid"></div>

        <!-- PREMIUM -->
        <div class="section-title">⭐ TELEGRAM PREMIUM</div>
        <div class="products-grid" id="premiumGrid"></div>
    </div>

    <!-- КНОПКА КОРЗИНЫ -->
    <button class="cart-button" onclick="toggleCart()">
        🛒
        <span class="cart-count" id="cartCount">0</span>
    </button>

    <!-- ПАНЕЛЬ КОРЗИНЫ -->
    <div class="cart-panel" id="cartPanel">
        <div class="cart-header">
            <span class="cart-title">🛒 КОРЗИНА</span>
            <button class="cart-close" onclick="toggleCart()">✕</button>
        </div>

        <div class="cart-items" id="cartItems"></div>

        <div class="cart-total">
            <span>ИТОГО:</span>
            <span class="cart-total-amount" id="cartTotal">0 ₽</span>
        </div>

        <div class="checkout-buttons">
            <button class="checkout-rub" onclick="checkout('rub')">💰 ОПЛАТИТЬ РУБЛЯМИ</button>
            <button class="checkout-ton" onclick="checkout('ton')" id="tonCheckoutBtn">
                <span>💎</span> TON
            </button>
        </div>
        
        <button class="clear-cart" onclick="clearCart()">ОЧИСТИТЬ КОРЗИНУ</button>
    </div>

    <!-- МОДАЛКА ОПЛАТЫ -->
    <div class="payment-modal" id="paymentModal">
        <div class="payment-content">
            <div class="payment-title" id="paymentTitle">ОПЛАТА TON</div>
            
            <div class="payment-details">
                <div class="payment-row">
                    <span>Сумма:</span>
                    <span id="paymentAmount">0 TON</span>
                </div>
                <div class="payment-row">
                    <span>Комиссия:</span>
                    <span>0.01 TON</span>
                </div>
            </div>

            <div class="payment-total" id="paymentTotal">0 TON</div>

            <div class="payment-address" id="paymentAddress">
                Адрес для оплаты появится после подключения кошелька
            </div>

            <div class="payment-status pending" id="paymentStatus">
                ⏳ ОЖИДАНИЕ ПОДКЛЮЧЕНИЯ КОШЕЛЬКА
            </div>

            <button class="payment-close" onclick="closePaymentModal()">ЗАКРЫТЬ</button>
        </div>
    </div>

    <script>
        // Telegram WebApp
        let tg = window.Telegram.WebApp;
        tg.expand();
        
        // Данные пользователя
        let user = tg.initDataUnsafe?.user;
        let cart = [];
        let walletAddress = null;
        let tonConnectUI = null;
        
        // Данные для отображения
        let nftProducts = [
            { id: 1, emoji: '🎨', title: 'Cosmic Dragon', desc: 'Редкий NFT дракон', price: 150, priceTon: 2.5, category: 'nft' },
            { id: 2, emoji: '👾', title: 'Pixel Punk', desc: 'Уникальный пиксель-арт', price: 200, priceTon: 3.2, category: 'nft' },
            { id: 3, emoji: '🌈', title: 'Neon Genesis', desc: 'Неоновое искусство', price: 300, priceTon: 5.0, category: 'nft' },
            { id: 4, emoji: '🤖', title: 'Cyber Bot', desc: 'Коллекционный робот', price: 250, priceTon: 4.1, category: 'nft' }
        ];
        
        let numberProducts = [
            { id: 5, emoji: '🇺🇸', title: 'USA +1', desc: 'Анонимный номер США', price: 500, priceTon: 8.5, category: 'numbers' },
            { id: 6, emoji: '🇬🇧', title: 'UK +44', desc: 'Великобритания', price: 550, priceTon: 9.2, category: 'numbers' },
            { id: 7, emoji: '🇩🇪', title: 'Germany +49', desc: 'Германия', price: 450, priceTon: 7.8, category: 'numbers' },
            { id: 8, emoji: '🇷🇺', title: 'Russia +7', desc: 'Россия', price: 400, priceTon: 6.9, category: 'numbers' }
        ];
        
        let giftProducts = [
            { id: 9, emoji: '🎁', title: 'Секретный подарок', desc: 'Рандомный подарок', price: 100, priceTon: 1.8, category: 'gifts' },
            { id: 10, emoji: '💎', title: 'Алмазная коробка', desc: 'Премиум подарок', price: 500, priceTon: 8.9, category: 'gifts' },
            { id: 11, emoji: '👑', title: 'Королевский дар', desc: 'VIP набор', price: 1000, priceTon: 17.5, category: 'gifts' },
            { id: 12, emoji: '🎮', title: 'Игровой набор', desc: 'Gift для геймеров', price: 300, priceTon: 5.2, category: 'gifts' }
        ];
        
        let premiumProducts = [
            { id: 13, emoji: '⭐', title: 'Premium 1 месяц', desc: 'Telegram Premium', price: 299, priceTon: 5.0, category: 'premium' },
            { id: 14, emoji: '🌟', title: 'Premium 6 месяцев', desc: 'Со скидкой 15%', price: 1499, priceTon: 25.0, category: 'premium' },
            { id: 15, emoji: '💫', title: 'Premium 1 год', desc: 'Максимальная выгода', price: 2699, priceTon: 45.0, category: 'premium' },
            { id: 16, emoji: '✨', title: 'Premium + Номер', desc: 'Комбо набор', price: 799, priceTon: 13.5, category: 'premium' }
        ];

        // Инициализация
        function initApp() {
            // Показываем пользователя
            if (user) {
                document.getElementById('userName').textContent = user.first_name || 'Пользователь';
                if (user.last_name) {
                    document.getElementById('userName').textContent += ' ' + user.last_name;
                }
                document.getElementById('userAvatar').textContent = user.first_name ? user.first_name[0].toUpperCase() : '👤';
            } else {
                document.getElementById('userName').textContent = 'Гость';
            }

            // Загружаем товары
            renderProducts();
            
            // Инициализируем TON Connect
            initTonConnect();
            
            // Загружаем корзину из localStorage
            loadCart();
        }

        // TON Connect инициализация
        function initTonConnect() {
            // Здесь будет инициализация TON Connect
            // В реальном проекте нужно добавить свой manifest
            console.log('TON Connect готов к подключению');
        }

        // Подключение кошелька
        async function connectWallet() {
            try {
                // Здесь реальное подключение к TON кошельку
                // Для демо показываем модалку
                document.getElementById('paymentModal').classList.add('active');
                document.getElementById('paymentStatus').textContent = '✅ КОШЕЛЕК ПОДКЛЮЧЕН';
                document.getElementById('paymentStatus').className = 'payment-status success';
                document.getElementById('paymentAddress').textContent = 'EQD...' + Math.random().toString(36).substring(2, 10).toUpperCase();
                
                walletAddress = 'EQD...CONNECTED';
                document.getElementById('connectWalletBtn').innerHTML = '<span>✅</span> КОШЕЛЕК ПОДКЛЮЧЕН';
            } catch (error) {
                alert('Ошибка подключения кошелька: ' + error.message);
            }
        }

        // Рендер товаров
        function renderProducts() {
            renderNft();
            renderNumbers();
            renderGifts();
            renderPremium();
        }

        function renderNft() {
            const grid = document.getElementById('nftGrid');
            grid.innerHTML = '';
            nftProducts.forEach(product => {
                grid.appendChild(createProductCard(product, 'nft-card', 'nft-badge', 'nft-price'));
            });
        }

        function renderNumbers() {
            const grid = document.getElementById('numbersGrid');
            grid.innerHTML = '';
            numberProducts.forEach(product => {
                grid.appendChild(createProductCard(product, 'number-card'));
            });
        }

        function renderGifts() {
            const grid = document.getElementById('giftsGrid');
            grid.innerHTML = '';
            giftProducts.forEach(product => {
                grid.appendChild(createProductCard(product, 'gift-card'));
            });
        }

        function renderPremium() {
            const grid = document.getElementById('premiumGrid');
            grid.innerHTML = '';
            premiumProducts.forEach(product => {
                grid.appendChild(createProductCard(product));
            });
        }

        function createProductCard(product, cardClass = '', badgeClass = '', priceClass = '') {
            const card = document.createElement('div');
            card.className = `product-card ${cardClass}`;
            card.setAttribute('data-category', product.category);
            
            card.innerHTML = `
                <div class="product-badge ${badgeClass}">${product.category === 'nft' ? 'NFT' : product.category === 'numbers' ? 'НОМЕР' : product.category === 'gifts' ? 'ПОДАРОК' : 'PREMIUM'}</div>
                <div class="product-emoji">${product.emoji}</div>
                <div class="product-title">${product.title}</div>
                <div class="product-description">${product.desc}</div>
                <div class="product-footer">
                    <div class="product-price ${priceClass}">
                        ${product.price} ₽<br>
                        <small>≈ ${product.priceTon} TON</small>
                    </div>
                    <button class="buy-btn" onclick="addToCart(${product.id})">В КОРЗИНУ</button>
                </div>
            `;
            
            return card;
        }

        // Фильтр товаров
        function filterProducts(category) {
            // Обновляем активную категорию
            document.querySelectorAll('.category').forEach(cat => {
                cat.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Показываем/скрываем секции
            const sections = {
                'nft': document.getElementById('nftGrid').closest('.section-title'),
                'numbers': document.getElementById('numbersGrid').closest('.section-title'),
                'gifts': document.getElementById('giftsGrid').closest('.section-title'),
                'premium': document.getElementById('premiumGrid').closest('.section-title')
            };
            
            if (category === 'all') {
                Object.values(sections).forEach(section => {
                    section.style.display = 'block';
                    section.nextElementSibling.style.display = 'grid';
                });
            } else {
                Object.entries(sections).forEach(([cat, section]) => {
                    if (cat === category) {
                        section.style.display = 'block';
                        section.nextElementSibling.style.display = 'grid';
                    } else {
                        section.style.display = 'none';
                        section.nextElementSibling.style.display = 'none';
                    }
                });
            }
        }

        // Добавление в корзину
        function addToCart(productId) {
            let product = [...nftProducts, ...numberProducts, ...giftProducts, ...premiumProducts]
                .find(p => p.id === productId);
            
            if (product) {
                const existingItem = cart.find(item => item.id === productId);
                
                if (existingItem) {
                    existingItem.quantity += 1;
                } else {
                    cart.push({
                        ...product,
                        quantity: 1
                    });
                }
                
                saveCart();
                updateCartUI();
                
                // Показываем корзину
                document.getElementById('cartPanel').classList.add('active');
            }
        }

        // Сохранение корзины
        function saveCart() {
            localStorage.setItem('cart', JSON.stringify(cart));
        }

        // Загрузка корзины
        function loadCart() {
            const saved = localStorage.getItem('cart');
            if (saved) {
                cart = JSON.parse(saved);
                updateCartUI();
            }
        }

        // Обновление UI корзины
        function updateCartUI() {
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');
            const cartCount = document.getElementById('cartCount');
            
            if (cart.length === 0) {
                cartItems.innerHTML = '<p style="text-align: center; color: #666;">Корзина пуста</p>';
                cartTotal.textContent = '0 ₽';
                cartCount.textContent = '0';
                return;
            }
            
            let totalRub = 0;
            let totalItems = 0;
            let itemsHtml = '';
            
            cart.forEach(item => {
                totalRub += item.price * item.quantity;
                totalItems += item.quantity;
                
                itemsHtml += `
                    <div class="cart-item">
                        <div class="cart-item-emoji">${item.emoji}</div>
                        <div class="cart-item-info">
                            <div class="cart-item-title">${item.title}</div>
                            <div class="cart-item-price">${item.price} ₽</div>
                        </div>
                        <div class="cart-item-quantity">
                            <button class="quantity-btn" onclick="changeQuantity(${item.id}, -1)">-</button>
                            <span>${item.quantity}</span>
                            <button class="quantity-btn" onclick="changeQuantity(${item.id}, 1)">+</button>
                        </div>
                    </div>
                `;
            });
            
            cartItems.innerHTML = itemsHtml;
            cartTotal.textContent = `${totalRub} ₽`;
            cartCount.textContent = totalItems;
        }

        // Изменение количества
        function changeQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += delta;
                if (item.quantity <= 0) {
                    cart = cart.filter(i => i.id !== productId);
                }
                saveCart();
                updateCartUI();
            }
        }

        // Очистка корзины
        function clearCart() {
            cart = [];
            saveCart();
            updateCartUI();
            document.getElementById('cartPanel').classList.remove('active');
        }

        // Переключение корзины
        function toggleCart() {
            document.getElementById('cartPanel').classList.toggle('active');
        }

        // Оформление заказа
        function checkout(type) {
            if (cart.length === 0) {
                alert('Корзина пуста!');
                return;
            }
            
            if (type === 'ton' && !walletAddress) {
                connectWallet();
                return;
            }
            
            // Считаем сумму
            let totalRub = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            let totalTon = cart.reduce((sum, item) => sum + (item.priceTon * item.quantity), 0);
            
            // Формируем данные для отправки
            let orderData = {
                action: 'new_order',
                items: cart,
                total_rub: totalRub,
                total_ton: totalTon,
                user_id: user?.id || 0,
                user_name: user?.first_name || 'Гость',
                wallet: walletAddress || null,
                payment_type: type
            };
            
            // Отправляем в бота
            tg.sendData(JSON.stringify(orderData));
            
            if (type === 'rub') {
                alert(`Заказ оформлен!\nСумма: ${totalRub} ₽\nДанные отправлены в бота`);
            } else {
                showTonPayment(totalTon);
            }
            
            // Очищаем корзину после успешной оплаты
            clearCart();
        }

        // Показ TON оплаты
        function showTonPayment(amount) {
            document.getElementById('paymentModal').classList.add('active');
            document.getElementById('paymentTitle').textContent = 'ОПЛАТА TON';
            document.getElementById('paymentAmount').textContent = `${amount.toFixed(2)} TON`;
            document.getElementById('paymentTotal').textContent = `${(amount + 0.01).toFixed(2)} TON`;
            document.getElementById('paymentStatus').textContent = '⏳ ОЖИДАНИЕ ОПЛАТЫ';
            document.getElementById('paymentStatus').className = 'payment-status pending';
        }

        // Закрытие модалки оплаты
        function closePaymentModal() {
            document.getElementById('paymentModal').classList.remove('active');
        }

        // Обработчики событий
        document.getElementById('connectWalletBtn').addEventListener('click', connectWallet);

        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
