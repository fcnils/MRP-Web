# MRP-Web<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>München RP (MRP) - Offizielles Webportal & Admin-Dashboard</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --bg-color: #06040d;
            --card-bg: rgba(18, 11, 31, 0.85);
            --border-glow: rgba(180, 0, 255, 0.35);
            --neon-purple: #b400ff;
            --neon-cyan: #00f0ff;
            --neon-pink: #ff0055;
            --discord-blue: #5865f2;
            --tiktok-pink: #fe2c55;
            --instagram-orange: #f58529;
            --text-main: #f0eafb;
            --text-muted: #a395c4;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(180, 0, 255, 0.18) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(0, 240, 255, 0.15) 0%, transparent 40%),
                linear-gradient(to bottom, rgba(6, 4, 13, 0.88), rgba(6, 4, 13, 0.96)),
                url('https://images.unsplash.com/photo-1519501025264-65ba15a82390?auto=format&fit=crop&w=1920&q=80');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background: rgba(10, 6, 20, 0.9);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border-glow);
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 20px rgba(0,0,0,0.5);
        }

        .brand-logo {
            font-size: 1.8rem;
            font-weight: 900;
            color: #fff;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 10px var(--neon-purple), 0 0 20px var(--neon-purple);
        }

        .brand-subtitle {
            font-size: 0.85rem;
            color: var(--neon-cyan);
            letter-spacing: 1px;
        }

        nav {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(180, 0, 255, 0.2);
            color: var(--text-main);
            padding: 10px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .nav-btn:hover, .nav-btn.active {
            background: rgba(180, 0, 255, 0.25);
            border-color: var(--neon-purple);
            box-shadow: 0 0 15px rgba(180, 0, 255, 0.5);
            color: #fff;
            transform: translateY(-2px);
        }

        .nav-btn.admin-nav {
            border-color: var(--neon-pink);
            background: rgba(255, 0, 85, 0.1);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 30px 20px;
            flex-grow: 1;
            width: 100%;
        }

        .hero-section {
            background: linear-gradient(180deg, rgba(18, 11, 31, 0.7) 0%, rgba(6, 4, 13, 0.9) 100%), 
                        url('https://images.unsplash.com/photo-1595867818082-083862f3d630?auto=format&fit=crop&w=1600&q=80');
            background-size: cover;
            background-position: center;
            border: 1px solid var(--border-glow);
            border-radius: 16px;
            padding: 50px 30px;
            text-align: center;
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
            box-shadow: 0 0 35px rgba(180, 0, 255, 0.25);
        }

        .hero-title {
            font-size: 3rem;
            font-weight: 900;
            margin-bottom: 12px;
            background: linear-gradient(135deg, #fff 0%, var(--neon-purple) 50%, var(--neon-cyan) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .hero-desc {
            color: var(--text-main);
            font-size: 1.15rem;
            max-width: 750px;
            margin: 0 auto 25px auto;
            line-height: 1.5;
        }

        .cta-btn {
            display: inline-flex;
            align-items: center;
            gap: 12px;
            background: linear-gradient(135deg, var(--discord-blue), #404EED);
            color: white;
            font-size: 1.15rem;
            font-weight: 700;
            padding: 14px 32px;
            border-radius: 12px;
            text-decoration: none;
            box-shadow: 0 0 20px rgba(88, 101, 242, 0.6);
            transition: all 0.3s ease;
        }

        .cta-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(88, 101, 242, 0.9);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 18px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            backdrop-filter: blur(8px);
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--neon-cyan);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 800;
            color: #fff;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-left: 4px solid var(--neon-purple);
            padding-left: 12px;
        }

        .landmark-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 20px;
            margin-bottom: 35px;
        }

        .landmark-card {
            background: var(--card-bg);
            border: 1px solid rgba(180, 0, 255, 0.2);
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .landmark-card:hover {
            transform: translateY(-5px);
            border-color: var(--neon-cyan);
            box-shadow: 0 5px 20px rgba(0, 240, 255, 0.3);
        }

        .landmark-img {
            height: 150px;
            width: 100%;
            background-size: cover;
            background-position: center;
            border-bottom: 1px solid rgba(180, 0, 255, 0.2);
        }

        .landmark-info {
            padding: 15px;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .landmark-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: #fff;
            margin-bottom: 5px;
        }

        .landmark-desc {
            font-size: 0.85rem;
            color: var(--text-muted);
            line-height: 1.4;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .rules-container {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 16px;
            padding: 30px;
            backdrop-filter: blur(10px);
        }

        .rules-button-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
        }

        .rule-btn {
            background: #5865f2;
            color: #ffffff;
            border: none;
            padding: 12px 22px;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.25s ease;
            display: inline-flex;
            align-items: center;
            gap: 10px;
        }

        .rule-btn:hover {
            background: #4752c4;
            transform: translateY(-2px);
        }

        .rule-btn.active {
            background: #3c45a5;
            border: 2px solid #fff;
        }

        .rule-display-box {
            background: rgba(10, 6, 20, 0.8);
            border: 1px solid rgba(180, 0, 255, 0.3);
            border-radius: 12px;
            padding: 25px;
            color: var(--text-main);
            min-height: 250px;
        }

        .rule-display-box h2 {
            color: var(--neon-cyan);
            margin-bottom: 15px;
            font-size: 1.5rem;
        }

        .rule-display-box ul {
            list-style: none;
            padding-left: 0;
        }

        .rule-display-box li {
            position: relative;
            padding-left: 25px;
            margin-bottom: 12px;
            line-height: 1.5;
            color: #e2d9f3;
        }

        .rule-display-box li::before {
            content: "➔";
            position: absolute;
            left: 0;
            color: var(--neon-pink);
            font-weight: bold;
        }

        .faction-selection-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .faction-big-btn {
            background: var(--card-bg);
            border: 2px solid var(--border-glow);
            border-radius: 16px;
            padding: 35px 25px;
            text-align: center;
            cursor: pointer;
            transition: all 0.4s ease;
            backdrop-filter: blur(10px);
        }

        .faction-big-btn:hover {
            transform: translateY(-6px);
        }

        .faction-big-btn.polizei.active {
            border-color: var(--neon-cyan);
            box-shadow: 0 0 30px rgba(0, 240, 255, 0.35);
            background: linear-gradient(145deg, rgba(18, 11, 31, 0.9), rgba(0, 240, 255, 0.15));
        }

        .faction-big-btn.feuerwehr.active {
            border-color: var(--neon-pink);
            box-shadow: 0 0 30px rgba(255, 0, 85, 0.35);
            background: linear-gradient(145deg, rgba(18, 11, 31, 0.9), rgba(255, 0, 85, 0.15));
        }

        .faction-icon {
            font-size: 3.2rem;
            margin-bottom: 15px;
        }

        .polizei .faction-icon { color: var(--neon-cyan); }
        .feuerwehr .faction-icon { color: var(--neon-pink); }

        .faction-title {
            font-size: 1.7rem;
            font-weight: 800;
            color: #fff;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        .faction-desc {
            color: var(--text-muted);
            font-size: 0.95rem;
        }

        .faction-detail-box {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 16px;
            padding: 30px;
            backdrop-filter: blur(10px);
        }

        .server-link-card {
            background: rgba(88, 101, 242, 0.15);
            border: 1px solid rgba(88, 101, 242, 0.4);
            border-radius: 12px;
            padding: 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
        }

        .server-link-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .server-link-info i {
            font-size: 2rem;
            color: var(--discord-blue);
        }

        .discord-join-btn {
            background: var(--discord-blue);
            color: #fff;
            text-decoration: none;
            padding: 10px 22px;
            border-radius: 8px;
            font-weight: 700;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s;
        }

        .discord-join-btn:hover {
            box-shadow: 0 0 15px rgba(88, 101, 242, 0.6);
        }

        .social-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .social-card {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 16px;
            padding: 35px 25px;
            text-align: center;
            backdrop-filter: blur(10px);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
            transition: all 0.3s ease;
        }

        .social-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 0 25px rgba(180, 0, 255, 0.25);
        }

        .social-icon {
            font-size: 3.5rem;
            margin-bottom: 15px;
        }

        .social-card.tiktok .social-icon { color: var(--tiktok-pink); }
        .social-card.instagram .social-icon { 
            background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .social-title {
            font-size: 1.5rem;
            font-weight: 800;
            color: #fff;
            margin-bottom: 8px;
        }

        .social-desc {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-bottom: 25px;
            line-height: 1.4;
        }

        .social-btn {
            color: #fff;
            text-decoration: none;
            padding: 12px 28px;
            border-radius: 10px;
            font-weight: 700;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s;
            width: 100%;
            justify-content: center;
        }

        .social-card.tiktok .social-btn {
            background: var(--tiktok-pink);
            box-shadow: 0 0 15px rgba(254, 44, 85, 0.4);
        }

        .social-card.tiktok .social-btn:hover {
            box-shadow: 0 0 25px rgba(254, 44, 85, 0.8);
            transform: scale(1.02);
        }

        .social-card.instagram .social-btn {
            background: linear-gradient(45deg, #f58529, #dd2a7b, #8134af);
            box-shadow: 0 0 15px rgba(221, 42, 123, 0.4);
        }

        .social-card.instagram .social-btn:hover {
            box-shadow: 0 0 25px rgba(221, 42, 123, 0.8);
            transform: scale(1.02);
        }

        .emergency-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .emergency-card {
            background: var(--card-bg);
            border: 1px solid var(--neon-pink);
            border-radius: 16px;
            padding: 25px;
            backdrop-filter: blur(10px);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .emergency-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .emergency-icon {
            font-size: 2.2rem;
            color: var(--neon-pink);
        }

        .emergency-title {
            font-size: 1.25rem;
            font-weight: 800;
            color: #fff;
        }

        .emergency-desc {
            color: var(--text-muted);
            font-size: 0.9rem;
            line-height: 1.5;
            margin-bottom: 20px;
        }

        .emergency-btn {
            background: linear-gradient(135deg, var(--neon-pink), #c40043);
            color: white;
            text-decoration: none;
            text-align: center;
            padding: 12px 18px;
            border-radius: 10px;
            font-weight: 700;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .card {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 20px;
            backdrop-filter: blur(8px);
        }

        .card-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .card-title {
            font-size: 1.15rem;
            font-weight: 700;
            color: #fff;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .user-tag {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            background: #2b2d31;
            color: #c4b5fd;
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-top: 4px;
            margin-right: 4px;
        }

        .empty-role {
            color: var(--text-muted);
            font-size: 0.85rem;
            font-style: italic;
        }

        .form-container {
            background: var(--card-bg);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 25px;
            margin-top: 25px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 6px;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .form-control {
            width: 100%;
            padding: 10px 14px;
            background: rgba(0,0,0,0.4);
            border: 1px solid rgba(180, 0, 255, 0.3);
            border-radius: 6px;
            color: #fff;
            outline: none;
        }

        .submit-btn {
            background: linear-gradient(135deg, var(--neon-purple), #7900bd);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
        }

        .login-box {
            max-width: 450px;
            margin: 50px auto;
            background: var(--card-bg);
            border: 1px solid var(--neon-pink);
            border-radius: 16px;
            padding: 35px;
            text-align: center;
            box-shadow: 0 0 30px rgba(255, 0, 85, 0.2);
        }

        .visitor-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
            background: rgba(10, 6, 20, 0.5);
            border-radius: 8px;
            overflow: hidden;
        }

        .visitor-table th, .visitor-table td {
            padding: 12px 15px;
            text-align: left;
            font-size: 0.9rem;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        .visitor-table th {
            background: rgba(180, 0, 255, 0.2);
            color: var(--neon-cyan);
            font-weight: 700;
        }

        footer {
            background: rgba(10, 6, 20, 0.9);
            border-top: 1px solid var(--border-glow);
            text-align: center;
            padding: 20px;
            color: var(--text-muted);
            font-size: 0.85rem;
            margin-top: auto;
        }
    </style>
</head>
<body>

    <header>
        <div class="brand">
            <div class="brand-logo">MRP</div>
            <div class="brand-subtitle">MÜNCHEN ROLEPLAY VC</div>
        </div>
        <nav>
            <button class="nav-btn active" onclick="switchTab('home', event)"><i class="fa-solid fa-house"></i> Übersicht</button>
            <button class="nav-btn" onclick="switchTab('social', event)"><i class="fa-solid fa-share-nodes"></i> Social Media</button>
            <button class="nav-btn" onclick="switchTab('notfall', event)"><i class="fa-solid fa-phone-volume"></i> Notfall-Kontakte</button>
            <button class="nav-btn" onclick="switchTab('regelwerke', event)"><i class="fa-solid fa-book-bookmark"></i> Regelwerke</button>
            <button class="nav-btn" onclick="switchTab('fraktion', event)"><i class="fa-solid fa-shield-halved"></i> Fraktionen</button>
            <button class="nav-btn" onclick="switchTab('team', event)"><i class="fa-solid fa-users-gear"></i> Teamliste</button>
            <button class="nav-btn admin-nav" onclick="switchTab('admin', event)"><i class="fa-solid fa-gauge-high" style="color:var(--neon-pink);"></i> Dashboard</button>
        </nav>
    </header>

    <div class="container">

        <!-- TAB 1: ÜBERSICHT -->
        <div id="tab-home" class="tab-content active">
            <div class="hero-section">
                <h1 class="hero-title">München RP VC</h1>
                <p class="hero-desc">Tauche ein in das realistischste Voice-Roleplay Erlebnis der bayerischen Landeshauptstadt. Erlebe packende Polizeieinsätze, Notfalleinsätze und dynamisches Stadtleben.</p>
                <a href="https://discord.gg/rcEQRjn6PM" target="_blank" class="cta-btn">
                    <i class="fa-brands fa-discord"></i> Haupt-Discord Beitreten
                </a>
            </div>

            <div class="stats-grid">
                <div class="stat-card"><div class="stat-value">Pre-Launch</div><div class="stat-label">Server Status</div></div>
                <div class="stat-card"><div class="stat-value">2</div><div class="stat-label">Hauptfraktionen</div></div>
                <div class="stat-card"><div class="stat-value">Voice RP</div><div class="stat-label">Kommunikation</div></div>
                <div class="stat-card"><div class="stat-value">24/7</div><div class="stat-label">Support</div></div>
            </div>

            <div class="section-title"><i class="fa-solid fa-location-dot" style="color:var(--neon-cyan)"></i> München Roleplay Hotspots</div>

            <div class="landmark-grid">
                <!-- 1. Allianz Arena (Mit passendem Bild der Allianz Arena ausgestattet) -->
                <div class="landmark-card">
                    <div class="landmark-img" style="background-image: url('https://images.unsplash.com/photo-1489944440615-453fc2b6a9a9?auto=format&fit=crop&w=600&q=80');"></div>
                    <div class="landmark-info">
                        <div>
                            <div class="landmark-title">Allianz Arena</div>
                            <div class="landmark-desc">Großveranstaltungen, Fußballeinsätze der Polizei.</div>
                        </div>
                    </div>
                </div>

                <!-- 2. Olympiaturm & Park -->
                <div class="landmark-card">
                    <div class="landmark-img" style="background-image: url('https://images.unsplash.com/photo-1513635269975-59663e0ac1ad?auto=format&fit=crop&w=600&q=80');"></div>
                    <div class="landmark-info">
                        <div>
                            <div class="landmark-title">Olympiaturm & Park</div>
                            <div class="landmark-desc">Einsatzgebiet für SEK und Luftrettung.</div>
                        </div>
                    </div>
                </div>

                <!-- 3. Marienplatz & Neues Rathaus -->
                <div class="landmark-card">
                    <div class="landmark-img" style="background-image: url('https://images.unsplash.com/photo-1467269204594-9661b134dd2b?auto=format&fit=crop&w=600&q=80');"></div>
                    <div class="landmark-info">
                        <div>
                            <div class="landmark-title">Marienplatz & Neues Rathaus</div>
                            <div class="landmark-desc">Zentrum für Zivilleben und Streifendienst.</div>
                        </div>
                    </div>
                </div>

                <!-- 4. Heckenstaller Park -->
                <div class="landmark-card">
                    <div class="landmark-img" style="background-image: url('https://images.unsplash.com/photo-1519331379826-f10be5486c6f?auto=format&fit=crop&w=600&q=80');"></div>
                    <div class="landmark-info">
                        <div>
                            <div class="landmark-title">Heckenstaller Park & Ring</div>
                            <div class="landmark-desc">Begrünter Erholungsraum und moderner Verkehrskorridor.</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- TAB: SOCIAL MEDIA -->
        <div id="tab-social" class="tab-content">
            <div class="section-title"><i class="fa-solid fa-share-nodes" style="color:var(--neon-cyan)"></i> Unsere Social Media Kanäle</div>
            <p style="color: var(--text-muted); margin-bottom: 25px; font-size: 1rem;">Folge uns auf unseren offiziellen Kanälen, um keine Clips, Teaser, Updates und Events rund um München RP zu verpassen!</p>
            
            <div class="social-grid">
                <div class="social-card tiktok">
                    <div>
                        <i class="fa-brands fa-tiktok social-icon"></i>
                        <div class="social-title">TikTok</div>
                        <div class="social-desc">Erlebe die besten RP-Momente, Highlights und Teaser direkt in deinen Feed!</div>
                    </div>
                    <a href="https://www.tiktok.com/@mnchen.rp91?is_from_webapp=1&sender_device=pc" target="_blank" class="social-btn">
                        <i class="fa-brands fa-tiktok"></i> TikTok Besuchen
                    </a>
                </div>

                <div class="social-card instagram">
                    <div>
                        <i class="fa-brands fa-instagram social-icon"></i>
                        <div class="social-title">Instagram</div>
                        <div class="social-desc">Hinter den Kulissen, Bilder aus der Stadt und die wichtigsten News im Überblick.</div>
                    </div>
                    <a href="https://www.instagram.com/munchen.rp?utm_source=ig_web_button_share_sheet&stkn=ZDNlZDc0MzIxNw==" target="_blank" class="social-btn">
                        <i class="fa-brands fa-instagram"></i> Instagram Folgen
                    </a>
                </div>
            </div>
        </div>

        <!-- TAB 2: NOTFALL KONTAKTE -->
        <div id="tab-notfall" class="tab-content">
            <div class="section-title"><i class="fa-solid fa-triangle-exclamation" style="color:var(--neon-pink)"></i> Notfall-Support</div>
            <div class="emergency-grid">
                <div class="emergency-card">
                    <div>
                        <div class="emergency-header"><i class="fa-solid fa-ticket emergency-icon"></i><div class="emergency-title">Owner Ticket</div></div>
                        <div class="emergency-desc">Direkter Draht zur Projektleitung bei schwerwiegenden Anliegen.</div>
                    </div>
                    <a href="https://discord.gg/6Rbr3SPjm" target="_blank" class="emergency-btn"><i class="fa-solid fa-ticket"></i> Ticket Öffnen</a>
                </div>
                <div class="emergency-card">
                    <div>
                        <div class="emergency-header"><i class="fa-solid fa-user-tie emergency-icon"></i><div class="emergency-title">Projekt-Büro</div></div>
                        <div class="emergency-desc">Sprachkanal für offizielle Termine und administrative Gespräche.</div>
                    </div>
                    <a href="https://discord.gg/gHeYhCBgN" target="_blank" class="emergency-btn"><i class="fa-solid fa-door-open"></i> Büro Betreten</a>
                </div>
                <div class="emergency-card">
                    <div>
                        <div class="emergency-header"><i class="fa-solid fa-headset emergency-icon"></i><div class="emergency-title">Support Warteraum</div></div>
                        <div class="emergency-desc">Schnelle Hilfe und Klärungen durch das Team.</div>
                    </div>
                    <a href="https://discord.gg/xUrKSXVkjS" target="_blank" class="emergency-btn"><i class="fa-solid fa-clock"></i> Zum Warteraum</a>
                </div>
                <div class="emergency-card">
                    <div>
                        <div class="emergency-header"><i class="fa-brands fa-discord emergency-icon" style="color:var(--discord-blue);"></i><div class="emergency-title">Haupt-Discord</div></div>
                        <div class="emergency-desc">Tritt unserer Community bei, um vollen Zugriff auf alle Kanäle zu erhalten.</div>
                    </div>
                    <a href="https://discord.gg/rcEQRjn6PM" target="_blank" class="emergency-btn" style="background:var(--discord-blue);"><i class="fa-brands fa-discord"></i> Beitreten</a>
                </div>
            </div>
        </div>

        <!-- TAB 3: REGELWERKE -->
        <div id="tab-regelwerke" class="tab-content">
            <div class="rules-container">
                <div class="section-title"><i class="fa-solid fa-book-bookmark" style="color:var(--neon-purple)"></i> Server Regelwerke</div>
                <div class="rules-button-grid">
                    <button class="rule-btn active" onclick="showRule('rp', event)"><i class="fa-solid fa-arrow-right"></i> RP Regelwerk</button>
                    <button class="rule-btn" onclick="showRule('discord', event)"><i class="fa-solid fa-arrow-right"></i> Discord Regelwerk</button>
                    <button class="rule-btn" onclick="showRule('polizei', event)"><i class="fa-solid fa-arrow-right"></i> Polizei Regelwerk</button>
                    <button class="rule-btn" onclick="showRule('fraktion', event)"><i class="fa-solid fa-arrow-right"></i> Fraktions Regelwerk</button>
                    <button class="rule-btn" onclick="showRule('immobilien', event)"><i class="fa-solid fa-arrow-right"></i> Immobilien Regelwerk</button>
                </div>
                <div class="rule-display-box" id="rule-content-box"></div>
            </div>
        </div>

        <!-- TAB 4: FRAKTIONEN -->
        <div id="tab-fraktion" class="tab-content">
            <div class="faction-selection-grid">
                <div class="faction-big-btn polizei active" id="btn-polizei" onclick="selectFaction('polizei')">
                    <i class="fa-solid fa-building-shield faction-icon"></i>
                    <div class="faction-title">München Polizei</div>
                    <div class="faction-desc">Bundespolizei, Streifenpolizei, Verkehrspolizei, SEK, Kripo & Einsatzleitung.</div>
                </div>

                <div class="faction-big-btn feuerwehr" id="btn-feuerwehr" onclick="selectFaction('feuerwehr')">
                    <i class="fa-solid fa-fire-extinguisher faction-icon"></i>
                    <div class="faction-title">München Feuerwehr</div>
                    <div class="faction-desc">Feuerwehr, Rettungsdienst, Notarzt & Einsatzleitung.</div>
                </div>
            </div>

            <!-- DETAIL POLIZEI -->
            <div id="faction-polizei-details" class="faction-detail-box">
                <div class="server-link-card">
                    <div class="server-link-info">
                        <i class="fa-brands fa-discord"></i>
                        <div>
                            <h3 style="color:#fff; font-size:1.1rem;">Fraktions-Discord: Polizei München</h3>
                            <span style="color:var(--text-muted); font-size:0.85rem;">Offizieller Discord-Server der Polizeibehörde</span>
                        </div>
                    </div>
                    <a href="https://discord.gg/ybyWTVJn8" target="_blank" class="discord-join-btn"><i class="fa-solid fa-right-to-bracket"></i> Server Beitreten</a>
                </div>

                <div class="card-grid" id="polizei-grid">
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-shield" style="color:var(--neon-cyan)"></i> Bundespolizei</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Bundespolizei – Überwachung von Bahnhöfen, Grenzen und bundesrechtlichen Liegenschaften.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-car-side" style="color:var(--neon-cyan)"></i> Streifenpolizei</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Streifenpolizei – Allgemeine Streifenfahrten, Bürgerservice und Erstabsicherung von Notrufen.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-road" style="color:var(--neon-cyan)"></i> Verkehrspolizei</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Verkehrspolizei – Verkehrskontrollen, Radarfallen und Absicherung von Unfallstellen.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-skull-crossbones" style="color:var(--neon-pink)"></i> SEK</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Spezialeinsatzkommando – Hochrisikoeinsätze, Geiselnahmen und bewaffnete Zugriffe.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-user-secret" style="color:var(--neon-cyan)"></i> Kripo</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Kriminalpolizei – Ermittlungen, Spurensicherung und Aufklärung schwerer Straftaten.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-headphones" style="color:var(--neon-pink)"></i> Einsatzleitung</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Polizei-Einsatzleitung – Koordination von Großeinsätzen, Funk- und Lagedienst.</p>
                    </div>
                </div>

                <div class="form-container" id="form-polizei-container" style="display:none;">
                    <h3 style="margin-bottom: 15px; color:#fff;"><i class="fa-solid fa-plus-circle"></i> Polizei-Abteilung hinzufügen (Admin)</h3>
                    <div class="form-group"><label>Name</label><input type="text" id="pol-name" class="form-control"></div>
                    <div class="form-group"><label>Beschreibung</label><input type="text" id="pol-status" class="form-control"></div>
                    <button class="submit-btn" onclick="addFactionPost('polizei')">Hinzufügen</button>
                </div>
            </div>

            <!-- DETAIL FEUERWEHR -->
            <div id="faction-feuerwehr-details" class="faction-detail-box" style="display: none;">
                <div class="server-link-card">
                    <div class="server-link-info">
                        <i class="fa-brands fa-discord"></i>
                        <div>
                            <h3 style="color:#fff; font-size:1.1rem;">Fraktions-Discord: Feuerwehr & RD München</h3>
                            <span style="color:var(--text-muted); font-size:0.85rem;">Offizieller Discord-Server der Rettungskräfte</span>
                        </div>
                    </div>
                    <a href="https://discord.gg/cQYqbgStP" target="_blank" class="discord-join-btn" style="background:#ff0055;"><i class="fa-solid fa-right-to-bracket"></i> Server Beitreten</a>
                </div>

                <div class="card-grid" id="feuerwehr-grid">
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-fire-extinguisher" style="color:var(--neon-pink)"></i> Feuerwehr</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Feuerwehr – Brandbekämpfung, technische Hilfeleistung und Bergung.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-truck-medical" style="color:var(--neon-pink)"></i> Rettungsdienst</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Rettungsdienst – Akute medizinische Notfallversorgung und Krankentransporte.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-user-doctor" style="color:var(--neon-cyan)"></i> Notarzt</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Notarzt – Erweiterte medizinische Versorgung vor Ort bei schwersten Verletzungen.</p>
                    </div>
                    <div class="card">
                        <div class="card-header"><span class="card-title"><i class="fa-solid fa-tower-broadcast" style="color:var(--neon-cyan)"></i> Einsatzleitung</span></div>
                        <p style="color:var(--text-muted); font-size:0.9rem;">Feuerwehr-Einsatzleitung – Koordinierung aller Rettungskräfte bei Großschadenslagen.</p>
                    </div>
                </div>

                <div class="form-container" id="form-feuerwehr-container" style="display:none;">
                    <h3 style="margin-bottom: 15px; color:#fff;"><i class="fa-solid fa-plus-circle"></i> Feuerwehr-Abteilung hinzufügen (Admin)</h3>
                    <div class="form-group"><label>Name</label><input type="text" id="fw-name" class="form-control"></div>
                    <div class="form-group"><label>Beschreibung</label><input type="text" id="fw-status" class="form-control"></div>
                    <button class="submit-btn" onclick="addFactionPost('feuerwehr')">Hinzufügen</button>
                </div>
            </div>
        </div>

        <!-- TAB 5: TEAMLISTE -->
        <div id="tab-team" class="tab-content">
            <div class="card-grid">
                <div class="card">
                    <div class="card-header"><span class="card-title" style="color:var(--neon-pink)">Owner</span></div>
                    <div>
                        <span class="user-tag">@MRP ❌ FC Nils</span>
                        <span class="user-tag">@MRP ❌ Mika</span>
                        <span class="user-tag">@MRP ❌ Cookie</span>
                    </div>
                </div>
                <div class="card"><div class="card-header"><span class="card-title">Co Owner</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Co Owner Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Stv. Co Owner</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Stv. Co Owner Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Projektleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Projektleitung Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Stv. Projektleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Stv. Projektleitung Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Teamleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Teamleitung Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Stv. Teamleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Stv. Teamleitung Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Teamaufsicht</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Teamaufsicht Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Stv. Teamaufsicht</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Stv. Teamaufsicht Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Serverleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Serverleitung Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Ausbilderleitung</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Ausbilderleitung Rolle.</div></div>

                <div class="card">
                    <div class="card-header"><span class="card-title" style="color:var(--neon-cyan)">Event Management</span></div>
                    <div><span class="user-tag">@MRP ❌ Cookie</span></div>
                </div>
                <div class="card">
                    <div class="card-header"><span class="card-title" style="color:var(--neon-cyan)">Soziale Media Management</span></div>
                    <div><span class="user-tag">@MRP ❌ FC Nils</span></div>
                </div>
                <div class="card"><div class="card-header"><span class="card-title">Develpor</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Develpor Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Management Anwärter</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Management Anwärter Rolle.</div></div>
                <div class="card">
                    <div class="card-header"><span class="card-title" style="color:var(--neon-cyan)">Ausbilder</span></div>
                    <div><span class="user-tag">@MRP ❌ Cookie</span></div>
                </div>

                <div class="card"><div class="card-header"><span class="card-title">Senior - Highteam</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Senior - Highteam Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Highteam</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Highteam Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Junior Highteam</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Junior Highteam Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Head Admin</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Head Admin Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Senior Admin</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Senior Admin Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Admin</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Admin Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Junior Admin</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Junior Admin Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Head Moderator</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Head Moderator Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Senior Moderator</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Senior Moderator Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Moderator</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Moderator Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Junior Moderator</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Junior Moderator Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Probe Moderator</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Probe Moderator Rolle.</div></div>

                <div class="card">
                    <div class="card-header"><span class="card-title" style="color:var(--neon-cyan)">Senior Supporter</span></div>
                    <div><span class="user-tag">@MRP ❌ X309lsa</span></div>
                </div>
                <div class="card"><div class="card-header"><span class="card-title">Supporter</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Supporter Rolle.</div></div>
                <div class="card"><div class="card-header"><span class="card-title">Test Supporter</span></div><div class="empty-role">Kein Mitglied des Servers hat die @Test Supporter Rolle.</div></div>
            </div>
        </div>

        <!-- TAB 6: ADMIN DASHBOARD -->
        <div id="tab-admin" class="tab-content">
            <div id="admin-login-screen" class="login-box">
                <h2 style="color: var(--neon-cyan); margin-bottom: 15px;"><i class="fa-solid fa-lock"></i> Admin Dashboard</h2>
                <p style="color: var(--text-muted); font-size: 0.9rem; margin-bottom: 20px;">Nur für berechtigte Personen (Passwort: MRP1).</p>
                <div class="form-group">
                    <input type="password" id="admin-password-input" class="form-control" placeholder="Passwort eingeben">
                </div>
                <button class="submit-btn" style="width: 100%; padding: 12px;" onclick="checkAdminLogin()">Einloggen</button>
            </div>

            <div id="admin-panel" style="display: none;">
                <div class="section-title" style="justify-content: space-between; align-items: center;">
                    <span><i class="fa-solid fa-gauge-high" style="color:var(--neon-pink)"></i> Admin Kontrollzentrum</span>
                    <button class="submit-btn" style="background: rgba(255,0,85,0.3); border:1px solid var(--neon-pink);" onclick="logoutAdmin()">Ausloggen</button>
                </div>

                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-value" id="stat-total-visits">0</div>
                        <div class="stat-label">Gesamte Seitenaufrufe</div>
                    </div>
                </div>

                <div class="card" style="margin-bottom: 25px;">
                    <div class="card-header"><span class="card-title">Besucher-Protokoll</span></div>
                    <div style="overflow-x: auto;">
                        <table class="visitor-table">
                            <thead>
                                <tr><th>Uhrzeit</th><th>Besucher</th><th>Gerät</th><th>Bereich</th></tr>
                            </thead>
                            <tbody id="visitor-log-body"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

    </div>

    <footer>
        <p>&copy; 2026 München RP VC | Offizielles Server-Portal</p>
    </footer>

    <script>
        let visitCount = localStorage.getItem('mrp_visits') ? parseInt(localStorage.getItem('mrp_visits')) + 1 : 1;
        localStorage.setItem('mrp_visits', visitCount);

        let visitors = JSON.parse(localStorage.getItem('mrp_visitors') || '[]');
        let currentTime = new Date().toLocaleTimeString('de-DE', { hour: '2-digit', minute: '2-digit' });
        let userAgent = navigator.userAgent.includes('Mobile') ? 'Mobiles Gerät' : 'Desktop PC';
        visitors.unshift({ time: currentTime, user: 'Besucher #' + Math.floor(Math.random()*9000+1000), device: userAgent, page: 'Portal' });
        if(visitors.length > 10) visitors.pop();
        localStorage.setItem('mrp_visitors', JSON.stringify(visitors));

        const ruleData = {
            rp: {
                title: "RP-Regeln München RP VC",
                content: [
                    "§1 Fail RP (FRP): Fail RP ist fehlerhaftes/unrealistisches Verhalten im RP (z.B. kein Angst RP ausspielen).",
                    "§2 Taschen-RP: Zu große Dinge aus der Hosentasche zu ziehen ist verboten (z.B. G36, M4 Karabiner). Hat man eine Tasche oder Rucksack ist dies nicht der Fall. Die Sniper und Leiter müssen immer aus dem Auto geholt werden.",
                    "§3 Crash RP: Nach Unfällen anhalten, Schaden prüfen → ADAC/Feuerwehr rufen.",
                    "§4 Schusscall: Ein Schusscall muss 3 Sekunden vorher gegeben werden (z.B. Waffe runter oder ich schieße!).",
                    "§5 Random Deathmatch (RDM): Spieler ohne Schuss-Call oder RP-Kontext erschießen.",
                    "§6 Vehicle Deathmatch (VDM): Jemanden ohne RP-Hintergrund mit einem Fahrzeug umfahren.",
                    "§7 Power RP: Keine übermenschlichen Actions (z. B. LKW wegschieben) oder Handlungen aufzwingen, sodass der Gegenüber keine Wahl hat (z.B. Stop sticks um das Auto).",
                    "§8 Meta Gaming: OOC-Infos dürfen nicht IC verwendet werden (z.B. über Discord).",
                    "§9 New Life Rule (NLR): Nach dem RP-Tod keine Erinnerung an die Situation. Rache nehmen nach dem Tod gibt es nicht.",
                    "§10 Combatlogging: Beabsichtigtes Ausloggen, um Kämpfe oder RP-Strafen zu umgehen ist verboten.",
                    "§11 Safezones: Krankenhaus, Polizeistation, Tuning Garage & Feuerwehr sind Safezones. Keine Gewalt oder Festnahmen. Flüchten in Safezones um z.B. nicht festgenommen zu werden ist nicht erlaubt.",
                    "§12 Roblox Regeln: Verbot von Erotik-RP, Suizid-RP, Terror-RP.",
                    "§14 Unrealistische Skins: Troll Skins/Kostüme (z. B. Pinguin) sind im RP verboten.",
                    "§15 Soundboard: Das Nutzen von Soundboards ist verboten. Musik hören im Auto als „Radio“ ist erlaubt solange es keine IC/OOC Situation stört.",
                    "§16 Admin-Flucht: Flucht vor dem Serverteam um Strafen zu vermeiden ist verboten."
                ]
            },
            discord: {
                title: "©RPDiscord-Regeln München RP VC (Bitte lesen & respektieren)",
                content: [
                    "Willkommen auf unserem Discord-Server! Um ein angenehmes Miteinander für alle zu gewährleisten, bitten wir euch, die folgenden Regeln zu beachten und einzuhalten.",
                    "Allgemeines Verhalten: Seid respektvoll im Umgang miteinander. Keine Beleidigungen, Provokationen, Diskriminierung oder Belästigung. Spam, Trolling und Stören der Unterhaltung sind verboten.",
                    "Sprache & Ausdruck: Nutzt eine angemessene Sprache. Kein NSFW/18+ Inhalt (Texte, Bilder, Sprache) – sofern nicht ausdrücklich erlaubt. Rassistische, sexistische oder sonstige verletzende Ausdrücke sind untersagt.",
                    "Werbung & Eigenwerbung: Werbung für andere Server, Social Media oder Produkte ist nur mit Erlaubnis erlaubt. Keine unaufgeforderte Eigenwerbung in DMs oder Kanälen.",
                    "Sprach- & Textkanäle: Nutzt die Kanäle nur für das jeweilige Thema. In Sprachkanälen gilt gegenseitiger Respekt. Keine Soundboards oder Störgeräusche ohne Zustimmung.",
                    "Datenschutz & Privatsphäre: Keine persönlichen Daten (Adressen, Telefonnummern etc.) veröffentlichen – weder eigene noch fremde. Leaks, Doxing oder ähnliches Verhalten führen zum sofortigen Bann."
                ]
            },
            polizei: {
                title: "©Cop-Regeln München RP VC",
                content: [
                    "§1 Cuffen: Bewusstlose Personen dürfen gefesselt werden. Mit Handschellen hinter einer Person herlaufen um sie festzunehmen ist verboten. Spieler aus dem Auto festzunehmen ist ebenfalls verboten.",
                    "§2 Blitzen: Blitzen in der ganzen Innenstadt verboten erst ab ares Höhe ist erlaubt (siehe map). Nur Einzelpersonen dürfen blitzen – keine Gruppenaktionen.",
                    "§3 Stop Sticks: Stop Sticks dürfen nur in die Fahrbahn geworfen werden, um fahrende Fahrzeuge zu stoppen – Nicht vor stehenden Fahrzeugen auslegen. Stop Sticks dürfen für Straßensperren verwendet werden.",
                    "§4 Geiselnahmen: Für jede Geisel maximal 1 Forderung. Pro Geisel max. 2000€.",
                    "§5 Teamen: Das Teamen zwischen Polizei und Kriminellen ist verboten."
                ]
            },
            fraktion: {
                title: "Fraktionsregelwerk München RP VC",
                content: [
                    "Neutrale Fraktionen (Beispiele: Tankstellen, Dönerbuden, Sicherheitsfirmen, Banken, Juweliere): Dürfen alle zum Verkauf stehenden Grundstücke kaufen. Maximal 7 Mitglieder gleichzeitig ingame.",
                    "Kriminelle Fraktionen (Beispiele: Gangs, Kartelle, Auftragskiller): Dürfen alle Grundstücke kaufen, außer Firmengrundstücke. Maximal 5 Mitglieder gleichzeitig ingame.",
                    "Ganggebiete - Polizei darf Ganggrundstücke nur betreten mit: Razzienbefehl, gültigem Haftbefehl oder Gefahr im Verzug.",
                    "Schusscall: Dauerhafter Schusscall gilt für eigene Gang und verfeindete Gangs. Polizei und Zivilisten müssen zuerst einen Schusscall setzen.",
                    "Gangkriege: Ohne Genehmigung erlaubt. Kämpfe nur auf Grundstücken der beteiligten Gangs.",
                    "Gangbündnisse: Bündnisse sind erlaubt. Danach dürfen nur noch 5 Mitglieder + Owner gleichzeitig ingame sein.",
                    "Polizei-Raids: PD-Raids nur mit Erlaubnis der FL oder Leitung. 5 Minuten vorher per Broadcast ankündigen. Polizeisafezone wird für 5 Minuten deaktiviert."
                ]
            },
            immobilien: {
                title: "Haus- und Immobilienregelung",
                content: [
                    "☆《1》 Keine Schutzzone: Häuser und Immobilien gelten nicht als Safezone. Roleplay-Situationen können dort unter denselben Voraussetzungen stattfinden wie an jedem anderen Ort des Servers.",
                    "☆《2》 Eigentumsverhältnisse: Das Eigentum an einer Immobilie steht ausschließlich der Person oder Gruppierung zu, die diese offiziell erworben hat. Ohne einen rechtsgültigen Kauf besteht keinerlei Besitzanspruch – unabhängig von Nutzung, Roleplay-Handlungen oder internen Absprachen.",
                    "☆《3》 Zutritt zu fremden Immobilien: Das Betreten fremder Häuser ist nur mit einem nachvollziehbaren und angemessenen RP-Hintergrund zulässig. Einbruch, Durchsuchung oder Besetzung setzen einen klar erkennbaren und begründeten Roleplay-Anlass voraus. Unbegründetes oder willkürliches Betreten ist untersagt.",
                    "☆《4》 Nutzung im Roleplay: Immobilien dürfen im Rahmen des regulären Roleplays genutzt werden (z. B. als Wohnsitz, Treffpunkt, Planungsort oder Rückzugsort). Unrealistisches Verhalten sowie Power-RP sind nicht gestattet.",
                    "☆《5》 Konflikte und Gewalt: Gewalthandlungen innerhalb oder im unmittelbaren Umfeld von Immobilien sind ausschließlich mit schlüssigem RP-Hintergrund erlaubt. RDM, dauerhaftes Belagern („Camping“) sowie sinnloses Abfarmen sind verboten.",
                    "☆《6》 Fairness und Regelkonformität: Immobilien dürfen nicht missbräuchlich genutzt werden, um Spielmechaniken auszunutzen, sich unfaire Vorteile zu verschaffen oder das Roleplay anderer Spieler negativ zu beeinflussen.",
                    "⚠️ Sanktionen bei Verstößen: Verstöße gegen diese Regelung können zu Verwarnungen, administrativen Maßnahmen oder im Einzelfall zum Entzug der Immobilie führen."
                ]
            }
        };

        function switchTab(tabId, evt) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
            document.getElementById('tab-' + tabId).classList.add('active');
            if (evt && evt.currentTarget) evt.currentTarget.classList.add('active');
            if(tabId === 'regelwerke') showRule('rp');
            if(tabId === 'admin') loadAdminDashboardData();
        }

        function showRule(key, evt) {
            document.querySelectorAll('.rule-btn').forEach(btn => btn.classList.remove('active'));
            if (evt && evt.currentTarget) {
                evt.currentTarget.classList.add('active');
            } else {
                document.querySelector('.rules-button-grid .rule-btn').classList.add('active');
            }

            const data = ruleData[key];
            let listHTML = '<ul>';
            data.content.forEach(item => listHTML += `<li>${item}</li>`);
            listHTML += '</ul>';
            document.getElementById('rule-content-box').innerHTML = `<h2>${data.title}</h2>${listHTML}`;
        }

        function selectFaction(fac) {
            document.getElementById('btn-polizei').classList.remove('active');
            document.getElementById('btn-feuerwehr').classList.remove('active');
            document.getElementById('faction-polizei-details').style.display = 'none';
            document.getElementById('faction-feuerwehr-details').style.display = 'none';

            if(fac === 'polizei') {
                document.getElementById('btn-polizei').classList.add('active');
                document.getElementById('faction-polizei-details').style.display = 'block';
            } else {
                document.getElementById('btn-feuerwehr').classList.add('active');
                document.getElementById('faction-feuerwehr-details').style.display = 'block';
            }
        }

        function checkAdminLogin() {
            const pass = document.getElementById('admin-password-input').value;
            if(pass === 'MRP1' || localStorage.getItem('mrp_logged_in') === 'true') {
                localStorage.setItem('mrp_logged_in', 'true');
                document.getElementById('admin-login-screen').style.display = 'none';
                document.getElementById('admin-panel').style.display = 'block';
                document.getElementById('form-polizei-container').style.display = 'block';
                document.getElementById('form-feuerwehr-container').style.display = 'block';
                loadAdminDashboardData();
            } else {
                alert('Falsches Passwort!');
            }
        }

        function logoutAdmin() {
            localStorage.setItem('mrp_logged_in', 'false');
            document.getElementById('admin-panel').style.display = 'none';
            document.getElementById('admin-login-screen').style.display = 'block';
            document.getElementById('form-polizei-container').style.display = 'none';
            document.getElementById('form-feuerwehr-container').style.display = 'none';
        }

        function loadAdminDashboardData() {
            document.getElementById('stat-total-visits').innerText = localStorage.getItem('mrp_visits') || 1;
            const tbody = document.getElementById('visitor-log-body');
            tbody.innerHTML = '';
            visitors.forEach(v => {
                tbody.innerHTML += `<tr><td>${v.time}</td><td>${v.user}</td><td>${v.device}</td><td>${v.page}</td></tr>`;
            });
        }

        function addFactionPost(type) {
            const name = document.getElementById(type === 'polizei' ? 'pol-name' : 'fw-name').value;
            const status = document.getElementById(type === 'polizei' ? 'pol-status' : 'fw-status').value;
            if(!name || !status) return alert('Bitte alle Felder ausfüllen!');
            const grid = document.getElementById(type === 'polizei' ? 'polizei-grid' : 'feuerwehr-grid');
            grid.innerHTML += `<div class="card"><div class="card-header"><span class="card-title">${name}</span></div><p style="color:var(--text-muted); font-size:0.9rem;">${status}</p></div>`;
            document.getElementById(type === 'polizei' ? 'pol-name' : 'fw-name').value = '';
            document.getElementById(type === 'polizei' ? 'pol-status' : 'fw-status').value = '';
        }

        window.onload = function() {
            showRule('rp');
            if(localStorage.getItem('mrp_logged_in') === 'true') {
                document.getElementById('admin-login-screen').style.display = 'none';
                document.getElementById('admin-panel').style.display = 'block';
                document.getElementById('form-polizei-container').style.display = 'block';
                document.getElementById('form-feuerwehr-container').style.display = 'block';
            }
        };
    </script>
</body>
</html>
