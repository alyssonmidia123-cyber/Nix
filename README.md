<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NIX - A Dona da Noite</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #050505;
            --card-bg: #121212;
            --accent-color: #bc13fe;
            --secondary-accent: #ff00de;
            --text-color: #ffffff;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: 'Inter', sans-serif;
            margin: 0; padding: 20px; padding-bottom: 90px;
        }

        /* --- LOGO & HEADER --- */
        .brand { font-family: 'Orbitron', sans-serif; font-size: 26px; color: var(--accent-color); text-align: center; margin-bottom: 30px; letter-spacing: 4px; }
        
        /* --- CARD ESTILIZADO --- */
        .card {
            background: var(--card-bg); border-radius: 20px; overflow: hidden;
            margin-bottom: 20px; border: 1px solid #1a1a1a; position: relative;
        }
        .card-img { width: 100%; height: 180px; object-fit: cover; opacity: 0.8; }
        .card-info { padding: 15px; }
        .price { font-size: 22px; font-weight: bold; color: #00ff88; }
        
        /* --- BOTÃO NIX --- */
        .btn-go {
            background: linear-gradient(45deg, var(--accent-color), var(--secondary-accent));
            color: white; border: none; padding: 12px 25px; border-radius: 12px;
            font-weight: bold; cursor: pointer; width: 100%; margin-top: 10px;
            font-family: 'Orbitron'; font-size: 14px;
        }

        /* --- MODAL DE RESERVA --- */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 5000; display: none; align-items: center; justify-content: center;
        }
        .modal-content {
            background: var(--card-bg); width: 90%; border-radius: 25px; padding: 30px;
            text-align: center; border: 1px solid var(--accent-color);
        }

        /* --- FILTRO --- */
        .filter { background: #111; padding: 15px; border-radius: 15px; margin-bottom: 20px; }
        input[type=range] { width: 100%; accent-color: var(--accent-color); }
    </style>
</head>
<body>

    <div class="brand">NIX</div>

    <div class="filter">
        <div style="display:flex; justify-content:space-between; font-size: 12px; margin-bottom: 8px;">
            <span>BUSCAR POR PREÇO</span>
            <span id="p-label" style="color:var(--secondary-accent)">R$ 350</span>
        </div>
        <input type="range" id="range" min="50" max="1000" value="350" oninput="render()">
    </div>

    <div id="lista"></div>

    <div id="modal" class="modal" onclick="fechar()">
        <div class="modal-content" onclick="event.stopPropagation()">
            <h2 id="m-nome" style="margin-bottom: 5px;">Nome</h2>
            <p id="m-dist" style="color: var(--accent-color); font-size: 14px; margin-top: 0;"></p>
            
            <div style="background: #000; padding: 20px; border-radius: 15px; margin: 20px 0;">
                <p style="font-size: 14px;">⚡ <strong>RESERVA EXPRESSA</strong></p>
                <p style="font-size: 12px; color: #888;">Sua vaga está garantida por 20 min. O pagamento é feito diretamente no motel.</p>
            </div>

            <button class="btn-go" onclick="confirmar()">CONFIRMAR MEU GO</button>
            <p onclick="fechar()" style="margin-top: 20px; font-size: 12px; color: #555;">Cancelar</p>
        </div>
    </div>

    <script>
        const moteis = [
            { id: 0, nome: "Opium Lux", preco: 189, lat: -23.519, lng: -46.664, img: "https://images.unsplash.com/photo-1618221195710-dd6b41faaea6?w=400" },
            { id: 1, nome: "Lina Concept", preco: 130, lat: -23.548, lng: -46.591, img: "https://images.unsplash.com/photo-1590490360182-c33d57733427?w=400" },
            { id: 2, nome: "Nix Suite", preco: 450, lat: -23.485, lng: -46.551, img: "https://images.unsplash.com/photo-1584132967334-10e028bd69f7?w=400" }
        ];

        function render() {
            const list = document.getElementById('lista');
            const val = document.getElementById('range').value;
            document.getElementById('p-label').innerText = `R$ ${val}`;
            list.innerHTML = "";

            moteis.filter(m => m.preco <= val).forEach(m => {
                list.innerHTML += `
                    <div class="card" onclick="abrir(${m.id})">
                        <img src="${m.img}" class="card-img">
                        <div class="card-info">
                            <h3 style="margin:0">${m.nome}</h3>
                            <div style="display:flex; justify-content:space-between; align-items:center; margin-top:10px">
                                <span class="price">R$ ${m.preco}</span>
                                <button class="btn-go" style="width:auto; margin:0">DETALHES</button>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        function abrir(id) {
            const m = moteis[id];
            document.getElementById('m-nome').innerText = m.nome;
            document.getElementById('m-dist').innerText = "📍 Próximo a você";
            document.getElementById('modal').style.display = 'flex';
        }

        function fechar() { document.getElementById('modal').style.display = 'none'; }

        function confirmar() {
            alert("🔥 GO CONFIRMADO! Nome na lista. Dirija-se ao local e identifique-se como cliente NIX.");
            fechar();
        }

        window.onload = render;
    </script>
</body>
</html>
