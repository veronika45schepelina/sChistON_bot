<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ЧистON</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&family=Open+Sans:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4CAF50;
            --primary-light: #81C784;
            --primary-dark: #388E3C;
            --secondary: #FF9800;
            --background: #F5F5F5;
            --surface: #FFFFFF;
            --error: #F44336;
            --text-primary: #212121;
            --text-secondary: #757575;
            --divider: #BDBDBD;
            --shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
            --radius: 12px;
            --radius-small: 8px;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Open Sans', sans-serif;
        }
        
        body {
            background-color: var(--background);
            color: var(--text-primary);
            padding: 16px;
            max-width: 100%;
            overflow-x: hidden;
        }
        
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Montserrat', sans-serif;
            font-weight: 600;
        }
        
        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }
        
        .header-title {
            font-size: 24px;
            font-weight: 700;
            color: var(--primary-dark);
        }
        
        .header-subtitle {
            font-size: 14px;
            color: var(--text-secondary);
            margin-top: 4px;
        }
        
        /* Cards */
        .card {
            background-color: var(--surface);
            border-radius: var(--radius);
            padding: 16px;
            margin-bottom: 16px;
            box-shadow: var(--shadow);
        }
        
        .card-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .card-title .icon {
            color: var(--primary);
        }
        
        /* Progress */
        .progress-container {
            width: 100%;
            margin: 16px 0;
        }
        
        .progress-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
        }
        
        .progress-bar {
            height: 8px;
            background-color: #E0E0E0;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary-light), var(--primary));
            border-radius: 4px;
            width: 64%;
        }
        
        /* Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            text-align: center;
            margin: 16px 0;
        }
        
        .stat-item {
            background-color: rgba(76, 175, 80, 0.1);
            border-radius: var(--radius-small);
            padding: 12px;
        }
        
        .stat-value {
            font-size: 20px;
            font-weight: 700;
            color: var(--primary-dark);
        }
        
        .stat-label {
            font-size: 12px;
            color: var(--text-secondary);
            margin-top: 4px;
        }
        
        /* Tasks */
        .task-item {
            display: flex;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .task-item:last-child {
            border-bottom: none;
        }
        
        .task-checkbox {
            width: 24px;
            height: 24px;
            border: 2px solid var(--divider);
            border-radius: 6px;
            margin-right: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .task-checkbox.checked {
            background-color: var(--primary);
            border-color: var(--primary);
            color: white;
        }
        
        .task-content {
            flex: 1;
        }
        
        .task-title {
            font-weight: 500;
        }
        
        .task-subtitle {
            font-size: 12px;
            color: var(--text-secondary);
            margin-top: 2px;
        }
        
        /* Buttons */
        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: var(--radius-small);
            padding: 12px 16px;
            font-size: 16px;
            font-weight: 500;
            width: 100%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.2s;
        }
        
        .btn:hover {
            background-color: var(--primary-dark);
        }
        
        .btn-outline {
            background-color: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
        }
        
        .btn-outline:hover {
            background-color: rgba(76, 175, 80, 0.1);
        }
        
        .btn-secondary {
            background-color: var(--secondary);
        }
        
        .btn-secondary:hover {
            background-color: #F57C00;
        }
        
        /* Badges */
        .badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: 500;
            margin-left: 8px;
        }
        
        .badge-easy {
            background-color: #E8F5E9;
            color: var(--primary-dark);
        }
        
        .badge-medium {
            background-color: #FFF8E1;
            color: #FF8F00;
        }
        
        .badge-hard {
            background-color: #FFEBEE;
            color: var(--error);
        }
        
        /* Tabs */
        .tabs {
            display: flex;
            border-bottom: 1px solid var(--divider);
            margin-bottom: 16px;
        }
        
        .tab {
            padding: 8px 16px;
            font-weight: 500;
            color: var(--text-secondary);
            border-bottom: 2px solid transparent;
            cursor: pointer;
        }
        
        .tab.active {
            color: var(--primary);
            border-bottom-color: var(--primary);
        }
        
        /* Settings */
        .settings-item {
            padding: 16px 0;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .settings-item:last-child {
            border-bottom: none;
        }
        
        .settings-label {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .settings-icon {
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary);
        }
        
        /* Balance */
        .balance-amount {
            font-size: 32px;
            font-weight: 700;
            text-align: center;
            margin: 24px 0;
            color: var(--primary-dark);
        }
        
        .balance-rate {
            text-align: center;
            color: var(--text-secondary);
            margin-bottom: 24px;
        }
        
        .history-item {
            padding: 12px 0;
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
            display: flex;
            justify-content: space-between;
        }
        
        .history-item:last-child {
            border-bottom: none;
        }
        
        .history-amount {
            color: var(--primary);
            font-weight: 500;
        }
        
        .history-date {
            color: var(--text-secondary);
            font-size: 12px;
        }
        
        /* Bottom Navigation */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: var(--surface);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.08);
            z-index: 100;
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            color: var(--text-secondary);
        }
        
        .nav-icon {
            font-size: 24px;
        }
        
        .nav-text {
            font-size: 12px;
            font-family: 'Montserrat', sans-serif;
        }
        
        .nav-active {
            color: var(--primary);
        }
        
        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .fade-in {
            animation: fadeIn 0.3s ease-out;
        }
        
        /* Utility */
        .mt-8 { margin-top: 8px; }
        .mt-16 { margin-top: 16px; }
        .mt-24 { margin-top: 24px; }
        .mb-8 { margin-bottom: 8px; }
        .mb-16 { margin-bottom: 16px; }
        .mb-24 { margin-bottom: 24px; }
        .text-center { text-align: center; }
    </style>
