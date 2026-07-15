<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏰 Clash Farm</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: Arial; background: #0d1117; color: white; padding: 10px; min-height: 100vh; }
        .header { text-align: center; padding: 20px; background: #161b22; border-radius: 15px; margin-bottom: 10px; border: 2px solid #f0b90b; }
        .header h1 { color: #f0b90b; }
        .balance { font-size: 36px; font-weight: bold; color: #f0b90b; margin: 10px 0; }
        .tabs { display: flex; gap: 3px; margin: 10px 0; flex-wrap: wrap; }
        .tab { flex: 1; min-width: 60px; padding: 10px 5px; text-align: center; background: #21262d; border-radius: 8px; font-size: 12px; cursor: pointer; }
        .tab.active { background: #f0b90b; color: #0d1117; font-weight: bold; }
        .card { background: #161b22; padding: 15px; border-radius: 12px; margin: 10px 0; border: 1px solid #30363d; }
        .hero { display: flex; justify-content: space-between; align-items: center; padding: 12px; background: #21262d; border-radius: 10px; margin: 8px 0; }
        .hero.owned { border: 2px solid #238636; }
        .hero-info { flex: 1; }
        .hero-name { font-weight: bold; font-size: 16px; }
        .hero-inc { color: #3fb950; font-size: 13px; }
        .hero-price { color: #f0b90b; }
        .btn { padding: 12px 20px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; }
        .btn-buy { background: #238636; color: white; }
        .btn-owned { background: #30363d; color: #484f58; }
        .btn-action { background: #1f6feb; color: white; padding: 14px; border: none; border-radius: 10px; width: 100%; font-size: 16px; margin: 5px 0; cursor: pointer; }
        .input { width: 100%; padding: 12px; border-radius: 8px; border: 1px solid #30363d; background: #0d1117; color: white; font-size: 16px; margin: 8px 0; }
        .link-box { background: #21262d; padding: 12px; border-radius: 8px; word-break: break-all; font-size: 13px; margin: 10px 0; }
        .info { color: #8b949e; font-size: 13px; margin: 5px 0; }
        .warning { color: #f85149; font-size: 13px; }
    </style>
</head>
<body>
    <div class="header">
        <h1>🏰 Clash Farm</h1>
        <div class="balance">💎 <span id="bal">0</span></div>
        <div class="info">⚡ Доход: +<span id="rate">0</span>💎/час</div>
    </div>

    <div class="tabs" id="tabs"></div>
    <div id="content"></div>

    <script>
        // Данные пользователя (сохраняются в localStorage)
        let data = JSON.parse(localStorage.getItem('clash_data') || '{"bal":0,"heroes":[0],"htime":' + Date.now() + ',"btime":0,"tasks":[],"refs":[],"promos":[]}');
        
        const heroes = [
            {n:"🏹 Лучница",p:0,i:0.05},
            {n:"👶 Гоблин",p:100,i:0.1},
            {n:"⚔️ Рыцарь",p:250,i:0.25},
            {n:"🐗 Кабан",p:500,i:0.5},
            {n:"🧙 Волшебник",p:1000,i:1},
            {n:"🐉 Дракон",p:2500,i:2.5},
            {n:"🔮 Искра",p:5000,i:5},
            {n:"👸🏼 Принцесса",p:10000,i:10},
            {n:"🤴🏼 Король",p:25000,i:25}
        ];

        function save() { localStorage.setItem('clash_data', JSON.stringify(data)); }
        
        function getRate() {
            let r = 0;
            data.heroes.forEach(h => { r += heroes[h].i; });
            return r;
        }

        function collect() {
            let elapsed = (Date.now() - data.htime) / 3600000;
            let inc = getRate() * elapsed;
            if (inc > 0) {
                data.bal += inc;
                data.htime = Date.now();
                save();
            }
            return inc;
        }

        function updateHeader() {
            collect();
            document.getElementById('bal').textContent = data.bal.toFixed(1);
            document.getElementById('rate').textContent = getRate().toFixed(2);
        }

        function showTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            let html = '';
            switch(tab) {
                case 'heroes':
                    html = '<h3>🏰 Герои</h3>';
                    heroes.forEach((h,i) => {
                        let owned = data.heroes.includes(i);
                        html += `<div class="hero ${owned ? 'owned' : ''}">
                            <div class="hero-info">
                                <div class="hero-name">${h.n}</div>
                                <div class="hero-inc">⚡ +${h.i}💎/час</div>
                                ${!owned ? `<div class="hero-price">💰 ${h.p}💎</div>` : ''}
                            </div>
                            ${owned ? '<button class="btn btn-owned">✅</button>' : 
                              `<button class="btn btn-buy" onclick="buy(${i})">Купить</button>`}
                        </div>`;
                    });
                    break;
                case 'tasks':
                    html = '<h3>📋 Задания</h3><p style="color:#8b949e">Задания добавляет админ бота</p>';
                    break;
                case 'refs':
                    html = `<h3>👥 Рефералы</h3>
                        <div class="link-box">🔗 https://t.me/YOUR_BOT?start=12345</div>
                        <p>👤 Рефералов: ${data.refs.length}</p>
                        <p class="info">💎 +1 за 5 заданий реферала</p>
                        <p class="info">💸 +5% от пополнений</p>`;
                    break;
                case 'bonus':
                    let canBonus = Date.now() - data.btime > 86400000;
                    html = `<h3>🎁 Бонус</h3>
                        <p>Ежедневный бонус: +0.5💎</p>
                        <button class="btn-action" ${canBonus ? '' : 'disabled'} 
                            onclick="getBonus()">${canBonus ? '🎁 Забрать бонус' : '⏳ Уже получен'}</button>`;
                    break;
                case 'depo':
                    html = `<h3>💎 Пополнение</h3>
                        <p>📌 Курс: 1 TON = 100💎</p>
                        <p>📌 Кошелёк:</p>
                        <div class="link-box">UQDmNY1TIMIgnALOpAyJ4_XO2uroUNLFVRwGie5AEwzccaps</div>
                        <p class="warning">⚠️ В комментарии укажите ваш ID!</p>`;
                    break;
                case 'wd':
                    html = `<h3>💸 Вывод</h3>
                        <p>📌 Курс: 100💎 = 1 TON</p>
                        <p>📌 Минимум: 50💎</p>
                        <input class="input" id="wdAmount" type="number" placeholder="Сумма 💎">
                        <input class="input" id="wdWallet" type="text" placeholder="TON кошелёк">
                        <button class="btn-action" onclick="withdraw()">💸 Вывести</button>`;
                    break;
            }
            document.getElementById('content').innerHTML = html;
        }

        function buy(i) {
            if (data.heroes.includes(i)) return alert('Уже куплен!');
            if (data.bal < heroes[i].p) return alert('Недостаточно 💎!');
            data.bal -= heroes[i].p;
            data.heroes.push(i);
            data.htime = Date.now();
            save();
            updateHeader();
            showTab('heroes');
        }

        function getBonus() {
            if (Date.now() - data.btime < 86400000) return alert('Уже получен!');
            data.bal += 0.5;
            data.btime = Date.now();
            save();
            updateHeader();
            showTab('bonus');
            alert('✅ +0.5💎!');
        }

        function withdraw() {
            let amt = parseFloat(document.getElementById('wdAmount').value);
            let wallet = document.getElementById('wdWallet').value;
            if (!amt || amt < 50 || amt > data.bal) return alert('❌ Неверная сумма!');
            if (!wallet) return alert('❌ Введите кошелёк!');
            let fee = amt * 0.05;
            let ton = (amt - fee) / 100;
            data.bal -= amt;
            save();
            updateHeader();
            alert('✅ Заявка на ' + ton.toFixed(2) + ' TON отправлена!');
        }

        // Инициализация
        updateHeader();
        document.getElementById('tabs').innerHTML = `
            <div class="tab active" onclick="showTab('heroes')">🏰</div>
            <div class="tab" onclick="showTab('tasks')">📋</div>
            <div class="tab" onclick="showTab('refs')">👥</div>
            <div class="tab" onclick="showTab('bonus')">🎁</div>
            <div class="tab" onclick="showTab('depo')">💎</div>
            <div class="tab" onclick="showTab('wd')">💸</div>
        `;
        showTab('heroes');
    </script>
</body>
</html>
