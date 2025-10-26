<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GCD Mapping Framework - Wessen Getachew</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: Georgia, 'Times New Roman', serif; background: #ffffff; color: #1a1a1a; line-height: 1.8; }
        header { background: #2c3e50; color: #ffffff; padding: 60px 40px; border-bottom: 4px solid #34495e; text-align: center; }
        h1 { font-size: 2.8em; font-weight: 400; margin-bottom: 15px; }
        .subtitle { font-size: 1.3em; font-weight: 300; opacity: 0.9; font-style: italic; margin-bottom: 20px; }
        .author { font-size: 1.1em; opacity: 0.85; font-family: 'Segoe UI', sans-serif; }
        nav { background: #34495e; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        nav ul { list-style: none; display: flex; max-width: 1400px; margin: 0 auto; }
        nav li { flex: 1; }
        nav a { display: block; padding: 18px 20px; color: #ecf0f1; text-decoration: none; text-align: center; border-right: 1px solid rgba(255,255,255,0.1); transition: background 0.3s; font-family: 'Segoe UI', sans-serif; font-size: 0.95em; }
        nav a:hover { background: #2c3e50; }
        section { max-width: 1400px; margin: 0 auto; padding: 60px 40px; border-bottom: 1px solid #e0e0e0; }
        section:nth-child(even) { background: #f8f9fa; }
        section h2 { font-size: 2.2em; font-weight: 400; margin-bottom: 30px; color: #2c3e50; border-bottom: 3px solid #3498db; padding-bottom: 15px; }
        .viz-container { display: grid; grid-template-columns: 350px 1fr; gap: 30px; margin-top: 30px; }
        .controls { background: #f8f9fa; padding: 25px; border: 1px solid #dee2e6; height: fit-content; }
        .control-group { margin-bottom: 25px; padding-bottom: 20px; border-bottom: 1px solid #dee2e6; }
        .control-group:last-child { border-bottom: none; }
        .control-group h3 { font-size: 1.05em; margin-bottom: 15px; color: #2c3e50; font-weight: 600; font-family: 'Segoe UI', sans-serif; }
        label { display: block; margin-bottom: 8px; font-size: 0.95em; color: #495057; font-family: 'Segoe UI', sans-serif; }
        input[type="range"] { width: 100%; margin: 10px 0; height: 4px; background: #dee2e6; border-radius: 2px; outline: none; -webkit-appearance: none; }
        input[type="range"]::-webkit-slider-thumb { -webkit-appearance: none; width: 16px; height: 16px; background: #3498db; cursor: pointer; border-radius: 50%; }
        input[type="range"]::-moz-range-thumb { width: 16px; height: 16px; background: #3498db; cursor: pointer; border-radius: 50%; border: none; }
        input[type="number"], select { width: 100%; padding: 8px 12px; background: #ffffff; border: 1px solid #ced4da; border-radius: 4px; color: #495057; font-size: 0.95em; font-family: 'Segoe UI', sans-serif; }
        button { width: 100%; padding: 10px; background: #3498db; border: none; border-radius: 4px; color: #ffffff; font-size: 0.95em; font-weight: 500; cursor: pointer; transition: background 0.3s; margin-top: 10px; font-family: 'Segoe UI', sans-serif; }
        button:hover { background: #2980b9; }
        .value-display { float: right; background: #e3f2fd; color: #1976d2; padding: 2px 10px; border-radius: 3px; font-weight: 600; }
        canvas { border: 1px solid #dee2e6; box-shadow: 0 4px 12px rgba(0,0,0,0.1); background: #0a0a0f; display: block; }
        .stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; margin: 30px 0; }
        .stat-box { background: #ffffff; padding: 25px; border: 1px solid #dee2e6; border-left: 4px solid #3498db; text-align: center; }
        .stat-value { font-size: 2.5em; font-weight: 300; color: #2c3e50; }
        .stat-label { font-size: 0.95em; color: #6c757d; margin-top: 8px; }
        .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin: 25px 0; }
        .card { background: #ffffff; padding: 20px; border: 1px solid #dee2e6; border-radius: 4px; }
        .card strong { color: #2c3e50; display: block; margin-bottom: 8px; }
        .card code { background: #f8f9fa; padding: 4px 8px; border-radius: 3px; font-size: 0.9em; display: block; margin: 8px 0; }
        .theorem { background: #ffffff; padding: 30px; margin: 25px 0; border: 1px solid #dee2e6; border-left: 4px solid #3498db; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .theorem h4 { color: #2c3e50; font-size: 1.3em; margin-bottom: 20px; font-weight: 500; }
        .formula { background: #f8f9fa; padding: 15px; border-radius: 4px; font-family: 'Courier New', monospace; margin: 15px 0; border-left: 3px solid #6c757d; }
        .highlight { background: #e3f2fd; padding: 20px; border-radius: 4px; margin: 20px 0; border-left: 4px solid #2196f3; }
        .export-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        input[type="checkbox"] { width: 18px; height: 18px; margin-right: 10px; cursor: pointer; }
        .tooltip { position: fixed; background: rgba(44, 62, 80, 0.95); color: #ffffff; padding: 12px 16px; border-radius: 4px; font-size: 0.9em; pointer-events: none; display: none; z-index: 1000; box-shadow: 0 4px 12px rgba(0,0,0,0.3); font-family: 'Segoe UI', sans-serif; }
        @media (max-width: 1200px) { .viz-container { grid-template-columns: 1fr; } .stats { grid-template-columns: repeat(2, 1fr); } .grid-3 { grid-template-columns: 1fr; } }
    </style>
</head>
<body>
    <header>
        <h1>GCD Mapping Framework</h1>
        <p class="subtitle">Modular Coprimality Geometry</p>
        <p class="author">Wessen Getachew</p>
    </header>
    
    <nav>
        <ul>
            <li><a href="#visualization">Visualization</a></li>
            <li><a href="#properties">Properties</a></li>
            <li><a href="#labeling">Labeling Systems</a></li>
            <li><a href="#theory">Theory</a></li>
        </ul>
    </nav>
    
    <section id="visualization">
        <h2>Interactive Visualization</h2>
        <p style="max-width: 900px; margin-bottom: 30px; color: #495057;">
            Explore the geometric structure of modular coprimality. Each residue <em>r ∈ {1,2,...,m}</em> 
            is mapped to angular position <em>θ = 2πr/m</em>, colored by <em>gcd(r,m)</em>.
        </p>
        
        <div class="viz-container">
            <div class="controls">
                <div class="control-group">
                    <h3>Modulus Settings</h3>
                    <label>Modulus (m): <span class="value-display" id="modulusValue">30</span></label>
                    <input type="range" id="modulusSlider" min="3" max="1000" value="30">
                    <input type="number" id="modulusInput" min="3" max="10000" value="30">
                </div>
                
                <div class="control-group">
                    <h3>Visualization Mode</h3>
                    <select id="vizMode">
                        <option value="unit">Unit Circle</option>
                        <option value="concentric">Concentric Rings</option>
                        <option value="nested">Nested Modular</option>
                        <option value="spiral">Logarithmic Spiral</option>
                    </select>
                </div>
                
                <div class="control-group">
                    <h3>Color Scheme</h3>
                    <select id="colorScheme">
                        <option value="classic">Classic</option>
                        <option value="rainbow">Rainbow</option>
                        <option value="heat">Heat Map</option>
                        <option value="ocean">Ocean</option>
                        <option value="sunset">Sunset</option>
                        <option value="neon">Neon</option>
                        <option value="forest">Forest</option>
                        <option value="monochrome">Monochrome</option>
                        <option value="pastel">Pastel</option>
                        <option value="fire">Fire & Ice</option>
                        <option value="cyberpunk">Cyberpunk</option>
                        <option value="galaxy">Galaxy</option>
                        <option value="earth">Earth</option>
                        <option value="aurora">Aurora</option>
                        <option value="copper">Copper</option>
                    </select>
                </div>
                
                <div class="control-group">
                    <h3>Global Rotation</h3>
                    <label>Angle: <span class="value-display" id="rotationValue">0°</span></label>
                    <input type="range" id="rotationAngle" min="0" max="360" value="0">
                    <label>Speed: <span class="value-display" id="rotationSpeedValue">0</span></label>
                    <input type="range" id="rotationSpeed" min="-100" max="100" value="0">
                    <label><input type="checkbox" id="rotateOuterIn"> Outer to Inner</label>
                    <label><input type="checkbox" id="rotateInnerOut"> Inner to Outer</label>
                    <button id="startRotation">Start Rotation</button>
                    <button id="stopRotation">Stop</button>
                    <button id="resetRotation">Reset</button>
                </div>
                
                <div class="control-group">
                    <h3>Point Styling</h3>
                    <label>Size: <span class="value-display" id="pointSizeValue">6</span></label>
                    <input type="range" id="pointSize" min="1" max="20" value="6">
                    <label>GCD=1 Opacity: <span class="value-display" id="gcd1OpacityValue">100%</span></label>
                    <input type="range" id="gcd1Opacity" min="10" max="100" value="100">
                    <label>GCD>1 Opacity: <span class="value-display" id="gcdNOpacityValue">80%</span></label>
                    <input type="range" id="gcdNOpacity" min="10" max="100" value="80">
                </div>
                
                <div class="control-group">
                    <h3>Labeling System</h3>
                    <select id="labelingSystem">
                        <option value="none">No Labels</option>
                        <option value="arithmetic">Arithmetic: gcd(r,m)</option>
                        <option value="farey">Farey Fraction</option>
                        <option value="theta">Theta: θ=2πr/m</option>
                        <option value="rootUnity">Root of Unity</option>
                        <option value="reducedMod">Reduced Modulus</option>
                        <option value="totient">Totient Shell</option>
                        <option value="fareyTheta">Farey-Theta</option>
                        <option value="character">Dirichlet Character</option>
                        <option value="divisor">Divisor Network</option>
                        <option value="analytic">Analytic Form</option>
                    </select>
                    <label>Label Size: <span class="value-display" id="labelSizeValue">10</span></label>
                    <input type="range" id="labelSize" min="6" max="20" value="10">
                </div>
                
                <div class="control-group">
                    <h3>Visual Effects</h3>
                    <label><input type="checkbox" id="showConnections"> Connect GCD=1</label>
                    <label><input type="checkbox" id="showGrid"> Show Grid</label>
                    <label><input type="checkbox" id="glowEffect" checked> Glow Effect</label>
                </div>
                
                <div class="control-group">
                    <h3>Export</h3>
                    <div class="export-grid">
                        <button onclick="exportImage(1920,1080)">HD</button>
                        <button onclick="exportImage(2560,1440)">QHD</button>
                        <button onclick="exportImage(3840,2160)">4K</button>
                        <button onclick="exportImage(7680,4320)">8K</button>
                    </div>
                    <button onclick="exportImage(0,0)">Export Current</button>
                </div>
            </div>
            
            <div>
                <canvas id="gcdCanvas" width="900" height="900"></canvas>
            </div>
        </div>
    </section>
    
    <section id="properties">
        <h2>Mathematical Properties</h2>
        <div class="stats">
            <div class="stat-box">
                <div class="stat-value" id="phiValue">8</div>
                <div class="stat-label">Euler's φ(m)</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="gcd1Count">8</div>
                <div class="stat-label">GCD = 1 Points</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="totalPoints">30</div>
                <div class="stat-label">Total Points</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="coprimeRatio">26.7%</div>
                <div class="stat-label">Coprime Ratio</div>
            </div>
        </div>
    </section>
    
    <section id="labeling">
        <h2>Advanced Labeling Systems</h2>
        <p style="max-width: 1000px; margin-bottom: 30px; color: #495057;">
            Each residue can be labeled through multiple mathematical lenses, transforming the GCD map 
            from simple arithmetic into a multi-layered harmonic field.
        </p>
        <div class="grid-3">
            <div class="card"><strong>1. Arithmetic Base</strong><code>gcd(r,m)</code><small style="color: #6c757d;">Raw divisibility structure</small></div>
            <div class="card"><strong>2. Farey Fraction</strong><code>(r/gcd)/(m/gcd) = a/b</code><small style="color: #6c757d;">Reduced rational geometry</small></div>
            <div class="card"><strong>3. Theta</strong><code>θ = 2πr/m</code><small style="color: #6c757d;">Angular harmonic</small></div>
            <div class="card"><strong>4. Root-of-Unity</strong><code>e^(i·2π(r/gcd)/(m/gcd))</code><small style="color: #6c757d;">Cyclotomic subsystem</small></div>
            <div class="card"><strong>5. Reduced Modulus</strong><code>m' = m/gcd(r,m)</code><small style="color: #6c757d;">Nested modular universe</small></div>
            <div class="card"><strong>6. Totient Shell</strong><code>φ(m/gcd)</code><small style="color: #6c757d;">Local coprime density</small></div>
            <div class="card"><strong>7. Farey-Theta</strong><code>2πa/b</code><small style="color: #6c757d;">Rational angular mapping</small></div>
            <div class="card"><strong>8. Dirichlet Character</strong><code>χ(r) = e^(i·2πkr/m)</code><small style="color: #6c757d;">Multiplicative field</small></div>
            <div class="card"><strong>9. Divisor Network</strong><code>Lattice position</code><small style="color: #6c757d;">Inclusion hierarchy</small></div>
            <div class="card"><strong>10. Analytic Form</strong><code>ζ(gcd^(-s))</code><small style="color: #6c757d;">Zeta resonance</small></div>
        </div>
    </section>
    
    <section id="theory">
        <h2>Theoretical Framework</h2>
        
        <div class="theorem">
            <h4>Theorem: Prime Persistence on Mod 1 Revalue Channels</h4>
            <p><strong>Definition.</strong> Let 𝓜 = {1,2,3,...}. For each modulus M, define reduced residue channels:</p>
            <div class="formula">Φ(M) = { a/M | 1 ≤ a < M, gcd(a,M) = 1 }</div>
            <p>Each maps to rotational channel: θ<sub>a,M</sub> = 2πa/M</p>
            <p><strong>Mod 1 Revalue Channel.</strong> Under compression to mod 1, the invariant channel is:</p>
            <div class="formula">𝓒₀ = { 0/M | M ≥ 1 }</div>
            <p>As M → ∞, channels approach continuum [0,1), but only 0/n alignments preserve coherent phase.</p>
            <div class="highlight">
                <strong>Core Theorem:</strong> For any prime p ∈ ℙ:
                <div style="margin: 10px 0; font-family: 'Courier New', monospace;">p mod 1 = 0</div>
                Therefore p remains aligned only along invariant channel 𝓒₀. All composite residues destructively interfere.
                <div style="margin-top: 15px; font-weight: 600;">Prime existence ⟺ persistence on Mod 1 Revalue Channel</div>
            </div>
            <p><strong>Geometric Interpretation:</strong></p>
            <ul style="margin-left: 25px; color: #495057;">
                <li>Each modulus M defines a ring with φ(M) active nodes</li>
                <li>𝓒₀ is central alignment axis where all rings intersect at θ = 0</li>
                <li>Only primes maintain full alignment along 𝓒₀</li>
                <li>Non-primes form dense interference background</li>
            </ul>
            <p style="margin-top: 20px;"><strong>Analytic Connection:</strong> Mirrors Riemann zeta:</p>
            <div class="formula">ζ(s) = ∏<sub>p∈ℙ</sub> (1 - p<sup>-s</sup>)<sup>-1</sup></div>
        </div>
        
        <div class="theorem">
            <h4>Theorem: Coprime Uniqueness of Primes</h4>
            <p>For prime p, the reduced residue system is:</p>
            <div class="formula">Φ(p) = {1, 2, ..., p-1}</div>
            <p>Every element of Φ(p) is coprime to p.</p>
            <div class="highlight">
                <strong>Core Theorem:</strong> Each prime p defines unique coprime structure:
                <div style="margin: 10px 0; font-family: 'Courier New', monospace;">p·a mod p² ∈ Orbit(p), ∀a ∈ Φ(p)</div>
                No other prime q ≠ p can reproduce this orbit. Coprimality structure is self-originating and non-interchangeable.
            </div>
            <p><strong>Corollary:</strong> For distinct primes p and q:</p>
            <div class="formula">Φ(pq) = Φ(p) × Φ(q)</div>
            <p>Composite moduli are tensor products of prime coprime channels.</p>
        </div>
        
        <div class="theorem">
            <h4>Theorem: Semiprime Generation from Prime Coprime Orbits</h4>
            <p>For prime p ∈ ℙ, define prime coprime subset:</p>
            <div class="formula">Φₚ = { q ∈ ℙ | q ≠ p }</div>
            <p>The semiprime set generated by p:</p>
            <div class="formula">Sₚ = { p × q | q ∈ Φₚ }</div>
            <div class="highlight">
                <strong>Core Theorem:</strong> Every semiprime n is uniquely:
                <div style="margin: 10px 0; font-family: 'Courier New', monospace;">n = p × q, where p,q ∈ ℙ, p ≤ q</div>
                Therefore:
                <div style="margin: 10px 0; font-family: 'Courier New', monospace;">⋃<sub>p∈ℙ</sub> Sₚ = {all semiprimes}</div>
            </div>
            <p><strong>Geometric Interpretation:</strong></p>
            <ul style="margin-left: 25px; color: #495057;">
                <li>Each prime p defines pure coprime orbit (Φ(p) ring)</li>
                <li>Multiplying by prime q creates intersection between orbits</li>
                <li>Intersections are semiprimes—minimal cross-links between prime channels</li>
            </ul>
            <p style="margin-top: 20px; font-weight: 600;">
                Semiprimes represent first layer of composite structure: pairwise interactions of two prime systems.
            </p>
        </div>
        
        <p style="color: #6c757d; margin-top: 40px; font-style: italic; text-align: center;">
            These theorems establish primes as the persistent modular backbone of the number system—
            phase-coherent anchors surviving all revaluation, with semiprimes forming the first 
            structural bridge between distinct prime coprime universes.
        </p>
    </section>
    
    <div class="tooltip" id="tooltip"></div>
    
    <script>
        const canvas = document.getElementById('gcdCanvas');
        let ctx = canvas.getContext('2d');
        let globalRotation = 0, isRotating = false, rotationAnimationId = null;
        
        const colorSchemes = {
            classic: { gcd1: '#3498db', gcdN: (gcd) => ['#e74c3c', '#2ecc71', '#f39c12', '#9b59b6', '#1abc9c'][(gcd-2)%5] },
            rainbow: { gcd1: '#FF0080', gcdN: (gcd) => `hsl(${(gcd*40)%360}, 85%, 60%)` },
            heat: { gcd1: '#00ffff', gcdN: (gcd) => { const i = Math.min(gcd/10,1); return `rgb(${255*i}, ${100*(1-i)}, ${50*(1-i)})`; } },
            ocean: { gcd1: '#00d4ff', gcdN: (gcd) => { const d = Math.min(gcd/8,1); return `rgb(${20*(1-d)}, ${100+100*(1-d)}, ${200+55*(1-d)})`; } },
            sunset: { gcd1: '#ff6b6b', gcdN: (gcd) => ['#ff8c42', '#ffa07a', '#ee6c4d', '#c1666b', '#9b4f96'][(gcd-2)%5] },
            neon: { gcd1: '#0ff', gcdN: (gcd) => ['#f0f', '#ff0', '#0f0', '#f00', '#00f', '#f80'][(gcd-2)%6] },
            forest: { gcd1: '#52c234', gcdN: (gcd) => ['#2d6a4f', '#40916c', '#52b788', '#74c69d', '#95d5b2'][(gcd-2)%5] },
            monochrome: { gcd1: '#ffffff', gcdN: (gcd) => { const i = 255-(gcd*25); return `rgb(${i}, ${i}, ${i})`; } },
            pastel: { gcd1: '#a8dadc', gcdN: (gcd) => ['#f1faee', '#e63946', '#457b9d', '#f4a261', '#e9c46a'][(gcd-2)%5] },
            fire: { gcd1: '#00f5ff', gcdN: (gcd) => ['#ff6b35', '#f7931e', '#fdc830', '#f37335', '#c0392b'][(gcd-2)%5] },
            cyberpunk: { gcd1: '#00fff9', gcdN: (gcd) => ['#ff00ff', '#ff0099', '#9d00ff', '#ff3300', '#00ff00'][(gcd-2)%5] },
            galaxy: { gcd1: '#e0aaff', gcdN: (gcd) => ['#c77dff', '#9d4edd', '#7209b7', '#560bad', '#3c096c'][(gcd-2)%5] },
            earth: { gcd1: '#8b4513', gcdN: (gcd) => ['#a0522d', '#daa520', '#cd853f', '#d2691e', '#b8860b'][(gcd-2)%5] },
            aurora: { gcd1: '#b8f3ff', gcdN: (gcd) => ['#72efdd', '#64dfdf', '#48bfe3', '#5390d9', '#6930c3'][(gcd-2)%5] },
            copper: { gcd1: '#ffd700', gcdN: (gcd) => ['#cd7f32', '#b87333', '#daa520', '#ff8c00', '#d4af37'][(gcd-2)%5] }
        };
        
        function gcd(a, b) { while (b !== 0) { let temp = b; b = a % b; a = temp; } return a; }
        function eulerPhi(n) { let result = 0; for (let i = 1; i <= n; i++) { if (gcd(i, n) === 1) result++; } return result; }
        function getColor(gcdValue, scheme) { const colors = colorSchemes[scheme]; return gcdValue === 1 ? colors.gcd1 : colors.gcdN(gcdValue); }
        function fareyFraction(r, m) { const g = gcd(r, m); return { numerator: r / g, denominator: m / g }; }
        
        function getLabel(r, m, system) {
            const g = gcd(r, m);
            switch(system) {
                case 'none': return null;
                case 'arithmetic': return g.toString();
                case 'farey': const f = fareyFraction(r, m); return `${f.numerator}/${f.denominator}`;
                case 'theta': return `${((2*Math.PI*r)/m).toFixed(2)}`;
                case 'rootUnity': const phase = (2*Math.PI*(r/g))/(m/g); return `e^{i${phase.toFixed(2)}}`;
                case 'reducedMod': return `${m/g}`;
                case 'totient': return `φ=${eulerPhi(m/g)}`;
                case 'fareyTheta': const ft = fareyFraction(r, m); return `${((2*Math.PI*ft.numerator)/ft.denominator).toFixed(2)}`;
                case 'character': return g === 1 ? `χ=${((2*Math.PI*r)/m).toFixed(1)}` : '0';
                case 'divisor': let dc = 0; for (let d = 1; d <= m; d++) { if (m % d === 0 && g % d === 0) dc++; } return `L${dc}`;
                case 'analytic': return `${(1/Math.pow(g, 2)).toFixed(3)}`;
                default: return null;
            }
        }
        
        function draw() {
            const m = parseInt(document.getElementById('modulusSlider').value);
            const mode = document.getElementById('vizMode').value;
            const scheme = document.getElementById('colorScheme').value;
            const pointSize = parseInt(document.getElementById('pointSize').value);
            const gcd1Opacity = parseInt(document.getElementById('gcd1Opacity').value) / 100;
            const gcdNOpacity = parseInt(document.getElementById('gcdNOpacity').value) / 100;
            const showConnections = document.getElementById('showConnections').checked;
            const showGrid = document.getElementById('showGrid').checked;
            const labelingSystem = document.getElementById('labelingSystem').value;
            const labelSize = parseInt(document.getElementById('labelSize').value);
            const glowEffect = document.getElementById('glowEffect').checked;
            const rotateOuterIn = document.getElementById('rotateOuterIn').checked;
            const rotateInnerOut = document.getElementById('rotateInnerOut').checked;
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const maxRadius = Math.min(centerX, centerY) * 0.85;
            
            ctx.fillStyle = '#0a0a0f';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            if (showGrid) {
                ctx.strokeStyle = 'rgba(255, 255, 255, 0.1)';
                ctx.lineWidth = 1;
                for (let i = 1; i <= 5; i++) { ctx.beginPath(); ctx.arc(centerX, centerY, (maxRadius / 5) * i, 0, 2 * Math.PI); ctx.stroke(); }
                for (let i = 0; i < 12; i++) { const angle = (i * Math.PI) / 6; ctx.beginPath(); ctx.moveTo(centerX, centerY); ctx.lineTo(centerX + maxRadius * Math.cos(angle), centerY + maxRadius * Math.sin(angle)); ctx.stroke(); }
            }
            
            const points = [];
            for (let r = 1; r <= m; r++) {
                const g = gcd(r, m);
                let theta = (2 * Math.PI * r) / m;
                let radius = mode === 'unit' ? maxRadius : mode === 'concentric' ? maxRadius * (g / m) : maxRadius * (r / m);
                const radiusRatio = radius / maxRadius;
                let rotationOffset = globalRotation * Math.PI / 180;
                if (rotateOuterIn) rotationOffset *= radiusRatio;
                else if (rotateInnerOut) rotationOffset *= (1 - radiusRatio);
                theta += rotationOffset;
                const x = centerX + radius * Math.cos(theta - Math.PI / 2);
                const y = centerY + radius * Math.sin(theta - Math.PI / 2);
                points.push({ x, y, gcd: g, r, m, theta });
            }
            
            if (showConnections) {
                const gcd1Points = points.filter(p => p.gcd === 1);
                ctx.strokeStyle = 'rgba(102, 126, 234, 0.2)';
                ctx.lineWidth = 1;
                for (let i = 0; i < gcd1Points.length; i++) {
                    const next = (i + 1) % gcd1Points.length;
                    ctx.beginPath(); ctx.moveTo(gcd1Points[i].x, gcd1Points[i].y); ctx.lineTo(gcd1Points[next].x, gcd1Points[next].y); ctx.stroke();
                }
            }
            
            points.forEach(point => {
                const color = getColor(point.gcd, scheme);
                const opacity = point.gcd === 1 ? gcd1Opacity : gcdNOpacity;
                if (glowEffect) { ctx.shadowBlur = pointSize * 2; ctx.shadowColor = color; }
                ctx.fillStyle = color; ctx.globalAlpha = opacity;
                ctx.beginPath(); ctx.arc(point.x, point.y, pointSize, 0, 2 * Math.PI); ctx.fill();
                
                if (labelingSystem !== 'none') {
                    const label = getLabel(point.r, point.m, labelingSystem);
                    if (label) {
                        ctx.shadowBlur = 0; ctx.fillStyle = '#fff'; ctx.globalAlpha = 0.8;
                        ctx.font = `${labelSize}px Arial`; ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
                        const metrics = ctx.measureText(label);
                        ctx.fillStyle = 'rgba(0, 0, 0, 0.7)'; ctx.globalAlpha = 0.7;
                        ctx.fillRect(point.x - metrics.width/2 - 3, point.y - pointSize - labelSize - 5, metrics.width + 6, labelSize + 4);
                        ctx.fillStyle = '#fff'; ctx.globalAlpha = 0.9;
                        ctx.fillText(label, point.x, point.y - pointSize - labelSize/2 - 3);
                    }
                }
            });
            ctx.shadowBlur = 0; ctx.globalAlpha = 1;
            updateStats(m);
        }
        
        function updateStats(m) {
            const phi = eulerPhi(m);
            let gcd1Count = 0;
            for (let r = 1; r <= m; r++) { if (gcd(r, m) === 1) gcd1Count++; }
            document.getElementById('phiValue').textContent = phi;
            document.getElementById('gcd1Count').textContent = gcd1Count;
            document.getElementById('totalPoints').textContent = m;
            document.getElementById('coprimeRatio').textContent = ((gcd1Count / m) * 100).toFixed(1) + '%';
        }
        
        function startRotation() { if (isRotating) return; isRotating = true; rotateLoop(); }
        function stopRotation() { isRotating = false; if (rotationAnimationId) { cancelAnimationFrame(rotationAnimationId); rotationAnimationId = null; } }
        function rotateLoop() {
            if (!isRotating) return;
            const speed = parseInt(document.getElementById('rotationSpeed').value);
            globalRotation += speed * 0.1;
            if (globalRotation >= 360) globalRotation -= 360;
            if (globalRotation < 0) globalRotation += 360;
            document.getElementById('rotationAngle').value = Math.round(globalRotation);
            document.getElementById('rotationValue').textContent = Math.round(globalRotation) + '°';
            draw();
            rotationAnimationId = requestAnimationFrame(rotateLoop);
        }
        function resetRotation() { stopRotation(); globalRotation = 0; document.getElementById('rotationAngle').value = 0; document.getElementById('rotationValue').textContent = '0°'; draw(); }
        
        function exportImage(width, height) {
            stopRotation();
            const originalWidth = canvas.width, originalHeight = canvas.height;
            if (width === 0 || height === 0) { width = originalWidth; height = originalHeight; }
            const exportCanvas = document.createElement('canvas');
            exportCanvas.width = width; exportCanvas.height = height;
            const tempCtx = ctx;
            ctx = exportCanvas.getContext('2d');
            canvas.width = width; canvas.height = height;
            draw();
            exportCanvas.toBlob((blob) => {
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url; a.download = `gcd_mapping_${width}x${height}_${Date.now()}.jpg`; a.click();
                URL.revokeObjectURL(url);
                canvas.width = originalWidth; canvas.height = originalHeight;
                ctx = tempCtx; draw();
            }, 'image/jpeg', 0.98);
        }
        
        canvas.addEventListener('mousemove', (e) => {
            const rect = canvas.getBoundingClientRect();
            const x = (e.clientX - rect.left) * (canvas.width / rect.width);
            const y = (e.clientY - rect.top) * (canvas.height / rect.height);
            const m = parseInt(document.getElementById('modulusSlider').value);
            const centerX = canvas.width / 2, centerY = canvas.height / 2;
            const maxRadius = Math.min(centerX, centerY) * 0.85;
            const tooltip = document.getElementById('tooltip');
            let found = false;
            for (let r = 1; r <= m; r++) {
                const g = gcd(r, m), theta = (2 * Math.PI * r) / m;
                const mode = document.getElementById('vizMode').value;
                let radius = mode === 'unit' ? maxRadius : mode === 'concentric' ? maxRadius * (g / m) : maxRadius * (r / m);
                const px = centerX + radius * Math.cos(theta - Math.PI / 2), py = centerY + radius * Math.sin(theta - Math.PI / 2);
                if (Math.sqrt((x - px) ** 2 + (y - py) ** 2) < 15) {
                    tooltip.style.display = 'block'; tooltip.style.left = e.clientX + 15 + 'px'; tooltip.style.top = e.clientY + 15 + 'px';
                    tooltip.innerHTML = `<strong>r = ${r}, m = ${m}</strong><br>gcd(${r}, ${m}) = ${g}<br>θ = ${(theta * 180 / Math.PI).toFixed(1)}°<br>${g === 1 ? '<em style="color: #52c234;">✓ Coprime</em>' : '<em style="color: #e74c3c;">✗ Composite</em>'}`;
                    found = true; break;
                }
            }
            if (!found) tooltip.style.display = 'none';
        });
        canvas.addEventListener('mouseleave', () => { document.getElementById('tooltip').style.display = 'none'; });
        
        document.getElementById('modulusSlider').addEventListener('input', (e) => { const value = e.target.value; document.getElementById('modulusInput').value = value; document.getElementById('modulusValue').textContent = value; draw(); });
        document.getElementById('modulusInput').addEventListener('input', (e) => { const value = Math.min(10000, Math.max(3, parseInt(e.target.value) || 3)); e.target.value = value; if (value <= 1000) document.getElementById('modulusSlider').value = value; document.getElementById('modulusValue').textContent = value; draw(); });
        document.getElementById('vizMode').addEventListener('change', draw);
        document.getElementById('colorScheme').addEventListener('change', draw);
        document.getElementById('pointSize').addEventListener('input', (e) => { document.getElementById('pointSizeValue').textContent = e.target.value; draw(); });
        document.getElementById('gcd1Opacity').addEventListener('input', (e) => { document.getElementById('gcd1OpacityValue').textContent = e.target.value + '%'; draw(); });
        document.getElementById('gcdNOpacity').addEventListener('input', (e) => { document.getElementById('gcdNOpacityValue').textContent = e.target.value + '%'; draw(); });
        document.getElementById('showConnections').addEventListener('change', draw);
        document.getElementById('showGrid').addEventListener('change', draw);
        document.getElementById('glowEffect').addEventListener('change', draw);
        document.getElementById('labelingSystem').addEventListener('change', draw);
        document.getElementById('labelSize').addEventListener('input', (e) => { document.getElementById('labelSizeValue').textContent = e.target.value; draw(); });
        document.getElementById('rotationAngle').addEventListener('input', (e) => { globalRotation = parseFloat(e.target.value); document.getElementById('rotationValue').textContent = Math.round(globalRotation) + '°'; draw(); });
        document.getElementById('rotationSpeed').addEventListener('input', (e) => { document.getElementById('rotationSpeedValue').textContent = e.target.value; });
        document.getElementById('rotateOuterIn').addEventListener('change', (e) => { if (e.target.checked) document.getElementById('rotateInnerOut').checked = false; draw(); });
        document.getElementById('rotateInnerOut').addEventListener('change', (e) => { if (e.target.checked) document.getElementById('rotateOuterIn').checked = false; draw(); });
        document.getElementById('startRotation').addEventListener('click', startRotation);
        document.getElementById('stopRotation').addEventListener('click', stopRotation);
        document.getElementById('resetRotation').addEventListener('click', resetRotation);
        
        draw();
    </script>
</body>
</html>
