<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏰 Clash Farm</title>
    <style>
        :root { --bg: #0a0e17; --card: #131a26; --gold: #f0b90b; --green: #00c853; --red: #ff1744; --blue: #1a73e8; --text: #e8e8e8; --sub: #8899aa; }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg); color: var(--text); padding: 10px; padding-bottom: 90px; min-height: 100vh; max-width: 500px; margin: 0 auto; }
        .header { background: linear-gradient(135deg, #1a1a3e, #0d1b2a); padding: 18px; border-radius: 14px; text-align: center; margin-bottom: 10px; border: 2px solid var(--gold); }
        .header h1 { font-size: 24px; color: var(--gold); }
        .balance { font-size: 38px; font-weight: bold; color: var(--gold); margin: 8px 0; }
        .stats { display: flex; gap: 6px; margin-top: 8px; }
        .stat { flex: 1; background: rgba(255,255,255,0.05); padding: 8px; border-radius: 8px; text-align: center; }
        .stat-val { font-size: 15px; font-weight: bold; color: var(--green); }
        .stat-label { font-size: 10px; color: var(--sub); }
        .nav { display: flex; gap: 4px; margin: 10px 0; overflow-x: auto; }
        .nav-btn { flex: 1; min-width: 45px; padding: 8px 4px; background: var(--card); border: 1px solid #2a3040; border-radius: 8px; text-align: center; cursor: pointer; font-size: 9px; color: var(--sub); }
        .nav-btn.active { background: var(--gold); color: #000; font-weight: bold; }
        .nav-btn .icon { font-size: 16px; display: block; }
        .section { display: none; }
        .section.active { display: block; }
        .card { background: var(--card); padding: 12px; border-radius: 10px; margin: 8px 0; border: 1px solid #2a3040; }
        .hero-item { display: flex; align-items: center; padding: 10px; background: rgba(255,255,255,0.03); border-radius: 10px; margin: 6px 0; border: 2px solid transparent; }
        .hero-item.owned { border-color: var(--green); }
        .hero-img { width: 55px; height: 55px; border-radius: 12px; margin-right: 10px; background: #1a1a3e; overflow: hidden; flex-shrink: 0; }
        .hero-img img { width: 100%; height: 100%; object-fit: cover; }
        .hero-info { flex: 1; }
        .hero-name { font-weight: bold; font-size: 14px; }
        .hero-inc { color: var(--green); font-size: 11px; }
        .hero-price { color: var(--gold); font-size: 12px; }
        .btn { padding: 8px 14px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; font-size: 13px; }
        .btn-buy { background: var(--green); color: #fff; }
        .btn-owned { background: #1a3a1a; color: var(--green); }
        .btn-action { background: var(--blue); color: #fff; padding: 12px; border-radius: 10px; width: 100%; font-size: 15px; margin: 4px 0; cursor: pointer; border: none; }
        .btn-gold { background: var(--gold); color: #000; padding: 12px; border-radius: 10px; width: 100%; font-size: 15px; margin: 4px 0; cursor: pointer; border: none; font-weight: bold; }
        .btn-red { background: var(--red); color: #fff; padding: 12px; border-radius: 10px; width: 100%; font-size: 15px; margin: 4px 0; cursor: pointer; border: none; }
        .input { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #2a3040; background: var(--bg); color: #fff; font-size: 14px; margin: 5px 0; }
        .task-item { background: rgba(255,255,255,0.03); padding: 10px; border-radius: 10px; margin: 6px 0; display: flex; justify-content: space-between; align-items: center; gap: 8px; }
        .task-info { flex: 1; }
        .badge { background: var(--green); padding: 3px 8px; border-radius: 15px; font-size: 10px; white-space: nowrap; }
        .link-box { background: var(--bg); padding: 8px; border-radius: 8px; word-break: break-all; font-size: 11px; margin: 6px 0; border: 1px solid #2a3040; cursor: pointer; }
        .warning { color: var(--red); font-size: 11px; }
        .info { color: var(--sub); font-size: 11px; }
        .admin-badge { background: var(--red); color: #fff; padding: 2px 6px; border-radius: 8px; font-size: 9px; }
    </style>
</head>
<body>
    <div class="header">
        <h1>🏰 Clash Farm <span class="admin-badge" id="adminBadge" style="display:none">АДМИН</span></h1>
        <div class="balance">💎 <span id="bal">0</span></div>
        <div class="stats">
            <div class="stat"><div class="stat-val" id="rate">0</div><div class="stat-label">⚡ Доход/час</div></div>
            <div class="stat"><div class="stat-val" id="heroCount">1</div><div class="stat-label">🏰 Героев</div></div>
            <div class="stat"><div class="stat-val" id="taskDone">0</div><div class="stat-label">✅ Заданий</div></div>
        </div>
    </div>

    <div class="nav" id="nav"></div>
    <div id="content"></div>

    <script>
        const TG = window.Telegram?.WebApp;
        let userId = localStorage.getItem('cf_userId');
        if (!userId) {
            userId = TG?.initDataUnsafe?.user?.id ? String(TG.initDataUnsafe.user.id) : prompt('Введите ваш Telegram ID (цифры):');
            if (userId) localStorage.setItem('cf_userId', userId);
        }
        if (!userId) userId = 'demo';
        
        let isAdmin = userId === '8684827145';
        let botUsername = 'Clashfarm1bot';
        let tonWallet = 'UQDmNY1TIMIgnALOpAyJ4_XO2uroUNLFVRwGie5AEwzccaps';

        let data = JSON.parse(localStorage.getItem('cf_' + userId) || '{"bal":0,"heroes":["default"],"htime":' + Date.now() + ',"btime":0,"tasks":[],"refs":[],"promosUsed":[]}');
        let heroes = JSON.parse(localStorage.getItem('cf_heroes') || '[{"id":"default","name":"🏹 Лучница","img":"","price":0,"income":0.05,"desc":"Стрелы не промахнутся!"}]');
        let tasks = JSON.parse(localStorage.getItem('cf_tasks') || '[]');
        let promos = JSON.parse(localStorage.getItem('cf_promos') || '[]');

        function save() { localStorage.setItem('cf_' + userId, JSON.stringify(data)); }
        function saveHeroes() { localStorage.setItem('cf_heroes', JSON.stringify(heroes)); }
        function saveTasks() { localStorage.setItem('cf_tasks', JSON.stringify(tasks)); }
        function savePromos() { localStorage.setItem('cf_promos', JSON.stringify(promos)); }

        function getRate() { let r = 0; data.heroes.forEach(hid => { let h = heroes.find(x => x.id === hid); if (h) r += h.income; }); return r; }
        
        function collect() {
            let elapsed = (Date.now() - data.htime) / 3600000;
            let inc = getRate() * elapsed;
            if (inc > 0) { data.bal += inc; data.htime = Date.now(); save(); }
            return inc;
        }

        function updateUI() {
            collect();
            document.getElementById('bal').textContent = data.bal.toFixed(2);
            document.getElementById('rate').textContent = getRate().toFixed(2);
            document.getElementById('heroCount').textContent = data.heroes.length;
            document.getElementById('taskDone').textContent = data.tasks.length;
            if (isAdmin) document.getElementById('adminBadge').style.display = 'inline';
        }

        function showSection(name) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            let sec = document.getElementById('sec_' + name);
            if (sec) sec.classList.add('active');
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            let btn = document.querySelector('[data-section="' + name + '"]');
            if (btn) btn.classList.add('active');
        }

        function renderHeroes() {
            let h = '<h3>🏰 Герои</h3><p class="info">Покупайте героев для пассивного дохода 💎</p>';
            heroes.forEach(hero => {
                let owned = data.heroes.includes(hero.id);
                let imgHtml = hero.img ? `<img src="${hero.img}" alt="${hero.name}">` : hero.name.split(' ')[0];
                h += `<div class="hero-item ${owned ? 'owned' : ''}">
                    <div class="hero-img">${imgHtml}</div>
                    <div class="hero-info">
                        <div class="hero-name">${hero.name}</div>
                        <div class="hero-inc">⚡ +${hero.income}💎/час</div>
                        <div class="hero-inc">💬 "${hero.desc}"</div>
                        ${!owned ? `<div class="hero-price">💰 ${hero.price}💎</div>` : ''}
                    </div>
                    ${owned ? `<button class="btn btn-owned">✅</button>` : 
                      `<button class="btn btn-buy" onclick="buyHero('${hero.id}')">Купить</button>`}
                </div>`;
            });
            return h;
        }

        function buyHero(id) {
            if (data.heroes.includes(id)) return alert('Уже куплен!');
            let hero = heroes.find(x => x.id === id);
            if (!hero) return;
            if (data.bal < hero.price) return alert('Недостаточно 💎!');
            data.bal -= hero.price;
            data.heroes.push(id);
            data.htime = Date.now();
            save();
            updateUI();
            refreshAll();
            alert(`✅ Куплен: ${hero.name}!`);
        }

        function renderTasks() {
            if (tasks.length === 0) return '<h3>📋 Задания</h3><p class="info">Пока нет заданий.</p>';
            let h = '<h3>📋 Задания</h3>';
            tasks.forEach((t, i) => {
                let done = data.tasks.includes(i);
                h += `<div class="task-item">
                    <div class="task-info">
                        <div class="hero-name">${t.name}</div>
                        <div class="hero-price">💰 +${t.reward}💎</div>
                    </div>
                    ${done ? '<span class="badge">✅</span>' : 
                      `<a href="${t.link}" target="_blank" class="btn btn-gold" style="padding:6px 10px;font-size:11px;text-decoration:none;width:auto;">🔗</a>
                       <button class="btn btn-buy" style="padding:6px 10px;font-size:11px;" onclick="checkTask(${i})">✅</button>`}
                </div>`;
            });
            return h;
        }

        function checkTask(i) {
            if (data.tasks.includes(i)) return;
            data.tasks.push(i);
            data.bal += tasks[i].reward;
            if (data.tasks.length % 5 === 0) {
                // Бонус рефереру
            }
            save();
            updateUI();
            refreshAll();
            alert(`✅ +${tasks[i].reward}💎`);
        }

        function renderRefs() {
            let link = `https://t.me/${botUsername}?start=${userId}`;
            return `<h3>👥 Реферальная система</h3>
                <div class="card">
                    <p><b>🔗 Ваша ссылка:</b></p>
                    <div class="link-box" onclick="copyText('${link}')">${link} (нажми, чтобы скопировать)</div>
                    <button class="btn btn-gold" onclick="copyText('${link}')">📋 Скопировать ссылку</button>
                    <p class="info" style="margin-top:8px">👤 Рефералов: <b>${data.refs.length}</b></p>
                    <p class="info">💎 +1💎 за 5 заданий реферала | 💸 +5% от пополнений</p>
                </div>`;
        }

        function renderBonus() {
            let can = Date.now() - data.btime > 86400000;
            return `<h3>🎁 Бонус</h3>
                <div class="card" style="text-align:center">
                    <p style="font-size:45px">🎁</p>
                    <p style="font-size:18px">+0.5💎 каждый день</p>
                    <button class="btn btn-gold" ${can ? '' : 'disabled'} onclick="getBonus()">${can ? '🎁 Забрать бонус' : '⏳ Уже получен'}</button>
                </div>
                <h3>🎫 Промокод</h3>
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
            let p = promos.find(x => x.code === code);
            if (!p) return alert('❌ Промокод не найден!');
            if (data.promosUsed.includes(code)) return alert('❌ Уже использован!');
            if (p.uses <= 0) return alert('❌ Закончился!');
            data.bal += p.reward;
            p.uses--;
            data.promosUsed.push(code);
            save();
            savePromos();
            updateUI();
            refreshAll();
            alert(`✅ +${p.reward}💎!`);
        }

        function renderDepo() {
            return `<h3>💎 Пополнение через TON</h3>
                <div class="card">
                    <p>📌 <b>Курс:</b> 1 TON = 100💎</p>
                    <p>📌 <b>Кошелёк:</b></p>
                    <div class="link-box" onclick="copyText('${tonWallet}')">${tonWallet} (нажми, чтобы скопировать)</div>
                    <button class="btn btn-gold" onclick="copyText('${tonWallet}')">📋 Скопировать адрес</button>
                    <p class="warning" style="margin-top:8px">⚠️ В комментарии к переводу укажите ваш ID: <b>${userId}</b></p>
                    <button class="btn-action" onclick="copyText('${userId}')">📋 Скопировать мой ID</button>
                </div>`;
        }

        function renderWithdraw() {
            return `<h3>💸 Вывод средств</h3>
                <div class="card">
                    <p>📌 <b>Курс:</b> 100💎 = 1 TON</p>
                    <p>📌 <b>Комиссия:</b> 5%</p>
                    <p>📌 <b>Минимум:</b> 50💎</p>
                    <p>💰 <b>Баланс:</b> ${data.bal.toFixed(2)}💎</p>
                    <input class="input" id="wdAmt" type="number" placeholder="Сумма (мин 50💎)">
                    <input class="input" id="wdWal" type="text" placeholder="Ваш TON кошелёк">
                    <button class="btn btn-gold" onclick="withdraw()">💸 Отправить заявку</button>
                </div>`;
        }

        function withdraw() {
            let amt = parseFloat(document.getElementById('wdAmt').value);
            let wal = document.getElementById('wdWal').value;
            if (!amt || amt < 50 || amt > data.bal) return alert('❌ Неверная сумма!');
            if (!wal) return alert('❌ Введите кошелёк!');
            let ton = (amt * 0.95) / 100;
            data.bal -= amt;
            save();
            updateUI();
            refreshAll();
            alert(`✅ Заявка на ${ton.toFixed(2)} TON отправлена!\nОжидайте обработки.`);
        }

        function renderAdmin() {
            if (!isAdmin) return '';
            return `<h3>🔧 Админ-панель</h3>
                <div class="card">
                    <h4>➕ Добавить героя</h4>
                    <input class="input" id="hName" placeholder="Имя героя">
                    <input class="input" id="hImg" placeholder="Ссылка на картинку (URL)">
                    <input class="input" id="hPrice" type="number" placeholder="Цена в 💎">
                    <input class="input" id="hIncome" type="number" placeholder="Доход в час" step="0.01">
                    <input class="input" id="hDesc" placeholder="Описание">
                    <button class="btn btn-buy" onclick="addHero()">✅ Добавить героя</button>
                </div>
                <div class="card">
                    <h4>📋 Добавить задание</h4>
                    <input class="input" id="tName" placeholder="Название задания">
                    <input class="input" id="tLink" placeholder="Ссылка">
                    <input class="input" id="tReward" type="number" placeholder="Награда 💎">
                    <button class="btn btn-buy" onclick="addTask()">✅ Добавить задание</button>
                </div>
                <div class="card">
                    <h4>🎫 Создать промокод</h4>
                    <input class="input" id="pCode" placeholder="Код">
                    <input class="input" id="pReward" type="number" placeholder="Награда 💎">
                    <input class="input" id="pUses" type="number" placeholder="Активаций (0=безлимит)">
                    <button class="btn btn-buy" onclick="addPromo()">✅ Создать</button>
                </div>
                <div class="card">
                    <h4>💰 Управление балансом</h4>
                    <input class="input" id="aUserId" placeholder="ID пользователя">
                    <input class="input" id="aAmount" type="number" placeholder="Сумма 💎">
                    <button class="btn btn-buy" onclick="changeBal(1)">➕ Начислить</button>
                    <button class="btn btn-red" onclick="changeBal(-1)">➖ Снять</button>
                </div>`;
        }

        function addHero() {
            let name = document.getElementById('hName').value.trim();
            let img = document.getElementById('hImg').value.trim();
            let price = parseFloat(document.getElementById('hPrice').value);
            let income = parseFloat(document.getElementById('hIncome').value);
            let desc = document.getElementById('hDesc').value.trim();
            if (!name || isNaN(price) || isNaN(income)) return alert('❌ Заполните все поля!');
            heroes.push({id: 'h' + Date.now(), name, img, price, income, desc});
            saveHeroes();
            alert('✅ Герой добавлен!');
            refreshAll();
        }

        function addTask() {
            let name = document.getElementById('tName').value.trim();
            let link = document.getElementById('tLink').value.trim();
            let reward = parseFloat(document.getElementById('tReward').value);
            if (!name || !link || !reward) return alert('❌ Заполните все поля!');
            tasks.push({name, link, reward});
            saveTasks();
            alert('✅ Задание добавлено!');
            refreshAll();
        }

        function addPromo() {
            let code = document.getElementById('pCode').value.trim().toUpperCase();
            let reward = parseFloat(document.getElementById('pReward').value);
            let uses = parseInt(document.getElementById('pUses').value) || 999999;
            if (!code || !reward) return alert('❌ Заполните поля!');
            promos.push({code, reward, uses});
            savePromos();
            alert('✅ Промокод создан!');
            refreshAll();
        }

        function changeBal(sign) {
            let uid = document.getElementById('aUserId').value.trim();
            let amt = parseFloat(document.getElementById('aAmount').value);
            if (!uid || !amt) return alert('❌ Заполните ID и сумму!');
            let userData = JSON.parse(localStorage.getItem('cf_' + uid) || '{"bal":0,"heroes":["default"],"htime":' + Date.now() + ',"btime":0,"tasks":[],"refs":[],"promosUsed":[]}');
            userData.bal += amt * sign;
            if (userData.bal < 0) userData.bal = 0;
            localStorage.setItem('cf_' + uid, JSON.stringify(userData));
            if (uid === userId) { data = userData; save(); updateUI(); }
            alert(`✅ ${sign > 0 ? 'Начислено' : 'Снято'} ${amt}💎 пользователю ${uid}`);
            refreshAll();
        }

        function copyText(t) {
            navigator.clipboard?.writeText(t);
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

        // Старт
        updateUI();
        document.getElementById('nav').innerHTML = `
            <div class="nav-btn active" data-section="heroes" onclick="showSection('heroes')"><span class="icon">🏰</span>Герои</div>
            <div class="nav-btn" data-section="tasks" onclick="showSection('tasks')"><span class="icon">📋</span>Задания</div>
            <div class="nav-btn" data-section="refs" onclick="showSection('refs')"><span class="icon">👥</span>Реф</div>
            <div class="nav-btn" data-section="bonus" onclick="showSection('bonus')"><span class="icon">🎁</span>Бонус</div>
            <div class="nav-btn" data-section="depo" onclick="showSection('depo')"><span class="icon">💎</span>Пополн</div>
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
