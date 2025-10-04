<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Sieve Analysis - Goldbach's Conjecture</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Times New Roman', serif;
            background: #f5f5f5;
            color: #222;
            padding: 20px;
        }
        
        .container {
            max-width: 1800px;
            margin: 0 auto;
            background: white;
            border: 1px solid #ddd;
        }
        
        header {
            background: #2c3e50;
            color: white;
            padding: 30px 40px;
            border-bottom: 3px solid #34495e;
        }
        
        h1 {
            font-size: 1.8em;
            font-weight: normal;
            margin-bottom: 8px;
            letter-spacing: 0.5px;
        }
        
        .subtitle {
            font-size: 0.95em;
            opacity: 0.9;
            font-style: italic;
        }
        
        .paper-ref {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid #445566;
            font-size: 0.85em;
            line-height: 1.6;
        }
        
        .content {
            display: grid;
            grid-template-columns: 380px 1fr;
            gap: 0;
        }
        
        .controls {
            background: #fafafa;
            padding: 25px;
            border-right: 1px solid #ddd;
            font-size: 0.9em;
        }
        
        .section-title {
            font-weight: bold;
            font-size: 1em;
            margin: 20px 0 10px 0;
            padding-bottom: 5px;
            border-bottom: 2px solid #2c3e50;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .control-group {
            margin-bottom: 16px;
        }
        
        .control-group label {
            display: block;
            font-weight: normal;
            margin-bottom: 5px;
            color: #333;
            font-size: 0.9em;
        }
        
        input[type="number"], select {
            width: 100%;
            padding: 8px;
            border: 1px solid #999;
            background: white;
            font-size: 0.9em;
            font-family: 'Courier New', monospace;
        }
        
        input[type="number"]:focus, select:focus {
            outline: none;
            border-color: #2c3e50;
        }
        
        input[type="checkbox"] {
            width: 16px;
            height: 16px;
            margin-right: 8px;
        }
        
        .checkbox-label {
            display: flex;
            align-items: center;
            margin: 8px 0;
            cursor: pointer;
            font-size: 0.9em;
        }
        
        button {
            width: 100%;
            padding: 10px;
            background: #2c3e50;
            color: white;
            border: none;
            font-size: 0.9em;
            font-weight: normal;
            cursor: pointer;
            margin-top: 8px;
            font-family: 'Times New Roman', serif;
            letter-spacing: 0.5px;
        }
        
        button:hover {
            background: #34495e;
        }
        
        button:active {
            background: #1a252f;
        }
        
        .zoom-controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            margin-top: 12px;
        }
        
        .export-btn {
            background: #27ae60;
            margin-top: 15px;
        }
        
        .export-btn:hover {
            background: #229954;
        }
        
        .visualization {
            padding: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        canvas {
            border: 1px solid #999;
            background: white;
            margin-bottom: 20px;
        }
        
        .info-panel {
            background: #fafafa;
            padding: 20px;
            border: 1px solid #ddd;
            margin-top: 20px;
            width: 100%;
            max-width: 1200px;
            font-size: 0.9em;
        }
        
        .info-panel h3 {
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.1em;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .stat-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
        }
        
        .stat {
            padding: 10px;
            background: white;
            border: 1px solid #ddd;
        }
        
        .stat-label {
            font-weight: normal;
            color: #666;
            font-size: 0.85em;
            margin-bottom: 4px;
        }
        
        .stat-value {
            font-family: 'Courier New', monospace;
            font-size: 1.1em;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .theorem-box {
            background: #fff9e6;
            border: 1px solid #d4c190;
            padding: 15px;
            margin-top: 20px;
            font-size: 0.88em;
            line-height: 1.7;
        }
        
        .theorem-box h4 {
            font-weight: bold;
            margin-bottom: 8px;
            font-size: 1em;
        }
        
        .theorem-box em {
            font-style: italic;
        }
        
        @media (max-width: 1400px) {
            .content {
                grid-template-columns: 1fr;
            }
            
            .controls {
                border-right: none;
                border-bottom: 1px solid #ddd;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Mathematical Analysis: Modular Sieve Approaches to Goldbach's Conjecture</h1>
            <p class="subtitle">Visualization of fundamental limitations in modular arithmetic methods</p>
            <div class="paper-ref">
                <strong>Key Finding:</strong> Modular residue classes partition ALL integers. The assertion that "mod 30 captures even numbers ≥ 18" constitutes a categorical error in understanding residue class properties.<br>
                <strong>Parity Problem (Selberg, 1949):</strong> Sieve methods cannot distinguish primes from semiprimes, yielding bounds off by factor ≥ 2.<br>
                <strong>Theoretical Limit:</strong> Chen's Theorem (1973) represents maximum achievement of pure sieve methods: every sufficiently large even number = prime + (prime OR semiprime).
            </div>
        </header>
        
        <div class="content">
            <div class="controls">
                <div class="section-title">Parameters</div>
                
                <div class="control-group">
                    <label for="modulus">Modulus m:</label>
                    <input type="number" id="modulus" value="30" min="2" max="1000">
                </div>
                
                <div class="control-group">
                    <label for="rings">Concentric Rings:</label>
                    <input type="number" id="rings" value="8" min="1" max="30">
                </div>
                
                <div class="control-group">
                    <label for="baseRange">Base Range [1, n]:</label>
                    <input type="number" id="baseRange" value="500" min="10" max="100000">
                </div>
                
                <div class="control-group">
                    <label for="zoomLevel">Zoom Level (10^x):</label>
                    <select id="zoomLevel">
                        <option value="0.1">10^-1 (×0.1)</option>
                        <option value="1" selected>10^0 (×1)</option>
                        <option value="10">10^1 (×10)</option>
                        <option value="100">10^2 (×100)</option>
                        <option value="1000">10^3 (×1000)</option>
                        <option value="10000">10^4 (×10000)</option>
                    </select>
                </div>
                
                <div class="zoom-controls">
                    <button onclick="zoomIn()">Zoom In (×10)</button>
                    <button onclick="zoomOut()">Zoom Out (÷10)</button>
                </div>
                
                <div class="section-title">Visualization Options</div>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showPrimes" checked>
                    <span>Mark Prime Numbers</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showSemiprimes" checked>
                    <span>Mark Semiprimes</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showGCD" checked>
                    <span>Color by GCD(n, m)</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showCoprimeOnly">
                    <span>Show Only GCD(n, m) = 1</span>
                </label>
                
                <div class="section-title">Canvas Settings</div>
                
                <div class="control-group">
                    <label for="resolution">Resolution:</label>
                    <select id="resolution">
                        <option value="1200">1200×1200</option>
                        <option value="2400">2400×2400</option>
                        <option value="3840" selected>3840×3840 (4K)</option>
                        <option value="7680">7680×7680 (8K)</option>
                    </select>
                </div>
                
                <button onclick="drawVisualization()">RENDER</button>
                <button class="export-btn" onclick="saveCanvas()">EXPORT PNG</button>
            </div>
            
            <div class="visualization">
                <canvas id="mainCanvas"></canvas>
                
                <div class="info-panel">
                    <h3>Computational Results</h3>
                    <div class="stat-grid">
                        <div class="stat">
                            <div class="stat-label">Modulus</div>
                            <div class="stat-value" id="statMod">30</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Euler φ(m)</div>
                            <div class="stat-value" id="statPhi">8</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Effective Range</div>
                            <div class="stat-value" id="statRange">[1, 500]</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Integers Plotted</div>
                            <div class="stat-value" id="statCount">0</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Primes</div>
                            <div class="stat-value" id="statPrimes">0</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Semiprimes</div>
                            <div class="stat-value" id="statSemiprimes">0</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">GCD = 1 Count</div>
                            <div class="stat-value" id="statCoprime">0</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Resolution</div>
                            <div class="stat-value" id="statRes">3840×3840</div>
                        </div>
                        <div class="stat">
                            <div class="stat-label">Zoom Factor</div>
                            <div class="stat-value" id="statZoom">1×</div>
                        </div>
                    </div>
                </div>
                
                <div class="theorem-box">
                    <h4>Fundamental Limitations of Modular Sieve Methods</h4>
                    <p><strong>1. Categorical Error:</strong> Every integer n belongs to exactly one residue class modulo m. The claim that specific moduli "capture" certain subsets (e.g., "mod 30 captures even numbers ≥ 18") demonstrates fundamental misunderstanding of modular arithmetic.</p>
                    
                    <p><strong>2. Parity Problem (Selberg, 1949):</strong> Sieve theory cannot distinguish between numbers with odd vs. even prime factor counts. For set A containing only products of odd number of primes, sieves cannot provide non-trivial lower bounds on |A|. Upper bounds are off by factor ≥ 2.</p>
                    
                    <p><strong>3. Chen's Theorem (1973):</strong> Every sufficiently large even integer n can be expressed as n = p + P₂, where p is prime and P₂ is either prime or semiprime. This represents the theoretical maximum of pure sieve methods—the 1+2 result cannot be improved to 1+1 (Goldbach's Conjecture) using sieve techniques alone.</p>
                    
                    <p><strong>4. Verification Status:</strong> Computational verification extends to n ≤ 4×10¹⁸ (Oliveira e Silva, 2013), but computational evidence does not constitute proof. The conjecture requires demonstration for ALL even integers, not merely "almost all" or "sufficiently large" integers.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('mainCanvas');
        const ctx = canvas.getContext('2d');
        
        function gcd(a, b) {
            while (b !== 0) {
                let t = b;
                b = a % b;
                a = t;
            }
            return a;
        }
        
        function eulerPhi(n) {
            let result = 0;
            for (let i = 1; i < n; i++) {
                if (gcd(i, n) === 1) result++;
            }
            return result;
        }
        
        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2) return true;
            if (n % 2 === 0) return false;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return false;
            }
            return true;
        }
        
        function primeFactorCount(n) {
            let count = 0;
            let num = n;
            
            for (let i = 2; i * i <= num; i++) {
                while (num % i === 0) {
                    count++;
                    num /= i;
                }
            }
            if (num > 1) count++;
            return count;
        }
        
        function isSemiprime(n) {
            return primeFactorCount(n) === 2;
        }
        
        function getGCDColor(gcdVal, maxGCD) {
            if (gcdVal === 1) return '#2c3e50';
            const intensity = 200 - (gcdVal / maxGCD) * 150;
            return `rgb(${intensity}, ${intensity}, ${intensity})`;
        }
        
        function zoomIn() {
            const select = document.getElementById('zoomLevel');
            const options = Array.from(select.options);
            const currentIndex = select.selectedIndex;
            if (currentIndex < options.length - 1) {
                select.selectedIndex = currentIndex + 1;
                drawVisualization();
            }
        }
        
        function zoomOut() {
            const select = document.getElementById('zoomLevel');
            const currentIndex = select.selectedIndex;
            if (currentIndex > 0) {
                select.selectedIndex = currentIndex - 1;
                drawVisualization();
            }
        }
        
        function drawVisualization() {
            const m = parseInt(document.getElementById('modulus').value);
            const numRings = parseInt(document.getElementById('rings').value);
            const baseRange = parseInt(document.getElementById('baseRange').value);
            const zoomFactor = parseFloat(document.getElementById('zoomLevel').value);
            const resolution = parseInt(document.getElementById('resolution').value);
            const showPrimes = document.getElementById('showPrimes').checked;
            const showSemiprimes = document.getElementById('showSemiprimes').checked;
            const showGCD = document.getElementById('showGCD').checked;
            const showCoprimeOnly = document.getElementById('showCoprimeOnly').checked;
            
            const maxNum = Math.floor(baseRange * zoomFactor);
            
            canvas.width = resolution;
            canvas.height = resolution;
            const scale = resolution / 1200;
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const maxRadius = canvas.width * 0.42;
            const minRadius = maxRadius * 0.12;
            
            // Background
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw concentric circles
            ctx.strokeStyle = '#cccccc';
            ctx.lineWidth = 0.5 * scale;
            for (let ring = 0; ring <= numRings; ring++) {
                const r = minRadius + (maxRadius - minRadius) * (ring / numRings);
                ctx.beginPath();
                ctx.arc(centerX, centerY, r, 0, 2 * Math.PI);
                ctx.stroke();
            }
            
            // Draw radial lines
            ctx.strokeStyle = '#e8e8e8';
            ctx.lineWidth = 0.3 * scale;
            for (let i = 0; i < m; i++) {
                const angle = (2 * Math.PI * i) / m - Math.PI / 2;
                const isCoprime = gcd(i, m) === 1;
                if (isCoprime) {
                    ctx.strokeStyle = '#d0d0d0';
                    ctx.lineWidth = 0.8 * scale;
                } else {
                    ctx.strokeStyle = '#e8e8e8';
                    ctx.lineWidth = 0.3 * scale;
                }
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(
                    centerX + maxRadius * Math.cos(angle),
                    centerY + maxRadius * Math.sin(angle)
                );
                ctx.stroke();
            }
            
            // Statistics
            let primeCount = 0;
            let semiprimeCount = 0;
            let coprimeCount = 0;
            let plottedCount = 0;
            const maxGCD = m;
            
            // Plot numbers
            for (let n = 1; n <= maxNum; n++) {
                const gcdVal = gcd(n, m);
                
                if (showCoprimeOnly && gcdVal !== 1) continue;
                
                const angle = (2 * Math.PI * n) / m - Math.PI / 2;
                const ring = Math.floor((n - 1) / (maxNum / numRings));
                const radius = minRadius + (maxRadius - minRadius) * (ring / numRings);
                
                const x = centerX + radius * Math.cos(angle);
                const y = centerY + radius * Math.sin(angle);
                
                const prime = isPrime(n);
                const semiprime = isSemiprime(n);
                
                if (prime) primeCount++;
                if (semiprime) semiprimeCount++;
                if (gcdVal === 1) coprimeCount++;
                plottedCount++;
                
                // Determine color
                let color;
                if (showPrimes && prime) {
                    color = '#27ae60';
                } else if (showSemiprimes && semiprime) {
                    color = '#e67e22';
                } else if (showGCD) {
                    color = getGCDColor(gcdVal, maxGCD);
                } else {
                    color = '#34495e';
                }
                
                // Draw point
                const pointSize = (gcdVal === 1 ? 2.5 : 2) * scale;
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, pointSize, 0, 2 * Math.PI);
                ctx.fill();
                
                if (gcdVal === 1 && showGCD) {
                    ctx.strokeStyle = '#000';
                    ctx.lineWidth = 0.4 * scale;
                    ctx.stroke();
                }
            }
            
            // Center label
            ctx.fillStyle = '#2c3e50';
            ctx.font = `${14 * scale}px Times New Roman`;
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(`mod ${m}`, centerX, centerY);
            
            // Update statistics
            document.getElementById('statMod').textContent = m;
            document.getElementById('statPhi').textContent = eulerPhi(m);
            document.getElementById('statRange').textContent = `[1, ${maxNum}]`;
            document.getElementById('statCount').textContent = plottedCount;
            document.getElementById('statPrimes').textContent = primeCount;
            document.getElementById('statSemiprimes').textContent = semiprimeCount;
            document.getElementById('statCoprime').textContent = coprimeCount;
            document.getElementById('statRes').textContent = `${resolution}×${resolution}`;
            document.getElementById('statZoom').textContent = `${zoomFactor}×`;
        }
        
        function saveCanvas() {
            const link = document.createElement('a');
            const m = document.getElementById('modulus').value;
            const zoom = document.getElementById('zoomLevel').value;
            const res = document.getElementById('resolution').value;
            link.download = `modular_sieve_analysis_m${m}_zoom${zoom}_${res}x${res}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
        }
        
        // Initial render
        drawVisualization();
    </script>
</body>
</html>
