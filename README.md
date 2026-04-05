<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nix - A Dona da Noite | Guia de Reservas</title>
    <style>
        /* Estilização Geral */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #050505;
            color: #ffffff;
            overflow-x: hidden;
        }

        /* Header */
        header {
            padding: 20px 5%;
            background: linear-gradient(to bottom, rgba(0,0,0,0.9), transparent);
            position: fixed;
            width: 100%;
            z-index: 100;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            letter-spacing: 5px;
            color: #9d4edd;
            text-shadow: 0 0 10px rgba(157, 78, 221, 0.5);
        }

        nav ul {
            display: flex;
            list-style: none;
            align-items: center;
        }

        nav ul li a {
            color: white;
            text-decoration: none;
            margin-left: 25px;
            font-size: 0.9rem;
            transition: 0.3s;
        }

        nav ul li a:hover {
            color: #9d4edd;
        }

        .btn-reserva {
            background: #9d4edd;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
        }

        /* Hero Section */
        .hero {
            height: 80vh;
            background: linear-gradient(rgba(0,0,0,0.7), rgba(5,5,5,1)), 
                        url('https://images.unsplash.com/photo-1514924013411-cbf25faa35bb?q=80&w=2000') no-repeat center center/cover;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 0 20px;
        }

        .hero-content h1 {
            font-size: clamp(2.5rem, 8vw, 4.5rem);
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .hero-content p {
            font-size: 1.2rem;
            margin-bottom: 40px;
            color: #ccc;
        }

        /* Barra de Busca */
        .search-bar {
            background: white;
            padding: 8px;
            border-radius: 50px;
            display: flex;
            max-width: 700px;
            margin: 0 auto;
            box-shadow: 0 0 30px rgba(157, 78, 221, 0.2);
        }

        .search-bar input {
            border: none;
            padding: 15px 25px;
            border-radius: 50px;
            flex: 1;
            outline: none;
            font-size: 1rem;
        }

        .search-bar button {
            background: #240046;
            color: white;
            border: none;
            padding: 0 35px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }

        .search-bar button:hover {
            background: #9d4edd;
        }

        /* Seção de Destaques */
        .destaques {
            padding: 60px 5%;
        }

        .container h2 {
            font-size: 2rem;
            margin-bottom: 40px;
            text-align: center;
            border-bottom: 2px solid #9d4edd;
            display: table;
            margin-left: auto;
            margin-right: auto;
            padding-bottom: 10px;
        }

        .grid-destaques {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        /* Cards */
        .card {
            background: #111;
            border-radius: 15px;
            overflow: hidden;
            transition: 0.4s;
            border: 1px solid #222;
        }

        .card:hover {
            transform: translateY(-10px);
            border-color: #9d4edd;
            box-shadow: 0 10px 40px rgba(0,0,0,0.8);
        }

        .card-img {
            height: 220px;
            background-size: cover;
            background-position: center;
            position: relative;
        }

        .tag {
            position: absolute;
            top: 15px;
            left: 15px;
            background: #9d4edd;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: bold;
            text-transform: uppercase;
        }

        .card-info {
            padding: 25px;
        }

        .card-info h3 {
            margin-bottom: 10px;
            font-size: 1.4rem;
        }

        .card-info p {
            font-size: 0.9rem;
            color: #888;
            margin-bottom: 25px;
            line-height: 1.5;
        }

        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-top: 1px solid #222;
            padding-top: 20px;
        }

        .preco {
            font-size: 1.1rem;
            font-weight: bold;
            color: #fff;
        }

        .btn-view {
            color: #9d4edd;
            text-decoration: none;
            font-size: 0.85rem;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: 0.3s;
        }

        .btn-view:hover {
            letter-spacing: 2px;
        }

        /* Mobile Adjustments */
        @media (max-width: 768px) {
            nav ul { display: none; }
            .hero-content h1 { font-size: 2.5rem; }
        }
    </style>
</head>
<body>

    <header>
        <nav>
            <div class="logo">NIX</div>
            <ul>
                <li><a href="#">Início</a></li>
                <li><a href="#">Cidades</a></li>
                <li><a href="#">Privacidade</a></li>
                <li><a href="#" class="btn-reserva">ENTRAR</a></li>
            </ul>
        </nav>
    </header>

    <section class="hero">
        <div class="hero-content">
            <h1>Nix: A Dona da Noite</h1>
            <p>Sua jornada noturna começa com discrição e sofisticação.</p>
            <div class="search-bar">
                <input type="text" placeholder="Bairro, Cidade ou Nome do Motel...">
                <button>BUSCAR</button>
            </div>
        </div>
    </section>

    <section class="destaques">
        <div class="container">
            <h2>EXPERIÊNCIAS EM DESTAQUE</h2>
            <div class="grid-destaques">
                
                <div class="card">
                    <div class="card-img" style="background-image: url('https://images.unsplash.com/photo-1618221195710-dd6b41faaea6?q=80&w=600');">
                        <span class="tag">Luxo Premium</span>
                    </div>
                    <div class="card-info">
                        <h3>Suíte Eclipse</h3>
                        <p>Hidromassagem com vista para o céu, automação via tablet e menu gourmet.</p>
                        <div class="card-footer">
                            <span class="preco">R$ 280,00</span>
                            <a href="#" class="btn-view">RESERVAR</a>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-img" style="background-image: url('https://images.unsplash.com/photo-1595526114035-0d45ed16cfbf?q=80&w=600');">
                        <span class="tag">Mais Procurada</span>
                    </div>
                    <div class="card-info">
                        <h3>Refúgio de Nix</h3>
                        <p>Iluminação em neon customizável, som de alta fidelidade e cadeira erótica.</p>
                        <div class="card-footer">
                            <span class="preco">R$ 195,00</span>
                            <a href="#" class="btn-view">RESERVAR</a>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-img" style="background-image: url('https://images.unsplash.com/photo-1584132967334-10e028bd69f7?q=80&w=600');">
                        <span class="tag">Privacidade Absoluta</span>
                    </div>
                    <div class="card-info">
                        <h3>Oásis Secreto</h3>
                        <p>Entrada e saída totalmente privativas, piscina aquecida e garagem dupla.</p>
                        <div class="card-footer">
                            <span class="preco">R$ 340,00</span>
                            <a href="#" class="btn-view">RESERVAR</a>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

</body>
</html>
