<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Arithmetic Visualizer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #333;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1800px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        h1 {
            font-size: 2em;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1em;
            opacity: 0.95;
        }
        
        .content {
            display: grid;
            grid-template-columns: 320px 1fr;
            gap: 0;
        }
        
        .controls {
            background: #f8f9fa;
            padding: 25px;
            border-right: 2px solid #e0e0e0;
            max-height: calc(100vh - 180px);
            overflow-y: auto;
        }
        
        .control-group {
            margin-bottom: 20px;
        }
        
        .control-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: #444;
            font-size: 0.9em;
        }
        
        input[type="number"], select {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 0.95em;
            transition: border-color 0.3s;
        }
        
        input[type="number"]:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }
        
        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            margin-right: 8px;
        }
        
        .checkbox-label {
            display: flex;
            align-items: center;
            margin-top: 10px;
            cursor: pointer;
        }
        
        button {
            width: 100%;
            padding: 12px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 0.95em;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            margin-top: 10px;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        button.secondary {
            background: linear-gradient(135deg, #43a047 0%, #66bb6a 100%);
        }
        
        button.secondary:hover {
            box-shadow: 0 4px 12px rgba(67, 160, 71, 0.4);
        }
        
        .visualization {
            padding: 25px;
            max-height: calc(100vh - 180px);
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        canvas {
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            background: white;
            margin-bottom: 20px;
        }
        
        .info-panel {
            background: #f8f9fa;
            padding: 18px;
            border-radius: 8px;
            margin-top: 20px;
            border-left: 4px solid #667eea;
            width: 100%;
            max-width: 1200px;
        }
        
        .info-panel h3 {
            color: #667eea;
            margin-bottom: 12px;
        }
        
        .stat {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .stat:last-child {
            border-bottom: none;
        }
        
        .stat-label {
            font-weight: 600;
            color: #555;
        }
        
        .stat-value {
            color: #667eea;
            font-weight: 700;
        }
        
        .warning {
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 12px;
            margin-top: 15px;
            border-radius: 6px;
        }
        
        .warning h4 {
            color: #856404;
            margin-bottom: 6px;
            font-size: 0.95em;
        }
        
        .warning p {
            color: #856404;
            font-size: 0.85em;
            line-height: 1.4;
        }
        
        @media (max-width: 1200px) {
            .content {
                grid-template-columns: 1fr;
            }
            
            .controls {
                border-right: none;
                border-bottom: 2px solid #e0e0e0;
                max-height: none;
            }
            
            .visualization {
                max-height: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Modular Arithmetic Unit Circle Visualizer</h1>
            <p class="subtitle">Explore GCD patterns and prime distribution on concentric rings</p>
        </header>
        
        <div class="content">
            <div class="controls">
                <div class="control-group">
                    <label for="modulus">Modulus (m):</label>
                    <input type="number" id="modulus" value="30" min="2" max="500">
                </div>
                
                <div class="control-group">
                    <label for="rings">Number of Rings:</label>
                    <input type="number" id="rings" value="5" min="1" max="20">
                </div>
                
                <div class="control-group">
                    <label for="maxNum">Maximum Number to Plot:</label>
                    <input type="number" id="maxNum" value="150" min="10" max="5000">
                </div>
                
                <div class="control-group">
                    <label for="resolution">Canvas Resolution:</label>
                    <select id="resolution">
                        <option value="1200">Standard (1200x1200)</option>
                        <option value="2400">HD (2400x2400)</option>
                        <option value="3840" selected>4K (3840x3840)</option>
                        <option value="7680">8K (7680x7680)</option>
                    </select>
                </div>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showPrimes" checked>
                    <span>Highlight Primes</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showSemiprimes" checked>
                    <span>Highlight Semiprimes</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showGCD" checked>
                    <span>Color by GCD</span>
                </label>
                
                <label class="checkbox-label">
                    <input type="checkbox" id="showLabels">
                    <span>Show Number Labels</span>
                </label>
                
                <button onclick="drawVisualization()">Update Visualization</button>
                <button class="secondary" onclick="saveCanvas()">Save as 4K Image</button>
                
                <div class="warning">
                    <h4>💡 About This Visualization</h4>
                    <p>Points are plotted at angle 2πn/m on concentric rings. Colors show GCD(n, m) patterns. Primes appear green, semiprimes orange.</p>
                </div>
            </div>
            
            <div class="visualization">
                <canvas id="mainCanvas"></canvas>
                
                <div class="info-panel">
                    <h3>Visualization Statistics</h3>
                    <div class="stat">
                        <span class="stat-label">Modulus (m):</span>
                        <span class="stat-value" id="statMod">30</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Euler's φ(m):</span>
                        <span class="stat-value" id="statPhi">8</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Numbers Plotted:</span>
                        <span class="stat-value" id="statCount">0</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Primes Found:</span>
                        <span class="stat-value" id="statPrimes">0</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Semiprimes Found:</span>
                        <span class="stat-value" id="statSemiprimes">0</span>
                    </div>
                    <div class="stat">
                        <span class="stat-label">Canvas Resolution:</span>
                        <span class="stat-value" id="statRes">3840x3840</span>
                    </div>
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
            const hue = (gcdVal / maxGCD) * 280;
            return `hsl(${hue}, 70%, 50%)`;
        }
        
        function drawVisualization() {
            const m = parseInt(document.getElementById('modulus').value);
            const numRings = parseInt(document.getElementById('rings').value);
            const maxNum = parseInt(document.getElementById('maxNum').value);
            const resolution = parseInt(document.getElementById('resolution').value);
            const showPrimes = document.getElementById('showPrimes').checked;
            const showSemiprimes = document.getElementById('showSemiprimes').checked;
            const showGCD = document.getElementById('showGCD').checked;
            const showLabels = document.getElementById('showLabels').checked;
            
            // Set canvas size
            canvas.width = resolution;
            canvas.height = resolution;
            const scale = resolution / 1200; // Scale factor
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const maxRadius = (canvas.width * 0.45);
            const minRadius = maxRadius * 0.15;
            
            // Draw background
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw concentric circles
            ctx.strokeStyle = '#e0e0e0';
            ctx.lineWidth = 1 * scale;
            for (let ring = 0; ring <= numRings; ring++) {
                const r = minRadius + (maxRadius - minRadius) * (ring / numRings);
                ctx.beginPath();
                ctx.arc(centerX, centerY, r, 0, 2 * Math.PI);
                ctx.stroke();
            }
            
            // Draw radial lines for each residue class
            ctx.strokeStyle = '#f0f0f0';
            ctx.lineWidth = 0.5 * scale;
            for (let i = 0; i < m; i++) {
                const angle = (2 * Math.PI * i) / m - Math.PI / 2;
                const isCoprime = gcd(i, m) === 1;
                if (isCoprime) {
                    ctx.strokeStyle = '#e8d5f2';
                    ctx.lineWidth = 1 * scale;
                } else {
                    ctx.strokeStyle = '#f0f0f0';
                    ctx.lineWidth = 0.5 * scale;
                }
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(
                    centerX + maxRadius * Math.cos(angle),
                    centerY + maxRadius * Math.sin(angle)
                );
                ctx.stroke();
            }
            
            // Count statistics
            let primeCount = 0;
            let semiprimeCount = 0;
            const maxGCD = m;
            
            // Plot numbers
            for (let n = 1; n <= maxNum; n++) {
                const angle = (2 * Math.PI * n) / m - Math.PI / 2;
                const ring = Math.floor((n - 1) / (maxNum / numRings));
                const radius = minRadius + (maxRadius - minRadius) * (ring / numRings);
                
                const x = centerX + radius * Math.cos(angle);
                const y = centerY + radius * Math.sin(angle);
                
                const gcdVal = gcd(n, m);
                const prime = isPrime(n);
                const semiprime = isSemiprime(n);
                
                if (prime) primeCount++;
                if (semiprime) semiprimeCount++;
                
                // Determine color
                let color;
                if (showPrimes && prime) {
                    color = '#4CAF50';
                } else if (showSemiprimes && semiprime) {
                    color = '#FF9800';
                } else if (showGCD) {
                    color = getGCDColor(gcdVal, maxGCD);
                } else {
                    color = '#2196F3';
                }
                
                // Draw point
                const pointSize = (gcdVal === 1 ? 4 : 3) * scale;
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, pointSize, 0, 2 * Math.PI);
                ctx.fill();
                
                // Add border for coprime numbers
                if (gcdVal === 1) {
                    ctx.strokeStyle = '#333';
                    ctx.lineWidth = 0.5 * scale;
                    ctx.stroke();
                }
                
                // Label numbers
                if (showLabels && (n <= 60 || n % 10 === 0)) {
                    ctx.fillStyle = '#333';
                    ctx.font = `${8 * scale}px Arial`;
                    ctx.textAlign = 'center';
                    ctx.fillText(n.toString(), x, y - 8 * scale);
                }
            }
            
            // Draw center label
            ctx.fillStyle = '#667eea';
            ctx.font = `bold ${16 * scale}px Arial`;
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(`mod ${m}`, centerX, centerY);
            
            // Update statistics
            document.getElementById('statMod').textContent = m;
            document.getElementById('statPhi').textContent = eulerPhi(m);
            document.getElementById('statCount').textContent = maxNum;
            document.getElementById('statPrimes').textContent = primeCount;
            document.getElementById('statSemiprimes').textContent = semiprimeCount;
            document.getElementById('statRes').textContent = `${resolution}x${resolution}`;
        }
        
        function saveCanvas() {
            const link = document.createElement('a');
            const m = document.getElementById('modulus').value;
            const res = document.getElementById('resolution').value;
            link.download = `modular_visualization_mod${m}_${res}x${res}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
        }
        
        // Initial draw
        drawVisualization();
    </script>
</body>
</html>
