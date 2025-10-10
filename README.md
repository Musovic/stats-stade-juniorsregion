<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stats Rugby - Juniors Régionaux</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #dc3545 0%, #8b0000 100%);
            min-height: 100vh;
        }

        .app-container {
            display: block;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            border: 3px solid #dc3545;
        }

        .header h1 {
            color: #dc3545;
            margin-bottom: 15px;
        }

        .header-actions {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .import-btn {
            position: relative;
            overflow: hidden;
        }

        .import-btn input[type="file"] {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .tab {
            padding: 12px 24px;
            background: white;
            border: 2px solid #dc3545;
            border-radius: 10px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            color: #dc3545;
            font-weight: bold;
        }

        .tab.active {
            background: #dc3545;
            color: white;
        }

        .content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            min-height: 500px;
            border: 3px solid #dc3545;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .player-form {
            display: grid;
            gap: 15px;
            max-width: 500px;
            margin-bottom: 30px;
        }

        .player-form input, .player-form select {
            padding: 10px;
            border: 2px solid #dc3545;
            border-radius: 8px;
            font-size: 14px;
        }

        .btn {
            padding: 10px 20px;
            background: #dc3545;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
        }

        .btn:hover {
            background: #c82333;
        }

        .players-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .player-card {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            border-left: 4px solid #dc3545;
        }

        .player-card h3 {
            color: #dc3545;
            margin-bottom: 5px;
        }

        .rugby-field {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin: 20px auto;
            background: linear-gradient(to bottom, #dc3545 0%, #dc3545 50%, white 50%, white 100%);
            border: 3px solid #333;
            padding: 20px;
            border-radius: 10px;
        }

        .position-slot {
            background: rgba(255,255,255,0.9);
            padding: 8px;
            margin: 8px;
            border-radius: 5px;
            text-align: center;
            border: 2px solid #dc3545;
        }

        .position-slot select {
            width: 100%;
            padding: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        .field-row {
            display: flex;
            justify-content: space-around;
            margin: 10px 0;
        }

        .match-form {
            max-width: 600px;
            margin-bottom: 30px;
        }

        .match-form input {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 2px solid #dc3545;
            border-radius: 8px;
        }

        .matches-list {
            margin-top: 30px;
        }

        .match-item {
            background: #f8f9fa;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s;
            border-left: 4px solid #dc3545;
        }

        .match-item:hover {
            transform: translateX(5px);
            background: #e9ecef;
        }

        .match-live {
            max-width: 900px;
            margin: 0 auto;
        }

        .scoreboard {
            background: linear-gradient(135deg, #dc3545, #8b0000);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 30px;
            text-align: center;
        }

        .score-display {
            font-size: 72px;
            font-weight: bold;
            margin: 20px 0;
        }

        .timer {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .timer-controls {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        .timer-btn {
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            background: white;
            color: #dc3545;
            font-weight: bold;
        }

        .score-actions {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }

        .score-btn {
            padding: 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
            color: white;
            transition: transform 0.2s;
        }

        .score-btn:hover {
            transform: scale(1.05);
        }

        .essai-btn { background: #28a745; }
        .transformation-btn { background: #17a2b8; }
        .penalite-btn { background: #ffc107; color: #333; }
        .carton-btn { background: #6c757d; }
        .remplacement-btn { background: #dc3545; }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 1000;
        }

        .modal.active {
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .player-detail-panel {
            display: none;
            position: fixed;
            top: 0;
            right: -400px;
            width: 400px;
            height: 100vh;
            background: white;
            box-shadow: -5px 0 20px rgba(0,0,0,0.3);
            z-index: 2000;
            transition: right 0.3s ease;
            overflow-y: auto;
        }

        .player-detail-panel.active {
            display: block;
            right: 0;
        }

        .panel-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1999;
        }

        .panel-overlay.active {
            display: block;
        }

        .panel-header {
            background: linear-gradient(135deg, #dc3545, #8b0000);
            color: white;
            padding: 20px;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .panel-content {
            padding: 20px;
        }

        .mini-stat {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 4px solid #dc3545;
        }

        .mini-stat-label {
            font-size: 12px;
            color: #666;
            margin-bottom: 5px;
        }

        .mini-stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #dc3545;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
            border: 3px solid #dc3545;
        }

        .modal-content h2 {
            margin-bottom: 20px;
            color: #dc3545;
        }

        .modal-content select, .modal-content input {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 2px solid #dc3545;
            border-radius: 8px;
        }

        .modal-content label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #333;
        }

        .modal-buttons {
            display: flex;
            gap: 10px;
            justify-content: flex-end;
        }

        .events-list {
            margin-top: 30px;
        }

        .event-item {
            background: #f8f9fa;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            border-left: 4px solid #dc3545;
        }

        .players-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 30px;
        }

        .players-table th, .players-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #e0e0e0;
        }

        .players-table th {
            background: #dc3545;
            color: white;
        }

        .carton-jaune {
            background: #ffc107;
            color: #333;
            padding: 3px 8px;
            border-radius: 5px;
            font-size: 12px;
        }

        .carton-rouge {
            background: #dc3545;
            color: white;
            padding: 3px 8px;
            border-radius: 5px;
            font-size: 12px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, #dc3545, #8b0000);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-card h3 {
            font-size: 36px;
            margin-bottom: 10px;
        }

        .player-stats-list {
            margin-top: 30px;
        }

        .player-stat-item {
            background: #f8f9fa;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            border-left: 4px solid #dc3545;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .player-stat-item strong {
            color: #dc3545;
        }

        .checkbox-group {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }

        .success-indicator {
            color: #28a745;
            font-weight: bold;
        }

        .fail-indicator {
            color: #dc3545;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="app-container" id="appContainer">
        <div class="header">
            <h1>🏉 Statistiques Rugby - Juniors Régionaux</h1>
            <div class="header-actions">
                <button class="btn" onclick="exportData()" style="background: #28a745;">
                    💾 Exporter les données
                </button>
                <div class="import-btn">
                    <button class="btn" style="background: #17a2b8;">
                        📥 Importer les données
                    </button>
                    <input type="file" id="importFile" accept=".json" onchange="importData(event)">
                </div>
                <button class="btn" onclick="clearAllData()" style="background: #6c757d;">
                    🗑️ Réinitialiser tout
                </button>
            </div>
        </div>

        <div class="tabs">
            <button class="tab active" onclick="switchTab('joueurs')">Joueurs</button>
            <button class="tab" onclick="switchTab('composition')">Composition</button>
            <button class="tab" onclick="switchTab('matchs')">Matchs</button>
            <button class="tab" onclick="switchTab('statistiques')">Statistiques Globales</button>
        </div>

        <div class="content">
            <!-- Onglet Joueurs -->
            <div class="tab-content active" id="joueurs">
                <h2 style="color: #dc3545;">Gestion des Joueurs</h2>
                <div class="player-form">
                    <input type="text" id="playerName" placeholder="Nom du joueur" />
                    <button class="btn" onclick="addPlayer()">Ajouter le joueur</button>
                </div>
                
                <h3 style="margin-top: 40px; color: #dc3545;">Liste des joueurs (par ordre alphabétique)</h3>
                <div class="player-stats-list" id="playersStatsList"></div>
            </div>

            <!-- Onglet Composition -->
            <div class="tab-content" id="composition">
                <h2 style="color: #dc3545;">Composition de l'équipe</h2>
                <div class="rugby-field">
                    <h3 style="color: #333; text-align: center; margin-bottom: 20px;">Terrain</h3>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>15 - Arrière</strong>
                            <select id="pos15" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>11 - Ailier</strong>
                            <select id="pos11" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>14 - Ailier</strong>
                            <select id="pos14" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>12 - Centre</strong>
                            <select id="pos12" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>13 - Centre</strong>
                            <select id="pos13" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>9 - Demi de mêlée</strong>
                            <select id="pos9" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>10 - Demi d'ouverture</strong>
                            <select id="pos10" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>6 - 3ème ligne</strong>
                            <select id="pos6" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>7 - 3ème ligne</strong>
                            <select id="pos7" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>8 - 3ème ligne</strong>
                            <select id="pos8" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>4 - 2ème ligne</strong>
                            <select id="pos4" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>5 - 2ème ligne</strong>
                            <select id="pos5" onchange="saveComposition()"></select>
                        </div>
                    </div>
                    
                    <div class="field-row">
                        <div class="position-slot">
                            <strong>1 - Pilier</strong>
                            <select id="pos1" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>2 - Talonneur</strong>
                            <select id="pos2" onchange="saveComposition()"></select>
                        </div>
                        <div class="position-slot">
                            <strong>3 - Pilier</strong>
                            <select id="pos3" onchange="saveComposition()"></select>
                        </div>
                    </div>
                </div>
                
                <h3 style="margin-top: 30px; color: #dc3545;">Remplaçants</h3>
                <div id="remplacants" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px; margin-top: 20px;">
                    <div class="position-slot">
                        <strong>16 - Remplaçant</strong>
                        <select id="pos16" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>17 - Remplaçant</strong>
                        <select id="pos17" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>18 - Remplaçant</strong>
                        <select id="pos18" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>19 - Remplaçant</strong>
                        <select id="pos19" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>20 - Remplaçant</strong>
                        <select id="pos20" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>21 - Remplaçant</strong>
                        <select id="pos21" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>22 - Remplaçant</strong>
                        <select id="pos22" onchange="saveComposition()"></select>
                    </div>
                    <div class="position-slot">
                        <strong>23 - Remplaçant</strong>
                        <select id="pos23" onchange="saveComposition()"></select>
                    </div>
                </div>
            </div>

            <!-- Onglet Matchs -->
            <div class="tab-content" id="matchs">
                <div id="matchsList">
                    <h2 style="color: #dc3545;">Liste des Matchs</h2>
                    <div class="match-form">
                        <input type="text" id="adversaire" placeholder="Équipe adverse" />
                        <input type="date" id="matchDate" />
                        <input type="text" id="lieu" placeholder="Lieu du match" />
                        <button class="btn" onclick="createMatch()">Créer un nouveau match</button>
                    </div>
                    <div class="matches-list" id="matchesList"></div>
                </div>

                <div id="matchLive" style="display: none;">
                    <button class="btn" onclick="backToMatches()" style="margin-bottom: 20px;">← Retour aux matchs</button>
                    <div class="match-live">
                        <div class="scoreboard">
                            <h2 id="matchTitle"></h2>
                            <div class="timer" id="timer">00:00</div>
                            <div class="timer-controls">
                                <button class="timer-btn" onclick="startTimer()">▶ Start</button>
                                <button class="timer-btn" onclick="pauseTimer()">⏸ Pause</button>
                                <button class="timer-btn" onclick="resetTimer()">↺ Reset</button>
                            </div>
                            <div class="score-display" id="scoreDisplay">0</div>
                        </div>

                        <div class="score-actions">
                            <button class="score-btn essai-btn" onclick="openModal('essai')">
                                Essai +5
                            </button>
                            <button class="score-btn transformation-btn" onclick="openModal('transformation')">
                                Transformation +2
                            </button>
                            <button class="score-btn penalite-btn" onclick="openModal('penalite')">
                                Pénalité +3
                            </button>
                            <button class="score-btn carton-btn" onclick="openModal('carton')">
                                Carton
                            </button>
                            <button class="score-btn remplacement-btn" onclick="openModal('remplacement')">
                                Remplacement
                            </button>
                        </div>

                        <div class="events-list" id="eventsList"></div>

                        <h3 style="margin-top: 30px; color: #dc3545;">Temps de jeu des joueurs</h3>
                        <table class="players-table">
                            <thead>
                                <tr>
                                    <th>Numéro</th>
                                    <th>Joueur</th>
                                    <th>Temps joué</th>
                                    <th>Cartons</th>
                                    <th>Points marqués</th>
                                </tr>
                            </thead>
                            <tbody id="playersStatsTable"></tbody>
                        </table>

                        <button class="btn" onclick="endMatch()" style="margin-top: 30px; background: #8b0000;">Terminer le match</button>
                    </div>
                </div>

                <div id="matchDebrief" style="display: none;">
                    <button class="btn" onclick="backToMatches()" style="margin-bottom: 20px;">← Retour aux matchs</button>
                    <button class="btn" onclick="exportToPDF()" style="margin-bottom: 20px; margin-left: 10px; background: #28a745;">📄 Exporter en PDF</button>
                    <h2 id="debriefTitle" style="color: #dc3545;"></h2>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <h3 id="debriefScore">0</h3>
                            <p>Score final</p>
                        </div>
                        <div class="stat-card">
                            <h3 id="debriefEssais">0</h3>
                            <p>Essais marqués</p>
                        </div>
                        <div class="stat-card">
                            <h3 id="debriefTransformations">0</h3>
                            <p>Transformations</p>
                        </div>
                        <div class="stat-card">
                            <h3 id="debriefPenalites">0</h3>
                            <p>Pénalités</p>
                        </div>
                    </div>

                    <h3 style="margin-top: 30px; color: #dc3545;">Taux de réussite aux transformations</h3>
                    <div id="transformationStats"></div>

                    <h3 style="margin-top: 30px; color: #dc3545;">Taux de réussite aux pénalités</h3>
                    <div id="penaliteStats"></div>

                    <h3 style="margin-top: 30px; color: #dc3545;">Détails des événements</h3>
                    <div id="debriefEvents"></div>

                    <h3 style="margin-top: 30px; color: #dc3545;">Statistiques des joueurs</h3>
                    <table class="players-table">
                        <thead>
                            <tr>
                                <th>Joueur</th>
                                <th>Temps joué</th>
                                <th>Points</th>
                                <th>Cartons</th>
                            </tr>
                        </thead>
                        <tbody id="debriefPlayersTable"></tbody>
                    </table>
                </div>
            </div>

            <!-- Onglet Statistiques Globales -->
            <div class="tab-content" id="statistiques">
                <h2 style="color: #dc3545;">Statistiques Globales de la Saison</h2>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <h3 id="globalTotalMatches">0</h3>
                        <p>Matchs joués</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalTotalPoints">0</h3>
                        <p>Points marqués</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalTotalEssais">0</h3>
                        <p>Essais marqués</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalTotalTransformations">0</h3>
                        <p>Transformations réussies</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalTotalPenalites">0</h3>
                        <p>Pénalités réussies</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalTransfoRate">0%</h3>
                        <p>Taux de réussite Transfo</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalPenaliteRate">0%</h3>
                        <p>Taux de réussite Péna</p>
                    </div>
                    <div class="stat-card">
                        <h3 id="globalAverageScore">0</h3>
                        <p>Score moyen par match</p>
                    </div>
                </div>

                <h3 style="margin-top: 40px; color: #dc3545;">Meilleurs marqueurs</h3>
                <div id="topScorers"></div>

                <h3 style="margin-top: 40px; color: #dc3545;">Meilleurs buteurs (Transformations & Pénalités)</h3>
                <div id="topKickers"></div>

                <h3 style="margin-top: 40px; color: #dc3545;">Temps de jeu par joueur</h3>
                <div id="playTimeChart"></div>

                <h3 style="margin-top: 40px; color: #dc3545;">Historique des matchs</h3>
                <div id="matchHistory"></div>
            </div>
        </div>
    </div>

    <!-- Panneau Détails Joueur -->
    <div class="panel-overlay" id="panelOverlay" onclick="closePlayerDetail()"></div>
    <div class="player-detail-panel" id="playerDetailPanel">
        <div class="panel-header">
            <div style="display: flex; justify-content: space-between; align-items: center;">
                <h2 id="playerDetailName" style="margin: 0; font-size: 24px;"></h2>
                <button onclick="closePlayerDetail()" style="background: white; color: #dc3545; border: none; width: 30px; height: 30px; border-radius: 50%; cursor: pointer; font-size: 18px; font-weight: bold;">×</button>
            </div>
        </div>
        <div class="panel-content" id="playerDetailBody"></div>
    </div>

    <!-- Modal -->
    <div class="modal" id="modal">
        <div class="modal-content">
            <h2 id="modalTitle"></h2>
            <div id="modalBody"></div>
            <div class="modal-buttons">
                <button class="btn" style="background: #6c757d;" onclick="closeModal()">Annuler</button>
                <button class="btn" onclick="confirmModal()">Confirmer</button>
            </div>
        </div>
    </div>

    <script>
        let players = [];
        let composition = {};
        let matches = [];
        let currentMatch = null;
        let timerInterval = null;
        let timerSeconds = 0;
        let timerRunning = false;
        let currentModalType = '';

        // Chargement des données
        function loadData() {
            players = JSON.parse(localStorage.getItem('rugbyPlayers') || '[]');
            composition = JSON.parse(localStorage.getItem('rugbyComposition') || '{}');
            matches = JSON.parse(localStorage.getItem('rugbyMatches') || '[]');
        }

        function saveData() {
            localStorage.setItem('rugbyPlayers', JSON.stringify(players));
            localStorage.setItem('rugbyComposition', JSON.stringify(composition));
            localStorage.setItem('rugbyMatches', JSON.stringify(matches));
        }

        // Navigation
        function switchTab(tabName) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tabName).classList.add('active');
            
            if (tabName === 'statistiques') {
                renderGlobalStats();
            }
        }

        // Gestion des joueurs
        function addPlayer() {
            const name = document.getElementById('playerName').value;
            
            if (!name) {
                alert('Veuillez entrer le nom du joueur');
                return;
            }
            
            // Trouver le prochain numéro disponible
            const existingNumbers = players.map(p => p.number);
            let nextNumber = 1;
            while (existingNumbers.includes(nextNumber)) {
                nextNumber++;
            }
            
            players.push({ 
                id: Date.now(), 
                name, 
                number: nextNumber, 
                position: 'Joueur',
                stats: {
                    totalMatches: 0,
                    totalPoints: 0,
                    essais: 0,
                    transformations: { reussies: 0, tentees: 0 },
                    penalites: { reussies: 0, tentees: 0 },
                    cartonsJaunes: 0,
                    cartonsRouges: 0,
                    tempsTotal: 0
                }
            });
            saveData();
            renderPlayersStats();
            renderComposition();
            
            document.getElementById('playerName').value = '';
        }

        function renderPlayersStats() {
            const sortedPlayers = [...players].sort((a, b) => a.name.localeCompare(b.name));
            const list = document.getElementById('playersStatsList');
            list.innerHTML = '';
            
            sortedPlayers.forEach(p => {
                const stats = p.stats;
                const transfoPct = stats.transformations.tentees > 0 ? 
                    Math.round((stats.transformations.reussies / stats.transformations.tentees) * 100) : 0;
                const penalitePct = stats.penalites.tentees > 0 ? 
                    Math.round((stats.penalites.reussies / stats.penalites.tentees) * 100) : 0;
                const minutes = Math.floor(stats.tempsTotal / 60);
                
                const itemDiv = document.createElement('div');
                itemDiv.className = 'player-stat-item';
                
                const infoDiv = document.createElement('div');
                infoDiv.innerHTML = `
                    <strong style="font-size: 18px;">${p.name}</strong>
                    <div style="font-size: 12px; color: #666; margin-top: 5px;">
                        Matchs: ${stats.totalMatches} | Points: ${stats.totalPoints} | Essais: ${stats.essais} | 
                        Transfo: ${stats.transformations.reussies}/${stats.transformations.tentees} (${transfoPct}%) | 
                        Péna: ${stats.penalites.reussies}/${stats.penalites.tentees} (${penalitePct}%) | 
                        Temps: ${minutes}min | 
                        Cartons: ${stats.cartonsJaunes}🟨 ${stats.cartonsRouges}🟥
                    </div>
                `;
                
                const buttonsDiv = document.createElement('div');
                buttonsDiv.style.display = 'flex';
                buttonsDiv.style.gap = '10px';
                
                const detailBtn = document.createElement('button');
                detailBtn.className = 'btn';
                detailBtn.style.background = '#17a2b8';
                detailBtn.style.fontSize = '12px';
                detailBtn.textContent = 'Détails';
                detailBtn.onclick = () => showPlayerDetail(p.id);
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'btn';
                deleteBtn.style.background = '#6c757d';
                deleteBtn.style.fontSize = '12px';
                deleteBtn.textContent = 'Supprimer';
                deleteBtn.onclick = () => deletePlayer(p.id);
                
                buttonsDiv.appendChild(detailBtn);
                buttonsDiv.appendChild(deleteBtn);
                
                itemDiv.appendChild(infoDiv);
                itemDiv.appendChild(buttonsDiv);
                list.appendChild(itemDiv);
            });
        }

        function showPlayerDetail(playerId) {
            const player = players.find(p => p.id === playerId);
            if (!player) return;
            
            const stats = player.stats;
            const transfoPct = stats.transformations.tentees > 0 ? 
                Math.round((stats.transformations.reussies / stats.transformations.tentees) * 100) : 0;
            const penalitePct = stats.penalites.tentees > 0 ? 
                Math.round((stats.penalites.reussies / stats.penalites.tentees) * 100) : 0;
            const totalMinutes = Math.floor(stats.tempsTotal / 60);
            const avgPoints = stats.totalMatches > 0 ? (stats.totalPoints / stats.totalMatches).toFixed(1) : 0;
            
            document.getElementById('playerDetailName').textContent = player.name;
            document.getElementById('playerDetailBody').innerHTML = `
                <div class="mini-stat">
                    <div class="mini-stat-label">Matchs joués</div>
                    <div class="mini-stat-value">${stats.totalMatches}</div>
                </div>

                <div class="mini-stat">
                    <div class="mini-stat-label">Points marqués</div>
                    <div class="mini-stat-value">${stats.totalPoints}</div>
                </div>

                <div class="mini-stat">
                    <div class="mini-stat-label">Moyenne points/match</div>
                    <div class="mini-stat-value">${avgPoints}</div>
                </div>

                <div class="mini-stat">
                    <div class="mini-stat-label">🏉 Essais marqués</div>
                    <div class="mini-stat-value">${stats.essais}</div>
                </div>

                <h4 style="color: #dc3545; margin: 25px 0 15px 0;">Précision au pied</h4>

                <div class="mini-stat">
                    <div class="mini-stat-label">🎯 Transformations</div>
                    <div class="mini-stat-value" style="font-size: 18px;">
                        ${stats.transformations.reussies}/${stats.transformations.tentees}
                        <span style="color: ${transfoPct >= 70 ? '#28a745' : transfoPct >= 50 ? '#ffc107' : '#dc3545'}; margin-left: 10px;">${transfoPct}%</span>
                    </div>
                    <div style="background: #e0e0e0; height: 10px; border-radius: 5px; overflow: hidden; margin-top: 8px;">
                        <div style="background: ${transfoPct >= 70 ? '#28a745' : transfoPct >= 50 ? '#ffc107' : '#dc3545'}; height: 100%; width: ${transfoPct}%; transition: width 0.3s;"></div>
                    </div>
                </div>

                <div class="mini-stat">
                    <div class="mini-stat-label">🥅 Pénalités</div>
                    <div class="mini-stat-value" style="font-size: 18px;">
                        ${stats.penalites.reussies}/${stats.penalites.tentees}
                        <span style="color: ${penalitePct >= 70 ? '#28a745' : penalitePct >= 50 ? '#ffc107' : '#dc3545'}; margin-left: 10px;">${penalitePct}%</span>
                    </div>
                    <div style="background: #e0e0e0; height: 10px; border-radius: 5px; overflow: hidden; margin-top: 8px;">
                        <div style="background: ${penalitePct >= 70 ? '#28a745' : penalitePct >= 50 ? '#ffc107' : '#dc3545'}; height: 100%; width: ${penalitePct}%; transition: width 0.3s;"></div>
                    </div>
                </div>

                <h4 style="color: #dc3545; margin: 25px 0 15px 0;">Temps de jeu & Discipline</h4>

                <div class="mini-stat">
                    <div class="mini-stat-label">⏱️ Temps de jeu total</div>
                    <div class="mini-stat-value">${totalMinutes} min</div>
                </div>

                <div class="mini-stat">
                    <div class="mini-stat-label">Cartons</div>
                    <div style="display: flex; gap: 20px; margin-top: 10px;">
                        <div style="text-align: center;">
                            <div style="font-size: 24px;">🟨</div>
                            <div style="font-size: 20px; font-weight: bold; color: #ffc107;">${stats.cartonsJaunes}</div>
                        </div>
                        <div style="text-align: center;">
                            <div style="font-size: 24px;">🟥</div>
                            <div style="font-size: 20px; font-weight: bold; color: #dc3545;">${stats.cartonsRouges}</div>
                        </div>
                    </div>
                </div>
            `;
            
            document.getElementById('playerDetailPanel').classList.add('active');
            document.getElementById('panelOverlay').classList.add('active');
        }

        function closePlayerDetail() {
            document.getElementById('playerDetailPanel').classList.remove('active');
            document.getElementById('panelOverlay').classList.remove('active');
        }

        // Statistiques globales
        function renderGlobalStats() {
            const finishedMatches = matches.filter(m => m.finished);
            
            // Calculs globaux
            let totalPoints = 0;
            let totalEssais = 0;
            let totalTransfoReussies = 0;
            let totalTransfoTentees = 0;
            let totalPenaliteReussies = 0;
            let totalPenaliteTentees = 0;
            
            finishedMatches.forEach(match => {
                totalPoints += match.score;
                match.events.forEach(e => {
                    if (e.type === 'essai') totalEssais++;
                    if (e.type === 'transformation') {
                        totalTransfoTentees++;
                        if (e.success) totalTransfoReussies++;
                    }
                    if (e.type === 'penalite') {
                        totalPenaliteTentees++;
                        if (e.success) totalPenaliteReussies++;
                    }
                });
            });
            
            const avgScore = finishedMatches.length > 0 ? Math.round(totalPoints / finishedMatches.length) : 0;
            const transfoRate = totalTransfoTentees > 0 ? Math.round((totalTransfoReussies / totalTransfoTentees) * 100) : 0;
            const penaliteRate = totalPenaliteTentees > 0 ? Math.round((totalPenaliteReussies / totalPenaliteTentees) * 100) : 0;
            
            document.getElementById('globalTotalMatches').textContent = finishedMatches.length;
            document.getElementById('globalTotalPoints').textContent = totalPoints;
            document.getElementById('globalTotalEssais').textContent = totalEssais;
            document.getElementById('globalTotalTransformations').textContent = totalTransfoReussies;
            document.getElementById('globalTotalPenalites').textContent = totalPenaliteReussies;
            document.getElementById('globalTransfoRate').textContent = transfoRate + '%';
            document.getElementById('globalPenaliteRate').textContent = penaliteRate + '%';
            document.getElementById('globalAverageScore').textContent = avgScore;
            
            // Meilleurs marqueurs
            const scorers = {};
            players.forEach(p => {
                if (p.stats.totalPoints > 0) {
                    scorers[p.name] = p.stats.totalPoints;
                }
            });
            
            const sortedScorers = Object.entries(scorers).sort((a, b) => b[1] - a[1]).slice(0, 5);
            const topScorersDiv = document.getElementById('topScorers');
            topScorersDiv.innerHTML = sortedScorers.length > 0 ? sortedScorers.map(([name, points], index) => {
                const maxPoints = sortedScorers[0][1];
                const barWidth = (points / maxPoints) * 100;
                return `
                    <div class="player-stat-item">
                        <div style="flex: 1;">
                            <strong>${index + 1}. ${name}</strong>
                            <div style="background: #e0e0e0; height: 20px; border-radius: 10px; margin-top: 5px; overflow: hidden;">
                                <div style="background: linear-gradient(135deg, #dc3545, #8b0000); height: 100%; width: ${barWidth}%; transition: width 0.3s;"></div>
                            </div>
                        </div>
                        <div style="font-size: 24px; font-weight: bold; color: #dc3545; margin-left: 20px;">
                            ${points}
                        </div>
                    </div>
                `;
            }).join('') : '<p>Aucun point marqué</p>';
            
            // Meilleurs buteurs
            const kickers = {};
            players.forEach(p => {
                const total = p.stats.transformations.reussies + p.stats.penalites.reussies;
                if (total > 0) {
                    kickers[p.name] = total;
                }
            });
            
            const sortedKickers = Object.entries(kickers).sort((a, b) => b[1] - a[1]).slice(0, 5);
            const topKickersDiv = document.getElementById('topKickers');
            topKickersDiv.innerHTML = sortedKickers.length > 0 ? sortedKickers.map(([name, kicks], index) => {
                const maxKicks = sortedKickers[0][1];
                const barWidth = (kicks / maxKicks) * 100;
                return `
                    <div class="player-stat-item">
                        <div style="flex: 1;">
                            <strong>${index + 1}. ${name}</strong>
                            <div style="background: #e0e0e0; height: 20px; border-radius: 10px; margin-top: 5px; overflow: hidden;">
                                <div style="background: linear-gradient(135deg, #17a2b8, #117a8b); height: 100%; width: ${barWidth}%; transition: width 0.3s;"></div>
                            </div>
                        </div>
                        <div style="font-size: 24px; font-weight: bold; color: #17a2b8; margin-left: 20px;">
                            ${kicks}
                        </div>
                    </div>
                `;
            }).join('') : '<p>Aucun coup de pied réussi</p>';
            
            // Temps de jeu
            const playTimes = {};
            players.forEach(p => {
                if (p.stats.tempsTotal > 0) {
                    playTimes[p.name] = Math.floor(p.stats.tempsTotal / 60);
                }
            });
            
            const sortedPlayTimes = Object.entries(playTimes).sort((a, b) => b[1] - a[1]).slice(0, 10);
            const playTimeChartDiv = document.getElementById('playTimeChart');
            playTimeChartDiv.innerHTML = sortedPlayTimes.length > 0 ? sortedPlayTimes.map(([name, minutes]) => {
                const maxMinutes = sortedPlayTimes[0][1];
                const barWidth = (minutes / maxMinutes) * 100;
                return `
                    <div class="player-stat-item">
                        <div style="flex: 1;">
                            <strong>${name}</strong>
                            <div style="background: #e0e0e0; height: 20px; border-radius: 10px; margin-top: 5px; overflow: hidden;">
                                <div style="background: linear-gradient(135deg, #28a745, #1e7e34); height: 100%; width: ${barWidth}%; transition: width 0.3s;"></div>
                            </div>
                        </div>
                        <div style="font-size: 18px; font-weight: bold; color: #28a745; margin-left: 20px;">
                            ${minutes} min
                        </div>
                    </div>
                `;
            }).join('') : '<p>Aucun temps de jeu enregistré</p>';
            
            // Historique des matchs
            const matchHistoryDiv = document.getElementById('matchHistory');
            matchHistoryDiv.innerHTML = finishedMatches.length > 0 ? finishedMatches.map(match => {
                const essais = match.events.filter(e => e.type === 'essai').length;
                const transfos = match.events.filter(e => e.type === 'transformation' && e.success).length;
                const penalites = match.events.filter(e => e.type === 'penalite' && e.success).length;
                
                return `
                    <div class="match-item">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div>
                                <h3 style="color: #dc3545;">${match.adversaire}</h3>
                                <p>📅 ${new Date(match.date).toLocaleDateString('fr-FR')} - 📍 ${match.lieu || 'Lieu non précisé'}</p>
                            </div>
                            <div style="text-align: center;">
                                <div style="font-size: 48px; font-weight: bold; color: #dc3545;">${match.score}</div>
                                <div style="font-size: 12px; color: #666;">
                                    ${essais} essais | ${transfos} transfo | ${penalites} péna
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }).join('') : '<p>Aucun match terminé</p>';
        }

        function deletePlayer(id) {
            if (confirm('Supprimer ce joueur ?')) {
                players = players.filter(p => p.id !== id);
                saveData();
                renderPlayersStats();
                renderComposition();
            }
        }

        // Composition
        function renderComposition() {
            for (let i = 1; i <= 23; i++) {
                const select = document.getElementById(`pos${i}`);
                if (select) {
                    select.innerHTML = '<option value="">Sélectionner</option>' + 
                        players.map(p => `<option value="${p.id}" ${composition[i] == p.id ? 'selected' : ''}>#${p.number} - ${p.name}</option>`).join('');
                }
            }
        }

        function saveComposition() {
            for (let i = 1; i <= 23; i++) {
                const select = document.getElementById(`pos${i}`);
                if (select && select.value) {
                    composition[i] = parseInt(select.value);
                }
            }
            saveData();
            
            // Si un match est en cours (non terminé), mettre à jour les joueurs
            if (currentMatch && !currentMatch.finished) {
                updateCurrentMatchPlayers();
            }
        }

        function updateCurrentMatchPlayers() {
            // Mettre à jour la liste des joueurs du match en cours
            const newSelectedPlayers = [];
            for (let i = 1; i <= 23; i++) {
                if (composition[i]) {
                    const player = players.find(p => p.id === composition[i]);
                    if (player) {
                        // Chercher si ce joueur était déjà dans le match
                        const existingPlayer = currentMatch.players.find(p => p.id === player.id);
                        
                        if (existingPlayer) {
                            // Garder les stats existantes
                            newSelectedPlayers.push(existingPlayer);
                        } else {
                            // Nouveau joueur
                            newSelectedPlayers.push({
                                ...player,
                                positionNumber: i,
                                timeOn: i <= 15 ? timerSeconds : null,
                                totalTime: 0,
                                cartons: [],
                                points: 0
                            });
                        }
                    }
                }
            }
            
            currentMatch.players = newSelectedPlayers;
            saveMatchData();
            if (document.getElementById('matchLive').style.display === 'block') {
                renderPlayersStatsTable();
            }
        }

        // Matchs
        function createMatch() {
            const adversaire = document.getElementById('adversaire').value;
            const date = document.getElementById('matchDate').value;
            const lieu = document.getElementById('lieu').value;
            
            if (!adversaire || !date) {
                alert('Veuillez remplir au moins l\'adversaire et la date');
                return;
            }
            
            const selectedPlayers = [];
            for (let i = 1; i <= 23; i++) {
                if (composition[i]) {
                    const player = players.find(p => p.id === composition[i]);
                    if (player) {
                        selectedPlayers.push({
                            ...player,
                            positionNumber: i,
                            timeOn: i <= 15 ? 0 : null,
                            totalTime: 0,
                            cartons: [],
                            points: 0
                        });
                    }
                }
            }
            
            const match = {
                id: Date.now(),
                adversaire,
                date,
                lieu,
                score: 0,
                events: [],
                players: selectedPlayers,
                finished: false,
                currentTime: 0
            };
            
            matches.push(match);
            saveData();
            renderMatches();
            
            document.getElementById('adversaire').value = '';
            document.getElementById('matchDate').value = '';
            document.getElementById('lieu').value = '';
        }

        function renderMatches() {
            const list = document.getElementById('matchesList');
            list.innerHTML = matches.map(m => `
                <div class="match-item" style="display: flex; justify-content: space-between; align-items: center;">
                    <div onclick="openMatch(${m.id})" style="flex: 1; cursor: pointer;">
                        <h3>${m.adversaire}</h3>
                        <p>📅 ${new Date(m.date).toLocaleDateString('fr-FR')}</p>
                        <p>📍 ${m.lieu || 'Lieu non précisé'}</p>
                        ${m.finished ? `<p><strong>Score final: ${m.score}</strong></p>` : '<p>Match à jouer</p>'}
                    </div>
                    <button class="btn" style="background: #6c757d; margin-left: 10px;" onclick="deleteMatchClick(event, ${m.id})">Supprimer</button>
                </div>
            `).join('');
        }

        function deleteMatchClick(e, matchId) {
            e.stopPropagation();
            deleteMatch(matchId);
        }

        function openMatch(matchId) {
            // Récupérer le match depuis le tableau pour avoir les dernières données
            const match = matches.find(m => m.id === matchId);
            currentMatch = match;
            
            if (currentMatch.finished) {
                showDebrief();
            } else {
                document.getElementById('matchsList').style.display = 'none';
                document.getElementById('matchLive').style.display = 'block';
                document.getElementById('matchTitle').textContent = `vs ${currentMatch.adversaire}`;
                document.getElementById('scoreDisplay').textContent = currentMatch.score;
                
                // Restaurer le temps du match (qui continue en arrière-plan)
                if (currentMatch.currentTime !== undefined) {
                    timerSeconds = currentMatch.currentTime;
                }
                
                updateTimer();
                renderEventsList();
                renderPlayersStatsTable();
            }
        }

        function deleteMatch(matchId) {
            if (confirm('Voulez-vous vraiment supprimer ce match ?')) {
                matches = matches.filter(m => m.id !== matchId);
                saveData();
                renderMatches();
            }
        }

        function backToMatches() {
            // Sauvegarder le temps actuel si le match n'est pas terminé
            if (currentMatch && !currentMatch.finished) {
                currentMatch.currentTime = timerSeconds;
                saveMatchData();
            }
            
            // Afficher la liste des matchs
            document.getElementById('matchsList').style.display = 'block';
            document.getElementById('matchLive').style.display = 'none';
            document.getElementById('matchDebrief').style.display = 'none';
            
            // Ne PAS réinitialiser currentMatch ni timerSeconds
            // Le timer continue en arrière-plan
            renderMatches();
        }

        // Timer
        function startTimer() {
            if (!timerRunning) {
                timerRunning = true;
                timerInterval = setInterval(() => {
                    timerSeconds++;
                    updateTimer();
                    updatePlayersTime();
                }, 1000);
            }
        }

        function pauseTimer() {
            timerRunning = false;
            if (timerInterval) {
                clearInterval(timerInterval);
            }
        }

        function resetTimer() {
            pauseTimer();
            timerSeconds = 0;
            updateTimer();
        }

        function updateTimer() {
            const minutes = Math.floor(timerSeconds / 60);
            const seconds = timerSeconds % 60;
            document.getElementById('timer').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        function updatePlayersTime() {
            if (currentMatch) {
                currentMatch.players.forEach(p => {
                    if (p.timeOn !== null) {
                        p.totalTime++;
                    }
                });
                
                // Sauvegarder le temps actuel du match
                currentMatch.currentTime = timerSeconds;
                saveMatchData();
            }
        }

        // Modal
        function openModal(type) {
            currentModalType = type;
            const modal = document.getElementById('modal');
            const modalTitle = document.getElementById('modalTitle');
            const modalBody = document.getElementById('modalBody');
            
            const activePlayers = currentMatch.players.filter(p => p.timeOn !== null);
            const minutes = Math.floor(timerSeconds / 60);
            const seconds = timerSeconds % 60;
            
            if (type === 'essai') {
                modalTitle.textContent = 'Essai marqué';
                modalBody.innerHTML = `
                    <label>Temps (minutes:secondes):</label>
                    <input type="text" id="eventTime" value="${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}" placeholder="00:00">
                    <label>Joueur:</label>
                    <select id="modalPlayerSelect">
                        <option value="">Sélectionner le joueur</option>
                        ${activePlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                `;
            } else if (type === 'transformation') {
                modalTitle.textContent = 'Transformation';
                modalBody.innerHTML = `
                    <label>Temps (minutes:secondes):</label>
                    <input type="text" id="eventTime" value="${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}" placeholder="00:00">
                    <label>Joueur:</label>
                    <select id="modalPlayerSelect">
                        <option value="">Sélectionner le joueur</option>
                        ${activePlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                    <div class="checkbox-group">
                        <input type="checkbox" id="transfoSuccess" checked>
                        <label for="transfoSuccess">Transformation réussie</label>
                    </div>
                `;
            } else if (type === 'penalite') {
                modalTitle.textContent = 'Pénalité';
                modalBody.innerHTML = `
                    <label>Temps (minutes:secondes):</label>
                    <input type="text" id="eventTime" value="${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}" placeholder="00:00">
                    <label>Joueur:</label>
                    <select id="modalPlayerSelect">
                        <option value="">Sélectionner le joueur</option>
                        ${activePlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                    <div class="checkbox-group">
                        <input type="checkbox" id="penaliteSuccess" checked>
                        <label for="penaliteSuccess">Pénalité réussie</label>
                    </div>
                `;
            } else if (type === 'carton') {
                modalTitle.textContent = 'Carton';
                modalBody.innerHTML = `
                    <label>Temps (minutes:secondes):</label>
                    <input type="text" id="eventTime" value="${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}" placeholder="00:00">
                    <label>Joueur:</label>
                    <select id="modalPlayerSelect">
                        <option value="">Sélectionner le joueur</option>
                        ${activePlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                    <label>Type de carton:</label>
                    <select id="cartonType">
                        <option value="jaune">Carton jaune</option>
                        <option value="rouge">Carton rouge</option>
                    </select>
                `;
            } else if (type === 'remplacement') {
                modalTitle.textContent = 'Remplacement';
                const benchPlayers = currentMatch.players.filter(p => p.timeOn === null);
                modalBody.innerHTML = `
                    <label>Temps (minutes:secondes):</label>
                    <input type="text" id="eventTime" value="${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}" placeholder="00:00">
                    <label>Joueur qui sort:</label>
                    <select id="playerOut">
                        <option value="">Sélectionner</option>
                        ${activePlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                    <label>Joueur qui entre:</label>
                    <select id="playerIn">
                        <option value="">Sélectionner</option>
                        ${benchPlayers.map(p => `<option value="${p.id}">#${p.number} - ${p.name}</option>`).join('')}
                    </select>
                `;
            }
            
            modal.classList.add('active');
        }

        function closeModal() {
            document.getElementById('modal').classList.remove('active');
        }

        function confirmModal() {
            const type = currentModalType;
            
            // Récupérer le temps saisi
            const eventTimeInput = document.getElementById('eventTime');
            let eventTime = timerSeconds;
            
            if (eventTimeInput) {
                const timeValue = eventTimeInput.value;
                const timeParts = timeValue.split(':');
                if (timeParts.length === 2) {
                    const mins = parseInt(timeParts[0]) || 0;
                    const secs = parseInt(timeParts[1]) || 0;
                    eventTime = mins * 60 + secs;
                }
            }
            
            if (type === 'essai') {
                const playerId = parseInt(document.getElementById('modalPlayerSelect').value);
                if (!playerId) {
                    alert('Veuillez sélectionner un joueur');
                    return;
                }
                
                currentMatch.score += 5;
                const player = currentMatch.players.find(p => p.id === playerId);
                player.points += 5;
                
                currentMatch.events.push({
                    type: 'essai',
                    time: eventTime,
                    player: player.name,
                    playerId: playerId,
                    points: 5
                });
                
            } else if (type === 'transformation') {
                const playerId = parseInt(document.getElementById('modalPlayerSelect').value);
                const success = document.getElementById('transfoSuccess').checked;
                
                if (!playerId) {
                    alert('Veuillez sélectionner un joueur');
                    return;
                }
                
                const player = currentMatch.players.find(p => p.id === playerId);
                
                if (success) {
                    currentMatch.score += 2;
                    player.points += 2;
                }
                
                currentMatch.events.push({
                    type: 'transformation',
                    time: eventTime,
                    player: player.name,
                    playerId: playerId,
                    points: success ? 2 : 0,
                    success: success
                });
                
            } else if (type === 'penalite') {
                const playerId = parseInt(document.getElementById('modalPlayerSelect').value);
                const success = document.getElementById('penaliteSuccess').checked;
                
                if (!playerId) {
                    alert('Veuillez sélectionner un joueur');
                    return;
                }
                
                const player = currentMatch.players.find(p => p.id === playerId);
                
                if (success) {
                    currentMatch.score += 3;
                    player.points += 3;
                }
                
                currentMatch.events.push({
                    type: 'penalite',
                    time: eventTime,
                    player: player.name,
                    playerId: playerId,
                    points: success ? 3 : 0,
                    success: success
                });
                
            } else if (type === 'carton') {
                const playerId = parseInt(document.getElementById('modalPlayerSelect').value);
                const cartonType = document.getElementById('cartonType').value;
                
                if (!playerId) {
                    alert('Veuillez sélectionner un joueur');
                    return;
                }
                
                const player = currentMatch.players.find(p => p.id === playerId);
                player.cartons.push({
                    type: cartonType,
                    time: eventTime
                });
                
                currentMatch.events.push({
                    type: 'carton',
                    cartonType: cartonType,
                    time: eventTime,
                    player: player.name,
                    playerId: playerId
                });
                
            } else if (type === 'remplacement') {
                const playerOutId = parseInt(document.getElementById('playerOut').value);
                const playerInId = parseInt(document.getElementById('playerIn').value);
                
                if (!playerOutId || !playerInId) {
                    alert('Veuillez sélectionner les deux joueurs');
                    return;
                }
                
                const playerOut = currentMatch.players.find(p => p.id === playerOutId);
                const playerIn = currentMatch.players.find(p => p.id === playerInId);
                
                playerOut.timeOn = null;
                playerIn.timeOn = eventTime;
                
                currentMatch.events.push({
                    type: 'remplacement',
                    time: eventTime,
                    playerOut: playerOut.name,
                    playerIn: playerIn.name
                });
            }
            
            saveMatchData();
            document.getElementById('scoreDisplay').textContent = currentMatch.score;
            renderEventsList();
            renderPlayersStatsTable();
            closeModal();
        }

        function saveMatchData() {
            if (currentMatch) {
                const matchIndex = matches.findIndex(m => m.id === currentMatch.id);
                if (matchIndex !== -1) {
                    matches[matchIndex] = currentMatch;
                    saveData();
                }
            }
        }

        function renderEventsList() {
            const list = document.getElementById('eventsList');
            list.innerHTML = '<h3 style="color: #dc3545;">Événements du match</h3>';
            
            const reversedEvents = [...currentMatch.events].reverse();
            
            reversedEvents.forEach((e, index) => {
                const actualIndex = currentMatch.events.length - 1 - index;
                const minutes = Math.floor(e.time / 60);
                const seconds = e.time % 60;
                const timeStr = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                
                const eventDiv = document.createElement('div');
                eventDiv.className = 'event-item';
                eventDiv.style.display = 'flex';
                eventDiv.style.justifyContent = 'space-between';
                eventDiv.style.alignItems = 'center';
                
                const textDiv = document.createElement('div');
                
                if (e.type === 'essai') {
                    textDiv.innerHTML = `⏱️ ${timeStr} - 🏉 <strong>Essai</strong> de ${e.player} (+5)`;
                } else if (e.type === 'transformation') {
                    const status = e.success ? '<span class="success-indicator">✓ Réussie</span>' : '<span class="fail-indicator">✗ Manquée</span>';
                    textDiv.innerHTML = `⏱️ ${timeStr} - 🎯 <strong>Transformation</strong> de ${e.player} ${status} ${e.success ? '(+2)' : ''}`;
                } else if (e.type === 'penalite') {
                    const status = e.success ? '<span class="success-indicator">✓ Réussie</span>' : '<span class="fail-indicator">✗ Manquée</span>';
                    textDiv.innerHTML = `⏱️ ${timeStr} - 🥅 <strong>Pénalité</strong> de ${e.player} ${status} ${e.success ? '(+3)' : ''}`;
                } else if (e.type === 'carton') {
                    const cartonEmoji = e.cartonType === 'jaune' ? '🟨' : '🟥';
                    textDiv.innerHTML = `⏱️ ${timeStr} - ${cartonEmoji} <strong>Carton ${e.cartonType}</strong> pour ${e.player}`;
                } else if (e.type === 'remplacement') {
                    textDiv.innerHTML = `⏱️ ${timeStr} - 🔄 <strong>Remplacement:</strong> ${e.playerOut} → ${e.playerIn}`;
                }
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'btn';
                deleteBtn.style.background = '#6c757d';
                deleteBtn.style.fontSize = '12px';
                deleteBtn.style.padding = '5px 10px';
                deleteBtn.textContent = 'Supprimer';
                deleteBtn.onclick = () => deleteEvent(actualIndex);
                
                eventDiv.appendChild(textDiv);
                eventDiv.appendChild(deleteBtn);
                list.appendChild(eventDiv);
            });
        }

        function deleteEvent(eventIndex) {
            if (!confirm('Supprimer cet événement ?')) {
                return;
            }
            
            const event = currentMatch.events[eventIndex];
            
            // Annuler les effets de l'événement
            if (event.type === 'essai') {
                currentMatch.score -= 5;
                const player = currentMatch.players.find(p => p.id === event.playerId);
                if (player) player.points -= 5;
            } else if (event.type === 'transformation' && event.success) {
                currentMatch.score -= 2;
                const player = currentMatch.players.find(p => p.id === event.playerId);
                if (player) player.points -= 2;
            } else if (event.type === 'penalite' && event.success) {
                currentMatch.score -= 3;
                const player = currentMatch.players.find(p => p.id === event.playerId);
                if (player) player.points -= 3;
            } else if (event.type === 'carton') {
                const player = currentMatch.players.find(p => p.id === event.playerId);
                if (player) {
                    player.cartons = player.cartons.filter(c => c.time !== event.time || c.type !== event.cartonType);
                }
            } else if (event.type === 'remplacement') {
                // Annuler le remplacement
                const playerOut = currentMatch.players.find(p => p.name === event.playerOut);
                const playerIn = currentMatch.players.find(p => p.name === event.playerIn);
                
                if (playerOut && playerIn) {
                    // Remettre le joueur sorti sur le terrain
                    playerOut.timeOn = 0;
                    // Remettre le joueur entré sur le banc
                    playerIn.timeOn = null;
                }
            }
            
            // Supprimer l'événement
            currentMatch.events.splice(eventIndex, 1);
            
            saveMatchData();
            document.getElementById('scoreDisplay').textContent = currentMatch.score;
            renderEventsList();
            renderPlayersStatsTable();
        }

        function renderPlayersStatsTable() {
            const tbody = document.getElementById('playersStatsTable');
            tbody.innerHTML = currentMatch.players.map(p => {
                const minutes = Math.floor(p.totalTime / 60);
                const seconds = p.totalTime % 60;
                const timeStr = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                
                const cartons = p.cartons.map(c => 
                    `<span class="carton-${c.type}">${c.type === 'jaune' ? '🟨' : '🟥'}</span>`
                ).join(' ');
                
                return `
                    <tr>
                        <td>#${p.number}</td>
                        <td>${p.name}</td>
                        <td>${timeStr}</td>
                        <td>${cartons || '-'}</td>
                        <td>${p.points}</td>
                    </tr>
                `;
            }).join('');
        }

        function endMatch() {
            if (!confirm('Voulez-vous vraiment terminer ce match ?')) {
                return;
            }
            
            pauseTimer();
            currentMatch.finished = true;
            currentMatch.finalTime = timerSeconds;
            
            // Mise à jour des stats des joueurs
            currentMatch.players.forEach(matchPlayer => {
                const player = players.find(p => p.id === matchPlayer.id);
                if (player) {
                    player.stats.totalMatches++;
                    player.stats.totalPoints += matchPlayer.points;
                    player.stats.tempsTotal += matchPlayer.totalTime;
                    
                    // Cartons
                    matchPlayer.cartons.forEach(c => {
                        if (c.type === 'jaune') player.stats.cartonsJaunes++;
                        else player.stats.cartonsRouges++;
                    });
                }
            });
            
            // Essais, transformations, pénalités
            currentMatch.events.forEach(e => {
                const player = players.find(p => p.id === e.playerId);
                if (player) {
                    if (e.type === 'essai') {
                        player.stats.essais++;
                    } else if (e.type === 'transformation') {
                        player.stats.transformations.tentees++;
                        if (e.success) player.stats.transformations.reussies++;
                    } else if (e.type === 'penalite') {
                        player.stats.penalites.tentees++;
                        if (e.success) player.stats.penalites.reussies++;
                    }
                }
            });
            
            saveMatchData();
            saveData();
            showDebrief();
        }

        function showDebrief() {
            document.getElementById('matchLive').style.display = 'none';
            document.getElementById('matchsList').style.display = 'none';
            document.getElementById('matchDebrief').style.display = 'block';
            
            document.getElementById('debriefTitle').textContent = `Débrief: vs ${currentMatch.adversaire}`;
            document.getElementById('debriefScore').textContent = currentMatch.score;
            
            const essais = currentMatch.events.filter(e => e.type === 'essai').length;
            const transformations = currentMatch.events.filter(e => e.type === 'transformation' && e.success).length;
            const penalites = currentMatch.events.filter(e => e.type === 'penalite' && e.success).length;
            
            document.getElementById('debriefEssais').textContent = essais;
            document.getElementById('debriefTransformations').textContent = transformations;
            document.getElementById('debriefPenalites').textContent = penalites;
            
            // Stats transformations par joueur
            const transfoStats = {};
            currentMatch.events.filter(e => e.type === 'transformation').forEach(e => {
                if (!transfoStats[e.player]) {
                    transfoStats[e.player] = { reussies: 0, tentees: 0 };
                }
                transfoStats[e.player].tentees++;
                if (e.success) transfoStats[e.player].reussies++;
            });
            
            const transfoDiv = document.getElementById('transformationStats');
            transfoDiv.innerHTML = Object.keys(transfoStats).length > 0 ? 
                Object.entries(transfoStats).map(([player, stats]) => {
                    const pct = Math.round((stats.reussies / stats.tentees) * 100);
                    return `
                        <div class="player-stat-item">
                            <div>
                                <strong>${player}</strong>: ${stats.reussies}/${stats.tentees} réussies
                            </div>
                            <div style="font-size: 24px; font-weight: bold; color: ${pct >= 70 ? '#28a745' : pct >= 50 ? '#ffc107' : '#dc3545'};">
                                ${pct}%
                            </div>
                        </div>
                    `;
                }).join('') : '<p>Aucune transformation tentée</p>';
            
            // Stats pénalités par joueur
            const penaliteStats = {};
            currentMatch.events.filter(e => e.type === 'penalite').forEach(e => {
                if (!penaliteStats[e.player]) {
                    penaliteStats[e.player] = { reussies: 0, tentees: 0 };
                }
                penaliteStats[e.player].tentees++;
                if (e.success) penaliteStats[e.player].reussies++;
            });
            
            const penaliteDiv = document.getElementById('penaliteStats');
            penaliteDiv.innerHTML = Object.keys(penaliteStats).length > 0 ? 
                Object.entries(penaliteStats).map(([player, stats]) => {
                    const pct = Math.round((stats.reussies / stats.tentees) * 100);
                    return `
                        <div class="player-stat-item">
                            <div>
                                <strong>${player}</strong>: ${stats.reussies}/${stats.tentees} réussies
                            </div>
                            <div style="font-size: 24px; font-weight: bold; color: ${pct >= 70 ? '#28a745' : pct >= 50 ? '#ffc107' : '#dc3545'};">
                                ${pct}%
                            </div>
                        </div>
                    `;
                }).join('') : '<p>Aucune pénalité tentée</p>';
            
            const eventsDiv = document.getElementById('debriefEvents');
            eventsDiv.innerHTML = currentMatch.events.map(e => {
                const minutes = Math.floor(e.time / 60);
                const seconds = e.time % 60;
                const timeStr = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                
                if (e.type === 'essai') {
                    return `<div class="event-item">⏱️ ${timeStr} - 🏉 Essai de ${e.player} (+5)</div>`;
                } else if (e.type === 'transformation') {
                    const status = e.success ? '✓ Réussie' : '✗ Manquée';
                    return `<div class="event-item">⏱️ ${timeStr} - 🎯 Transformation de ${e.player} ${status} ${e.success ? '(+2)' : ''}</div>`;
                } else if (e.type === 'penalite') {
                    const status = e.success ? '✓ Réussie' : '✗ Manquée';
                    return `<div class="event-item">⏱️ ${timeStr} - 🥅 Pénalité de ${e.player} ${status} ${e.success ? '(+3)' : ''}</div>`;
                } else if (e.type === 'carton') {
                    const cartonEmoji = e.cartonType === 'jaune' ? '🟨' : '🟥';
                    return `<div class="event-item">⏱️ ${timeStr} - ${cartonEmoji} Carton ${e.cartonType} pour ${e.player}</div>`;
                } else if (e.type === 'remplacement') {
                    return `<div class="event-item">⏱️ ${timeStr} - 🔄 ${e.playerOut} → ${e.playerIn}</div>`;
                }
            }).join('');
            
            const tbody = document.getElementById('debriefPlayersTable');
            tbody.innerHTML = currentMatch.players.map(p => {
                const minutes = Math.floor(p.totalTime / 60);
                const seconds = p.totalTime % 60;
                const timeStr = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                
                const cartons = p.cartons.map(c => 
                    `<span class="carton-${c.type}">${c.type === 'jaune' ? 'Jaune' : 'Rouge'}</span>`
                ).join(', ');
                
                return `
                    <tr>
                        <td>#${p.number} - ${p.name}</td>
                        <td>${timeStr}</td>
                        <td>${p.points}</td>
                        <td>${cartons || '-'}</td>
                    </tr>
                `;
            }).join('');
        }

        function exportToPDF() {
            window.print();
        }

        // Export/Import des données
        function exportData() {
            const data = {
                players: players,
                composition: composition,
                matches: matches,
                exportDate: new Date().toISOString(),
                version: '1.0'
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], { type: 'application/json' });
            
            const url = URL.createObjectURL(dataBlob);
            const link = document.createElement('a');
            link.href = url;
            link.download = `rugby-stats-${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            
            alert('✅ Données exportées avec succès !');
        }

        function importData(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    
                    // Validation basique
                    if (!data.players || !Array.isArray(data.players)) {
                        throw new Error('Format de données invalide');
                    }
                    
                    // Confirmation avant d'écraser les données
                    const confirm = window.confirm(
                        '⚠️ Attention ! L\'importation va remplacer toutes vos données actuelles.\n\n' +
                        `Données à importer:\n` +
                        `- ${data.players.length} joueurs\n` +
                        `- ${data.matches ? data.matches.length : 0} matchs\n\n` +
                        'Voulez-vous continuer ?'
                    );
                    
                    if (!confirm) {
                        event.target.value = ''; // Reset file input
                        return;
                    }
                    
                    // Importer les données
                    players = data.players || [];
                    composition = data.composition || {};
                    matches = data.matches || [];
                    
                    // Sauvegarder
                    saveData();
                    
                    // Rafraîchir l'affichage
                    renderPlayersStats();
                    renderComposition();
                    renderMatches();
                    
                    alert('✅ Données importées avec succès !');
                    
                    // Reset file input
                    event.target.value = '';
                    
                } catch (error) {
                    alert('❌ Erreur lors de l\'importation : ' + error.message);
                    event.target.value = '';
                }
            };
            
            reader.readAsText(file);
        }

        function clearAllData() {
            const confirm = window.confirm(
                '⚠️ ATTENTION ! Cette action va supprimer TOUTES les données :\n\n' +
                '- Tous les joueurs\n' +
                '- Tous les matchs\n' +
                '- Toutes les compositions\n' +
                '- Toutes les statistiques\n\n' +
                '⚠️ Cette action est IRRÉVERSIBLE !\n\n' +
                'Êtes-vous absolument sûr de vouloir tout réinitialiser ?'
            );
            
            if (!confirm) return;
            
            // Double confirmation
            const confirmAgain = window.confirm('Confirmez-vous vraiment la suppression totale de toutes les données ?');
            
            if (!confirmAgain) return;
            
            // Tout supprimer
            players = [];
            composition = {};
            matches = [];
            
            // Sauvegarder
            saveData();
            
            // Rafraîchir l'affichage
            renderPlayersStats();
            renderComposition();
            renderMatches();
            
            alert('✅ Toutes les données ont été supprimées.');
        }

        // Initialisation
        window.onload = function() {
            loadData();
            renderPlayersStats();
            renderComposition();
            renderMatches();
        };
    </script>
</body>
</html>
