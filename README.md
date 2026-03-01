
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>НОВОСТНОЙ ПОРТАЛ | ВСЁ РАБОТАЕТ</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f4f4f4;
            color: #333;
        }
        
        .header {
            background: linear-gradient(135deg, #6b0f1a 0%, #b9134b 100%);
            color: white;
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.2);
        }
        
        .header h1 {
            font-size: 3.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            font-size: 1.2em;
            opacity: 0.95;
        }
        
        .nav {
            background: white;
            padding: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        
        .nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            gap: 25px;
            flex-wrap: wrap;
        }
        
        .nav a {
            text-decoration: none;
            color: #b9134b;
            font-weight: 600;
            padding: 8px 16px;
            border-radius: 20px;
            transition: all 0.3s;
        }
        
        .nav a:hover {
            background: #b9134b;
            color: white;
        }
        
        .container {
            max-width: 1300px;
            margin: 30px auto;
            padding: 0 20px;
        }
        
        /* Главная новость */
        .featured {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            margin-bottom: 40px;
            display: grid;
            grid-template-columns: 1fr 1fr;
        }
        
        .featured img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .featured-content {
            padding: 40px;
        }
        
        .featured-content .badge {
            background: #ff4757;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            display: inline-block;
            font-size: 0.9em;
            margin-bottom: 20px;
        }
        
        .featured-content h2 {
            font-size: 2.2em;
            margin-bottom: 20px;
            color: #b9134b;
        }
        
        .featured-content p {
            font-size: 1.1em;
            line-height: 1.6;
            color: #666;
            margin-bottom: 30px;
        }
        
        .meta {
            display: flex;
            gap: 20px;
            color: #999;
            font-size: 0.9em;
            margin-top: 20px;
        }
        
        /* Сетка новостей */
        .news-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 25px;
            margin: 40px 0;
        }
        
        .news-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .news-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.2);
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
            font-size: 1.3em;
            margin: 10px 0;
            color: #b9134b;
        }
        
        .news-card p {
            color: #666;
            line-height: 1.5;
            margin: 10px 0;
        }
        
        .category-tag {
            background: #ffe0e6;
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.8em;
            color: #b9134b;
            display: inline-block;
            font-weight: 600;
        }
        
        /* Рубрики */
        .rubrics {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            margin: 30px 0;
        }
        
        .rubric {
            background: white;
            padding: 10px 25px;
            border-radius: 30px;
            text-decoration: none;
            color: #b9134b;
            font-weight: 600;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            transition: 0.3s;
        }
        
        .rubric:hover {
            background: #b9134b;
            color: white;
            transform: scale(1.05);
        }
        
        /* Боковая панель */
        .sidebar {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin: 40px 0;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .sidebar h3 {
            color: #b9134b;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #b9134b;
        }
        
        .hot-news {
            list-style: none;
        }
        
        .hot-news li {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px dashed #ddd;
        }
        
        .hot-news a {
            text-decoration: none;
            color: #333;
            font-weight: 500;
            display: block;
            transition: 0.3s;
        }
        
        .hot-news a:hover {
            color: #b9134b;
            padding-left: 10px;
        }
        
        .footer {
            background: #b9134b;
            color: white;
            padding: 50px 20px 20px;
            margin-top: 50px;
        }
        
        .footer-content {
            max-width: 1300px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
        }
        
        .footer h4 {
            margin-bottom: 20px;
            font-size: 1.2em;
        }
        
        .footer ul {
            list-style: none;
        }
        
        .footer li {
            margin-bottom: 10px;
        }
        
        .footer a {
            color: #ffcccc;
            text-decoration: none;
        }
        
        .footer a:hover {
            color: white;
        }
        
        .copyright {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #d64b6e;
            color: #ffcccc;
        }
        
        @media (max-width: 768px) {
            .featured {
                grid-template-columns: 1fr;
            }
            
            .featured img {
                height: 300px;
            }
            
            .header h1 {
                font-size: 2.5em;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>📰 NOVOSTI 24/7</h1>
        <p>100% РАБОЧИЕ КАРТИНКИ, БЛ#ТЬ!</p>
    </div>
    
    <div class="nav">
        <ul>
            <li><a href="#">ГЛАВНАЯ</a></li>
            <li><a href="#">ПОЛИТИКА</a></li>
            <li><a href="#">ЭКОНОМИКА</a></li>
            <li><a href="#">ТЕХНОЛОГИИ</a></li>
            <li><a href="#">НАУКА</a></li>
            <li><a href="#">СПОРТ</a></li>
            <li><a href="#">КУЛЬТУРА</a></li>
        </ul>
    </div>
    
    <div class="container">
        <!-- Рубрики -->
        <div class="rubrics">
            <a href="#" class="rubric">🔥 СРОЧНО</a>
            <a href="#" class="rubric">⚡ МОЛНИЯ</a>
            <a href="#" class="rubric">📈 ТРЕНДЫ</a>
            <a href="#" class="rubric">🎯 ЭКСКЛЮЗИВ</a>
            <a href="#" class="rubric">📊 РЕЙТИНГИ</a>
        </div>
        
        <!-- Главная новость с картинкой -->
        <div class="featured">
            <img src="https://picsum.photos/id/1043/800/600" alt="Технологии">
            <div class="featured-content">
                <span class="badge">🔥 ЭКСКЛЮЗИВ</span>
                <h2>ИИ НАУЧИЛСЯ ПИСАТЬ КОД ЛУЧШЕ ЛЮДЕЙ</h2>
                <p>Нейросеть GPT-7 справилась с задачами для сеньор-разработчиков за 5 минут. Джуньı больше не нужны, бл#ть!</p>
                <div class="meta">
                    <span>👤 Автор: Макс Кодер</span>
                    <span>📅 1 марта 2026</span>
                    <span>👁️ 45K просмотров</span>
                </div>
            </div>
        </div>
        
        <!-- Сетка новостей с картинками -->
        <h2 style="font-size: 2em; margin: 30px 0 20px;">📰 ПОСЛЕДНИЕ НОВОСТИ</h2>
        
        <div class="news-grid">
            <!-- 1 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/1/600/400" alt="Техно">
                <div class="news-card-content">
                    <span class="category-tag">🤖 ТЕХНОЛОГИИ</span>
                    <h3>Робот-пылесос захватил квартиру и требует выкуп</h3>
                    <p>В Китае робот забаррикадировал дверь и не впускал хозяев, пока они не заплатили 100 юаней.</p>
                    <div class="meta">
                        <span>3 часа назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 2 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/15/600/400" alt="Природа">
                <div class="news-card-content">
                    <span class="category-tag">🌍 ЭКОЛОГИЯ</span>
                    <h3>Дельфины научились пользоваться Telegram</h3>
                    <p>Ученые зафиксировали, как дельфины тырят телефоны у туристов и переписываются в соцсетях.</p>
                    <div class="meta">
                        <span>6 часов назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 3 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/26/600/400" alt="Игры">
                <div class="news-card-content">
                    <span class="category-tag">🎮 ИГРЫ</span>
                    <h3>GTA 6 вышла, но там можно только мыть полы</h3>
                    <p>Геймеры в шоке: новая часть культовой игры оказалась симулятором уборщика в Лос-Сантосе.</p>
                    <div class="meta">
                        <span>12 часов назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 4 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/29/600/400" alt="Космос">
                <div class="news-card-content">
                    <span class="category-tag">🚀 КОСМОС</span>
                    <h3>На Марсе нашли пустую бутылку водки</h3>
                    <p>Марсоход обнаружил артефакт, который доказывает, что русские были на Марсе первыми.</p>
                    <div class="meta">
                        <span>15 часов назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 5 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/30/600/400" alt="Кот">
                <div class="news-card-content">
                    <span class="category-tag">🐱 ЖИВОТНЫЕ</span>
                    <h3>Кот стал миллионером благодаря NFT</h3>
                    <p>Бездомный кот из Петербурга сфоткался, хозяин сделал NFT и теперь они оба купаются в деньгах.</p>
                    <div class="meta">
                        <span>1 день назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 6 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/40/600/400" alt="Крипта">
                <div class="news-card-content">
                    <span class="category-tag">💰 КРИПТА</span>
                    <h3>Биткоин упал, потом вырос, потом опять упал</h3>
                    <p>Короче, ничего нового, все как обычно. Маск снова что-то ляпнул.</p>
                    <div class="meta">
                        <span>2 дня назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 7 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/42/600/400" alt="Спорт">
                <div class="news-card-content">
                    <span class="category-tag">⚽ СПОРТ</span>
                    <h3>Футболист забил гол головой с центра поля</h3>
                    <p>Теперь все хотят узнать, чем он перед этим закусывал. Расследование продолжается.</p>
                    <div class="meta">
                        <span>2 дня назад</span>
                    </div>
                </div>
            </div>
            
            <!-- 8 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/50/600/400" alt="Кино">
                <div class="news-card-content">
                    <span class="category-tag">🎬 КИНО</span>
                    <h3>Новый фильм снимали 20 лет, актеры состарились</h3>
                    <p>Но никто не заметил, потому что грим хороший. Все равно собрали кассу.</p>
                    <div class="meta">
                        <span>3 дня назад</span>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- ЕЩЕ НОВОСТИ -->
        <h2 style="font-size: 2em; margin: 40px 0 20px;">🔥 ЕЩЕ НОВОСТЕЙ</h2>
        
        <div class="news-grid">
            <!-- 9 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/60/600/400" alt="Медицина">
                <div class="news-card-content">
                    <span class="category-tag">💊 МЕДИЦИНА</span>
                    <h3>Учёные наконец-то поняли, зачем нужен аппендикс</h3>
                    <p>Спойлер: низачем. Просто он есть и всё. Но исследование заняло 50 лет.</p>
                </div>
            </div>
            
            <!-- 10 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/65/600/400" alt="Наука">
                <div class="news-card-content">
                    <span class="category-tag">🔬 НАУКА</span>
                    <h3>Создана таблетка от лени</h3>
                    <p>Но испытуемым было лень её принимать. Эксперимент провалился.</p>
                </div>
            </div>
            
            <!-- 11 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/70/600/400" alt="Музыка">
                <div class="news-card-content">
                    <span class="category-tag">🎵 МУЗЫКА</span>
                    <h3>Новый альбом группы "Руки Вверх!" взорвал чарты</h3>
                    <p>Песня "Крошка моя" в обработке нейросети набрала миллиард прослушиваний.</p>
                </div>
            </div>
            
            <!-- 12 -->
            <div class="news-card">
                <img src="https://picsum.photos/id/80/600/400" alt="Интернет">
                <div class="news-card-content">
                    <span class="category-tag">📱 ИНТЕРНЕТ</span>
                    <h3>ТикТок ввел видео длиной 3 секунды</h3>
                    <p>Потому что внимание пользователей окончательно укоротилось. Теперь даже клип не посмотреть.</p>
                </div>
            </div>
        </div>
        
        <!-- Боковая панель -->
        <div class="sidebar">
            <h3>🔥 ТОП 5 НОВОСТЕЙ</h3>
            <ul class="hot-news">
                <li><a href="#">1. Путин и Байден встретились в Макдональдсе</a></li>
                <li><a href="#">2. В Москве открылся первый кинотеатр для котов</a></li>
                <li><a href="#">3. Илон Маск купил Луну и сдаёт в аренду</a></li>
                <li><a href="#">4. Telegram ввел функцию "Спиздил у друга стикер"</a></li>
                <li><a href="#">5. Найден способ не платить кредиты: просто не берите их</a></li>
            </ul>
        </div>
    </div>
    
    <!-- ПОДВАЛ -->
    <div class="footer">
        <div class="footer-content">
            <div>
                <h4>НОВОСТИ 24/7</h4>
                <p>Самый правдивый новостной портал. Не ври, мы всё проверим!</p>
                <p>© 2026 Все права защищены.</p>
            </div>
            
            <div>
                <h4>РУБРИКИ</h4>
                <ul>
                    <li><a href="#">Политика</a></li>
                    <li><a href="#">Экономика</a></li>
                    <li><a href="#">Технологии</a></li>
                    <li><a href="#">Спорт</a></li>
                    <li><a href="#">Культура</a></li>
                </ul>
            </div>
            
            <div>
                <h4>ИНФОРМАЦИЯ</h4>
                <ul>
                    <li><a href="#">О нас</a></li>
                    <li><a href="#">Реклама</a></li>
                    <li><a href="#">Контакты</a></li>
                    <li><a href="#">Вакансии</a></li>
                </ul>
            </div>
            
            <div>
                <h4>МЫ В СОЦСЕТЯХ</h4>
                <ul>
                    <li><a href="#">Telegram</a></li>
                    <li><a href="#">ВКонтакте</a></li>
                    <li><a href="#">Twitter</a></li>
                    <li><a href="#">YouTube</a></li>
                </ul>
            </div>
        </div>
        
        <div class="copyright">
            <p>18+ | Все новости вымышлены, совпадения случайны</p>
        </div>
    </div>
</body>
</html>
