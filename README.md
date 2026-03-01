<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>НОВОСТИ 24/7 | ВСЯ ХУЙНЯ МИРА</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background: #f0f2f5;
            color: #1a1a1a;
        }
        
        /* ШАПКА */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }
        
        .header h1 {
            font-size: 48px;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        
        .header p {
            font-size: 18px;
            opacity: 0.9;
        }
        
        /* МЕНЮ */
        .nav {
            background: white;
            padding: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
        }
        
        .nav a {
            text-decoration: none;
            color: #333;
            font-weight: 600;
            padding: 5px 10px;
            transition: 0.3s;
        }
        
        .nav a:hover {
            color: #667eea;
            background: #f0f2f5;
            border-radius: 5px;
        }
        
        /* КОНТЕЙНЕР */
        .container {
            max-width: 1200px;
            margin: 30px auto;
            padding: 0 20px;
        }
        
        /* ГЛАВНАЯ НОВОСТЬ */
        .main-news {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-bottom: 30px;
        }
        
        .main-news img {
            width: 100%;
            height: 400px;
            object-fit: cover;
        }
        
        .main-news-content {
            padding: 30px;
        }
        
        .main-news h2 {
            font-size: 32px;
            margin-bottom: 15px;
            color: #1a1a1a;
        }
        
        .main-news p {
            font-size: 18px;
            line-height: 1.6;
            color: #4a4a4a;
        }
        
        .meta {
            color: #888;
            font-size: 14px;
            margin: 15px 0;
            display: flex;
            gap: 20px;
        }
        
        /* СЕТКА НОВОСТЕЙ */
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }
        
        .news-card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }
        
        .news-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }
        
        .news-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }
        
        .news-card-content {
            padding: 20px;
        }
        
        .news-card h3 {
            font-size: 20px;
            margin-bottom: 10px;
            color: #1a1a1a;
        }
        
        .news-card p {
            color: #666;
            line-height: 1.5;
            margin-bottom: 15px;
        }
        
        .read-more {
            color: #667eea;
            text-decoration: none;
            font-weight: 600;
            display: inline-block;
        }
        
        .read-more:hover {
            text-decoration: underline;
        }
        
        /* КАТЕГОРИИ */
        .categories {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 30px 0;
        }
        
        .category {
            background: white;
            padding: 8px 20px;
            border-radius: 25px;
            font-weight: 600;
            color: #333;
            text-decoration: none;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: 0.3s;
        }
        
        .category:hover {
            background: #667eea;
            color: white;
        }
        
        /* САЙДБАР */
        .sidebar {
            background: white;
            border-radius: 12px;
            padding: 25px;
            margin-top: 30px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }
        
        .sidebar h3 {
            font-size: 24px;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #667eea;
        }
        
        .popular-news {
            list-style: none;
        }
        
        .popular-news li {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .popular-news a {
            text-decoration: none;
            color: #333;
            font-weight: 500;
            line-height: 1.4;
        }
        
        .popular-news a:hover {
            color: #667eea;
        }
        
        /* ПОДВАЛ */
        .footer {
            background: #1a1a1a;
            color: white;
            padding: 40px 20px;
            margin-top: 50px;
        }
        
        .footer-content {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }
        
        .footer-section h4 {
            margin-bottom: 20px;
            color: #667eea;
        }
        
        .footer-section ul {
            list-style: none;
        }
        
        .footer-section li {
            margin-bottom: 10px;
        }
        
        .footer-section a {
            color: #aaa;
            text-decoration: none;
        }
        
        .footer-section a:hover {
            color: white;
        }
        
        .copyright {
            text-align: center;
            padding-top: 30px;
            color: #666;
            border-top: 1px solid #333;
            margin-top: 30px;
        }
        
        /* ТЕГИ */
        .tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin: 20px 0;
        }
        
        .tag {
            background: #eef2f7;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 14px;
            color: #555;
        }
        
        /* АДАПТАЦИЯ */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 32px;
            }
            
            .main-news h2 {
                font-size: 24px;
            }
            
            .news-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>НОВОСТИ 24/7</h1>
        <p>ВСЕ САМЫЕ СВЕЖИЕ НОВОСТИ СО ВСЕГО МИРА, БЛ#ТЬ!</p>
    </div>
    
    <div class="nav">
        <ul>
            <li><a href="#">ГЛАВНАЯ</a></li>
            <li><a href="#">ПОЛИТИКА</a></li>
            <li><a href="#">ЭКОНОМИКА</a></li>
            <li><a href="#">ТЕХНОЛОГИИ</a></li>
            <li><a href="#">СПОРТ</a></li>
            <li><a href="#">КУЛЬТУРА</a></li>
            <li><a href="#">НАУКА</a></li>
            <li><a href="#">ШОУ-БИЗ</a></li>
        </ul>
    </div>
    
    <div class="container">
        <!-- КАТЕГОРИИ -->
        <div class="categories">
            <a href="#" class="category">🔥 ГОРЯЧИЕ</a>
            <a href="#" class="category">⚡ СРОЧНЫЕ</a>
            <a href="#" class="category">📱 ТРЕНДЫ</a>
            <a href="#" class="category">🎯 ЭКСКЛЮЗИВ</a>
            <a href="#" class="category">📊 АНАЛИТИКА</a>
            <a href="#" class="category">🎥 ВИДЕО</a>
        </div>
        
        <!-- ГЛАВНАЯ НОВОСТЬ -->
        <div class="main-news">
            <img src="https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=1200" alt="Главная новость">
            <div class="main-news-content">
                <div class="meta">
                    <span>🔥 СРОЧНО</span>
                    <span>📅 1 марта 2026</span>
                    <span>👁️ 12.5K просмотров</span>
                </div>
                <h2>ГЛОБАЛЬНЫЙ ТЕХНОЛОГИЧЕСКИЙ САММИТ 2026: ИИ ЗАХВАТЫВАЕТ МИР</h2>
                <p>На проходящем в Дубае саммите лидеры технологической индустрии представили революционные разработки в области искусственного интеллекта. Новые нейросети способны не только генерировать контент, но и полностью автономно управлять сложными системами. Эксперты прогнозируют, что к 2030 году до 40% рабочих процессов будут автоматизированы с помощью ИИ. Особый резонанс вызвало заявление компании Neuralink о первых успешных испытаниях нейроинтерфейса нового поколения, позволяющего управлять техникой силой мысли.</p>
                <div style="margin-top: 20px;">
                    <a href="#" class="read-more">ЧИТАТЬ ДАЛЬШЕ →</a>
                </div>
            </div>
        </div>
        
        <!-- СЕТКА НОВОСТЕЙ -->
        <h2 style="margin: 40px 0 20px; font-size: 28px;">📰 ПОСЛЕДНИЕ НОВОСТИ</h2>
        
        <div class="news-grid">
            <!-- НОВОСТЬ 1 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1529107386315-e1a2ed48a620?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>💻 ТЕХНО</span>
                        <span>2 часа назад</span>
                    </div>
                    <h3>Российские ученые создали квантовый процессор с рекордной производительностью</h3>
                    <p>Новый процессор на 128 кубитах обходит существующие аналоги в 3 раза. Разработка открывает путь к созданию сверхмощных компьютеров нового поколения...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
            
            <!-- НОВОСТЬ 2 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1446776811953-b23d57bd21aa?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>🌍 ПОЛИТИКА</span>
                        <span>5 часов назад</span>
                    </div>
                    <h3>Саммит G20: лидеры договорились о новой системе международных расчетов</h3>
                    <p>20 стран подписали соглашение о создании альтернативной SWIFT системы на основе блокчейна. Новая система начнет работу с 2027 года...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
            
            <!-- НОВОСТЬ 3 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1461896836934-ffe607ba8211?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>⚽ СПОРТ</span>
                        <span>8 часов назад</span>
                    </div>
                    <h3>Чемпионат мира по футболу 2026: неожиданные результаты</h3>
                    <p>Сборная Марокко сенсационно обыграла Бразилию со счетом 3:1 и вышла в полуфинал. Бразильские болельщики требуют отставки тренера...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
            
            <!-- НОВОСТЬ 4 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1504384764586-bb4cdc1707b0?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>🎬 КИНО</span>
                        <span>12 часов назад</span>
                    </div>
                    <h3>"Дюна 3" собрала миллиард за первую неделю проката</h3>
                    <p>Фантастический блокбастер Дени Вильнева установил рекорд кассовых сборов 2026 года. Зрители и критики в восторге от визуальных эффектов...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
            
            <!-- НОВОСТЬ 5 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1581091226033-d5c48150dbaa?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>🔬 НАУКА</span>
                        <span>16 часов назад</span>
                    </div>
                    <h3>NASA объявило о наличии следов жизни на Марсе</h3>
                    <p>Марсоход Perseverance обнаружил органические молекулы в образцах грунта, которые могут указывать на существование бактерий в прошлом...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
            
            <!-- НОВОСТЬ 6 -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=600" alt="Новость">
                <div class="news-card-content">
                    <div class="meta" style="margin: 0 0 10px;">
                        <span>💰 ЭКОНОМИКА</span>
                        <span>1 день назад</span>
                    </div>
                    <h3>Биткоин обновил исторический максимум, превысив $150,000</h3>
                    <p>Криптовалюта продолжает расти на фоне принятия биткоина как официального платежного средства в нескольких странах. Аналитики прогнозируют рост до $200,000...</p>
                    <a href="#" class="read-more">Подробнее</a>
                </div>
            </div>
        </div>
        
        <!-- ТЕГИ -->
        <div class="tags">
            <span class="tag">#ИИ</span>
            <span class="tag">#ТЕХНОЛОГИИ</span>
            <span class="tag">#ПОЛИТИКА</span>
            <span class="tag">#СПОРТ</span>
            <span class="tag">#КРИПТОВАЛЮТА</span>
            <span class="tag">#КОСМОС</span>
            <span class="tag">#НАУКА</span>
            <span class="tag">#КИНО</span>
            <span class="tag">#ЭКОНОМИКА</span>
        </div>
        
        <!-- САЙДБАР -->
        <div class="sidebar">
            <h3>🔥 ПОПУЛЯРНОЕ</h3>
            <ul class="popular-news">
                <li><a href="#">Как искусственный интеллект меняет рынок труда: 10 профессий исчезнут к 2030 году</a></li>
                <li><a href="#">Скандал в правительстве: министр финансов подал в отставку</a></li>
                <li><a href="#">Топ-10 самых богатых людей мира 2026: кто потерял, а кто заработал</a></li>
                <li><a href="#">Новый iPhone 16: характеристики, цена, дата выхода</a></li>
                <li><a href="#">Климатический кризис: рекордная жара в Европе</a></li>
                <li><a href="#">Слив данных миллиона пользователей: крупнейший хакерский взлом года</a></li>
            </ul>
            
            <h3 style="margin-top: 30px;">📅 АРХИВ</h3>
            <ul class="popular-news">
                <li><a href="#">Февраль 2026</a></li>
                <li><a href="#">Январь 2026</a></li>
                <li><a href="#">Декабрь 2025</a></li>
                <li><a href="#">Ноябрь 2025</a></li>
            </ul>
        </div>
        
        <!-- ЕЩЕ НОВОСТИ -->
        <h2 style="margin: 40px 0 20px;">📌 РЕКОМЕНДУЕМ</h2>
        
        <div class="news-grid">
            <!-- ДОПОЛНИТЕЛЬНЫЕ НОВОСТИ -->
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1496449903678-68ddcb189a24?w=600" alt="Новость">
                <div class="news-card-content">
                    <h4>Путешествия: 10 самых дешевых стран для отдыха в 2026</h4>
                    <p>Эксперты составили рейтинг бюджетных направлений...</p>
                </div>
            </div>
            
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?w=600" alt="Новость">
                <div class="news-card-content">
                    <h4>Здоровье: новая диета продлевает жизнь на 15 лет</h4>
                    <p>Ученые из Гарварда подтвердили эффективность...</p>
                </div>
            </div>
            
            <div class="news-card">
                <img src="https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=600" alt="Новость">
                <div class="news-card-content">
                    <h4>Автомобили: электрокары обогнали бензиновые по продажам</h4>
                    <p>В Европе впервые продано больше электромобилей...</p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- ПОДВАЛ -->
    <div class="footer">
        <div class="footer-content">
            <div class="footer-section">
                <h4>НОВОСТИ 24/7</h4>
                <p>Самые свежие и достоверные новости со всего мира. Работаем 24/7, без выходных и перерывов.</p>
            </div>
            
            <div class="footer-section">
                <h4>РАЗДЕЛЫ</h4>
                <ul>
                    <li><a href="#">Политика</a></li>
                    <li><a href="#">Экономика</a></li>
                    <li><a href="#">Технологии</a></li>
                    <li><a href="#">Спорт</a></li>
                    <li><a href="#">Культура</a></li>
                </ul>
            </div>
            
            <div class="footer-section">
                <h4>ИНФО</h4>
                <ul>
                    <li><a href="#">О нас</a></li>
                    <li><a href="#">Реклама</a></li>
                    <li><a href="#">Контакты</a></li>
                    <li><a href="#">Вакансии</a></li>
                </ul>
            </div>
            
            <div class="footer-section">
                <h4>СОЦСЕТИ</h4>
                <ul>
                    <li><a href="#">Telegram</a></li>
                    <li><a href="#">VK</a></li>
                    <li><a href="#">Twitter</a></li>
                    <li><a href="#">YouTube</a></li>
                </ul>
            </div>
        </div>
        
        <div class="copyright">
            © 2026 НОВОСТИ 24/7. Все права защищены. 18+
        </div>
    </div>
</body>
</html>
