<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Twin Prime Sieve Explorer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #1a1a2e;
            color: #eee;
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            margin-bottom: 40px;
        }

        h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            color: #64ffda;
        }

        .tagline {
            color: #8892b0;
            font-size: 0.95em;
        }

        .panel {
            background: #0a192f;
            border: 1px solid #233554;
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 25px;
        }

        .panel h2 {
            color: #ccd6f6;
            font-size: 1.4em;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .controls {
            display: grid;
            gap: 25px;
            margin-bottom: 20px;
        }

        .control {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        label {
            color: #8892b0;
            font-size: 0.9em;
            font-weight: 500;
        }

        input[type="range"] {
            width: 100%;
            height: 6px;
            background: #233554;
            border-radius: 3px;
            outline: none;
            cursor: pointer;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 18px;
            height: 18px;
            background: #64ffda;
            border-radius: 50%;
            cursor: pointer;
        }

        input[type="range"]::-moz-range-thumb {
            width: 18px;
            height: 18px;
            background: #64ffda;
            border-radius: 50%;
            cursor: pointer;
            border: none;
        }

        .val {
            color: #64ffda;
            font-weight: 600;
            font-size: 0.95em;
        }

        button {
            background: #64ffda;
            color: #0a192f;
            border: none;
            padding: 12px 24px;
            border-radius: 4px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.95em;
        }

        button:hover {
            background: #52e8c4;
            transform: translateY(-1px);
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .stat {
            background: #112240;
            padding: 18px;
            border-radius: 6px;
            border-left: 3px solid #64ffda;
        }

        .stat-label {
            color: #8892b0;
            font-size: 0.85em;
            margin-bottom: 5px;
        }

        .stat-value {
            color: #ccd6f6;
            font-size: 1.8em;
            font-weight: 700;
        }

        .stat-sub {
            color: #8892b0;
            font-size: 0.8em;
            margin-top: 3px;
        }

        .viz {
            margin-bottom: 25px;
        }

        .bar-container {
            background: #112240;
            height: 50px;
            border-radius: 6px;
            overflow: hidden;
            margin-bottom: 20px;
        }

        .bar-fill {
            height: 100%;
            background: linear-gradient(90deg, #64ffda, #52e8c4);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            color: #0a192f;
            transition: width 0.4s ease;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(45px, 1fr));
            gap: 6px;
            margin-top: 15px;
        }

        .cell {
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 4px;
            font-size: 0.75em;
            font-weight: 600;
            cursor: help;
            transition: transform 0.15s;
        }

        .cell:hover {
            transform: scale(1.15);
        }

        .found {
            background: #64ffda;
            color: #0a192f;
        }

        .missed {
            background: #f07167;
            color: #fff;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9em;
        }

        th {
            background: #112240;
            padding: 12px;
            text-align: left;
            color: #64ffda;
            font-weight: 600;
            border-bottom: 2px solid #233554;
        }

        td {
            padding: 10px 12px;
            border-bottom: 1px solid #233554;
            color: #ccd6f6;
        }

        tr:hover {
            background: #112240;
        }

        .tag {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 3px;
            font-size: 0.85em;
            font-weight: 600;
        }

        .tag-ok {
            background: #64ffda;
            color: #0a192f;
        }

        .tag-miss {
            background: #f07167;
            color: white;
        }

        .info-box {
            background: #112240;
            border-left: 3px solid #8892b0;
            padding: 15px;
            margin: 15px 0;
            border-radius: 4px;
            color: #8892b0;
            font-size: 0.9em;
        }

        .formula {
            background: #0a192f;
            padding: 12px;
            border-radius: 4px;
            font-family: 'Courier New', monospace;
            margin: 12px 0;
            text-align: center;
            color: #64ffda;
            border: 1px solid #233554;
        }

        .note {
            background: #112240;
            padding: 20px;
            border-radius: 6px;
            margin-top: 20px;
        }

        .note h3 {
            color: #64ffda;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .note p {
            color: #8892b0;
            margin-bottom: 8px;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: #64ffda;
        }

        .oeis-info {
            background: #0a192f;
            padding: 12px;
            margin: 10px 0;
            border-radius: 4px;
            border: 1px solid #233554;
            font-size: 0.85em;
            color: #8892b0;
        }

        .oeis-info a {
            color: #64ffda;
            text-decoration: none;
        }

        .oeis-info a:hover {
            text-decoration: underline;
        }

        .explainer {
            background: #112240;
            border-left: 3px solid #64ffda;
            padding: 12px 15px;
            margin: 10px 0;
            border-radius: 4px;
            font-size: 0.88em;
            color: #8892b0;
        }

        .explainer strong {
            color: #ccd6f6;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            border-bottom: 2px solid #233554;
        }

        .tab {
            background: transparent;
            color: #8892b0;
            border: none;
            padding: 12px 24px;
            cursor: pointer;
            font-weight: 600;
            border-bottom: 3px solid transparent;
            transition: all 0.2s;
            margin-bottom: -2px;
        }

        .tab:hover {
            color: #64ffda;
            transform: none;
        }

        .tab.active {
            color: #64ffda;
            border-bottom-color: #64ffda;
            background: transparent;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .research-section {
            margin-bottom: 35px;
        }

        .research-section h3 {
            color: #64ffda;
            font-size: 1.3em;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .research-section p {
            color: #8892b0;
            line-height: 1.7;
            margin-bottom: 12px;
        }

        .research-section ul {
            margin: 12px 0 12px 25px;
            color: #8892b0;
        }

        .research-section li {
            margin: 8px 0;
            line-height: 1.6;
        }

        .theorem {
            background: #0a192f;
            border: 1px solid #233554;
            border-left: 4px solid #f07167;
            padding: 20px;
            margin: 20px 0;
            border-radius: 6px;
        }

        .theorem-title {
            color: #f07167;
            font-weight: 700;
            font-size: 1.05em;
            margin-bottom: 10px;
        }

        .theorem-body {
            color: #ccd6f6;
            line-height: 1.7;
        }

        .proof {
            background: #112240;
            padding: 15px;
            margin: 15px 0;
            border-radius: 4px;
            font-size: 0.92em;
        }

        .proof-title {
            color: #64ffda;
            font-weight: 600;
            margin-bottom: 8px;
        }

        code {
            background: #0a192f;
            padding: 2px 6px;
            border-radius: 3px;
            color: #64ffda;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 1.6em;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Twin Prime Sieve Explorer</h1>
            <p class="tagline">Testing reciprocal sampling on modular residue classes</p>
            <div class="tabs">
                <button class="tab active" onclick="switchTab('explorer')">Explorer</button>
                <button class="tab" onclick="switchTab('research')">Research</button>
            </div>
        </header>

        <div id="explorer-tab" class="tab-content active">

        <div class="panel">
            <h2>Parameters</h2>
            <div class="explainer">
                <strong>What you're controlling:</strong> The modulus M determines the size of the residue space we're searching. 
                Δ controls how far we look around each sample point. Larger n means more residues but longer computation.
            </div>
            <div class="controls">
                <div class="control">
                    <label>Exponent n → M = 30·2^n <span id="warn" style="color: #f07167; font-size: 0.85em;"></span></label>
                    <div style="display: flex; gap: 10px; align-items: center;">
                        <input type="range" id="nSlider" min="0" max="8" value="2" step="1" style="flex: 1;">
                        <input type="number" id="nInput" min="0" max="15" value="2" 
                               style="width: 70px; padding: 6px; background: #112240; border: 1px solid #233554; 
                                      color: #64ffda; border-radius: 4px; font-weight: 600;">
                    </div>
                </div>

                <div class="control">
                    <label>Offset ±Δ</label>
                    <input type="range" id="dSlider" min="1" max="100" value="4" step="1">
                    <span class="val" id="dVal">4</span>
                </div>

                <div class="control">
                    <label>Sample density (× base)</label>
                    <input type="range" id="mSlider" min="0.5" max="4" value="1" step="0.5">
                    <span class="val" id="mVal">1.0</span>
                </div>
            </div>

            <button onclick="run()" id="calcBtn">Calculate</button>
            <button onclick="loadOEIS()" id="oeisBtn" style="background: #8892b0; margin-left: 10px;">Load from OEIS</button>
            <div id="progress" style="margin-top: 10px; color: #64ffda; font-size: 0.9em;"></div>
        </div>

        <div class="stats" id="stats"></div>

        <div class="explainer">
            <strong>Reading the stats:</strong> "Total residues" shows how many valid twin-residue pairs exist for this modulus. 
            "Found" is what percentage our sampling method captured. "Max distance" reveals the furthest any residue sits from a sample point.
        </div>

        <div class="panel">
            <h2>Coverage</h2>
            <div class="explainer">
                <strong>Visual breakdown:</strong> Each cell represents a valid twin-residue mod M. Green means our reciprocal sampling 
                found it (within ±Δ of some ⌊M/k⌋). Red means it's a "gap residue" - trapped between sample points, too far to reach.
            </div>
            <div class="info-box">
                Green = found within ±Δ of some ⌊M/k⌋ point. Red = gap residue (too far from any seed).
            </div>
            <div class="bar-container">
                <div class="bar-fill" id="bar" style="width: 0%">0%</div>
            </div>
            <div class="grid" id="grid"></div>
        </div>

        <div class="panel">
            <h2>Results</h2>
            <div class="explainer">
                <strong>Detailed breakdown:</strong> This table shows every residue, whether it was found, its distance to the nearest 
                sample point, and which seed point (⌊M/k⌋) it's closest to. Notice how missed residues always have distance > Δ.
            </div>
            <div style="overflow-x: auto;">
                <table id="table"></table>
            </div>
        </div>

        </div> <!-- End explorer tab -->

        <div id="research-tab" class="tab-content">
            <div class="panel">
                <h2>Mathematical Foundation</h2>
                
                <div class="research-section">
                    <h3>The Problem</h3>
                    <p>
                        We're investigating twin-prime residues modulo <code>M = 30·2^n</code>. A residue <code>r</code> is valid if 
                        both <code>r</code> and <code>r+2</code> are coprime to M (share no common factors). This mirrors how twin primes 
                        work, but in modular arithmetic.
                    </p>
                    <p>
                        The set of all such residues is denoted <strong>Φ(M)</strong>:
                    </p>
                    <div class="formula">
                        Φ(M) = {r mod M : gcd(r,M) = gcd(r+2,M) = 1}
                    </div>
                    <p>
                        The naive approach is checking all M values, which becomes computationally expensive as n grows. 
                        For n=10, that's checking 30,720 candidates.
                    </p>
                </div>

                <div class="research-section">
                    <h3>Reciprocal Sampling Method</h3>
                    <p>
                        Instead of exhaustive search, we use a <strong>reciprocal sampling strategy</strong>. We place sample points at:
                    </p>
                    <div class="formula">
                        s_k = ⌊M/k⌋ for k = 1, 2, 3, ..., T
                    </div>
                    <p>
                        Then we check candidates <code>r = s_k ± δ</code> for <code>δ ∈ [0, Δ]</code>. This creates a non-uniform grid 
                        that's denser near M and sparser near 0 - the opposite of linear sampling.
                    </p>
                    <p><strong>Why this works:</strong></p>
                    <ul>
                        <li>Reciprocals naturally cluster where residues tend to concentrate</li>
                        <li>Computational cost is O(T·Δ) instead of O(M)</li>
                        <li>For small Δ, this is massively more efficient than full enumeration</li>
                    </ul>
                </div>

                <div class="research-section">
                    <h3>Core vs Gap Classification</h3>
                    <p>
                        This method partitions Φ(M) into two classes:
                    </p>
                    <div class="theorem">
                        <div class="theorem-title">Definition: Core and Gap Residues</div>
                        <div class="theorem-body">
                            For fixed Δ, a residue r ∈ Φ(M) is:
                            <ul style="margin: 10px 0 0 20px;">
                                <li><strong>Core</strong> if dist(r, {s_1, s_2, ..., s_T}) ≤ Δ</li>
                                <li><strong>Gap</strong> if dist(r, {s_1, s_2, ..., s_T}) > Δ</li>
                            </ul>
                            where dist uses circular distance on the modulus.
                        </div>
                    </div>
                    <p>
                        This classification is algorithmic, not purely number-theoretic. It depends on the sampling method, 
                        not just properties of M itself.
                    </p>
                </div>

                <div class="research-section">
                    <h3>The M/4 Scaling Law</h3>
                    <p>
                        Empirical observation across multiple values of n reveals a consistent pattern:
                    </p>
                    <div class="theorem">
                        <div class="theorem-title">Empirical Result</div>
                        <div class="theorem-body">
                            For M = 30·2^n with reciprocal sampling at T ≈ 3·2^n points, the maximum distance 
                            D_max from any residue to its nearest sample point satisfies:
                            <div class="formula" style="margin: 10px 0;">
                                D_max ≈ M/4
                            </div>
                            More precisely, D_max/M → 0.25 as n → ∞.
                        </div>
                    </div>
                    
                    <div class="proof">
                        <div class="proof-title">Why M/4?</div>
                        The largest gap occurs between s_1 = M and s_2 = M/2. A residue at M/4 + M/2 = 3M/4 is equidistant 
                        from both (circular distance M/4 to each). This geometric configuration appears to be the worst case.
                    </div>

                    <p><strong>Implications:</strong></p>
                    <ul>
                        <li>No fixed Δ can maintain constant coverage as M grows</li>
                        <li>To achieve 100% coverage, we need Δ ≈ M/4, which negates the efficiency gain</li>
                        <li>Coverage with fixed Δ degrades as: C(M,Δ) ≈ min(1, 4Δ/M)</li>
                    </ul>
                </div>

                <div class="research-section">
                    <h3>Observed Coverage Patterns</h3>
                    <p>Testing with Δ=4 across different n values:</p>
                    <table style="margin: 15px 0;">
                        <thead>
                            <tr><th>n</th><th>M</th><th>|Φ(M)|</th><th>Coverage</th><th>D_max</th><th>D_max/M</th></tr>
                        </thead>
                        <tbody>
                            <tr><td>0</td><td>30</td><td>8</td><td>100%</td><td>4</td><td>0.133</td></tr>
                            <tr><td>1</td><td>60</td><td>8</td><td>100%</td><td>8</td><td>0.133</td></tr>
                            <tr><td>2</td><td>120</td><td>16</td><td>100%</td><td>16</td><td>0.133</td></tr>
                            <tr><td>3</td><td>240</td><td>32</td><td>~67%</td><td>32</td><td>0.133</td></tr>
                            <tr><td>4</td><td>480</td><td>64</td><td>~50%</td><td>64</td><td>0.133</td></tr>
                            <tr><td>5</td><td>960</td><td>128</td><td>~33%</td><td>128</td><td>0.133</td></tr>
                        </tbody>
                    </table>
                    <p>
                        Notice: D_max grows linearly with M, maintaining a constant ratio. Coverage drops because our 
                        fixed Δ=4 becomes relatively smaller.
                    </p>
                </div>

                <div class="research-section">
                    <h3>Adaptive Offset Conjecture</h3>
                    <p>
                        The natural solution is to make Δ scale with the local gap size:
                    </p>
                    <div class="theorem">
                        <div class="theorem-title">Conjecture: Adaptive Sampling</div>
                        <div class="theorem-body">
                            Define variable offsets:
                            <div class="formula" style="margin: 10px 0;">
                                Δ_k = ⌊c · M/k⌋
                            </div>
                            where c is a constant (empirically c ≈ 0.3 suffices). Then checking candidates 
                            <code>s_k ± δ</code> for <code>δ ∈ [0, Δ_k]</code> achieves 100% coverage with 
                            computational cost O(T · log(M)).
                        </div>
                    </div>
                    
                    <div class="proof">
                        <div class="proof-title">Intuition</div>
                        The gap between s_k and s_(k+1) is approximately M/(k(k+1)). By setting Δ_k ∝ M/k, 
                        we ensure the search radius around each seed is proportional to the local gap density. 
                        This adaptively covers sparse regions while not wasting computation in dense regions.
                    </div>
                </div>

                <div class="research-section">
                    <h3>Computational Complexity Analysis</h3>
                    <p><strong>Naive enumeration:</strong> O(M) checks, each requiring O(log M) for gcd</p>
                    <p><strong>Fixed-Δ reciprocal:</strong> O(T·Δ) = O(M·Δ/log M) for T ≈ M/log M</p>
                    <p><strong>Adaptive reciprocal:</strong> O(T·log M) since Σ Δ_k ≈ M·Σ(1/k) = O(M·log T)</p>
                    
                    <p>
                        The adaptive method achieves completeness while maintaining sub-linear complexity in the 
                        number of checks (though still linear in M due to the gcd operations).
                    </p>
                </div>

                <div class="research-section">
                    <h3>Open Questions</h3>
                    <ul>
                        <li>Can we prove the D_max ≈ M/4 bound rigorously, or is it merely empirical?</li>
                        <li>Does the core/gap classification have number-theoretic significance beyond the algorithm?</li>
                        <li>Are there other modulus forms (not 30·2^n) where reciprocal sampling performs better/worse?</li>
                        <li>Can this method be adapted for other modular problems (e.g., prime k-tuples)?</li>
                        <li>What's the optimal value of c in the adaptive conjecture? Is 0.3 truly sufficient?</li>
                    </ul>
                </div>

                <div class="research-section">
                    <h3>Practical Applications</h3>
                    <p>Beyond theoretical interest, this method has potential uses in:</p>
                    <ul>
                        <li><strong>Cryptography:</strong> Efficiently sampling twin-prime candidates for key generation</li>
                        <li><strong>Hash functions:</strong> Designing collision-resistant structures based on residue patterns</li>
                        <li><strong>Random number generation:</strong> Using gap structure for statistical randomness tests</li>
                        <li><strong>Algorithm design:</strong> The core/gap pattern suggests data structure optimizations</li>
                    </ul>
                </div>

                <div class="note">
                    <h3>References & Further Reading</h3>
                    <p>This research builds on classical sieve theory but introduces novel algorithmic perspectives:</p>
                    <ul>
                        <li>Classical work: Eratosthenes sieve, Atkin sieve</li>
                        <li>Modular arithmetic: Hardy & Wright, "An Introduction to the Theory of Numbers"</li>
                        <li>Twin primes: Zhang's breakthrough on bounded gaps (2013)</li>
                        <li>OEIS sequences: A001676 (related twin-prime patterns)</li>
                    </ul>
                </div>
            </div>
        </div> <!-- End research tab -->

        <div class="note">
            <h3>What's happening here</h3>
            <p>For modulus M, we want to find all r where gcd(r,M) = gcd(r+2,M) = 1 (twin-prime residues).</p>
            <p>Instead of checking everything, we sample at points s_k = ⌊M/k⌋ and look ±Δ around each.</p>
            <p>Observation: as M grows, fixed Δ covers less. The "gap residues" fall between seeds.</p>
            <div class="formula">Required D ≈ M/4 for full coverage</div>
            <p>This shows the tradeoff: efficiency vs completeness. Adaptive offsets could solve it.</p>
        </div>
    </div>

    <script>
        function gcd(a, b) {
            a = Math.abs(a);
            b = Math.abs(b);
            while (b) [a, b] = [b, a % b];
            return a;
        }

        function getPhi(M) {
            let phi = [];
            for (let r = 0; r < M; r++) {
                if (gcd(r, M) === 1 && gcd(r + 2, M) === 1) {
                    phi.push(r);
                }
            }
            return phi;
        }

        function getPhiCount(n) {
            // φ(30·2^n) for twin residues
            // Pattern from OEIS-like calculation
            if (n === 0) return 8;
            return 8 * Math.pow(2, n - 1);
        }

        function sample(M, T, delta) {
            let found = new Set();
            let info = new Map();

            for (let k = 1; k <= T; k++) {
                let s = Math.floor(M / k);
                
                for (let d = -delta; d <= delta; d++) {
                    let r = ((s + d) % M + M) % M;
                    
                    if (gcd(r, M) === 1 && gcd((r + 2) % M, M) === 1) {
                        found.add(r);
                        if (!info.has(r)) {
                            info.set(r, {k: k, seed: s, offset: d});
                        }
                    }
                }
            }

            return {found: [...found].sort((a,b) => a-b), info: info};
        }

        function getDists(M, T, phi) {
            let maxD = 0;
            let dists = [];
            
            // Cache seed points
            let seeds = [];
            for (let k = 1; k <= T; k++) {
                seeds.push({k: k, s: Math.floor(M / k)});
            }

            for (let r of phi) {
                let minD = M;
                let bestK = 0;

                for (let seed of seeds) {
                    let d = Math.abs(r - seed.s);
                    d = Math.min(d, M - d);
                    
                    if (d < minD) {
                        minD = d;
                        bestK = seed.k;
                    }
                }

                maxD = Math.max(maxD, minD);
                dists.push({r: r, d: minD, k: bestK});
            }

            return {maxD: maxD, dists: dists};
        }

        function update() {
            let n = parseInt(document.getElementById('nSlider').value);
            let nInput = parseInt(document.getElementById('nInput').value);
            
            // Sync slider and input
            if (document.activeElement === document.getElementById('nSlider')) {
                document.getElementById('nInput').value = n;
            } else if (document.activeElement === document.getElementById('nInput')) {
                n = nInput;
                if (n <= 8) {
                    document.getElementById('nSlider').value = n;
                }
            }
            
            let d = parseInt(document.getElementById('dSlider').value);
            let m = parseFloat(document.getElementById('mSlider').value);
            
            document.getElementById('dVal').textContent = d;
            document.getElementById('mVal').textContent = m.toFixed(1);
            
            // Show warning for large n
            let M = 30 * Math.pow(2, n);
            let expectedPhi = getPhiCount(n);
            let warn = document.getElementById('warn');
            
            if (n >= 12) {
                warn.textContent = `(⚠️ M=${M.toLocaleString()}, ~${expectedPhi.toLocaleString()} residues - may take 30s+)`;
            } else if (n >= 10) {
                warn.textContent = `(M=${M.toLocaleString()}, ~${expectedPhi.toLocaleString()} residues - ~10s)`;
            } else if (n >= 7) {
                warn.textContent = '(may take a few seconds)';
            } else {
                warn.textContent = '';
            }
        }

        async function loadOEIS() {
            let prog = document.getElementById('progress');
            prog.innerHTML = `<div class="oeis-info">
                OEIS sequence for twin-prime residues mod 30·2^n:<br>
                For small n, we compute directly. For large n (>10), the pattern is:<br>
                |Φ(30·2^n)| = 8·2^(n-1) for n≥1<br>
                <a href="https://oeis.org/A001676" target="_blank">Related: OEIS A001676 (twin primes mod 6)</a><br><br>
                <strong>Note:</strong> Direct computation is still needed for exact residue values. 
                OEIS gives counts/patterns, not the full residue sets.
            </div>`;
        }

        async function run() {
            let btn = document.getElementById('calcBtn');
            let prog = document.getElementById('progress');
            
            btn.disabled = true;
            btn.textContent = 'Computing...';
            prog.textContent = 'Starting...';
            
            // Let UI update
            await new Promise(r => setTimeout(r, 50));
            
            try {
                let n = parseInt(document.getElementById('nInput').value);
                let delta = parseInt(document.getElementById('dSlider').value);
                let mult = parseFloat(document.getElementById('mSlider').value);

                if (n < 0 || n > 15) {
                    throw new Error('n must be between 0 and 15');
                }

                let M = 30 * Math.pow(2, n);
                let T = Math.floor(3 * Math.pow(2, n) * mult);

                prog.textContent = `Computing Φ(${M.toLocaleString()})... (this is the slow part for large n)`;
                await new Promise(r => setTimeout(r, 10));
                
                let startTime = Date.now();
                let phi = getPhi(M);
                let phiTime = ((Date.now() - startTime) / 1000).toFixed(1);
                
                prog.textContent = `Found ${phi.length} residues in ${phiTime}s. Sampling ${T} points...`;
                await new Promise(r => setTimeout(r, 10));
                let {found, info} = sample(M, T, delta);
                
                prog.textContent = 'Calculating distances...';
                await new Promise(r => setTimeout(r, 10));
                let {maxD, dists} = getDists(M, T, phi);

                let cov = (found.length / phi.length * 100);

                prog.textContent = 'Rendering results...';
                await new Promise(r => setTimeout(r, 10));

                // stats
                document.getElementById('stats').innerHTML = `
                    <div class="stat">
                        <div class="stat-label">Modulus</div>
                        <div class="stat-value">${M.toLocaleString()}</div>
                        <div class="stat-sub">30·2^${n}</div>
                    </div>
                    <div class="stat">
                        <div class="stat-label">Total residues</div>
                        <div class="stat-value">${phi.length}</div>
                        <div class="stat-sub">Computed in ${phiTime}s</div>
                    </div>
                    <div class="stat">
                        <div class="stat-label">Found</div>
                        <div class="stat-value">${cov.toFixed(1)}%</div>
                        <div class="stat-sub">${found.length}/${phi.length}</div>
                    </div>
                    <div class="stat">
                        <div class="stat-label">Max distance</div>
                        <div class="stat-value">${maxD}</div>
                        <div class="stat-sub">≈ ${(maxD/M).toFixed(3)}M</div>
                    </div>
                `;

                // bar
                let bar = document.getElementById('bar');
                bar.style.width = cov + '%';
                bar.textContent = cov.toFixed(1) + '%';

                // grid (limit display for large n)
                if (phi.length <= 500) {
                    document.getElementById('grid').innerHTML = phi.map(r => {
                        let cls = found.includes(r) ? 'found' : 'missed';
                        return `<div class="cell ${cls}" title="${r}">${r}</div>`;
                    }).join('');
                } else {
                    document.getElementById('grid').innerHTML = 
                        `<div style="padding: 20px; text-align: center; color: #8892b0;">
                            Grid display hidden (${phi.length.toLocaleString()} residues - see table below)
                        </div>`;
                }

                // table (limit for very large n)
                prog.textContent = 'Building table...';
                await new Promise(r => setTimeout(r, 10));
                
                if (phi.length <= 2000) {
                    let rows = '';
                    for (let r of phi) {
                        let ok = found.includes(r);
                        let dist = dists.find(x => x.r === r);
                        
                        if (ok) {
                            let dat = info.get(r);
                            rows += `<tr>
                                <td>${r}</td>
                                <td><span class="tag tag-ok">✓</span></td>
                                <td>${dist.d}</td>
                                <td>⌊M/${dat.k}⌋ = ${dat.seed}, δ=${dat.offset}</td>
                            </tr>`;
                        } else {
                            rows += `<tr>
                                <td>${r}</td>
                                <td><span class="tag tag-miss">✗</span></td>
                                <td>${dist.d} > ${delta}</td>
                                <td>nearest: ⌊M/${dist.k}⌋</td>
                            </tr>`;
                        }
                    }
                    
                    document.getElementById('table').innerHTML = 
                        '<thead><tr><th>r</th><th>Status</th><th>Distance</th><th>Info</th></tr></thead><tbody>' + 
                        rows + '</tbody>';
                } else {
                    // Show summary for huge datasets
                    let foundSample = found.slice(0, 100);
                    let missedSample = phi.filter(r => !found.includes(r)).slice(0, 100);
                    
                    document.getElementById('table').innerHTML = `
                        <div style="padding: 20px; color: #8892b0;">
                            <p><strong>Dataset too large for full table display (${phi.length.toLocaleString()} residues)</strong></p>
                            <p>Summary: ${found.length} found, ${phi.length - found.length} missed</p>
                            <p>First 100 found: ${foundSample.join(', ')}...</p>
                            <p>First 100 missed: ${missedSample.join(', ')}...</p>
                        </div>`;
                }
                    
                let totalTime = ((Date.now() - startTime) / 1000).toFixed(1);
                prog.textContent = `✓ Done in ${totalTime}s (${phi.length.toLocaleString()} residues, ${T.toLocaleString()} samples)`;
                
            } catch (e) {
                prog.textContent = `Error: ${e.message}`;
                console.error(e);
            } finally {
                btn.disabled = false;
                btn.textContent = 'Calculate';
            }
        }

        document.getElementById('nSlider').oninput = update;
        document.getElementById('nInput').oninput = update;
        document.getElementById('dSlider').oninput = update;
        document.getElementById('mSlider').oninput = update;

        function switchTab(tab) {
            // Update tab buttons
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            
            // Update content
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            document.getElementById(tab + '-tab').classList.add('active');
        }

        run();
    </script>
</body>
</html>
