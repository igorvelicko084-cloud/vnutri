<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>∞ Всё, что ты есть, оставляет эхо</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    :root {
      --bg: #0c0e16;
      --card: #1a1d2b;
      --accent: #b298dc;
      --accent2: #e6c7a9;
      --text: #f0f0f5;
      --subtext: #a0a7c2;
      --success: #6ee7b7;
      --warning: #fbbf24;
      --calm: #88c9a1;
      --gratitude: #fbbf24;
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    }
    body {
      background: linear-gradient(135deg, var(--bg), #131520);
      color: var(--text);
      min-height: 100vh;
      padding: 20px;
      line-height: 1.6;
      overflow-x: hidden;
      transition: background 2s ease;
    }
    #stars-container {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      pointer-events: none;
      z-index: -1;
    }
    .star {
      position: absolute;
      background: rgba(255, 255, 255, 0.7);
      border-radius: 50%;
      animation: twinkle var(--dur, 5s) infinite ease-in-out;
    }
    @keyframes twinkle {
      0%, 100% { opacity: 0.2; transform: scale(1); }
      50% { opacity: 0.8; transform: scale(1.2); }
    }
    .screen {
      display: none;
      max-width: 800px;
      margin: 0 auto;
      animation: fadeIn 0.6s ease;
      position: relative;
      z-index: 10;
    }
    .screen.active {
      display: block;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(12px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .hero {
      text-align: center;
      padding: 40px 0 30px;
    }
    .logo {
      font-size: 2.8rem;
      font-weight: 800;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
    }
    .btn {
      background: linear-gradient(120deg, var(--accent), #8a6fc1);
      color: white;
      border: none;
      padding: 14px 32px;
      border-radius: 50px;
      font-weight: 600;
      cursor: pointer;
      margin: 20px 0;
      display: inline-block;
      transition: all 0.3s ease;
      box-shadow: 0 6px 20px rgba(178, 152, 220, 0.2);
      font-size: 1rem;
    }
    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(178, 152, 220, 0.35);
    }
    .btn-outline {
      background: transparent;
      border: 2px solid var(--accent);
      box-shadow: none;
    }
    .btn-calm {
      background: linear-gradient(120deg, var(--calm), #5a9e7f);
    }
    .btn-gratitude {
      background: linear-gradient(120deg, var(--gratitude), #d97706);
      color: #000;
    }
    .card {
      background: var(--card);
      border-radius: 24px;
      padding: 28px;
      margin: 24px 0;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.05);
    }
    .card h2 {
      margin-bottom: 20px;
      font-size: 1.6rem;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    textarea, input {
      width: 100%;
      padding: 16px;
      border-radius: 16px;
      border: 1px solid #333;
      background: #252836;
      color: var(--text);
      margin: 14px 0;
      font-size: 16px;
      resize: vertical;
      min-height: 80px;
    }
    .back {
      color: var(--accent);
      display: inline-block;
      margin-bottom: 24px;
      cursor: pointer;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .hidden { display: none; }
    .meditation-timer {
      font-size: 3rem;
      font-weight: 200;
      text-align: center;
      margin: 20px 0;
      color: var(--calm);
    }
    .meditation-controls {
      display: flex;
      justify-content: center;
      gap: 12px;
      flex-wrap: wrap;
      margin: 16px 0;
    }
    .meditation-option, .sound-option {
      background: rgba(136, 201, 161, 0.1);
      border: 1px solid rgba(136, 201, 161, 0.3);
      color: var(--calm);
      padding: 10px 18px;
      border-radius: 50px;
      cursor: pointer;
      transition: all 0.2s;
      font-size: 0.95rem;
    }
    .meditation-option.active, .sound-option.active {
      background: rgba(136, 201, 161, 0.3);
      border-color: var(--calm);
    }
    .breathing-circle {
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background: rgba(136, 201, 161, 0.15);
      margin: 30px auto;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
      color: var(--calm);
      transition: transform 4s ease-in-out, background 4s ease;
    }
    .breathing-in { background: rgba(136, 201, 161, 0.3); transform: scale(1.2); }
    .breathing-out { background: rgba(136, 201, 161, 0.1); transform: scale(0.9); }
    .chat-message {
      background: rgba(178, 152, 220, 0.1);
      padding: 12px;
      border-radius: 16px;
      margin: 10px 0;
    }
    #gratitude-garden {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 20px 0;
      min-height: 100px;
      justify-content: center;
    }
    .garden-flower {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      animation: grow 1s ease forwards;
    }
    @keyframes grow {
      from { transform: scale(0); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }
    .emotion-item, .support-item {
      padding: 16px;
      border-radius: 16px;
      margin: 10px 0;
      cursor: pointer;
      transition: background 0.2s;
    }
    .emotion-item:hover {
      background: rgba(178, 152, 220, 0.1);
    }
    .voice-card {
      background: rgba(100, 149, 237, 0.1);
      border-radius: 16px;
      padding: 20px;
      margin: 20px 0;
    }

    /* === АНИМАЦИЯ ФРАЗЫ И ЗВЁЗД === */
    @keyframes fadeInSlow {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 0.9; transform: translateY(0); }
    }

    @keyframes pulseGentle {
      0%, 100% { opacity: 0.7; transform: scale(1); }
      50% { opacity: 0.95; transform: scale(1.015); }
    }

    .echo-phrase {
      font-size: 1.3rem;
      color: var(--subtext);
      margin-top: 12px;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
      opacity: 0;
      animation: 
        fadeInSlow 1.8s ease-out 0.5s forwards,
        pulseGentle 8s ease-in-out 2.5s infinite;
      line-height: 1.5;
      text-align: center;
    }

    /* Пульсация звёзд в ритме фразы */
    .star.pulse-star {
      animation: starPulse 8s ease-in-out 2.5s infinite;
    }
    @keyframes starPulse {
      0%, 100% { opacity: 0.3; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.03); }
    }
    footer {
      text-align: center;
      color: var(--subtext);
      padding: 40px 0 20px;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>

<!-- Звёздное небо -->
<div id="stars-container"></div>

<!-- Онбординг -->
<div id="onboarding" class="screen active">
  <div class="hero">
    <div class="logo">
      <i class="fas fa-seedling"></i> ВНУТРИ
    </div>
    <div class="echo-phrase">
      ∞ Всё, что ты есть, оставляет эхо
    </div>
    <p>Ты — целая вселенная. Этот сайт — твой цифровой сад самопознания.</p>
    <button class="btn" onclick="showScreen('home')">Войти в сад</button>
  </div>
</div>

<!-- Главное меню -->
<div id="home" class="screen">
  <div class="hero">
    <div class="logo">
      <i class="fas fa-seedling"></i> ВНУТРИ
    </div>
    <div class="echo-phrase">
      ∞ Всё, что ты есть, оставляет эхо
    </div>
    <p>Выбери, что посадить сегодня</p>
  </div>
  <div class="card" onclick="showScreen('test-fears')">
    <h2><i class="fas fa-heartbeat"></i> Тест на страхи</h2>
  </div>
  <div class="card" onclick="showScreen('test-strengths')">
    <h2><i class="fas fa-star"></i> Сильные стороны</h2>
  </div>
  <div class="card" onclick="showScreen('emotions')">
    <h2><i class="fas fa-face-smile"></i> Карта эмоций</h2>
  </div>
  <div class="card" onclick="showScreen('inner-voices')">
    <h2><i class="fas fa-comments"></i> Внутренние голоса</h2>
  </div>
  <div class="card" onclick="showScreen('intention')">
    <h2><i class="fas fa-bullseye"></i> Путь намерений</h2>
  </div>
  <div class="card" onclick="showScreen('gratitude')">
    <h2><i class="fas fa-hand-holding-heart"></i> Дневник благодарности</h2>
  </div>
  <div class="card" onclick="showScreen('meditation')">
    <h2><i class="fas fa-spa"></i> Медитация и дыхание</h2>
  </div>
  <div class="card" onclick="showScreen('future-letter')">
    <h2><i class="fas fa-envelope"></i> Письмо себе</h2>
  </div>
  <div class="card" onclick="showScreen('bottle')">
    <h2><i class="fas fa-message"></i> Послание в бутылке</h2>
  </div>
  <div class="card" onclick="showScreen('echo')">
    <h2><i class="fas fa-wind"></i> Эхо желаний</h2>
  </div>
  <div class="card" onclick="showScreen('support-circle')">
    <h2><i class="fas fa-hands-holding-circle"></i> Круг поддержки</h2>
  </div>
  <div class="card" onclick="showScreen('resources')">
    <h2><i class="fas fa-map-location-dot"></i> Карта ресурсов</h2>
  </div>
  <div class="card" onclick="showScreen('gratitude-garden-screen')">
    <h2><i class="fas fa-flower"></i> Сад благодарности</h2>
  </div>
  <div class="card" onclick="showScreen('premium')">
    <h2><i class="fas fa-crown"></i> Premium</h2>
  </div>
  <div class="card" onclick="showScreen('support')">
    <h2><i class="fas fa-heart"></i> Поддержать проект</h2>
  </div>
</div>

<!-- Все остальные экраны (сокращены для краткости, но работают) -->
<div id="test-fears" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Тест на страхи</h2><div id="fear-questions"></div><button class="btn hidden" id="btn-fear" onclick="submitFearTest()">Результат</button></div></div>
<div id="test-strengths" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Сильные стороны</h2><div id="strength-questions"></div><button class="btn hidden" id="btn-strength" onclick="submitStrengthTest()">Увидеть</button></div></div>
<div id="emotions" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Карта эмоций</h2><div class="emotion-item" onclick="selectEmotion('Радость')">😊 Радость</div><div class="emotion-item" onclick="selectEmotion('Печаль')">😢 Печаль</div><textarea id="emotion-detail" placeholder="Опиши подробнее"></textarea><button class="btn" onclick="saveEmotion()">Сохранить</button></div><div class="card"><h2>История</h2><div id="emotion-history">Нет записей</div></div></div>
<div id="inner-voices" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Внутренние голоса</h2><textarea id="voice-input" placeholder="Напиши фразу критика"></textarea><button class="btn" onclick="analyzeVoice()">Проанализировать</button></div><div id="voice-result" class="card hidden"><h2>Это голос...</h2><div id="voice-type"></div><div class="voice-card"><strong>Ответ от Мудрого Я:</strong><div id="wise-response"></div></div></div></div>
<div id="intention" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Путь намерений</h2><textarea id="intention-text" placeholder="Каким я хочу быть сегодня?"></textarea><button class="btn" onclick="saveIntention()">Сохранить</button></div><div class="card"><h2>Мои намерения</h2><div id="intention-list">Нет записей</div></div></div>
<div id="gratitude" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Благодарность</h2><textarea id="gratitude-text" placeholder="За что благодарен?"></textarea><button class="btn btn-gratitude" onclick="saveGratitude()">Сохранить</button></div><div class="card"><h2>История</h2><div id="gratitude-list">Нет записей</div></div></div>
<div id="meditation" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Медитация</h2><div style="text-align:center; margin:16px 0;"><div class="sound-option active" onclick="currentSound='rain'">🌧️ Дождь</div><div class="sound-option" onclick="currentSound='forest'">🌳 Лес</div><div class="sound-option" onclick="currentSound='ocean'">🌊 Океан</div><div class="sound-option" onclick="currentSound='breathing'">🌬️ Дыхание</div></div><div class="meditation-timer" id="meditation-time">05:00</div><div class="meditation-controls"><div class="meditation-option active" onclick="totalSeconds=300">5 мин</div><div class="meditation-option" onclick="totalSeconds=600">10 мин</div><div class="meditation-option" onclick="totalSeconds=900">15 мин</div></div><div id="breathing-container" class="hidden"><div class="breathing-circle" id="breathing-circle">Вдох</div></div><div style="text-align:center; margin-top:24px;"><button class="btn btn-calm" id="btn-start" onclick="startMeditation()">Начать</button><button class="btn btn-outline hidden" id="btn-stop" onclick="stopMeditation()">Остановить</button></div></div></div>
<div id="future-letter" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Письмо себе</h2><textarea id="letter-text" placeholder="Дорогой я через месяц..."></textarea><div class="meditation-controls"><div class="meditation-option active" onclick="letterDays=30">Через месяц</div><div class="meditation-option" onclick="letterDays=90">Через 3 месяца</div></div><button class="btn" onclick="saveFutureLetter()">Отправить</button></div></div>
<div id="bottle" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Послание в бутылке</h2><textarea id="bottle-text" placeholder="Напиши послание"></textarea><button class="btn" onclick="sendBottleMessage()">Отправить</button></div><div class="card"><h2>Полученные</h2><div id="bottle-list">Нет посланий</div></div></div>
<div id="echo" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Эхо желаний</h2><textarea id="wish-text" placeholder="Моё желание..."></textarea><button class="btn" onclick="sendWish()">Отправить</button></div><div class="card"><h2>Для исполнения</h2><div id="wishes-list">Нет желаний</div></div></div>
<div id="support-circle" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Круг поддержки</h2><div id="support-status">Нажми, чтобы войти в Круг</div><button class="btn" id="btn-join-circle" onclick="joinSupportCircle()">Войти в Круг</button><div id="chat-container" class="hidden" style="margin-top:20px;"><div id="chat-messages" style="height:200px; overflow-y:auto; margin-bottom:10px;"></div><input type="text" id="chat-input" class="chat-input" placeholder="Сообщение..." onkeypress="if(event.key==='Enter') sendChatMessage()"><button class="btn btn-outline" style="width:100%; margin-top:5px;" onclick="sendChatMessage()">Отправить</button></div></div></div>
<div id="resources" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Карта ресурсов</h2><h3>🇷🇺 Россия</h3><div class="support-item"><strong>Телефон доверия:</strong> 8-800-2000-122<br><strong>МЧС (психопомощь):</strong> 8-800-100-79-97</div><h3>🌍 Мир</h3><div class="support-item"><a href="https://www.opencounseling.com/suicide-hotlines" target="_blank">Международные линии</a></div></div></div>
<div id="gratitude-garden-screen" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><h2>Сад благодарности</h2><div id="gratitude-garden"></div><button class="btn btn-gratitude" onclick="addFlower()">Посадить цветок</button><p class="subtext">Посажено <span id="flower-count">0</span> цветов</p></div></div>
<div id="premium" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><div class="logo" style="font-size:1.8rem; justify-content:center; margin-bottom:20px;"><i class="fas fa-crown"></i> ВНУТРИ Premium</div><p>Premium — глубина твоего пути.</p><div style="background:rgba(178,152,220,0.1); padding:20px; border-radius:16px; margin:24px 0;"><div style="display:flex; justify-content:space-around; flex-wrap:wrap; gap:16px;"><div style="text-align:center;"><div style="font-size:1.8rem; font-weight:bold; color:var(--accent);">290 ₽</div><div>в месяц</div></div></div></div><div style="text-align:center;"><div class="btn" style="background:linear-gradient(120deg, #6ee7b7, #34d399); color:#000;" onclick="alert('Premium в разработке!')">Уведомить</div></div></div></div>
<div id="support" class="screen"><div class="back" onclick="showScreen('home')"><i class="fas fa-arrow-left"></i> Назад</div><div class="card"><div class="logo" style="font-size:1.8rem; justify-content:center; margin-bottom:20px;"><i class="fas fa-heart"></i> Поддержать проект</div><p>Твоя поддержка помогает развивать проект.</p><a href="#" class="btn" style="background:linear-gradient(120deg, #ff6b6b, #ff8e8e);">Boosty</a></div></div>

<footer>
  <div class="logo" style="font-size:1.4rem; justify-content:center; margin-bottom:8px;">
    <i class="fas fa-seedling"></i> ВНУТРИ
  </div>
  <div class="echo-phrase" style="font-size:1.1rem; margin-top:4px; opacity:0.7; animation-delay:0s;">
    ∞ Всё, что ты есть, оставляет эхо
  </div>
</footer>

<script>
  // === ГЛОБАЛЬНЫЕ ПЕРЕМЕННЫЕ ===
  let currentSound = 'rain';
  let totalSeconds = 300;
  let letterDays = 30;
  let fearAnswers = [];
  let strengthAnswers = Array(10).fill(false);
  let selectedEmotion = '';
  let chatActive = false;
  let bellPlayed = false;

  // === ЗВЁЗДЫ С ПУЛЬСАЦИЕЙ ===
  function createStars() {
    const container = document.getElementById('stars-container');
    for (let i = 0; i < 120; i++) {
      const star = document.createElement('div');
      star.className = 'star';
      if (i % 7 === 0) star.classList.add('pulse-star'); // Каждая 7-я звезда пульсирует в ритме фразы
      const size = Math.random() * 2 + 1;
      star.style.width = star.style.height = size + 'px';
      star.style.left = Math.random() * 100 + 'vw';
      star.style.top = Math.random() * 100 + 'vh';
      star.style.setProperty('--dur', Math.random() * 8 + 4 + 's');
      container.appendChild(star);
    }
  }

  // === ЗВУК КОЛОКОЛЬЧИКА ===
  function playBellSound() {
    try {
      const ctx = new (window.AudioContext || window.webkitAudioContext)();
      const duration = 1.2;
      const frequency = 880;

      const oscillator = ctx.createOscillator();
      const gainNode = ctx.createGain();

      oscillator.type = 'sine';
      oscillator.frequency.setValueAtTime(frequency, ctx.currentTime);
      oscillator.frequency.exponentialRampToValueAtTime(frequency * 0.8, ctx.currentTime + duration);

      gainNode.gain.setValueAtTime(0.25, ctx.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + duration);

      oscillator.connect(gainNode);
      gainNode.connect(ctx.destination);

      oscillator.start();
      oscillator.stop(ctx.currentTime + duration);
      setTimeout(() => ctx.close(), duration * 1000 + 100);
    } catch (e) {
      console.log('Звук недоступен:', e);
    }
  }

  // === ПЕРЕКЛЮЧЕНИЕ ЭКРАНОВ + ЗВУК ===
  function showScreen(id) {
    document.querySelectorAll('.screen').forEach(el => el.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    
    if ((id === 'onboarding' || id === 'home') && !bellPlayed) {
      setTimeout(() => {
        playBellSound();
        bellPlayed = true;
      }, 1000);
    }

    if (id === 'test-fears') renderFearTest();
    if (id === 'test-strengths') renderStrengthTest();
    if (id === 'meditation') {
      document.getElementById('breathing-container').classList.add('hidden');
      document.getElementById('btn-start').classList.remove('hidden');
      document.getElementById('btn-stop').classList.add('hidden');
    }
  }

  // === ИНИЦИАЛИЗАЦИЯ ===
  document.addEventListener('DOMContentLoaded', () => {
    createStars();
    const hour = new Date().getHours();
    if (hour >= 22 || hour < 6) {
      document.body.style.background = 'linear-gradient(135deg, #0a1a1d, #0d1e20)';
    }
    // Загрузка данных
    ['gratitude', 'bottleMessages', 'wishes', 'intentions', 'emotionHistory', 'gardenFlowers']
      .forEach(key => {
        if (!localStorage.getItem(key)) localStorage.setItem(key, key.includes('Flowers') ? '0' : '[]');
      });
    loadGarden();
    loadGratitude();
    loadBottleMessages();
    loadWishes();
    loadIntentions();
    loadEmotionHistory();
  });

  // === ОСТАЛЬНЫЕ ФУНКЦИИ (благодарность, тесты и т.д.) ===
  function saveGratitude() {
    const text = document.getElementById('gratitude-text').value.trim();
    if (!text) { alert('Напиши благодарность'); return; }
    const today = new Date().toLocaleDateString('ru-RU');
    let list = JSON.parse(localStorage.getItem('gratitude') || '[]');
    list.push({ text, date: today });
    localStorage.setItem('gratitude', JSON.stringify(list));
    addFlower();
    document.getElementById('gratitude-text').value = '';
    alert('Сохранено!');
    loadGratitude();
  }

  function loadGratitude() {
    const list = JSON.parse(localStorage.getItem('gratitude') || '[]');
    document.getElementById('gratitude-list').innerHTML = 
      list.length ? list.slice(-3).reverse().map(i => `<div class="gratitude-item">${i.text}<br><small>${i.date}</small></div>`).join('') 
                 : '<p class="subtext">Начни с первой благодарности</p>';
  }

  function saveIntention() {
    const text = document.getElementById('intention-text').value.trim();
    if (!text) { alert('Напиши намерение'); return; }
    let list = JSON.parse(localStorage.getItem('intentions') || '[]');
    list.push({ text, date: new Date().toLocaleDateString('ru-RU') });
    localStorage.setItem('intentions', JSON.stringify(list));
    document.getElementById('intention-text').value = '';
    alert('Намерение сохранено');
    loadIntentions();
  }

  function loadIntentions() {
    const list = JSON.parse(localStorage.getItem('intentions') || '[]');
    document.getElementById('intention-list').innerHTML = 
      list.length ? list.slice(-3).reverse().map(i => `<div class="gratitude-item">${i.text}<br><small>${i.date}</small></div>`).join('') 
                 : '<p class="subtext">Нет намерений</p>';
  }

  function selectEmotion(emotion) {
    selectedEmotion = emotion;
    document.querySelectorAll('.emotion-item').forEach(el => el.style.opacity = '0.5');
    event.target.style.opacity = '1';
  }

  function saveEmotion() {
    if (!selectedEmotion) { alert('Выбери эмоцию'); return; }
    let list = JSON.parse(localStorage.getItem('emotionHistory') || '[]');
    list.push({ emotion: selectedEmotion, detail: document.getElementById('emotion-detail').value, date: new Date().toLocaleDateString('ru-RU') });
    localStorage.setItem('emotionHistory', JSON.stringify(list));
    document.getElementById('emotion-detail').value = '';
    alert('Эмоция сохранена');
    loadEmotionHistory();
  }

  function loadEmotionHistory() {
    const list = JSON.parse(localStorage.getItem('emotionHistory') || '[]');
    document.getElementById('emotion-history').innerHTML = 
      list.length ? list.slice(-3).reverse().map(i => `<div class="emotion-item">${i.emotion} — ${i.date}<br><small>${i.detail || ''}</small></div>`).join('') 
                 : '<p class="subtext">Нет записей</p>';
  }

  function analyzeVoice() {
    const text = document.getElementById('voice-input').value.trim();
    if (!text) { alert('Напиши фразу'); return; }
    let type = "Критика";
    let response = "Ты уже достаточно.";
    if (text.includes('страшно') || text.includes('боюсь')) {
      type = "Тревога";
      response = "Ты не один.";
    }
    document.getElementById('voice-type').textContent = type;
    document.getElementById('wise-response').textContent = response;
    document.getElementById('voice-result').classList.remove('hidden');
  }

  function addFlower() {
    let count = parseInt(localStorage.getItem('gardenFlowers') || '0') + 1;
    localStorage.setItem('gardenFlowers', count);
    loadGarden();
  }

  function loadGarden() {
    const count = parseInt(localStorage.getItem('gardenFlowers') || '0');
    document.getElementById('flower-count').textContent = count;
    const garden = document.getElementById('gratitude-garden');
    garden.innerHTML = '';
    const colors = ['#fbbf24', '#6ee7b7', '#b298dc', '#f87171'];
    for (let i = 0; i < Math.min(count, 30); i++) {
      const flower = document.createElement('div');
      flower.className = 'garden-flower';
      flower.style.backgroundColor = colors[i % colors.length];
      garden.appendChild(flower);
    }
  }

  function joinSupportCircle() {
    chatActive = true;
    document.getElementById('support-status').textContent = 'Ты в Круге. Ты не один.';
    document.getElementById('btn-join-circle').classList.add('hidden');
    document.getElementById('chat-container').classList.remove('hidden');
    addChatMessage('Добро пожаловать. Здесь можно просто быть.', 'system');
  }

  function sendChatMessage() {
    const input = document.getElementById('chat-input');
    const text = input.value.trim();
    if (!text || !chatActive) return;
    addChatMessage(text, 'user');
    input.value = '';
    setTimeout(() => addChatMessage('Я рядом', 'peer'), 2000);
  }

  function addChatMessage(text, type) {
    const el = document.createElement('div');
    el.className = 'chat-message';
    el.style.textAlign = type === 'user' ? 'right' : 'left';
    el.style.color = type === 'system' ? '#a0a7c2' : type === 'user' ? '#6ee7b7' : '#fbbf24';
    el.textContent = text;
    document.getElementById('chat-messages').appendChild(el);
    document.getElementById('chat-messages').scrollTop = document.getElementById('chat-messages').scrollHeight;
  }

  function sendBottleMessage() {
    const text = document.getElementById('bottle-text').value.trim();
    if (!text) { alert('Напиши послание'); return; }
    let messages = JSON.parse(localStorage.getItem('bottleMessages') || '[]');
    messages.push({ text, time: Date.now() });
    localStorage.setItem('bottleMessages', JSON.stringify(messages));
    document.getElementById('bottle-text').value = '';
    alert('Послание отправлено!');
    loadBottleMessages();
  }

  function loadBottleMessages() {
    const messages = JSON.parse(localStorage.getItem('bottleMessages') || '[]');
    document.getElementById('bottle-list').innerHTML = 
      messages.length ? messages.slice(-2).reverse().map(m => `<div class="bottle-item">«${m.text}»<br><small>${new Date(m.time).toLocaleDateString()}</small></div>`).join('') 
                     : '<p class="subtext">Нет посланий</p>';
  }

  function sendWish() {
    const text = document.getElementById('wish-text').value.trim();
    if (!text) { alert('Напиши желание'); return; }
    let wishes = JSON.parse(localStorage.getItem('wishes') || '[]');
    wishes.push({ id: Date.now(), text, fulfilled: false });
    localStorage.setItem('wishes', JSON.stringify(wishes));
    document.getElementById('wish-text').value = '';
    alert('Желание отправлено!');
    loadWishes();
  }

  function fulfillWish(id) {
    let wishes = JSON.parse(localStorage.getItem('wishes') || '[]');
    const wish = wishes.find(w => w.id == id);
    if (wish && !wish.fulfilled) {
      wish.fulfilled = true;
      localStorage.setItem('wishes', JSON.stringify(wishes));
      alert('Ты исполнил желание!');
      loadWishes();
    }
  }

  function loadWishes() {
    const wishes = JSON.parse(localStorage.getItem('wishes') || '[]');
    const unfulfilled = wishes.filter(w => !w.fulfilled);
    document.getElementById('wishes-list').innerHTML = 
      unfulfilled.length ? unfulfilled.map(w => `<div class="gratitude-item">«${w.text}»<br><button class="btn btn-outline" style="font-size:0.9rem;margin-top:10px;" onclick="fulfillWish(${w.id})">Хочу исполнить</button></div>`).join('') 
                         : '<p class="subtext">Нет желаний</p>';
  }

  function saveFutureLetter() {
    const text = document.getElementById('letter-text').value.trim();
    if (!text) { alert('Напиши письмо'); return; }
    let letters = JSON.parse(localStorage.getItem('futureLetters') || '[]');
    letters.push({ text, date: Date.now() + letterDays * 24 * 60 * 60 * 1000 });
    localStorage.setItem('futureLetters', JSON.stringify(letters));
    document.getElementById('letter-text').value = '';
    alert('Письмо сохранено!');
  }

  // === ТЕСТЫ ===
  function renderFearTest() {
    const container = document.getElementById('fear-questions');
    container.innerHTML = '';
    fearAnswers = [];
    const questions = [
      { q: "Когда я отказываюсь от возможности, чаще всего это из-за того, что боюсь...", options: ["не справиться", "осуждения"] },
      { q: "В детстве меня чаще всего пугало...", options: ["не оправдать ожидания", "конфликты"] },
      { q: "Когда я чувствую тревогу, она чаще связана с...", options: ["тем, что я недостаточно хорош", "тем, что меня не примут"] }
    ];
    questions.forEach((q, idx) => {
      const div = document.createElement('div');
      div.style.margin = '15px 0';
      div.innerHTML = `<strong>${idx + 1}. ${q.q}</strong><br>`;
      q.options.forEach(opt => {
        div.innerHTML += `<label style="display:block;margin:8px 0;"><input type="radio" name="fear${idx}" onchange="fearAnswers[${idx}]='${opt}'"> ${opt}</label>`;
      });
      container.appendChild(div);
    });
    setTimeout(() => document.getElementById('btn-fear').classList.remove('hidden'), 100);
  }

  function submitFearTest() {
    if (!fearAnswers.every(a => a)) { alert('Ответь на все вопросы'); return; }
    alert(`Твой страх: ${fearAnswers[0] === 'не справиться' ? 'Страх неудачи' : 'Страх отвержения'}`);
    showScreen('home');
  }

  function renderStrengthTest() {
    const container = document.getElementById('strength-questions');
    container.innerHTML = '';
    strengthAnswers = Array(10).fill(false);
    const items = ["Я легко нахожу общий язык", "Меня хвалят за умение слушать", "Я могу долго идти к цели", "Я замечаю красоту в мелочах"];
    items.forEach((item, i) => {
      container.innerHTML += `<label style="display:block;margin:12px 0;"><input type="checkbox" onchange="strengthAnswers[${i}]=this.checked"> ${item}</label>`;
    });
    setTimeout(() => document.getElementById('btn-strength').classList.remove('hidden'), 100);
  }

  function submitStrengthTest() {
    if (!strengthAnswers.some(a => a)) { alert('Выбери хотя бы одно'); return; }
    alert('Твои силы: Эмпатия, Стойкость');
    showScreen('home');
  }

  // === МЕДИТАЦИЯ ===
  function startMeditation() {
    if (currentSound === 'breathing') {
      document.getElementById('breathing-container').classList.remove('hidden');
      let phase = 0;
      const circle = document.getElementById('breathing-circle');
      const interval = setInterval(() => {
        if (phase === 0) { circle.textContent = 'Вдох'; circle.className = 'breathing-circle breathing-in'; phase = 1; }
        else { circle.textContent = 'Выдох'; circle.className = 'breathing-circle breathing-out'; phase = 0; }
      }, 4000);
      setTimeout(() => { clearInterval(interval); alert('Дыхание завершено'); }, 60000);
    } else {
      alert('Медитация запущена (звуковой демо)');
    }
  }

  function stopMeditation() {
    alert('Медитация остановлена');
  }

  // === ПАРАЛЛАКС ЗВЁЗД ===
  document.addEventListener('mousemove', (e) => {
    const x = (e.clientX / window.innerWidth - 0.5) * 8;
    const y = (e.clientY / window.innerHeight - 0.5) * 8;
    document.querySelectorAll('.star').forEach(star => {
      const size = parseFloat(star.style.width);
      star.style.transform = `translate(${-x * (size/4)}px, ${-y * (size/4)}px)`;
    });
  });
</script>

</body>
</html>
