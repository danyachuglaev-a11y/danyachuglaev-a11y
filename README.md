<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>МОЙ МИНИАПП | ТЕЛЕГРАМ</title>
    <!-- Подключаем Telegram WebApp SDK -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --tg-theme-bg-color: var(--tg-theme-bg-color, #ffffff);
            --tg-theme-text-color: var(--tg-theme-text-color, #222222);
            --tg-theme-hint-color: var(--tg-theme-hint-color, #999999);
            --tg-theme-link-color: var(--tg-theme-link-color, #2481cc);
            --tg-theme-button-color: var(--tg-theme-button-color, #2481cc);
            --tg-theme-button-text-color: var(--tg-theme-button-text-color, #ffffff);
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: var(--tg-theme-bg-color);
            color: var(--tg-theme-text-color);
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
        }
        
        /* Хедер с информацией о пользователе */
        .user-card {
            background: var(--tg-theme-bg-color);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 25px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            border: 1px solid rgba(128,128,128,0.2);
        }
        
        .user-avatar {
            width: 60px;
            height: 60px;
            border-radius: 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            font-weight: bold;
            margin-right: 15px;
        }
        
        .user-info {
            display: flex;
            align-items: center;
        }
        
        .user-details h3 {
            font-size: 18px;
            margin-bottom: 5px;
        }
        
        .user-details p {
            color: var(--tg-theme-hint-color);
            font-size: 14px;
        }
        
        /* Карточки товаров */
        .section-title {
            font-size: 22px;
            margin: 30px 0 20px;
            color: var(--tg-theme-text-color);
            font-weight: 600;
        }
        
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }
        
        .product-card {
            background: var(--tg-theme-bg-color);
            border-radius: 14px;
            padding: 16px;
            border: 1px solid rgba(128,128,128,0.2);
            transition: transform 0.2s, box-shadow 0.2s;
            position: relative;
        }
        
        .product-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.12);
        }
        
        .product-emoji {
            font-size: 40px;
            margin-bottom: 10px;
        }
        
        .product-title {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 8px;
        }
        
        .product-description {
            font-size: 14px;
            color: var(--tg-theme-hint-color);
            margin-bottom: 15px;
            line-height: 1.4;
        }
        
        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }
        
        .product-price {
            font-size: 20px;
            font-weight: 700;
            color: var(--tg-theme-button-color);
        }
        
        .add-to-cart {
            background: var(--tg-theme-button-color);
            color: var(--tg-theme-button-text-color);
            border: none;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: opacity 0.2s;
        }
        
        .add-to-cart:hover {
            opacity: 0.9;
        }
        
        .add-to-cart:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        /* Корзина */
        .cart-panel {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: var(--tg-theme-bg-color);
            border-top: 1px solid rgba(128,128,128,0.2);
            padding: 16px 20px 20px;
            box-shadow: 0 -4px 20px rgba(0,0,0,0.1);
            display: none;
            z-index: 1000;
        }
        
        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .cart-title {
            font-size: 18px;
            font-weight: 600;
        }
        
        .cart-items {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 15px;
        }
        
        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid rgba(128,128,128,0.1);
        }
        
        .cart-item-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .cart-item-emoji {
            font-size: 20px;
        }
        
        .cart-item-title {
            font-size: 14px;
        }
        
        .cart-item-price {
            font-weight: 600;
        }
        
        .cart-item-quantity {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .quantity-btn {
            background: none;
            border: 1px solid rgba(128,128,128,0.3);
            width: 24px;
            height: 24px;
            border-radius: 12px;
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .quantity-btn:hover {
            background: rgba(128,128,128,0.1);
        }
        
        .cart-total {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 15px 0;
            font-size: 18px;
            font-weight: 600;
        }
        
        .cart-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        
        .checkout-btn {
            background: var(--tg-theme-button-color);
            color: var(--tg-theme-button-text-color);
            border: none;
            padding: 14px;
            border-radius: 14px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
        }
        
        .clear-cart-btn {
            background: transparent;
            border: 1px solid rgba(255, 71, 87, 0.5);
            color: #ff4757;
            padding: 14px;
            border-radius: 14px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
        }
        
        .clear-cart-btn:hover {
            background: rgba(255, 71, 87, 0.1);
        }
        
        /* Секция с действиями */
        .actions-section {
            background: var(--tg-theme-bg-color);
            border-radius: 16px;
            padding: 20px;
            border: 1px solid rgba(128,128,128,0.2);
            margin: 30px 0;
        }
        
        .action-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
        }
        
        .tg-button {
            background: var(--tg-theme-button-color);
            color: var(--tg-theme-button-text-color);
            border: none;
            padding: 14px;
            border-radius: 14px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: opacity 0.2s;
        }
        
        .tg-button:hover {
            opacity: 0.9;
        }
        
        .tg-button.secondary {
            background: transparent;
            border: 1px solid var(--tg-theme-button-color);
            color: var(--tg-theme-button-color);
        }
        
        /* Статус */
        .status-badge {
            background: rgba(36, 129, 204, 0.1);
            color: var(--tg-theme-button-color);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 14px;
            display: inline-block;
            margin-bottom: 15px;
        }
        
        /* Кнопка закрытия */
        .close-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--tg-theme-bg-color);
            border: 1px solid rgba(128,128,128,0.2);
            width: 40px;
            height: 40px;
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            cursor: pointer;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            z-index: 1000;
        }
        
        .close-btn:hover {
            background: rgba(128,128,128,0.1);
        }
        
        /* Адаптация для темной темы */
        @media (prefers-color-scheme: dark) {
            body {
                background: var(--tg-theme-bg-color);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Кнопка закрытия (будет видна только если надо) -->
        <div class="close-btn" onclick="closeApp()">✕</div>
        
        <!-- Карточка пользователя -->
        <div class="user-card" id="userCard">
            <div class="user-info">
                <div class="user-avatar" id="userAvatar">👤</div>
                <div class="user-details">
                    <h3 id="userName">Загрузка...</h3>
                    <p id="userId">ID: загрузка...</p>
                </div>
            </div>
        </div>
        
        <!-- Статус подключения -->
        <div class="status-badge" id="tgStatus">
            ⚡ Telegram Mini App активен
        </div>
        
        <!-- Товары -->
        <h2 class="section-title">🛍️ Наши товары</h2>
        
        <div class="products-grid" id="productsGrid">
            <!-- Товары будут добавляться через JS -->
        </div>
        
        <!-- Действия -->
        <div class="actions-section">
            <h3 style="margin-bottom: 10px;">⚡ Действия</h3>
            <p style="color: var(--tg-theme-hint-color); margin-bottom: 15px;">Взаимодействие с Telegram</p>
            
            <div class="action-buttons">
                <button class="tg-button" onclick="showMainButton()">
                    🔘 Показать главную кнопку
                </button>
                <button class="tg-button secondary" onclick="showPopup()">
                    📋 Показать попап
                </button>
                <button class="tg-button" onclick="showAlert()">
                    ⚠️ Показать alert
                </button>
                <button class="tg-button secondary" onclick="showConfirm()">
                    ✅ Показать confirm
                </button>
            </div>
        </div>
    </div>
    
    <!-- Панель корзины -->
    <div class="cart-panel" id="cartPanel">
        <div class="cart-header">
            <span class="cart-title">🛒 Корзина</span>
            <span id="cartItemCount">0 товаров</span>
        </div>
        
        <div class="cart-items" id="cartItems"></div>
        
        <div class="cart-total">
            <span>Итого:</span>
            <span id="cartTotal">0 ₽</span>
        </div>
        
        <div class="cart-actions">
            <button class="clear-cart-btn" onclick="clearCart()">Очистить</button>
            <button class="checkout-btn" onclick="checkout()">Оформить заказ</button>
        </div>
    </div>

    <script>
        // Инициализация Telegram WebApp
        let tg = window.Telegram.WebApp;
        
        // Данные пользователя
        let user = tg.initDataUnsafe?.user;
        let products = [];
        let cart = [];
        
        // Товары (можно заменить на свои)
        const productsData = [
            {
                id: 1,
                emoji: '⭐',
                title: 'Telegram Stars 50',
                description: '50 звезд для поддержки любимых каналов',
                price: 60
            },
            {
                id: 2,
                emoji: '🌟',
                title: 'Telegram Stars 250',
                description: '250 звезд - популярный пакет',
                price: 300
            },
            {
                id: 3,
                emoji: '💎',
                title: 'Telegram Stars 1000',
                description: '1000 звезд для активных пользователей',
                price: 1200
            },
            {
                id: 4,
                emoji: '👑',
                title: 'Telegram Premium',
                description: 'Подписка Premium на 1 месяц',
                price: 299
            },
            {
                id: 5,
                emoji: '📱',
                title: 'Анонимный номер',
                description: 'Виртуальный номер для Telegram',
                price: 500
            },
            {
                id: 6,
                emoji: '🎁',
                title: 'Случайный подарок',
                description: 'Сюрприз от нашего магазина',
                price: 150
            }
        ];
        
        // Загрузка приложения
        function initApp() {
            // Растягиваем на весь экран
            tg.expand();
            
            // Отображаем информацию о пользователе
            if (user) {
                document.getElementById('userName').textContent = user.first_name || 'Пользователь';
                if (user.last_name) {
                    document.getElementById('userName').textContent += ' ' + user.last_name;
                }
                document.getElementById('userId').textContent = `ID: ${user.id}`;
                
                // Аватар с первой буквой имени
                if (user.first_name) {
                    document.getElementById('userAvatar').textContent = user.first_name[0].toUpperCase();
                }
            } else {
                // Если нет данных (тестовый режим)
                document.getElementById('userName').textContent = 'Тестовый пользователь';
                document.getElementById('userId').textContent = 'ID: 123456789';
            }
            
            // Загружаем товары
            loadProducts();
            
            // Настраиваем главную кнопку
            tg.MainButton.setText('ОТКРЫТЬ КОРЗИНУ');
            tg.MainButton.onClick(function() {
                toggleCart();
            });
        }
        
        // Загрузка товаров в сетку
        function loadProducts() {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';
            
            productsData.forEach(product => {
                const card = document.createElement('div');
                card.className = 'product-card';
                card.innerHTML = `
                    <div class="product-emoji">${product.emoji}</div>
                    <div class="product-title">${product.title}</div>
                    <div class="product-description">${product.description}</div>
                    <div class="product-footer">
                        <span class="product-price">${product.price} ₽</span>
                        <button class="add-to-cart" onclick="addToCart(${product.id})" id="btn-${product.id}">
                            В корзину
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }
        
        // Добавление в корзину
        function addToCart(productId) {
            const product = productsData.find(p => p.id === productId);
            if (!product) return;
            
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    ...product,
                    quantity: 1
                });
            }
            
            // Анимация кнопки
            const btn = document.getElementById(`btn-${productId}`);
            btn.textContent = '✓ Добавлено';
            btn.disabled = true;
            setTimeout(() => {
                btn.textContent = 'В корзину';
                btn.disabled = false;
            }, 1000);
            
            updateCart();
            showCartNotification();
        }
        
        // Показать уведомление о корзине
        function showCartNotification() {
            if (cart.length > 0) {
                document.getElementById('cartPanel').style.display = 'block';
                tg.MainButton.setText(`КОРЗИНА (${cart.reduce((sum, item) => sum + item.quantity, 0)})`);
                tg.MainButton.show();
            }
        }
        
        // Обновление корзины
        function updateCart() {
            const cartItemsDiv = document.getElementById('cartItems');
            const cartTotalSpan = document.getElementById('cartTotal');
            const cartItemCount = document.getElementById('cartItemCount');
            
            if (cart.length === 0) {
                cartItemsDiv.innerHTML = '<p style="text-align: center; color: var(--tg-theme-hint-color); padding: 20px;">Корзина пуста</p>';
                cartTotalSpan.textContent = '0 ₽';
                cartItemCount.textContent = '0 товаров';
                document.getElementById('cartPanel').style.display = 'none';
                tg.MainButton.hide();
                return;
            }
            
            let itemsHtml = '';
            let total = 0;
            let totalItems = 0;
            
            cart.forEach(item => {
                total += item.price * item.quantity;
                totalItems += item.quantity;
                
                itemsHtml += `
                    <div class="cart-item">
                        <div class="cart-item-info">
                            <span class="cart-item-emoji">${item.emoji}</span>
                            <span class="cart-item-title">${item.title}</span>
                        </div>
                        <div class="cart-item-quantity">
                            <button class="quantity-btn" onclick="changeQuantity(${item.id}, -1)">-</button>
                            <span>${item.quantity}</span>
                            <button class="quantity-btn" onclick="changeQuantity(${item.id}, 1)">+</button>
                        </div>
                        <span class="cart-item-price">${item.price * item.quantity} ₽</span>
                    </div>
                `;
            });
            
            cartItemsDiv.innerHTML = itemsHtml;
            cartTotalSpan.textContent = `${total} ₽`;
            cartItemCount.textContent = `${totalItems} ${getItemWord(totalItems)}`;
            
            // Обновляем кнопку
            tg.MainButton.setText(`КОРЗИНА (${totalItems})`);
        }
        
        // Изменение количества
        function changeQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += delta;
                if (item.quantity <= 0) {
                    cart = cart.filter(i => i.id !== productId);
                }
                updateCart();
            }
        }
        
        // Очистка корзины
        function clearCart() {
            cart = [];
            updateCart();
        }
        
        // Оформление заказа
        function checkout() {
            if (cart.length === 0) {
                tg.showAlert('Корзина пуста!');
                return;
            }
            
            let total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            let itemsList = cart.map(item => `${item.emoji} ${item.title} x${item.quantity} = ${item.price * item.quantity}₽`).join('\n');
            
            let message = `🛍️ НОВЫЙ ЗАКАЗ\n\n${itemsList}\n\n💰 ИТОГО: ${total}₽`;
            
            if (user) {
                message += `\n\n👤 Покупатель: ${user.first_name || ''} ${user.last_name || ''}\n🆔 ID: ${user.id}`;
            }
            
            // Отправляем данные в бота
            tg.sendData(JSON.stringify({
                action: 'new_order',
                items: cart,
                total: total,
                user_id: user?.id,
                user_name: user?.first_name
            }));
            
            // Показываем подтверждение
            tg.showAlert(`Заказ отправлен!\nСумма: ${total}₽`);
            
            // Очищаем корзину
            clearCart();
        }
        
        // Склонение слова "товар"
        function getItemWord(count) {
            if (count % 10 === 1 && count % 100 !== 11) return 'товар';
            if ([2,3,4].includes(count % 10) && ![12,13,14].includes(count % 100)) return 'товара';
            return 'товаров';
        }
        
        // Показать/скрыть корзину
        function toggleCart() {
            const cartPanel = document.getElementById('cartPanel');
            if (cartPanel.style.display === 'none' || cartPanel.style.display === '') {
                cartPanel.style.display = 'block';
            } else {
                cartPanel.style.display = 'none';
            }
        }
        
        // Закрыть приложение
        function closeApp() {
            tg.close();
        }
        
        // Показать главную кнопку (демонстрация)
        function showMainButton() {
            tg.MainButton.setText('ГЛАВНАЯ КНОПКА');
            tg.MainButton.show();
            tg.MainButton.onClick(function() {
                tg.showAlert('Кнопка нажата!');
            });
        }
        
        // Показать попап
        function showPopup() {
            tg.showPopup({
                title: 'Заголовок',
                message: 'Это попап окно в Telegram',
                buttons: [
                    {id: 'ok', type: 'default', text: 'ОК'},
                    {id: 'cancel', type: 'destructive', text: 'Отмена'}
                ]
            }, function(buttonId) {
                tg.showAlert(`Нажата кнопка: ${buttonId}`);
            });
        }
        
        // Показать alert
        function showAlert() {
            tg.showAlert('Это alert сообщение!');
        }
        
        // Показать confirm
        function showConfirm() {
            tg.showConfirm('Вы уверены?', function(confirmed) {
                if (confirmed) {
                    tg.showAlert('Подтверждено!');
                } else {
                    tg.showAlert('Отменено');
                }
            });
        }
        
        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
