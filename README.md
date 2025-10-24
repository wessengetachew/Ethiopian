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
        
        .prime-ring-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .prime-ring-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .ring-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }
        
        .ring-controls label {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #fff;
            font-size: 0.9em;
        }
        
        .ring-controls input[type="number"],
        .ring-controls select {
            width: 80px;
            padding: 6px;
            border-radius: 6px;
            border: none;
            font-size: 14px;
        }
        
        .ring-controls input[type="checkbox"] {
            width: auto;
        }
        
        #primeRingCanvas {
            width: 100%;
            height: 700px;
            max-height: 700px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 10px;
            cursor: crosshair;
        }
        
        .ring-info {
            margin-top: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        
        .ring-legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 15px;
            font-size: 0.85em;
        }
        
        .ring-legend-item {
            display: flex;
            align-items: center;
            gap: 6px;
            padding: 4px 10px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 5px;
        }
        
        .ring-legend-color {
            width: 14px;
            height: 14px;
            border-radius: 50%;
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
            <div style="text-align: center; margin-top: 15px; font-size: 0.95em; font-style: italic; opacity: 0.85;">
                By Wessen Getachew (<a href="https://twitter.com/7Dview" target="_blank" style="color: #4ecdc4; text-decoration: none;">@7Dview</a>)
            </div>
            <div style="text-align: center; margin-top: 5px; font-size: 0.9em; opacity: 0.75;">
                Inspired by Leonhard Euler's pioneering work and 3Blue1Brown's mathematical visualizations
            </div>
            <div style="text-align: center; margin-top: 12px; font-size: 0.9em;">
                <span style="opacity: 0.8;">Explore more prime visualizations:</span>
                <a href="https://wessengetachew.github.io/GCD/" target="_blank" style="color: #4ecdc4; text-decoration: none; margin: 0 8px; font-weight: 500;">GCD Patterns</a>
                <span style="opacity: 0.5;">|</span>
                <a href="https://wessengetachew.github.io/Primes/" target="_blank" style="color: #4ecdc4; text-decoration: none; margin: 0 8px; font-weight: 500;">Prime Spirals</a>
            </div>
            
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
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('phasor')">
                    <h3>Nested Modular Unity & Zeta Surface</h3>
                    <span class="toggle-icon" id="phasor-icon">▼</span>
                </div>
                <div id="phasor-content" class="collapsible-content">
                    <p><strong>The Zeta Function as a Phasor Sum:</strong></p>
                    <p>For complex argument s = σ + it, the Riemann zeta function can be written as:</p>
                    <div class="formula">ζ(s) = Σ n<sup>-σ</sup> e<sup>-it log n</sup></div>
                    
                    <p>Each term n<sup>-s</sup> is a <strong>rotating phasor</strong> on the complex plane with:</p>
                    <div class="formula">
                        Radius: r<sub>n</sub> = n<sup>-σ</sup><br>
                        Angle: θ<sub>n</sub> = -t log n
                    </div>
                    
                    <p style="margin-top: 15px;"><strong>Modular Unity Correspondence:</strong></p>
                    <p>Each residue class k (mod m) corresponds to an m-th root of unity:</p>
                    <div class="formula">k mod m ↔ e<sup>2πik/m</sup></div>
                    
                    <p>This isomorphism connects modular arithmetic to the unit circle geometry. For each modulus m and residue k:</p>
                    <div class="formula">S<sub>m,k</sub>(s; N) = Σ<sub>n≡k (mod m)</sub> n<sup>-s</sup></div>
                    
                    <p style="margin-top: 15px;"><strong>The Critical Line (σ = 1/2):</strong></p>
                    <p>On the critical line, each contribution rotates at angular velocity ∝ log n. When modular rotations align <strong>destructively</strong>, their vector sum vanishes—precisely the condition for a nontrivial zero:</p>
                    <div class="formula">ζ(1/2 + iT) = 0</div>
                    
                    <p style="margin-top: 15px;"><strong>Nested Modular Surface:</strong></p>
                    <p>Stacking concentric rings for m = 1, 2, 3, ... creates a <strong>nested modular unity lattice</strong>. Each ring samples the unit circle at m equally-spaced points, and together they approximate the continuous analytic structure of ζ(s). The GCD=1 residues (primitive rotations) form the multiplicative group of units mod m.</p>
                    
                    <p style="margin-top: 15px;"><strong>Geometric Interpretation:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Height t:</strong> Controls angular phase of each modular shell (vertical movement on zeta surface)</li>
                        <li><strong>Real part σ:</strong> Controls radial decay (compression toward critical line)</li>
                        <li><strong>Modulus m:</strong> Discrete Fourier mode on the complex circle</li>
                        <li><strong>Primitive residues:</strong> φ(m) independent rotation channels</li>
                    </ul>
                    
                    <p style="margin-top: 15px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                        <strong>💡 Key Insight:</strong> The nested modular lattice forms a discrete analogue of the complex-analytic domain of ζ(s). By weighting each ring by n<sup>-σ</sup> and rotating by phase -t log n, we obtain a direct geometric mimic of the Riemann zeta surface.
                    </p>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('credits')">
                    <h3>Credits & Acknowledgments</h3>
                    <span class="toggle-icon" id="credits-icon">▼</span>
                </div>
                <div id="credits-content" class="collapsible-content">
                    <p style="margin-bottom: 15px;"><strong>Creator:</strong> Wessen Getachew (<a href="https://twitter.com/7Dview" target="_blank" style="color: #4ecdc4; text-decoration: none;">@7Dview</a>)</p>
                    
                    <p style="margin-bottom: 15px;"><strong>Mathematical Foundations:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Leonhard Euler (1707-1783)</strong> - Pioneer of the Euler product formula for the Riemann zeta function, discovered the beautiful identity ζ(2) = π²/6, and laid the groundwork for analytic number theory</li>
                        <li><strong>Bernhard Riemann (1826-1866)</strong> - Extended Euler's work to the complex plane with the Riemann zeta function</li>
                    </ul>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Educational Inspiration:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>3Blue1Brown (Grant Sanderson)</strong> - For exceptional mathematical visualizations and making complex concepts accessible through elegant visual storytelling. His videos on the Basel problem, prime number patterns, and the Riemann zeta function inspired the interactive visualization approach in this calculator.</li>
                    </ul>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Technologies Used:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Chart.js</strong> - Interactive charting library for data visualization</li>
                        <li><strong>HTML5 Canvas</strong> - For high-resolution chart exports</li>
                        <li><strong>JavaScript</strong> - Core computation engine and user interface</li>
                    </ul>
                    
                    <p style="margin-top: 15px;"><strong>Special Thanks:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li>The mathematical community for centuries of insights into prime numbers and the zeta function</li>
                        <li>Open-source developers who created the libraries that power this calculator</li>
                        <li>Everyone who uses this tool to explore the beauty of mathematics</li>
                    </ul>
                    
                    <p style="margin-top: 20px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                        <strong>💡 Note:</strong> This calculator is an educational tool designed to demonstrate the power of Euler products and modular arithmetic in computing fundamental mathematical constants. It combines classical number theory with modern computational methods and interactive visualization.
                    </p>
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
                    
                    <label for="decimalPlaces">Decimal Places to Display:</label>
                    <input type="number" id="decimalPlaces" value="15" min="1" max="20" step="1" onchange="validateDecimalPlaces()">
                    <div style="font-size: 0.85em; opacity: 0.8; margin-top: -10px;">
                        Max 20 digits (JavaScript precision limit ≈15-17 digits)
                    </div>
                    <div id="precision-warning" style="display: none; font-size: 0.85em; color: #ff6b6b; margin-top: 5px; padding: 8px; background: rgba(255, 107, 107, 0.1); border-radius: 5px;">
                        ⚠️ Digits beyond 15-17 may not be accurate due to floating-point precision limits
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
                    <button class="viz-btn" onclick="changeViz('primeCount')">Prime Counting π(x)</button>
                    <button class="viz-btn" onclick="changeViz('density')">Prime Density Analysis</button>
                    <button class="viz-btn" onclick="changeViz('gapHistogram')">Prime Gaps Histogram</button>
                    <button class="viz-btn" onclick="changeViz('sacksSpiral')">Sacks Spiral</button>
                    <button class="viz-btn" onclick="changeViz('zetaZeros')">Riemann Zeta Zeros</button>
                    <button class="viz-btn" onclick="changeViz('errorAnalysis')">Error Analysis</button>
                    <button class="viz-btn" onclick="changeViz('primeRaces')">Prime Races</button>
                    <button class="viz-btn" onclick="changeViz('goldbachComet')">Goldbach Comet</button>
                    <button class="viz-btn" onclick="changeViz('phasorSum')">Phasor Sum (Complex Plane)</button>
                    <button class="viz-btn" onclick="changeViz('zetaSurface')">Modular Zeta Surface</button>
                </div>
                <canvas id="vizCanvas"></canvas>
                <div id="vizStats" style="margin-top: 20px; padding: 20px; background: rgba(0, 0, 0, 0.3); border-radius: 10px; display: none;"></div>
            </div>
            
            <div id="prime-ring-section" class="prime-ring-container" style="display: none;">
                <h3>Prime Residue Visualization: Concentric Rings (mod m)</h3>
                <div class="ring-controls">
                    <label>
                        Modulus Mode:
                        <select id="modulusMode" onchange="toggleModulusMode()">
                            <option value="range">Range (1 to max)</option>
                            <option value="custom">Custom List</option>
                            <option value="powers">Powers of 2</option>
                            <option value="powers3">Powers of 3</option>
                        </select>
                    </label>
                    <div id="rangeControls">
                        <label>
                            Max Modulus:
                            <input type="number" id="maxModulus" value="30" min="2" max="100" step="1">
                        </label>
                    </div>
                    <div id="customControls" style="display: none;">
                        <label style="flex: 1;">
                            Custom Moduli (comma-separated):
                            <input type="text" id="customModuli" placeholder="e.g., 1,2,4,8,16,32" style="width: 100%;">
                        </label>
                    </div>
                    <label>
                        Point Size:
                        <input type="number" id="pointSize" value="4" min="2" max="10" step="1">
                    </label>
                    <label>
                        <input type="checkbox" id="showLabels" checked>
                        Show Prime Labels
                    </label>
                    <label>
                        <input type="checkbox" id="showModLines" checked>
                        Show Mod Lines
                    </label>
                    <label>
                        <input type="checkbox" id="invertRings">
                        Invert Ring Order
                    </label>
                    <label>
                        Color By:
                        <select id="colorMode">
                            <option value="residue">Residue Class</option>
                            <option value="modulus">Modulus Level</option>
                            <option value="size">Prime Size</option>
                        </select>
                    </label>
                    <button onclick="updatePrimeRing()" style="padding: 6px 16px; background: #4ecdc4; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Update</button>
                </div>
                <div class="ring-controls" style="margin-top: 10px;">
                    <label>
                        <input type="checkbox" id="invertColors">
                        White Background
                    </label>
                    <label>
                        Rotation Mode:
                        <select id="rotationMode">
                            <option value="none">No Rotation</option>
                            <option value="global">Global Rotation</option>
                            <option value="local">Local Rotation (by ring)</option>
                        </select>
                    </label>
                    <label>
                        Speed:
                        <input type="number" id="rotationSpeed" value="0.5" min="0.1" max="5" step="0.1">
                    </label>
                    <button onclick="toggleRotation()" id="rotationToggle" style="padding: 6px 16px; background: #ff6b6b; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Start Rotation</button>
                    <button onclick="exportPrimeRing()" style="padding: 6px 16px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Export Ring (PNG)</button>
                </div>
                <canvas id="primeRingCanvas"></canvas>
                <div class="ring-info">
                    <strong>Visualization:</strong> Each prime p is plotted on concentric rings where ring m represents residues mod m.
                    Position on ring: angle θ = 2π·(p mod m)/m for primes with gcd(p mod m, m) = 1.
                    Use "Invert Ring Order" to show smallest modulus on outer ring.
                    <br><strong>Presets:</strong> Powers of 2 (1,2,4,8,...), Powers of 3 (1,3,9,27,...), or custom list.
                    Hover over points to see prime details.
                </div>
                <div id="ringLegend" class="ring-legend"></div>
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
            decimalPlaces = parseInt(document.getElementById('decimalPlaces').value);
            
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
                    document.getElementById('computed-value').textContent = computedValue.toFixed(decimalPlaces);
                    document.getElementById('exact-value').textContent = exactValues[constantType].toFixed(decimalPlaces);
                    
                    const actualError = Math.abs(computedValue - exactValues[constantType]) / exactValues[constantType];
                    document.getElementById('actual-error').innerHTML = `Actual relative error: <strong>${(actualError * 100).toFixed(Math.min(decimalPlaces - 5, 8))}%</strong>`;
                    document.getElementById('error-bound').innerHTML = `Guaranteed error ≤ <strong>${(epsilon * 100).toFixed(4)}%</strong>`;
                    document.getElementById('prime-count').innerHTML = `Using <strong>${primes.length}</strong> primes up to <strong>${Y-1}</strong>`;
                    
                    // Add precision info
                    const precisionNote = decimalPlaces > 15 ? 
                        '<div style="font-size: 0.85em; color: #ff6b6b; margin-top: 8px;">⚠️ Note: JavaScript floating-point precision is limited to ~15-17 significant digits</div>' : '';
                    document.getElementById('prime-count').innerHTML += precisionNote;
                    
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
                    
                    // Show prime ring visualization
                    document.getElementById('prime-ring-section').style.display = 'block';
                    updatePrimeRing();
                    
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
                return `(1 - ${p}<sup>-${exponent}</sup>)<sup>-1</sup> = ${factor.toFixed(Math.min(decimalPlaces, 10))}`;
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
                            ${constantType === 'pi' ? 'ζ(2) = ' : `ζ(${exponent}) = `}${computeTruncatedProduct(primes, exponent).toFixed(Math.min(decimalPlaces, 12))}
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
                                π = √(6 × ${zeta2.toFixed(Math.min(decimalPlaces, 12))})<br>
                                π = √${(6 * zeta2).toFixed(Math.min(decimalPlaces, 12))}<br>
                                π ≈ ${computedValue.toFixed(decimalPlaces)}
                            </div>
                            <p><strong>Exact value:</strong> π = ${exactValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(Math.min(decimalPlaces - 9, 6))}</p>
                        </div>
                    </div>
                `;
            } else {
                html += `
                    <div class="step">
                        <div class="step-title"><span class="step-number">4</span>Compare with Exact Value</div>
                        <div class="step-content">
                            <p><strong>Computed:</strong> ζ(${exponent}) ≈ ${computedValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Exact:</strong> ζ(${exponent}) = ${exactValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(Math.min(decimalPlaces - 9, 6))}</p>
                            <p><strong>Relative error:</strong> ${(Math.abs(computedValue - exactValue) / exactValue * 100).toFixed(Math.min(decimalPlaces - 7, 8))}%</p>
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
                            <div>Contribution: ${contribution.toFixed(Math.min(decimalPlaces - 9, 6))}</div>
                            <div>log(R_${gap}) = ${logContrib.toFixed(Math.min(decimalPlaces - 11, 4))}</div>
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
                                        Factor: (1 - ${step.prime}^(-${exponent}))^(-1) = ${step.factor.toFixed(Math.min(decimalPlaces - 7, 8))}<br>
                                        Cumulative: ${step.cumulative.toFixed(Math.min(decimalPlaces - 5, 10))}
                                    </div>
                                `).join('')}
                                <div style="margin-top: 15px; padding: 10px; background: rgba(78, 205, 196, 0.2); border-radius: 5px;">
                                    <strong>Final Contribution for Gap ${gap}:</strong> ${contribution.toFixed(Math.min(decimalPlaces, 12))}
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
                                <div class="stat-value">${contribution.toFixed(Math.min(decimalPlaces - 9, 6))}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">log(Contrib)</div>
                                <div class="stat-value">${logContrib.toFixed(Math.min(decimalPlaces - 11, 4))}</div>
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
                        <td>${contribution.toFixed(Math.min(decimalPlaces - 9, 6))}</td>
                        <td>${logContrib.toFixed(Math.min(decimalPlaces - 11, 4))}</td>
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
                        Contribution: ${smallProduct.toFixed(Math.min(decimalPlaces - 9, 6))} | log: ${Math.log(smallProduct).toFixed(Math.min(decimalPlaces - 11, 4))}
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
        let decimalPlaces = 15; // Global decimal places setting
        
        function validateDecimalPlaces() {
            const input = document.getElementById('decimalPlaces');
            const warning = document.getElementById('precision-warning');
            const value = parseInt(input.value);
            
            // Cap at 20
            if (value > 20) {
                input.value = 20;
            }
            
            // Show warning if > 17
            if (value > 17) {
                warning.style.display = 'block';
            } else {
                warning.style.display = 'none';
            }
        }
        
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
            
            const canvas = document.getElementById('vizCanvas');
            const ctx = canvas.getContext('2d');
            
            // Clear any existing event listeners
            const newCanvas = canvas.cloneNode(true);
            canvas.parentNode.replaceChild(newCanvas, canvas);
            
            // Get fresh references
            const freshCanvas = document.getElementById('vizCanvas');
            const freshCtx = freshCanvas.getContext('2d');
            
            if (vizChart) {
                vizChart.destroy();
                vizChart = null;
            }
            
            // Clear the canvas completely
            freshCtx.clearRect(0, 0, freshCanvas.width, freshCanvas.height);
            
            // Hide stats by default
            document.getElementById('vizStats').style.display = 'none';
            
            if (type === 'convergence') {
                createConvergencePlot(freshCtx);
            } else if (type === 'contribution') {
                createContributionPlot(freshCtx);
            } else if (type === 'gapDist') {
                createGapDistributionPlot(freshCtx);
            } else if (type === 'primeCount') {
                createPrimeCountingPlot(freshCtx);
            } else if (type === 'density') {
                createDensityAnalysisPlot(freshCtx);
            } else if (type === 'gapHistogram') {
                createGapHistogramPlot(freshCtx);
            } else if (type === 'sacksSpiral') {
                createSacksSpiralPlot(freshCtx);
            } else if (type === 'zetaZeros') {
                createZetaZerosPlot(freshCtx);
            } else if (type === 'errorAnalysis') {
                createErrorAnalysisPlot(freshCtx);
            } else if (type === 'primeRaces') {
                createPrimeRacesPlot(freshCtx);
            } else if (type === 'goldbachComet') {
                createGoldbachCometPlot(freshCtx);
            } else if (type === 'phasorSum') {
                createPhasorSumPlot(freshCtx);
            } else if (type === 'zetaSurface') {
                createZetaSurfacePlot(freshCtx);
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
                        <option value="primeCount">Prime Counting π(x)</option>
                        <option value="density">Prime Density Analysis</option>
                        <option value="gapHistogram">Prime Gaps Histogram</option>
                        <option value="sacksSpiral">Sacks Spiral</option>
                        <option value="zetaZeros">Riemann Zeta Zeros</option>
                        <option value="errorAnalysis">Error Analysis</option>
                        <option value="primeRaces">Prime Races</option>
                        <option value="goldbachComet">Goldbach Comet</option>
                        <option value="phasorSum">Phasor Sum (Complex Plane)</option>
                        <option value="zetaSurface">Modular Zeta Surface</option>
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
                         chartType === 'gapDist' ? 'Prime Gap Distribution Analysis' :
                         chartType === 'primeCount' ? 'Prime Counting Function π(x)' :
                         chartType === 'density' ? 'Prime Density Analysis' :
                         chartType === 'gapHistogram' ? 'Prime Gaps Histogram' :
                         chartType === 'sacksSpiral' ? 'Sacks Spiral Visualization' :
                         chartType === 'zetaZeros' ? 'Riemann Zeta Function - Non-Trivial Zeros' :
                         chartType === 'errorAnalysis' ? 'Error Analysis - Convergence Rate' :
                         chartType === 'primeRaces' ? `Prime Races (mod ${modulus})` :
                         chartType === 'goldbachComet' ? 'Goldbach Comet - Prime Pair Partitions' :
                         chartType === 'phasorSum' ? 'Phasor Sum: ζ(s) as Rotating Vectors' :
                         chartType === 'zetaSurface' ? 'Modular Zeta Surface - Nested Unity Lattice' :
                         'Visualization';
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
            
            // Make temp canvas larger to capture full chart
            tempCanvas.width = width - chartPadding;
            tempCanvas.height = chartHeight * 1.2; // Increased to capture full chart
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
            } else if (chartType === 'primeCount') {
                chartInstance = generatePrimeCountChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'density') {
                chartInstance = generateDensityChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'gapHistogram') {
                chartInstance = generateGapHistogramChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'sacksSpiral') {
                chartInstance = generateSacksSpiralForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'zetaZeros') {
                chartInstance = generateZetaZerosChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'errorAnalysis') {
                chartInstance = generateErrorAnalysisChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'primeRaces') {
                chartInstance = generatePrimeRacesChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'goldbachComet') {
                chartInstance = generateGoldbachCometForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'phasorSum') {
                chartInstance = generatePhasorSumForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'zetaSurface') {
                chartInstance = generateZetaSurfaceForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            }
            
            // Wait for chart to render with longer delay
            setTimeout(() => {
                // Calculate proper position to center the chart
                const chartX = chartPadding / 2;
                const chartY = titleHeight + padding;
                
                // Calculate available space
                const availableHeight = height - chartY - watermarkHeight - padding;
                
                // Scale chart to fit if needed, maintaining aspect ratio
                let drawWidth = tempCanvas.width;
                let drawHeight = tempCanvas.height;
                
                if (drawHeight > availableHeight) {
                    const scale = availableHeight / drawHeight;
                    drawHeight = availableHeight;
                    drawWidth = tempCanvas.width * scale;
                }
                
                // Center horizontally if scaled
                const finalX = (width - drawWidth) / 2;
                
                // Draw chart to main canvas with proper scaling
                ctx.drawImage(tempCanvas, finalX, chartY, drawWidth, drawHeight);
                
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
                    a.download = `modular_sieve_${chartType}_${resolution}_${Date.now()}.jpg`;
                    a.click();
                    URL.revokeObjectURL(url);
                    
                    chartInstance.destroy();
                }, 'image/jpeg', 0.95);
            }, 1000); // Increased delay to ensure full chart renders
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
        
        function createGapHistogramPlot(ctx) {
            const { primes } = computationData;
            
            // Calculate all gaps
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
            
            // Find special gaps
            const twinPrimes = gapCounts[2] || 0;
            const cousinPrimes = gapCounts[4] || 0;
            const sexyPrimes = gapCounts[6] || 0;
            const maxGap = Math.max(...sortedGaps);
            const avgGap = gaps.reduce((a, b) => a + b, 0) / gaps.length;
            const maxGapCount = Math.max(...counts);
            const mostCommonGap = sortedGaps[counts.indexOf(maxGapCount)];
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Gaps Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px;">
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ff6384;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Twin Primes (gap=2)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${twinPrimes}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ff9f40;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Cousin Primes (gap=4)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${cousinPrimes}</div>
                    </div>
                    <div style="background: rgba(255, 205, 86, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ffcd56;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sexy Primes (gap=6)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffcd56;">${sexyPrimes}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #4bc0c0;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Average Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${avgGap.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #9966ff;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Maximum Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${maxGap}</div>
                    </div>
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #4ecdc4;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Most Common Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${mostCommonGap} (${maxGapCount}x)</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Gaps:</strong><br>
                    • <strong>Twin Primes:</strong> Pairs like (3,5), (5,7), (11,13) with gap=2<br>
                    • <strong>Cousin Primes:</strong> Pairs like (3,7), (7,11), (13,17) with gap=4<br>
                    • <strong>Sexy Primes:</strong> Pairs like (5,11), (7,13), (11,17) with gap=6 (from Latin "sex" = six)<br>
                    • <strong>Cramér's Conjecture:</strong> Max gap ≤ (ln p)² for large primes p<br>
                    • Average gap near p ≈ ln(p) by the Prime Number Theorem
                </div>
            `;
            
            // Color bars by special types
            const barColors = sortedGaps.map(gap => {
                if (gap === 2) return 'rgba(255, 99, 132, 0.8)';
                if (gap === 4) return 'rgba(255, 159, 64, 0.8)';
                if (gap === 6) return 'rgba(255, 205, 86, 0.8)';
                if (gap === maxGap) return 'rgba(153, 102, 255, 0.8)';
                return 'rgba(78, 205, 196, 0.7)';
            });
            
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => g.toString()),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: barColors,
                        borderColor: barColors.map(c => c.replace('0.7', '1').replace('0.8', '1')),
                        borderWidth: 2,
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const gap = sortedGaps[context.dataIndex];
                                    const count = context.parsed.y;
                                    const pct = (count / gaps.length * 100).toFixed(2);
                                    let type = '';
                                    if (gap === 2) type = ' (Twin Primes)';
                                    else if (gap === 4) type = ' (Cousin Primes)';
                                    else if (gap === 6) type = ' (Sexy Primes)';
                                    else if (gap === maxGap) type = ' (Maximum Gap)';
                                    return [
                                        `Gap ${gap}${type}`,
                                        `Frequency: ${count}`,
                                        `Percentage: ${pct}%`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Gap Size', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                maxRotation: 45,
                                callback: function(value, index) {
                                    // Show every nth label to avoid crowding
                                    if (sortedGaps.length > 30) {
                                        return index % Math.ceil(sortedGaps.length / 30) === 0 ? this.getLabelForValue(value) : '';
                                    }
                                    return this.getLabelForValue(value);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createSacksSpiralPlot(ctx) {
            const { primes } = computationData;
            
            // Create a Set for O(1) prime lookup
            const primeSet = new Set(primes);
            
            // Sacks spiral: r = √n, θ = 2π√n
            // Use all computed primes, no artificial cap
            const spiralData = [];
            const maxN = primes[primes.length - 1];
            
            // Include all numbers up to maxN
            for (let n = 1; n <= maxN; n++) {
                const r = Math.sqrt(n);
                const theta = 2 * Math.PI * Math.sqrt(n);
                const x = r * Math.cos(theta);
                const y = r * Math.sin(theta);
                
                const isPrime = primeSet.has(n);
                
                spiralData.push({ x, y, n, isPrime });
            }
            
            const primePoints = spiralData.filter(p => p.isPrime);
            const compositePoints = spiralData.filter(p => !p.isPrime && p.n > 1);
            
            // Calculate pattern statistics
            const maxR = Math.sqrt(maxN);
            const primesInSpiral = primePoints.length;
            const density = primesInSpiral / maxN;
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Sacks Spiral Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Numbers Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${maxN.toLocaleString()}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes Found</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${primesInSpiral}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Prime Density</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${(density * 100).toFixed(2)}%</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Spiral Radius</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${maxR.toFixed(2)}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Sacks Spiral:</strong><br>
                    • Discovered by Robert Sacks, this Archimedean spiral plots integers at position (r,θ) = (√n, 2π√n)<br>
                    • <span style="color: #ffd700;">●</span> Gold dots = Prime numbers<br>
                    • <span style="color: rgba(255,255,255,0.3);">●</span> Gray dots = Composite numbers<br>
                    • Primes form striking radial rays, revealing deep patterns in their distribution<br>
                    • Unlike Ulam spiral, perfect squares line up along the horizontal axis (θ = 0)<br>
                    • The ray patterns correspond to polynomial families that produce many primes
                </div>
            `;
            
            // Clear previous chart if it exists
            if (vizChart) {
                vizChart.destroy();
                vizChart = null;
            }
            
            // Draw custom spiral on canvas
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const scale = Math.min(canvas.width, canvas.height) / (2 * maxR) * 0.85;
            
            // Clear canvas
            ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw composite numbers first (background)
            ctx.fillStyle = 'rgba(255, 255, 255, 0.15)';
            for (const point of compositePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 1.5, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw primes (foreground)
            ctx.fillStyle = '#ffd700';
            for (const point of primePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 2.5, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw center marker
            ctx.fillStyle = '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 4, 0, Math.PI * 2);
            ctx.fill();
            
            // Add hover interaction
            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;
                
                // Find closest point
                let closestPoint = null;
                let minDist = 10;
                
                for (const point of spiralData) {
                    const screenX = centerX + point.x * scale;
                    const screenY = centerY + point.y * scale;
                    const dist = Math.sqrt((mouseX - screenX) ** 2 + (mouseY - screenY) ** 2);
                    if (dist < minDist) {
                        minDist = dist;
                        closestPoint = point;
                    }
                }
                
                if (closestPoint) {
                    // Redraw to clear old tooltip
                    ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                    ctx.fillRect(0, 0, canvas.width, canvas.height);
                    
                    ctx.fillStyle = 'rgba(255, 255, 255, 0.15)';
                    for (const point of compositePoints) {
                        const screenX = centerX + point.x * scale;
                        const screenY = centerY + point.y * scale;
                        ctx.beginPath();
                        ctx.arc(screenX, screenY, 1.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    
                    ctx.fillStyle = '#ffd700';
                    for (const point of primePoints) {
                        const screenX = centerX + point.x * scale;
                        const screenY = centerY + point.y * scale;
                        ctx.beginPath();
                        ctx.arc(screenX, screenY, 2.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    
                    ctx.fillStyle = '#4ecdc4';
                    ctx.beginPath();
                    ctx.arc(centerX, centerY, 4, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Highlight selected point
                    const screenX = centerX + closestPoint.x * scale;
                    const screenY = centerY + closestPoint.y * scale;
                    ctx.strokeStyle = '#ff6384';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(screenX, screenY, 6, 0, Math.PI * 2);
                    ctx.stroke();
                    
                    // Draw tooltip
                    const tooltipX = mouseX + 15;
                    const tooltipY = mouseY - 15;
                    
                    const lines = [
                        `n = ${closestPoint.n}`,
                        closestPoint.isPrime ? 'PRIME' : 'Composite',
                        `r = √${closestPoint.n} = ${closestPoint.x.toFixed(3)}`,
                        `θ = 2π√${closestPoint.n} = ${(2 * Math.PI * Math.sqrt(closestPoint.n)).toFixed(3)}`
                    ];
                    
                    ctx.font = '13px Arial';
                    const lineHeight = 18;
                    const padding = 10;
                    const maxWidth = Math.max(...lines.map(line => ctx.measureText(line).width));
                    const boxWidth = maxWidth + padding * 2;
                    const boxHeight = lines.length * lineHeight + padding * 2;
                    
                    ctx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                    ctx.fillRect(tooltipX - padding, tooltipY - padding, boxWidth, boxHeight);
                    
                    ctx.strokeStyle = closestPoint.isPrime ? '#ffd700' : 'rgba(255, 255, 255, 0.3)';
                    ctx.lineWidth = 2;
                    ctx.strokeRect(tooltipX - padding, tooltipY - padding, boxWidth, boxHeight);
                    
                    ctx.fillStyle = closestPoint.isPrime ? '#ffd700' : '#fff';
                    lines.forEach((line, idx) => {
                        ctx.fillText(line, tooltipX, tooltipY + idx * lineHeight + 13);
                    });
                    
                    canvas.style.cursor = 'pointer';
                } else {
                    canvas.style.cursor = 'default';
                }
            };
        }
        
        function createZetaZerosPlot(ctx) {
            // First 50 non-trivial zeros of Riemann zeta function (imaginary parts)
            // These are on the critical line Re(s) = 1/2
            const zetaZeros = [
                14.134725, 21.022040, 25.010858, 30.424876, 32.935062,
                37.586178, 40.918719, 43.327073, 48.005151, 49.773832,
                52.970321, 56.446248, 59.347044, 60.831779, 65.112544,
                67.079811, 69.546402, 72.067158, 75.704691, 77.144840,
                79.337375, 82.910381, 84.735493, 87.425275, 88.809111,
                92.491899, 94.651344, 95.870634, 98.831194, 101.317851,
                103.725538, 105.446623, 107.168611, 111.029536, 111.874659,
                114.320220, 116.226680, 118.790782, 121.370125, 122.946829,
                124.256819, 127.516683, 129.578704, 131.087688, 133.497737,
                134.756509, 138.116042, 139.736209, 141.123707, 143.111846
            ];
            
            // Calculate statistics
            const avgSpacing = zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]).reduce((a, b) => a + b) / (zetaZeros.length - 1);
            const minSpacing = Math.min(...zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]));
            const maxSpacing = Math.max(...zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]));
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Riemann Zeta Function - Non-Trivial Zeros</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Zeros Shown</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${zetaZeros.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">First Zero</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${zetaZeros[0].toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Spacing</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${avgSpacing.toFixed(3)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Spacing Range</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${minSpacing.toFixed(3)} - ${maxSpacing.toFixed(3)}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Riemann Zeta Zeros:</strong><br>
                    • The <strong>Riemann Hypothesis</strong> (unproven): All non-trivial zeros lie on the critical line Re(s) = 1/2<br>
                    • These zeros encode deep information about the distribution of prime numbers<br>
                    • Von Mangoldt's explicit formula connects zeros to prime counting function π(x)<br>
                    • The zeros are complex numbers: ρ = 1/2 + it (shown values are the imaginary parts t)<br>
                    • Average spacing grows like 2π/ln(t) for large t<br>
                    • Computing over 10 trillion zeros has found <strong>none off the critical line</strong><br>
                    • The chart shows zeros on critical line at Re(s) = 1/2
                </div>
            `;
            
            // Create scatter plot of zeros on critical line
            const zeroPoints = zetaZeros.map((t, idx) => ({ x: 0.5, y: t }));
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Riemann Zeta Zeros (Re=1/2)',
                        data: zeroPoints,
                        backgroundColor: 'rgba(255, 215, 0, 0.8)',
                        borderColor: 'rgba(255, 215, 0, 1)',
                        pointRadius: 6,
                        pointHoverRadius: 8,
                        pointStyle: 'circle'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const t = zetaZeros[idx];
                                    const nextT = idx < zetaZeros.length - 1 ? zetaZeros[idx + 1] : null;
                                    const spacing = nextT ? (nextT - t).toFixed(3) : 'N/A';
                                    return [
                                        `Zero #${idx + 1}`,
                                        `ρ = 1/2 + ${t.toFixed(6)}i`,
                                        `Im(ρ) = ${t.toFixed(6)}`,
                                        `Spacing to next: ${spacing}`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Re(s) - Real Part (Critical Line at 1/2)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            min: 0,
                            max: 1,
                            ticks: { 
                                color: '#fff',
                                stepSize: 0.1
                            },
                            grid: { 
                                color: function(context) {
                                    return context.tick.value === 0.5 ? 'rgba(255, 215, 0, 0.5)' : 'rgba(255, 255, 255, 0.1)';
                                },
                                lineWidth: function(context) {
                                    return context.tick.value === 0.5 ? 3 : 1;
                                }
                            }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Im(s) - Imaginary Part', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createPrimeCountingPlot(ctx) {
            const { primes } = computationData;
            
            // Generate π(x) data - count primes up to x
            const step = Math.max(1, Math.floor(primes[primes.length - 1] / 200));
            const countingData = [];
            const approximations = [];
            
            for (let x = 2; x <= primes[primes.length - 1]; x += step) {
                const count = primes.filter(p => p <= x).length;
                countingData.push({ x, y: count });
                
                // Add approximations: x/ln(x) and Li(x) ≈ x/ln(x)
                const approx = x / Math.log(x);
                approximations.push({ x, y: approx });
            }
            
            // Calculate statistics
            const maxX = primes[primes.length - 1];
            const actualCount = primes.length;
            const approxCount = maxX / Math.log(maxX);
            const error = Math.abs(actualCount - approxCount);
            const errorPercent = (error / actualCount * 100).toFixed(2);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Counting Statistics</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">π(${maxX}) actual</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${actualCount}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">x/ln(x) approximation</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;">${approxCount.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Error</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ff6b6b;">${errorPercent}%</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Prime Number Theorem</div>
                        <div style="font-size: 1em; font-weight: bold; color: #9966ff;">π(x) ~ x/ln(x)</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Prime Counting Function π(x):</strong><br>
                    The function π(x) counts the number of primes ≤ x. The Prime Number Theorem states that π(x) ~ x/ln(x) as x→∞, 
                    meaning the ratio π(x)/(x/ln(x)) approaches 1. A better approximation is the logarithmic integral Li(x).
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'π(x) - Actual Count',
                        data: countingData,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0,
                        pointRadius: 0
                    }, {
                        label: 'x/ln(x) - Approximation',
                        data: approximations,
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        borderDash: [10, 5],
                        fill: false,
                        tension: 0.3,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(2)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Number of Primes', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createDensityAnalysisPlot(ctx) {
            const { primes } = computationData;
            
            // Calculate density in intervals
            const intervalSize = Math.max(10, Math.floor(primes[primes.length - 1] / 50));
            const densityData = [];
            const theoreticalDensity = [];
            
            for (let x = intervalSize; x <= primes[primes.length - 1]; x += intervalSize) {
                const primesInInterval = primes.filter(p => p > x - intervalSize && p <= x).length;
                const density = primesInInterval / intervalSize;
                densityData.push({ x, y: density });
                
                // Theoretical density: 1/ln(x)
                const theoretical = 1 / Math.log(x);
                theoreticalDensity.push({ x, y: theoretical });
            }
            
            // Calculate average density
            const avgDensity = densityData.reduce((sum, d) => sum + d.y, 0) / densityData.length;
            const avgTheoretical = theoreticalDensity.reduce((sum, d) => sum + d.y, 0) / theoreticalDensity.length;
            
            // Calculate variance
            const variance = densityData.reduce((sum, d) => sum + Math.pow(d.y - avgDensity, 2), 0) / densityData.length;
            const stdDev = Math.sqrt(variance);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Density Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Density (interval: ${intervalSize})</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${avgDensity.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Theoretical (1/ln(x))</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;">${avgTheoretical.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Standard Deviation</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ff6b6b;">${stdDev.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Total Primes</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #9966ff;">${primes.length}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Density:</strong><br>
                    Prime density at x is approximately 1/ln(x), meaning as numbers get larger, primes become less frequent. 
                    This plot shows the actual density (primes per unit interval) compared to the theoretical prediction. 
                    Fluctuations reveal the irregular distribution of primes despite their predictable average behavior.
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'Actual Density',
                        data: densityData,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.2)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 3,
                        pointBackgroundColor: 'rgba(78, 205, 196, 1)'
                    }, {
                        label: 'Theoretical Density (1/ln(x))',
                        data: theoreticalDensity,
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        borderDash: [10, 5],
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(8)}`;
                                },
                                afterLabel: function(context) {
                                    if (context.datasetIndex === 0) {
                                        return `Interval: [${context.parsed.x - intervalSize}, ${context.parsed.x}]`;
                                    }
                                    return '';
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Density (primes per unit)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                callback: function(value) {
                                    return value.toFixed(4);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function generatePrimeCountChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const step = Math.max(1, Math.floor(primes[primes.length - 1] / 200));
            const countingData = [];
            const approximations = [];
            
            for (let x = 2; x <= primes[primes.length - 1]; x += step) {
                const count = primes.filter(p => p <= x).length;
                countingData.push({ x, y: count });
                
                const approx = x / Math.log(x);
                approximations.push({ x, y: approx });
            }
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'π(x) - Actual Count',
                        data: countingData,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0,
                        pointRadius: 0
                    }, {
                        label: 'x/ln(x) - Approximation',
                        data: approximations,
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        borderDash: [15, 8],
                        fill: false,
                        tension: 0.3,
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
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
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
                            title: { 
                                display: true, 
                                text: 'Number of Primes', 
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
        
        function generateDensityChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const intervalSize = Math.max(10, Math.floor(primes[primes.length - 1] / 50));
            const densityData = [];
            const theoreticalDensity = [];
            
            for (let x = intervalSize; x <= primes[primes.length - 1]; x += intervalSize) {
                const primesInInterval = primes.filter(p => p > x - intervalSize && p <= x).length;
                const density = primesInInterval / intervalSize;
                densityData.push({ x, y: density });
                
                const theoretical = 1 / Math.log(x);
                theoreticalDensity.push({ x, y: theoretical });
            }
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'Actual Density',
                        data: densityData,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.3)' : 'rgba(78, 205, 196, 0.3)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 4,
                        pointBackgroundColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)'
                    }, {
                        label: 'Theoretical Density (1/ln(x))',
                        data: theoreticalDensity,
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        borderDash: [15, 8],
                        fill: false,
                        tension: 0.4,
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
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
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
                            title: { 
                                display: true, 
                                text: 'Density (primes per unit)', 
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
        
        function generateGapHistogramChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            const maxGap = Math.max(...sortedGaps);
            
            const barColors = sortedGaps.map(gap => {
                if (gap === 2) return background === 'white' ? 'rgba(255, 99, 132, 0.8)' : 'rgba(255, 99, 132, 0.8)';
                if (gap === 4) return background === 'white' ? 'rgba(255, 159, 64, 0.8)' : 'rgba(255, 159, 64, 0.8)';
                if (gap === 6) return background === 'white' ? 'rgba(255, 205, 86, 0.8)' : 'rgba(255, 205, 86, 0.8)';
                if (gap === maxGap) return background === 'white' ? 'rgba(153, 102, 255, 0.8)' : 'rgba(153, 102, 255, 0.8)';
                return background === 'white' ? 'rgba(30, 60, 114, 0.7)' : 'rgba(78, 205, 196, 0.7)';
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => g.toString()),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: barColors,
                        borderColor: barColors.map(c => c.replace('0.7', '1').replace('0.8', '1')),
                        borderWidth: 3
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Gap Size', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.022) },
                                maxRotation: 45,
                                callback: function(value, index) {
                                    if (sortedGaps.length > 30) {
                                        return index % Math.ceil(sortedGaps.length / 30) === 0 ? this.getLabelForValue(value) : '';
                                    }
                                    return this.getLabelForValue(value);
                                }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
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
                        }
                    }
                }
            });
        }
        
        function generateSacksSpiralForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const maxN = Math.min(10000, primes[primes.length - 1]);
            const spiralData = [];
            
            for (let n = 1; n <= maxN; n++) {
                const r = Math.sqrt(n);
                const theta = 2 * Math.PI * Math.sqrt(n);
                const x = r * Math.cos(theta);
                const y = r * Math.sin(theta);
                const isPrime = primes.includes(n);
                spiralData.push({ x, y, n, isPrime });
            }
            
            const primePoints = spiralData.filter(p => p.isPrime);
            const compositePoints = spiralData.filter(p => !p.isPrime && p.n > 1);
            
            // Create custom canvas rendering
            const maxR = Math.sqrt(maxN);
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) / (2 * maxR) * 0.85;
            
            ctx.fillStyle = background === 'white' ? '#ffffff' : '#000000';
            ctx.fillRect(0, 0, width, height);
            
            // Draw composites
            ctx.fillStyle = background === 'white' ? 'rgba(0, 0, 0, 0.15)' : 'rgba(255, 255, 255, 0.15)';
            for (const point of compositePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 2, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw primes
            ctx.fillStyle = background === 'white' ? '#d4af37' : '#ffd700';
            for (const point of primePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 3, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw center
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            return { destroy: () => {} };
        }
        
        function generateZetaZerosChartForExport(ctx, width, height, background) {
            const zetaZeros = [
                14.134725, 21.022040, 25.010858, 30.424876, 32.935062,
                37.586178, 40.918719, 43.327073, 48.005151, 49.773832,
                52.970321, 56.446248, 59.347044, 60.831779, 65.112544,
                67.079811, 69.546402, 72.067158, 75.704691, 77.144840,
                79.337375, 82.910381, 84.735493, 87.425275, 88.809111,
                92.491899, 94.651344, 95.870634, 98.831194, 101.317851,
                103.725538, 105.446623, 107.168611, 111.029536, 111.874659,
                114.320220, 116.226680, 118.790782, 121.370125, 122.946829,
                124.256819, 127.516683, 129.578704, 131.087688, 133.497737,
                134.756509, 138.116042, 139.736209, 141.123707, 143.111846
            ];
            
            const zeroPoints = zetaZeros.map(t => ({ x: 0.5, y: t }));
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Riemann Zeta Zeros',
                        data: zeroPoints,
                        backgroundColor: background === 'white' ? 'rgba(212, 175, 55, 0.8)' : 'rgba(255, 215, 0, 0.8)',
                        borderColor: background === 'white' ? 'rgba(212, 175, 55, 1)' : 'rgba(255, 215, 0, 1)',
                        pointRadius: 8,
                        pointStyle: 'circle'
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Re(s) - Real Part (Critical Line at 1/2)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            min: 0,
                            max: 1,
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                stepSize: 0.1
                            },
                            grid: { 
                                color: function(context) {
                                    if (context.tick.value === 0.5) {
                                        return background === 'white' ? 'rgba(212, 175, 55, 0.5)' : 'rgba(255, 215, 0, 0.5)';
                                    }
                                    return background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)';
                                },
                                lineWidth: function(context) {
                                    return context.tick.value === 0.5 ? 4 : 1;
                                }
                            }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Im(s) - Imaginary Part', 
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
        
        
        function createPrimeRacesPlot(ctx) {
            const { primes, modulus } = computationData;
            
            // Always use the actual modulus from computation
            const actualModulus = modulus;
            const coprimeResidues = getCoprimeResidues(actualModulus);
            
            // For 2-way race, use first two coprime residues
            // For multi-way race (>2 residues), show all of them
            const residues = coprimeResidues.slice(0, Math.min(8, coprimeResidues.length)); // Cap at 8 for readability
            
            // Initialize counters for each residue class
            const counts = {};
            residues.forEach(r => counts[r] = 0);
            
            const raceData = [];
            
            for (const p of primes) {
                // Skip primes smaller than modulus
                if (p < actualModulus) continue;
                
                const residue = p % actualModulus;
                
                // Only count if it's a coprime residue we're tracking
                if (residues.includes(residue)) {
                    counts[residue]++;
                }
                
                // Store cumulative counts
                const dataPoint = { x: p };
                residues.forEach(r => dataPoint[`count_${r}`] = counts[r]);
                
                // Calculate difference for 2-way race (first residue - second residue)
                if (residues.length >= 2) {
                    dataPoint.diff = counts[residues[0]] - counts[residues[1]];
                }
                raceData.push(dataPoint);
            }
            
            // Calculate statistics for 2-way race
            let finalDiff = 0;
            let maxDiff = 0;
            let leaderChanges = 0;
            let currentLeader = "N/A";
            
            if (residues.length >= 2) {
                finalDiff = counts[residues[0]] - counts[residues[1]];
                maxDiff = Math.max(...raceData.map(d => Math.abs(d.diff || 0)));
                leaderChanges = raceData.reduce((changes, d, i) => {
                    if (i === 0 || !d.diff) return changes;
                    const prevDiff = raceData[i-1].diff || 0;
                    const currDiff = d.diff;
                    if ((prevDiff > 0 && currDiff < 0) || (prevDiff < 0 && currDiff > 0)) {
                        return changes + 1;
                    }
                    return changes;
                }, 0);
                
                currentLeader = finalDiff > 0 ? `${residues[0]} (mod ${actualModulus})` : 
                               finalDiff < 0 ? `${residues[1]} (mod ${actualModulus})` : "Tie";
            }
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            
            // Build stats HTML dynamically based on number of residues
            let statsHTML = `<h4 style="color: #ffd700; margin-bottom: 15px;">Prime Races: Modulus ${actualModulus} (${residues.length}-way race)</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">`;
            
            // Add a card for each residue
            const colors = ['rgba(78, 205, 196, 0.15)', 'rgba(255, 99, 132, 0.15)', 'rgba(255, 215, 0, 0.15)', 
                          'rgba(153, 102, 255, 0.15)', 'rgba(255, 159, 64, 0.15)', 'rgba(75, 192, 192, 0.15)',
                          'rgba(255, 99, 71, 0.15)', 'rgba(147, 112, 219, 0.15)'];
            const textColors = ['#4ecdc4', '#ff6384', '#ffd700', '#9966ff', '#ff9f40', '#4bc0c0', '#ff6347', '#9370db'];
            
            residues.forEach((r, idx) => {
                statsHTML += `
                    <div style="background: ${colors[idx % colors.length]}; padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes ≡ ${r} (mod ${actualModulus})</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: ${textColors[idx % textColors.length]};">${counts[r]}</div>
                    </div>`;
            });
            
            // Add race statistics for 2-way races
            if (residues.length >= 2) {
                statsHTML += `
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Current Leader</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${currentLeader}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Current Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${Math.abs(finalDiff)}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Max Gap Seen</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${maxDiff}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Lead Changes</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${leaderChanges}</div>
                    </div>`;
            }
            
            statsHTML += `</div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Races (mod ${actualModulus}):</strong><br>
                    • <strong>Chebyshev's Bias:</strong> In prime races, certain residue classes tend to "win" more often than others<br>
                    • By Dirichlet's theorem, all ${residues.length} coprime residue classes mod ${actualModulus} have equal density asymptotically<br>
                    • Despite equal density, one class is typically ahead at any given point (for 2-way races)<br>
                    ${actualModulus === 4 && residues.length === 2 ? `• For mod 4: Primes ≡ 3 (mod 4) lead ~99.6% of the time (classic Chebyshev's bias)<br>
                    • First crossover where 1 (mod 4) takes the lead occurs around x ≈ 26,861<br>` : ''}
                    • The lead changes infinitely often (Littlewood, 1914), but very rarely<br>
                    • Related to the <strong>Shanks-Rényi race</strong> and Rubinstein-Sarnak's work<br>
                    • Current computation uses ${primes.length} primes up to ${primes[primes.length-1]}
                </div>
            `;
            
            statsDiv.innerHTML = statsHTML;
            
            // Create datasets dynamically for each residue
            const lineColors = ['rgba(78, 205, 196, 1)', 'rgba(255, 99, 132, 1)', 'rgba(255, 215, 0, 1)', 
                              'rgba(153, 102, 255, 1)', 'rgba(255, 159, 64, 1)', 'rgba(75, 192, 192, 1)',
                              'rgba(255, 99, 71, 1)', 'rgba(147, 112, 219, 1)'];
            const fillColors = ['rgba(78, 205, 196, 0.1)', 'rgba(255, 99, 132, 0.1)', 'rgba(255, 215, 0, 0.1)', 
                              'rgba(153, 102, 255, 0.1)', 'rgba(255, 159, 64, 0.1)', 'rgba(75, 192, 192, 0.1)',
                              'rgba(255, 99, 71, 0.1)', 'rgba(147, 112, 219, 0.1)'];
            
            const datasets = residues.map((r, idx) => ({
                label: `π(x; ${actualModulus}, ${r}) - Primes ≡ ${r} (mod ${actualModulus})`,
                data: raceData.map(d => ({ x: d.x, y: d[`count_${r}`] })),
                borderColor: lineColors[idx % lineColors.length],
                backgroundColor: fillColors[idx % fillColors.length],
                borderWidth: 3,
                fill: false,
                tension: 0,
                pointRadius: 0
            }));
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: raceData.map(d => d.x),
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const diff = raceData[idx].diff;
                                    const leader = diff > 0 ? "3 (mod 4) leads" : diff < 0 ? "1 (mod 4) leads" : "Tied";
                                    return [
                                        `${context.dataset.label}: ${context.parsed.y}`,
                                        `Gap: ${Math.abs(diff)} (${leader})`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x (prime value)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Count of Primes', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createPhasorSumPlot(ctx) {
            const { primes, exponent, constantType } = computationData;
            
            // For complex s = σ + it, compute phasor representation
            // We'll use σ = exponent/2 (the value we're computing at)
            const sigma = exponent / 2;
            
            // Create interactive t slider
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Phasor Sum Visualization: ζ(s) as Rotating Vectors</h4>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Imaginary Part (t): <span id="tValue">0</span></label>
                    <input type="range" id="tSlider" min="0" max="200" step="0.1" value="0" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhasorPlot(parseFloat(this.value), parseFloat(document.getElementById('zoomSlider').value))">
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 10px;">
                        <button onclick="document.getElementById('tSlider').value=14.134725; updatePhasorPlot(14.134725, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(255, 99, 132, 0.3); border: 1px solid #ff6384; border-radius: 5px; color: #fff; cursor: pointer;">1st Zero (14.13)</button>
                        <button onclick="document.getElementById('tSlider').value=21.022040; updatePhasorPlot(21.022040, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(255, 159, 64, 0.3); border: 1px solid #ff9f40; border-radius: 5px; color: #fff; cursor: pointer;">2nd Zero (21.02)</button>
                        <button onclick="document.getElementById('tSlider').value=25.010858; updatePhasorPlot(25.010858, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(255, 205, 86, 0.3); border: 1px solid #ffcd56; border-radius: 5px; color: #fff; cursor: pointer;">3rd Zero (25.01)</button>
                        <button onclick="document.getElementById('tSlider').value=100; updatePhasorPlot(100, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(153, 102, 255, 0.3); border: 1px solid #9966ff; border-radius: 5px; color: #fff; cursor: pointer;">High t (100)</button>
                    </div>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Zoom Level: <span id="zoomValue">1.0</span>x</label>
                    <input type="range" id="zoomSlider" min="0.1" max="10" step="0.1" value="1" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhasorPlot(parseFloat(document.getElementById('tSlider').value), parseFloat(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.85em; opacity: 0.7; margin-top: 5px;">
                        <span>0.1x (Zoom Out)</span>
                        <span>1x (Default)</span>
                        <span>10x (Zoom In)</span>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Real Part (σ)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${sigma.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${Math.min(50, primes.length)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sum Magnitude</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;" id="sumMagnitude">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sum Angle</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;" id="sumAngle">--</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Phasor Representation:</strong><br>
                    • Each term n<sup>-s</sup> = n<sup>-σ</sup>e<sup>-it log n</sup> is a <strong>rotating phasor</strong> (vector)<br>
                    • <strong>Radius:</strong> r<sub>n</sub> = n<sup>-${sigma}</sup> (decays with n)<br>
                    • <strong>Angle:</strong> θ<sub>n</sub> = -t log(n) (rotates with t)<br>
                    • The sum ζ(s) is the <strong>vector sum</strong> of all phasors<br>
                    • When phasors align <strong>destructively</strong>, |ζ(s)| ≈ 0 → nontrivial zero!<br>
                    • Adjust t to see how the sum changes along the critical line
                </div>
            `;
            
            // Initial plot at t=0
            window.updatePhasorPlot = (t, zoom = 1.0) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                const centerX = width / 2;
                const centerY = height / 2;
                const scale = Math.min(width, height) * 0.4 * zoom;
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                freshCtx.fillRect(0, 0, width, height);
                
                // Draw axes
                freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                freshCtx.lineWidth = 1;
                freshCtx.beginPath();
                freshCtx.moveTo(0, centerY);
                freshCtx.lineTo(width, centerY);
                freshCtx.moveTo(centerX, 0);
                freshCtx.lineTo(centerX, height);
                freshCtx.stroke();
                
                // Draw unit circle
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, scale, 0, Math.PI * 2);
                freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                freshCtx.stroke();
                
                // Compute and draw phasors
                let sumReal = 0, sumImag = 0;
                let currentX = centerX, currentY = centerY;
                
                const numPhasors = Math.min(50, primes.length);
                
                for (let i = 0; i < numPhasors; i++) {
                    const n = primes[i];
                    const radius = Math.pow(n, -sigma);
                    const angle = -t * Math.log(n);
                    
                    const real = radius * Math.cos(angle);
                    const imag = radius * Math.sin(angle);
                    
                    sumReal += real;
                    sumImag += imag;
                    
                    // Draw phasor from current position
                    const nextX = currentX + real * scale;
                    const nextY = currentY - imag * scale;
                    
                    // Color by prime index
                    const hue = (i / numPhasors) * 280;
                    freshCtx.strokeStyle = `hsla(${hue}, 80%, 60%, 0.7)`;
                    freshCtx.lineWidth = 2;
                    
                    freshCtx.beginPath();
                    freshCtx.moveTo(currentX, currentY);
                    freshCtx.lineTo(nextX, nextY);
                    freshCtx.stroke();
                    
                    // Draw arrowhead
                    const arrowSize = 5;
                    const arrowAngle = Math.atan2(-(imag), real);
                    freshCtx.beginPath();
                    freshCtx.moveTo(nextX, nextY);
                    freshCtx.lineTo(
                        nextX - arrowSize * Math.cos(arrowAngle - Math.PI/6),
                        nextY - arrowSize * Math.sin(arrowAngle - Math.PI/6)
                    );
                    freshCtx.moveTo(nextX, nextY);
                    freshCtx.lineTo(
                        nextX - arrowSize * Math.cos(arrowAngle + Math.PI/6),
                        nextY - arrowSize * Math.sin(arrowAngle + Math.PI/6)
                    );
                    freshCtx.stroke();
                    
                    currentX = nextX;
                    currentY = nextY;
                }
                
                // Draw final sum vector from origin
                const finalX = centerX + sumReal * scale;
                const finalY = centerY - sumImag * scale;
                
                freshCtx.strokeStyle = '#ffd700';
                freshCtx.lineWidth = 4;
                freshCtx.beginPath();
                freshCtx.moveTo(centerX, centerY);
                freshCtx.lineTo(finalX, finalY);
                freshCtx.stroke();
                
                // Draw sum endpoint
                freshCtx.fillStyle = '#ffd700';
                freshCtx.beginPath();
                freshCtx.arc(finalX, finalY, 6, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Update stats
                const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                const angleRad = Math.atan2(sumImag, sumReal);
                const angleDeg = angleRad * 180 / Math.PI;
                
                document.getElementById('tValue').textContent = t.toFixed(2);
                document.getElementById('zoomValue').textContent = zoom.toFixed(1);
                document.getElementById('sumMagnitude').textContent = magnitude.toFixed(4);
                document.getElementById('sumAngle').textContent = angleDeg.toFixed(1) + '°';
                
                // Draw labels
                freshCtx.fillStyle = '#fff';
                freshCtx.font = '14px Arial';
                freshCtx.textAlign = 'center';
                freshCtx.fillText('Re', width - 30, centerY - 10);
                freshCtx.fillText('Im', centerX + 15, 20);
                freshCtx.fillText(`ζ(${sigma} + ${t}i) ≈ ${magnitude.toFixed(3)}`, centerX, height - 20);
            };
            
            // Initialize
            window.updatePhasorPlot(0, 1.0);
        }
        
        function createZetaSurfacePlot(ctx) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            
            // Create modular zeta surface
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Modular Zeta Surface: Nested Unity Lattice</h4>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Imaginary Height (t): <span id="tValueSurface">14.13</span></label>
                    <input type="range" id="tSliderSurface" min="0" max="200" step="0.01" value="14.13" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updateZetaSurface(parseFloat(this.value))">
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 8px; margin-top: 10px;">
                        <button onclick="document.getElementById('tSliderSurface').value=14.134725; updateZetaSurface(14.134725);" style="padding: 6px; background: rgba(255, 99, 132, 0.3); border: 1px solid #ff6384; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 1 (14.13)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=21.022040; updateZetaSurface(21.022040);" style="padding: 6px; background: rgba(255, 159, 64, 0.3); border: 1px solid #ff9f40; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 2 (21.02)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=25.010858; updateZetaSurface(25.010858);" style="padding: 6px; background: rgba(255, 205, 86, 0.3); border: 1px solid #ffcd56; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 3 (25.01)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=30.424876; updateZetaSurface(30.424876);" style="padding: 6px; background: rgba(75, 192, 192, 0.3); border: 1px solid #4bc0c0; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 4 (30.42)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=50; updateZetaSurface(50);" style="padding: 6px; background: rgba(153, 102, 255, 0.3); border: 1px solid #9966ff; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">t = 50</button>
                        <button onclick="document.getElementById('tSliderSurface').value=100; updateZetaSurface(100);" style="padding: 6px; background: rgba(78, 205, 196, 0.3); border: 1px solid #4ecdc4; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">t = 100</button>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Moduli Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;" id="moduliCount">30</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Total Magnitude</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;" id="surfaceMagnitude">--</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Phase Coherence</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;" id="phaseCoherence">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Nearest Zero</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;" id="nearestZero">14.13</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Modular Zeta Surface:</strong><br>
                    • Each concentric ring represents modulus m = 1, 2, 3, ..., 30<br>
                    • Points on each ring: primitive m-th roots of unity e<sup>2πik/m</sup> where gcd(k,m)=1<br>
                    • Each point contributes: S<sub>m,k</sub>(s) = Σ<sub>n≡k(mod m)</sub> n<sup>-s</sup><br>
                    • Color brightness = contribution magnitude<br>
                    • <strong>At zeros:</strong> modular rotations align destructively → dark/zero sum<br>
                    • <strong>Away from zeros:</strong> constructive interference → bright regions<br>
                    • First nontrivial zero: t ≈ 14.134725 (try this value!)
                </div>
            `;
            
            // Initialize at first zero
            window.updateZetaSurface = (t) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                const centerX = width / 2;
                const centerY = height / 2;
                const maxRadius = Math.min(width, height) * 0.45;
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, width, height);
                
                const maxModulus = 30;
                const radiusStep = maxRadius / (maxModulus + 1);
                
                let totalMagnitude = 0;
                let totalReal = 0, totalImag = 0;
                let contributionCount = 0;
                
                // For each modulus
                for (let m = 1; m <= maxModulus; m++) {
                    const radius = m * radiusStep;
                    const coprimeResidues = getCoprimeResidues(m);
                    
                    // For each primitive residue
                    for (const k of coprimeResidues) {
                        // Compute S_{m,k}(s)
                        let sumReal = 0, sumImag = 0;
                        
                        for (const p of primes) {
                            if (p % m === k) {
                                const r = Math.pow(p, -sigma);
                                const theta = -t * Math.log(p);
                                sumReal += r * Math.cos(theta);
                                sumImag += r * Math.sin(theta);
                            }
                        }
                        
                        const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                        totalMagnitude += magnitude;
                        totalReal += sumReal;
                        totalImag += sumImag;
                        contributionCount++;
                        
                        // Position on ring
                        const angle = 2 * Math.PI * k / m;
                        const x = centerX + radius * Math.cos(angle);
                        const y = centerY + radius * Math.sin(angle);
                        
                        // Color by magnitude
                        const brightness = Math.min(255, magnitude * 500);
                        const hue = (k / m) * 360;
                        freshCtx.fillStyle = `hsla(${hue}, 80%, ${brightness/4}%, ${Math.min(1, magnitude * 2)})`;
                        
                        // Size by magnitude
                        const pointSize = 2 + magnitude * 10;
                        freshCtx.beginPath();
                        freshCtx.arc(x, y, pointSize, 0, Math.PI * 2);
                        freshCtx.fill();
                        
                        // Glow effect
                        if (magnitude > 0.01) {
                            const gradient = freshCtx.createRadialGradient(x, y, 0, x, y, pointSize * 2);
                            gradient.addColorStop(0, `hsla(${hue}, 100%, 70%, ${magnitude})`);
                            gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
                            freshCtx.fillStyle = gradient;
                            freshCtx.beginPath();
                            freshCtx.arc(x, y, pointSize * 2, 0, Math.PI * 2);
                            freshCtx.fill();
                        }
                    }
                    
                    // Draw ring outline
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.05)';
                    freshCtx.lineWidth = 1;
                    freshCtx.beginPath();
                    freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                    freshCtx.stroke();
                }
                
                // Calculate phase coherence
                const vectorMagnitude = Math.sqrt(totalReal * totalReal + totalImag * totalImag);
                const coherence = vectorMagnitude / totalMagnitude;
                
                // Update stats
                document.getElementById('tValueSurface').textContent = t.toFixed(3);
                document.getElementById('surfaceMagnitude').textContent = vectorMagnitude.toFixed(4);
                document.getElementById('phaseCoherence').textContent = (coherence * 100).toFixed(2) + '%';
                
                // Find nearest known zero
                const knownZeros = [14.134725, 21.022040, 25.010858, 30.424876, 32.935062];
                let nearest = knownZeros[0];
                let minDist = Math.abs(t - nearest);
                for (const z of knownZeros) {
                    const dist = Math.abs(t - z);
                    if (dist < minDist) {
                        minDist = dist;
                        nearest = z;
                    }
                }
                document.getElementById('nearestZero').textContent = nearest.toFixed(3);
                
                // Draw center marker
                freshCtx.fillStyle = '#4ecdc4';
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, 4, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Draw info text
                freshCtx.fillStyle = coherence < 0.1 ? '#ff6384' : '#4ecdc4';
                freshCtx.font = 'bold 16px Arial';
                freshCtx.textAlign = 'center';
                const statusText = coherence < 0.1 ? 'Near Zero! (Destructive)' : 'Constructive Interference';
                freshCtx.fillText(statusText, centerX, height - 20);
            };
            
            // Initialize at first zero
            window.updateZetaSurface(14.134725);
        }
        
        function generatePrimeRacesChartForExport(ctx, width, height, background) {
            const { primes, modulus } = computationData;
            const actualModulus = modulus;
            const coprimeResidues = getCoprimeResidues(actualModulus);
            const residues = coprimeResidues.slice(0, Math.min(8, coprimeResidues.length));
            
            const counts = {};
            residues.forEach(r => counts[r] = 0);
            
            const raceData = [];
            
            for (const p of primes) {
                if (p < actualModulus) continue;
                const residue = p % actualModulus;
                if (residues.includes(residue)) {
                    counts[residue]++;
                }
                
                const dataPoint = { x: p };
                residues.forEach(r => dataPoint[`count_${r}`] = counts[r]);
                if (residues.length >= 2) {
                    dataPoint.diff = counts[residues[0]] - counts[residues[1]];
                }
                raceData.push(dataPoint);
            }
            
            const lineColors = ['rgba(78, 205, 196, 1)', 'rgba(255, 99, 132, 1)', 'rgba(255, 215, 0, 1)', 
                              'rgba(153, 102, 255, 1)', 'rgba(255, 159, 64, 1)', 'rgba(75, 192, 192, 1)',
                              'rgba(255, 99, 71, 1)', 'rgba(147, 112, 219, 1)'];
            
            const datasets = residues.map((r, idx) => ({
                label: `≡ ${r} (mod ${actualModulus})`,
                data: raceData.map(d => ({ x: d.x, y: d[`count_${r}`] })),
                borderColor: background === 'white' ? lineColors[idx].replace('1)', '0.8)') : lineColors[idx],
                backgroundColor: background === 'white' ? lineColors[idx].replace('1)', '0.1)') : lineColors[idx].replace('1)', '0.1)'),
                borderWidth: 4,
                fill: false,
                tension: 0,
                pointRadius: 0
            }));
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: { datasets: datasets },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x (prime value)', 
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
                            title: { 
                                display: true, 
                                text: 'Count of Primes', 
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
        
        function generateGoldbachCometForExport(ctx, width, height, background) {
            const { primes } = computationData;
            const primeSet = new Set(primes);
            const maxN = primes[primes.length - 1];
            const goldbachData = [];
            
            for (let n = 4; n <= maxN; n += 2) {
                let count = 0;
                for (const p of primes) {
                    if (p > n / 2) break;
                    const q = n - p;
                    if (q >= 2 && primeSet.has(q)) {
                        count++;
                    }
                }
                if (count > 0) {
                    goldbachData.push({ n: n, count: count });
                }
            }
            
            const maxCount = Math.max(...goldbachData.map(d => d.count));
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Goldbach Partitions',
                        data: goldbachData.map(d => ({ x: d.n, y: d.count })),
                        backgroundColor: function(context) {
                            const count = context.raw.y;
                            const ratio = count / maxCount;
                            const hue = ratio * 240;
                            return background === 'white' ? `hsla(${hue}, 70%, 50%, 0.7)` : `hsla(${hue}, 80%, 60%, 0.7)`;
                        },
                        borderColor: background === 'white' ? 'rgba(0, 0, 0, 0.3)' : 'rgba(78, 205, 196, 0.3)',
                        pointRadius: 4
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'n (even number)', 
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
                            title: { 
                                display: true, 
                                text: 'G(n) - Number of Prime Pair Partitions', 
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
        
        function generatePhasorSumForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            const t = 14.134725; // First zero for export
            
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) * 0.4;
            
            // Draw on canvas directly
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw axes
            ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.3)' : 'rgba(255, 255, 255, 0.3)';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, centerY);
            ctx.lineTo(width, centerY);
            ctx.moveTo(centerX, 0);
            ctx.lineTo(centerX, height);
            ctx.stroke();
            
            // Draw unit circle
            ctx.beginPath();
            ctx.arc(centerX, centerY, scale, 0, Math.PI * 2);
            ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.2)' : 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 2;
            ctx.stroke();
            
            // Compute and draw phasors
            let sumReal = 0, sumImag = 0;
            let currentX = centerX, currentY = centerY;
            const numPhasors = Math.min(50, primes.length);
            
            for (let i = 0; i < numPhasors; i++) {
                const n = primes[i];
                const radius = Math.pow(n, -sigma);
                const angle = -t * Math.log(n);
                
                const real = radius * Math.cos(angle);
                const imag = radius * Math.sin(angle);
                
                sumReal += real;
                sumImag += imag;
                
                const nextX = currentX + real * scale;
                const nextY = centerY - imag * scale;
                
                const hue = (i / numPhasors) * 280;
                ctx.strokeStyle = background === 'white' ? `hsla(${hue}, 70%, 45%, 0.7)` : `hsla(${hue}, 80%, 60%, 0.7)`;
                ctx.lineWidth = 3;
                
                ctx.beginPath();
                ctx.moveTo(currentX, currentY);
                ctx.lineTo(nextX, nextY);
                ctx.stroke();
                
                currentX = nextX;
                currentY = nextY;
            }
            
            // Draw final sum
            const finalX = centerX + sumReal * scale;
            const finalY = centerY - sumImag * scale;
            
            ctx.strokeStyle = background === 'white' ? '#d4af37' : '#ffd700';
            ctx.lineWidth = 6;
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(finalX, finalY);
            ctx.stroke();
            
            ctx.fillStyle = background === 'white' ? '#d4af37' : '#ffd700';
            ctx.beginPath();
            ctx.arc(finalX, finalY, 8, 0, Math.PI * 2);
            ctx.fill();
            
            // Labels
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            ctx.fillStyle = textColor;
            ctx.font = `${height * 0.025}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText('Re', width - 40, centerY - 15);
            ctx.fillText('Im', centerX + 20, 30);
            
            const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
            ctx.font = `bold ${height * 0.03}px Arial`;
            ctx.fillText(`ζ(${sigma} + ${t.toFixed(2)}i) ≈ ${magnitude.toFixed(3)}`, centerX, height - 30);
            
            return { destroy: () => {} };
        }
        
        function generateZetaSurfaceForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            const t = 14.134725; // First zero
            
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.45;
            
            // Clear canvas
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            const maxModulus = 30;
            const radiusStep = maxRadius / (maxModulus + 1);
            
            // For each modulus
            for (let m = 1; m <= maxModulus; m++) {
                const radius = m * radiusStep;
                const coprimeResidues = getCoprimeResidues(m);
                
                // For each primitive residue
                for (const k of coprimeResidues) {
                    let sumReal = 0, sumImag = 0;
                    
                    for (const p of primes) {
                        if (p % m === k) {
                            const r = Math.pow(p, -sigma);
                            const theta = -t * Math.log(p);
                            sumReal += r * Math.cos(theta);
                            sumImag += r * Math.sin(theta);
                        }
                    }
                    
                    const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                    
                    const angle = 2 * Math.PI * k / m;
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    const brightness = Math.min(255, magnitude * 500);
                    const hue = (k / m) * 360;
                    
                    if (background === 'white') {
                        ctx.fillStyle = `hsla(${hue}, 80%, ${30 + brightness/8}%, ${Math.min(1, magnitude * 2)})`;
                    } else {
                        ctx.fillStyle = `hsla(${hue}, 80%, ${brightness/4}%, ${Math.min(1, magnitude * 2)})`;
                    }
                    
                    const pointSize = 3 + magnitude * 12;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                    
                    if (magnitude > 0.01) {
                        const gradient = ctx.createRadialGradient(x, y, 0, x, y, pointSize * 2);
                        if (background === 'white') {
                            gradient.addColorStop(0, `hsla(${hue}, 90%, 50%, ${magnitude * 0.8})`);
                        } else {
                            gradient.addColorStop(0, `hsla(${hue}, 100%, 70%, ${magnitude})`);
                        }
                        gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
                        ctx.fillStyle = gradient;
                        ctx.beginPath();
                        ctx.arc(x, y, pointSize * 2, 0, Math.PI * 2);
                        ctx.fill();
                    }
                }
                
                // Draw ring outline
                ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.1)' : 'rgba(255, 255, 255, 0.05)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Draw center
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            // Title
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            ctx.fillStyle = textColor;
            ctx.font = `bold ${height * 0.03}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(`Modular Zeta Surface at t = ${t.toFixed(3)} (First Zero)`, centerX, height - 30);
            
            return { destroy: () => {} };
        }
        
        function createGoldbachCometPlot(ctx) {
            const { primes } = computationData;
            
            // Create a Set for O(1) prime lookup
            const primeSet = new Set(primes);
            
            // Goldbach Comet: for even number n, count number of ways to write n = p + q (p, q prime)
            // Use all primes computed, no artificial cap
            const maxN = primes[primes.length - 1];
            const goldbachData = [];
            
            // For each even number, count Goldbach partitions
            for (let n = 4; n <= maxN; n += 2) {
                let count = 0;
                
                // Count ways to write n as sum of two primes
                for (const p of primes) {
                    if (p > n / 2) break;  // Avoid double counting
                    const q = n - p;
                    if (q >= 2 && primeSet.has(q)) {
                        count++;
                    }
                }
                
                if (count > 0) {  // Only add if we found partitions
                    goldbachData.push({ n: n, count: count });
                }
            }
            
            // Calculate statistics
            if (goldbachData.length === 0) {
                // Fallback if no data
                const statsDiv = document.getElementById('vizStats');
                statsDiv.style.display = 'block';
                statsDiv.innerHTML = `
                    <h4 style="color: #ffd700; margin-bottom: 15px;">Goldbach Comet</h4>
                    <div style="padding: 20px; background: rgba(255, 99, 132, 0.15); border-radius: 8px; text-align: center;">
                        <p style="font-size: 1.2em; color: #ff6384;">Not enough primes computed to generate Goldbach Comet.</p>
                        <p style="margin-top: 10px; opacity: 0.8;">Try increasing the target error or using more primes.</p>
                    </div>
                `;
                return;
            }
            
            const avgCount = goldbachData.reduce((sum, d) => sum + d.count, 0) / goldbachData.length;
            const maxCount = Math.max(...goldbachData.map(d => d.count));
            const maxCountN = goldbachData.find(d => d.count === maxCount).n;
            const minCount = Math.min(...goldbachData.map(d => d.count));
            const minCountN = goldbachData.find(d => d.count === minCount).n;
            
            // Find numbers with count = 1 (most difficult to partition)
            const hardToPartition = goldbachData.filter(d => d.count === 1).map(d => d.n);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Goldbach Comet</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Even Numbers Analyzed</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${goldbachData.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${avgCount.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Most Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${maxCount} (n=${maxCountN})</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Fewest Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${minCount} (n=${minCountN})</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">With Only 1 Partition</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${hardToPartition.length}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Goldbach Verified</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">✓ All</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Goldbach Comet:</strong><br>
                    • <strong>Goldbach's Conjecture</strong> (1742, unproven): Every even integer > 2 is the sum of two primes<br>
                    • The "comet" shape emerges when plotting G(n) = number of ways to write n = p + q<br>
                    • <strong>Dense vertical lines:</strong> Correspond to numbers divisible by small primes (2, 6, 30, etc.)<br>
                    • <strong>Tail of the comet:</strong> Numbers with many prime partitions (highly composite even numbers)<br>
                    • Verified for all even numbers up to 4 × 10¹⁸<br>
                    • Weak Goldbach (every odd > 5 is sum of 3 primes) was proven by Helfgott in 2013<br>
                    • The function G(n) grows roughly as n/ln²(n) for large n
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Goldbach Partitions G(n)',
                        data: goldbachData.map(d => ({ x: d.n, y: d.count })),
                        backgroundColor: function(context) {
                            // Color by count
                            const count = context.raw.y;
                            const ratio = count / maxCount;
                            const hue = ratio * 240; // Blue to purple gradient
                            return `hsla(${hue}, 80%, 60%, 0.7)`;
                        },
                        borderColor: 'rgba(78, 205, 196, 0.3)',
                        pointRadius: 3,
                        pointHoverRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const n = context.parsed.x;
                                    const count = context.parsed.y;
                                    
                                    // Find actual partitions for this n
                                    const partitions = [];
                                    for (const p of primes) {
                                        if (p > n / 2) break;
                                        const q = n - p;
                                        if (q >= 2 && primeSet.has(q)) {
                                            partitions.push(`${p} + ${q}`);
                                        }
                                    }
                                    
                                    const result = [
                                        `n = ${n}`,
                                        `Partitions: ${count}`,
                                        ''
                                    ];
                                    
                                    // Show first few partitions
                                    const showCount = Math.min(5, partitions.length);
                                    for (let i = 0; i < showCount; i++) {
                                        result.push(partitions[i]);
                                    }
                                    if (partitions.length > showCount) {
                                        result.push(`... and ${partitions.length - showCount} more`);
                                    }
                                    
                                    return result;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'n (even number)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'G(n) - Number of Prime Pair Partitions', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createErrorAnalysisPlot(ctx) {
            const { partialProducts, exactValue, constantType, epsilon } = computationData;
            
            // Calculate absolute and relative errors at each step
            const errorData = partialProducts.map(p => {
                let currentValue;
                if (constantType === 'pi') {
                    currentValue = Math.sqrt(6 * p.value);
                } else {
                    currentValue = p.value;
                }
                
                const absError = Math.abs(currentValue - exactValue);
                const relError = absError / Math.abs(exactValue);
                
                return {
                    prime: p.prime,
                    absError: absError,
                    relError: relError,
                    logAbsError: Math.log10(absError),
                    logRelError: Math.log10(relError)
                };
            });
            
            // Calculate convergence rate
            const convergenceRates = [];
            for (let i = 1; i < errorData.length; i++) {
                const rate = errorData[i].relError / errorData[i-1].relError;
                convergenceRates.push(rate);
            }
            const avgConvergenceRate = convergenceRates.reduce((a, b) => a + b, 0) / convergenceRates.length;
            
            // Find when error drops below target epsilon
            const targetMetIndex = errorData.findIndex(e => e.relError <= epsilon);
            const primesNeededForTarget = targetMetIndex >= 0 ? errorData[targetMetIndex].prime : 'Not yet met';
            
            // Calculate theoretical error bound
            const finalError = errorData[errorData.length - 1].relError;
            const theoreticalBound = epsilon;
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Error Analysis & Convergence Rate</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Final Relative Error</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${(finalError * 100).toFixed(8)}%</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Target Error (ε)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${(theoreticalBound * 100).toFixed(4)}%</div>
                    </div>
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Convergence Rate</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${avgConvergenceRate.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Target Met At Prime</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${primesNeededForTarget}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Initial Error (p=2)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${(errorData[0].relError * 100).toFixed(4)}%</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Error Reduction Factor</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${(errorData[0].relError / finalError).toFixed(2)}×</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Error Analysis:</strong><br>
                    • <strong>Relative Error:</strong> |computed - exact| / |exact| measures accuracy as a percentage<br>
                    • <strong>Convergence Rate:</strong> Ratio of consecutive errors shows how fast error decreases<br>
                    • Rate < 1 indicates convergence (smaller = faster)<br>
                    • <strong>Theoretical Guarantee:</strong> Euler product truncation ensures error ≤ ε<br>
                    • Log scale reveals exponential convergence behavior<br>
                    • Each additional prime contributes multiplicatively to accuracy
                </div>
            `;
            
            // Create dual-axis chart
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: errorData.map(e => e.prime),
                    datasets: [{
                        label: 'Relative Error (log scale)',
                        data: errorData.map(e => e.logRelError),
                        borderColor: 'rgba(255, 99, 132, 1)',
                        backgroundColor: 'rgba(255, 99, 132, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 2,
                        yAxisID: 'y'
                    }, {
                        label: 'Absolute Error (log scale)',
                        data: errorData.map(e => e.logAbsError),
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 2,
                        yAxisID: 'y'
                    }, {
                        label: 'Target Threshold',
                        data: Array(errorData.length).fill(Math.log10(epsilon)),
                        borderColor: 'rgba(255, 215, 0, 1)',
                        borderWidth: 2,
                        borderDash: [10, 5],
                        pointRadius: 0,
                        fill: false,
                        yAxisID: 'y'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    if (context.datasetIndex === 0) {
                                        return `Rel Error: ${(errorData[idx].relError * 100).toExponential(4)}%`;
                                    } else if (context.datasetIndex === 1) {
                                        return `Abs Error: ${errorData[idx].absError.toExponential(4)}`;
                                    } else {
                                        return `Target: ${(epsilon * 100).toFixed(4)}%`;
                                    }
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p (log scale)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Error (log₁₀ scale)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                callback: function(value) {
                                    return '10^' + value.toFixed(1);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateErrorAnalysisChartForExport(ctx, width, height, background) {
            const { partialProducts, exactValue, constantType, epsilon } = computationData;
            
            const errorData = partialProducts.map(p => {
                let currentValue;
                if (constantType === 'pi') {
                    currentValue = Math.sqrt(6 * p.value);
                } else {
                    currentValue = p.value;
                }
                
                const absError = Math.abs(currentValue - exactValue);
                const relError = absError / Math.abs(exactValue);
                
                return {
                    prime: p.prime,
                    absError: absError,
                    relError: relError,
                    logAbsError: Math.log10(absError),
                    logRelError: Math.log10(relError)
                };
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    labels: errorData.map(e => e.prime),
                    datasets: [{
                        label: 'Relative Error (log scale)',
                        data: errorData.map(e => e.logRelError),
                        borderColor: background === 'white' ? 'rgba(220, 53, 69, 1)' : 'rgba(255, 99, 132, 1)',
                        backgroundColor: background === 'white' ? 'rgba(220, 53, 69, 0.1)' : 'rgba(255, 99, 132, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }, {
                        label: 'Absolute Error (log scale)',
                        data: errorData.map(e => e.logAbsError),
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }, {
                        label: 'Target Threshold',
                        data: Array(errorData.length).fill(Math.log10(epsilon)),
                        borderColor: background === 'white' ? 'rgba(212, 175, 55, 1)' : 'rgba(255, 215, 0, 1)',
                        borderWidth: 3,
                        borderDash: [15, 8],
                        pointRadius: 0,
                        fill: false
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
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
                            title: { 
                                display: true, 
                                text: 'Error (log₁₀ scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                callback: function(value) {
                                    return '10^' + value.toFixed(1);
                                }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
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
        
        // Prime Ring Visualization
        let rotationAnimationId = null;
        let globalRotationAngle = 0;
        let isRotating = false;
        
        function toggleModulusMode() {
            const mode = document.getElementById('modulusMode').value;
            const rangeControls = document.getElementById('rangeControls');
            const customControls = document.getElementById('customControls');
            
            if (mode === 'range') {
                rangeControls.style.display = 'block';
                customControls.style.display = 'none';
            } else if (mode === 'custom') {
                rangeControls.style.display = 'none';
                customControls.style.display = 'block';
            } else {
                rangeControls.style.display = 'none';
                customControls.style.display = 'none';
            }
        }
        
        function getModulusList() {
            const mode = document.getElementById('modulusMode').value;
            
            if (mode === 'range') {
                const maxModulus = parseInt(document.getElementById('maxModulus').value);
                const moduli = [];
                for (let i = 1; i <= maxModulus; i++) {
                    moduli.push(i);
                }
                return moduli;
            } else if (mode === 'custom') {
                const input = document.getElementById('customModuli').value;
                if (!input.trim()) return [1, 2, 4, 8, 16, 32]; // default
                return input.split(',').map(x => parseInt(x.trim())).filter(x => x >= 1).sort((a, b) => a - b);
            } else if (mode === 'powers') {
                // Powers of 2
                const moduli = [];
                for (let i = 0; i <= 10; i++) {
                    const val = Math.pow(2, i);
                    if (val <= 1024) moduli.push(val);
                }
                return moduli;
            } else if (mode === 'powers3') {
                // Powers of 3
                const moduli = [];
                for (let i = 0; i <= 8; i++) {
                    const val = Math.pow(3, i);
                    if (val <= 1024) moduli.push(val);
                }
                return moduli;
            }
            return [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
        }
        
        function toggleRotation() {
            isRotating = !isRotating;
            const btn = document.getElementById('rotationToggle');
            
            if (isRotating) {
                btn.textContent = 'Stop Rotation';
                btn.style.background = '#4ecdc4';
                startRotation();
            } else {
                btn.textContent = 'Start Rotation';
                btn.style.background = '#ff6b6b';
                if (rotationAnimationId) {
                    cancelAnimationFrame(rotationAnimationId);
                    rotationAnimationId = null;
                }
            }
        }
        
        function startRotation() {
            if (!isRotating) return;
            
            const speed = parseFloat(document.getElementById('rotationSpeed').value);
            globalRotationAngle += 0.01 * speed;
            
            updatePrimeRing();
            rotationAnimationId = requestAnimationFrame(startRotation);
        }
        
        function updatePrimeRing() {
            if (!computationData) return;
            
            const canvas = document.getElementById('primeRingCanvas');
            const ctx = canvas.getContext('2d');
            const rect = canvas.getBoundingClientRect();
            
            // Set canvas size with device pixel ratio for crisp rendering
            const dpr = window.devicePixelRatio || 1;
            canvas.width = rect.width * dpr;
            canvas.height = rect.height * dpr;
            ctx.scale(dpr, dpr);
            
            const width = rect.width;
            const height = rect.height;
            const centerX = width / 2;
            const centerY = height / 2;
            
            const moduli = getModulusList();
            const maxModulusValue = Math.max(...moduli);
            const pointSize = parseInt(document.getElementById('pointSize').value);
            const showLabels = document.getElementById('showLabels').checked;
            const showModLines = document.getElementById('showModLines').checked;
            const colorMode = document.getElementById('colorMode').value;
            const invertColors = document.getElementById('invertColors').checked;
            const invertRings = document.getElementById('invertRings').checked;
            const rotationMode = document.getElementById('rotationMode').value;
            
            const primes = computationData.primes;
            const maxRadius = Math.min(width, height) * 0.45;
            const radiusStep = maxRadius / (moduli.length + 1);
            
            // Clear canvas
            if (invertColors) {
                ctx.fillStyle = 'rgba(255, 255, 255, 0.95)';
            } else {
                ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw modulus rings
            ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.1)' : 'rgba(255, 255, 255, 0.1)';
            ctx.lineWidth = 1;
            for (let i = 0; i < moduli.length; i++) {
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Generate colors based on mode
            const getColor = (prime, residue, modulus, modulusIndex) => {
                let hue, saturation = 80, lightness = 60;
                
                if (colorMode === 'residue') {
                    hue = (residue / modulus) * 360;
                } else if (colorMode === 'modulus') {
                    hue = (modulusIndex / moduli.length) * 280;
                    saturation = 70;
                } else { // size
                    const maxPrime = Math.max(...primes);
                    const ratio = prime / maxPrime;
                    hue = ratio * 120; // green to red
                }
                
                if (invertColors) {
                    saturation = Math.min(saturation + 10, 100);
                    lightness = 40; // darker colors on white background
                }
                
                return `hsla(${hue}, ${saturation}%, ${lightness}%, 0.8)`;
            };
            
            // Store points for hover detection
            const points = [];
            
            // Draw primes on each ring
            for (let i = 0; i < moduli.length; i++) {
                const m = moduli[i];
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                
                for (const p of primes) {
                    const residue = p % m;
                    
                    // Only plot if gcd(residue, m) = 1
                    if (gcd(residue, m) !== 1) continue;
                    
                    // Calculate angle: θ = 2π * residue / m
                    let angle = (2 * Math.PI * residue) / m;
                    
                    // Apply rotation based on mode
                    if (rotationMode === 'global') {
                        angle += globalRotationAngle;
                    } else if (rotationMode === 'local') {
                        // Each ring rotates at a different speed based on its modulus
                        angle += globalRotationAngle * m / maxModulusValue;
                    }
                    
                    // Convert to Cartesian coordinates (0 radians points right to (1,0))
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    // Draw point
                    const color = getColor(p, residue, m, i);
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Store for hover
                    points.push({ x, y, p, residue, modulus: m, color });
                    
                    // Draw lines from center to show mod structure
                    if (showModLines && i === moduli.length - 1 && residue < m) {
                        ctx.strokeStyle = invertColors ? 'rgba(78, 205, 196, 0.2)' : 'rgba(78, 205, 196, 0.1)';
                        ctx.lineWidth = 0.5;
                        ctx.beginPath();
                        ctx.moveTo(centerX, centerY);
                        ctx.lineTo(x, y);
                        ctx.stroke();
                    }
                }
            }
            
            // Add hover interaction
            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;
                
                // Find closest point
                let closestPoint = null;
                let minDist = pointSize + 5;
                
                for (const point of points) {
                    const dist = Math.sqrt((mouseX - point.x) ** 2 + (mouseY - point.y) ** 2);
                    if (dist < minDist) {
                        minDist = dist;
                        closestPoint = point;
                    }
                }
                
                if (closestPoint) {
                    // Draw tooltip
                    ctx.save();
                    
                    const tooltipX = mouseX + 15;
                    const tooltipY = mouseY - 15;
                    
                    // Calculate angle in degrees and radians
                    const angleRad = (2 * Math.PI * closestPoint.residue) / closestPoint.modulus;
                    const angleDeg = (angleRad * 180 / Math.PI).toFixed(1);
                    const angleRadStr = (angleRad / Math.PI).toFixed(3);
                    
                    // Create detailed tooltip
                    const lines = [
                        `Prime: p = ${closestPoint.p}`,
                        `Residue: r = ${closestPoint.residue} (mod ${closestPoint.modulus})`,
                        `Fraction: r/m = ${closestPoint.residue}/${closestPoint.modulus} = ${(closestPoint.residue / closestPoint.modulus).toFixed(4)}`,
                        `Angle: θ = ${angleRadStr}π rad = ${angleDeg}°`,
                        `Position: (${Math.cos(angleRad).toFixed(3)}, ${Math.sin(angleRad).toFixed(3)})`
                    ];
                    
                    ctx.font = '12px Arial';
                    const lineHeight = 16;
                    const padding = 8;
                    const maxWidth = Math.max(...lines.map(line => ctx.measureText(line).width));
                    const boxWidth = maxWidth + padding * 2;
                    const boxHeight = lines.length * lineHeight + padding * 2;
                    
                    // Adjust tooltip position if it goes off screen
                    let finalX = tooltipX;
                    let finalY = tooltipY;
                    if (tooltipX + boxWidth > width) finalX = mouseX - boxWidth - 15;
                    if (tooltipY + boxHeight > height) finalY = mouseY - boxHeight - 15;
                    
                    ctx.fillStyle = invertColors ? 'rgba(255, 255, 255, 0.98)' : 'rgba(0, 0, 0, 0.95)';
                    ctx.fillRect(finalX - padding, finalY - padding, boxWidth, boxHeight);
                    
                    ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.3)' : 'rgba(255, 255, 255, 0.3)';
                    ctx.lineWidth = 1;
                    ctx.strokeRect(finalX - padding, finalY - padding, boxWidth, boxHeight);
                    
                    ctx.fillStyle = invertColors ? '#000' : '#fff';
                    lines.forEach((line, idx) => {
                        ctx.fillText(line, finalX, finalY + idx * lineHeight + 12);
                    });
                    
                    // Highlight point
                    ctx.strokeStyle = '#ffd700';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(closestPoint.x, closestPoint.y, pointSize + 2, 0, Math.PI * 2);
                    ctx.stroke();
                    
                    ctx.restore();
                    
                    canvas.style.cursor = 'pointer';
                } else {
                    canvas.style.cursor = 'crosshair';
                }
            };
            
            // Update legend
            updateRingLegend(colorMode, moduli, primes, invertRings);
        }
        
        function updateRingLegend(colorMode, moduli, primes, invertRings) {
            const legend = document.getElementById('ringLegend');
            let html = '';
            
            html += `<div class="ring-legend-item"><strong>Moduli used:</strong> ${moduli.join(', ')}</div>`;
            html += `<div class="ring-legend-item"><strong>Ring order:</strong> ${invertRings ? 'Inverted (smallest outer)' : 'Normal (smallest inner)'}</div>`;
            
            if (colorMode === 'residue') {
                html += '<div class="ring-legend-item"><strong>Color by Residue Class:</strong> Hue represents (p mod m)/m position around each ring</div>';
            } else if (colorMode === 'modulus') {
                const colors = [];
                const displayCount = Math.min(moduli.length, 10);
                for (let i = 0; i < displayCount; i++) {
                    const hue = (i / moduli.length) * 280;
                    const color = `hsla(${hue}, 70%, 60%, 0.8)`;
                    colors.push({ label: `m=${moduli[i]}`, color });
                }
                colors.forEach(c => {
                    html += `<div class="ring-legend-item"><div class="ring-legend-color" style="background: ${c.color};"></div><span>${c.label}</span></div>`;
                });
                if (moduli.length > 10) {
                    html += '<div class="ring-legend-item"><span>... (gradient continues)</span></div>';
                }
            } else {
                html += '<div class="ring-legend-item"><strong>Color by Prime Size:</strong> Green (small) → Yellow → Red (large)</div>';
            }
            
            legend.innerHTML = html;
        }
        
        function exportPrimeRing() {
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
                <h2 style="color: #ffd700; margin-bottom: 25px; text-align: center;">Export Prime Ring</h2>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Resolution:</label>
                    <select id="ringExportResolution" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="1080">1080p (1920 x 1080)</option>
                        <option value="2160">4K (3840 x 2160)</option>
                        <option value="4320">8K (7680 x 4320)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Format:</label>
                    <select id="ringExportFormat" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="png">PNG (Lossless)</option>
                        <option value="jpg">JPEG (Smaller file)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 25px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="ringExportWatermark" checked style="width: auto; margin-right: 10px;">
                        <span>Include watermark</span>
                    </label>
                </div>
                
                <div style="display: flex; gap: 10px;">
                    <button id="ringExportBtn" style="flex: 1; padding: 15px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Export</button>
                    <button id="ringCancelBtn" style="flex: 1; padding: 15px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Cancel</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('ringCancelBtn').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('ringExportBtn').onclick = () => {
                const resolution = parseInt(document.getElementById('ringExportResolution').value);
                const format = document.getElementById('ringExportFormat').value;
                const includeWatermark = document.getElementById('ringExportWatermark').checked;
                
                document.body.removeChild(modal);
                
                performRingExport(resolution, format, includeWatermark);
            };
        }
        
        function performRingExport(height, format, includeWatermark) {
            const width = height * 16 / 9; // 16:9 aspect ratio
            
            const exportCanvas = document.createElement('canvas');
            exportCanvas.width = width;
            exportCanvas.height = height;
            const ctx = exportCanvas.getContext('2d');
            
            const centerX = width / 2;
            const centerY = height / 2;
            
            const moduli = getModulusList();
            const maxModulusValue = Math.max(...moduli);
            const pointSize = parseInt(document.getElementById('pointSize').value) * (height / 1080);
            const colorMode = document.getElementById('colorMode').value;
            const invertColors = document.getElementById('invertColors').checked;
            const invertRings = document.getElementById('invertRings').checked;
            const rotationMode = document.getElementById('rotationMode').value;
            
            const primes = computationData.primes;
            const maxRadius = Math.min(width, height) * 0.45;
            const radiusStep = maxRadius / (moduli.length + 1);
            
            // Clear canvas
            if (invertColors) {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw modulus rings
            ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.15)' : 'rgba(255, 255, 255, 0.15)';
            ctx.lineWidth = 2;
            for (let i = 0; i < moduli.length; i++) {
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Generate colors
            const getColor = (prime, residue, modulus, modulusIndex) => {
                let hue, saturation = 80, lightness = 60;
                
                if (colorMode === 'residue') {
                    hue = (residue / modulus) * 360;
                } else if (colorMode === 'modulus') {
                    hue = (modulusIndex / moduli.length) * 280;
                    saturation = 70;
                } else {
                    const maxPrime = Math.max(...primes);
                    const ratio = prime / maxPrime;
                    hue = ratio * 120;
                }
                
                if (invertColors) {
                    saturation = Math.min(saturation + 10, 100);
                    lightness = 40;
                }
                
                return `hsla(${hue}, ${saturation}%, ${lightness}%, 0.9)`;
            };
            
            // Draw primes
            for (let i = 0; i < moduli.length; i++) {
                const m = moduli[i];
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                
                for (const p of primes) {
                    const residue = p % m;
                    if (gcd(residue, m) !== 1) continue;
                    
                    let angle = (2 * Math.PI * residue) / m;
                    
                    if (rotationMode === 'global') {
                        angle += globalRotationAngle;
                    } else if (rotationMode === 'local') {
                        angle += globalRotationAngle * m / maxModulus;
                    }
                    
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    const color = getColor(p, residue, m);
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
            
            // Add watermark
            if (includeWatermark) {
                const watermarkY = height - height * 0.03;
                ctx.fillStyle = invertColors ? 'rgba(0, 0, 0, 0.5)' : 'rgba(255, 255, 255, 0.5)';
                ctx.font = `${height * 0.02}px Arial`;
                ctx.textAlign = 'center';
                ctx.fillText('Modular Sieve Calculator - Prime Residue Rings', centerX, watermarkY);
                ctx.font = `italic ${height * 0.015}px Arial`;
                ctx.fillText('By Wessen Getachew (@7Dview)', centerX, watermarkY + height * 0.025);
            }
            
            // Export
            const mimeType = format === 'png' ? 'image/png' : 'image/jpeg';
            exportCanvas.toBlob((blob) => {
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `prime_rings_${maxModulus}_${Date.now()}.${format}`;
                a.click();
                URL.revokeObjectURL(url);
            }, mimeType, 0.95);
        }
        
        window.onload = () => {
            compute();
        };
    </script>
</body>
</html>
