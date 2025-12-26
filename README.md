<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Respzona - Official Website</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>

<style>
:root {
    --color-primary: #00d4ff;
    --color-primary-dark: #0099cc;
    --color-secondary: #ff006e;
    --color-tertiary: #8338ec;
    --color-accent: #ffbe0b;
    --color-bg: #050714;
    --color-surface: rgba(26, 31, 58, 0.75);
    --color-surface-light: rgba(37, 45, 74, 0.8);
    --color-text: #e8e8ff;
    --color-text-secondary: #b0b5d3;
    --color-danger: #ff3366;
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }

/* ANIMATED GRADIENT BACKGROUND */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: var(--color-text);
    overflow-x: hidden;
    position: relative;
    min-height: 100vh;
    background: linear-gradient(-45deg, #0a0e27, #240b36, #1a1f3a, #002244);
    background-size: 400% 400%;
    animation: gradientBG 15s ease infinite;
}

@keyframes gradientBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

/* STAR CANVAS */
#star-canvas {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    z-index: -1; pointer-events: none; background: transparent;
}

@keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(0, 212, 255, 0.4); }
    70% { box-shadow: 0 0 0 20px rgba(0, 212, 255, 0); }
    100% { box-shadow: 0 0 0 0 rgba(0, 212, 255, 0); }
}

.content { position: relative; z-index: 10; display: flex; flex-direction: column; }

/* LANGUAGE TOGGLE */
.lang-toggle {
    position: fixed; top: 20px; right: 20px; z-index: 998;
    display: flex; gap: 10px;
}

.lang-btn {
    padding: 10px 15px; background: var(--color-surface);
    border: 2px solid var(--color-primary); border-radius: 8px;
    color: var(--color-text); cursor: pointer; font-weight: 600;
    transition: 0.3s; text-transform: uppercase; font-size: 12px;
    letter-spacing: 1px;
}

.lang-btn.active {
    background: var(--color-primary); color: #000;
    box-shadow: 0 0 20px var(--color-primary);
}

.lang-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 15px rgba(0, 212, 255, 0.5);
}

