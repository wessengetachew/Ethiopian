<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Sieve: π and ζ(2n) Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        .header {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ffd700, #ffed4e);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .subtitle {
            text-align: center;
            font-size: 1.1em;
            opacity: 0.9;
            margin-bottom: 20px;
        }
        
        .info-section {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 15px;
            margin-top: 15px;
            border-left: 4px solid #ffd700;
        }
        
        .info-section h3 {
            color: #ffd700;
            margin-bottom: 10px;
        }
        
        .info-section p {
            line-height: 1.6;
            margin-bottom: 10px;
        }
        
        .formula {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            margin: 10px 0;
            overflow-x: auto;
        }
        
        .main-content {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .control-group {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .control-group h3 {
            margin-bottom: 15px;
            color: #ffd700;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
            font-size: 0.9em;
        }
        
        input, select, button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 15px;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
        }
        
        button {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(238, 90, 82, 0.3);
        }
        
        .export-btn {
            background: linear-gradient(45deg, #4ecdc4, #44a8a3);
            margin-top: 10px;
        }
        
        .export-btn:hover {
            box-shadow: 0 10px 20px rgba(78, 205, 196, 0.3);
        }
        
        .results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .result-card {
            background: rgba(255, 255, 255, 0.08);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-card h4 {
            color: #ffd700;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
        
        .value {
            font-family: 'Courier New', monospace;
            font-size: 1.2em;
            background: rgba(0, 0, 0, 0.3);
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            word-break: break-all;
        }
        
        .error-info {
            font-size: 0.9em;
            opacity: 0.8;
            margin-top: 10px;
        }
        
        .step-by-step {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .step-by-step h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .step {
            background: rgba(255, 255, 255, 0.08);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 4px solid #4ecdc4;
        }
        
        .step-number {
            display: inline-block;
            background: #4ecdc4;
            color: #1e3c72;
            font-weight: bold;
            padding: 5px 12px;
            border-radius: 50%;
            margin-right: 10px;
        }
        
        .step-title {
            font-size: 1.1em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .step-content {
            margin-left: 40px;
            line-height: 1.6;
        }
        
        .step-formula {
            background: rgba(0, 0, 0, 0.4);
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
        }
        
        .gap-analysis {
            margin-top: 30px;
            background: rgba(30, 60, 114, 0.95);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .gap-analysis h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .gap-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }
        
        .gap-item {
            background: rgba(255, 255, 255, 0.15);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .gap-item:hover {
            background: rgba(255, 255, 255, 0.25);
            border-color: #4ecdc4;
            transform: translateY(-2px);
        }
        
        .gap-item.expanded {
            grid-column: 1 / -1;
            background: rgba(78, 205, 196, 0.2);
            border-color: #4ecdc4;
        }
        
        .gap-primes-list {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.3);
            display: none;
        }
        
        .gap-primes-list.visible {
            display: block;
        }
        
        .gap-primes-container {
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            border-radius: 8px;
            max-height: 400px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.8;
            text-align: left;
        }
        
        .gap-cumulative-section {
            margin-top: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            text-align: left;
        }
        
        .cumulative-step {
            padding: 8px;
            margin: 5px 0;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 5px;
            font-family: 'Courier New', monospace;
            font-size: 0.85em;
        }
        
        .gap-value {
            font-size: 1.1em;
            font-weight: bold;
            color: #4ecdc4;
        }
        
        .channel-analysis {
            margin-top: 30px;
            background: rgba(30, 60, 114, 0.95);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .channel-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .channel-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .channel-item:hover {
            background: rgba(255, 255, 255, 0.15);
            border-color: #4ecdc4;
            transform: translateY(-2px);
        }
        
        .channel-item.expanded {
            grid-column: 1 / -1;
            background: rgba(78, 205, 196, 0.1);
            border-color: #4ecdc4;
        }
        
        .channel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .channel-residue {
            font-size: 1.1em;
            font-weight: bold;
            color: #4ecdc4;
        }
        
        .channel-count {
            background: rgba(78, 205, 196, 0.2);
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.9em;
        }
        
        .channel-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }
        
        .stat-item {
            background: rgba(0, 0, 0, 0.2);
            padding: 8px;
            border-radius: 5px;
        }
        
        .stat-label {
            font-size: 0.8em;
            opacity: 0.8;
            margin-bottom: 3px;
        }
        
        .stat-value {
            font-size: 1em;
            font-weight: bold;
            color: #ffd700;
        }
        
        .primes-list {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            display: none;
        }
        
        .primes-list.visible {
            display: block;
        }
        
        .primes-list h4 {
            color: #ffd700;
            margin-bottom: 10px;
        }
        
        .primes-container {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 8px;
            max-height: 300px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.6;
        }
        
        .primes-container::-webkit-scrollbar {
            width: 8px;
        }
        
        .primes-container::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 4px;
        }
        
        .primes-container::-webkit-scrollbar-thumb {
            background: #4ecdc4;
            border-radius: 4px;
        }
        
        .expand-indicator {
            color: #4ecdc4;
            font-size: 0.8em;
            margin-top: 8px;
            text-align: center;
            opacity: 0.7;
        }
        
        .view-options {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .view-btn {
            padding: 8px 16px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9em;
        }
        
        .view-btn.active {
            background: #4ecdc4;
            border-color: #4ecdc4;
            color: #1e3c72;
        }
        
        .view-btn:hover {
            background: rgba(78, 205, 196, 0.3);
            border-color: #4ecdc4;
        }
        
        .distribution-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            overflow: hidden;
        }
        
        .distribution-table th {
            background: rgba(78, 205, 196, 0.3);
            padding: 12px;
            text-align: left;
            font-weight: bold;
            color: #ffd700;
        }
        
        .distribution-table td {
            padding: 10px 12px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(30, 60, 114, 0.4);
            color: #ffffff;
        }
        
        .distribution-table tr:hover {
            background: rgba(78, 205, 196, 0.2);
        }
        
        .distribution-table tr:hover td {
            background: rgba(78, 205, 196, 0.2);
        }
        
        .progress-bar {
            width: 100%;
            height: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            overflow: hidden;
            margin-top: 5px;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4, #44a8a3);
            transition: width 0.3s ease;
        }
        
        .chart-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .chart-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
            text-align: center;
        }
        
        #channelChart {
            width: 100%;
            height: 400px;
            max-height: 400px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        
        .chart-legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
            font-size: 0.9em;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 2px;
        }
        
        .visualization-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .visualization-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .viz-options {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .viz-btn {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .viz-btn.active {
            background: #4ecdc4;
            border-color: #4ecdc4;
            color: #1e3c72;
        }
        
        .viz-btn:hover {
            background: rgba(78, 205, 196, 0.3);
            border-color: #4ecdc4;
        }
        
        #vizCanvas {
            width: 100%;
            height: 500px;
            max-height: 500px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        
        .loading {
            text-align: center;
            font-style: italic;
            opacity: 0.7;
        }
        
        .toggle-section {
            cursor: pointer;
            user-select: none;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
        .toggle-icon {
            transition: transform 0.3s ease;
        }
        
        .toggle-icon.open {
            transform: rotate(180deg);
        }
        
        .collapsible-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease;
        }
        
        .collapsible-content.open {
            max-height: 5000px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Modular Sieve Calculator</h1>
            <div class="subtitle">Computing π and ζ(2n) via Gap-Class and Residue-Channel Decompositions</div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('theory')">
                    <h3>Mathematical Framework</h3>
                    <span class="toggle-icon" id="theory-icon">▼</span>
                </div>
                <div id="theory-content" class="collapsible-content">
                    <p>This calculator implements the rigorous framework for computing π and ζ(2n) using Euler product decompositions.</p>
                    
                    <p><strong>Key Identity:</strong> For ℜ(s) > 1, the Riemann zeta function has the Euler product:</p>
                    <div class="formula">ζ(s) = ∏<sub>p prime</sub> (1 - p<sup>-s</sup>)<sup>-1</sup></div>
                    
                    <p><strong>Recovering π:</strong> Since ζ(2) = π²/6, we have:</p>
                    <div class="formula">π = √6 · ∏<sub>p prime</sub> (1 - p<sup>-2</sup>)<sup>-1/2</sup></div>
                    
                    <p><strong>Two Decomposition Methods:</strong></p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>Gap-Class:</strong> Groups primes by their gaps g(p) = p - p<sub>prev</sub></li>
                        <li><strong>Residue Channels:</strong> Splits primes by residue classes mod m, giving φ(m) independent channels for gcd(a,m)=1. Default uses m=30 with 8 channels, but supports any modulus.</li>
                    </ul>
                    
                    <p style="margin-top: 15px;"><strong>Error Control:</strong> For target error ε, include primes up to:</p>
                    <div class="formula">
                        Y ≈ 1 + 1/ε  (for π)<br>
                        Y ≈ (2/((2n-1)·ε))<sup>1/(2n-1)</sup>  (for ζ(2n))
                    </div>
                </div>
            </div>
        </div>
        
        <div class="main-content">
            <div class="controls">
                <div class="control-group">
                    <h3>Target Accuracy</h3>
                    <label for="epsilon">Relative Error (ε):</label>
                    <input type="number" id="epsilon" value="1" step="0.0001" min="0.0001" max="10">
                    
                    <div style="margin-bottom: 15px;">
                        <label style="font-size: 0.9em; opacity: 0.9;">Quick Presets:</label>
                        <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin-top: 8px;">
                            <button onclick="setEpsilon(0.01)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">1% (0.01)</button>
                            <button onclick="setEpsilon(0.0001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">0.01% (10⁻⁴)</button>
                            <button onclick="setEpsilon(0.0000001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">10⁻⁷</button>
                            <button onclick="setEpsilon(0.000000000001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">10⁻¹²</button>
                        </div>
                    </div>
                    
                    <label for="constant">Constant to Compute:</label>
                    <select id="constant">
                        <option value="pi">π (from ζ(2))</option>
                        <option value="zeta4">ζ(4)</option>
                        <option value="zeta6">ζ(6)</option>
                        <option value="zeta8">ζ(8)</option>
                        <option value="zeta10">ζ(10)</option>
                    </select>
                    
                    <label for="modulus">Modulus for Residue Channels:</label>
                    <input type="number" id="modulus" value="30" min="2" max="210" step="1">
                    <div style="font-size: 0.85em; opacity: 0.8; margin-top: -10px;">
                        φ(m) channels for gcd(a,m)=1. Try: 6, 12, 30, 60, 210
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>Computation Method</h3>
                    <label for="method">Decomposition:</label>
                    <select id="method">
                        <option value="standard">Standard Euler Product</option>
                        <option value="gap">Gap-Class Analysis</option>
                        <option value="residue">Residue Channels (Custom Mod)</option>
                        <option value="both">Gap + Residue Combined</option>
                    </select>
                    
                    <label>
                        <input type="checkbox" id="showSteps" checked style="width: auto; margin-right: 10px;">
                        Show Step-by-Step Work
                    </label>
                </div>
                
                <div class="control-group">
                    <h3>Actions</h3>
                    <button onclick="compute()">Calculate</button>
                    <button class="export-btn" onclick="exportResults()">Export Results (JSON)</button>
                    <button class="export-btn" onclick="exportStepsText()">Export Steps (TXT)</button>
                    <button class="export-btn" onclick="exportChartImage()">Export Chart (4K/8K JPEG)</button>
                </div>
            </div>
            
            <div id="results" class="results" style="display: none;">
                <div class="result-card">
                    <h4>Computed Value</h4>
                    <div id="computed-value" class="value"></div>
                    <div id="error-bound" class="error-info"></div>
                    <div id="prime-count" class="error-info"></div>
                </div>
                
                <div class="result-card">
                    <h4>Exact Reference</h4>
                    <div id="exact-value" class="value"></div>
                    <div id="actual-error" class="error-info"></div>
                </div>
            </div>
            
            <div id="step-by-step" class="step-by-step" style="display: none;"></div>
            
            <div id="gap-analysis" class="gap-analysis" style="display: none;">
                <h3>Gap-Class Decomposition</h3>
                <div id="gap-grid" class="gap-grid"></div>
            </div>
            
            <div id="channel-analysis" class="channel-analysis" style="display: none;">
                <h3>Residue Channel Analysis</h3>
                <div class="view-options">
                    <button class="view-btn active" onclick="changeChannelView('cards')">Card View</button>
                    <button class="view-btn" onclick="changeChannelView('table')">Table View</button>
                    <button class="view-btn" onclick="changeChannelView('distribution')">Distribution Chart</button>
                </div>
                <div id="channel-content"></div>
            </div>
            
            <div id="chart-section" class="chart-container" style="display: none;">
                <h3>Residue Channel Contributions (ℤ<sub>a</sub>(s;30))</h3>
                <canvas id="channelChart"></canvas>
                <div class="chart-legend" id="chartLegend"></div>
            </div>
            
            <div id="visualization-section" class="visualization-container" style="display: none;">
                <h3>Interactive Visualization</h3>
                <div class="viz-options">
                    <button class="viz-btn active" onclick="changeViz('convergence')">Convergence Plot</button>
                    <button class="viz-btn" onclick="changeViz('contribution')">Prime Contributions</button>
                    <button class="viz-btn" onclick="changeViz('gapDist')">Gap Distribution</button>
                </div>
                <canvas id="vizCanvas"></canvas>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <script>
        // Compute Euler's totient function
        function eulerPhi(n) {
            let result = n;
            for (let p = 2; p * p <= n; p++) {
                if (n % p === 0) {
                    while (n % p === 0) n /= p;
                    result -= result / p;
                }
            }
            if (n > 1) result -= result / n;
            return result;
        }
        
        // Get coprime residues mod m
        function getCoprimeResidues(m) {
            const residues = [];
            for (let a = 1; a < m; a++) {
                if (gcd(a, m) === 1) {
                    residues.push(a);
                }
            }
            return residues;
        }
        
        // GCD helper
        function gcd(a, b) {
            while (b !== 0) {
                const temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }
        
        let computationData = null;
        let channelChart = null;
        let vizChart = null;
        let currentViz = 'convergence';
        let currentChannelView = 'cards';
        let channelDataGlobal = null;
        
        function setEpsilon(value) {
            document.getElementById('epsilon').value = value;
            // Visual feedback
            const epsilonInput = document.getElementById('epsilon');
            epsilonInput.style.background = 'rgba(78, 205, 196, 0.3)';
            setTimeout(() => {
                epsilonInput.style.background = 'rgba(255, 255, 255, 0.9)';
            }, 300);
        }
        
        function toggleSection(id) {
            const content = document.getElementById(id + '-content');
            const icon = document.getElementById(id + '-icon');
            content.classList.toggle('open');
            icon.classList.toggle('open');
        }
        
        // Sieve of Eratosthenes
        function sieveOfEratosthenes(limit) {
            if (limit < 2) return [];
            
            const isPrime = new Array(limit + 1).fill(true);
            isPrime[0] = isPrime[1] = false;
            
            for (let i = 2; i * i <= limit; i++) {
                if (isPrime[i]) {
                    for (let j = i * i; j <= limit; j += i) {
                        isPrime[j] = false;
                    }
                }
            }
            
            const primes = [];
            for (let i = 2; i <= limit; i++) {
                if (isPrime[i]) primes.push(i);
            }
            return primes;
        }
        
        // Compute gap classes
        function computeGapClasses(primes) {
            const gapClasses = {};
            
            for (let i = 1; i < primes.length; i++) {
                const gap = primes[i] - primes[i-1];
                if (!gapClasses[gap]) gapClasses[gap] = [];
                gapClasses[gap].push(primes[i]);
            }
            
            return gapClasses;
        }
        
        // Compute residue channels for any modulus
        function computeResidueChannels(primes, modulus) {
            const coprimeResidues = getCoprimeResidues(modulus);
            const channels = {};
            
            coprimeResidues.forEach(a => channels[a] = []);
            
            primes.forEach(p => {
                if (p >= modulus) {
                    const residue = p % modulus;
                    if (coprimeResidues.includes(residue)) {
                        channels[residue].push(p);
                    }
                }
            });
            
            return channels;
        }
        
        // Compute Y cutoff
        function computeCutoff(epsilon, constantType) {
            if (constantType === 'pi') {
                return Math.ceil(1 + 1 / Math.log(1 + epsilon));
            } else {
                const n = parseInt(constantType.replace('zeta', '')) / 2;
                const power = 1 / (2 * n - 1);
                return Math.ceil(Math.pow(2 / ((2 * n - 1) * Math.log(1 + epsilon)), power));
            }
        }
        
        // Compute truncated product
        function computeTruncatedProduct(primes, exponent) {
            let product = 1;
            for (const p of primes) {
                product *= 1 / (1 - Math.pow(p, -exponent));
            }
            return product;
        }
        
        // Compute partial products (for convergence visualization)
        function computePartialProducts(primes, exponent) {
            const partials = [];
            let product = 1;
            
            for (const p of primes) {
                product *= 1 / (1 - Math.pow(p, -exponent));
                partials.push({ prime: p, value: product });
            }
            
            return partials;
        }
        
        // Exact values
        const exactValues = {
            'pi': Math.PI,
            'zeta4': Math.PI ** 4 / 90,
            'zeta6': Math.PI ** 6 / 945,
            'zeta8': Math.PI ** 8 / 9450,
            'zeta10': Math.PI ** 10 / 93555
        };
        
        function compute() {
            const epsilon = parseFloat(document.getElementById('epsilon').value);
            const constantType = document.getElementById('constant').value;
            const method = document.getElementById('method').value;
            const showSteps = document.getElementById('showSteps').checked;
            const modulus = parseInt(document.getElementById('modulus').value);
            
            document.getElementById('results').style.display = 'block';
            document.getElementById('computed-value').innerHTML = '<div class="loading">Computing...</div>';
            
            setTimeout(() => {
                try {
                    const Y = computeCutoff(epsilon, constantType);
                    const primes = sieveOfEratosthenes(Y - 1);
                    
                    let computedValue;
                    const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
                    
                    if (constantType === 'pi') {
                        const zetaProduct = computeTruncatedProduct(primes, 2);
                        computedValue = Math.sqrt(6 * zetaProduct);
                    } else {
                        const n = parseInt(constantType.replace('zeta', '')) / 2;
                        computedValue = computeTruncatedProduct(primes, 2 * n);
                    }
                    
                    // Store computation data
                    computationData = {
                        epsilon,
                        constantType,
                        method,
                        modulus,
                        Y,
                        primes,
                        exponent,
                        computedValue,
                        exactValue: exactValues[constantType],
                        partialProducts: computePartialProducts(primes, constantType === 'pi' ? 2 : exponent)
                    };
                    
                    // Display results
                    document.getElementById('computed-value').textContent = computedValue.toFixed(15);
                    document.getElementById('exact-value').textContent = exactValues[constantType].toFixed(15);
                    
                    const actualError = Math.abs(computedValue - exactValues[constantType]) / exactValues[constantType];
                    document.getElementById('actual-error').innerHTML = `Actual relative error: <strong>${(actualError * 100).toFixed(8)}%</strong>`;
                    document.getElementById('error-bound').innerHTML = `Guaranteed error ≤ <strong>${(epsilon * 100).toFixed(4)}%</strong>`;
                    document.getElementById('prime-count').innerHTML = `Using <strong>${primes.length}</strong> primes up to <strong>${Y-1}</strong>`;
                    
                    // Show step-by-step
                    if (showSteps) {
                        showStepByStep(computationData);
                    } else {
                        document.getElementById('step-by-step').style.display = 'none';
                    }
                    
                    // Method-specific analysis
                    if (method === 'gap' || method === 'both') {
                        showGapAnalysis(primes, constantType);
                    } else {
                        document.getElementById('gap-analysis').style.display = 'none';
                    }
                    
                    if (method === 'residue' || method === 'both') {
                        showResidueAnalysis(primes, constantType, modulus);
                    } else {
                        document.getElementById('channel-analysis').style.display = 'none';
                        document.getElementById('chart-section').style.display = 'none';
                    }
                    
                    // Show visualization
                    document.getElementById('visualization-section').style.display = 'block';
                    updateVisualization(currentViz);
                    
                } catch (error) {
                    document.getElementById('computed-value').innerHTML = `<span style="color: #ff6b6b;">Error: ${error.message}</span>`;
                }
            }, 100);
        }
        
        function showStepByStep(data) {
            const { epsilon, constantType, Y, primes, exponent, computedValue, exactValue } = data;
            
            let html = '<h3>Step-by-Step Calculation</h3>';
            
            // Step 1: Determine cutoff
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">1</span>Determine Required Cutoff Y</div>
                    <div class="step-content">
                        <p>Given target relative error ε = ${epsilon}</p>
                        ${constantType === 'pi' ? `
                            <p>For π, we use: Y = ⌈1 + 1/log(1+ε)⌉</p>
                            <div class="step-formula">
                                Y = ⌈1 + 1/log(1+${epsilon})⌉<br>
                                Y = ⌈1 + ${(1/Math.log(1+epsilon)).toFixed(4)}⌉<br>
                                Y = ${Y}
                            </div>
                        ` : `
                            <p>For ζ(${exponent}), we use: Y = ⌈(2/((2n-1)·log(1+ε)))<sup>1/(2n-1)</sup>⌉ where n = ${exponent/2}</p>
                            <div class="step-formula">
                                Y = ⌈(2/(${exponent-1}·log(1+${epsilon})))<sup>1/${exponent-1}</sup>⌉<br>
                                Y = ${Y}
                            </div>
                        `}
                        <p>Therefore, we need all primes up to ${Y-1}.</p>
                    </div>
                </div>
            `;
            
            // Step 2: Generate primes
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">2</span>Generate Primes Using Sieve</div>
                    <div class="step-content">
                        <p>Using the Sieve of Eratosthenes to find all primes ≤ ${Y-1}:</p>
                        <p><strong>Found ${primes.length} primes:</strong></p>
                        <div class="step-formula">
                            {${primes.slice(0, 20).join(', ')}${primes.length > 20 ? ', ..., ' + primes[primes.length-1] : ''}}
                        </div>
                    </div>
                </div>
            `;
            
            // Step 3: Compute Euler product
            const firstFewFactors = primes.slice(0, 5).map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return `(1 - ${p}<sup>-${exponent}</sup>)<sup>-1</sup> = ${factor.toFixed(6)}`;
            }).join('<br>');
            
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">3</span>Compute Euler Product</div>
                    <div class="step-content">
                        <p>${constantType === 'pi' ? 'For π, compute ζ(2) = ∏(1-p<sup>-2</sup>)<sup>-1</sup>' : `Compute ζ(${exponent}) = ∏(1-p<sup>-${exponent}</sup>)<sup>-1</sup>`}</p>
                        <p><strong>First few factors:</strong></p>
                        <div class="step-formula">${firstFewFactors}</div>
                        <p><strong>Product of all ${primes.length} factors:</strong></p>
                        <div class="step-formula">
                            ${constantType === 'pi' ? 'ζ(2) = ' : `ζ(${exponent}) = `}${computeTruncatedProduct(primes, exponent).toFixed(12)}
                        </div>
                    </div>
                </div>
            `;
            
            // Step 4: Final computation
            if (constantType === 'pi') {
                const zeta2 = computeTruncatedProduct(primes, 2);
                html += `
                    <div class="step">
                        <div class="step-title"><span class="step-number">4</span>Extract π from ζ(2)</div>
                        <div class="step-content">
                            <p>Using the identity ζ(2) = π²/6, we have π = √(6·ζ(2))</p>
                            <div class="step-formula">
                                π = √(6 × ${zeta2.toFixed(12)})<br>
                                π = √${(6 * zeta2).toFixed(12)}<br>
                                π ≈ ${computedValue.toFixed(15)}
                            </div>
                            <p><strong>Exact value:</strong> π = ${exactValue.toFixed(15)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(6)}</p>
                        </div>
                    </div>
                `;
            } else {
                html += `
                    <div class="step">
                        <div class="step-title"><span class="step-number">4</span>Compare with Exact Value</div>
                        <div class="step-content">
                            <p><strong>Computed:</strong> ζ(${exponent}) ≈ ${computedValue.toFixed(15)}</p>
                            <p><strong>Exact:</strong> ζ(${exponent}) = ${exactValue.toFixed(15)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(6)}</p>
                            <p><strong>Relative error:</strong> ${(Math.abs(computedValue - exactValue) / exactValue * 100).toFixed(8)}%</p>
                        </div>
                    </div>
                `;
            }
            
            // Step 5: Error verification
            const actualError = Math.abs(computedValue - exactValue) / exactValue;
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">5</span>Verify Error Bound</div>
                    <div class="step-content">
                        <p><strong>Guaranteed bound:</strong> relative error ≤ ${(epsilon * 100).toFixed(4)}%</p>
                        <p><strong>Actual error:</strong> ${(actualError * 100).toFixed(8)}%</p>
                        <p style="color: ${actualError <= epsilon ? '#4ecdc4' : '#ff6b6b'}; font-weight: bold;">
                            ${actualError <= epsilon ? '✓ Error bound satisfied!' : '⚠ Note: Actual error slightly exceeds theoretical bound (due to finite precision)'}
                        </p>
                    </div>
                </div>
            `;
            
            document.getElementById('step-by-step').innerHTML = html;
            document.getElementById('step-by-step').style.display = 'block';
        }
        
        function showGapAnalysis(primes, constantType) {
            const gapClasses = computeGapClasses(primes);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            
            let html = '<div style="margin-bottom: 20px;">';
            html += '<button class="view-btn active" onclick="expandAllGaps()">Expand All</button>';
            html += '<button class="view-btn" onclick="collapseAllGaps()">Collapse All</button>';
            html += '</div>';
            
            const sortedGaps = Object.keys(gapClasses).map(Number).sort((a, b) => a - b);
            
            for (const gap of sortedGaps) {
                const gapPrimes = gapClasses[gap];
                const contribution = computeTruncatedProduct(gapPrimes, exponent);
                const logContrib = Math.log(contribution);
                
                // Calculate cumulative product steps
                let cumulativeSteps = [];
                let cumProduct = 1;
                for (const p of gapPrimes) {
                    const factor = 1 / (1 - Math.pow(p, -exponent));
                    cumProduct *= factor;
                    cumulativeSteps.push({
                        prime: p,
                        factor: factor,
                        cumulative: cumProduct
                    });
                }
                
                html += `
                    <div class="gap-item" onclick="toggleGap(${gap})">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div><strong>Gap ${gap}</strong></div>
                            <div class="gap-value">${gapPrimes.length} primes</div>
                        </div>
                        <div style="margin-top: 10px; font-size: 0.9em;">
                            <div>Contribution: ${contribution.toFixed(6)}</div>
                            <div>log(R_${gap}) = ${logContrib.toFixed(4)}</div>
                        </div>
                        <div style="margin-top: 8px; font-size: 0.85em; opacity: 0.8;">
                            Range: ${Math.min(...gapPrimes)} - ${Math.max(...gapPrimes)}
                        </div>
                        <div class="expand-indicator">Click to view details</div>
                        
                        <div class="gap-primes-list" id="gap-primes-${gap}">
                            <h4 style="color: #ffd700; margin-bottom: 10px;">All ${gapPrimes.length} Primes in Gap ${gap}:</h4>
                            <div class="gap-primes-container">${gapPrimes.map((p, idx) => {
                                const nextP = gapPrimes[idx + 1];
                                const prevP = idx > 0 ? gapPrimes[idx - 1] : (gap === 2 && p === 3 ? 2 : primes[primes.indexOf(p) - 1]);
                                return `p = ${p} (gap: ${p} - ${prevP} = ${gap})`;
                            }).join('<br>')}</div>
                            
                            <div class="gap-cumulative-section">
                                <h4 style="color: #4ecdc4; margin-bottom: 10px;">Cumulative Product Steps:</h4>
                                ${cumulativeSteps.map((step, idx) => `
                                    <div class="cumulative-step">
                                        <strong>Step ${idx + 1}:</strong> p = ${step.prime}<br>
                                        Factor: (1 - ${step.prime}^(-${exponent}))^(-1) = ${step.factor.toFixed(8)}<br>
                                        Cumulative: ${step.cumulative.toFixed(10)}
                                    </div>
                                `).join('')}
                                <div style="margin-top: 15px; padding: 10px; background: rgba(78, 205, 196, 0.2); border-radius: 5px;">
                                    <strong>Final Contribution for Gap ${gap}:</strong> ${contribution.toFixed(12)}
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            document.getElementById('gap-grid').innerHTML = html;
            document.getElementById('gap-analysis').style.display = 'block';
        }
        
        function toggleGap(gapId) {
            const primesList = document.getElementById(`gap-primes-${gapId}`);
            if (!primesList) return;
            
            primesList.classList.toggle('visible');
            
            const gapItem = primesList.closest('.gap-item');
            gapItem.classList.toggle('expanded');
        }
        
        function sortGapsBySize() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'size');
        }
        
        function sortGapsByCount() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'count');
        }
        
        function sortGapsByContribution() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'contribution');
        }
        
        function expandAllGaps() {
            document.querySelectorAll('.gap-primes-list').forEach(list => {
                list.classList.add('visible');
                list.closest('.gap-item').classList.add('expanded');
            });
        }
        
        function collapseAllGaps() {
            document.querySelectorAll('.gap-primes-list').forEach(list => {
                list.classList.remove('visible');
                list.closest('.gap-item').classList.remove('expanded');
            });
        }
        
        function showResidueAnalysis(primes, constantType, modulus) {
            const channels = computeResidueChannels(primes, modulus);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const smallPrimes = primes.filter(p => p < modulus);
            const smallProduct = computeTruncatedProduct(smallPrimes, exponent);
            
            channelDataGlobal = {
                channels,
                coprimeResidues,
                smallPrimes,
                smallProduct,
                exponent,
                modulus,
                allPrimes: primes
            };
            
            document.getElementById('channel-analysis').style.display = 'block';
            renderChannelView(currentChannelView);
            
            // Destroy existing chart before creating new one
            if (channelChart) {
                channelChart.destroy();
                channelChart = null;
            }
            
            // Clear canvas before creating new chart
            const canvas = document.getElementById('channelChart');
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            createChannelChart(coprimeResidues, channels, exponent, smallProduct, modulus);
        }
        
        function changeChannelView(viewType) {
            currentChannelView = viewType;
            renderChannelView(viewType);
            updateChannelViewButtons();
        }
        
        function renderChannelView(viewType) {
            if (!channelDataGlobal) return;
            
            const { channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus } = channelDataGlobal;
            
            if (viewType === 'cards') {
                renderCardView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            } else if (viewType === 'table') {
                renderTableView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            } else if (viewType === 'distribution') {
                renderDistributionView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            }
        }
        
        function renderCardView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            let html = '<div class="channel-grid">';
            
            // Small primes card
            html += `
                <div class="channel-item" onclick="toggleChannel('small-primes')">
                    <div class="channel-header">
                        <div class="channel-residue">Small Primes (< ${modulus})</div>
                        <div class="channel-count">${smallPrimes.length}</div>
                    </div>
                    <div class="channel-stats">
                        <div class="stat-item">
                            <div class="stat-label">Contribution</div>
                            <div class="stat-value">${smallProduct.toFixed(6)}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">log(Contrib)</div>
                            <div class="stat-value">${Math.log(smallProduct).toFixed(4)}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Avg Prime</div>
                            <div class="stat-value">${(smallPrimes.reduce((a,b)=>a+b,0)/smallPrimes.length).toFixed(1)}</div>
                        </div>
                    </div>
                    <div class="expand-indicator">Click to view primes</div>
                    <div class="primes-list" id="primes-small-primes">
                        <h4>All ${smallPrimes.length} Primes:</h4>
                        <div class="primes-container">${smallPrimes.join(', ')}</div>
                    </div>
                </div>
            `;
            
            // Channel cards
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const avgPrime = channelPrimes.length > 0 ? channelPrimes.reduce((sum, p) => sum + p, 0) / channelPrimes.length : 0;
                const minPrime = channelPrimes.length > 0 ? Math.min(...channelPrimes) : 0;
                const maxPrime = channelPrimes.length > 0 ? Math.max(...channelPrimes) : 0;
                
                html += `
                    <div class="channel-item" onclick="toggleChannel('${a}')">
                        <div class="channel-header">
                            <div class="channel-residue">≡ ${a} (mod ${modulus})</div>
                            <div class="channel-count">${channelPrimes.length}</div>
                        </div>
                        <div class="channel-stats">
                            <div class="stat-item">
                                <div class="stat-label">Contribution</div>
                                <div class="stat-value">${contribution.toFixed(6)}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">log(Contrib)</div>
                                <div class="stat-value">${logContrib.toFixed(4)}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Avg Prime</div>
                                <div class="stat-value">${avgPrime > 0 ? avgPrime.toFixed(1) : 'N/A'}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Range</div>
                                <div class="stat-value">${minPrime > 0 ? `${minPrime} - ${maxPrime}` : 'N/A'}</div>
                            </div>
                        </div>
                        ${channelPrimes.length > 0 ? '<div class="expand-indicator">Click to view primes</div>' : ''}
                        <div class="primes-list" id="primes-${a}">
                            <h4>All ${channelPrimes.length} Primes in Channel ${a}:</h4>
                            <div class="primes-container">${channelPrimes.join(', ')}</div>
                        </div>
                    </div>
                `;
            }
            
            html += '</div>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function renderTableView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            let html = '<table class="distribution-table">';
            html += `
                <thead>
                    <tr>
                        <th>Residue Class</th>
                        <th>Prime Count</th>
                        <th>Contribution</th>
                        <th>log(Contribution)</th>
                        <th>Avg Prime</th>
                        <th>Min Prime</th>
                        <th>Max Prime</th>
                        <th>% of Total</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
            `;
            
            const totalPrimes = smallPrimes.length + coprimeResidues.reduce((sum, a) => sum + channels[a].length, 0);
            
            // Small primes row
            html += `
                <tr>
                    <td><strong>Small (< ${modulus})</strong></td>
                    <td>${smallPrimes.length}</td>
                    <td>${smallProduct.toFixed(6)}</td>
                    <td>${Math.log(smallProduct).toFixed(4)}</td>
                    <td>${(smallPrimes.reduce((a,b)=>a+b,0)/smallPrimes.length).toFixed(1)}</td>
                    <td>${Math.min(...smallPrimes)}</td>
                    <td>${Math.max(...smallPrimes)}</td>
                    <td>${((smallPrimes.length / totalPrimes) * 100).toFixed(2)}%</td>
                    <td><button class="view-btn" style="padding: 4px 8px; font-size: 0.8em;" onclick="showPrimesModal('small-primes', ${JSON.stringify(smallPrimes).replace(/"/g, '&quot;')})">View Primes</button></td>
                </tr>
            `;
            
            // Channel rows
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const avgPrime = channelPrimes.length > 0 ? channelPrimes.reduce((sum, p) => sum + p, 0) / channelPrimes.length : 0;
                const minPrime = channelPrimes.length > 0 ? Math.min(...channelPrimes) : 0;
                const maxPrime = channelPrimes.length > 0 ? Math.max(...channelPrimes) : 0;
                const percentage = (channelPrimes.length / totalPrimes) * 100;
                
                html += `
                    <tr>
                        <td><strong>≡ ${a} (mod ${modulus})</strong></td>
                        <td>${channelPrimes.length}</td>
                        <td>${contribution.toFixed(6)}</td>
                        <td>${logContrib.toFixed(4)}</td>
                        <td>${avgPrime > 0 ? avgPrime.toFixed(1) : 'N/A'}</td>
                        <td>${minPrime > 0 ? minPrime : 'N/A'}</td>
                        <td>${maxPrime > 0 ? maxPrime : 'N/A'}</td>
                        <td>${percentage.toFixed(2)}%</td>
                        <td>${channelPrimes.length > 0 ? `<button class="view-btn" style="padding: 4px 8px; font-size: 0.8em;" onclick='showPrimesModal("${a}", ${JSON.stringify(channelPrimes)})'>View Primes</button>` : 'N/A'}</td>
                    </tr>
                `;
            }
            
            html += '</tbody></table>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function renderDistributionView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            const totalPrimes = smallPrimes.length + coprimeResidues.reduce((sum, a) => sum + channels[a].length, 0);
            
            let html = '<div style="margin-top: 20px; background: rgba(0, 0, 0, 0.6); padding: 20px; border-radius: 15px;">';
            html += '<h4 style="color: #ffd700; margin-bottom: 15px;">Prime Distribution by Residue Class</h4>';
            
            // Small primes
            const smallPercent = (smallPrimes.length / totalPrimes) * 100;
            html += `
                <div style="margin-bottom: 20px; padding: 15px; background: rgba(30, 60, 114, 0.6); border-radius: 10px;">
                    <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                        <span><strong>Small Primes (< ${modulus})</strong></span>
                        <span><strong>${smallPrimes.length} primes (${smallPercent.toFixed(2)}%)</strong></span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: ${smallPercent}%;"></div>
                    </div>
                    <div style="margin-top: 8px; font-size: 0.9em; opacity: 0.8;">
                        Contribution: ${smallProduct.toFixed(6)} | log: ${Math.log(smallProduct).toFixed(4)}
                    </div>
                </div>
            `;
            
            // Channels
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const percent = (channelPrimes.length / totalPrimes) * 100;
                
                html += `
                    <div style="margin-bottom: 20px; padding: 15px; background: rgba(30, 60, 114, 0.6); border-radius: 10px;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span><strong>≡ ${a} (mod ${modulus})</strong></span>
                            <span><strong>${channelPrimes.length} primes (${percent.toFixed(2)}%)</strong></span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${percent}%;"></div>
                        </div>
                        <div style="margin-top: 8px; font-size: 0.9em; opacity: 0.8;">
                            Contribution: ${contribution.toFixed(6)} | log: ${logContrib.toFixed(4)}
                            ${channelPrimes.length > 0 ? ` | <button class="view-btn" style="padding: 2px 8px; font-size: 0.8em;" onclick='showPrimesModal("${a}", ${JSON.stringify(channelPrimes)})'>View Primes</button>` : ''}
                        </div>
                    </div>
                `;
            }
            
            html += '</div>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function toggleChannel(id) {
            const primesList = document.getElementById(`primes-${id}`);
            if (!primesList) return;
            
            primesList.classList.toggle('visible');
            
            const channelItem = primesList.closest('.channel-item');
            channelItem.classList.toggle('expanded');
        }
        
        let channelSortOrder = 'residue';
        
        function updateChannelViewButtons() {
            document.querySelectorAll('.view-options .view-btn').forEach(btn => {
                btn.classList.remove('active');
                const text = btn.textContent.toLowerCase();
                if (currentChannelView === 'cards' && text.includes('card')) btn.classList.add('active');
                if (currentChannelView === 'table' && text.includes('table')) btn.classList.add('active');
                if (currentChannelView === 'distribution' && text.includes('distribution')) btn.classList.add('active');
            });
        }
        
        function expandAllChannels() {
            document.querySelectorAll('.primes-list').forEach(list => {
                list.classList.add('visible');
                list.closest('.channel-item').classList.add('expanded');
            });
        }
        
        function collapseAllChannels() {
            document.querySelectorAll('.primes-list').forEach(list => {
                list.classList.remove('visible');
                list.closest('.channel-item').classList.remove('expanded');
            });
        }
        
        function showPrimesModal(channelId, primes) {
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.9);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 10000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: linear-gradient(135deg, #1e3c72, #2a5298);
                padding: 40px;
                border-radius: 20px;
                max-width: 800px;
                width: 90%;
                max-height: 80vh;
                overflow-y: auto;
                box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            `;
            
            const primesArray = Array.isArray(primes) ? primes : JSON.parse(primes);
            
            content.innerHTML = `
                <h2 style="color: #ffd700; margin-bottom: 20px;">Channel ${channelId} - ${primesArray.length} Primes</h2>
                <div style="background: rgba(0, 0, 0, 0.3); padding: 20px; border-radius: 10px; font-family: 'Courier New', monospace; line-height: 1.8; margin-bottom: 20px;">
                    ${primesArray.join(', ')}
                </div>
                <div style="display: flex; gap: 10px;">
                    <button id="copyPrimes" style="flex: 1; padding: 12px; background: #4ecdc4; color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Copy to Clipboard</button>
                    <button id="closeModal" style="flex: 1; padding: 12px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Close</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('closeModal').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('copyPrimes').onclick = () => {
                navigator.clipboard.writeText(primesArray.join(', ')).then(() => {
                    const btn = document.getElementById('copyPrimes');
                    btn.textContent = 'Copied!';
                    setTimeout(() => {
                        btn.textContent = 'Copy to Clipboard';
                    }, 2000);
                });
            };
            
            modal.onclick = (e) => {
                if (e.target === modal) {
                    document.body.removeChild(modal);
                }
            };
        }
        
        function createChannelChart(coprimeResidues, channels, exponent, smallProduct, modulus) {
            const ctx = document.getElementById('channelChart').getContext('2d');
            
            if (channelChart) {
                channelChart.destroy();
            }
            
            const labels = [`Small Primes (< ${modulus})`];
            const contributions = [smallProduct];
            const primeCounts = [computationData.primes.filter(p => p < modulus).length];
            
            coprimeResidues.forEach(a => {
                labels.push(`≡ ${a} (mod ${modulus})`);
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                contributions.push(contribution);
                primeCounts.push(channelPrimes.length);
            });
            
            const colors = generateColors(labels.length);
            
            channelChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Channel Contribution',
                        data: contributions,
                        backgroundColor: colors,
                        borderColor: colors.map(c => c.replace('0.8', '1')),
                        borderWidth: 2,
                        borderRadius: 8,
                        borderSkipped: false,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            titleColor: '#fff',
                            bodyColor: '#fff',
                            borderColor: 'rgba(255, 255, 255, 0.3)',
                            borderWidth: 1,
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const contrib = contributions[idx];
                                    const logContrib = Math.log(contrib);
                                    const count = primeCounts[idx];
                                    
                                    return [
                                        `Contribution: ${contrib.toFixed(6)}`,
                                        `log(Contribution): ${logContrib.toFixed(4)}`,
                                        `Prime count: ${count}`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            ticks: {
                                color: '#fff',
                                maxRotation: 45,
                                font: {
                                    size: 10
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            }
                        },
                        y: {
                            ticks: {
                                color: '#fff',
                                callback: function(value) {
                                    return value.toFixed(3);
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            title: {
                                display: true,
                                text: `Contribution (mod ${modulus})`,
                                color: '#fff',
                                font: {
                                    size: 14,
                                    weight: 'bold'
                                }
                            }
                        }
                    },
                    animation: {
                        duration: 1500,
                        easing: 'easeOutQuart'
                    }
                }
            });
            
            document.getElementById('chart-section').style.display = 'block';
            createChartLegend(labels, colors, primeCounts);
        }
        
        function generateColors(count) {
            const baseColors = [
                'rgba(255, 215, 0, 0.8)',
                'rgba(255, 99, 132, 0.8)',
                'rgba(54, 162, 235, 0.8)', 
                'rgba(255, 205, 86, 0.8)',
                'rgba(75, 192, 192, 0.8)',
                'rgba(153, 102, 255, 0.8)',
                'rgba(255, 159, 64, 0.8)',
                'rgba(199, 199, 199, 0.8)',
                'rgba(83, 102, 255, 0.8)'
            ];
            
            const colors = [];
            for (let i = 0; i < count; i++) {
                if (i < baseColors.length) {
                    colors.push(baseColors[i]);
                } else {
                    const hue = (i * 137.5) % 360;
                    colors.push(`hsla(${hue}, 70%, 60%, 0.8)`);
                }
            }
            return colors;
        }
        
        function createChartLegend(labels, colors, primeCounts) {
            let legendHtml = '';
            
            for (let i = 0; i < labels.length; i++) {
                legendHtml += `
                    <div class="legend-item">
                        <div class="legend-color" style="background-color: ${colors[i]};"></div>
                        <span>${labels[i]} (${primeCounts[i]} primes)</span>
                    </div>
                `;
            }
            
            document.getElementById('chartLegend').innerHTML = legendHtml;
        }
        
        function changeViz(type) {
            currentViz = type;
            
            document.querySelectorAll('.viz-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            
            updateVisualization(type);
        }
        
        function updateVisualization(type) {
            if (!computationData) return;
            
            const ctx = document.getElementById('vizCanvas').getContext('2d');
            
            if (vizChart) {
                vizChart.destroy();
            }
            
            if (type === 'convergence') {
                createConvergencePlot(ctx);
            } else if (type === 'contribution') {
                createContributionPlot(ctx);
            } else if (type === 'gapDist') {
                createGapDistributionPlot(ctx);
            }
        }
        
        function createConvergencePlot(ctx) {
            const { partialProducts, exactValue, constantType } = computationData;
            
            const labels = partialProducts.map(p => p.prime);
            const values = partialProducts.map(p => {
                if (constantType === 'pi') {
                    return Math.sqrt(6 * p.value);
                }
                return p.value;
            });
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Partial Product',
                        data: values,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'Exact Value',
                        data: Array(labels.length).fill(exactValue),
                        borderColor: 'rgba(255, 215, 0, 1)',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(10)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { display: true, text: 'Prime p', color: '#fff' },
                            ticks: { color: '#fff', maxTicksLimit: 15 },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { display: true, text: 'Value', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createContributionPlot(ctx) {
            const { primes, exponent } = computationData;
            
            const contributions = primes.map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return factor - 1;
            });
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Prime Contribution',
                        data: primes.map((p, i) => ({ x: p, y: contributions[i] })),
                        backgroundColor: 'rgba(255, 99, 132, 0.6)',
                        borderColor: 'rgba(255, 99, 132, 1)',
                        pointRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `p=${context.parsed.x}: contribution = ${context.parsed.y.toFixed(8)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { display: true, text: 'Prime p (log scale)', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { display: true, text: 'Contribution (log scale)', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createGapDistributionPlot(ctx) {
            const { primes, exponent } = computationData;
            
            // Calculate gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Calculate contributions by gap
            const gapContributions = sortedGaps.map(gap => {
                const gapPrimes = [];
                for (let i = 1; i < primes.length; i++) {
                    if (primes[i] - primes[i-1] === gap) {
                        gapPrimes.push(primes[i]);
                    }
                }
                return gapPrimes.length > 0 ? computeTruncatedProduct(gapPrimes, exponent) : 1;
            });
            
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => `Gap ${g}`),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: 'rgba(78, 205, 196, 0.6)',
                        borderColor: 'rgba(78, 205, 196, 1)',
                        borderWidth: 2,
                        yAxisID: 'y',
                    }, {
                        label: 'Contribution',
                        data: gapContributions,
                        type: 'line',
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        yAxisID: 'y1',
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const gap = sortedGaps[context.dataIndex];
                                    if (context.datasetIndex === 0) {
                                        return `Frequency: ${context.parsed.y} primes`;
                                    } else {
                                        return `Contribution: ${context.parsed.y.toFixed(6)}`;
                                    }
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { display: true, text: 'Prime Gap Size', color: '#fff' },
                            ticks: { color: '#fff', maxRotation: 45 },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { display: true, text: 'Frequency', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { display: true, text: 'Contribution', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function exportChartImage() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            // Create modal for export options
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.8);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 10000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: linear-gradient(135deg, #1e3c72, #2a5298);
                padding: 40px;
                border-radius: 20px;
                max-width: 500px;
                width: 90%;
                box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            `;
            
            content.innerHTML = `
                <h2 style="color: #ffd700; margin-bottom: 25px; text-align: center;">Export Chart Options</h2>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Resolution:</label>
                    <select id="exportResolution" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="1080p">Full HD (1920 x 1080)</option>
                        <option value="1080p2x">Full HD 2x (3840 x 2160)</option>
                        <option value="4k">4K (3840 x 2160)</option>
                        <option value="8k">8K (7680 x 4320)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Background:</label>
                    <select id="exportBackground" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="black">Black</option>
                        <option value="white">White</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Chart Type:</label>
                    <select id="exportChartType" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="channel">Residue Channel Contributions</option>
                        <option value="convergence">Convergence Plot</option>
                        <option value="contribution">Prime Contributions</option>
                        <option value="gapDist">Gap Distribution Analysis</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 25px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="exportWatermark" checked style="width: auto; margin-right: 10px;">
                        <span>Include watermark by Wessen Getachew</span>
                    </label>
                </div>
                
                <div style="display: flex; gap: 10px;">
                    <button id="exportBtn" style="flex: 1; padding: 15px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Export</button>
                    <button id="cancelBtn" style="flex: 1; padding: 15px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Cancel</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('cancelBtn').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('exportBtn').onclick = () => {
                const resolution = document.getElementById('exportResolution').value;
                const background = document.getElementById('exportBackground').value;
                const chartType = document.getElementById('exportChartType').value;
                const includeWatermark = document.getElementById('exportWatermark').checked;
                
                document.body.removeChild(modal);
                
                performExport(resolution, background, chartType, includeWatermark);
            };
        }
        
        function performExport(resolution, background, chartType, includeWatermark) {
            const { epsilon, constantType, modulus, primes, computedValue, exactValue } = computationData;
            
            let width, height;
            if (resolution === '1080p') {
                width = 1920;
                height = 1080;
            } else if (resolution === '1080p2x') {
                width = 3840;
                height = 2160;
            } else if (resolution === '4k') {
                width = 3840;
                height = 2160;
            } else {
                width = 7680;
                height = 4320;
            }
            
            const exportCanvas = document.createElement('canvas');
            exportCanvas.width = width;
            exportCanvas.height = height;
            const ctx = exportCanvas.getContext('2d');
            
            // Set background
            ctx.fillStyle = background === 'white' ? '#ffffff' : '#000000';
            ctx.fillRect(0, 0, width, height);
            
            // Calculate dimensions with better proportions
            const padding = width * 0.04;
            const titleHeight = height * 0.15;
            const chartHeight = height * 0.70;
            const watermarkHeight = includeWatermark ? height * 0.05 : 0;
            
            // Text color based on background
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            const accentColor = background === 'white' ? '#1e3c72' : '#ffd700';
            
            // Draw title
            ctx.fillStyle = accentColor;
            ctx.font = `bold ${height * 0.045}px Arial`;
            ctx.textAlign = 'center';
            const title = chartType === 'channel' ? `Residue Channel Contributions (mod ${modulus})` :
                         chartType === 'convergence' ? 'Convergence to Exact Value' :
                         chartType === 'contribution' ? 'Individual Prime Contributions' :
                         'Prime Gap Distribution Analysis';
            ctx.fillText(title, width / 2, padding + height * 0.045);
            
            // Draw subtitle
            ctx.fillStyle = textColor;
            ctx.font = `${height * 0.025}px Arial`;
            const subtitle = `Computing ${constantType === 'pi' ? 'π' : 'ζ(' + computationData.exponent + ')'} using ${primes.length} primes (ε = ${epsilon})`;
            ctx.fillText(subtitle, width / 2, padding + height * 0.08);
            
            // Draw computed vs exact values - split into two columns
            ctx.font = `${height * 0.022}px Arial`;
            ctx.textAlign = 'left';
            const statsY = padding + height * 0.11;
            const leftX = padding;
            const rightX = width * 0.5 + padding;
            
            ctx.fillText(`Computed: ${computedValue.toFixed(15)}`, leftX, statsY);
            ctx.fillText(`Exact: ${exactValue.toFixed(15)}`, rightX, statsY);
            
            const relError = Math.abs(computedValue - exactValue) / exactValue;
            ctx.fillText(`Relative Error: ${(relError * 100).toFixed(8)}%`, leftX, statsY + height * 0.028);
            ctx.fillText(`Primes Used: ${primes.length}`, rightX, statsY + height * 0.028);
            
            // Create temporary canvas for chart with proper sizing
            const tempCanvas = document.createElement('canvas');
            const chartPadding = padding * 2;
            tempCanvas.width = width - chartPadding;
            tempCanvas.height = chartHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Generate chart based on type
            let chartInstance;
            
            if (chartType === 'channel') {
                chartInstance = generateChannelChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'convergence') {
                chartInstance = generateConvergenceChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'contribution') {
                chartInstance = generateContributionChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'gapDist') {
                chartInstance = generateGapDistChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            }
            
            // Wait for chart to render
            setTimeout(() => {
                // Calculate proper position to center the chart
                const chartX = chartPadding / 2;
                const chartY = titleHeight + padding;
                
                // Draw chart to main canvas without stretching
                ctx.drawImage(tempCanvas, chartX, chartY, tempCanvas.width, tempCanvas.height);
                
                // Draw watermark if enabled
                if (includeWatermark) {
                    const watermarkY = height - padding - height * 0.025;
                    ctx.fillStyle = background === 'white' ? 'rgba(0, 0, 0, 0.4)' : 'rgba(255, 255, 255, 0.4)';
                    ctx.font = `italic ${height * 0.022}px Arial`;
                    ctx.textAlign = 'center';
                    ctx.fillText('Generated by Wessen Getachew - Modular Sieve Calculator', width / 2, watermarkY);
                    
                    ctx.font = `${height * 0.018}px Arial`;
                    ctx.fillText(new Date().toISOString().split('T')[0], width / 2, watermarkY + height * 0.025);
                }
                
                // Convert to JPEG and download
                exportCanvas.toBlob((blob) => {
                    const url = URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.href = url;
                    a.download = `zeta_chart_${chartType}_${resolution}_${Date.now()}.jpg`;
                    a.click();
                    URL.revokeObjectURL(url);
                    
                    chartInstance.destroy();
                }, 'image/jpeg', 0.95);
            }, 500);
        }
        
        function generateChannelChartForExport(ctx, width, height, background) {
            const { primes, exponent, modulus } = computationData;
            const channels = computeResidueChannels(primes, modulus);
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const smallPrimes = primes.filter(p => p < modulus);
            const smallProduct = computeTruncatedProduct(smallPrimes, exponent);
            
            const labels = [`Small Primes`, ...coprimeResidues.map(a => `≡ ${a} (mod ${modulus})`)];
            const contributions = [smallProduct, ...coprimeResidues.map(a => {
                const channelPrimes = channels[a];
                return channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
            })];
            
            const colors = generateColors(labels.length);
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Contribution',
                        data: contributions,
                        backgroundColor: colors,
                        borderColor: colors.map(c => c.replace('0.8', '1')),
                        borderWidth: 3
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: { display: false },
                        title: { display: false }
                    },
                    scales: {
                        x: {
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' },
                            title: {
                                display: true,
                                text: 'Contribution',
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    }
                }
            });
        }
        
        function generateConvergenceChartForExport(ctx, width, height, background) {
            const { partialProducts, exactValue, constantType } = computationData;
            
            const labels = partialProducts.map(p => p.prime);
            const values = partialProducts.map(p => {
                if (constantType === 'pi') {
                    return Math.sqrt(6 * p.value);
                }
                return p.value;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Partial Product',
                        data: values,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'Exact Value',
                        data: Array(labels.length).fill(exactValue),
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        borderWidth: 3,
                        borderDash: [10, 10],
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Prime p', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                maxTicksLimit: 20
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Value', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateContributionChartForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            
            const contributions = primes.map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return factor - 1;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Prime Contribution',
                        data: primes.map((p, i) => ({ x: p, y: contributions[i] })),
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.6)' : 'rgba(255, 99, 132, 0.6)',
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(255, 99, 132, 1)',
                        pointRadius: 5
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p (log scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Contribution (log scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateComparisonChartForExport(ctx, width, height, background) {
            const { primes, exponent, modulus } = computationData;
            const channels = computeResidueChannels(primes, modulus);
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const colors = generateColors(coprimeResidues.length);
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            const datasets = coprimeResidues.map((a, idx) => {
                const channelPrimes = channels[a];
                const contributions = channelPrimes.map(p => {
                    const factor = 1 / (1 - Math.pow(p, -exponent));
                    return factor - 1;
                });
                
                return {
                    label: `≡ ${a} (mod ${modulus})`,
                    data: channelPrimes.map((p, i) => ({ x: p, y: contributions[i] })),
                    backgroundColor: colors[idx],
                    borderColor: colors[idx].replace('0.8', '1'),
                    pointRadius: 4
                };
            });
            
            return new Chart(ctx, {
                type: 'scatter',
                data: { datasets },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor, 
                                font: { size: Math.floor(height * 0.02) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Contribution', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateGapDistChartForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            
            // Calculate gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Calculate contributions by gap
            const gapContributions = sortedGaps.map(gap => {
                const gapPrimes = [];
                for (let i = 1; i < primes.length; i++) {
                    if (primes[i] - primes[i-1] === gap) {
                        gapPrimes.push(primes[i]);
                    }
                }
                return gapPrimes.length > 0 ? computeTruncatedProduct(gapPrimes, exponent) : 1;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => `Gap ${g}`),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.6)' : 'rgba(78, 205, 196, 0.6)',
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        borderWidth: 3,
                        yAxisID: 'y',
                    }, {
                        label: 'Contribution',
                        data: gapContributions,
                        type: 'line',
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        yAxisID: 'y1',
                        tension: 0.4,
                        pointRadius: 6
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Prime Gap Size', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.022) },
                                maxRotation: 45
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { 
                                display: true, 
                                text: 'Contribution', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function exportResults() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const exportData = {
                timestamp: new Date().toISOString(),
                parameters: {
                    epsilon: computationData.epsilon,
                    constantType: computationData.constantType,
                    method: computationData.method,
                    cutoff: computationData.Y
                },
                results: {
                    computedValue: computationData.computedValue,
                    exactValue: computationData.exactValue,
                    absoluteError: Math.abs(computationData.computedValue - computationData.exactValue),
                    relativeError: Math.abs(computationData.computedValue - computationData.exactValue) / computationData.exactValue,
                    primesUsed: computationData.primes.length,
                    primes: computationData.primes
                }
            };
            
            const blob = new Blob([JSON.stringify(exportData, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `zeta_calculation_${computationData.constantType}_${Date.now()}.json`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        function exportStepsText() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const { epsilon, constantType, Y, primes, exponent, computedValue, exactValue } = computationData;
            
            let text = `MODULAR SIEVE CALCULATION\n`;
            text += `${'='.repeat(80)}\n\n`;
            text += `Timestamp: ${new Date().toISOString()}\n`;
            text += `Constant: ${constantType === 'pi' ? 'π' : 'ζ(' + exponent + ')'}\n`;
            text += `Target Error: ${epsilon}\n\n`;
            
            text += `STEP 1: DETERMINE CUTOFF\n`;
            text += `${'-'.repeat(80)}\n`;
            if (constantType === 'pi') {
                text += `For π: Y = ⌈1 + 1/log(1+ε)⌉\n`;
                text += `Y = ⌈1 + ${(1/Math.log(1+epsilon)).toFixed(4)}⌉ = ${Y}\n`;
            } else {
                text += `For ζ(${exponent}): Y = ⌈(2/((2n-1)·log(1+ε)))^(1/(2n-1))⌉\n`;
                text += `Y = ${Y}\n`;
            }
            text += `\nNeed all primes ≤ ${Y-1}\n\n`;
            
            text += `STEP 2: GENERATE PRIMES\n`;
            text += `${'-'.repeat(80)}\n`;
            text += `Found ${primes.length} primes using Sieve of Eratosthenes:\n`;
            text += `{${primes.slice(0, 50).join(', ')}${primes.length > 50 ? ', ...' : ''}}\n\n`;
            
            text += `STEP 3: COMPUTE EULER PRODUCT\n`;
            text += `${'-'.repeat(80)}\n`;
            const product = computeTruncatedProduct(primes, exponent);
            text += `${constantType === 'pi' ? 'ζ(2)' : 'ζ(' + exponent + ')'} = ∏(1-p^(-${exponent}))^(-1) = ${product.toFixed(15)}\n\n`;
            
            if (constantType === 'pi') {
                text += `STEP 4: EXTRACT π\n`;
                text += `${'-'.repeat(80)}\n`;
                text += `π = √(6·ζ(2)) = √(6 × ${product.toFixed(12)})\n`;
                text += `π ≈ ${computedValue.toFixed(15)}\n\n`;
            }
            
            text += `RESULTS\n`;
            text += `${'-'.repeat(80)}\n`;
            text += `Computed: ${computedValue.toFixed(15)}\n`;
            text += `Exact:    ${exactValue.toFixed(15)}\n`;
            text += `Abs Err:  ${Math.abs(computedValue - exactValue).toExponential(10)}\n`;
            text += `Rel Err:  ${(Math.abs(computedValue - exactValue) / exactValue * 100).toFixed(10)}%\n`;
            
            const blob = new Blob([text], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `zeta_steps_${constantType}_${Date.now()}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        window.onload = () => {
            compute();
        };
    </script>
</body>
</html>
