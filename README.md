<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>GoalPay Pro | Soccer & Payments</title>
    
    <!-- Fontes Estilo Gamer -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&family=Orbitron:wght@700;900&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary: #00ff88;
            --secondary: #6e00ff;
            --dark: #0b0b0e;
            --card-bg: #16161d;
            --text: #ffffff;
            --danger: #ff4d4d;
            --gold: #ffcc00;
            --mp-blue: #009ee3;
        }

        * { box-sizing: border-box; font-family: 'Poppins', sans-serif; }
        
        body { 
            background: var(--dark); 
            color: var(--text); 
            margin: 0; 
            display: flex; 
            justify-content: center;
            background-image: radial-gradient(circle at top right, #1a1a2e, #0b0b0e);
        }

        /* Container Principal */
        .app-shell {
            width: 100%;
            max-width: 430px;
            background: var(--card-bg);
            min-height: 100vh;
            position: relative;
            box-shadow: 0 0 50px rgba(0,0,0,0.8);
            display: flex;
            flex-direction: column;
        }

        /* Header Dinâmico */
        .header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.9)), url('https://wallpaperaccess.com/full/1335757.jpg');
            background-size: cover;
            padding: 25px 20px;
            border-bottom: 2px solid var(--primary);
            text-align: center;
        }

        .brand { font-family: 'Orbitron', sans-serif; font-size: 22px; color: var(--primary); letter-spacing: 2px; }
        
        .balance-container { margin-top: 15px; }
        .bal-label { font-size: 11px; text-transform: uppercase; opacity: 0.7; letter-spacing: 1px; }
        .bal-value { font-family: 'Orbitron', sans-serif; font-size: 34px; color: #fff; text-shadow: 0 0 10px var(--primary); }

        /* Navegação */
        .nav-bar {
            display: flex;
            background: #000;
            padding: 5px;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .nav-item {
            flex: 1;
            padding: 12px 5px;
            border: none;
            background: none;
            color: #666;
            font-size: 10px;
            font-weight: 800;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.3s;
        }
        .nav-item.active { color: var(--primary); border-bottom: 3px solid var(--primary); }

        /* Conteúdo */
        .main-content { padding: 20px; flex-grow: 1; }
        .view { display: none; animation: slideUp 0.3s ease-out; }
        .view.active { display: block; }
        
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Cartões e UI */
        .card { 
            background: rgba(255,255,255,0.05); 
            border-radius: 15px; 
            padding: 15px; 
            margin-bottom: 15px; 
            border: 1px solid rgba(255,255,255,0.1); 
        }

        .btn {
            width: 100%;
            padding: 14px;
            border-radius: 10px;
            border: none;
            font-weight: 800;
            text-transform: uppercase;
            cursor: pointer;
            transition: 0.2s;
            margin-bottom: 10px;
        }
        .btn-pix { background: var(--primary); color: #000; }
        .btn-p2p { background: var(--secondary); color: #fff; }
        .btn:active { transform: scale(0.98); }

        input {
            width: 100%;
            padding: 12px;
            background: #000;
            border: 1px solid #333;
            color: #fff;
            border-radius: 8px;
            margin-bottom: 15px;
            font-size: 16px;
        }

        /* P2P Team Grid */
        .team-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin: 15px 0; }
        .team-box { 
            background: #111; 
            padding: 10px; 
            border-radius: 10px; 
            text-align: center; 
            border: 2px solid transparent; 
            cursor: pointer;
        }
        .team-box.selected { border-color: var(--primary); background: rgba(0,255,136,0.1); }
        .team-box img { width: 40px; height: 40px; object-fit: contain; }
        .team-box span { display: block; font-size: 10px; margin-top: 5px; font-weight: bold; }

        /* Simulação de Partida */
        .match-screen {
            display: none;
            background: linear-gradient(rgba(0,0,0,0.9), rgba(0,0,0,0.9)), url('https://wallpapercave.com/wp/wp10503027.jpg');
            background-size: cover;
            border-radius: 20px;
            padding: 25px;
            text-align: center;
            border: 2px solid var(--primary);
        }
        .scoreboard { font-family: 'Orbitron', sans-serif; font-size: 40px; margin: 20px 0; color: var(--primary); }
        .live-tag { background: red; padding: 2px 8px; border-radius: 5px; font-size: 10px; font-weight: bold; animation: blink 1s infinite; }
        @keyframes blink { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }

        /* Marketing Banner */
        .ad-card {
            background: linear-gradient(90deg, #1e1e26, #2a2a35);
            border-left: 4px solid var(--gold);
            padding: 12px;
            display: flex;
            align-items: center;
            gap: 15px;
            cursor: pointer;
        }

        /* History */
        .hist-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #222;
            font-size: 12px;
        }
        .val-plus { color: var(--primary); font-weight: bold; }
        .val-minus { color: var(--danger); font-weight: bold; }

    </style>
</head>
<body>

<div class="app-shell">
    
    <!-- HEADER -->
    <div class="header">
        <div class="brand">GOALPAY PRO ⚽</div>
        <div class="balance-container">
            <div class="bal-label">Saldo em Carteira</div>
            <div class="bal-value" id="display-balance">R$ 0,00</div>
        </div>
    </div>

    <!-- TABS -->
    <div class="nav-bar">
        <button class="nav-item active" onclick="showTab('wallet', this)">Wallet</button>
        <button class="nav-item" onclick="showTab('p2p', this)">P2P Match</button>
        <button class="nav-item" onclick="showTab('fifa', this)">FIFA Connect</button>
        <button class="nav-item" onclick="showTab('history', this)">Extrato</button>
    </div>

    <div class="main-content">
        
        <!-- VIEW: WALLET -->
        <div id="view-wallet" class="view active">
            <div class="card">
                <h3 style="margin-top:0">⚡ Depósito Pix</h3>
                <p style="font-size:12px; opacity:0.7">Adicione saldo instantaneamente para jogar e apostar.</p>
                <input type="number" id="dep-amount" placeholder="Valor R$ 0,00" min="1">
                <button class="btn btn-pix" onclick="handleDeposit()">Gerar QR Code Pix</button>
            </div>

            <div class="ad-card" onclick="alert('Redirecionando para Pack Opening...')">
                <div style="font-size: 24px;">🎁</div>
                <div>
                    <div style="font-weight: 800; font-size: 13px;">PACK OURO FIFA 24</div>
                    <div style="font-size: 10px; color: var(--gold);">Ganhe 1 jogador 85+ agora!</div>
                </div>
            </div>
        </div>

        <!-- VIEW: P2P -->
        <div id="view-p2p" class="view">
            <div id="p2p-lobby">
                <h3 style="margin-top:0; color:var(--primary)">⚔️ Desafio P2P</h3>
                <p style="font-size:12px">Vença a CPU ou Jogadores e ganhe 90% da aposta.</p>
                
                <label style="font-size:11px; font-weight:bold">VALOR DA APOSTA (R$)</label>
                <input type="number" id="bet-amount" value="10" min="2">

                <label style="font-size:11px; font-weight:bold">ESCOLHA SEU TIME</label>
                <div class="team-grid">
                    <div class="team-box" onclick="selectTeam('Flamengo', this)">
                        <img src="https://logodetimes.com/times/flamengo/logo-flamengo-256.png">
                        <span>FLA</span>
                    </div>
                    <div class="team-box" onclick="selectTeam('Real Madrid', this)">
                        <img src="https://logodetimes.com/times/real-madrid/logo-real-madrid-256.png">
                        <span>RMA</span>
                    </div>
                    <div class="team-box" onclick="selectTeam('Man. City', this)">
                        <img src="https://logodetimes.com/times/manchester-city/logo-manchester-city-256.png">
                        <span>MCI</span>
                    </div>
                </div>

                <button class="btn btn-p2p" id="btn-start" onclick="startMatch()" disabled>Buscar Adversário</button>
            </div>

            <!-- Tela de Partida -->
            <div id="p2p-match" class="match-screen">
                <div class="live-tag">AO VIVO</div>
                <div id="match-timer" style="margin-top:10px">00:00</div>
                <div class="scoreboard">
                    <span id="score-home">0</span> : <span id="score-away">0</span>
                </div>
                <div id="match-events" style="font-size:12px; color:var(--primary); font-style:italic">Aquecendo jogadores...</div>
            </div>
        </div>

        <!-- VIEW: FIFA -->
        <div id="view-fifa" class="view">
            <div class="card" style="background:#fff; color:#000">
                <center><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/aa/EA_Sports_logo.svg/1200px-EA_Sports_logo.svg.png" width="50"></center>
                <h3 style="text-align:center; margin:10px 0">Login EA Sports</h3>
                <input type="email" placeholder="E-mail FIFA/EA" style="background:#f0f0f0; color:#000">
                <input type="password" placeholder="Senha da Conta" style="background:#f0f0f0; color:#000">
                <button class="btn" style="background:#000; color:#fff" onclick="alert('Sincronizando saldo com FIFA 24...')">Conectar Conta</button>
            </div>
        </div>

        <!-- VIEW: HISTORY -->
        <div id="view-history" class="view">
            <h3 style="margin-top:0">📊 Meu Extrato</h3>
            <div id="history-list">
                <!-- Inserido via JS -->
            </div>
        </div>

    </div>
</div>

<script>
    // --- ESTADO GLOBAL (SALVO NO BROWSER) ---
    let userState = {
        balance: 50.00,
        history: [],
        selectedTeam: null
    };

    // --- INICIALIZAÇÃO ---
    function init() {
        const saved = localStorage.getItem('goalpay_data');
        if (saved) userState = JSON.parse(saved);
        updateUI();
    }

    function updateUI() {
        document.getElementById('display-balance').innerText = `R$ ${userState.balance.toFixed(2)}`;
        
        // Atualizar Lista de Histórico
        const histContainer = document.getElementById('history-list');
        histContainer.innerHTML = userState.history.length ? '' : '<p style="font-size:12px; opacity:0.5">Sem movimentações.</p>';
        
        userState.history.slice().reverse().forEach(item => {
            const div = document.createElement('div');
            div.className = 'hist-item';
            div.innerHTML = `
                <span>${item.desc}</span>
                <span class="${item.amt > 0 ? 'val-plus' : 'val-minus'}">
                    ${item.amt > 0 ? '+' : ''} R$ ${item.amt.toFixed(2)}
                </span>
            `;
            histContainer.appendChild(div);
        });

        localStorage.setItem('goalpay_data', JSON.stringify(userState));
    }

    function logTransaction(desc, amt) {
        userState.balance += amt;
        userState.history.push({ desc, amt, time: new Date() });
        updateUI();
    }

    // --- NAVEGAÇÃO ---
    function showTab(tabId, btn) {
        document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        document.getElementById(`view-${tabId}`).classList.add('active');
        btn.classList.add('active');
    }

    // --- CARTEIRA ---
    function handleDeposit() {
        const amt = parseFloat(document.getElementById('dep-amount').value);
        if (isNaN(amt) || amt <= 0) return alert("Insira um valor válido.");
        
        alert(`PIX GERADO!\n\nValor: R$ ${amt.toFixed(2)}\n\n(Simulando confirmação do Mercado Pago...)`);
        
        setTimeout(() => {
            logTransaction("Depósito via Pix", amt);
            alert("Pagamento Confirmado! Saldo Atualizado.");
            document.getElementById('dep-amount').value = '';
        }, 2000);
    }

    // --- P2P MATCH ---
    function selectTeam(name, el) {
        userState.selectedTeam = name;
        document.querySelectorAll('.team-box').forEach(b => b.classList.remove('selected'));
        el.classList.add('selected');
        document.getElementById('btn-start').disabled = false;
        document.getElementById('btn-start').innerText = `DESAFIAR COM ${name.toUpperCase()}`;
    }

    function startMatch() {
        const stake = parseFloat(document.getElementById('bet-amount').value);
        if (userState.balance < stake) return alert("Saldo insuficiente!");

        // Retirar aposta (Escrow)
        logTransaction(`Aposta P2P: ${userState.selectedTeam}`, -stake);

        // Mudar Tela
        document.getElementById('p2p-lobby').style.display = 'none';
        document.getElementById('p2p-match').style.display = 'block';

        let clock = 0;
        let homeScore = 0;
        let awayScore = 0;
        const eventText = document.getElementById('match-events');

        const matchInterval = setInterval(() => {
            clock += 10;
            document.getElementById('match-timer').innerText = `Tempo: ${clock}'`;

            // Lógica de Gols (Sorte)
            if (Math.random() > 0.8) {
                if (Math.random() > 0.4) {
                    homeScore++;
                    document.getElementById('score-home').innerText = homeScore;
                    eventText.innerText = `⚽ GOL DO ${userState.selectedTeam.toUpperCase()}!`;
                } else {
                    awayScore++;
                    document.getElementById('score-away').innerText = awayScore;
                    eventText.innerText = `⚽ GOL DO ADVERSÁRIO!`;
                }
            } else {
                eventText.innerText = "Partida disputada no meio de campo...";
            }

            if (clock >= 90) {
                clearInterval(matchInterval);
                finishMatch(homeScore, awayScore, stake);
            }
        }, 800);
    }

    function finishMatch(h, a, stake) {
        let result = "";
        if (h > a) {
            const prize = stake * 1.9; // 10% de taxa da casa
            logTransaction(`Vitória P2P: ${userState.selectedTeam}`, prize);
            result = `🏆 VITÓRIA! Você ganhou R$ ${prize.toFixed(2)}`;
        } else if (h === a) {
            logTransaction(`Empate P2P: Reembolso`, stake);
            result = "🤝 EMPATE! Valor devolvido.";
        } else {
            result = "❌ DERROTA! Você perdeu a aposta.";
        }

        setTimeout(() => {
            alert(result);
            document.getElementById('p2p-lobby').style.display = 'block';
            document.getElementById('p2p-match').style.display = 'none';
            document.getElementById('score-home').innerText = '0';
            document.getElementById('score-away').innerText = '0';
        }, 1500);
    }

    // Start App
    init();

</script>

</body>
</html>