/* HEADER */
header { padding: 40px 16px; text-align: center; }
.logo-image {
    width: 140px; height: 140px; border-radius: 50%;
    border: 3px solid var(--color-primary); margin: 0 auto 15px;
    background: #000; box-shadow: 0 0 40px var(--color-primary);
    overflow: hidden;
}
.logo-image img { width: 100%; height: 100%; object-fit: cover; }
.title-section h1 {
    font-size: 3.5rem; font-weight: 800; text-transform: uppercase;
    background: linear-gradient(90deg, #00d4ff, #ff006e, #8338ec);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    margin-bottom: 5px; letter-spacing: 2px;
    filter: drop-shadow(0 0 10px rgba(131, 56, 236, 0.5));
}
.title-section p { font-size: 14px; letter-spacing: 4px; color: var(--color-text-secondary); text-transform: uppercase; }

main { max-width: 960px; margin: 0 auto; padding: 20px; }

/* CARDS */
.info-card {
    background: var(--color-surface); backdrop-filter: blur(12px);
    border: 1px solid rgba(0, 212, 255, 0.3); border-radius: 20px;
    padding: 30px; margin-bottom: 30px;
    transform: translateY(30px); opacity: 0;
    box-shadow: 0 10px 30px rgba(0,0,0,0.4);
}
h2 { color: var(--color-primary); font-size: 26px; margin-bottom: 20px; text-transform: uppercase; border-left: 4px solid var(--color-secondary); padding-left: 15px; font-weight: 700; }
p { line-height: 1.7; margin-bottom: 15px; color: #ced4ea; }

/* TRACKS & GALLERY */
.tracks-gallery, .gallery-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-top: 20px; }
.track-card, .gallery-item {
    border-radius: 15px; overflow: hidden; position: relative; aspect-ratio: 1;
    cursor: pointer; transition: 0.3s; border: 2px solid var(--color-primary); background: #000;
}
.track-card:hover, .gallery-item:hover { transform: scale(1.05); z-index: 2; box-shadow: 0 0 25px var(--color-primary); }
.track-card img, .gallery-item img { width: 100%; height: 100%; object-fit: cover; }
.track-info-overlay {
    position: absolute; bottom: 0; left: 0; right: 0;
    background: linear-gradient(to top, rgba(0,0,0,1), transparent);
    padding: 10px; font-size: 11px; text-transform: uppercase; letter-spacing: 1px;
}

/* LEADERS */
.leaders-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
.leader-card {
    background: var(--color-surface-light); border: 2px solid var(--color-primary);
    border-radius: 15px; padding: 25px 20px; text-align: center;
    position: relative; transition: 0.3s; cursor: pointer;
}
.leader-card:hover { transform: translateY(-5px); box-shadow: 0 10px 30px rgba(0, 212, 255, 0.3); background: rgba(37, 45, 74, 1); }
.leader-card.main { border-color: var(--color-secondary); }
.leader-alias { color: var(--color-primary); font-size: 22px; font-weight: 800; display: block; margin-bottom: 5px; text-shadow: 0 0 10px rgba(0, 212, 255, 0.4); }
.leader-desc { font-size: 13px; color: var(--color-text-secondary); margin-top: 10px; line-height: 1.5; }
.tap-hint { font-size: 10px; color: #aaa; margin-top: 10px; text-transform: uppercase; letter-spacing: 1px; opacity: 0.7; }

/* STATS */
.stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 15px; text-align: center; }
.stat-box { background: rgba(0,0,0,0.3); padding: 15px; border-radius: 10px; border: 1px solid var(--color-primary); }
.stat-box h3 { font-size: 22px; color: var(--color-accent); margin-bottom: 5px; }
.stat-box p { margin: 0; font-size: 12px; }

/* SUPPORT & LINKS */
.support-card { border-color: var(--color-danger); }
.support-buttons { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 10px; margin-top: 20px; }
.support-btn {
    display: flex; align-items: center; justify-content: center;
    padding: 15px; background: linear-gradient(45deg, var(--color-danger), #ff5a7a);
    border: none; border-radius: 10px; color: white; text-decoration: none;
    font-weight: bold; cursor: pointer; transition: 0.3s;
}
.support-btn:hover { transform: translateY(-3px); box-shadow: 0 5px 20px rgba(255, 51, 102, 0.4); }

.links-section { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; }
.link-button {
    display: block; padding: 15px; text-align: center;
    background: var(--color-surface-light); border: 1px solid var(--color-primary);
    border-radius: 10px; color: white; text-decoration: none; font-weight: 600;
    transition: 0.3s;
}
.link-button:hover { background: var(--color-primary); color: #000; }

/* CHATBOT */
.chatbot-btn {
    position: fixed; bottom: 30px; right: 30px; z-index: 999;
    border: 3px solid var(--color-primary); border-radius: 50%;
    width: 70px; height: 70px; cursor: pointer;
    background: #000; overflow: hidden; animation: pulse 2s infinite; transition: 0.3s;
}
.chatbot-btn img { width: 100%; height: 100%; object-fit: cover; }
.chatbot-btn:hover { transform: scale(1.1); }
.ai-modal-content {
    position: fixed; bottom: 110px; right: 30px; width: 300px;
    background: #1a1f3a; border: 2px solid var(--color-primary);
    border-radius: 15px; padding: 20px; text-align: center;
    display: none; z-index: 1000; box-shadow: 0 0 20px rgba(0,0,0,0.5);
}

/* MODALS */
.modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 2000; backdrop-filter: blur(8px); overflow-y: auto; }
.modal-content {
    background: #0f1225; margin: 5vh auto; padding: 30px; width: 90%; max-width: 600px;
    border-radius: 20px; border: 2px solid var(--color-primary); position: relative;
    box-shadow: 0 0 50px rgba(0,212,255,0.2); animation: slideUp 0.3s ease;
}
@keyframes slideUp { from { transform: translateY(50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
.close-btn { position: absolute; top: 15px; right: 20px; font-size: 30px; cursor: pointer; color: var(--color-primary); }
.youtube-link { display: block; text-align: center; background: #ff0000; color: white; padding: 15px; border-radius: 8px; text-decoration: none; margin-top: 25px; font-weight: bold; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
.youtube-link:hover { background: #cc0000; box-shadow: 0 0 15px rgba(255,0,0,0.4); }

.card-number-box {
    background: rgba(255,255,255,0.1); padding: 20px;
    border-radius: 10px; border: 1px dashed var(--color-primary);
    text-align: center; font-size: 24px; font-weight: bold; letter-spacing: 2px;
    margin: 20px 0; color: #fff;
}

/* GENERATOR UI */
.generator-ui { margin-top: 20px; display: grid; gap: 10px; }
.gen-input { background: rgba(0,0,0,0.3); border: 1px solid var(--color-primary); color: white; padding: 12px; border-radius: 8px; width: 100%; }
.gen-select { background: #1a1f3a; color: white; border: 1px solid var(--color-primary); padding: 12px; border-radius: 8px; width: 100%; cursor: pointer; }
.gen-btn { width: 100%; background: var(--color-primary); color: #000; padding: 12px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; text-transform: uppercase; }
.gen-btn:hover { background: #fff; box-shadow: 0 0 15px var(--color-primary); }

/* FOOTER */
footer { text-align: center; padding: 40px; margin-top: 40px; border-top: 1px solid rgba(255,255,255,0.1); font-size: 14px; opacity: 0.7; }
.email-link { color: var(--color-primary); text-decoration: none; }

@media (max-width: 600px) {
    .title-section h1 { font-size: 2.2rem; }
    .stats-grid { grid-template-columns: 1fr 1fr; }
    .card-number-box { font-size: 18px; }
    .lang-toggle { top: 80px; right: 20px; }
}
</style>
</head>
<body>

<canvas id="star-canvas"></canvas>

<!-- LANGUAGE TOGGLE -->
<div class="lang-toggle">
    <button class="lang-btn active" onclick="setLanguage('ru')" id="btn-ru">РУ</button>
    <button class="lang-btn" onclick="setLanguage('en')" id="btn-en">EN</button>
</div>

<button class="chatbot-btn" id="chatbotBtn" onclick="toggleAI()">
    <img src="https://user-gen-media-assets.s3.amazonaws.com/seedream_images/dbd745d4-fb00-4faf-98b2-b3c1cefda994.png" alt="RESP AI">
</button>
<div id="aiModal" class="ai-modal-content">
    <h3 style="color:var(--color-primary)">🤖 RESP AI</h3>
    <p id="ai-title">Система в разработке...</p>
    <p id="ai-desc" style="font-size:12px; color:#aaa;">ИИ группы скоро будет доступен.</p>
</div>

<div class="content">
    <header>
        <div class="logo-image gs-reveal">
            <img src="https://agi-prod-file-upload-public-main-use1.s3.amazonaws.com/1b3a7c15-396a-4339-b2df-7a1959999c6a" alt="Respzona Logo">
        </div>
        <div class="title-section gs-reveal">
            <h1>RESPZONA</h1>
            <p>POP / RAP / PHONK / MEME</p>
        </div>
    </header>

    <main>
        <div class="info-card gs-reveal">
            <h2 id="about-title">🎵 О нас</h2>
            <p id="about-text-1">Respzona — музыкальная команда из Уфы и Стерлитамака...</p>
            <p id="about-text-2">Для нас важно, чтобы треки были и про эмоции...</p>
        </div>

        <div class="info-card gs-reveal">
            <h2 id="releases-title">🔥 Наши релизы</h2>
            <p id="releases-hint" style="font-size:13px; color:var(--color-text-secondary);">Нажми на обложку, чтобы узнать подробности.</p>
            <div class="tracks-gallery">
                <div class="track-card" onclick="openModal('huday')">
                    <img src="5343980051684330937.jpg" alt="HUDAY">
                    <div class="track-info-overlay"><strong>HUDAY</strong></div>
                </div>
                <div class="track-card" onclick="openModal('huday-phonk')">
                    <img src="5343980051684330938.jpg" alt="PHONK">
                    <div class="track-info-overlay"><strong>HUDAY PHONK</strong></div>
                </div>
                <div class="track-card" onclick="openModal('world-run')">
                    <img src="5343980051684330936.jpg" alt="RUN">
                    <div class="track-info-overlay"><strong>WORLD RUN</strong></div>
                </div>
                <div class="track-card" onclick="openModal('midnight-glow')">
                    <img src="5346018889839611074.jpg" alt="GLOW">
                    <div class="track-info-overlay"><strong>MIDNIGHT GLOW</strong></div>
                </div>
            </div>
        </div>

        <div class="info-card gs-reveal">
            <h2 id="members-title">👥 Участники Respzona</h2>
            <div class="leaders-grid">
                <div class="leader-card main" onclick="openMemberModal('aryx')">
                    <span class="leader-alias">Aryx</span>
                    <h3 id="aryx-name">Арсен</h3>
                    <p class="leader-desc" id="aryx-short">Основатель и главный идеолог...</p>
                    <div class="tap-hint" id="hint-detail">👆 Подробнее</div>
                </div>
                <div class="leader-card main" onclick="openMemberModal('nng')">
                    <span class="leader-alias">Nng</span>
                    <h3 id="nng-name">Дамир</h3>
                    <p class="leader-desc" id="nng-short">Главный идеолог...</p>
                    <div class="tap-hint" id="hint-detail-2">👆 Подробнее</div>
                </div>
                <div class="leader-card" onclick="openMemberModal('nris')">
                    <span class="leader-alias">nRIS</span>
                    <h3 id="nris-name">Радмир</h3>
                    <p class="leader-desc" id="nris-short">Помощник проекта...</p>
                    <div class="tap-hint" id="hint-detail-3">👆 Подробнее</div>
                </div>
            </div>
        </div>

        <div class="info-card gs-reveal">
            <h2 id="gallery-title">📸 Визуал</h2>
            <div class="gallery-grid">
                <div class="gallery-item">
                    <img src="5343980051684331144.jpg" alt="Art 1">
                </div>
                <div class="gallery-item">
                    <img src="5343980051684331143.jpg" alt="Art 2">
                </div>
            </div>
        </div>

        <div class="info-card gs-reveal">
            <h2 id="stats-title">📊 Статистика</h2>
            <div class="stats-grid">
                <div class="stat-box"><h3>2025</h3><p id="stat-founded">Основание</p></div>
                <div class="stat-box"><h3>2</h3><p id="stat-cities">Города</p></div>
                <div class="stat-box"><h3>3+</h3><p id="stat-releases">Релизов</p></div>
                <div class="stat-box"><h3>100%</h3><p id="stat-vibe">Вайб</p></div>
            </div>
        </div>

        <!-- GENERATOR -->
        <div class="info-card gs-reveal" style="border-color: var(--color-secondary);">
            <h2 id="gen-title">🎨 Генератор Обложек</h2>
            <p id="gen-desc">Создай уникальный арт в стиле нашей музыки.</p>
            <div class="generator-ui">
                <input type="text" id="fanName" class="gen-input" placeholder="Твой Ник" value="LISTENER">
                <select id="artStyle" class="gen-select">
                    <option value="guitar">🎸 Cyber Guitar</option>
                    <option value="phonk">🚗 Phonk Drift</option>
                    <option value="glitch">👾 Glitch Core</option>
                    <option value="vinyl">💿 Vinyl Retro</option>
                    <option value="space">🌌 Space Mood</option>
                </select>
                <button class="gen-btn" id="gen-btn" onclick="generateCover()">Сгенерировать</button>
            </div>
            <canvas id="coverCanvas" width="800" height="800" style="width:100%; max-width:350px; display:block; margin:20px auto; border:2px solid #fff; box-shadow: 0 0 30px rgba(0,0,0,0.5);"></canvas>
            <button id="download-btn" onclick="downloadCover()" style="background:transparent; border:1px solid #fff; color:#fff; padding:10px; width:100%; cursor:pointer; border-radius:5px;">⬇ Скачать Обложку</button>
        </div>

        <div class="support-card info-card gs-reveal">
            <h2 id="support-title">💝 Поддержать Группу</h2>
            <div class="support-buttons">
                <a href="https://yoomoney.ru/to/4100118663676748" target="_blank" class="support-btn">💰 YooMoney</a>
                <button class="support-btn" onclick="openDonateModal()">💳 Карта</button>
                <a href="https://boosty.to/respzona/donate" target="_blank" class="support-btn" style="background:linear-gradient(45deg, #f97316, #ea580c)">⭐ Boosty</a>
            </div>
        </div>

        <div class="info-card gs-reveal">
            <h2 id="socials-title">📱 Наши платформы</h2>
            <div class="links-section">
                <a href="https://t.me/respzonamus_bot" target="_blank" class="link-button">🤖 Telegram Bot</a>
                <a href="https://t.me/RESPZONA" target="_blank" class="link-button">📱 Telegram Channel</a>
                <a href="https://www.youtube.com/channel/UChsMW4vND4KZpFOj-NObNTA" target="_blank" class="link-button">🎬 YouTube</a>
            </div>
        </div>
    </main>

    <footer>
        <p id="copyright">© 2026 RESPZONA. Official Website.</p>
        <p style="margin-top:10px;"><a href="mailto:resp.zona@bk.ru" class="email-link">resp.zona@bk.ru</a></p>
    </footer>
</div>

<!-- TRACK MODAL TEMPLATE -->
<div id="modal-tpl" class="modal" onclick="if(event.target===this)this.style.display='none'">
    <div class="modal-content">
        <span class="close-btn" onclick="this.parentElement.parentElement.style.display='none'">&times;</span>
        <h2 id="modal-title" style="margin-top:0; color:var(--color-primary); font-size: 2rem;">TRACK</h2>
        <div style="display:flex; justify-content:space-between; margin:10px 0; border-bottom:1px solid rgba(255,255,255,0.1); padding-bottom:10px;">
            <span style="color:var(--color-secondary);">📅 <span id="modal-date">Date</span></span>
            <span style="color:var(--color-text-secondary);" id="modal-artists">🎤 Aryx, Nng</span>
        </div>
        <div style="background:rgba(0,0,0,0.3); padding:15px; border-radius:10px; margin-top:15px;">
            <p style="color:#aaa; font-size:12px; text-transform:uppercase; margin-bottom:5px;" id="modal-label">О треке:</p>
            <p id="modal-desc" style="font-size:15px; line-height:1.6; color:#fff;">Desc</p>
        </div>
        <a href="#" id="modal-link" target="_blank" class="youtube-link">▶ Слушать на YouTube</a>
    </div>
</div>

<!-- MEMBER MODAL TEMPLATE -->
<div id="member-modal" class="modal" onclick="if(event.target===this)this.style.display='none'">
    <div class="modal-content" style="border-color: var(--color-secondary);">
        <span class="close-btn" onclick="this.parentElement.parentElement.style.display='none'">&times;</span>
        <h2 id="mem-alias" style="margin-top:0; color:var(--color-secondary); font-size: 2.5rem; text-transform:uppercase;">ALIAS</h2>
        <h3 id="mem-name" style="margin-top:-10px; margin-bottom:20px; color:#aaa; font-weight:normal;">Name</h3>
        
        <div style="background:rgba(37, 45, 74, 0.5); padding:20px; border-radius:15px; text-align:left;">
            <p style="margin-bottom:10px;"><strong style="color:var(--color-primary);" id="mem-role-label">Роль:</strong> <span id="mem-role" style="color:#fff;">...</span></p>
            <p style="margin-bottom:10px;"><strong style="color:var(--color-primary);" id="mem-inst-label">Инструменты:</strong> <span id="mem-inst" style="color:#fff;">...</span></p>
            <hr style="border:0; border-top:1px solid rgba(255,255,255,0.1); margin:15px 0;">
            <p style="margin-bottom:5px; font-size:12px; color:#aaa; text-transform:uppercase;" id="mem-more-label">Подробнее:</p>
            <p id="mem-desc" style="line-height:1.6; font-size:15px; color:#ddd;">...</p>
        </div>
    </div>
</div>

<!-- DONATE MODAL TEMPLATE -->
<div id="donate-modal" class="modal" onclick="if(event.target===this)this.style.display='none'">
    <div class="modal-content" style="border-color: var(--color-danger); text-align:center;">
        <span class="close-btn" onclick="this.parentElement.parentElement.style.display='none'">&times;</span>
        <h2 id="donate-title" style="margin-top:0; color:var(--color-danger); font-size: 2rem;">ПОДДЕРЖКА ПРОЕКТА</h2>
        <p id="donate-thanks" style="margin-top:20px; color:#eee;">Спасибо за ваш интерес к Respzona! 🖤</p>
        <p id="donate-desc" style="font-size:14px; color:#aaa; margin-bottom:20px;">Ваши донаты идут на покупку оборудования...</p>
        
        <div class="card-number-box" id="cardNumber">2200 7019 4251 1996</div>
        
        <button id="copy-card-btn" onclick="copyCardNumber()" class="support-btn" style="width:100%; margin-top:10px;">📋 Скопировать номер</button>
    </div>
</div>

<script>
// ===== LANGUAGE DATA =====
const translations = {
    ru: {
        'about-title': '🎵 О нас',
        'about-text-1': 'Respzona — музыкальная команда из Уфы и Стерлитамака, которая стартовала в июне 2025 года и сразу пошла в эксперимент с попом, рэпом и атмосферной электронной музыкой.',
        'about-text-2': 'Для нас важно, чтобы треки были и про эмоции, и про угар: где-то серьёзные вайбы, где-то чисто мемы, но всегда так, чтобы слушатель залип и возвращался к нашим релизам.',
        'releases-title': '🔥 Наши релизы',
        'releases-hint': 'Нажми на обложку, чтобы узнать подробности.',
        'members-title': '👥 Участники Respzona',
        'aryx-name': 'Арсен',
        'aryx-short': 'Основатель и главный идеолог. Полностью отвечает за визуал, код, монтаж и ведение всех соцсетей.',
        'nng-name': 'Дамир',
        'nng-short': 'Главный идеолог, электрогитара, тексты. Event Manager проекта.',
        'nris-name': 'Радмир',
        'nris-short': 'Помощник проекта. 3-я гитара.',
        'hint-detail': '👆 Подробнее',
        'gallery-title': '📸 Визуал',
        'stats-title': '📊 Статистика',
        'stat-founded': 'Основание',
        'stat-cities': 'Города',
        'stat-releases': 'Релизов',
        'stat-vibe': 'Вайб',
        'gen-title': '🎨 Генератор Обложек',
        'gen-desc': 'Создай уникальный арт в стиле нашей музыки.',
        'gen-btn': 'Сгенерировать',
        'download-btn': '⬇ Скачать Обложку',
        'support-title': '💝 Поддержать Группу',
        'socials-title': '📱 Наши платформы',
        'copyright': '© 2026 RESPZONA. Official Website.',
        'modal-label': 'О треке:',
        'modal-artists': '🎤 Aryx, Nng',
        'mem-role-label': 'Роль:',
        'mem-inst-label': 'Инструменты:',
        'mem-more-label': 'Подробнее:',
        'donate-title': 'ПОДДЕРЖКА ПРОЕКТА',
        'donate-thanks': 'Спасибо за ваш интерес к Respzona! 🖤',
        'donate-desc': 'Ваши донаты идят на покупку оборудования, рекламу новых релизов и создание качественного контента.',
        'copy-card-btn': '📋 Скопировать номер',
        'ai-title': 'Система в разработке...',
        'ai-desc': 'ИИ группы скоро будет доступен.',
    },
    en: {
        'about-title': '🎵 About Us',
        'about-text-1': 'Respzona is a music team from Ufa and Sterlitamak that started in June 2025 and immediately experimented with pop, rap, and atmospheric electronic music.',
        'about-text-2': 'For us, it\'s important that the tracks are both about emotions and about fun: somewhere serious vibes, somewhere purely memes, but always so that the listener gets hooked and returns to our releases.',
        'releases-title': '🔥 Our Releases',
        'releases-hint': 'Click on the cover to learn more details.',
        'members-title': '👥 Respzona Members',
        'aryx-name': 'Arsen',
        'aryx-short': 'Founder and chief ideologist. Responsible for all visual design, coding, editing and social media management.',
        'nng-name': 'Damir',
        'nng-short': 'Chief ideologist, electric guitar, lyrics. Project Event Manager.',
        'nris-name': 'Radmir',
        'nris-short': 'Project assistant. 3rd guitar.',
        'hint-detail': '👆 More info',
        'gallery-title': '📸 Visual Gallery',
        'stats-title': '📊 Statistics',
        'stat-founded': 'Founded',
        'stat-cities': 'Cities',
        'stat-releases': 'Releases',
        'stat-vibe': 'Vibe',
        'gen-title': '🎨 Cover Generator',
        'gen-desc': 'Create unique art in the style of our music.',
        'gen-btn': 'Generate',
        'download-btn': '⬇ Download Cover',
        'support-title': '💝 Support Us',
        'socials-title': '📱 Follow Us',
        'copyright': '© 2026 RESPZONA. Official Website.',
        'modal-label': 'About the track:',
        'modal-artists': '🎤 Aryx, Nng',
        'mem-role-label': 'Role:',
        'mem-inst-label': 'Instruments:',
        'mem-more-label': 'More info:',
        'donate-title': 'SUPPORT THE PROJECT',
        'donate-thanks': 'Thank you for your interest in Respzona! 🖤',
        'donate-desc': 'Your donations go towards purchasing equipment, promoting new releases, and creating quality content.',
        'copy-card-btn': '📋 Copy Number',
        'ai-title': 'System in development...',
        'ai-desc': 'Group AI will be available soon.',
    }
};

const trackDataRU = {
    'huday': { 
        title: 'HUDAY', 
        date: '19.06.2025', 
        desc: 'Это чисто мемный по настроению, но при этом завалакивающий трек. Странный сюжет про бездомного и его пирог, абсурдные образы, цепляющий припев на странном лиспе — вайб такой, что хочется включать его снова и снова.' 
    },
    'huday-phonk': { 
        title: 'HUDAY PHONK', 
        date: '30.10.2025', 
        desc: 'Это киберпанк-версия легендарного HUDAY. Кибер-вайб, неоновые синтезаторы, агрессивный beat и атмосфера будущего.' 
    },
    'world-run': { 
        title: 'WORLD RUN PHONK', 
        date: '01.11.2025', 
        desc: 'Энергетичный трек, который бросает вызов законам физики и логики. Быстрый beat, интенсивные синтезаторы.' 
    },
    'midnight-glow': { 
        title: 'MIDNIGHT GLOW', 
        date: 'В разработке', 
        desc: 'Трек, который завораживает холодным и одновременно тёплым сиянием ночи. Синий свет неона, ночные улицы под звёздами и луной.'
    }
};

const trackDataEN = {
    'huday': { 
        title: 'HUDAY', 
        date: '19.06.2025', 
        desc: 'A purely meme-vibed yet captivating track. Strange plot about a homeless man and his pie, absurd imagery, catchy chorus with a strange lisp.' 
    },
    'huday-phonk': { 
        title: 'HUDAY PHONK', 
        date: '30.10.2025', 
        desc: 'A cyberpunk version of the legendary HUDAY. Cyber vibes, neon synthesizers, aggressive beat and future atmosphere.' 
    },
    'world-run': { 
        title: 'WORLD RUN PHONK', 
        date: '01.11.2025', 
        desc: 'An energetic track that defies the laws of physics and logic. Fast beat, intense synthesizers, futuristic atmosphere.' 
    },
    'midnight-glow': { 
        title: 'MIDNIGHT GLOW', 
        date: 'In development', 
        desc: 'A track that fascinates with the cold and warm glow of night. Neon blue light, night streets under stars and moon.'
    }
};

const memberDataRU = {
    'aryx': {
        alias: 'Aryx',
        name: 'Арсен',
        role: 'Главный идеолог',
        instrument: 'Основная гитара',
        desc: 'Главный идеолог проекта. Отвечает за весь визуал (обложки, превью), программную часть, тексты и соцсети. Ведущая гитара и креативный центр проекта.'
    },
    'nng': {
        alias: 'Nng',
        name: 'Дамир',
        role: 'Главный идеолог',
        instrument: 'Электрогитара',
        desc: 'Главный идеолог проекта. Занимается соц сетями, тексты, играет на электрогитаре. Event Manager проекта.'
    },
    'nris': {
        alias: 'nRIS',
        name: 'Радмир',
        role: 'Помощник проекта',
        instrument: '3-я гитара',
        desc: 'Помощник проекта. Оценщик идей и концепций. Играет на третьей гитаре.'
    }
};

const memberDataEN = {
    'aryx': {
        alias: 'Aryx',
        name: 'Arsen',
        role: 'Chief Ideologist',
        instrument: 'Lead Guitar',
        desc: 'Chief ideologist of the project. Responsible for all visual design (covers, previews), programming, lyrics and social media. Lead guitar and creative center of the project.'
    },
    'nng': {
        alias: 'Nng',
        name: 'Damir',
        role: 'Chief Ideologist',
        instrument: 'Electric Guitar',
        desc: 'Chief ideologist of the project. Manages social networks, writes lyrics, plays electric guitar. Project Event Manager.'
    },
    'nris': {
        alias: 'nRIS',
        name: 'Radmir',
        role: 'Project Assistant',
        instrument: '3rd Guitar',
        desc: 'Project assistant. Evaluator of ideas and concepts. Plays the third guitar.'
    }
};

let currentLang = 'ru';

function setLanguage(lang) {
    currentLang = lang;
    
    // Update button active state
    document.getElementById('btn-ru').classList.toggle('active', lang === 'ru');
    document.getElementById('btn-en').classList.toggle('active', lang === 'en');
    
    // Update translations
    const trans = translations[lang];
    for (const [key, value] of Object.entries(trans)) {
        const elem = document.getElementById(key);
        if (elem) elem.textContent = value;
    }
    
    // Save to localStorage
    localStorage.setItem('respzone-lang', lang);
}

// Load saved language
window.addEventListener('DOMContentLoaded', () => {
    const savedLang = localStorage.getItem('respzone-lang') || 'ru';
    setLanguage(savedLang);
    generateCover();
});

// 1. STAR BACKGROUND
const canvas = document.getElementById('star-canvas');
const ctx = canvas.getContext('2d');
let stars = [];

function resizeCanvas() { 
    canvas.width = window.innerWidth; 
    canvas.height = window.innerHeight; 
}

resizeCanvas(); 
window.addEventListener('resize', resizeCanvas);

class Star {
    constructor() { 
        this.reset(); 
        this.y = Math.random() * canvas.height; 
    }
    reset() { 
        this.x = Math.random() * canvas.width; 
        this.y = canvas.height + 10; 
        this.size = Math.random() * 2 + 0.5; 
        this.speed = Math.random() * 0.5 + 0.1; 
        this.opacity = Math.random() * 0.5 + 0.3; 
    }
    update() { 
        this.y -= this.speed; 
        if (this.y < -10) this.reset(); 
    }
    draw() { 
        ctx.fillStyle = `rgba(255, 255, 255, ${this.opacity})`; 
        ctx.beginPath(); 
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2); 
        ctx.fill(); 
    }
}

for (let i = 0; i < 200; i++) stars.push(new Star());

function animateStars() { 
    ctx.clearRect(0, 0, canvas.width, canvas.height); 
    stars.forEach(star => { 
        star.update(); 
        star.draw(); 
    }); 
    requestAnimationFrame(animateStars); 
}

animateStars();

// 2. GSAP
gsap.registerPlugin(ScrollTrigger);
gsap.utils.toArray('.gs-reveal').forEach(elem => {
    gsap.to(elem, { 
        scrollTrigger: { trigger: elem, start: "top 85%" }, 
        y: 0, 
        opacity: 1, 
        duration: 0.8, 
        ease: "power2.out" 
    });
});

// 3. GENERATOR LOGIC
function generateCover() {
    let name = document.getElementById('fanName').value;
    
    const badWords = [
        'сука', 'бля', 'хуй', 'пизд', 'ебат', 'хер', 'мудак', 'урод', 'говн', 'жопа', 
        'fuck', 'bitch', 'shit', 'dick', 'cock', 'pussy', 'whore', 'asshole', 'cunt', 'idiot',
        'faggot', 'nigger', 'nigga', 'retard', 'scum', 'kill', 'die', 'death', 'sex', 'porn'
    ];
    
    const combined = name.toLowerCase().replace(/[^a-zа-яё]/g, '');
    let isToxic = false;
    
    if (combined.length > 0) {
        for (let word of badWords) {
            if (combined.includes(word)) { isToxic = true; break; }
        }
    }

    if(isToxic) {
        alert(currentLang === 'ru' ? "🚫 TOXIC DETECTED! Введите нормальный текст." : "🚫 TOXIC DETECTED! Enter normal text.");
        document.getElementById('fanName').value = "NICE TRY";
        return;
    }
    
    const cvs = document.getElementById('coverCanvas');
    const cx = cvs.getContext('2d');
    name = name.toUpperCase();
    const style = document.getElementById('artStyle').value;
    
    cx.fillStyle = "#000"; 
    cx.fillRect(0,0,800,800);

    if(style === 'guitar') {
        const grd = cx.createLinearGradient(0,0,0,800);
        grd.addColorStop(0, "#050510"); 
        grd.addColorStop(1, "#1a0b2e");
        cx.fillStyle = grd; 
        cx.fillRect(0,0,800,800);
        cx.lineWidth = 3;
        for(let i=0; i<6; i++) {
            cx.strokeStyle = `rgba(0, 212, 255, ${0.4 + i*0.1})`;
            cx.beginPath(); 
            cx.moveTo(350 + i*20, 0); 
            cx.lineTo(350 + i*20, 800); 
            cx.stroke();
        }
        cx.shadowBlur = 40; 
        cx.shadowColor = "#00d4ff";
        cx.fillStyle = "rgba(0,0,0,0.6)"; 
        cx.fillRect(340, 0, 120, 800);
        cx.shadowBlur = 0;
        cx.fillStyle = "#fff"; 
        cx.font = "bold 90px Impact"; 
        cx.textAlign = "center";
        cx.fillText("CYBER", 400, 380); 
        cx.fillText("ACOUSTIC", 400, 480);
    }
    else if (style === 'phonk') {
        cx.fillStyle = "#1a051a"; 
        cx.fillRect(0,0,800,800);
        for(let i=0; i<6000; i++) {
            cx.fillStyle = Math.random()>0.5 ? "rgba(255,0,255,0.3)" : "rgba(0,255,255,0.2)";
            cx.fillRect(Math.random()*800, Math.random()*800, 4, 4);
        }
    }
    else if (style === 'glitch') {
        cx.fillStyle = "#000"; 
        cx.fillRect(0,0,800,800);
        for(let i=0; i<60; i++) {
            cx.fillStyle = `hsl(${Math.random()*360}, 100%, 50%)`;
            cx.fillRect(Math.random()*800, Math.random()*800, Math.random()*150, 6);
        }
        cx.font = "bold 100px Courier New"; 
        cx.textAlign = "center";
        cx.fillStyle = "cyan"; 
        cx.fillText("ERROR", 395, 395);
        cx.fillStyle = "magenta"; 
        cx.fillText("ERROR", 405, 405);
        cx.fillStyle = "white"; 
        cx.fillText("ERROR", 400, 400);
    }
    else if (style === 'vinyl') {
        cx.fillStyle = "#222"; 
        cx.fillRect(0,0,800,800);
        cx.beginPath(); 
        cx.arc(400, 400, 350, 0, Math.PI*2);
        cx.fillStyle = "#111"; 
        cx.fill(); 
        cx.strokeStyle = "#444"; 
        cx.lineWidth=3; 
        cx.stroke();
        for(let r=150; r<340; r+=8) {
            cx.beginPath(); 
            cx.arc(400, 400, r, 0, Math.PI*2); 
            cx.stroke();
        }
        cx.beginPath(); 
        cx.arc(400, 400, 140, 0, Math.PI*2);
        cx.fillStyle = "#ffbe0b"; 
        cx.fill();
        cx.fillStyle = "#000"; 
        cx.font = "bold 40px Arial"; 
        cx.textAlign = "center";
        cx.fillText("SIDE A", 400, 350);
        cx.fillText("GOLD", 400, 450);
    }
    else {
        const grd = cx.createLinearGradient(0,0,800,800);
        grd.addColorStop(0, "#050714"); 
        grd.addColorStop(1, "#1a1f3a");
        cx.fillStyle = grd; 
        cx.fillRect(0,0,800,800);
        for(let i=0; i<100; i++) {
            cx.beginPath(); 
            cx.fillStyle = "white"; 
            cx.arc(Math.random()*800, Math.random()*800, Math.random()*3, 0, Math.PI*2); 
            cx.fill();
        }
        cx.fillStyle = "#00d4ff"; 
        cx.font = "bold 100px Arial"; 
        cx.textAlign = "center";
        cx.fillText("COSMOS", 400, 400);
    }

    cx.save();
    cx.shadowColor = "#00d4ff"; 
    cx.shadowBlur = 20;
    cx.fillStyle = "#fff"; 
    cx.font = "900 100px Impact"; 
    cx.textAlign = "center";
    cx.fillText("RESPZONA", 400, 150);
    cx.shadowBlur = 0;
    cx.strokeStyle = "#000"; 
    cx.lineWidth = 3; 
    cx.strokeText("RESPZONA", 400, 150);
    cx.restore();

    cx.fillStyle = "#fff";
    cx.font = "bold 50px Arial"; 
    cx.shadowBlur = 10; 
    cx.shadowColor="#000";
    cx.fillText("FEAT. " + name, 400, 700);
}

function downloadCover() {
    const link = document.createElement('a');
    link.download = 'Respzona_Fan_Art.png';
    link.href = document.getElementById('coverCanvas').toDataURL();
    link.click();
}

function toggleAI() { 
    const m = document.getElementById('aiModal'); 
    m.style.display = m.style.display === 'block' ? 'none' : 'block'; 
}

// 4. DATA & MODALS
function getTrackData() {
    return currentLang === 'ru' ? trackDataRU : trackDataEN;
}

function getMemberData() {
    return currentLang === 'ru' ? memberDataRU : memberDataEN;
}

function getTrackLinks() {
    return {
        'huday': 'https://youtu.be/zcZD49lSZ0c?si=HR5QgiKETcIQVuOf',
        'huday-phonk': 'https://youtu.be/TycoSw8aKY0?si=wcggh_3fjYZzBf7x',
        'world-run': 'https://youtu.be/QCyttiwe7Fk?si=0YZ3Y4Om8oaqosfn',
        'midnight-glow': 'https://www.youtube.com/channel/UChsMW4vND4KZpFOj-NObNTA'
    };
}

function openModal(id) {
    const trackData = getTrackData();
    const links = getTrackLinks();
    const d = trackData[id];
    
    document.getElementById('modal-title').innerText = d.title;
    document.getElementById('modal-date').innerText = d.date;
    document.getElementById('modal-desc').innerText = d.desc;
    
    const linkBtn = document.getElementById('modal-link');
    if(id === 'midnight-glow') { 
        linkBtn.innerText = currentLang === 'ru' ? "🔔 Подписаться (Скоро)" : "🔔 Subscribe (Coming Soon)"; 
    } 
    else { 
        linkBtn.innerText = currentLang === 'ru' ? "▶ Слушать на YouTube" : "▶ Listen on YouTube"; 
    }
    linkBtn.href = links[id];
    document.getElementById('modal-tpl').style.display = 'block';
}

function openMemberModal(id) {
    const memberData = getMemberData();
    const m = memberData[id];
    
    document.getElementById('mem-alias').innerText = m.alias;
    document.getElementById('mem-name').innerText = m.name;
    document.getElementById('mem-role').innerText = m.role;
    document.getElementById('mem-inst').innerText = m.instrument;
    document.getElementById('mem-desc').innerText = m.desc;
    document.getElementById('member-modal').style.display = 'block';
}

function openDonateModal() {
    document.getElementById('donate-modal').style.display = 'block';
}

function copyCardNumber() {
    navigator.clipboard.writeText('2200701942511996');
    const btn = document.querySelector('#donate-modal .support-btn');
    const originalText = btn.innerHTML;
    btn.innerHTML = currentLang === 'ru' ? '✅ Скопировано!' : '✅ Copied!';
    setTimeout(() => { btn.innerHTML = originalText; }, 2000);
}
</script>
</body>
</html>
