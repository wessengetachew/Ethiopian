<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Professional Modular Arithmetic Ring Analyzer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #1a1a1a;
            color: #e0e0e0;
            overflow-x: hidden;
        }

        .container {
            display: grid;
            grid-template-columns: 350px 1fr 350px;
            height: 100vh;
            gap: 0;
        }

        .panel {
            background: #2a2a2a;
            border-right: 1px solid #444;
            overflow-y: auto;
            padding: 20px;
        }

        .panel h2 {
            font-size: 1.1em;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #555;
            color: #4fc3f7;
        }

        .control-group {
            margin-bottom: 18px;
        }

        .control-group label {
            display: block;
            margin-bottom: 6px;
            font-size: 0.85em;
            font-weight: 500;
            color: #b0b0b0;
        }

        .control-group input[type="text"],
        .control-group input[type="number"],
        .control-group select {
            width: 100%;
            padding: 8px;
            background: #1a1a1a;
            border: 1px solid #555;
            border-radius: 4px;
            color: #e0e0e0;
            font-family: 'Consolas', monospace;
            font-size: 0.9em;
        }

        .control-group input[type="text"]:focus,
        .control-group input[type="number"]:focus,
        .control-group select:focus {
            outline: none;
            border-color: #4fc3f7;
        }

        .control-group input[type="checkbox"] {
            width: 16px;
            height: 16px;
            margin-right: 8px;
            cursor: pointer;
        }

        .checkbox-label {
            display: flex;
            align-items: center;
            cursor: pointer;
            font-size: 0.9em;
        }

        .btn {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 4px;
            font-weight: 600;
            font-size: 0.9em;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary {
            background: #1976d2;
            color: white;
        }

        .btn-primary:hover {
            background: #1565c0;
        }

        .btn-secondary {
            background: #424242;
            color: white;
            margin-top: 8px;
        }

        .btn-secondary:hover {
            background: #616161;
        }

        .canvas-container {
            background: #0a0a0a;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
        }

        #mainCanvas {
            border: 1px solid #444;
            cursor: crosshair;
            max-width: 100%;
            max-height: calc(100vh - 100px);
        }

        .title-overlay {
            position: absolute;
            top: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.85);
            padding: 15px 30px;
            border-radius: 8px;
            border: 1px solid #555;
            display: none;
        }

        .title-overlay h1 {
            font-size: 1.5em;
            color: #4fc3f7;
            text-align: center;
        }

        .info-panel {
            background: #2a2a2a;
            overflow-y: auto;
            padding: 20px;
        }

        .detail-section {
            background: #1a1a1a;
            padding: 15px;
            border-radius: 4px;
            margin-bottom: 15px;
            border: 1px solid #444;
        }

        .detail-section h3 {
            font-size: 1em;
            color: #4fc3f7;
            margin-bottom: 10px;
            padding-bottom: 8px;
            border-bottom: 1px solid #444;
        }

        .detail-row {
            display: flex;
            justify-content: space-between;
            padding: 6px 0;
            font-size: 0.85em;
            border-bottom: 1px solid #333;
        }

        .detail-row:last-child {
            border-bottom: none;
        }

        .detail-label {
            color: #9e9e9e;
        }

        .detail-value {
            color: #e0e0e0;
            font-family: 'Consolas', monospace;
            font-weight: 500;
        }

        .pattern-list {
            max-height: 300px;
            overflow-y: auto;
            margin-top: 10px;
        }

        .pattern-item {
            background: #2a2a2a;
            padding: 8px;
            margin-bottom: 6px;
            border-radius: 3px;
            font-size: 0.85em;
            font-family: 'Consolas', monospace;
        }

        .legend-box {
            background: rgba(0, 0, 0, 0.85);
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #555;
            font-size: 0.85em;
        }

        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
        }

        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 3px;
            margin-right: 10px;
        }

        .input-hint {
            font-size: 0.75em;
            color: #757575;
            margin-top: 4px;
        }

        .section-divider {
            height: 1px;
            background: #444;
            margin: 20px 0;
        }

        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #1a1a1a;
        }

        ::-webkit-scrollbar-thumb {
            background: #555;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #666;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Left Panel: Controls -->
        <div class="panel">
            <h2>Configuration Parameters</h2>
            
            <div class="control-group">
                <label>Custom Title</label>
                <input type="text" id="customTitle" placeholder="Enter custom title">
                <div class="input-hint">Leave blank for default</div>
            </div>

            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="showTitle">
                    <span>Display Title Overlay</span>
                </label>
            </div>

            <div class="section-divider"></div>

            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="useDynadic">
                    <span>Use Dyadic Family (m×2ⁿ)</span>
                </label>
            </div>

            <div id="regularControls">
                <div class="control-group">
                    <label>Moduli Range (comma-separated or range)</label>
                    <input type="text" id="moduliInput" value="1,2,3,4,5,6,7,8,9,10">
                    <div class="input-hint">e.g., "2,3,5,7" or "1-10" or "2"</div>
                </div>
            </div>

            <div id="dyadicControls" style="display: none;">
                <div class="control-group">
                    <label>Base Value (m)</label>
                    <input type="number" id="dynadicBase" value="30" step="1">
                </div>
                
                <div class="control-group">
                    <label>Maximum Exponent (n)</label>
                    <input type="number" id="dynadicExp" value="3" min="0" max="10">
                </div>
            </div>

            <div class="section-divider"></div>
            
            <div class="control-group">
                <label>Range Start (r)</label>
                <input type="number" id="rangeStart" value="0" step="1">
            </div>
            
            <div class="control-group">
                <label>Range End</label>
                <input type="number" id="rangeEnd" value="100" step="1">
            </div>
            
            <div class="control-group">
                <label>Connection Gap</label>
                <input type="number" id="connectionGap" value="2" min="0" step="1">
                <div class="input-hint">Set to 0 to disable</div>
            </div>

            <div class="section-divider"></div>

            <div class="control-group">
                <label>Angle Display Format</label>
                <select id="angleFormat">
                    <option value="degrees">Degrees (0-360°)</option>
                    <option value="radians">Radians (0-2π)</option>
                    <option value="fraction">Fraction (r/m)</option>
                </select>
            </div>

            <div class="control-group">
                <label>Farey Sequence Display</label>
                <select id="fareyFormat">
                    <option value="fraction">Fraction (p/q)</option>
                    <option value="decimal">Decimal</option>
                    <option value="both">Both</option>
                </select>
            </div>

            <div class="control-group">
                <label>Decimal Precision</label>
                <input type="number" id="decimalPrecision" value="4" min="1" max="10">
            </div>

            <div class="section-divider"></div>

            <div class="control-group">
                <label>Global Scale Multiplier</label>
                <input type="number" id="globalScale" value="1.0" step="0.1" min="0.1" max="5.0">
            </div>

            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="invertScale">
                    <span>Invert Scale (Inside-Out)</span>
                </label>
            </div>

            <div class="section-divider"></div>

            <div class="control-group">
                <label>Point Subdivision</label>
                <input type="number" id="pointSubdivision" value="1" min="1" max="100">
                <div class="input-hint">Multiply points per modulo unit</div>
            </div>

            <div class="control-group">
                <label>Color Scheme</label>
                <select id="colorScheme">
                    <option value="viridis">Viridis</option>
                    <option value="rainbow">Rainbow</option>
                    <option value="plasma">Plasma</option>
                    <option value="grayscale">Grayscale</option>
                    <option value="thermal">Thermal</option>
                </select>
            </div>
            
            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="showLabels" checked>
                    <span>Show Point Labels</span>
                </label>
            </div>
            
            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="showConnections" checked>
                    <span>Show Connections</span>
                </label>
            </div>
            
            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="showPrimes" checked>
                    <span>Highlight Prime Numbers</span>
                </label>
            </div>

            <div class="control-group">
                <label class="checkbox-label">
                    <input type="checkbox" id="enableAI">
                    <span>AI Pattern Recognition</span>
                </label>
            </div>

            <div class="section-divider"></div>
            
            <button class="btn btn-primary" onclick="drawVisualization()">Render Visualization</button>
            <button class="btn btn-secondary" onclick="downloadImage()">Download Image (8K)</button>
        </div>

        <!-- Center: Canvas -->
        <div class="canvas-container">
            <div class="title-overlay" id="titleOverlay">
                <h1 id="displayTitle">Modular Arithmetic Ring Analysis</h1>
            </div>
            <canvas id="mainCanvas" width="7680" height="4320"></canvas>
        </div>

        <!-- Right Panel: Information -->
        <div class="info-panel">
            <h2>Point Information</h2>
            
            <div class="detail-section">
                <h3>Click Detection</h3>
                <div class="detail-row">
                    <span class="detail-label">Status:</span>
                    <span class="detail-value" id="clickStatus">Click on a point</span>
                </div>
            </div>

            <div class="detail-section" id="pointDetails" style="display: none;">
                <h3>Point Details</h3>
                <div class="detail-row">
                    <span class="detail-label">Modulus (m):</span>
                    <span class="detail-value" id="detailMod">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Residue (r):</span>
                    <span class="detail-value" id="detailResidue">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">GCD(r, m):</span>
                    <span class="detail-value" id="detailGCD">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Coprime:</span>
                    <span class="detail-value" id="detailCoprime">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Is Prime:</span>
                    <span class="detail-value" id="detailPrime">-</span>
                </div>
            </div>

            <div class="detail-section" id="angleDetails" style="display: none;">
                <h3>Angle Information</h3>
                <div class="detail-row">
                    <span class="detail-label">Degrees:</span>
                    <span class="detail-value" id="angleDegrees">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Radians:</span>
                    <span class="detail-value" id="angleRadians">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Fraction:</span>
                    <span class="detail-value" id="angleFraction">-</span>
                </div>
            </div>

            <div class="detail-section" id="fareyDetails" style="display: none;">
                <h3>Farey Sequence</h3>
                <div class="detail-row">
                    <span class="detail-label">Reduced Fraction:</span>
                    <span class="detail-value" id="fareyFraction">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Decimal:</span>
                    <span class="detail-value" id="fareyDecimal">-</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Mediant:</span>
                    <span class="detail-value" id="fareyMediant">-</span>
                </div>
            </div>

            <div class="detail-section" id="patternDetails" style="display: none;">
                <h3>AI Pattern Recognition</h3>
                <div class="pattern-list" id="patternList"></div>
            </div>

            <div class="detail-section">
                <h3>Legend</h3>
                <div class="legend-box" id="legendBox"></div>
            </div>

            <div class="detail-section">
                <h3>Statistics</h3>
                <div class="detail-row">
                    <span class="detail-label">Total Moduli:</span>
                    <span class="detail-value" id="statModuli">0</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Total Points:</span>
                    <span class="detail-value" id="statPoints">0</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Primes Found:</span>
                    <span class="detail-value" id="statPrimes">0</span>
                </div>
                <div class="detail-row">
                    <span class="detail-label">Connections:</span>
                    <span class="detail-value" id="statConnections">0</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        let primes = [];
        let currentModuli = [];
        let clickablePoints = [];

        function gcd(a, b) {
            return b === 0 ? a : gcd(b, a % b);
        }

        function sieveOfEratosthenes(max) {
            const sieve = new Array(max + 1).fill(true);
            sieve[0] = sieve[1] = false;
            
            for (let i = 2; i * i <= max; i++) {
                if (sieve[i]) {
                    for (let j = i * i; j <= max; j += i) {
                        sieve[j] = false;
                    }
                }
            }
            
            return sieve.map((isPrime, num) => isPrime ? num : -1).filter(n => n > 0);
        }

        function parseModuliInput(input) {
            input = input.trim();
            
            if (input.includes('-')) {
                const parts = input.split('-').map(p => parseInt(p.trim()));
                if (parts.length === 2 && !isNaN(parts[0]) && !isNaN(parts[1])) {
                    const result = [];
                    for (let i = Math.min(parts[0], parts[1]); i <= Math.max(parts[0], parts[1]); i++) {
                        if (i > 0) result.push(i);
                    }
                    return result;
                }
            }
            
            return input.split(',')
                .map(s => parseInt(s.trim()))
                .filter(n => !isNaN(n) && n > 0)
                .sort((a, b) => a - b);
        }

        function getColor(index, total, scheme) {
            const t = index / Math.max(total - 1, 1);
            
            switch (scheme) {
                case 'viridis':
                    return `hsl(${240 + t * 120}, 70%, ${30 + t * 40}%)`;
                case 'rainbow':
                    return `hsl(${t * 360}, 80%, 50%)`;
                case 'plasma':
                    return `hsl(${280 - t * 200}, 90%, ${40 + t * 30}%)`;
                case 'grayscale':
                    const gray = Math.floor(50 + t * 150);
                    return `rgb(${gray}, ${gray}, ${gray})`;
                case 'thermal':
                    return `hsl(${240 - t * 240}, 100%, 50%)`;
                default:
                    return `hsl(${t * 360}, 70%, 50%)`;
            }
        }

        function analyzePatterns(mod, residue) {
            const patterns = [];
            
            const g = gcd(residue, mod);
            if (g === 1) {
                patterns.push(`Coprime to ${mod}: generates cyclic group`);
            } else {
                patterns.push(`GCD = ${g}: subgroup of order ${mod / g}`);
            }
            
            if (primes.includes(residue)) {
                patterns.push(`Prime number: fundamental building block`);
            }
            
            const phi = mod - 1;
            if (residue === phi) {
                patterns.push(`φ(${mod}) = ${phi}: Euler's totient`);
            }
            
            if (mod % residue === 0) {
                patterns.push(`Divides modulus: ${mod / residue} × ${residue} = ${mod}`);
            }
            
            const angle = (residue / mod) * 360;
            if (Math.abs(angle - 90) < 1) patterns.push('Quadrature point (90°)');
            if (Math.abs(angle - 180) < 1) patterns.push('Opposition point (180°)');
            if (Math.abs(angle - 120) < 1) patterns.push('Trine point (120°)');
            
            return patterns;
        }

        function formatAngle(r, m, format) {
            const fraction = r / m;
            switch (format) {
                case 'degrees':
                    return (fraction * 360).toFixed(2) + '°';
                case 'radians':
                    return (fraction * 2 * Math.PI).toFixed(4) + ' rad';
                case 'fraction':
                    return `${r}/${m} turn`;
                default:
                    return (fraction * 360).toFixed(2) + '°';
            }
        }

        function formatFarey(r, m, format, precision) {
            const g = gcd(r, m);
            const p = r / g;
            const q = m / g;
            const decimal = (r / m).toFixed(precision);
            
            switch (format) {
                case 'fraction':
                    return `${p}/${q}`;
                case 'decimal':
                    return decimal;
                case 'both':
                    return `${p}/${q} ≈ ${decimal}`;
                default:
                    return `${p}/${q}`;
            }
        }

        function drawVisualization() {
            const canvas = document.getElementById('mainCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            
            const useDynadic = document.getElementById('useDynadic').checked;
            const moduliInput = document.getElementById('moduliInput').value;
            const dynadicBase = parseInt(document.getElementById('dynadicBase').value) || 30;
            const dynadicExp = parseInt(document.getElementById('dynadicExp').value) || 3;
            const rangeStart = parseInt(document.getElementById('rangeStart').value) || 0;
            const rangeEnd = parseInt(document.getElementById('rangeEnd').value) || 100;
            const connectionGap = parseInt(document.getElementById('connectionGap').value) || 0;
            const colorScheme = document.getElementById('colorScheme').value;
            const showLabels = document.getElementById('showLabels').checked;
            const showConnections = document.getElementById('showConnections').checked;
            const showPrimes = document.getElementById('showPrimes').checked;
            const globalScale = parseFloat(document.getElementById('globalScale').value) || 1.0;
            const invertScale = document.getElementById('invertScale').checked;
            const pointSubdiv = parseInt(document.getElementById('pointSubdivision').value) || 1;
            const showTitle = document.getElementById('showTitle').checked;
            const customTitle = document.getElementById('customTitle').value.trim();
            
            document.getElementById('titleOverlay').style.display = showTitle ? 'block' : 'none';
            document.getElementById('displayTitle').textContent = customTitle || 'Modular Arithmetic Ring Analysis';
            
            let moduli = [];
            if (useDynadic) {
                for (let n = 0; n <= dynadicExp; n++) {
                    moduli.push(dynadicBase * Math.pow(2, n));
                }
            } else {
                moduli = parseModuliInput(moduliInput);
            }
            
            currentModuli = moduli;
            clickablePoints = [];
            
            const maxRange = Math.max(rangeEnd, 1000);
            primes = sieveOfEratosthenes(maxRange);
            const primeSet = new Set(primes);
            
            ctx.fillStyle = '#0a0a0a';
            ctx.fillRect(0, 0, width, height);
            
            const totalMods = moduli.length;
            const baseMaxRadius = Math.min(width, height) * 0.42;
            const maxRadius = baseMaxRadius * globalScale;
            const radiusStep = maxRadius / totalMods;
            
            let totalPoints = 0;
            let totalConnections = 0;
            
            moduli.forEach((mod, modIndex) => {
                let radius = (modIndex + 1) * radiusStep;
                if (invertScale) {
                    radius = maxRadius - radius + radiusStep;
                }
                
                const color = getColor(modIndex, totalMods, colorScheme);
                
                ctx.strokeStyle = color;
                ctx.lineWidth = 2;
                ctx.globalAlpha = 0.3;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
                ctx.stroke();
                
                ctx.globalAlpha = 1;
                
                const effectiveMod = mod * pointSubdiv;
                
                for (let rBase = rangeStart; rBase <= Math.min(rangeEnd, mod - 1); rBase++) {
                    for (let sub = 0; sub < pointSubdiv; sub++) {
                        const r = rBase * pointSubdiv + sub;
                        if (r >= effectiveMod) continue;
                        
                        const angle = (2 * Math.PI * r) / effectiveMod;
                        const x = centerX + radius * Math.cos(angle - Math.PI / 2);
                        const y = centerY + radius * Math.sin(angle - Math.PI / 2);
                        
                        const actualR = rBase;
                        const isPrime = showPrimes && primeSet.has(actualR);
                        
                        ctx.beginPath();
                        ctx.arc(x, y, isPrime ? 5 : 3, 0, 2 * Math.PI);
                        ctx.fillStyle = isPrime ? '#ffff00' : color;
                        ctx.fill();
                        
                        clickablePoints.push({
                            x: x / (width / canvas.offsetWidth),
                            y: y / (height / canvas.offsetHeight),
                            mod: mod,
                            residue: actualR,
                            angle: angle,
                            isPrime: isPrime
                        });
                        
                        totalPoints++;
                        
                        if (showLabels && modIndex < 3 && sub === 0) {
                            ctx.fillStyle = '#ffffff';
                            ctx.font = '10px monospace';
                            ctx.fillText(actualR.toString(), x + 8, y + 3);
                        }
                        
                        if (showConnections && connectionGap > 0 && sub === 0) {
                            const r2Base = actualR + connectionGap;
                            if (r2Base < mod) {
                                const r2 = r2Base * pointSubdiv;
                                const angle2 = (2 * Math.PI * r2) / effectiveMod;
                                const x2 = centerX + radius * Math.cos(angle2 - Math.PI / 2);
                                const y2 = centerY + radius * Math.sin(angle2 - Math.PI / 2);
                                
                                if (gcd(actualR, mod) === 1 || gcd(r2Base, mod) === 1) {
                                    ctx.strokeStyle = color;
                                    ctx.lineWidth = 0.5;
                                    ctx.globalAlpha = 0.2;
                                    ctx.beginPath();
                                    ctx.moveTo(x, y);
                                    ctx.lineTo(x2, y2);
                                    ctx.stroke();
                                    totalConnections++;
                                }
                            }
                        }
                    }
                }
                
                ctx.globalAlpha = 1;
                ctx.fillStyle = '#ffffff';
                ctx.font = 'bold 14px monospace';
                const labelX = centerX + radius * Math.cos(-Math.PI / 2) + 10;
                const labelY = centerY + radius * Math.sin(-Math.PI / 2);
                ctx.fillText(`mod ${mod}`, labelX, labelY);
            });
            
            updateLegend(colorScheme, moduli);
            updateStatistics(moduli.length, totalPoints, primes.length, totalConnections);
        }

        function updateLegend(scheme, moduli) {
            const legendBox = document.getElementById('legendBox');
            legendBox.innerHTML = '';
            
            const items = [
                { color: '#ffff00', label: 'Prime Numbers' },
                { color: '#ff0000', label: 'Connections' },
            ];
            
            if (moduli.length <= 10) {
                moduli.forEach((mod, i) => {
                    items.push({
                        color: getColor(i, moduli.length, scheme),
                        label: `mod ${mod}`
                    });
                });
            }
            
            items.forEach(item => {
                const div = document.createElement('div');
                div.className = 'legend-item';
                div.innerHTML = `
                    <div class="legend-color" style="background: ${item.color}"></div>
                    <span>${item.label}</span>
                `;
                legendBox.appendChild(div);
            });
        }

        function updateStatistics(modCount, pointCount, primeCount, connCount) {
            document.getElementById('statModuli').textContent = modCount;
            document.getElementById('statPoints').textContent = pointCount;
            document.getElementById('statPrimes').textContent = primeCount;
            document.getElementById('statConnections').textContent = connCount;
        }

        function handleCanvasClick(event) {
            const canvas = document.getElementById('mainCanvas');
            const rect = canvas.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;
            
            const threshold = 10;
            let closestPoint = null;
            let minDist = Infinity;
            
            clickablePoints.forEach(point => {
                const dx = point.x - x;
                const dy = point.y - y;
                const dist = Math.sqrt(dx * dx + dy * dy);
                
                if (dist < threshold && dist < minDist) {
                    minDist = dist;
                    closestPoint = point;
                }
            });
            
            if (closestPoint) {
                displayPointInfo(closestPoint);
            }
        }

        function displayPointInfo(point) {
            const angleFormat = document.getElementById('angleFormat').value;
            const fareyFormat = document.getElementById('fareyFormat').value;
            const precision = parseInt(document.getElementById('decimalPrecision').value) || 4;
            const enableAI = document.getElementById('enableAI').checked;
            
            document.getElementById('clickStatus').textContent = 'Point selected';
            document.getElementById('pointDetails').style.display = 'block';
            document.getElementById('angleDetails').style.display = 'block';
            document.getElementById('fareyDetails').style.display = 'block';
            
            const g = gcd(point.residue, point.mod);
            const isCoprime = g === 1;
            
            document.getElementById('detailMod').textContent = point.mod;
            document.getElementById('detailResidue').textContent = point.residue;
            document.getElementById('detailGCD').textContent = g;
            document.getElementById('detailCoprime').textContent = isCoprime ? 'Yes' : 'No';
            document.getElementById('detailPrime').textContent = point.isPrime ? 'Yes' : 'No';
            
            const degrees = ((point.residue / point.mod) * 360).toFixed(precision);
            const radians = ((point.residue / point.mod) * 2 * Math.PI).toFixed(precision);
            const fraction = `${point.residue}/${point.mod}`;
            
            document.getElementById('angleDegrees').textContent = degrees + '°';
            document.getElementById('angleRadians').textContent = radians + ' rad';
            document.getElementById('angleFraction').textContent = fraction + ' turn';
            
            const fareyG = gcd(point.residue, point.mod);
            const fareyP = point.residue / fareyG;
            const fareyQ = point.mod / fareyG;
            const fareyDecimal = (point.residue / point.mod).toFixed(precision);
            
            document.getElementById('fareyFraction').textContent = `${fareyP}/${fareyQ}`;
            document.getElementById('fareyDecimal').textContent = fareyDecimal;
            
            const nextR = (point.residue + 1) % point.mod;
            const mediantNum = fareyP + nextR;
            const mediantDen = fareyQ + point.mod;
            const mediantG = gcd(mediantNum, mediantDen);
            document.getElementById('fareyMediant').textContent = 
                `${mediantNum / mediantG}/${mediantDen / mediantG}`;
            
            if (enableAI) {
                const patterns = analyzePatterns(point.mod, point.residue);
                document.getElementById('patternDetails').style.display = 'block';
                const patternList = document.getElementById('patternList');
                patternList.innerHTML = '';
                
                patterns.forEach(pattern => {
                    const div = document.createElement('div');
                    div.className = 'pattern-item';
                    div.textContent = '• ' + pattern;
                    patternList.appendChild(div);
                });
            } else {
                document.getElementById('patternDetails').style.display = 'none';
            }
        }

        function downloadImage() {
            const canvas = document.getElementById('mainCanvas');
            const ctx = canvas.getContext('2d');
            
            ctx.globalAlpha = 0.7;
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 20px monospace';
            ctx.fillText('© Professional Analysis Tool', canvas.width - 350, canvas.height - 20);
            ctx.globalAlpha = 1;
            
            const link = document.createElement('a');
            link.download = `modular_analysis_${Date.now()}.jpg`;
            link.href = canvas.toDataURL('image/jpeg', 0.95);
            link.click();
            
            drawVisualization();
        }

        document.getElementById('useDynadic').addEventListener('change', function() {
            document.getElementById('regularControls').style.display = this.checked ? 'none' : 'block';
            document.getElementById('dyadicControls').style.display = this.checked ? 'block' : 'none';
        });

        document.getElementById('mainCanvas').addEventListener('click', handleCanvasClick);

        drawVisualization();
    </script>
</body>
</html>
