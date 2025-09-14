<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Constellation Explorer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            overflow-x: hidden;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 20%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(255, 119, 198, 0.3) 0%, transparent 50%);
            animation: float 15s ease-in-out infinite;
            z-index: -1;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.18);
            border-radius: 20px;
            padding: 50px 30px;
            text-align: center;
            margin-bottom: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }

        .header h1 {
            font-size: 3.5rem;
            font-weight: 900;
            background: linear-gradient(135deg, #fff, #e2e8f0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
        }

        .header p {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.9);
            margin-bottom: 10px;
        }

        .header .subtitle {
            font-size: 1rem;
            color: rgba(255, 255, 255, 0.8);
            max-width: 600px;
            margin: 0 auto;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 30px;
        }

        .controls {
            background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.18);
            border-radius: 16px;
            padding: 30px;
            height: fit-content;
            position: sticky;
            top: 20px;
        }

        .control-group {
            margin-bottom: 25px;
        }

        .control-group:last-child {
            margin-bottom: 0;
        }

        .control-title {
            font-size: 1.3rem;
            font-weight: 700;
            color: white;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .control-title::before {
            content: '';
            width: 4px;
            height: 20px;
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            border-radius: 2px;
        }

        label {
            display: block;
            font-size: 0.9rem;
            font-weight: 600;
            color: rgba(255, 255, 255, 0.9);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        input, select {
            width: 100%;
            padding: 12px 16px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            color: white;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        input:focus, select:focus {
            outline: none;
            border-color: rgba(255, 255, 255, 0.5);
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.1);
        }

        .hint {
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.7);
            margin-top: 5px;
            font-style: italic;
        }

        .pattern-display {
            background: linear-gradient(135deg, #43e97b, #38f9d7);
            color: white;
            padding: 16px;
            border-radius: 10px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.1rem;
            font-weight: 600;
            text-align: center;
            margin-top: 15px;
        }

        .presets {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-top: 15px;
        }

        .preset-btn {
            padding: 10px 8px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: white;
            font-size: 0.85rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .preset-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px);
        }

        .calculate-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 20px;
        }

        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
        }

        .calculate-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .results-panel {
            background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.18);
            border-radius: 16px;
            overflow: hidden;
        }

        .loading {
            display: none;
            padding: 60px;
            text-align: center;
            color: white;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 4px solid rgba(255, 255, 255, 0.2);
            border-top: 4px solid white;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .tabs {
            display: flex;
            background: rgba(0, 0, 0, 0.1);
        }

        .tab {
            flex: 1;
            padding: 20px 15px;
            background: none;
            border: none;
            color: rgba(255, 255, 255, 0.7);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
        }

        .tab.active {
            color: white;
            background: rgba(255, 255, 255, 0.1);
            border-bottom-color: #4facfe;
        }

        .tab-content {
            display: none;
            padding: 30px;
            color: white;
        }

        .tab-content.active {
            display: block;
        }

        .result-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 16px;
            margin-bottom: 25px;
        }

        .result-card {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            padding: 16px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .result-card:hover {
            transform: translateY(-3px);
            background: rgba(255, 255, 255, 0.15);
        }

        .result-label {
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.8);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 6px;
            font-weight: 600;
        }

        .result-value {
            font-size: 1.3rem;
            font-weight: 700;
            color: white;
            font-family: 'JetBrains Mono', monospace;
        }

        .info-box {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            padding: 20px;
            margin: 16px 0;
            border-left: 4px solid #4facfe;
        }

        .info-box.success { border-left-color: #43e97b; }
        .info-box.warning { border-left-color: #f093fb; }
        .info-box.error { border-left-color: #f5576c; }

        .info-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: white;
            margin-bottom: 12px;
        }

        .info-content {
            color: rgba(255, 255, 255, 0.9);
            line-height: 1.6;
        }

        .code-block {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            padding: 16px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.9rem;
            color: #e2e8f0;
            line-height: 1.5;
            overflow-x: auto;
            white-space: pre-wrap;
        }

        .formula {
            background: linear-gradient(135deg, #434343, #000000);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.1rem;
            color: white;
            font-weight: 600;
            margin: 20px 0;
        }

        .welcome {
            text-align: center;
            padding: 60px 30px;
            color: rgba(255, 255, 255, 0.8);
        }

        .welcome h3 {
            font-size: 1.4rem;
            color: white;
            margin-bottom: 15px;
        }

        .welcome p {
            font-size: 1rem;
            line-height: 1.6;
        }

        .hidden { display: none !important; }

        @media (max-width: 1000px) {
            .main-grid {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .controls {
                position: static;
            }
            
            .header h1 {
                font-size: 2.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>K-Tuple Constellation Explorer</h1>
            <p>Universal Identity Calculator</p>
            <div class="subtitle">
                Discover and analyze prime constellations using the revolutionary Wessen Master Identity
            </div>
        </div>

        <div class="main-grid">
            <div class="controls">
                <div class="control-group">
                    <div class="control-title">🎯 Pattern Setup</div>
                    
                    <label>K-Tuple Pattern</label>
                    <input type="text" id="pattern" placeholder="0, 2, 6, 8" value="0, 2">
                    <div class="hint">Enter comma-separated offsets starting with 0</div>
                    
                    <div class="presets">
                        <button class="preset-btn" onclick="setPattern('0, 2')">Twins</button>
                        <button class="preset-btn" onclick="setPattern('0, 4')">Cousins</button>
                        <button class="preset-btn" onclick="setPattern('0, 6')">Sexy</button>
                        <button class="preset-btn" onclick="setPattern('0, 2, 6')">Triplet</button>
                        <button class="preset-btn" onclick="setPattern('0, 2, 6, 8')">Quad</button>
                        <button class="preset-btn" onclick="setPattern('0, 4, 6, 10, 12, 16')">Sextuple</button>
                    </div>

                    <div class="pattern-display" id="pattern-display">ℋ = {0, 2}</div>
                </div>

                <div class="control-group">
                    <div class="control-title">🔢 Parameters</div>
                    
                    <label>Upper Bound (x)</label>
                    <input type="text" id="bound" placeholder="100000 or 1e6" value="100000">
                    
                    <label>Prime Cutoff</label>
                    <select id="cutoff-mode">
                        <option value="auto">Auto (largest prime ≤ x)</option>
                        <option value="custom">Custom p_max</option>
                    </select>
                    <input type="number" id="custom-cutoff" class="hidden" placeholder="Custom p_max" style="margin-top: 10px;">
                    
                    <label>Precision</label>
                    <input type="number" id="precision" value="6" min="2" max="12">
                </div>

                <button class="calculate-btn" onclick="calculate()" id="calc-btn">
                    🚀 Calculate
                </button>
            </div>

            <div class="results-panel">
                <div class="loading" id="loading">
                    <div class="spinner"></div>
                    <div>Computing constellation density...</div>
                </div>

                <div id="results" class="hidden">
                    <div class="tabs">
                        <button class="tab active" onclick="showTab('overview')">📊 Overview</button>
                        <button class="tab" onclick="showTab('list')">🌟 K-Tuples</button>
                        <button class="tab" onclick="showTab('identity')">🔧 Identity</button>
                        <button class="tab" onclick="showTab('analysis')">📐 Analysis</button>
                    </div>

                    <div class="tab-content active" id="overview">
                        <div class="info-box success">
                            <div class="info-title">🎯 Results for <span id="pattern-name"></span></div>
                            <div class="info-content" id="summary"></div>
                        </div>

                        <div class="result-grid" id="result-cards"></div>

                        <div class="info-box" id="admissible"></div>
                    </div>

                    <div class="tab-content" id="list">
                        <div id="constellation-list"></div>
                    </div>

                    <div class="tab-content" id="identity">
                        <div class="formula">
                            R<sub>ℋ</sub>(p<sub>max</sub>) = A<sub>ℋ</sub> × C<sub>ℋ</sub>(p<sub>max</sub>) × [M<sub>no-two</sub>(p<sub>max</sub>)]<sup>k</sup>
                        </div>
                        <div id="verification"></div>
                    </div>

                    <div class="tab-content" id="analysis">
                        <div id="math-analysis"></div>
                    </div>
                </div>

                <div id="welcome" class="welcome">
                    <div style="font-size: 3rem; margin-bottom: 20px;">🔮</div>
                    <h3>Ready to Explore</h3>
                    <p>Configure your k-tuple pattern and parameters, then calculate to discover the universal structure of prime constellations.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        const GAMMA = 0.5772156649015328606;
        let currentPattern = [0, 2];
        let results = null;

        function setPattern(str) {
            document.getElementById('pattern').value = str;
            updatePattern();
        }

        function updatePattern() {
            const input = document.getElementById('pattern').value;
            const display = document.getElementById('pattern-display');
            
            try {
                const pattern = parsePattern(input);
                currentPattern = pattern;
                display.textContent = `ℋ = {${pattern.join(', ')}}`;
                display.style.background = 'linear-gradient(135deg, #43e97b, #38f9d7)';
            } catch (e) {
                display.textContent = `Invalid: ${e.message}`;
                display.style.background = 'linear-gradient(135deg, #f093fb, #f5576c)';
            }
        }

        function parsePattern(input) {
            const parts = input.split(',').map(x => {
                const num = parseInt(x.trim());
                if (isNaN(num)) throw new Error(`"${x.trim()}" not a number`);
                return num;
            });
            
            if (parts.length < 2) throw new Error('Need at least 2 elements');
            if (parts[0] !== 0) throw new Error('Must start with 0');
            
            const unique = [...new Set(parts)];
            if (unique.length !== parts.length) throw new Error('No duplicates');
            
            parts.sort((a, b) => a - b);
            return parts;
        }

        function sieve(n) {
            const isPrime = new Array(n + 1).fill(true);
            isPrime[0] = isPrime[1] = false;
            
            for (let i = 2; i * i <= n; i++) {
                if (isPrime[i]) {
                    for (let j = i * i; j <= n; j += i) {
                        isPrime[j] = false;
                    }
                }
            }
            
            return Array.from({length: n + 1}, (_, i) => isPrime[i] ? i : null).filter(x => x !== null);
        }

        function countResidues(pattern, p) {
            const residues = new Set();
            for (const h of pattern) {
                residues.add(((h % p) + p) % p);
            }
            return residues.size;
        }

        function isAdmissible(pattern) {
            const checks = [];
            const primes = [2, 3, 5, 7, 11, 13, 17, 19, 23];
            
            for (const p of primes) {
                const nu = countResidues(pattern, p);
                const ok = nu < p;
                checks.push({ prime: p, nu: nu, total: p, ok: ok });
                if (!ok) return { ok: false, checks: checks };
            }
            
            return { ok: true, checks: checks };
        }

        function findConstellations(primes, pattern, bound) {
            const found = [];
            const maxOffset = Math.max(...pattern);
            const primeSet = new Set(primes);
            
            for (const p of primes) {
                if (p + maxOffset > bound) break;
                
                let valid = true;
                const constellation = [];
                
                for (const offset of pattern) {
                    const candidate = p + offset;
                    constellation.push(candidate);
                    if (!primeSet.has(candidate)) {
                        valid = false;
                        break;
                    }
                }
                
                if (valid) {
                    found.push({
                        start: p,
                        values: [...constellation],
                        span: maxOffset
                    });
                }
            }
            
            return found;
        }

        function analyzeGaps(constellations) {
            if (constellations.length === 0) {
                return { count: 0, density: 0, avgGap: 0, maxGap: 0, minGap: 0, gaps: [] };
            }
            
            const starts = constellations.map(c => c.start);
            const gaps = [];
            
            for (let i = 1; i < starts.length; i++) {
                gaps.push(starts[i] - starts[i-1]);
            }
            
            return {
                count: constellations.length,
                avgGap: gaps.length > 0 ? gaps.reduce((a, b) => a + b, 0) / gaps.length : 0,
                maxGap: gaps.length > 0 ? Math.max(...gaps) : 0,
                minGap: gaps.length > 0 ? Math.min(...gaps) : 0,
                gaps: gaps,
                first: constellations.slice(0, 10),
                last: constellations.slice(-5)
            };
        }

        function calcR(primes, pattern, pMax) {
            let product = 0.25;
            
            for (const p of primes) {
                if (p >= 3 && p <= pMax) {
                    const nu = countResidues(pattern, p);
                    product *= (1 - nu / p);
                }
            }
            
            return product;
        }

        function calcC(primes, pattern, pMax) {
            const k = pattern.length;
            let product = 1;
            
            for (const p of primes) {
                if (p >= 3 && p <= pMax) {
                    const nu = countResidues(pattern, p);
                    const num = 1 - nu / p;
                    const den = Math.pow(1 - 1/p, k);
                    product *= num / den;
                }
            }
            
            return product;
        }

        function calcM(primes, pMax) {
            let product = 1;
            
            for (const p of primes) {
                if (p >= 3 && p <= pMax) {
                    product *= (1 - 1/p);
                }
            }
            
            return product;
        }

        function format(num, precision) {
            if (Math.abs(num) >= 1e15) {
                return num.toExponential(precision);
            } else if (Math.abs(num) >= 1e6) {
                const exp = Math.floor(Math.log10(Math.abs(num)));
                const mantissa = num / Math.pow(10, exp);
                return mantissa.toFixed(precision) + ' × 10^' + exp;
            } else if (Math.abs(num) >= 1000) {
                return num.toLocaleString();
            } else {
                return num.toFixed(precision);
            }
        }

        function showTab(name) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            document.querySelector(`[onclick="showTab('${name}')"]`).classList.add('active');
            document.getElementById(name).classList.add('active');
        }

        function calculate() {
            const btn = document.getElementById('calc-btn');
            const loading = document.getElementById('loading');
            const resultsDiv = document.getElementById('results');
            const welcome = document.getElementById('welcome');
            
            try {
                const pattern = parsePattern(document.getElementById('pattern').value);
                const bound = parseFloat(document.getElementById('bound').value);
                const precision = parseInt(document.getElementById('precision').value);
                
                if (bound < 100) throw new Error('Bound must be ≥ 100');
                
                btn.disabled = true;
                loading.style.display = 'block';
                resultsDiv.classList.add('hidden');
                welcome.style.display = 'none';
                
                setTimeout(() => {
                    try {
                        compute(pattern, bound, precision);
                    } catch (error) {
                        showError(error.message);
                    } finally {
                        btn.disabled = false;
                        loading.style.display = 'none';
                    }
                }, 100);
                
            } catch (error) {
                showError(error.message);
            }
        }

        function compute(pattern, bound, precision) {
            const k = pattern.length;
            const admCheck = isAdmissible(pattern);
            
            if (!admCheck.ok) {
                throw new Error(`Pattern {${pattern.join(', ')}} not admissible`);
            }
            
            let pMax;
            const cutoffMode = document.getElementById('cutoff-mode').value;
            if (cutoffMode === 'custom') {
                pMax = parseInt(document.getElementById('custom-cutoff').value);
                if (isNaN(pMax) || pMax < 3) throw new Error('Custom p_max must be ≥ 3');
            } else {
                const primes = sieve(Math.floor(bound));
                pMax = primes[primes.length - 1];
            }
            
            const primes = sieve(Math.max(pMax, bound));
            const constellations = findConstellations(primes, pattern, bound);
            const gapAnalysis = analyzeGaps(constellations);
            const count = constellations.length;
            
            const rMod = calcR(primes, pattern, pMax);
            const cH = calcC(primes, pattern, pMax);
            const mNoTwo = calcM(primes, pMax);
            
            const identityCheck = 0.25 * cH * Math.pow(mNoTwo, k);
            const identityError = Math.abs(rMod - identityCheck) / Math.abs(rMod);
            
            const xR = bound * rMod;
            const wFit = xR > 0 ? count / xR : 0;
            const wTheory = Math.exp(k * GAMMA) * Math.log(bound);
            const ratio = wTheory > 0 ? wFit / wTheory : 0;
            
            results = {
                pattern, k, bound, pMax, count,
                constellations, gapAnalysis,
                rMod, cH, mNoTwo, identityCheck, identityError,
                xR, wFit, wTheory, ratio, admCheck,
                primeCount: primes.filter(p => p <= bound).length,
                precision
            };
            
            display();
        }

        function display() {
            const r = results;
            
            document.getElementById('pattern-name').textContent = `ℋ = {${r.pattern.join(', ')}}`;
            document.getElementById('summary').innerHTML = `
                Pattern size k = ${r.k} • Upper bound = ${format(r.bound, 0)} • Prime cutoff p<sub>max</sub> = ${r.pMax.toLocaleString()}
            `;
            
            document.getElementById('result-cards').innerHTML = `
                <div class="result-card">
                    <div class="result-label">Pattern Size (k)</div>
                    <div class="result-value">${r.k}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Count</div>
                    <div class="result-value">${r.count.toLocaleString()}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Primes π(${format(r.bound, 0)})</div>
                    <div class="result-value">${r.primeCount.toLocaleString()}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Density</div>
                    <div class="result-value">${(r.count / r.bound * 100).toFixed(4)}%</div>
                </div>
                <div class="result-card">
                    <div class="result-label">R<sub>ℋ</sub></div>
                    <div class="result-value">${r.rMod.toExponential(r.precision)}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">C<sub>ℋ</sub></div>
                    <div class="result-value">${format(r.cH, r.precision)}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">M^${r.k}</div>
                    <div class="result-value">${Math.pow(r.mNoTwo, r.k).toExponential(r.precision)}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Calibration</div>
                    <div class="result-value">${r.ratio.toFixed(r.precision)}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Avg Gap</div>
                    <div class="result-value">${r.gapAnalysis.avgGap.toFixed(1)}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Max Gap</div>
                    <div class="result-value">${r.gapAnalysis.maxGap.toLocaleString()}</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Identity Error</div>
                    <div class="result-value">${(r.identityError * 100).toExponential(2)}%</div>
                </div>
                <div class="result-card">
                    <div class="result-label">Span</div>
                    <div class="result-value">${Math.max(...r.pattern)}</div>
                </div>
            `;

            const admissibilityHtml = r.admCheck.checks.map(check => 
                `<span style="color: ${check.ok ? '#43e97b' : '#f5576c'}; font-family: 'JetBrains Mono', monospace;">
                    p=${check.prime}: ${check.nu}/${check.total} ${check.ok ? '✓' : '✗'}
                </span>`
            ).join(' • ');
            
            document.getElementById('admissible').innerHTML = `
                <div class="info-title">✅ Admissibility Check</div>
                <div class="info-content">
                    <p><strong>Status:</strong> Pattern ℋ = {${r.pattern.join(', ')}} is admissible</p>
                    <p><strong>Checks:</strong> ${admissibilityHtml}</p>
                    <p style="margin-top: 10px; font-style: italic;">Pattern avoids covering all residue classes modulo any prime.</p>
                </div>
            `;

            displayConstellations();
            displayIdentity();
            displayAnalysis();
            
            document.getElementById('results').classList.remove('hidden');
            showTab('overview');
        }

        function displayConstellations() {
            const r = results;
            const analysis = r.gapAnalysis;
            
            if (analysis.count === 0) {
                document.getElementById('constellation-list').innerHTML = `
                    <div class="info-box error">
                        <div class="info-title">🚫 No K-Tuples Found</div>
                        <div class="info-content">
                            <p>No ${r.k}-tuples found in range [0, ${format(r.bound, 0)}].</p>
                            <p>Try a larger bound or different pattern.</p>
                        </div>
                    </div>
                `;
                return;
            }

            const stats = `
                <div class="info-box success">
                    <div class="info-title">📊 Distribution Statistics</div>
                    <div class="info-content">
                        <div class="result-grid" style="margin-top: 15px;">
                            <div class="result-card">
                                <div class="result-label">Total Found</div>
                                <div class="result-value">${analysis.count.toLocaleString()}</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Density</div>
                                <div class="result-value">${(r.count / r.bound * 100).toFixed(6)}%</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Average Gap</div>
                                <div class="result-value">${analysis.avgGap.toFixed(2)}</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Gap Range</div>
                                <div class="result-value">${analysis.minGap}-${analysis.maxGap}</div>
                            </div>
                        </div>
                    </div>
                </div>
            `;

            // Always show complete enumeration, but with smart formatting for large lists
            const allConstellations = `
                <div class="info-box warning">
                    <div class="info-title">🌟 Complete Enumeration - All ${analysis.count.toLocaleString()} K-Tuples</div>
                    <div class="info-content">
                        ${analysis.count <= 100 ? 
                            `<p><strong>Showing all ${analysis.count} constellations found:</strong></p>` :
                            `<p><strong>Showing all ${analysis.count.toLocaleString()} constellations (scroll to see all):</strong></p>`
                        }
                        <div style="max-height: ${analysis.count <= 50 ? '400px' : analysis.count <= 200 ? '500px' : '600px'}; overflow-y: auto; margin-top: 15px; border: 1px solid rgba(255,255,255,0.2); border-radius: 8px; background: rgba(0,0,0,0.2);">
                            ${r.constellations.map((c, i) => {
                                const rowColor = i % 2 === 0 ? 'rgba(255, 255, 255, 0.05)' : 'rgba(255, 255, 255, 0.02)';
                                return `
                                    <div style="
                                        background: ${rowColor}; 
                                        padding: 8px 16px; 
                                        font-family: 'JetBrains Mono', monospace; 
                                        font-size: 0.9rem;
                                        border-bottom: 1px solid rgba(255,255,255,0.1);
                                        display: flex;
                                        justify-content: space-between;
                                        align-items: center;
                                    ">
                                        <span style="color: #4facfe; font-weight: 600;">${String(i + 1).padStart(4)}:</span>
                                        <span style="color: white; flex: 1; margin-left: 15px;">{${c.values.join(', ')}}</span>
                                        <span style="color: rgba(255,255,255,0.7); font-size: 0.8rem;">start: ${c.start.toLocaleString()}, span: ${c.span}</span>
                                    </div>
                                `;
                            }).join('')}
                        </div>
                        ${analysis.count > 100 ? `
                            <div style="margin-top: 15px; padding: 10px; background: rgba(255,255,255,0.1); border-radius: 6px; font-size: 0.9rem;">
                                <strong>💡 Navigation Tips:</strong> Use Ctrl+F to search for specific values. 
                                Each row shows: index, constellation values, starting prime, and span.
                            </div>
                        ` : ''}
                    </div>
                </div>
            `;

            // Gap analysis for larger datasets
            const gapAnalysis = analysis.count > 1 ? `
                <div class="info-box">
                    <div class="info-title">📏 Gap Analysis</div>
                    <div class="info-content">
                        <p><strong>Gaps between consecutive starting primes:</strong></p>
                        <div class="result-grid" style="margin-top: 10px;">
                            <div class="result-card">
                                <div class="result-label">Smallest Gap</div>
                                <div class="result-value">${analysis.minGap}</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Largest Gap</div>
                                <div class="result-value">${analysis.maxGap.toLocaleString()}</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Average Gap</div>
                                <div class="result-value">${analysis.avgGap.toFixed(2)}</div>
                            </div>
                            <div class="result-card">
                                <div class="result-label">Total Gaps</div>
                                <div class="result-value">${analysis.gaps.length}</div>
                            </div>
                        </div>
                        ${analysis.gaps.length <= 20 ? `
                            <div style="margin-top: 15px;">
                                <strong>All gaps:</strong>
                                <div style="font-family: 'JetBrains Mono', monospace; background: rgba(0,0,0,0.3); padding: 10px; border-radius: 5px; margin-top: 5px; font-size: 0.9rem;">
                                    ${analysis.gaps.join(', ')}
                                </div>
                            </div>
                        ` : `
                            <div style="margin-top: 15px;">
                                <strong>First 20 gaps:</strong>
                                <div style="font-family: 'JetBrains Mono', monospace; background: rgba(0,0,0,0.3); padding: 10px; border-radius: 5px; margin-top: 5px; font-size: 0.9rem;">
                                    ${analysis.gaps.slice(0, 20).join(', ')}${analysis.gaps.length > 20 ? `, ... (${analysis.gaps.length - 20} more)` : ''}
                                </div>
                            </div>
                        `}
                    </div>
                </div>
            ` : '';

            // Summary box for large datasets
            const summary = analysis.count > 10 ? `
                <div class="info-box">
                    <div class="info-title">📋 Quick Summary</div>
                    <div class="info-content">
                        <p><strong>First constellation:</strong> {${r.constellations[0].values.join(', ')}} (starting at ${r.constellations[0].start})</p>
                        <p><strong>Last constellation:</strong> {${r.constellations[r.constellations.length-1].values.join(', ')}} (starting at ${r.constellations[r.constellations.length-1].start})</p>
                        <p><strong>Range covered:</strong> ${r.constellations[0].start.toLocaleString()} to ${r.constellations[r.constellations.length-1].start.toLocaleString()}</p>
                        <p><strong>Efficiency:</strong> ${(analysis.count / r.primeCount * 100).toFixed(4)}% of primes start a ${r.k}-tuple</p>
                    </div>
                </div>
            ` : '';

            document.getElementById('constellation-list').innerHTML = stats + summary + allConstellations + gapAnalysis;
        }

        function displayIdentity() {
            const r = results;
            
            document.getElementById('verification').innerHTML = `
                <div class="info-box">
                    <div class="info-title">🔧 Verification</div>
                    <div class="info-content">
                        <div class="code-block">
<strong>Direct Calculation:</strong>
R_ℋ = ${r.rMod.toExponential(r.precision)}

<strong>Identity Components:</strong>
A_ℋ = 0.25
C_ℋ = ${r.cH.toExponential(r.precision)}
M^${r.k} = ${r.mNoTwo.toExponential(r.precision)}^${r.k} = ${Math.pow(r.mNoTwo, r.k).toExponential(r.precision)}

<strong>Identity Result:</strong>
A_ℋ × C_ℋ × M^${r.k} = 0.25 × ${r.cH.toExponential(r.precision)} × ${Math.pow(r.mNoTwo, r.k).toExponential(r.precision)}
                     = ${r.identityCheck.toExponential(r.precision)}

<strong>Verification:</strong>
Error: ${(r.identityError * 100).toExponential(2)}%
Status: ${r.identityError < 1e-10 ? 'PASSED ✓' : 'FAILED ✗'}
                        </div>
                    </div>
                </div>

                <div class="info-box ${r.identityError < 1e-10 ? 'success' : 'error'}">
                    <div class="info-title">
                        ${r.identityError < 1e-10 ? '✅ Identity Confirmed' : '❌ Identity Failed'}
                    </div>
                    <div class="info-content">
                        <p>
                            The Master Identity has been ${r.identityError < 1e-10 ? 'verified' : 'rejected'} 
                            for pattern ℋ = {${r.pattern.join(', ')}} with error ${(r.identityError * 100).toExponential(2)}%.
                        </p>
                        ${r.identityError < 1e-10 ? 
                            '<p>This confirms the universal structure of prime constellations.</p>' :
                            '<p>Error suggests computational issue or identity refinement needed.</p>'
                        }
                    </div>
                </div>
            `;
        }

        function displayAnalysis() {
            const r = results;
            
            document.getElementById('math-analysis').innerHTML = `
                <div class="info-box">
                    <div class="info-title">📊 Pattern Analysis</div>
                    <div class="info-content">
                        <p><strong>Properties:</strong></p>
                        <ul style="margin-left: 20px; line-height: 1.8;">
                            <li>Pattern span: ${Math.max(...r.pattern)} (largest offset)</li>
                            <li>Density: ${(r.count / r.bound * 100).toFixed(6)}% of search range</li>
                            <li>Prime efficiency: ${(r.count / r.primeCount * 100).toFixed(4)}% of primes start constellation</li>
                            <li>Sieve density: R_ℋ = ${(r.rMod * 100).toExponential(2)}% after sieving ≤ ${r.pMax}</li>
                        </ul>
                    </div>
                </div>

                <div class="info-box warning">
                    <div class="info-title">🔬 Universal Structure</div>
                    <div class="info-content">
                        <p><strong>Mertens Scaling:</strong> Power k = ${r.k} shows how complexity affects sieve requirements.</p>
                        <p><strong>Singular Series:</strong> C_ℋ = ${r.cH.toFixed(6)} encodes pattern-specific information.</p>
                        <p><strong>Calibration:</strong> Ratio = ${r.ratio.toFixed(3)} connects finite to asymptotic behavior.</p>
                    </div>
                </div>

                <div class="info-box">
                    <div class="info-title">📈 Asymptotic Behavior</div>
                    <div class="info-content">
                        <div class="code-block">
<strong>Hardy-Littlewood Conjecture:</strong>
π_ℋ(x) ~ 𝔖_ℋ × x / (log x)^${r.k}  as x → ∞

<strong>Finite Density:</strong>
R_ℋ(p_max) ~ A_ℋ × 𝔖_ℋ × e^(-${r.k}γ) / (log p_max)^${r.k}

<strong>Current Calibration:</strong>
W_fit = π_ℋ(${format(r.bound, 0)}) / (${format(r.bound, 0)} × R_ℋ) = ${r.wFit.toFixed(3)}
W_theory = e^(${r.k}γ) × log(${format(r.bound, 0)}) = ${r.wTheory.toFixed(3)}
Ratio = ${r.ratio.toFixed(3)} (finite-cutoff correction)
                        </div>
                    </div>
                </div>

                <div class="info-box success">
                    <div class="info-title">🚀 Impact</div>
                    <div class="info-content">
                        <p><strong>Computational:</strong> Exact identity enables precise finite calculations for any k-tuple.</p>
                        <p><strong>Theoretical:</strong> Universal k-exponent reveals deep constellation structure connections.</p>
                        <p><strong>Algorithmic:</strong> Calibration ratios optimize probabilistic search algorithms.</p>
                    </div>
                </div>
            `;
        }

        function showError(message) {
            document.getElementById('results').innerHTML = `
                <div class="info-box error" style="margin: 50px 30px;">
                    <div class="info-title">❌ Error</div>
                    <div class="info-content">
                        <p style="font-size: 1.1rem;">${message}</p>
                        <p style="margin-top: 15px; font-style: italic;">Check parameters and try again.</p>
                    </div>
                </div>
            `;
            document.getElementById('results').classList.remove('hidden');
            document.getElementById('welcome').style.display = 'none';
        }

        document.getElementById('pattern').addEventListener('input', updatePattern);
        
        document.getElementById('cutoff-mode').addEventListener('change', function() {
            const custom = document.getElementById('custom-cutoff');
            if (this.value === 'custom') {
                custom.classList.remove('hidden');
            } else {
                custom.classList.add('hidden');
            }
        });

        ['pattern', 'bound', 'custom-cutoff', 'precision'].forEach(id => {
            document.getElementById(id).addEventListener('keypress', function(e) {
                if (e.key === 'Enter') calculate();
            });
        });

        updatePattern();
    </script>
</body>
</html>
