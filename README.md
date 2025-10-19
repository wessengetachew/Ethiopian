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
                    
                    <p style="margin-top: 15px;"><strong>Error Control:</strong> For target error ε, include primes up to:</p>
                    <div class="formula">
                        Y ≈ 1 + 1/ε  (for π)<br>
                        Y ≈ (2/((2n-1)·ε))<sup>1/(2n-1)</sup>  (for ζ(2n))
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('methods')">
                    <h3>Decomposition Methods</h3>
                    <span class="toggle-icon" id="methods-icon">▼</span>
                </div>
                <div id="methods-content" class="collapsible-content">
                    <p><strong>1. Standard Euler Product:</strong> Direct computation using all primes without decomposition.</p>
                    
                    <p><strong>2. Gap-Class Analysis:</strong> Groups primes by their gaps g(p) = p - p<sub>prev</sub>. Shows distribution of twin primes (gap=2), cousin primes (gap=4), etc.</p>
                    
                    <p><strong>3. Residue Channels (Custom Mod):</strong> Splits primes by residue classes mod m, giving φ(m) independent channels for gcd(a,m)=1. Demonstrates Dirichlet's theorem on primes in arithmetic progressions.</p>
                    
                    <p><strong>4. Quadratic Residue Classes:</strong> Partitions primes p by whether a fixed value a is a quadratic residue mod p (solvability of x² ≡ a mod p). Uses Legendre symbol (a/p) = ±1.</p>
                    
                    <p><strong>5. Arithmetic Progression Channels:</strong> Similar to residue channels but emphasizes the arithmetic progression structure p ≡ a (mod m). Visualizes Dirichlet density theorem.</p>
                    
                    <p><strong>6. Prime Constellations:</strong> Finds clusters of primes in admissible patterns: twin (p, p+2), triplet (p, p+2, p+6), quadruplet (p, p+2, p+6, p+8), etc. Shows rarity of higher-order k-tuples.</p>
                    
                    <p><strong>7. Digit Sum Partitions:</strong> Groups primes by digital root (repeated digit sum). All primes > 3 have digital roots in {1,2,4,5,7,8} mod 9, never {3,6,9}.</p>
                    
                    <p><strong>8. Binary Weight Classes:</strong> Partitions primes by Hamming weight (popcount) - the number of 1-bits in binary representation. Links to computational number theory.</p>
                    
                    <p><strong>9. Primitive Root Decomposition:</strong> Classifies primes p by their smallest primitive root g. A primitive root generates all units mod p via powers g¹, g², ..., g^(p-1).</p>
                    
                    <p><strong>10. Sophie Germain Chains:</strong> Tracks chains where p, 2p+1, 4p+3, ... are all prime. Prime p with 2p+1 prime is a Sophie Germain prime; 2p+1 is a safe prime. Shows chain length distribution.</p>
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
                        <strong>Note:</strong> This calculator is an educational tool designed to demonstrate the power of Euler products and modular arithmetic in computing fundamental mathematical constants. It combines classical number theory with modern computational methods and interactive visualization.
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
                        WARNING: Digits beyond 15-17 may not be accurate due to floating-point precision limits
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
                        <option value="quadratic">Quadratic Residue Classes</option>
                        <option value="arithmetic">Arithmetic Progression Channels</option>
                        <option value="constellation">Prime Constellations</option>
                        <option value="digitsum">Digit Sum Partitions</option>
                        <option value="binaryweight">Binary Weight Classes</option>
                        <option value="primitiveroot">Primitive Root Decomposition</option>
                        <option value="sophiegermain">Sophie Germain Chains</option>
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
                    <button class="viz-btn" onclick="changeViz('methodComparison')">Method Comparison</button>
                    <button class="viz-btn" onclick="changeViz('densityAnalysis')">Density Analysis</button>
                </div>
                <canvas id="vizCanvas"></canvas>
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
                        <input type="checkbox" id="showGCDLabels">
                        Show GCD/Farey Labels
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
                        <input type="checkbox" id="showLiftConnections">
                        Show r→r Lift Connections
                    </label>
                    <label>
                        Lift Thickness:
                        <input type="number" id="liftThickness" value="1" min="0.5" max="5" step="0.5">
                    </label>
                    <label>
                        <input type="checkbox" id="showGapConnections">
                        Show Gap Connections (r, r+2n)
                    </label>
                    <label>
                        Gap Thickness:
                        <input type="number" id="gapThickness" value="1.5" min="0.5" max="5" step="0.5">
                    </label>
                    <label>
                        Color By:
                        <select id="colorMode">
                            <option value="residue">Residue Class</option>
                            <option value="modulus">Modulus Level</option>
                            <option value="size">Prime Size</option>
                            <option value="gcd">GCD (Farey)</option>
                        </select>
                    </label>
                    <label style="flex: 1;">
                        Lift Color:
                        <input type="color" id="liftColor" value="#4ecdc4">
                    </label>
                    <label style="flex: 1;">
                        Gap Color (base):
                        <input type="color" id="gapColor" value="#ff6b6b">
                    </label>
                    <button onclick="updatePrimeRing()" style="padding: 6px 16px; background: #4ecdc4; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Update</button>
                </div>
                <div class="ring-controls" style="margin-top: 10px;">
                    <label>
                        Gap Pattern:
                        <select id="gapPattern" onchange="updateGapPatternUI()">
                            <option value="custom">Custom Gaps</option>
                            <option value="twin">Twin Primes (2)</option>
                            <option value="cousin">Cousin Primes (4)</option>
                            <option value="sexy">Sexy Primes (6)</option>
                            <option value="tuple-3">Prime Triplet (2,6)</option>
                            <option value="tuple-4">Prime Quadruplet (2,6,8)</option>
                            <option value="tuple-5">Prime Quintuplet (2,6,8,12)</option>
                            <option value="all-even">All Even Gaps (2,4,6,...)</option>
                        </select>
                    </label>
                    <div id="customGapInput">
                        <label style="flex: 1;">
                            Custom Gaps (comma-separated):
                            <input type="text" id="customGaps" placeholder="e.g., 2,4,6" value="2,4,6" style="width: 100%;">
                        </label>
                    </div>
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
                    <br><strong>Lift Connections (r→r):</strong> Connect primes with same residue r across consecutive modulus rings (m to m+1). Shows how residue classes "lift" through the modular hierarchy.
                    <br><strong>Gap Connections (p, p+gap):</strong> On the largest modulus ring, connect prime p at residue r to prime p+gap at residue r' when both are prime.
                    Visualizes prime gaps (twin primes: gap=2, cousin primes: gap=4, sexy primes: gap=6, prime k-tuples, etc.).
                    Each gap size is shown in a different color. Statistics show the count of each gap pattern found.
                    <br><strong>Presets:</strong> Powers of 2 (1,2,4,8,...), Powers of 3 (1,3,9,27,...), or custom list.
                    Hover over points to see prime details and gap connections.
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
        
        // Quadratic residue check (Legendre symbol for prime modulus)
        function isQuadraticResidue(a, p) {
            if (p === 2) return true;
            // Use Euler's criterion: a^((p-1)/2) ≡ 1 (mod p) for QR
            const exp = (p - 1) / 2;
            return modPow(a % p, exp, p) === 1;
        }
        
        // Modular exponentiation
        function modPow(base, exp, mod) {
            let result = 1;
            base = base % mod;
            while (exp > 0) {
                if (exp % 2 === 1) result = (result * base) % mod;
                exp = Math.floor(exp / 2);
                base = (base * base) % mod;
            }
            return result;
        }
        
        // Find smallest primitive root of prime p
        function smallestPrimitiveRoot(p) {
            if (p === 2) return 1;
            
            const phi = p - 1;
            const primeFactors = [];
            let n = phi;
            
            // Get prime factors of phi
            for (let i = 2; i * i <= n; i++) {
                if (n % i === 0) {
                    primeFactors.push(i);
                    while (n % i === 0) n /= i;
                }
            }
            if (n > 1) primeFactors.push(n);
            
            // Test each candidate
            for (let g = 2; g < p; g++) {
                let isPrimRoot = true;
                for (const factor of primeFactors) {
                    if (modPow(g, phi / factor, p) === 1) {
                        isPrimRoot = false;
                        break;
                    }
                }
                if (isPrimRoot) return g;
            }
            return -1;
        }
        
        // Check if p is Sophie Germain prime (2p+1 is also prime)
        function isSophieGermain(p, primeSet) {
            return primeSet.has(2 * p + 1);
        }
        
        // Get Sophie Germain chain length
        function getSophieGermainChainLength(p, primeSet) {
            let length = 1;
            let current = p;
            
            while (primeSet.has(2 * current + 1)) {
                length++;
                current = 2 * current + 1;
            }
            
            return length;
        }
        
        // Calculate digit sum
        function digitSum(n) {
            let sum = 0;
            while (n > 0) {
                sum += n % 10;
                n = Math.floor(n / 10);
            }
            return sum;
        }
        
        // Calculate digital root (repeated digit sum until single digit)
        function digitalRoot(n) {
            while (n >= 10) {
                n = digitSum(n);
            }
            return n;
        }
        
        // Count 1s in binary representation (Hamming weight/popcount)
        function hammingWeight(n) {
            let count = 0;
            while (n > 0) {
                count += n & 1;
                n >>= 1;
            }
            return count;
        }
        
        // Check if primes form a k-tuple constellation
        function findConstellation(startPrime, pattern, primeSet) {
            for (const offset of pattern) {
                if (!primeSet.has(startPrime + offset)) {
                    return false;
                }
            }
            return true;
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
        
        // Generate Farey sequence of order n
        function fareySequence(n) {
            const farey = [];
            for (let q = 1; q <= n; q++) {
                for (let p = 0; p <= q; p++) {
                    if (gcd(p, q) === 1) {
                        farey.push({ p, q, value: p / q });
                    }
                }
            }
            return farey.sort((a, b) => a.value - b.value);
        }
        
        // Get Farey fraction for a given residue and modulus
        function getFareyFraction(residue, modulus) {
            const g = gcd(residue, modulus);
            return { p: residue / g, q: modulus / g, gcd: g };
        }
        
        // Get gap pattern based on selection
        function getGapPattern() {
            const pattern = document.getElementById('gapPattern').value;
            
            if (pattern === 'custom') {
                const input = document.getElementById('customGaps').value;
                if (!input.trim()) return [2];
                return input.split(',').map(x => parseInt(x.trim())).filter(x => x > 0);
            } else if (pattern === 'twin') {
                return [2];
            } else if (pattern === 'cousin') {
                return [4];
            } else if (pattern === 'sexy') {
                return [6];
            } else if (pattern === 'tuple-3') {
                return [2, 6]; // (p, p+2, p+6)
            } else if (pattern === 'tuple-4') {
                return [2, 6, 8]; // (p, p+2, p+6, p+8)
            } else if (pattern === 'tuple-5') {
                return [2, 6, 8, 12]; // (p, p+2, p+6, p+8, p+12)
            } else if (pattern === 'all-even') {
                return [2, 4, 6, 8, 10, 12, 14, 16, 18, 20];
            }
            
            return [2];
        }
        
        // Update gap pattern UI
        function updateGapPatternUI() {
            const pattern = document.getElementById('gapPattern').value;
            const customInput = document.getElementById('customGapInput');
            
            if (pattern === 'custom') {
                customInput.style.display = 'block';
            } else {
                customInput.style.display = 'none';
            }
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
                        '<div style="font-size: 0.85em; color: #ff6b6b; margin-top: 8px;">Note: JavaScript floating-point precision is limited to ~15-17 significant digits</div>' : '';
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
                    } else if (method === 'quadratic') {
                        showQuadraticResidueAnalysis(primes, constantType, modulus);
                    } else if (method === 'arithmetic') {
                        showArithmeticProgressionAnalysis(primes, constantType, modulus);
                    } else if (method === 'constellation') {
                        showConstellationAnalysis(primes, constantType);
                    } else if (method === 'digitsum') {
                        showDigitSumAnalysis(primes, constantType);
                    } else if (method === 'binaryweight') {
                        showBinaryWeightAnalysis(primes, constantType);
                    } else if (method === 'primitiveroot') {
                        showPrimitiveRootAnalysis(primes, constantType);
                    } else if (method === 'sophiegermain') {
                        showSophieGermainAnalysis(primes, constantType);
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
                            ${actualError <= epsilon ? 'Success: Error bound satisfied!' : 'Note: Actual error slightly exceeds theoretical bound (due to finite precision)'}
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
            } else if (type === 'methodComparison') {
                createMethodComparisonPlot(ctx);
            } else if (type === 'densityAnalysis') {
                createDensityAnalysisPlot(ctx);
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
        
        function createMethodComparisonPlot(ctx) {
            const { primes, exponent, modulus } = computationData;
            
            // Compare different decomposition methods
            const methods = [];
            
            // Gap classes
            const gapClasses = computeGapClasses(primes);
            const topGaps = Object.keys(gapClasses).map(Number).sort((a, b) => 
                gapClasses[b].length - gapClasses[a].length
            ).slice(0, 8);
            
            topGaps.forEach(gap => {
                const contribution = computeTruncatedProduct(gapClasses[gap], exponent);
                methods.push({
                    method: `Gap ${gap}`,
                    contribution: contribution,
                    count: gapClasses[gap].length
                });
            });
            
            // Residue channels
            const channels = computeResidueChannels(primes, modulus);
            const coprimeResidues = getCoprimeResidues(modulus);
            
            coprimeResidues.slice(0, 8).forEach(a => {
                const channelPrimes = channels[a];
                if (channelPrimes.length > 0) {
                    const contribution = computeTruncatedProduct(channelPrimes, exponent);
                    methods.push({
                        method: `Res ${a} (mod ${modulus})`,
                        contribution: contribution,
                        count: channelPrimes.length
                    });
                }
            });
            
            const labels = methods.map(m => m.method);
            const contributions = methods.map(m => m.contribution);
            const counts = methods.map(m => m.count);
            
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Contribution',
                        data: contributions,
                        backgroundColor: generateColors(labels.length),
                        borderColor: generateColors(labels.length).map(c => c.replace('0.8', '1')),
                        borderWidth: 2,
                        yAxisID: 'y'
                    }, {
                        label: 'Prime Count',
                        data: counts,
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
                                    if (context.datasetIndex === 0) {
                                        return `Contribution: ${context.parsed.y.toFixed(6)}`;
                                    } else {
                                        return `Primes: ${context.parsed.y}`;
                                    }
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { display: true, text: 'Decomposition Class', color: '#fff' },
                            ticks: { color: '#fff', maxRotation: 45, minRotation: 45 },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { display: true, text: 'Contribution', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { display: true, text: 'Prime Count', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function createDensityAnalysisPlot(ctx) {
            const { primes, method, modulus } = computationData;
            
            let densityData = [];
            let chartTitle = 'Prime Density Analysis';
            
            if (method === 'gap' || method === 'both') {
                // Analyze gap distribution over prime range
                const rangeSize = 100;
                const ranges = Math.ceil(primes.length / rangeSize);
                
                for (let i = 0; i < ranges; i++) {
                    const start = i * rangeSize;
                    const end = Math.min((i + 1) * rangeSize, primes.length);
                    const rangePrimes = primes.slice(start, end);
                    
                    if (rangePrimes.length < 2) continue;
                    
                    const gaps = [];
                    for (let j = 1; j < rangePrimes.length; j++) {
                        gaps.push(rangePrimes[j] - rangePrimes[j-1]);
                    }
                    
                    const avgGap = gaps.reduce((a, b) => a + b, 0) / gaps.length;
                    const avgPrime = rangePrimes.reduce((a, b) => a + b, 0) / rangePrimes.length;
                    
                    densityData.push({ x: avgPrime, y: avgGap });
                }
                
                chartTitle = 'Average Gap vs Prime Value';
                
            } else if (method === 'residue' || method === 'arithmetic') {
                // Analyze distribution across residue classes
                const channels = computeResidueChannels(primes, modulus);
                const coprimeResidues = getCoprimeResidues(modulus);
                
                coprimeResidues.forEach(a => {
                    const channelPrimes = channels[a];
                    densityData.push({
                        x: a,
                        y: channelPrimes.length,
                        label: `a=${a}`
                    });
                });
                
                chartTitle = `Prime Distribution Across Residues (mod ${modulus})`;
                
            } else if (method === 'digitsum') {
                // Digital root distribution
                const digitClasses = {};
                for (const p of primes) {
                    const root = digitalRoot(p);
                    digitClasses[root] = (digitClasses[root] || 0) + 1;
                }
                
                for (const [root, count] of Object.entries(digitClasses)) {
                    densityData.push({ x: parseInt(root), y: count });
                }
                
                chartTitle = 'Prime Count by Digital Root';
                
            } else if (method === 'binaryweight') {
                // Hamming weight distribution
                const weightClasses = {};
                for (const p of primes) {
                    const weight = hammingWeight(p);
                    weightClasses[weight] = (weightClasses[weight] || 0) + 1;
                }
                
                for (const [weight, count] of Object.entries(weightClasses)) {
                    densityData.push({ x: parseInt(weight), y: count });
                }
                
                chartTitle = 'Prime Count by Hamming Weight';
                
            } else {
                // Default: prime counting function comparison
                densityData = primes.map((p, i) => ({ x: p, y: i + 1 }));
                chartTitle = 'Prime Counting Function π(x)';
            }
            
            const isScatter = method === 'gap' || method === 'both' || !method || method === 'standard';
            
            vizChart = new Chart(ctx, {
                type: isScatter ? 'scatter' : 'bar',
                data: {
                    labels: isScatter ? undefined : densityData.map(d => d.x),
                    datasets: [{
                        label: chartTitle,
                        data: isScatter ? densityData : densityData.map(d => d.y),
                        backgroundColor: 'rgba(78, 205, 196, 0.6)',
                        borderColor: 'rgba(78, 205, 196, 1)',
                        borderWidth: 2,
                        pointRadius: isScatter ? 3 : undefined
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
                                    if (isScatter) {
                                        return `(${context.parsed.x.toFixed(2)}, ${context.parsed.y.toFixed(2)})`;
                                    } else {
                                        return `Count: ${context.parsed.y}`;
                                    }
                                }
                            }
                        },
                        title: {
                            display: true,
                            text: chartTitle,
                            color: '#fff',
                            font: { size: 16 }
                        }
                    },
                    scales: {
                        x: {
                            type: isScatter ? 'linear' : 'category',
                            title: { 
                                display: true, 
                                text: method === 'gap' ? 'Average Prime Value' : 
                                      method === 'residue' || method === 'arithmetic' ? 'Residue Class' :
                                      method === 'digitsum' ? 'Digital Root' :
                                      method === 'binaryweight' ? 'Hamming Weight' : 'Prime p',
                                color: '#fff' 
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: method === 'gap' ? 'Average Gap' : 
                                      'Count',
                                color: '#fff' 
                            },
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
                        <input type="checkbox" id="exportLegend" checked style="width: auto; margin-right: 10px;">
                        <span>Include detailed legend</span>
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
                const includeLegend = document.getElementById('exportLegend').checked;
                
                document.body.removeChild(modal);
                
                performExport(resolution, background, chartType, includeLegend);
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
            const showGCDLabels = document.getElementById('showGCDLabels').checked;
            const showModLines = document.getElementById('showModLines').checked;
            const showLiftConnections = document.getElementById('showLiftConnections').checked;
            const liftThickness = parseFloat(document.getElementById('liftThickness').value);
            const liftColor = document.getElementById('liftColor').value;
            const showGapConnections = document.getElementById('showGapConnections').checked;
            const gapThickness = parseFloat(document.getElementById('gapThickness').value);
            const gapColor = document.getElementById('gapColor').value;
            const gapPattern = getGapPattern();
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
                } else if (colorMode === 'size') {
                    const maxPrime = Math.max(...primes);
                    const ratio = prime / maxPrime;
                    hue = ratio * 120; // green to red
                } else if (colorMode === 'gcd') {
                    // Color by GCD using Farey sequence
                    const g = gcd(residue, modulus);
                    const maxGCD = Math.max(10, g);
                    hue = (g / maxGCD) * 280;
                    saturation = 70 + (g > 1 ? 20 : 0);
                    lightness = 60 - (g * 3);
                }
                
                if (invertColors) {
                    saturation = Math.min(saturation + 10, 100);
                    lightness = 40; // darker colors on white background
                }
                
                return `hsla(${hue}, ${saturation}%, ${lightness}%, 0.8)`;
            };
            
            // Store points for hover detection and lift connections
            const points = [];
            const residueMap = {}; // Map residue -> array of {prime, x, y, modulus, modulusIndex}
            const primePositions = {}; // Map prime -> {x, y, residue, modulus}
            
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
                    
                    // Store for lift connections
                    if (!residueMap[residue]) residueMap[residue] = [];
                    residueMap[residue].push({ prime: p, x, y, modulus: m, modulusIndex: i });
                    
                    // Store for gap connections (use largest modulus ring for clearest view)
                    if (i === moduli.length - 1) {
                        primePositions[p] = { x, y, residue, modulus: m };
                    }
                    
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
            
            // Draw r→r lift connections (only to next modulus level)
            if (showLiftConnections) {
                ctx.strokeStyle = liftColor;
                ctx.lineWidth = liftThickness;
                ctx.globalAlpha = 0.4;
                
                for (const residue in residueMap) {
                    const pointsWithResidue = residueMap[residue];
                    // Sort by modulus index to ensure we connect consecutive rings
                    pointsWithResidue.sort((a, b) => a.modulusIndex - b.modulusIndex);
                    
                    // Connect each point to the next modulus level only
                    for (let i = 0; i < pointsWithResidue.length - 1; i++) {
                        const p1 = pointsWithResidue[i];
                        const p2 = pointsWithResidue[i + 1];
                        
                        // Only connect if they are on consecutive modulus rings
                        if (p2.modulusIndex === p1.modulusIndex + 1) {
                            ctx.beginPath();
                            ctx.moveTo(p1.x, p1.y);
                            ctx.lineTo(p2.x, p2.y);
                            ctx.stroke();
                        }
                    }
                }
                
                ctx.globalAlpha = 1.0;
            }
            
            // Draw gap connections (r to r+2n when both are prime)
            if (showGapConnections) {
                ctx.lineWidth = gapThickness;
                ctx.globalAlpha = 0.5;
                
                // Create map of gaps found for statistics
                const gapsFound = {};
                gapPattern.forEach(g => gapsFound[g] = 0);
                
                // For each prime p, check if p + gap is also prime
                // Then connect their positions on the largest modulus ring
                const largestMod = moduli[moduli.length - 1];
                
                for (const p of primes) {
                    for (const gap of gapPattern) {
                        const targetPrime = p + gap;
                        
                        // Check if target is also a prime
                        if (primes.includes(targetPrime)) {
                            // Get residues for both primes mod largest modulus
                            const r1 = p % largestMod;
                            const r2 = targetPrime % largestMod;
                            
                            // Only draw if both residues are coprime to modulus
                            if (gcd(r1, largestMod) === 1 && gcd(r2, largestMod) === 1) {
                                // Calculate positions on largest ring
                                const ringIndex = invertRings ? 0 : (moduli.length - 1);
                                const radius = (ringIndex + 1) * radiusStep;
                                
                                let angle1 = (2 * Math.PI * r1) / largestMod;
                                let angle2 = (2 * Math.PI * r2) / largestMod;
                                
                                // Apply rotation
                                if (rotationMode === 'global') {
                                    angle1 += globalRotationAngle;
                                    angle2 += globalRotationAngle;
                                } else if (rotationMode === 'local') {
                                    const rotationOffset = globalRotationAngle * largestMod / maxModulusValue;
                                    angle1 += rotationOffset;
                                    angle2 += rotationOffset;
                                }
                                
                                const x1 = centerX + radius * Math.cos(angle1);
                                const y1 = centerY + radius * Math.sin(angle1);
                                const x2 = centerX + radius * Math.cos(angle2);
                                const y2 = centerY + radius * Math.sin(angle2);
                                
                                // Use different colors for different gaps
                                const gapIndex = gapPattern.indexOf(gap);
                                const hue = (gapIndex / gapPattern.length) * 360;
                                ctx.strokeStyle = `hsla(${hue}, 80%, 60%, 0.6)`;
                                
                                ctx.beginPath();
                                ctx.moveTo(x1, y1);
                                ctx.lineTo(x2, y2);
                                ctx.stroke();
                                
                                gapsFound[gap]++;
                            }
                        }
                    }
                }
                
                ctx.globalAlpha = 1.0;
                
                // Display gap statistics
                if (Object.keys(gapsFound).length > 0) {
                    ctx.save();
                    ctx.font = `${Math.max(10, height * 0.015)}px Arial`;
                    ctx.textAlign = 'left';
                    
                    const statsX = padding;
                    const statsY = padding + height * 0.05;
                    
                    // Background
                    ctx.fillStyle = invertColors ? 'rgba(255, 255, 255, 0.9)' : 'rgba(0, 0, 0, 0.8)';
                    ctx.fillRect(statsX, statsY, width * 0.15, Object.keys(gapsFound).length * height * 0.025 + padding);
                    
                    // Text
                    ctx.fillStyle = invertColors ? '#000' : '#fff';
                    let yOffset = statsY + height * 0.02;
                    
                    for (const gap in gapsFound) {
                        const count = gapsFound[gap];
                        const gapIndex = gapPattern.indexOf(parseInt(gap));
                        const hue = (gapIndex / gapPattern.length) * 360;
                        
                        // Color indicator
                        ctx.fillStyle = `hsla(${hue}, 80%, 60%, 0.8)`;
                        ctx.fillRect(statsX + padding / 2, yOffset - height * 0.012, height * 0.015, height * 0.015);
                        
                        // Text
                        ctx.fillStyle = invertColors ? '#000' : '#fff';
                        ctx.fillText(`Gap ${gap}: ${count} pairs`, statsX + padding / 2 + height * 0.02, yOffset);
                        yOffset += height * 0.025;
                    }
                    
                    ctx.restore();
                }
            }
            
            // Draw GCD/Farey labels
            if (showGCDLabels) {
                ctx.font = `${Math.max(8, pointSize)}px Arial`;
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                
                const labeledResidues = new Set();
                
                for (let i = moduli.length - 1; i >= 0; i--) {
                    const m = moduli[i];
                    const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                    const radius = (ringIndex + 1) * radiusStep;
                    
                    // Only show labels for outer rings to avoid clutter
                    if (i < moduli.length - 3) continue;
                    
                    for (let r = 0; r < m; r++) {
                        if (gcd(r, m) !== 1) continue;
                        
                        const farey = getFareyFraction(r, m);
                        const labelKey = `${farey.p}/${farey.q}`;
                        
                        // Avoid duplicate labels
                        if (labeledResidues.has(labelKey)) continue;
                        labeledResidues.add(labelKey);
                        
                        let angle = (2 * Math.PI * r) / m;
                        if (rotationMode === 'global') {
                            angle += globalRotationAngle;
                        } else if (rotationMode === 'local') {
                            angle += globalRotationAngle * m / maxModulusValue;
                        }
                        
                        const labelRadius = radius + radiusStep * 0.3;
                        const x = centerX + labelRadius * Math.cos(angle);
                        const y = centerY + labelRadius * Math.sin(angle);
                        
                        // Draw background for label
                        const labelText = farey.gcd > 1 ? `${farey.p}/${farey.q} (gcd=${farey.gcd})` : `${farey.p}/${farey.q}`;
                        const metrics = ctx.measureText(labelText);
                        const padding = 3;
                        
                        ctx.fillStyle = invertColors ? 'rgba(255, 255, 255, 0.9)' : 'rgba(0, 0, 0, 0.8)';
                        ctx.fillRect(
                            x - metrics.width / 2 - padding,
                            y - pointSize - padding,
                            metrics.width + padding * 2,
                            pointSize * 2 + padding * 2
                        );
                        
                        // Draw label text
                        ctx.fillStyle = invertColors ? '#000' : (farey.gcd > 1 ? '#ffd700' : '#4ecdc4');
                        ctx.fillText(labelText, x, y);
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
                    
                    // Get Farey representation
                    const farey = getFareyFraction(closestPoint.residue, closestPoint.modulus);
                    
                    // Check for gap connections
                    const gapConnections = [];
                    for (const gap of gapPattern) {
                        if (primes.includes(closestPoint.p + gap)) {
                            gapConnections.push(`+${gap}`);
                        }
                        if (primes.includes(closestPoint.p - gap)) {
                            gapConnections.push(`-${gap}`);
                        }
                    }
                    
                    // Create detailed tooltip
                    const lines = [
                        `Prime: p = ${closestPoint.p}`,
                        `Residue: r = ${closestPoint.residue} (mod ${closestPoint.modulus})`,
                        `Farey: ${farey.p}/${farey.q}${farey.gcd > 1 ? ` (gcd=${farey.gcd})` : ''}`,
                        `Fraction: r/m = ${closestPoint.residue}/${closestPoint.modulus} = ${(closestPoint.residue / closestPoint.modulus).toFixed(4)}`,
                        `Angle: θ = ${angleRadStr}π rad = ${angleDeg}°`,
                        `Position: (${Math.cos(angleRad).toFixed(3)}, ${Math.sin(angleRad).toFixed(3)})`
                    ];
                    
                    if (gapConnections.length > 0) {
                        lines.push(`Gap connections: ${gapConnections.join(', ')}`);
                    }
                    
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
            
            if (showGapConnections) {
                const pattern = getGapPattern();
                html += `<div class="ring-legend-item"><strong>Gap pattern:</strong> ${pattern.join(', ')}</div>`;
                
                // Show color coding for gaps
                pattern.forEach((gap, idx) => {
                    const hue = (idx / pattern.length) * 360;
                    const color = `hsla(${hue}, 80%, 60%, 0.6)`;
                    html += `<div class="ring-legend-item"><div class="ring-legend-color" style="background: ${color};"></div><span>Gap ${gap}</span></div>`;
                });
            }
            
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
            } else if (colorMode === 'size') {
                html += '<div class="ring-legend-item"><strong>Color by Prime Size:</strong> Green (small) → Yellow → Red (large)</div>';
            } else if (colorMode === 'gcd') {
                html += '<div class="ring-legend-item"><strong>Color by GCD (Farey):</strong> Colors represent gcd(r,m) values in reduced fractions p/q</div>';
                html += '<div class="ring-legend-item"><div class="ring-legend-color" style="background: hsla(0, 70%, 60%, 0.8);"></div><span>gcd=1 (coprime)</span></div>';
                html += '<div class="ring-legend-item"><div class="ring-legend-color" style="background: hsla(140, 90%, 40%, 0.8);"></div><span>gcd>1 (composite)</span></div>';
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
            updateGapPatternUI();
        };
    </script>
</body>
</html>
