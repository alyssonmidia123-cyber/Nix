<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="theme-color" content="#050505">
    <title>NIX - A Dona da Noite</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #050505;
            --card-bg: #121212;
            --accent-color: #bc13fe;
            --secondary-accent: #ff00de;
            --text-color: #ffffff;
            --success: #00ff88;
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: 'Inter', sans-serif;
            margin: 0; padding: 20px; padding-bottom: 100px;
            overflow-x: hidden;
        }

        /* --- SPLASH SCREEN --- */
        #splash {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #000; z-index: 9999; display: flex;
            align-items: center; justify-content: center; text-align: center;
            transition: opacity 0.8s ease;
        }
        .logo-nix {
            font-family: 'Orbitron', sans-serif; font-size: 60px;
            background: linear-gradient(to right, var(--accent-color), var(--secondary-accent));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(188, 19, 254, 0.5);
        }

        /* --- UI ELEMENTS --- */
        header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; }
        .brand { font-family: 'Orbitron', sans-serif; font-size: 22px; color: var(--accent-color); letter-spacing: 2px; }
        
        .filter-box { 
            background: var(--card-bg); padding: 15px; border-radius: 20px; 
            margin-bottom: 25px; border: 1px solid #222;
        }
        input[type=range] { width: 100%; accent-color: var(--secondary-accent); margin-top: 10px; }

        /* --- CARDS --- */
        .card {
            background: var(--card-bg); border-radius: 24px; overflow: hidden;
            margin-bottom: 20px; border: 1px solid #1a1a1a; position: relative;
        }
        .card-img { width: 100%; height: 200px; object-fit: cover; filter: brightness(0.8); }
        .card-badge {
            position: absolute; top: 15px; right: 15px;
            background: rgba(0,0,0,0.7); padding: 5px 12px; border-radius: 10px;
            font-size: 12px; border: 1px solid var(--accent-color);
        }
        .card-info { padding: 18px; }
        .price-tag { font-size: 22px; font-weight: bold; color: var(--success); }

        /* --- BUTTONS --- */
        .btn-main {
            background: linear-gradient(45deg, var(--accent-color), var(--secondary-accent));
            color: white; border: none; padding: 12px 25px; border-radius: 14px;
            font-weight: 600; cursor: pointer; font-family: 'Inter';
        }

        /* --- MODALS --- */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 5000; display: none; align-items: flex-end;
        }
        .modal-content {
            background: var(--card-bg); width: 100%; max-height: 90%;
            border-radius: 30px 30px 0 0; padding: 25px; overflow-y: auto;
            border-top: 2px solid var(--accent-color);
        }

        /* --- NAV BAR --- */
        nav {
            position: fixed; bottom: 0; left: 0; width: 100%; height: 75px;
            background: rgba(5,5,5,0.95); backdrop-filter: blur(15px);
            display: flex; justify-content: space-around; align-items: center;
            border-top: 1px solid #222; z-index: 4000;
        }
        .nav-icon { font-size: 24px; color: #555; cursor: pointer; transition: 0.3s; }
        .nav-active { color: var(--accent-color); filter: drop-shadow(0 0 8px var(--accent-color)); }

        /* --- ADMIN/OWNER STYLES --- */
        .admin-input { 
            width: 100%; padding: 15px; background: #000; border: 1px solid #333; 
            border-radius: 12px; color: white; margin: 10px 0; 
        }
    </style>
</head>
<body>

    <div id="splash">
        <div>
            <div class="logo-nix">NIX</div>
            <p style="letter-spacing: 3px; color: #666; font-size: 12px;">A DONA DA NOITE</p>
        </div>
    </div>

    <header>
        <div class="brand">NIX</div>
        <div onclick="abrirAdmin()" style="cursor:pointer">⚙️</div>
    </header>

    <div class="filter-box">
        <div style="display:flex; justify-content:space-between">
            <span>Preço Máximo</span>
            <span id="price-label" style="color:var(--secondary-accent)">R$ 300</span>
        </div>
        <input type="range" id="price-range" min="60" max="800" value="300" oninput="atualizarFiltro()">
    </div>

    <div id="lista-moteis"></div>

    <div id="modal-reserva" class="modal" onclick="fecharModal()">
        <div class="modal-content" onclick="event.stopPropagation()">
            <h2 id="m-nome" style="margin-top:0">Nome do Motel</h2>
            <p id="m-dist" style="color:var(--accent-color)"></p>
            <hr style="border:0; border-top:1px solid #222; margin:20px 0">
            <h3>Pague via PIX para Garantir</h3>
            <div style="background:#000; padding:20px; border-radius:15px; text-align:center; border:1px dashed var(--success)">
                <p style="font-size:12px; color:#888">Copie a chave abaixo:</p>
                <code style="color:var(--success); word-break: break-all;">00020126580014br.gov.bcb.pix0136nix-pagamentos-transacionais-oficial</code>
            </div>
            <button class="btn-main" style="width:100%; margin-top:20px; padding:18px" onclick="finalizarGo()">JÁ PAGUEI, QUERO MEU GO!</button>
        </div>
    </div>

    <div id="modal-admin" class="modal">
        <div class="modal-content" style="height:80%">
            <h2 style="font-family:Orbitron; color:var(--accent-color)">NIX CONTROL</h2>
            <p>Gerenciar Unidade: **Opium Premium**</p>
            <label>Novo Preço da Suíte (R$):</label>
            <input type="number" id="adm-preco" class="admin-input" placeholder="150.00">
            <label>Status Atual:</label>
            <select id="adm-status" class="admin-input">
                <option value="disponivel">🟢 Disponível agora</option>
                <option value="lotado">🔴 Lotado</option>
            </select>
            <button class="btn-main" style="width:100%; margin-top:20px" onclick="salvarAdmin()">ATUALIZAR PLATAFORMA</button>
            <button onclick="document.getElementById('modal-admin').style.display='none'" style="background:none; border:none; color:#555; width:100%; margin-top:15px">Sair</button>
        </div>
    </div>

    <nav>
        <div class="nav-icon nav-active">🔍</div>
        <div class="nav-icon">🔥</div>
        <div class="nav-icon">❤️</div>
        <div class="nav-icon" onclick="alert('Histórico de Noites em breve!')">🕒</div>
    </nav>

    <script>
        // Dados Iniciais (Simulando Banco de Dados)
        let moteis = [
            { id: 0, nome: "Opium Premium", lat: -23.519, lng: -46.664, preco: 189, img: "https://images.unsplash.com/photo-1618221195710-dd6b41faaea6?auto=format&fit=crop&w=500" },
            { id: 1, nome: "Lina Concept", lat: -23.548, lng: -46.591, preco: 120, img: "https://images.unsplash.com/photo-1584132967334-10e028bd69f7?auto=format&fit=crop&w=500" },
            { id: 2, nome: "Mint Privé", lat: -23.485, lng: -46.551, preco: 250, img: "https://images.unsplash.com/photo-1590490360182-c33d57733427?auto=format&fit=crop&w=500" }
        ];

        let userPos = { lat: -23.5505, lng: -46.6333 }; // Default SP

        // Inicialização
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => document.getElementById('splash').style.display = 'none', 800);
            }, 2500);

            if(navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(p => {
                    userPos = { lat: p.coords.latitude, lng: p.coords.longitude };
                    render();
                });
            }
            render();
        };

        // Cálculo de Distância Real
        function getDist(lat1, lon1, lat2, lon2) {
            const R = 6371;
            const dLat = (lat2-lat1) * Math.PI/180;
            const dLon = (lon2-lon1) * Math.PI/180;
            const a = Math.sin(dLat/2)**2 + Math.cos(lat1*Math.PI/180)*Math.cos(lat2*Math.PI/180)*Math.sin(dLon/2)**2;
            return (R * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a))).toFixed(1);
        }

        function render() {
            const lista = document.getElementById('lista-moteis');
            const maxP = document.getElementById('price-range').value;
            document.getElementById('price-label').innerText = `R$ ${maxP}`;
            
            lista.innerHTML = "";
            moteis.filter(m => m.preco <= maxP).forEach(m => {
                const d = getDist(userPos.lat, userPos.lng, m.lat, m.lng);
                lista.innerHTML += `
                    <div class="card" onclick="abrirReserva(${m.id}, ${d})">
                        <img src="${m.img}" class="card-img">
                        <div class="card-badge">📍 ${d} km</div>
                        <div class="card-info">
                            <h3 style="margin:0">${m.nome}</h3>
                            <div style="display:flex; justify-content:space-between; align-items:center; margin-top:10px">
                                <span class="price-tag">R$ ${m.preco}</span>
                                <button class="btn-main">RESERVAR</button>
                            </div>
                        </div>
                    </div>`;
            });
        }

        function atualizarFiltro() { render(); }

        function abrirReserva(id, d) {
            const m = moteis.find(x => x.id == id);
            document.getElementById('m-nome').innerText = m.nome;
            document.getElementById('m-dist').innerText = `Você está a ${d} km desta experiência.`;
            document.getElementById('modal-reserva').style.display = 'flex';
        }

        function fecharModal() { document.getElementById('modal-reserva').style.display = 'none'; }

        function finalizarGo() {
            alert("🔥 PAGAMENTO RECEBIDO! Sua entrada foi liberada via GPS. Mostre esta tela na recepção.");
            fecharModal();
        }

        // Funções Admin
        function abrirAdmin() { document.getElementById('modal-admin').style.display = 'flex'; }
        
        function salvarAdmin() {
            const p = document.getElementById('adm-preco').value;
            if(p) {
                moteis[0].preco = parseInt(p);
                render();
                alert("NIX: Preço atualizado no app dos usuários!");
                document.getElementById('modal-admin').style.display = 'none';
            }
        }
    </script>
</body>
</html>
