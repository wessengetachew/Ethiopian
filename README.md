<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Farey Sequence and Dyadic Lifts</title>
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
            max-width: 1400px;
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
            font-size: 2.2em;
            margin-bottom: 10px;
            font-weight: 600;
        }
        
        .subtitle {
            font-size: 1.1em;
            opacity: 0.95;
            font-weight: 300;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 350px 1fr;
            gap: 0;
        }
        
        .controls {
            background: #f8f9fa;
            border-right: 2px solid #e0e0e0;
            padding: 25px;
            overflow-y: auto;
            max-height: calc(100vh - 200px);
        }
        
        .control-section {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }
        
        .control-section:last-child {
            border-bottom: none;
        }
        
        .control-section h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.1em;
            font-weight: 600;
        }
        
        .control-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 6px;
            font-weight: 500;
            color: #555;
            font-size: 0.9em;
        }
        
        input[type="number"],
        input[type="range"],
        select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 0.9em;
        }
        
        input[type="range"] {
            padding: 0;
        }
        
        .range-value {
            display: inline-block;
            margin-left: 10px;
            font-weight: 600;
            color: #667eea;
        }
        
        input[type="checkbox"] {
            margin-right: 8px;
        }
        
        .checkbox-label {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
            cursor: pointer;
        }
        
        button {
            width: 100%;
            padding: 12px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1em;
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
        
        .canvas-container {
            padding: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #fafbfc;
        }
        
        canvas {
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            background: white;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }
        
        .info-panel {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
            width: 100%;
            max-width: 800px;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }
        
        .info-item {
            padding: 12px;
            background: #f8f9fa;
            border-radius: 6px;
            border-left: 4px solid #667eea;
        }
        
        .info-item strong {
            display: block;
            color: #667eea;
            margin-bottom: 4px;
            font-size: 0.85em;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .info-item span {
            font-size: 1.3em;
            font-weight: 600;
            color: #333;
        }
        
        .legend {
            margin-top: 15px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 6px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
        }
        
        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            margin-right: 10px;
            border: 2px solid #333;
        }
        
        .warning {
            background: #fff3cd;
            border: 1px solid #ffc107;
            padding: 12px;
            border-radius: 6px;
            margin-top: 10px;
            font-size: 0.85em;
            color: #856404;
        }
        
        @media (max-width: 1024px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .controls {
                max-height: none;
                border-right: none;
                border-bottom: 2px solid #e0e0e0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Modular Farey Sequence Visualization</h1>
            <p class="subtitle">Interactive exploration of coprime residue shells and dyadic lifts</p>
        </header>
        
        <div class="main-content">
            <aside class="controls">
                <div class="control-section">
                    <h3>Modulus Configuration</h3>
                    <div class="control-group">
                        <label for="baseModulus">Base Modulus (M₀)</label>
                        <input type="number" id="baseModulus" value="30" min="2" max="100" step="1">
                    </div>
                    <div class="control-group">
                        <label for="numShells">Number of Shells (n)</label>
                        <input type="range" id="numShells" value="3" min="1" max="6" step="1">
                        <span class="range-value" id="numShellsValue">3</span>
                    </div>
                    <div class="control-group">
                        <label for="liftType">Lift Type</label>
                        <select id="liftType">
                            <option value="dyadic">Dyadic (×2)</option>
                            <option value="triadic">Triadic (×3)</option>
                            <option value="custom">Custom Factor</option>
                        </select>
                    </div>
                    <div class="control-group" id="customFactorGroup" style="display:none;">
                        <label for="customFactor">Custom Factor</label>
                        <input type="number" id="customFactor" value="2" min="2" max="10" step="1">
                    </div>
                </div>
                
                <div class="control-section">
                    <h3>Display Options</h3>
                    <div class="checkbox-label">
                        <input type="checkbox" id="showAngles" checked>
                        <label for="showAngles">Show Angular Positions</label>
                    </div>
                    <div class="checkbox-label">
                        <input type="checkbox" id="showLabels" checked>
                        <label for="showLabels">Show Residue Labels</label>
                    </div>
                    <div class="control-group">
                        <label for="connectionType">Lift Connections</label>
                        <select id="connectionType">
                            <option value="none">None</option>
                            <option value="direct">Direct (r → r)</option>
                            <option value="both">Both (r → r and r → r+M)</option>
                        </select>
                    </div>
                    <div class="checkbox-label">
                        <input type="checkbox" id="showParity" checked>
                        <label for="showParity">Color by Parity</label>
                    </div>
                    <div class="checkbox-label">
                        <input type="checkbox" id="showFarey">
                        <label for="showFarey">Show Farey Projection</label>
                    </div>
                    <div class="checkbox-label">
                        <input type="checkbox" id="showDirichlet">
                        <label for="showDirichlet">Highlight Dirichlet Support</label>
                    </div>
                </div>
                
                <div class="control-section">
                    <h3>Visualization Style</h3>
                    <div class="control-group">
                        <label for="pointSize">Point Size</label>
                        <input type="range" id="pointSize" value="6" min="2" max="12" step="1">
                        <span class="range-value" id="pointSizeValue">6</span>
                    </div>
                    <div class="control-group">
                        <label for="scaleFactor">Scale Factor</label>
                        <input type="range" id="scaleFactor" value="80" min="40" max="150" step="10">
                        <span class="range-value" id="scaleFactorValue">80</span>
                    </div>
                    <div class="control-group">
                        <label for="animationSpeed">Animation Speed</label>
                        <input type="range" id="animationSpeed" value="50" min="0" max="100" step="10">
                        <span class="range-value" id="animationSpeedValue">50</span>
                    </div>
                </div>
                
                <div class="control-section">
                    <button id="updateBtn">Update Visualization</button>
                    <button id="animateBtn">Animate Lifting</button>
                    <button id="resetBtn">Reset View</button>
                </div>
            </aside>
            
            <main class="canvas-container">
                <canvas id="mainCanvas" width="800" height="800"></canvas>
                
                <div class="info-panel">
                    <div class="info-grid" id="infoGrid">
                        <!-- Dynamically populated -->
                    </div>
                    
                    <div class="legend">
                        <strong>Legend</strong>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #4CAF50;"></div>
                            <span>Odd Residues</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: #2196F3;"></div>
                            <span>Even Residues</span>
                        </div>
                        <div class="legend-item">
                            <div style="width: 30px; height: 3px; background: #4CAF50; margin-right: 10px;"></div>
                            <span>Direct Lift (r → r)</span>
                        </div>
                        <div class="legend-item">
                            <div style="width: 30px; height: 3px; background: #9C27B0; margin-right: 10px; border-top: 2px dashed #9C27B0;"></div>
                            <span>Offset Lift (r → r+M)</span>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>
    
    <script>
        // Utility functions
        function gcd(a, b) {
            a = Math.abs(a);
            b = Math.abs(b);
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
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
            return Math.round(result);
        }
        
        function getCoprimeResidues(m) {
            const residues = [];
            for (let r = 1; r < m; r++) {
                if (gcd(r, m) === 1) {
                    residues.push(r);
                }
            }
            return residues;
        }
        
        // Main visualization class
        class ModularVisualizer {
            constructor(canvasId) {
                this.canvas = document.getElementById(canvasId);
                this.ctx = this.canvas.getContext('2d');
                this.centerX = this.canvas.width / 2;
                this.centerY = this.canvas.height / 2;
                
                this.config = {
                    baseModulus: 30,
                    numShells: 3,
                    liftFactor: 2,
                    pointSize: 6,
                    scaleFactor: 80,
                    showAngles: true,
                    showLabels: true,
                    connectionType: 'none',
                    showParity: true,
                    showFarey: false,
                    showDirichlet: false
                };
                
                this.shells = [];
                this.animating = false;
                this.animationFrame = 0;
            }
            
            computeShells() {
                this.shells = [];
                let currentModulus = this.config.baseModulus;
                
                for (let i = 0; i < this.config.numShells; i++) {
                    const residues = getCoprimeResidues(currentModulus);
                    const radius = 50 + (i * this.config.scaleFactor);
                    
                    const points = residues.map(r => ({
                        residue: r,
                        modulus: currentModulus,
                        angle: (2 * Math.PI * r) / currentModulus,
                        radius: radius,
                        x: this.centerX + radius * Math.cos((2 * Math.PI * r) / currentModulus - Math.PI / 2),
                        y: this.centerY + radius * Math.sin((2 * Math.PI * r) / currentModulus - Math.PI / 2),
                        parity: r % 2 === 0 ? 'even' : 'odd'
                    }));
                    
                    this.shells.push({
                        modulus: currentModulus,
                        radius: radius,
                        points: points,
                        phi: residues.length
                    });
                    
                    currentModulus *= this.config.liftFactor;
                }
            }
            
            draw() {
                this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
                
                // Draw shells (circles)
                this.shells.forEach((shell, idx) => {
                    this.ctx.beginPath();
                    this.ctx.arc(this.centerX, this.centerY, shell.radius, 0, 2 * Math.PI);
                    this.ctx.strokeStyle = '#ddd';
                    this.ctx.lineWidth = 1;
                    this.ctx.stroke();
                    
                    // Draw modulus label
                    this.ctx.fillStyle = '#666';
                    this.ctx.font = '14px Arial';
                    this.ctx.fillText(`M = ${shell.modulus}`, this.centerX + shell.radius + 10, this.centerY);
                });
                
                // Draw connections between shells
                if (this.config.connectionType !== 'none' && this.shells.length > 1) {
                    for (let i = 0; i < this.shells.length - 1; i++) {
                        const currentShell = this.shells[i];
                        const nextShell = this.shells[i + 1];
                        
                        currentShell.points.forEach(point => {
                            if (this.config.connectionType === 'direct') {
                                // Only r → r connections
                                const liftedDirect = this.findDirectLift(point, nextShell);
                                if (liftedDirect) {
                                    this.ctx.beginPath();
                                    this.ctx.moveTo(point.x, point.y);
                                    this.ctx.lineTo(liftedDirect.x, liftedDirect.y);
                                    this.ctx.strokeStyle = point.parity === 'odd' ? 'rgba(76, 175, 80, 0.4)' : 'rgba(33, 150, 243, 0.4)';
                                    this.ctx.lineWidth = 2;
                                    this.ctx.stroke();
                                }
                            } else if (this.config.connectionType === 'both') {
                                // Both r → r and r → r+M connections
                                const liftedPoints = this.findAllLifts(point, nextShell);
                                liftedPoints.forEach((lifted, idx) => {
                                    this.ctx.beginPath();
                                    this.ctx.moveTo(point.x, point.y);
                                    this.ctx.lineTo(lifted.x, lifted.y);
                                    // Different styles for direct vs offset lift
                                    if (idx === 0) {
                                        // Direct lift (r → r)
                                        this.ctx.strokeStyle = point.parity === 'odd' ? 'rgba(76, 175, 80, 0.5)' : 'rgba(33, 150, 243, 0.5)';
                                        this.ctx.lineWidth = 2;
                                    } else {
                                        // Offset lift (r → r+M)
                                        this.ctx.strokeStyle = point.parity === 'odd' ? 'rgba(156, 39, 176, 0.4)' : 'rgba(255, 152, 0, 0.4)';
                                        this.ctx.lineWidth = 1.5;
                                        this.ctx.setLineDash([5, 5]);
                                    }
                                    this.ctx.stroke();
                                    this.ctx.setLineDash([]);
                                });
                            }
                        });
                    }
                }
                
                // Draw points
                this.shells.forEach(shell => {
                    shell.points.forEach(point => {
                        let color;
                        if (this.config.showParity) {
                            color = point.parity === 'odd' ? '#4CAF50' : '#2196F3';
                        } else {
                            color = '#9C27B0';
                        }
                        
                        if (this.config.showDirichlet) {
                            this.ctx.beginPath();
                            this.ctx.arc(point.x, point.y, this.config.pointSize + 3, 0, 2 * Math.PI);
                            this.ctx.fillStyle = 'rgba(255, 193, 7, 0.3)';
                            this.ctx.fill();
                        }
                        
                        this.ctx.beginPath();
                        this.ctx.arc(point.x, point.y, this.config.pointSize, 0, 2 * Math.PI);
                        this.ctx.fillStyle = color;
                        this.ctx.fill();
                        this.ctx.strokeStyle = '#333';
                        this.ctx.lineWidth = 1.5;
                        this.ctx.stroke();
                        
                        if (this.config.showLabels) {
                            this.ctx.fillStyle = '#333';
                            this.ctx.font = '11px Arial';
                            this.ctx.fillText(point.residue, point.x + 10, point.y - 10);
                        }
                        
                        if (this.config.showAngles) {
                            const angleLabel = `${(point.angle * 180 / Math.PI).toFixed(1)}°`;
                            this.ctx.fillStyle = '#999';
                            this.ctx.font = '9px Arial';
                            this.ctx.fillText(angleLabel, point.x + 10, point.y + 5);
                        }
                    });
                });
                
                // Draw Farey projection
                if (this.config.showFarey) {
                    this.drawFareyProjection();
                }
            }
            
            findDirectLift(point, nextShell) {
                // Find r → r lift (direct mapping)
                const r = point.residue;
                const normalized = r % nextShell.modulus;
                return nextShell.points.find(p => p.residue === normalized);
            }
            
            findAllLifts(point, nextShell) {
                // Find both r → r and r → r+M lifts
                const lifted = [];
                const m = point.modulus;
                const r = point.residue;
                
                // Direct lift: r → r
                const directNormalized = r % nextShell.modulus;
                const directPoint = nextShell.points.find(p => p.residue === directNormalized);
                if (directPoint) lifted.push(directPoint);
                
                // Offset lift: r → r+M
                const offsetNormalized = (r + m) % nextShell.modulus;
                const offsetPoint = nextShell.points.find(p => p.residue === offsetNormalized);
                if (offsetPoint && offsetPoint !== directPoint) {
                    lifted.push(offsetPoint);
                }
                
                return lifted;
            }
            
            drawFareyProjection() {
                const y = this.canvas.height - 40;
                
                // Draw baseline
                this.ctx.beginPath();
                this.ctx.moveTo(50, y);
                this.ctx.lineTo(this.canvas.width - 50, y);
                this.ctx.strokeStyle = '#333';
                this.ctx.lineWidth = 2;
                this.ctx.stroke();
                
                // Project points
                this.shells.forEach(shell => {
                    shell.points.forEach(point => {
                        const fraction = point.residue / point.modulus;
                        const x = 50 + fraction * (this.canvas.width - 100);
                        
                        this.ctx.beginPath();
                        this.ctx.arc(x, y, 3, 0, 2 * Math.PI);
                        this.ctx.fillStyle = point.parity === 'odd' ? '#4CAF50' : '#2196F3';
                        this.ctx.fill();
                    });
                });
            }
            
            updateInfo() {
                const infoGrid = document.getElementById('infoGrid');
                infoGrid.innerHTML = '';
                
                let totalPoints = 0;
                this.shells.forEach(shell => {
                    totalPoints += shell.phi;
                    
                    const item = document.createElement('div');
                    item.className = 'info-item';
                    item.innerHTML = `
                        <strong>M = ${shell.modulus}</strong>
                        <span>φ(M) = ${shell.phi}</span>
                    `;
                    infoGrid.appendChild(item);
                });
                
                const totalItem = document.createElement('div');
                totalItem.className = 'info-item';
                totalItem.innerHTML = `
                    <strong>Total Points</strong>
                    <span>${totalPoints}</span>
                `;
                infoGrid.appendChild(totalItem);
            }
            
            update() {
                this.computeShells();
                this.draw();
                this.updateInfo();
            }
        }
        
        // Initialize
        const viz = new ModularVisualizer('mainCanvas');
        viz.update();
        
        // Event listeners
        document.getElementById('numShells').addEventListener('input', (e) => {
            document.getElementById('numShellsValue').textContent = e.target.value;
        });
        
        document.getElementById('pointSize').addEventListener('input', (e) => {
            document.getElementById('pointSizeValue').textContent = e.target.value;
        });
        
        document.getElementById('scaleFactor').addEventListener('input', (e) => {
            document.getElementById('scaleFactorValue').textContent = e.target.value;
        });
        
        document.getElementById('animationSpeed').addEventListener('input', (e) => {
            document.getElementById('animationSpeedValue').textContent = e.target.value;
        });
        
        document.getElementById('liftType').addEventListener('change', (e) => {
            const customGroup = document.getElementById('customFactorGroup');
            if (e.target.value === 'custom') {
                customGroup.style.display = 'block';
            } else {
                customGroup.style.display = 'none';
                viz.config.liftFactor = e.target.value === 'dyadic' ? 2 : 3;
            }
        });
        
        document.getElementById('updateBtn').addEventListener('click', () => {
            viz.config.baseModulus = parseInt(document.getElementById('baseModulus').value);
            viz.config.numShells = parseInt(document.getElementById('numShells').value);
            viz.config.pointSize = parseInt(document.getElementById('pointSize').value);
            viz.config.scaleFactor = parseInt(document.getElementById('scaleFactor').value);
            viz.config.showAngles = document.getElementById('showAngles').checked;
            viz.config.showLabels = document.getElementById('showLabels').checked;
            viz.config.connectionType = document.getElementById('connectionType').value;
            viz.config.showParity = document.getElementById('showParity').checked;
            viz.config.showFarey = document.getElementById('showFarey').checked;
            viz.config.showDirichlet = document.getElementById('showDirichlet').checked;
            
            const liftType = document.getElementById('liftType').value;
            if (liftType === 'custom') {
                viz.config.liftFactor = parseInt(document.getElementById('customFactor').value);
            }
            
            viz.update();
        });
        
        document.getElementById('resetBtn').addEventListener('click', () => {
            document.getElementById('baseModulus').value = 30;
            document.getElementById('numShells').value = 3;
            document.getElementById('numShellsValue').textContent = 3;
            document.getElementById('pointSize').value = 6;
            document.getElementById('pointSizeValue').textContent = 6;
            document.getElementById('scaleFactor').value = 80;
            document.getElementById('scaleFactorValue').textContent = 80;
            
            viz.config = {
                baseModulus: 30,
                numShells: 3,
                liftFactor: 2,
                pointSize: 6,
                scaleFactor: 80,
                showAngles: true,
                showLabels: true,
                connectionType: 'none',
                showParity: true,
                showFarey: false,
                showDirichlet: false
            };
            
            viz.update();
        });
        
        document.getElementById('animateBtn').addEventListener('click', () => {
            if (!viz.animating) {
                viz.animating = true;
                animateLift();
            }
        });
        
        function animateLift() {
            // Simple animation placeholder
            let frame = 0;
            const maxFrames = 60;
            
            function animate() {
                if (frame < maxFrames && viz.animating) {
                    frame++;
                    viz.draw();
                    requestAnimationFrame(animate);
                } else {
                    viz.animating = false;
                }
            }
            
            animate();
        }
    </script>
</body>
</html>
