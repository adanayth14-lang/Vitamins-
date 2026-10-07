# Vitamins-
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NutriBot: Campaña Nutricional Virtual</title>
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #311042 100%);
            --card-bg: rgba(255, 255, 255, 0.07);
            --card-border: rgba(255, 255, 255, 0.18);
            
            /* Vibrant Fun Palette */
            --pop-cyan: #00f2fe;
            --pop-pink: #ff007f;
            --pop-yellow: #ffe600;
            --pop-green: #00ff87;
            --pop-purple: #a855f7;
            
            --text-light: #ffffff;
            --text-dim: #cbd5e1;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Outfit', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: var(--bg-gradient);
            color: var(--text-light);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 920px;
            background: var(--card-bg);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border-radius: 24px;
            padding: 28px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5), inset 0 0 2px rgba(255, 255, 255, 0.2);
            border: 1px solid var(--card-border);
        }

        header {
            text-align: center;
            margin-bottom: 24px;
        }

        h1 {
            font-size: 2.2rem;
            font-weight: 800;
            background: linear-gradient(90deg, var(--pop-cyan), var(--pop-pink), var(--pop-yellow));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 6px;
            letter-spacing: -0.5px;
        }

        .subtitle {
            color: var(--text-dim);
            font-size: 1rem;
            font-weight: 500;
        }

        /* Status Header Bar */
        .status-header {
            display: flex;
            justify-content: space-between;
            background: rgba(0, 0, 0, 0.35);
            padding: 14px 24px;
            border-radius: 16px;
            margin-bottom: 24px;
            font-weight: 700;
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .badge {
            background: linear-gradient(135deg, var(--pop-cyan), #0077ff);
            padding: 6px 16px;
            border-radius: 30px;
            color: #000;
            font-weight: 800;
            box-shadow: 0 0 12px rgba(0, 242, 254, 0.4);
        }

        .badge-attempts {
            background: linear-gradient(135deg, var(--pop-yellow), #ff9900);
            color: #000;
            box-shadow: 0 0 12px rgba(255, 230, 0, 0.4);
        }

        /* Game Layout */
        .game-layout {
            display: grid;
            grid-template-columns: 1.1fr 1fr;
            gap: 24px;
        }

        @media (max-width: 800px) {
            .game-layout {
                grid-template-columns: 1fr;
            }
        }

        /* Character Section */
        .character-card {
            background: rgba(0, 0, 0, 0.25);
            border-radius: 20px;
            padding: 22px;
            display: flex;
            flex-direction: column;
            align-items: center;
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .bot-avatar {
            font-size: 5.5rem;
            margin-bottom: 8px;
            filter: drop-shadow(0 0 15px rgba(0, 242, 254, 0.3));
            transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .bot-avatar.bounce {
            transform: scale(1.25) rotate(-8deg);
        }

        .bot-status-text {
            font-size: 1.05rem;
            font-weight: 700;
            color: var(--pop-cyan);
            margin-bottom: 18px;
            text-align: center;
            min-height: 28px;
        }

        .section-title {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: var(--pop-yellow);
            margin-bottom: 12px;
            font-weight: 800;
            width: 100%;
            text-align: left;
        }

        /* Metrics Grid (Casillas) */
        .metrics-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            width: 100%;
        }

        .metric-card {
            background: rgba(255, 255, 255, 0.05);
            padding: 12px;
            border-radius: 14px;
            cursor: pointer;
            transition: all 0.25s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .metric-card:hover {
            background: rgba(255, 255, 255, 0.12);
            border-color: var(--pop-cyan);
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .metric-title {
            display: flex;
            justify-content: space-between;
            font-size: 0.85rem;
            margin-bottom: 8px;
            font-weight: 700;
        }

        .bar-container {
            width: 100%;
            height: 12px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            overflow: hidden;
            padding: 2px;
        }

        .bar-fill {
            height: 100%;
            width: 30%;
            border-radius: 8px;
            transition: width 0.5s ease;
        }

        .fill-vision { background: linear-gradient(90deg, #00f2fe, #4facfe); box-shadow: 0 0 10px #00f2fe; }
        .fill-energia { background: linear-gradient(90deg, #ffe600, #ffb700); box-shadow: 0 0 10px #ffe600; }
        .fill-inmunidad { background: linear-gradient(90deg, #00ff87, #60efff); box-shadow: 0 0 10px #00ff87; }
        .fill-estructura { background: linear-gradient(90deg, #ff007f, #7928ca); box-shadow: 0 0 10px #ff007f; }

        /* Vitamin Buttons Grid */
        .controls-section {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .vitamin-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
        }

        .btn-vitamin {
            background: rgba(255, 255, 255, 0.06);
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: var(--text-light);
            padding: 12px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 700;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.2s ease;
        }

        .btn-vitamin:hover:not(:disabled) {
            background: linear-gradient(135deg, var(--pop-pink), var(--pop-purple));
            border-color: transparent;
            transform: scale(1.03);
            box-shadow: 0 5px 15px rgba(255, 0, 127, 0.4);
        }

        .btn-vitamin:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        .vit-tag {
            font-size: 0.68rem;
            padding: 3px 8px;
            border-radius: 20px;
            background: rgba(0, 0, 0, 0.4);
            font-weight: 600;
        }

        /* Info Panel */
        .info-panel {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 16px;
            padding: 16px;
            border-left: 4px solid var(--pop-cyan);
            min-height: 115px;
            box-shadow: inset 0 0 10px rgba(0,0,0,0.3);
        }

        .info-panel h4 {
            color: var(--pop-green);
            margin-bottom: 6px;
            font-size: 1rem;
        }

        .info-panel p {
            font-size: 0.88rem;
            color: var(--text-dim);
            line-height: 1.45;
        }

        /* Footer Actions */
        .footer-actions {
            display: flex;
            margin-top: 24px;
        }

        .btn-action {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 14px;
            font-weight: 800;
            font-size: 0.95rem;
            cursor: pointer;
            transition: all 0.2s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-reset {
            background: rgba(255, 255, 255, 0.1);
            color: var(--text-light);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .btn-reset:hover {
            background: rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
        }

        /* Final Report Modal */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 23, 42, 0.92);
            backdrop-filter: blur(10px);
            display: none;
            justify-content: center;
            align-items: center;
            padding: 20px;
            z-index: 100;
            overflow-y: auto;
        }

        .modal-content {
            background: #1e1b4b;
            padding: 28px;
            border-radius: 24px;
            max-width: 580px;
            width: 100%;
            text-align: center;
            border: 2px solid var(--pop-green);
            box-shadow: 0 0 40px rgba(0, 255, 135, 0.3);
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-title {
            color: var(--pop-green);
            font-size: 1.7rem;
            margin-bottom: 8px;
            font-weight: 800;
        }

        .modal-body {
            font-size: 0.95rem;
            color: var(--text-dim);
            margin-bottom: 20px;
            line-height: 1.5;
            text-align: left;
        }

        /* Custom Styling for the Report Box */
        .report-card {
            background: rgba(0, 0, 0, 0.45);
            border-radius: 16px;
            padding: 20px;
            margin: 16px 0;
            border: 1px solid rgba(255, 255, 255, 0.12);
            text-align: left;
        }

        .report-header {
            font-size: 1.2rem;
            font-weight: 800;
            color: var(--pop-yellow);
            border-bottom: 1px solid rgba(255,255,255,0.1);
            padding-bottom: 8px;
            margin-bottom: 14px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .report-score-badge {
            background: linear-gradient(90deg, var(--pop-pink), var(--pop-purple));
            color: #fff;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 1rem;
        }

        .report-metrics-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 16px;
        }

        .report-metric-item {
            background: rgba(255,255,255,0.05);
            padding: 8px 12px;
            border-radius: 10px;
            font-weight: 600;
            font-size: 0.9rem;
            display: flex;
            justify-content: space-between;
        }

        .report-decisions {
            display: flex;
            gap: 12px;
            margin-bottom: 16px;
            font-size: 0.88rem;
        }

        .report-dec-box {
            flex: 1;
            padding: 10px;
            border-radius: 10px;
            text-align: center;
            font-weight: 700;
        }

        .dec-correct {
            background: rgba(0, 255, 135, 0.15);
            border: 1px solid var(--pop-green);
            color: var(--pop-green);
        }

        .dec-suboptimal {
            background: rgba(255, 0, 127, 0.15);
            border: 1px solid var(--pop-pink);
            color: var(--pop-pink);
        }

        .report-vitamins-list {
            background: rgba(255,255,255,0.05);
            padding: 10px 14px;
            border-radius: 10px;
            margin-bottom: 16px;
            font-size: 0.9rem;
            letter-spacing: 1px;
            word-wrap: break-word;
        }

        .report-review-box {
            background: rgba(255, 230, 0, 0.08);
            border-left: 4px solid var(--pop-yellow);
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
        }

        .report-review-box h5 {
            color: var(--pop-yellow);
            margin-bottom: 6px;
            font-size: 0.95rem;
            text-transform: uppercase;
        }

        .report-review-box ul {
            padding-left: 18px;
            font-size: 0.85rem;
            color: var(--text-dim);
            line-height: 1.5;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;700;800&display=swap" rel="stylesheet">
</head>
<body>

<div class="container">
    <header>
        <h1>🤖 NutriBot: Campaña Virtual</h1>
        <p class="subtitle">Simulador de optimización metabólica y nutrición celular</p>
    </header>

    <!-- Top Status Bar -->
    <div class="status-header">
        <div>Ronda: <span id="round-display" class="badge">1 / 5</span></div>
        <div>Dosis Restantes: <span id="attempts-display" class="badge badge-attempts">3</span></div>
    </div>

    <!-- Main Content -->
    <div class="game-layout">
        
        <!-- Left Column: Character & Metric Cards -->
        <div class="character-card">
            <div id="bot-avatar" class="bot-avatar">🤖</div>
            <div id="bot-status" class="bot-status-text">"Sistemas inicializados..."</div>

            <div class="section-title">Casillas de Estado (Clic para info)</div>
            <div class="metrics-grid">
                
                <!-- Visión -->
                <div class="metric-card" onclick="showMetricInfo('vision')">
                    <div class="metric-title">
                        <span>👁️ Visión</span>
                        <span id="val-vision">0%</span>
                    </div>
                    <div class="bar-container">
                        <div id="bar-vision" class="bar-fill fill-vision"></div>
                    </div>
                </div>

                <!-- Energía -->
                <div class="metric-card" onclick="showMetricInfo('energia')">
                    <div class="metric-title">
                        <span>⚡ Energía</span>
                        <span id="val-energia">0%</span>
                    </div>
                    <div class="bar-container">
                        <div id="bar-energia" class="bar-fill fill-energia"></div>
                    </div>
                </div>

                <!-- Inmunidad -->
                <div class="metric-card" onclick="showMetricInfo('inmunidad')">
                    <div class="metric-title">
                        <span>🛡️ Inmunidad</span>
                        <span id="val-inmunidad">0%</span>
                    </div>
                    <div class="bar-container">
                        <div id="bar-inmunidad" class="bar-fill fill-inmunidad"></div>
                    </div>
                </div>

                <!-- Estructura -->
                <div class="metric-card" onclick="showMetricInfo('estructura')">
                    <div class="metric-title">
                        <span>🦴 Estructura</span>
                        <span id="val-estructura">0%</span>
                    </div>
                    <div class="bar-container">
                        <div id="bar-estructura" class="bar-fill fill-estructura"></div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Right Column: Controls & Information -->
        <div class="controls-section">
            <div class="section-title">Administrar Vitamina (1 Dosis)</div>
            
            <div class="vitamin-buttons">
                <button class="btn-vitamin" onclick="applyVitamin('A')">
                    Vitamina A <span class="vit-tag">Lipo</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('C')">
                    Vitamina C <span class="vit-tag">Hidro</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('D')">
                    Vitamina D <span class="vit-tag">Lipo</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('E')">
                    Vitamina E <span class="vit-tag">Lipo</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('K')">
                    Vitamina K <span class="vit-tag">Lipo</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('B12')">
                    Vitamina B12 <span class="vit-tag">Hidro</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('B2')">
                    Vitamina B2 <span class="vit-tag">Hidro</span>
                </button>
                <button class="btn-vitamin" onclick="applyVitamin('B9')">
                    Ácido Fólico <span class="vit-tag">Hidro</span>
                </button>
            </div>

            <!-- Information Panel -->
            <div class="info-panel">
                <h4 id="info-title">Selecciona una opción</h4>
                <p id="info-body">Haz clic en los botones de vitamina para administrar dosis o presiona cualquiera de las casillas de estado para consultar su fundamento biomédico.</p>
            </div>
        </div>

    </div>

    <!-- Bottom Actions -->
    <div class="footer-actions">
        <button class="btn-action btn-reset" onclick="resetFullGame()">🔄 Reiniciar Partida (Nuevos Déficits)</button>
    </div>
</div>

<!-- Modal Evaluation Window -->
<div id="report-modal" class="modal-overlay">
    <div class="modal-content">
        <h2 class="modal-title" id="modal-result-title">Evaluación Clínica Final</h2>
        <div class="modal-body">
            <p id="modal-result-desc"></p>
            
            <!-- Performance Report Component -->
            <div class="report-card">
                <div class="report-header">
                    <span>🏆 INFORME DE DESEMPEÑO</span>
                    <span class="report-score-badge">Puntuación: <strong id="report-score">0/100</strong></span>
                </div>

                <div class="report-metrics-grid">
                    <div class="report-metric-item">
                        <span>👁️ Visión:</span>
                        <span id="rep-val-vision" style="color: var(--pop-cyan)">0%</span>
                    </div>
                    <div class="report-metric-item">
                        <span>⚡ Energía:</span>
                        <span id="rep-val-energia" style="color: var(--pop-yellow)">0%</span>
                    </div>
                    <div class="report-metric-item">
                        <span>🛡️ Inmunidad:</span>
                        <span id="rep-val-inmunidad" style="color: var(--pop-green)">0%</span>
                    </div>
                    <div class="report-metric-item">
                        <span>🦴 Estructura:</span>
                        <span id="rep-val-estructura" style="color: var(--pop-pink)">0%</span>
                    </div>
                </div>

                <div class="report-decisions">
                    <div class="report-dec-box dec-correct">
                        Decisiones correctas: <span id="rep-dec-correct">0</span>
                    </div>
                    <div class="report-dec-box dec-suboptimal">
                        
