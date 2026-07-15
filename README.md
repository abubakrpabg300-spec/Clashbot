<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏰 Clash Farm</title>
    <style>
        :root {
            --bg: #0a0e17; --card: #131a26; --gold: #f0b90b;
            --green: #00c853; --red: #ff1744; --blue: #1a73e8;
            --text: #e8e8e8; --sub: #8899aa;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg); color: var(--text); padding: 12px; padding-bottom: 90px; min-height: 100vh; max-width: 500px; margin: 0 auto; }
        .header { background: linear-gradient(135deg, #1a1a3e, #0d1b2a); padding: 20px; border-radius: 16px; text-align: center; margin-bottom: 12px; border: 2px solid var(--gold); box-shadow: 0 0 20px rgba(240,185,11,0.2); }
        .header h1 { font-size: 26px; color: var(--gold); margin-bottom: 5px; }
        .balance { font-size: 42px; font-weight: bold; color: var(--gold); }
        .stats { display: flex; gap: 8px; margin-top: 10px; }
        .stat { flex: 1; background: rgba(255,255,255,0.05); padding: 10px; border-radius: 10px; text-align: center; }
        .stat-val { font-size: 16px; font-weight: bold; color: var(--green); }
        .stat-label { font-size: 10px; color: var(--sub); }
        .nav { display: flex; gap: 5px; margin: 10px 0; overflow-x: auto; -webkit-overflow-scrolling: touch; }
        .nav-btn { flex: 1; min-width: 50px; padding: 10px 6px; background: var(--card); border: 1px solid #2a3040; border-radius: 10px; text-align: center; cursor: pointer; font-size: 10px; color: var(--sub); transition: all 0.2s; }
        .nav-btn.active { background: var(--gold); color: #000; font-weight: bold; }
        .nav-btn .icon { font-size: 18px; display: block; margin-bottom: 2px; }
        .section { display: none; }
        .section.active { display: block; }
        .card { background: var(--card); padding: 14px; border-radius: 12px; margin: 8px 0; border: 1px solid #2a3040; }
        .card h3 { margin-bottom: 8px; font-size: 17px; }
        .hero-item { display: flex; align-items: center; padding: 12px; background: rgba(255,255,255,0.03); border-radius: 10px; margin: 6px 0; border: 2px solid transparent; }
        .hero-item.owned { border-color: var(--green); }
        .hero-icon { font-size: 40px; margin-right: 10px; }
        .hero-info { flex: 1; }
        .hero-name { font-weight: bold; font-size: 15px; }
        .hero-inc { color: var(--green); font-size: 12px; }
        .hero-price { color: var(--gold); font-size: 13px; font-weight: bold; }
        .btn { padding: 10px 16px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; font-size: 14px; }
        .btn-buy { background: var(--green); color: #fff; }
        .btn-owned { background: #1a3a1a; color: var(--green); }
        .btn-action { background: var(--blue); color: #fff; padding: 14px; border-radius: 10px; width: 100%; font-size: 16px; margin: 5px 0; cursor: pointer; border: none; }
        .btn-gold { background: var(--gold); color: #000; padding: 14px; border-radius: 10px; width: 100%; font-size: 16px; margin: 5px 0; cursor: pointer; border: none; font-weight: bold; }
        .btn-red { background: var(--red); color: #fff; }
        .input { width: 100%; padding: 12px; border-radius: 8px; border: 1px solid #2a3040; background: var(--bg); color: #fff; font-size: 15px; margin: 6px 0; }
        .task-item { background: rgba(255,255,255,0.03); padding: 12px; border-radius: 10px; margin: 8px 0; display: flex; justify-content: space-between; align-items: center; }
        .task-info { flex: 1; }
        .task-name { font-weight: bold; }
        .task-reward { color: var(--gold); font-size: 13px; }
        .badge { background: var(--green); padding: 4px 10px; border-radius: 20px; font-size: 11px; }
        .badge-gray { background: #2a3040; padding: 4px 10px; border-radius: 20px; font-size: 11px; }
        .link-box { background: var(--bg); padding: 10px; border-radius: 8px; word-break: break-all; font-size: 12px; margin: 8px 0; border: 1px solid #2a3040; }
        .warning { color: var(--red); font-size: 12px; }
        .info { color: var(--sub); font-size: 12px; }
        .admin-badge { background: var(--red); color: #fff; padding: 2px 8px; border-radius: 10px; font-size: 10px; margin-left: 5px; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 1000; justify-content: center; align-items: center; }
        .modal.active { display: flex; }
        .modal-content { background: var(--card); padding: 20px; border-radius: 16px; width: 90%; max-width: 400px; border: 1px solid var(--gold); }
    </style>
</head>
<body>
    <div class="header">
        <h1>🏰 Clash Farm <span class="admin-badge" id="adminBadge" style="display:none">АДМИН</span></h1>
        <div class="balance">💎 <span id="bal">0</span></div>
        <div class="stats">
            <div class="stat"><div class="stat-val" id="rate">0</div><div class="stat-label">⚡ Доход/час</div></div>
            <div class="stat"><div class="stat-val" id="heroCount">1</div><div class="stat-label">🏰 Героев</div></div>
            <div class="stat"><div class="stat-val" id="taskCount">0</div><div class="stat-label">✅ Заданий</div></div>
        </div>
    </div>

    <div class="nav" id="nav"></div>
    <div id="content"></div>

    <!-- Модальное окно -->
    <div class="modal" id="modal">
        <div class="modal-content" id="modalContent"></div>
    </div>

    <script>
        const TG = window.Telegram?.WebApp;
        let user = TG?.initDataUnsafe?.user || {};
        let userId = user.id ? String(user.id) : 'demo';
        let isAdmin = userId === '8684827145';

        // Данные
        let data = JSON.parse(localStorage.getItem('cf_data_' + userId) || '{"bal":0,"heroes":[0],"htime":' + Date.now() + ',"btime":0,"tasks":[],"refId":"' + userId + '","refs":[]}');
        let tasks = JSON.parse(localStorage.getItem('cf_tasks') || '[]');
        let promos = JSON.parse(localStorage.getItem('cf_promos') || '[]');

        const heroes = [
            {n:"🏹 Лучница",p:0,i:0.05,d:"Стрелы не промахнутся!"},
            {n:"👶 Гоблин",p:100,i:0.1,d:"Где золото?!"},
            {n:"⚔️ Рыцарь",p:250,i:0.25,d:"За честь и корону!"},
            {n:"🐗 Кабан",p:500,i:0.5,d:"Хрю-хрю, с дороги!"},
            {n:"🧙 Волшебник",p:1000,i:1,d:"Магия решит всё!"},
            {n:"🐉 Дракон",p:2500,i:2.5,d:"Огонь и ярость!"},
            {n:"🔮 Искра",p:5000,i:5,d:"Скорость молнии!"},
            {n:"👸🏼 Принцесса",p:10000,i:10,d:"Королевская мощь!"},
            {n:"🤴🏼 Король",p:25000,i:25,d:"Вся арена моя!"}
        ];

        function save() { localStorage.setItem('cf_data_' + userId, JSON.stringify(data)); }
        function saveTasks() { localStorage.setItem('cf_tasks', JSON.stringify(tasks)); }
        function savePromos() { localStorage.setItem('cf_promos', JSON.stringify(promos)); }

        function getRate() { let r = 0; data.heroes.forEach(h => r += heroes[h].i); return r; }
        
        function collect() {
            let elapsed = (Date.now() - data.htime) / 3600000;
            let inc = getRate() * elapsed;
            if (inc > 0) { data.bal += inc; data.htime = Date.now(); save(); }
            return inc;
        }

        function updateUI() {
            collect();
            document.getElementById('bal').textContent = data.bal.toFixed(1);
            document.getElementById('rate').textContent = getRate().toFixed(2);
            document.getElementById('heroCount').textContent = data.heroes.length;
            document.getElementById('taskCount').textContent = data.tasks.length;
            if (isAdmin) document.getElementById('adminBadge').style.display = 'inline';
        }

        function showSection(name) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.getElementById('sec_' + name).classList.add('active');
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.querySelector('[data-section="' + name + '"]').classList.add('active');
        }

        function renderHeroes() {
            let h = '<h3>🏰 Герои</h3><p class="info">Покупайте героев для пассивного дохода</p>';
            heroes.forEach((hero, i) => {
                let owned = data.heroes.includes(i);
                h += `<div class="hero-item ${owned ? 'owned' : ''}">
                    <div class="hero-icon">${hero.n.split(' ')[0]}</div>
                    <div class="hero-info">
                        <div class="hero-name">${hero.n}</div>
                        <div class="hero-inc">⚡ +${hero.i}💎/час | 💬 "${hero.d}"</div>
                        ${!owned ? `<div class="hero-price">💰 ${hero.p}💎</div>` : ''}
                    </div>
                    ${owned ? `<button class="btn btn-owned">✅ Куплен</button>` : 
                      `<button class="btn btn-buy" onclick="buyHero(${i})">Купить за ${hero.p}💎</button>`}
                </div>`;
            });
            return h;
        }

        function buyHero(i) {
            if (data.heroes.includes(i)) return alert('Этот герой уже куплен!');
            if (data.bal < heroes[i].p) return alert('Недостаточно 💎! Выполняйте задания и копите алмазы.');
            data.bal -= heroes[i].p;
            data.heroes.push(i);
            data.htime = Date.now();
            save();
            updateUI();
            refreshAll();
        }

        function renderTasks() {
            if (tasks.length === 0) return '<h3>📋 Задания</h3><p class="info">Пока нет доступных заданий. Админ скоро добавит новые.</p>';
            let h = '<h3>📋 Задания</h3>';
            tasks.forEach((t, i) => {
                let done = data.tasks.includes(i);
                h += `<div class="task-item">
                    <div class="task-info">
                        <div class="task-name">${t.name}</div>
                        <div class="task-reward">💰 +${t.reward}💎</div>
                    </div>
                    ${done ? '<span class="badge">✅ Выполнено</span>' : 
                      `<span><a href="${t.link}" target="_blank" class="btn btn-gold" style="padding:8px 12px;font-size:12px;text-decoration:none;">🔗 Перейти</a>
                      <button class="btn btn-buy" style="padding:8px 12px;font-size:12px;" onclick="checkTask(${i})">✅ Проверить</button></span>`}
                </div>`;
            });
            return h;
        }

        function checkTask(i) {
            if (data.tasks.includes(i)) return;
            data.tasks.push(i);
            data.bal += tasks[i].reward;
            // Проверка реферала
            if (data.tasks.length === 5 && data.refId !== userId) {
                // Бонус рефереру (в реальном боте)
            }
            save();
            updateUI();
            refreshAll();
            alert(`✅ Задание выполнено! +${tasks[i].reward}💎`);
        }

        function renderRefs() {
            let link = `https://t.me/ClashFarmBot?start=${userId}`;
            return `<h3>👥 Реферальная система</h3>
                <p class="info">Приглашайте друзей и получайте бонусы!</p>
                <div class="card">
                    <p><b>🔗 Ваша реферальная ссылка:</b></p>
                    <div class="link-box">${link}</div>
                    <button class="btn btn-gold" onclick="copyText('${link}')">📋 Скопировать ссылку</button>
                </div>
                <div class="card">
                    <p>👤 Рефералов: <b>${data.refs.length} чел.</b></p>
                    <p class="info">💎 +1💎 за каждые 5 заданий реферала</p>
                    <p class="info">💸 +5% от пополнений рефералов</p>
                </div>`;
        }

        function renderBonus() {
            let can = Date.now() - data.btime > 86400000;
            return `<h3>🎁 Ежедневный бонус</h3>
                <div class="card" style="text-align:center">
                    <p style="font-size:50px">🎁</p>
                    <p style="font-size:20px">+0.5💎</p>
                    <p class="info">Каждые 24 часа</p>
                    <button class="btn btn-gold" ${can ? '' : 'disabled'} onclick="getBonus()">
                        ${can ? '🎁 Забрать бонус' : '⏳ Уже получен'}
                    </button>
                </div>
                <h3 style="margin-top:15px">🎫 Промокод</h3>
                <input class="input" id="promoCode" placeholder="Введите промокод">
                <button class="btn-action" onclick="usePromo()">Активировать</button>`;
        }

        function getBonus() {
            if (Date.now() - data.btime < 86400000) return;
            data.bal += 0.5;
            data.btime = Date.now();
            save();
            updateUI();
            refreshAll();
            alert('✅ +0.5💎!');
        }

        function usePromo() {
            let code = document.getElementById('promoCode').value.trim().toUpperCase();
            let promo = promos.find(p => p.code === code);
            if (!promo) return alert('❌ Промокод не найден!');
            if (promo.usedBy && promo.usedBy.includes(userId)) return alert('❌ Вы уже использовали этот промокод!');
            if (promo.uses <= 0) return alert('❌ Промокод закончился!');
            data.bal += promo.reward;
            promo.uses--;
            if (!promo.usedBy) promo.usedBy = [];
            promo.usedBy.push(userId);
            save();
            savePromos();
            updateUI();
            refreshAll();
            alert(`✅ +${promo.reward}💎!`);
        }

        function renderDepo() {
            return `<h3>💎 Пополнение через TON</h3>
                <div class="card">
                    <p>📌 <b>Курс:</b> 1 TON = 100💎</p>
                    <p>📌 <b>Минимум:</b> 1 TON</p>
                    <p>📌 <b>Кошелёк:</b></p>
                    <div class="link-box">UQDmNY1TIMIgnALOpAyJ4_XO2uroUNLFVRwGie5AEwzccaps</div>
                    <p class="warning">⚠️ В комментарии к переводу обязательно укажите ваш ID: <b>${userId}</b></p>
                    <p class="warning">Без ID деньги не будут зачислены!</p>
                    <button class="btn-action" onclick="copyText('${userId}')">📋 Скопировать мой ID</button>
                </div>`;
        }

        function renderWithdraw() {
            return `<h3>💸 Вывод средств</h3>
                <div class="card">
                    <p>📌 <b>Курс:</b> 100💎 = 1 TON</p>
                    <p>📌 <b>Комиссия:</b> 5%</p>
                    <p>📌 <b>Минимум:</b> 50💎</p>
                    <p>💰 <b>Ваш баланс:</b> ${data.bal.toFixed(1)}💎</p>
                    <input class="input" id="wdAmount" type="number" placeholder="Сумма для вывода (минимум 50💎)">
                    <p class="info" id="wdResult"></p>
                    <input class="input" id="wdWallet" type="text" placeholder="Ваш TON кошелёк">
                    <button class="btn btn-gold" onclick="withdraw()">💸 Отправить заявку</button>
                </div>`;
        }

        document.getElementById('wdAmount')?.addEventListener('input', function() {
            let amt = parseFloat(this.value);
            if (amt && amt >= 50) {
                let fee = amt * 0.05;
                let ton = (amt - fee) / 100;
                document.getElementById('wdResult').textContent = `💰 Вы получите: ${ton.toFixed(2)} TON (комиссия: ${fee.toFixed(1)}💎)`;
            }
        });

        function withdraw() {
            let amt = parseFloat(document.getElementById('wdAmount').value);
            let wallet = document.getElementById('wdWallet').value;
            if (!amt || amt < 50) return alert('❌ Минимальная сумма вывода: 50💎');
            if (amt > data.bal) return alert('❌ Недостаточно средств!');
            if (!wallet) return alert('❌ Введите адрес TON кошелька!');
            let fee = amt * 0.05;
            let ton = (amt - fee) / 100;
            data.bal -= amt;
            save();
            updateUI();
            refreshAll();
            alert(`✅ Заявка на ${ton.toFixed(2)} TON отправлена!\nОжидайте обработки в течение 24 часов.`);
        }

        // Админ-панель
        function renderAdmin() {
            if (!isAdmin) return '';
            return `<h3>🔧 Админ-панель <span class="admin-badge">ADMIN</span></h3>
                <div class="card">
                    <h4>📋 Добавить задание</h4>
                    <input class="input" id="taskName" placeholder="Название задания">
                    <input class="input" id="taskLink" placeholder="Ссылка (https://...)">
                    <input class="input" id="taskReward" type="number" placeholder="Награда в 💎">
                    <button class="btn btn-buy" onclick="addTask()">✅ Добавить задание</button>
                </div>
                <div class="card">
                    <h4>🎫 Создать промокод</h4>
                    <input class="input" id="promoCodeNew" placeholder="Код (например: BONUS)">
                    <input class="input" id="promoReward" type="number" placeholder="Награда в 💎">
                    <input class="input" id="promoUses" type="number" placeholder="Количество активаций (0=безлимит)">
                    <button class="btn btn-buy" onclick="addPromo()">✅ Создать промокод</button>
                </div>
                <div class="card">
                    <h4>📊 Статистика</h4>
                    <p>👥 Пользователей: <b>${Object.keys(localStorage).filter(k => k.startsWith('cf_data_')).length}</b></p>
                    <p>📋 Заданий: <b>${tasks.length}</b></p>
                    <p>🎫 Промокодов: <b>${promos.length}</b></p>
                </div>`;
        }

        function addTask() {
            let name = document.getElementById('taskName').value.trim();
            let link = document.getElementById('taskLink').value.trim();
            let reward = parseFloat(document.getElementById('taskReward').value);
            if (!name || !link || !reward) return alert('❌ Заполните все поля!');
            tasks.push({name, link, reward});
            saveTasks();
            alert('✅ Задание добавлено!');
            refreshAll();
        }

        function addPromo() {
            let code = document.getElementById('promoCodeNew').value.trim().toUpperCase();
            let reward = parseFloat(document.getElementById('promoReward').value);
            let uses = parseInt(document.getElementById('promoUses').value) || 999999;
            if (!code || !reward) return alert('❌ Заполните все поля!');
            promos.push({code, reward, uses, usedBy: []});
            savePromos();
            alert('✅ Промокод создан!');
            refreshAll();
        }

        function copyText(text) {
            navigator.clipboard?.writeText(text);
            alert('✅ Скопировано!');
        }

        function refreshAll() {
            document.getElementById('sec_heroes').innerHTML = renderHeroes();
            document.getElementById('sec_tasks').innerHTML = renderTasks();
            document.getElementById('sec_refs').innerHTML = renderRefs();
            document.getElementById('sec_bonus').innerHTML = renderBonus();
            document.getElementById('sec_depo').innerHTML = renderDepo();
            document.getElementById('sec_withdraw').innerHTML = renderWithdraw();
            if (isAdmin) document.getElementById('sec_admin').innerHTML = renderAdmin();
        }

        // Инициализация
        updateUI();
        document.getElementById('nav').innerHTML = `
            <div class="nav-btn active" data-section="heroes" onclick="showSection('heroes')"><span class="icon">🏰</span>Герои</div>
            <div class="nav-btn" data-section="tasks" onclick="showSection('tasks')"><span class="icon">📋</span>Задания</div>
            <div class="nav-btn" data-section="refs" onclick="showSection('refs')"><span class="icon">👥</span>Рефералы</div>
            <div class="nav-btn" data-section="bonus" onclick="showSection('bonus')"><span class="icon">🎁</span>Бонус</div>
            <div class="nav-btn" data-section="depo" onclick="showSection('depo')"><span class="icon">💎</span>Пополнение</div>
            <div class="nav-btn" data-section="withdraw" onclick="showSection('withdraw')"><span class="icon">💸</span>Вывод</div>
            ${isAdmin ? '<div class="nav-btn" data-section="admin" onclick="showSection(\'admin\')"><span class="icon">🔧</span>Админ</div>' : ''}
        `;
        document.getElementById('content').innerHTML = `
            <div class="section active" id="sec_heroes"></div>
            <div class="section" id="sec_tasks"></div>
            <div class="section" id="sec_refs"></div>
            <div class="section" id="sec_bonus"></div>
            <div class="section" id="sec_depo"></div>
            <div class="section" id="sec_withdraw"></div>
            ${isAdmin ? '<div class="section" id="sec_admin"></div>' : ''}
        `;
        refreshAll();

        if (TG) { TG.ready(); TG.expand(); }
    </script>
</body>
</html>