</head>
<body>
    <!-- Главный экран -->
    <div id="main-screen">
        <div class="header">
            <div>
                <h1 class="header-title">Привет, Алексей!</h1>
                <div class="header-subtitle">Уровень 5 • 17 заданий выполнено</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <div class="progress-container">
                <div class="progress-header">
                    <span>1606 баллов</span>
                    <span>12 место</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 64%"></div>
                </div>
            </div>
            
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-value">1606</div>
                    <div class="stat-label">Баллов</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value">17</div>
                    <div class="stat-label">Заданий</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value">15</div>
                    <div class="stat-label">января</div>
                </div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">📝</span> Активности</h3>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">Поиск заданий</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox checked">✓</div>
                <div class="task-content">
                    <div class="task-title">Фотоотчет</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">Мои финансы</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">Рейтинг</div>
                    <div class="task-subtitle">Место: 12</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">Активные задания</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox checked">✓</div>
                <div class="task-content">
                    <div class="task-title">Настройки</div>
                </div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🌟</span> Рекомендуемые задания</h3>
            <button class="btn mt-16" onclick="openTasks()">
                Найти задания
            </button>
        </div>
    </div>
    
    <!-- Экран настроек -->
    <div id="settings-screen" style="display: none;">
        <div class="header">
            <h1 class="header-title">Настройки</h1>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🔔</span> Напоминания</h3>
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">📩</div>
                    <div>Напоминания о принятых заданиях</div>
                </div>
                <div>→</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">✅</div>
                    <div>Уведомления о проверке заданий</div>
                </div>
                <div>→</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">🏆</div>
                    <div>Уведомления о полученных баллах</div>
                </div>
                <div>→</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🌐</span> Приложение</h3>
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">🗣️</div>
                    <div>Язык</div>
                </div>
                <div>Русский →</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">❓</div>
                    <div>Помощь</div>
                </div>
                <div>→</div>
            </div>
            
            <div class="settings-item">
                <div class="settings-label">
                    <div class="settings-icon">ℹ️</div>
                    <div>О приложении</div>
                </div>
                <div>Версия 1.0.0 →</div>
            </div>
        </div>
        
        <button class="btn btn-outline mt-16" style="color: var(--error); border-color: var(--error);">
            Выйти из аккаунта
        </button>
    </div>
    
    <!-- Экран категорий -->
    <div id="category-screen" style="display: none;">
        <div class="header">
            <h1 class="header-title">Категория</h1>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🗂️</span> Мусор</h3>
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Переработка</div>
                </div>
                <div>→</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Озеленение</div>
                </div>
                <div>→</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">⚙️</span> Сложность</h3>
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Легко</div>
                </div>
                <div>→</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Средне</div>
                </div>
                <div>→</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Сложно</div>
                </div>
                <div>→</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">📊</span> Результаты</h3>
            <div class="text-center mb-16">5 заданий</div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Очистка парка Горького</div>
                    <div class="task-subtitle">Сбор мусора в центральной части парка. Необходимо собрать не менее 3 мешков.</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">Парк Горького, Москва</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox"></div>
                <div class="task-content">
                    <div class="task-title">30.05.2025</div>
                </div>
            </div>
            
            <div class="mt-16">
                <span class="badge badge-easy">Легко</span>
                <span style="font-weight: 500;">150 баллов</span>
            </div>
            
            <button class="btn mt-16">
                Принять задание
            </button>
        </div>
    </div>
    
    <!-- Экран профиля -->
    <div id="profile-screen" style="display: none;">
        <div class="header">
            <h1 class="header-title">Алексей Волонтеров</h1>
            <div class="header-subtitle">Уровень 5</div>
        </div>
        
        <div class="card fade-in">
            <div class="progress-container">
                <div class="progress-header">
                    <span>1606 баллов</span>
                    <span>2500 до следующего уровня</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 64%"></div>
                </div>
            </div>
            
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-value">1606</div>
                    <div class="stat-label">Баллов</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value">17</div>
                    <div class="stat-label">Заданий</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value">15</div>
                    <div class="stat-label">января</div>
                </div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🏆</span> Ваше место в рейтинге</h3>
            <div class="text-center mt-8 mb-8" style="font-size: 24px; font-weight: 700;">12 место</div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">⏱️</span> Последняя активность</h3>
            <div class="text-center mt-8 mb-16" style="color: var(--text-secondary);">
                У вас пока нет выполненных заданий
            </div>
            
            <button class="btn" onclick="openTasks()">
                Найти новые задания
            </button>
        </div>
    </div>
    
    <!-- Экран карты -->
    <div id="map-screen" style="display: none;">
        <div class="header">
            <h1 class="header-title">Карта заданий</h1>
            <div class="header-subtitle">Здесь будет интерактивная карта с заданиями</div>
        </div>
        
        <div class="tabs">
            <div class="tab active">Все</div>
            <div class="tab">Мусор</div>
            <div class="tab">Переработка</div>
            <div class="tab">Озеленение</div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">📌</span> Все задания</h3>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Очистка парка Горького</div>
                    <div class="task-subtitle">© Парк Горького</div>
                </div>
                <div style="font-weight: 500; color: var(--primary);">150 баллов</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Сортировка вторсырья</div>
                    <div class="task-subtitle">© Пункт приема вторсырья</div>
                </div>
                <div style="font-weight: 500; color: var(--primary);">200 баллов</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Посадка деревьев</div>
                    <div class="task-subtitle">© Сквер на Тверской улице</div>
                </div>
                <div style="font-weight: 500; color: var(--primary);">300 баллов</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Очистка берега реки</div>
                    <div class="task-subtitle">© Набережная Москвы-реки</div>
                </div>
                <div style="font-weight: 500; color: var(--primary);">250 баллов</div>
            </div>
            
            <div class="task-item">
                <div class="task-content">
                    <div class="task-title">Эко-лекция для школьников</div>
                    <div class="task-subtitle">© Школа №123</div>
                </div>
                <div style="font-weight: 500; color: var(--primary);">180 баллов</div>
            </div>
        </div>
    </div>
    
    <!-- Экран баланса -->
    <div id="balance-screen" style="display: none;">
        <div class="header">
            <h1 class="header-title">Баланс баллов</h1>
        </div>
        
        <div class="card fade-in">
            <div class="balance-amount">1606</div>
            <div class="balance-rate">1 балл = 1 рубль</div>
            
            <button class="btn btn-secondary">
                Вывести средства
            </button>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">🕒</span> История операций</h3>
            
            <div class="history-item">
                <div>
                    <div>Очистка парка Горького</div>
                    <div class="history-date">20.05.2025</div>
                </div>
                <div class="history-amount">+150</div>
            </div>
            
            <div class="history-item">
                <div>
                    <div>Сортировка вторсырья</div>
                    <div class="history-date">15.05.2025</div>
                </div>
                <div class="history-amount">+200</div>
            </div>
        </div>
        
        <div class="card fade-in">
            <h3 class="card-title"><span class="icon">❓</span> Как получить баллы?</h3>
            
            <div class="task-item">
                <div class="task-checkbox">1</div>
                <div class="task-content">
                    <div class="task-title">Выполняйте эко-задания в приложении</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox">2</div>
                <div class="task-content">
                    <div class="task-title">Делайте фотоотчеты о проделанной работе</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox">3</div>
                <div class="task-content">
                    <div class="task-title">Получайте баллы после проверки модератором</div>
                </div>
            </div>
            
            <div class="task-item">
                <div class="task-checkbox">4</div>
                <div class="task-content">
                    <div class="task-title">Выводите баллы на карту (1 балл = 1 рубль)</div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Нижнее меню -->
    <div class="bottom-nav">
        <div class="nav-item nav-active" onclick="showScreen('main-screen')">
            <div class="nav-icon">🏠</div>
            <div class="nav-text">Главная</div>
        </div>
        <div class="nav-item" onclick="showScreen('map-screen')">
            <div class="nav-icon">🗺️</div>
            <div class="nav-text">Карта</div>
        </div>
        <div class="nav-item" onclick="showScreen('profile-screen')">
            <div class="nav-icon">👤</div>
            <div class="nav-text">Профиль</div>
        </div>
    </div>
    
    <script>
        // Инициализация Telegram WebApp
        const tg = window.Telegram.WebApp;
        tg.expand();
        
        // Показать экран
        function showScreen(screenId) {
            document.querySelectorAll('[id$="-screen"]').forEach(screen => {
                screen.style.display = 'none';
            });
            document.getElementById(screenId).style.display = 'block';
            
            // Обновить активную вкладку в нижнем меню
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('nav-active');
            });
            
            if (screenId === 'main-screen') document.querySelector('.nav-item:nth-child(1)').classList.add('nav-active');
            if (screenId === 'map-screen') document.querySelector('.nav-item:nth-child(2)').classList.add('nav-active');
            if (screenId === 'profile-screen') document.querySelector('.nav-item:nth-child(3)').classList.add('nav-active');
        }
        
        // Функции для обработки нажатий
        function openSettings() {
            showScreen('settings-screen');
        }
        
        function openCategory() {
            showScreen('category-screen');
        }
        
        function openBalance() {
            showScreen('balance-screen');
        }
        
        function openTasks() {
            showScreen('map-screen');
        }
        
        // Обработка вкладок
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', function() {
                document.querySelectorAll('.tab').forEach(t => {
                    t.classList.remove('active');
                });
                this.classList.add('active');
            });
        });
    </script>
</body>
</html>
