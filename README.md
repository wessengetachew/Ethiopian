<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Modular Ring System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 50%, #7e22ce 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1900px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.4);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 50%, #7e22ce 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.8em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            font-size: 1.2em;
            opacity: 0.95;
        }
        
        .content {
            display: grid;
            grid-template-columns: 380px 1fr;
            gap: 20px;
            padding: 30px;
        }
        
        .controls {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            height: fit-content;
            max-height: 90vh;
            overflow-y: auto;
        }
        
        .control-group {
            margin-bottom: 20px;
        }
        
        .control-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: #333;
            font-size: 0.95em;
        }
        
        .control-group input[type="number"],
        .control-group select {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s;
        }
        
        .control-group input[type="number"]:focus,
        .control-group select:focus {
            outline: none;
            border-color: #7e22ce;
        }
        
        .control-group input[type="range"] {
            width: 100%;
        }
        
        .checkbox-group {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }
        
        .checkbox-group input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .checkbox-group label {
            margin: 0;
            cursor: pointer;
            font-weight: 500;
        }
        
        .color-input-group {
            display: grid;
            grid-template-columns: 1fr 80px;
            gap: 10px;
            align-items: center;
        }
        
        input[type="color"] {
            width: 100%;
            height: 40px;
            border: 2px solid #ddd;
            border-radius: 8px;
            cursor: pointer;
        }
        
        button {
            width: 100%;
            padding: 12px;
            font-size: 1em;
            font-weight: 600;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 10px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #7e22ce 0%, #9333ea 100%);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(126, 34, 206, 0.4);
        }
        
        .btn-secondary {
            background: #10b981;
            color: white;
        }
        
        .btn-secondary:hover {
            background: #059669;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(16, 185, 129, 0.4);
        }
        
        .btn-tertiary {
            background: #3b82f6;
            color: white;
        }
        
        .btn-tertiary:hover {
            background: #2563eb;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(59, 130, 246, 0.4);
        }
        
        .btn-danger {
            background: #ef4444;
            color: white;
        }
        
        .btn-danger:hover {
            background: #dc2626;
        }
        
        .canvas-container {
            background: white;
            border-radius: 15px;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 900px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        canvas {
            max-width: 100%;
            height: auto;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            cursor: crosshair;
        }
        
        .info-panel {
            background: linear-gradient(135deg, #dbeafe 0%, #e0e7ff 100%);
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            font-size: 0.9em;
        }
        
        .info-panel h3 {
            margin-bottom: 10px;
            color: #1e40af;
        }
        
        .info-item {
            margin-bottom: 5px;
            color: #1e293b;
            font-weight: 500;
        }
        
        .value-display {
            display: inline-block;
            background: white;
            padding: 2px 8px;
            border-radius: 4px;
            margin-left: 5px;
            font-weight: 700;
            color: #7e22ce;
        }
        
        .export-options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        
        .section-title {
            font-size: 1.2em;
            font-weight: 700;
            margin-bottom: 15px;
            color: #7e22ce;
            border-bottom: 2px solid #7e22ce;
            padding-bottom: 8px;
        }
        
        .gcd-colormap {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 5px;
            margin-top: 10px;
        }
        
        .gcd-color-item {
            display: flex;
            align-items: center;
            gap: 5px;
            font-size: 0.85em;
        }
        
        .gcd-color-box {
            width: 20px;
            height: 20px;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        
        .preset-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }
        
        .preset-btn {
            padding: 8px;
            font-size: 0.9em;
            background: #e2e8f0;
            color: #334155;
        }
        
        .preset-btn:hover {
            background: #cbd5e1;
        }
        
        @media (max-width: 1400px) {
            .content {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌟 Advanced Modular Ring System</h1>
            <p>Interactive visualization with GCD color coding, Farey fractions, and ultra high-res export</p>
        </div>
        
        <div class="content">
            <div class="controls">
                <div class="section-title">⚙️ Ring Configuration</div>
                
                <div class="control-group">
                    <label for="maxMod">Maximum Modulus (1-100):</label>
                    <input type="number" id="maxMod" min="1" max="100" value="15">
                </div>
                
                <div class="control-group">
                    <label for="startMod">Start Modulus:</label>
                    <input type="number" id="startMod" min="1" max="100" value="1">
                </div>
                
                <div class="control-group">
                    <label for="ringSpacing">Ring Spacing:</label>
                    <input type="range" id="ringSpacing" min="10" max="120" value="45">
                    <span class="value-display" id="ringSpacingValue">45</span>
                </div>
                
                <div class="control-group">
                    <label for="pointSize">Point Size:</label>
                    <input type="range" id="pointSize" min="1" max="25" value="7">
                    <span class="value-display" id="pointSizeValue">7</span>
                </div>
                
                <div class="checkbox-group">
                    <input type="checkbox" id="showRingGuides" checked>
                    <label for="showRingGuides">Show Ring Guides</label>
                </div>
                
                <div class="checkbox-group">
                    <input type="checkbox" id="showRadialLines">
                    <label for="showRadialLines">Show Radial Lines</label>
                </div>
                
                <div class="section-title">🎨 Color Mode</div>
                
                <div class="control-group">
                    <label for="colorMode">Color Mode:</label>
                    <select id="colorMode" onchange="updateColorMode()">
                        <option value="binary">Binary (Coprime/Non-coprime)</option>
                        <option value="gcd">GCD Value</option>
                        <option value="gradient">Gradient by Angle</option>
                        <option value="totient">Euler Totient Class</option>
                    </select>
                </div>
                
                <div id="binaryColorControls">
                    <div class="control-group">
                        <label>Coprime Color (GCD=1):</label>
                        <div class="color-input-group">
                            <input type="color" id="coprimeColor" value="#3b82f6">
                            <span class="value-display">#3b82f6</span>
                        </div>
                    </div>
                    
                    <div class="control-group">
                        <label>Non-Coprime Color (GCD>1):</label>
                        <div class="color-input-group">
                            <input type="color" id="nonCoprimeColor" value="#ef4444">
                            <span class="value-display">#ef4444</span>
                        </div>
                    </div>
                </div>
                
                <div class="control-group">
                    <label>Background Color:</label>
                    <div class="color-input-group">
                        <input type="color" id="bgColor" value="#FFFFFF">
                        <span class="value-display">#FFFFFF</span>
                    </div>
                </div>
                
                <div class="section-title">🏷️ Label Options</div>
                
                <div class="control-group">
                    <label for="labelType">Label Type:</label>
                    <select id="labelType">
                        <option value="none">No Labels</option>
                        <option value="angle">Angle (degrees)</option>
                        <option value="angle_rad">Angle (radians)</option>
                        <option value="gcd">GCD Value</option>
                        <option value="farey">Farey Fraction (k/m)</option>
                        <option value="farey_reduced">Farey Reduced</option>
                        <option value="element">Element (k)</option>
                        <option value="element_mod">Element k (mod m)</option>
                    </select>
                </div>
                
                <div class="control-group">
                    <label for="labelMod">Label Specific Modulus (0 = all):</label>
                    <input type="number" id="labelMod" min="0" max="100" value="0">
                </div>
                
                <div class="control-group">
                    <label for="labelFilter">Label Filter:</label>
                    <select id="labelFilter">
                        <option value="all">All Points</option>
                        <option value="coprime">Coprime Only (GCD=1)</option>
                        <option value="noncoprime">Non-Coprime Only (GCD>1)</option>
                        <option value="gcd_specific">Specific GCD Value</option>
                    </select>
                </div>
                
                <div class="control-group" id="gcdFilterGroup" style="display:none;">
                    <label for="gcdFilterValue">GCD Value to Label:</label>
                    <input type="number" id="gcdFilterValue" min="1" max="100" value="2">
                </div>
                
                <div class="control-group">
                    <label for="labelSize">Label Font Size:</label>
                    <input type="range" id="labelSize" min="4" max="24" value="9">
                    <span class="value-display" id="labelSizeValue">9</span>
                </div>
                
                <div class="control-group">
                    <label>Label Color:</label>
                    <div class="color-input-group">
                        <input type="color" id="labelColor" value="#000000">
                        <span class="value-display">#000000</span>
                    </div>
                </div>
                
                <div class="section-title">🎯 Presets</div>
                
                <div class="preset-buttons">
                    <button class="preset-btn" onclick="loadPreset('classic')">Classic</button>
                    <button class="preset-btn" onclick="loadPreset('dark')">Dark Mode</button>
                    <button class="preset-btn" onclick="loadPreset('rainbow')">Rainbow</button>
                    <button class="preset-btn" onclick="loadPreset('minimal')">Minimal</button>
                </div>
                
                <div class="section-title">📤 Export</div>
                
                <div class="control-group">
                    <label for="exportFormat">Format:</label>
                    <select id="exportFormat">
                        <option value="png">PNG (Lossless)</option>
                        <option value="jpeg">JPEG (Compressed)</option>
                    </select>
                </div>
                
                <div class="export-options">
                    <button class="btn-secondary" onclick="exportImage(4096)">📥 4K (4096px)</button>
                    <button class="btn-secondary" onclick="exportImage(7680)">📥 8K (7680px)</button>
                </div>
                
                <button class="btn-tertiary" onclick="exportImage(1920)">📥 Full HD (1920px)</button>
                <button class="btn-tertiary" onclick="exportImage(3840)">📥 4K UHD (3840px)</button>
                
                <button class="btn-primary" onclick="drawRings()">🔄 Redraw</button>
                
                <div class="info-panel">
                    <h3>📊 Statistics</h3>
                    <div class="info-item">Total Rings: <span class="value-display" id="totalRings">15</span></div>
                    <div class="info-item">Total Points: <span class="value-display" id="totalPoints">0</span></div>
                    <div class="info-item">Coprime: <span class="value-display" id="coprimePoints">0</span></div>
                    <div class="info-item">Non-Coprime: <span class="value-display" id="nonCoprimePoints">0</span></div>
                    <div class="info-item">Coprime %: <span class="value-display" id="coprimePercent">0%</span></div>
                </div>
            </div>
            
            <div class="canvas-container">
                <canvas id="ringCanvas"></canvas>
            </div>
        </div>
    </div>
    
    <script>
        // Utility functions
        function gcd(a, b) {
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return Math.abs(a);
        }
        
        function getCoprimElements(m) {
            if (m === 1) return [0];
            const coprimes = [];
            for (let k = 0; k < m; k++) {
                if (gcd(k, m) === 1) {
                    coprimes.push(k);
                }
            }
            return coprimes;
        }
        
        function simplifyFraction(num, den) {
            const g = gcd(num, den);
            return [num / g, den / g];
        }
        
        function eulerPhi(n) {
            let result = n;
            for (let p = 2; p * p <= n; p++) {
                if (n % p === 0) {
                    while (n % p === 0) n /= p;
                    result -= result / p;
                }
            }
            if (n > 1) result -= result / n;
            return Math.floor(result);
        }
        
        function hslToHex(h, s, l) {
            l /= 100;
            const a = s * Math.min(l, 1 - l) / 100;
            const f = n => {
                const k = (n + h / 30) % 12;
                const color = l - a * Math.max(Math.min(k - 3, 9 - k, 1), -1);
                return Math.round(255 * color).toString(16).padStart(2, '0');
            };
            return `#${f(0)}${f(8)}${f(4)}`;
        }
        
        function getColorByGCD(gcdValue, maxGcd) {
            // Generate distinct colors for different GCD values
            const hue = (gcdValue * 137.5) % 360; // Golden angle for distribution
            const saturation = 70;
            const lightness = gcdValue === 1 ? 50 : 45 + (gcdValue / maxGcd) * 20;
            return hslToHex(hue, saturation, lightness);
        }
        
        // Canvas drawing
        const canvas = document.getElementById('ringCanvas');
        const ctx = canvas.getContext('2d');
        
        // Initialize canvas size
        canvas.width = 1400;
        canvas.height = 1400;
        
        function drawRings() {
            const maxMod = parseInt(document.getElementById('maxMod').value);
            const startMod = parseInt(document.getElementById('startMod').value);
            const ringSpacing = parseInt(document.getElementById('ringSpacing').value);
            const pointSize = parseInt(document.getElementById('pointSize').value);
            const labelType = document.getElementById('labelType').value;
            const labelMod = parseInt(document.getElementById('labelMod').value);
            const labelFilter = document.getElementById('labelFilter').value;
            const gcdFilterValue = parseInt(document.getElementById('gcdFilterValue').value);
            const labelSize = parseInt(document.getElementById('labelSize').value);
            const labelColor = document.getElementById('labelColor').value;
            const coprimeColor = document.getElementById('coprimeColor').value;
            const nonCoprimeColor = document.getElementById('nonCoprimeColor').value;
            const bgColor = document.getElementById('bgColor').value;
            const colorMode = document.getElementById('colorMode').value;
            const showRingGuides = document.getElementById('showRingGuides').checked;
            const showRadialLines = document.getElementById('showRadialLines').checked;
            
            // Clear canvas
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const maxRadius = Math.min(canvas.width, canvas.height) * 0.44;
            
            let totalPoints = 0;
            let coprimePointsCount = 0;
            let nonCoprimePointsCount = 0;
            
            // Find max GCD for color scaling
            let maxGcdValue = 1;
            for (let m = startMod; m <= maxMod; m++) {
                for (let k = 0; k < m; k++) {
                    maxGcdValue = Math.max(maxGcdValue, gcd(k, m));
                }
            }
            
            // Draw radial lines if enabled
            if (showRadialLines) {
                ctx.strokeStyle = '#e0e0e0';
                ctx.lineWidth = 1;
                const numLines = 12;
                for (let i = 0; i < numLines; i++) {
                    const angle = (2 * Math.PI * i / numLines) - Math.PI / 2;
                    ctx.beginPath();
                    ctx.moveTo(centerX, centerY);
                    ctx.lineTo(
                        centerX + maxRadius * Math.cos(angle),
                        centerY + maxRadius * Math.sin(angle)
                    );
                    ctx.stroke();
                }
            }
            
            // Draw rings
            for (let m = startMod; m <= maxMod; m++) {
                const radius = (m - startMod + 1) * ringSpacing;
                if (radius > maxRadius) continue;
                
                // Draw ring circle (guide)
                if (showRingGuides) {
                    ctx.strokeStyle = '#e5e7eb';
                    ctx.lineWidth = 1;
                    ctx.beginPath();
                    ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
                    ctx.stroke();
                }
                
                // Get coprime elements
                const coprimes = new Set(getCoprimElements(m));
                
                // Draw points for this modulus
                for (let k = 0; k < m; k++) {
                    const angle = (2 * Math.PI * k / m) - Math.PI / 2; // Start from top
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    const isCoprime = coprimes.has(k);
                    const gcdValue = gcd(k, m);
                    
                    // Choose color based on mode
                    let pointColor;
                    switch (colorMode) {
                        case 'binary':
                            pointColor = isCoprime ? coprimeColor : nonCoprimeColor;
                            break;
                        case 'gcd':
                            pointColor = getColorByGCD(gcdValue, maxGcdValue);
                            break;
                        case 'gradient':
                            const hue = (k * 360 / m) % 360;
                            pointColor = hslToHex(hue, 70, isCoprime ? 50 : 40);
                            break;
                        case 'totient':
                            const phi = eulerPhi(m);
                            const hue2 = (phi * 30) % 360;
                            pointColor = hslToHex(hue2, 65, isCoprime ? 55 : 45);
                            break;
                    }
                    
                    ctx.fillStyle = pointColor;
                    
                    // Draw point
                    if (isCoprime) {
                        ctx.beginPath();
                        ctx.arc(x, y, pointSize / 2, 0, 2 * Math.PI);
                        ctx.fill();
                        coprimePointsCount++;
                    } else {
                        ctx.strokeStyle = pointColor;
                        ctx.lineWidth = 2.5;
                        const offset = pointSize / 2;
                        ctx.beginPath();
                        ctx.moveTo(x - offset, y - offset);
                        ctx.lineTo(x + offset, y + offset);
                        ctx.moveTo(x + offset, y - offset);
                        ctx.lineTo(x - offset, y + offset);
                        ctx.stroke();
                        nonCoprimePointsCount++;
                    }
                    
                    totalPoints++;
                    
                    // Determine if this point should be labeled
                    let shouldLabel = (labelMod === 0 || labelMod === m);
                    if (shouldLabel) {
                        switch (labelFilter) {
                            case 'coprime':
                                shouldLabel = isCoprime;
                                break;
                            case 'noncoprime':
                                shouldLabel = !isCoprime;
                                break;
                            case 'gcd_specific':
                                shouldLabel = (gcdValue === gcdFilterValue);
                                break;
                        }
                    }
                    
                    // Draw labels
                    if (labelType !== 'none' && shouldLabel) {
                        let labelText = '';
                        
                        switch (labelType) {
                            case 'angle':
                                const degrees = ((k * 360 / m) % 360).toFixed(1);
                                labelText = degrees + '°';
                                break;
                            case 'angle_rad':
                                const radians = ((k * 2 * Math.PI / m) % (2 * Math.PI)).toFixed(3);
                                labelText = radians + 'r';
                                break;
                            case 'gcd':
                                labelText = gcdValue.toString();
                                break;
                            case 'farey':
                                labelText = k + '/' + m;
                                break;
                            case 'farey_reduced':
                                const [num, den] = simplifyFraction(k, m);
                                labelText = num + '/' + den;
                                break;
                            case 'element':
                                labelText = k.toString();
                                break;
                            case 'element_mod':
                                labelText = `${k}₍${m}₎`;
                                break;
                        }
                        
                        // Position label
                        const labelOffset = pointSize + 10;
                        const labelX = centerX + (radius + labelOffset) * Math.cos(angle);
                        const labelY = centerY + (radius + labelOffset) * Math.sin(angle);
                        
                        // Draw label background for readability
                        ctx.font = `${labelSize}px Arial`;
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'middle';
                        const metrics = ctx.measureText(labelText);
                        const padding = 2;
                        
                        ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                        ctx.fillRect(
                            labelX - metrics.width / 2 - padding,
                            labelY - labelSize / 2 - padding,
                            metrics.width + padding * 2,
                            labelSize + padding * 2
                        );
                        
                        ctx.fillStyle = labelColor;
                        ctx.fillText(labelText, labelX, labelY);
                    }
                }
            }
            
            // Draw center point
            ctx.fillStyle = '#9333ea';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 4, 0, 2 * Math.PI);
            ctx.fill();
            
            // Draw title
            ctx.fillStyle = '#1e293b';
            ctx.font = 'bold 28px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`Modular Rings: mod ${startMod} to ${maxMod}`, centerX, 35);
            
            // Draw subtitle with label info
            if (labelType !== 'none') {
                ctx.font = '14px Arial';
                ctx.fillStyle = '#64748b';
                const labelTypeNames = {
                    'angle': 'Angles (degrees)',
                    'angle_rad': 'Angles (radians)',
                    'gcd': 'GCD values',
                    'farey': 'Farey fractions',
                    'farey_reduced': 'Reduced fractions',
                    'element': 'Elements',
                    'element_mod': 'Elements with modulus'
                };
                ctx.fillText(`Labels: ${labelTypeNames[labelType]}`, centerX, 58);
            }
            
            // Draw legend
            const legendY = canvas.height - 45;
            ctx.font = '16px Arial';
            
            if (colorMode === 'binary') {
                ctx.fillStyle = coprimeColor;
                ctx.beginPath();
                ctx.arc(centerX - 180, legendY, 7, 0, 2 * Math.PI);
                ctx.fill();
                ctx.fillStyle = '#1e293b';
                ctx.fillText('Coprime (GCD=1)', centerX - 100, legendY + 5);
                
                ctx.strokeStyle = nonCoprimeColor;
                ctx.lineWidth = 2.5;
                ctx.beginPath();
                ctx.moveTo(centerX + 60, legendY - 7);
                ctx.lineTo(centerX + 74, legendY + 7);
                ctx.moveTo(centerX + 74, legendY - 7);
                ctx.lineTo(centerX + 60, legendY + 7);
                ctx.stroke();
                ctx.fillStyle = '#1e293b';
                ctx.fillText('Non-Coprime (GCD>1)', centerX + 160, legendY + 5);
            } else {
                ctx.fillStyle = '#1e293b';
                ctx.fillText(`Color Mode: ${colorMode}`, centerX, legendY + 5);
            }
            
            // Update info panel
            const numRings = maxMod - startMod + 1;
            document.getElementById('totalRings').textContent = numRings;
            document.getElementById('totalPoints').textContent = totalPoints;
            document.getElementById('coprimePoints').textContent = coprimePointsCount;
            document.getElementById('nonCoprimePoints').textContent = nonCoprimePointsCount;
            const coprimePercent = totalPoints > 0 ? 
                (coprimePointsCount / totalPoints * 100).toFixed(1) : 0;
            document.getElementById('coprimePercent').textContent = coprimePercent + '%';
        }
        
        function exportImage(resolution) {
            const format = document.getElementById('exportFormat').value;
            
            // Save current canvas size
            const originalWidth = canvas.width;
            const originalHeight = canvas.height;
            
            // Calculate scale factor
            const scale = resolution / originalWidth;
            
            // Save current parameter values
            const originalValues = {
                ringSpacing: document.getElementById('ringSpacing').value,
                pointSize: document.getElementById('pointSize').value,
                labelSize: document.getElementById('labelSize').value
            };
            
            // Scale parameters
            document.getElementById('ringSpacing').value = Math.round(parseInt(originalValues.ringSpacing) * scale);
            document.getElementById('pointSize').value = Math.round(parseInt(originalValues.pointSize) * scale);
            document.getElementById('labelSize').value = Math.round(parseInt(originalValues.labelSize) * scale);
            
            // Resize canvas
            canvas.width = resolution;
            canvas.height = resolution;
            
            // Draw high-res version
            drawRings();
            
            // Export
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            const filename = `modular_rings_${resolution}x${resolution}_${timestamp}.${format}`;
            
            if (format === 'png') {
                link.href = canvas.toDataURL('image/png');
            } else {
                link.href = canvas.toDataURL('image/jpeg', 0.95);
            }
            
            link.download = filename;
            link.click();
            
            // Restore original size and parameters
            canvas.width = originalWidth;
            canvas.height = originalHeight;
            document.getElementById('ringSpacing').value = originalValues.ringSpacing;
            document.getElementById('pointSize').value = originalValues.pointSize;
            document.getElementById('labelSize').value = originalValues.labelSize;
            
            // Redraw at normal resolution
            drawRings();
            
            console.log(`Exported ${resolution}x${resolution} ${format.toUpperCase()} image: ${filename}`);
        }
        
        function updateColorMode() {
            const colorMode = document.getElementById('colorMode').value;
            const binaryControls = document.getElementById('binaryColorControls');
            
            if (colorMode === 'binary') {
                binaryControls.style.display = 'block';
            } else {
                binaryControls.style.display = 'none';
            }
            
            drawRings();
        }
        
        function loadPreset(presetName) {
            switch (presetName) {
                case 'classic':
                    document.getElementById('coprimeColor').value = '#3b82f6';
                    document.getElementById('nonCoprimeColor').value = '#ef4444';
                    document.getElementById('bgColor').value = '#ffffff';
                    document.getElementById('labelColor').value = '#000000';
                    document.getElementById('colorMode').value = 'binary';
                    break;
                case 'dark':
                    document.getElementById('coprimeColor').value = '#60a5fa';
                    document.getElementById('nonCoprimeColor').value = '#f87171';
                    document.getElementById('bgColor').value = '#1e293b';
                    document.getElementById('labelColor').value = '#ffffff';
                    document.getElementById('colorMode').value = 'binary';
                    break;
                case 'rainbow':
                    document.getElementById('bgColor').value = '#0f172a';
                    document.getElementById('labelColor').value = '#ffffff';
                    document.getElementById('colorMode').value = 'gradient';
                    break;
                case 'minimal':
                    document.getElementById('coprimeColor').value = '#000000';
                    document.getElementById('nonCoprimeColor').value = '#999999';
                    document.getElementById('bgColor').value = '#ffffff';
                    document.getElementById('labelColor').value = '#000000';
                    document.getElementById('colorMode').value = 'binary';
                    document.getElementById('showRingGuides').checked = false;
                    break;
            }
            updateColorMode();
            updateColorDisplays();
            drawRings();
        }
        
        function updateColorDisplays() {
            document.getElementById('coprimeColor').nextElementSibling.textContent = 
                document.getElementById('coprimeColor').value;
            document.getElementById('nonCoprimeColor').nextElementSibling.textContent = 
                document.getElementById('nonCoprimeColor').value;
            document.getElementById('bgColor').nextElementSibling.textContent = 
                document.getElementById('bgColor').value;
            document.getElementById('labelColor').nextElementSibling.textContent = 
                document.getElementById('labelColor').value;
        }
        
        // Event listeners
        document.getElementById('ringSpacing').addEventListener('input', function() {
            document.getElementById('ringSpacingValue').textContent = this.value;
        });
        
        document.getElementById('pointSize').addEventListener('input', function() {
            document.getElementById('pointSizeValue').textContent = this.value;
        });
        
        document.getElementById('labelSize').addEventListener('input', function() {
            document.getElementById('labelSizeValue').textContent = this.value;
        });
        
        ['coprimeColor', 'nonCoprimeColor', 'bgColor', 'labelColor'].forEach(id => {
            document.getElementById(id).addEventListener('input', function() {
                this.nextElementSibling.textContent = this.value;
            });
        });
        
        document.getElementById('labelFilter').addEventListener('change', function() {
            const gcdGroup = document.getElementById('gcdFilterGroup');
            gcdGroup.style.display = (this.value === 'gcd_specific') ? 'block' : 'none';
        });
        
        // Auto-redraw on changes
        ['maxMod', 'startMod', 'labelType', 'labelMod', 'labelFilter', 
         'showRingGuides', 'showRadialLines'].forEach(id => {
            document.getElementById(id).addEventListener('change', drawRings);
        });
        
        // Initial draw
        drawRings();
    </script>
</body>
</html>
