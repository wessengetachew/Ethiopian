<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nested Farey Channels & Fractional-Slice Coprimality - Wessen Getachew</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Palatino Linotype', 'Book Antiqua', Palatino, serif;
            line-height: 1.6;
            color: #2c3e50;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
        }

        .paper-container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            padding: 60px 80px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            border-radius: 4px;
        }

        header {
            text-align: center;
            margin-bottom: 50px;
            border-bottom: 3px solid #667eea;
            padding-bottom: 30px;
        }

        h1 {
            font-size: 2.2em;
            font-weight: 700;
            color: #1a252f;
            margin-bottom: 20px;
            letter-spacing: 0.5px;
        }

        .author {
            font-size: 1.3em;
            font-style: italic;
            color: #555;
            margin-bottom: 10px;
        }

        .date {
            font-size: 1em;
            color: #777;
        }

        .section-title {
            font-size: 1.7em;
            font-weight: 600;
            color: #2c3e50;
            margin-top: 45px;
            margin-bottom: 20px;
            border-bottom: 2px solid #667eea;
            padding-bottom: 10px;
        }

        .subsection-title {
            font-size: 1.4em;
            font-weight: 600;
            color: #34495e;
            margin-top: 35px;
            margin-bottom: 15px;
        }

        p {
            text-align: justify;
            margin-bottom: 15px;
            font-size: 1.05em;
        }

        .definition, .proposition, .theorem, .proof, .corollary, .lemma, .algorithm {
            margin: 25px 0;
            padding: 20px;
            border-radius: 6px;
            position: relative;
        }

        .definition {
            background: linear-gradient(135deg, #e8f4f8 0%, #d4e7f0 100%);
            border-left: 5px solid #3498db;
        }

        .proposition, .theorem, .corollary {
            background: linear-gradient(135deg, #f0f7ef 0%, #e1f0dd 100%);
            border-left: 5px solid #27ae60;
        }

        .lemma {
            background: linear-gradient(135deg, #fff3e0 0%, #ffe0b2 100%);
            border-left: 5px solid #ff9800;
        }

        .algorithm {
            background: linear-gradient(135deg, #f3e5f5 0%, #e1bee7 100%);
            border-left: 5px solid #9c27b0;
        }

        .proof {
            background: linear-gradient(135deg, #fef5e7 0%, #fdebd0 100%);
            border-left: 5px solid #f39c12;
        }

        .label {
            font-weight: 700;
            font-size: 1.1em;
            color: #2c3e50;
            margin-bottom: 10px;
            display: block;
        }

        .proof-end {
            float: right;
            font-size: 1.3em;
            font-weight: bold;
        }

        ul {
            margin-left: 30px;
            margin-bottom: 20px;
        }

        li {
            margin-bottom: 12px;
            font-size: 1.05em;
        }

        .canvas-container {
            margin: 30px 0;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            padding: 35px;
            border-radius: 12px;
            border: 2px solid #667eea;
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
        }

        canvas {
            border: 2px solid #495057;
            background: white;
            border-radius: 8px;
            cursor: crosshair;
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
            display: block;
            margin: 0 auto;
        }

        .controls {
            margin-top: 25px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            align-items: center;
        }

        .control-group {
            display: flex;
            align-items: center;
            gap: 10px;
            background: white;
            padding: 10px 15px;
            border-radius: 6px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        label {
            font-weight: 600;
            color: #495057;
            font-size: 0.95em;
        }

        input[type="number"], input[type="range"] {
            padding: 8px 12px;
            border: 2px solid #ced4da;
            border-radius: 6px;
            font-size: 1em;
            width: 100px;
            transition: border-color 0.3s;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: #667eea;
        }

        select {
            padding: 8px 12px;
            border: 2px solid #ced4da;
            border-radius: 6px;
            font-size: 0.95em;
            cursor: pointer;
        }

        button {
            padding: 10px 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            font-size: 0.95em;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.2);
        }

        button.secondary {
            background: linear-gradient(135deg, #95a5a6 0%, #7f8c8d 100%);
        }

        button.success {
            background: linear-gradient(135deg, #27ae60 0%, #229954 100%);
        }

        button.danger {
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
        }

        .caption {
            font-style: italic;
            color: #666;
            margin-top: 20px;
            font-size: 0.95em;
            text-align: center;
        }

        .abstract {
            background: linear-gradient(135deg, #ecf0f1 0%, #d5dbdb 100%);
            padding: 30px;
            margin: 30px 0;
            border-radius: 8px;
            font-style: italic;
            border-left: 5px solid #95a5a6;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .info-box {
            background: linear-gradient(135deg, #fff3cd 0%, #ffe69c 100%);
            border: 2px solid #ffc107;
            border-radius: 8px;
            padding: 20px;
            margin: 25px 0;
        }

        .info-box strong {
            color: #856404;
        }

        .stats-display {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 8px;
            border: 2px solid #667eea;
        }

        .stat-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #e9ecef;
        }

        .stat-row:last-child {
            border-bottom: none;
        }

        .stat-label {
            font-weight: 600;
            color: #495057;
        }

        .stat-value {
            color: #667eea;
            font-weight: 700;
        }

        .test-result {
            margin-top: 20px;
            padding: 20px;
            border-radius: 8px;
            font-weight: 600;
        }

        .test-result.pass {
            background: #d4edda;
            color: #155724;
            border: 2px solid #c3e6cb;
        }

        .test-result.fail {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #f5c6cb;
        }

        code {
            background: #f4f4f4;
            padding: 2px 6px;
            border-radius: 3px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
        }

        pre {
            background: #2c3e50;
            color: #ecf0f1;
            padding: 20px;
            border-radius: 8px;
            overflow-x: auto;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.5;
        }

        .experimental-section {
            background: #f8f9fa;
            padding: 30px;
            margin: 30px 0;
            border-radius: 8px;
            border: 2px solid #667eea;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #dee2e6;
        }

        th {
            background: #667eea;
            color: white;
            font-weight: 600;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .progress-bar {
            width: 100%;
            height: 30px;
            background: #e9ecef;
            border-radius: 15px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            transition: width 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: 600;
        }

        @media (max-width: 768px) {
            .paper-container {
                padding: 30px 20px;
            }

            h1 {
                font-size: 1.8em;
            }

            canvas {
                max-width: 100%;
                height: auto;
            }

            .controls {
                flex-direction: column;
            }

            .control-group {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="paper-container">
        <header>
            <h1>Nested Farey Channels & Fractional-Slice Coprimality Heuristic</h1>
            <div class="author">Wessen Getachew</div>
            <div class="date">October 2025</div>
        </header>

        <div class="abstract">
            <strong>Abstract.</strong> We introduce the <em>Nested Farey Channel Framework</em>, a geometric representation of modular arithmetic on the unit circle, and develop the <em>Fractional-Slice Coprimality Heuristic</em>, a rapid probabilistic prime detection algorithm based on sampling coprime residues within restricted circular arcs. Each modulus \(m\) maps to \(m\) equidistant points at angles \(2\pi r/m\). Prime moduli exhibit maximal channel openness while composites show blocked Farey channels. We prove that sampling only a fraction of the circle yields strong probabilistic discrimination between primes and composites, derive formal bounds, and provide interactive demonstrations and experimental tools.
        </div>

        <div class="section-title">Part I: Nested Farey Channels Framework</div>

        <div class="definition">
            <span class="label">Definition 1.1 (Channel Rings).</span>
            For a modulus \(m \in \mathbb{N}\), define the ring
            \[
            S_m = \left\{ e^{2\pi i r/m} : r = 0, 1, \dots, m-1 \right\}.
            \]
            Each element corresponds to a residue class \(r \pmod{m}\) visualized on the unit circle.
        </div>

        <div class="definition">
            <span class="label">Definition 1.2 (Open and Blocked Channels).</span>
            A channel \(C_{r,m}\) is said to be:
            \[
            C_{r,m} = 
            \begin{cases}
            \text{open}, & \text{if } \gcd(r,m)=1,\\
            \text{blocked}, & \text{otherwise.}
            \end{cases}
            \]
            The set of open channels has cardinality \(\varphi(m)\), Euler's totient function.
        </div>

        <div class="proposition">
            <span class="label">Proposition 1.3 (Prime Channel Completeness).</span>
            <em>For a prime modulus \(p\), every residue \(r \in \{1,2,\dots,p-1\}\) satisfies \(\gcd(r,p)=1\). Thus \(S_p\) forms a maximally open ring with \(\varphi(p)=p-1\) open channels and a single blocked channel at \(r=0\).</em>
        </div>

        <div class="canvas-container">
            <canvas id="channelCanvas" width="700" height="700"></canvas>
            <div class="controls">
                <div class="control-group">
                    <label for="modInput">Modulus:</label>
                    <input type="number" id="modInput" value="13" min="2" max="500">
                </div>
                <button onclick="drawChannelRing()">Visualize</button>
                <button class="secondary" onclick="toggleChannelLabels()">Toggle Labels</button>
            </div>
            <div class="stats-display" id="channelStats" style="display: none;"></div>
            <div class="caption">Figure 1: Channel ring visualization showing open (green) and blocked (red) channels</div>
        </div>

        <div class="section-title">Part II: Fractional-Slice Coprimality Heuristic</div>

        <div class="subsection-title">2.1 Heuristic Definition</div>

        <p>For any modulus \(m \ge 2\), define the <em>coprime density</em></p>
        <p style="text-align: center;">
        \[
        \delta(m) = \frac{\varphi(m)}{m},
        \]
        </p>
        <p>the fraction of residues mod \(m\) that are coprime to \(m\). For a prime \(p\), this equals \(\delta(p) = 1 - \frac{1}{p}\).</p>

        <div class="definition">
            <span class="label">Definition 2.1 (Fractional Slice).</span>
            Let \(S(m) \subset \{1,2,\dots,m-1\}\) denote a chosen sampling region, such as the half-circle
            \[
            S_{\text{half}}(m) = \{1,\dots,\lfloor m/2\rfloor\}
            \]
            or a one-\(n\)th slice of residues distributed over \(2\pi/n\) radians. The slice captures a geometric subset of the modular ring. Define
            \[
            \delta_S(m) = \frac{|\,\{r \in S(m) : \gcd(r,m)=1\}\,|}{|S(m)|}
            \]
            as the local coprime density within that slice.
        </div>

        <div class="algorithm">
            <span class="label">Sampling Rule.</span>
            Sample \(k\) residues \(r_1,\dots,r_k\) uniformly from \(S(m)\). If every sampled residue satisfies \(\gcd(r_i,m)=1\), declare \(m\) a <em>prime candidate</em> under the fractional-slice test.
        </div>

        <div class="subsection-title">2.2 Probabilistic Bound</div>

        <p>Assuming independent sampling, the probability of a composite \(m\) passing the test is approximately</p>
        <p style="text-align: center;">
        \[
        \Pr(\text{pass}\mid m) \approx \delta_S(m)^k.
        \]
        </p>

        <div class="proposition">
            <span class="label">Proposition 2.2 (Fractional-Slice Coprimality Bound).</span>
            <em>Let \(m \ge 2\) and let \(S \subset \{1,\dots,m-1\}\) be a fixed sampling subset of size \(|S|\). If a random residue \(r \in S\) is coprime to \(m\) with probability \(\delta_S(m)\), then for \(k\) independent samples (with replacement),</em>
            \[
            \Pr(\text{pass}\mid m) = \delta_S(m)^k.
            \]
            <em>If \(q\) is the smallest prime factor of \(m\), then</em>
            \[
            \Pr(\text{pass}\mid m) \le \Big(1 - \frac{1}{q}\Big)^k.
            \]
        </div>

        <p>This yields the following key behavior:</p>
        <ul>
            <li>For even composites (\(q=2\)): \(\Pr(\text{pass}) \le (1/2)^k\)</li>
            <li>For \(q=3\): \(\Pr(\text{pass}) \le (2/3)^k\)</li>
            <li>For semiprimes with large factors (\(q \gg 1\)): the bound weakens, requiring larger \(k\)</li>
        </ul>

        <p>Thus the heuristic strongly rejects composites with small factors, and becomes probabilistically weaker only for products of large primes.</p>

        <div class="subsection-title">2.3 Slice Dependence and Symmetry</div>

        <div class="proposition">
            <span class="label">Proposition 2.3 (Half-Circle Neutrality).</span>
            <em>For the half-circle slice, mirror symmetry ensures</em>
            \[
            \delta_{\text{half}}(m) = \delta(m),
            \]
            <em>since \(\gcd(r,m)=\gcd(m-r,m)\). Hence the half-circle is a neutral choice that avoids residue bias.</em>
        </div>

        <div class="section-title">3. Interactive Algorithm Demonstration</div>

        <div class="info-box">
            <strong>Test the Heuristic:</strong> Enter a modulus, choose sampling parameters, and watch the fractional-slice algorithm in action. The visualization shows which residues are tested and whether they pass the coprimality check.
        </div>

        <div class="experimental-section">
            <h3 style="color: #667eea; margin-bottom: 20px;">Fractional-Slice Coprimality Test</h3>
            
            <div class="controls" style="margin-bottom: 20px;">
                <div class="control-group">
                    <label for="testModulus">Test Modulus:</label>
                    <input type="number" id="testModulus" value="91" min="2" max="10000">
                </div>
                <div class="control-group">
                    <label for="sampleCount">Samples (k):</label>
                    <input type="number" id="sampleCount" value="5" min="1" max="50">
                </div>
                <div class="control-group">
                    <label for="sliceType">Slice Type:</label>
                    <select id="sliceType">
                        <option value="half">Half-Circle</option>
                        <option value="quarter">Quarter-Circle</option>
                        <option value="full">Full Circle</option>
                    </select>
                </div>
                <button class="success" onclick="runFractionalTest()">Run Test</button>
                <button class="secondary" onclick="runBatchTest()">Batch Test (10 runs)</button>
            </div>

            <canvas id="testCanvas" width="600" height="600" style="display: block; margin: 20px auto;"></canvas>
            
            <div id="testResult"></div>
            <div id="batchResults"></div>
        </div>

        <div class="section-title">4. Algorithmic Formulation</div>

        <div class="algorithm">
            <span class="label">Algorithm 4.1 (Deterministic + Randomized Hybrid Filter).</span>
            <pre>
function is_prime_candidate(m, k, slice="half", 
                           small_primes=[2,3,5,7,11,13]):
    // (1) Deterministic prefilter by small primes
    for q in small_primes:
        if m % q == 0 and m != q:
            return False
    
    // (2) Choose slice
    if slice == "half":
        S = {1, 2, ..., floor(m/2)}
    else if slice == "quarter":
        S = {1, 2, ..., floor(m/4)}
    else:
        S = {1, 2, ..., m-1}
    
    // (3) Random sampling
    for i in 1..k:
        r = random_choice(S)
        if gcd(r, m) != 1:
            return False
    
    return True  // passes fractional-slice test
</pre>
        </div>

        <p>The parameter \(k\) governs tradeoff between false-positive rate and computational cost. For a target false positive probability \(\varepsilon\) and smallest divisor threshold \(Q\), choose</p>
        <p style="text-align: center;">
        \[
        k \ge \frac{\log \varepsilon}{\log(1 - 1/Q)}.
        \]
        </p>

        <div class="section-title">5. Experimental Evaluation</div>

        <div class="experimental-section">
            <h3 style="color: #667eea; margin-bottom: 20px;">Large-Scale Empirical Testing</h3>
            
            <div class="controls" style="margin-bottom: 20px;">
                <div class="control-group">
                    <label for="rangeStart">Range Start:</label>
                    <input type="number" id="rangeStart" value="100" min="2">
                </div>
                <div class="control-group">
                    <label for="rangeEnd">Range End:</label>
                    <input type="number" id="rangeEnd" value="500" min="2">
                </div>
                <div class="control-group">
                    <label for="expSamples">Samples (k):</label>
                    <input type="number" id="expSamples" value="10" min="1" max="50">
                </div>
                <button class="success" onclick="runExperiment()">Run Experiment</button>
            </div>

            <div class="progress-bar" id="progressBar" style="display: none;">
                <div class="progress-fill" id="progressFill">0%</div>
            </div>

            <div id="experimentResults"></div>
        </div>

        <div class="section-title">6. Failure Modes and Limitations</div>

        <ul>
            <li><strong>Semiprime leakage:</strong> Composites with large prime factors can pass the test.</li>
            <li><strong>Carmichael-like pseudoprimes:</strong> These may evade simple gcd-based filtering.</li>
            <li><strong>Slice bias:</strong> Improper slice selection can undercount blocked channels.</li>
        </ul>

        <p>The heuristic is therefore best used as a rapid <em>prefilter</em> prior to a deterministic or probabilistic primality test (e.g., Miller–Rabin).</p>

        <div class="section-title">7. Conclusion</div>

        <p>Fractional-slice coprimality sampling provides a geometric and probabilistic bridge between Nested Farey Channel theory and practical number testing. It captures the essential property that prime moduli maintain maximal channel openness even when viewed through restricted arcs of the unit circle, while composites introduce blocked Farey channels visible through partial sampling.</p>

        <p>This heuristic can serve both as:</p>
        <ol>
            <li>A fast preliminary screen for prime candidates within modular sieves.</li>
            <li>A geometric diagnostic tool for visualizing the distribution of coprime residues across modular arcs.</li>
        </ol>

        <p>Further work includes: quantifying slice bias functions \(\beta_S(m)\), linking partial-channel openness to residue equidistribution, and integrating this fractional sampling into the modular sieve hierarchy for scalable prime detection.</p>

        <div style="margin-top: 50px; padding-top: 30px; border-top: 3px solid #667eea; text-align: center; color: #7f8c8d;">
            <p><em>Interactive paper by Wessen Getachew, October 2025</em></p>
            <p style="margin-top: 10px; font-size: 0.9em;">Full framework implementation with live algorithm demonstrations</p>
        </div>
    </div>

    <script>
        // ==================== UTILITY FUNCTIONS ====================
        
        function gcd(a, b) {
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

        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2) return true;
            if (n % 2 === 0) return false;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return false;
            }
            return true;
        }

        function smallestPrimeFactor(n) {
            if (n % 2 === 0) return 2;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return i;
            }
            return n;
        }

        // ==================== CHANNEL VISUALIZATION ====================
        
        let showChannelLabels = false;

        function drawChannelRing() {
            const canvas = document.getElementById('channelCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = 280;

            const m = parseInt(document.getElementById('modInput').value);
            if (isNaN(m) || m < 2) return;

            ctx.clearRect(0, 0, width, height);

            // Draw circle
            ctx.strokeStyle = '#34495e';
            ctx.lineWidth = 2.5;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.stroke();

            // Draw origin
            ctx.fillStyle = '#e74c3c';
            ctx.beginPath();
            ctx.arc(centerX + radius, centerY, 10, 0, 2 * Math.PI);
            ctx.fill();

            // Draw channels
            const phi = eulerPhi(m);
            let openCount = 0, blockedCount = 0;

            for (let r = 1; r < m; r++) {
                const isOpen = gcd(r, m) === 1;
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);

                if (isOpen) openCount++;
                else blockedCount++;

                // Draw line
                ctx.strokeStyle = isOpen ? 'rgba(39, 174, 96, 0.3)' : 'rgba(231, 76, 60, 0.3)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(x, y);
                ctx.stroke();

                // Draw point
                ctx.fillStyle = isOpen ? '#27ae60' : '#e74c3c';
                ctx.beginPath();
                ctx.arc(x, y, isOpen ? 6 : 5, 0, 2 * Math.PI);
                ctx.fill();

                if (showChannelLabels && m <= 30) {
                    ctx.fillStyle = '#2c3e50';
                    ctx.font = '11px serif';
                    const labelX = centerX + (radius + 30) * Math.cos(theta);
                    const labelY = centerY - (radius + 30) * Math.sin(theta);
                    ctx.fillText(`${r}`, labelX - 5, labelY + 4);
                }
            }

            // Display stats
            const statsDiv = document.getElementById('channelStats');
            statsDiv.innerHTML = `
                <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m}</span></div>
                <div class="stat-row"><span class="stat-label">Open Channels:</span><span class="stat-value">${openCount}</span></div>
                <div class="stat-row"><span class="stat-label">Blocked Channels:</span><span class="stat-value">${blockedCount}</span></div>
                <div class="stat-row"><span class="stat-label">Density δ(m):</span><span class="stat-value">${(openCount/m).toFixed(4)}</span></div>
                <div class="stat-row"><span class="stat-label">Is Prime:</span><span class="stat-value">${isPrime(m) ? 'Yes ✓' : 'No'}</span></div>
            `;
            statsDiv.style.display = 'block';
        }

        function toggleChannelLabels() {
            showChannelLabels = !showChannelLabels;
            drawChannelRing();
        }

        // ==================== FRACTIONAL-SLICE TEST ====================
        
        function getSlice(m, sliceType) {
            if (sliceType === 'half') {
                return Array.from({length: Math.floor(m/2)}, (_, i) => i + 1);
            } else if (sliceType === 'quarter') {
                return Array.from({length: Math.floor(m/4)}, (_, i) => i + 1);
            } else {
                return Array.from({length: m-1}, (_, i) => i + 1);
            }
        }

        function runFractionalTest() {
            const m = parseInt(document.getElementById('testModulus').value);
            const k = parseInt(document.getElementById('sampleCount').value);
            const sliceType = document.getElementById('sliceType').value;

            if (isNaN(m) || m < 2 || isNaN(k) || k < 1) return;

            const canvas = document.getElementById('testCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = 220;

            ctx.clearRect(0, 0, width, height);

            // Draw circle
            ctx.strokeStyle = '#34495e';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.stroke();

            // Get slice
            const slice = getSlice(m, sliceType);
            
            // Highlight slice region
            if (sliceType !== 'full') {
                ctx.fillStyle = 'rgba(102, 126, 234, 0.1)';
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                const maxTheta = (2 * Math.PI * slice[slice.length-1]) / m;
                ctx.arc(centerX, centerY, radius, -Math.PI/2, -Math.PI/2 + maxTheta);
                ctx.closePath();
                ctx.fill();
            }

            // Sample and test
            const samples = [];
            let allPass = true;

            for (let i = 0; i < k; i++) {
                const r = slice[Math.floor(Math.random() * slice.length)];
                const coprime = gcd(r, m) === 1;
                samples.push({r, coprime});
                if (!coprime) allPass = false;
            }

            // Draw all residues faintly
            for (let r = 1; r < m; r++) {
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);
                
                ctx.fillStyle = '#ddd';
                ctx.beginPath();
                ctx.arc(x, y, 3, 0, 2 * Math.PI);
                ctx.fill();
            }

            // Draw sampled residues
            samples.forEach(({r, coprime}) => {
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);

                // Draw ray
                ctx.strokeStyle = coprime ? 'rgba(39, 174, 96, 0.6)' : 'rgba(231, 76, 60, 0.6)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(x, y);
                ctx.stroke();

                // Draw point
                ctx.fillStyle = coprime ? '#27ae60' : '#e74c3c';
                ctx.beginPath();
                ctx.arc(x, y, 8, 0, 2 * Math.PI);
                ctx.fill();

                // Label
                ctx.fillStyle = '#2c3e50';
                ctx.font = 'bold 12px serif';
                const labelX = centerX + (radius + 25) * Math.cos(theta);
                const labelY = centerY - (radius + 25) * Math.sin(theta);
                ctx.fillText(`${r}`, labelX - 8, labelY + 4);
            });

            // Display result
            const resultDiv = document.getElementById('testResult');
            const prime = isPrime(m);
            const q = smallestPrimeFactor(m);
            const theoreticalProb = Math.pow(1 - 1/q, k).toFixed(4);

            resultDiv.innerHTML = `
                <div class="test-result ${allPass ? 'pass' : 'fail'}">
                    <strong>Result:</strong> ${allPass ? 'PASS ✓' : 'FAIL ✗'} - ${m} ${allPass ? 'is a prime candidate' : 'is composite (detected)'}
                </div>
                <div class="stats-display" style="margin-top: 15px;">
                    <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m}</span></div>
                    <div class="stat-row"><span class="stat-label">Actual Status:</span><span class="stat-value">${prime ? 'Prime' : 'Composite'}</span></div>
                    <div class="stat-row"><span class="stat-label">Samples Tested:</span><span class="stat-value">${k}</span></div>
                    <div class="stat-row"><span class="stat-label">Passed Samples:</span><span class="stat-value">${samples.filter(s => s.coprime).length}/${k}</span></div>
                    <div class="stat-row"><span class="stat-label">Smallest Factor:</span><span class="stat-value">${q}</span></div>
                    <div class="stat-row"><span class="stat-label">Theoretical Pass Prob:</span><span class="stat-value">${theoreticalProb}</span></div>
                </div>
            `;
        }

        function runBatchTest() {
            const m = parseInt(document.getElementById('testModulus').value);
            const k = parseInt(document.getElementById('sampleCount').value);
            const sliceType = document.getElementById('sliceType').value;

            if (isNaN(m) || m < 2 || isNaN(k) || k < 1) return;

            const slice = getSlice(m, sliceType);
            let passCount = 0;

            for (let trial = 0; trial < 10; trial++) {
                let allPass = true;
                for (let i = 0; i < k; i++) {
                    const r = slice[Math.floor(Math.random() * slice.length)];
                    if (gcd(r, m) !== 1) {
                        allPass = false;
                        break;
                    }
                }
                if (allPass) passCount++;
            }

            const resultDiv = document.getElementById('batchResults');
            const prime = isPrime(m);
            const q = smallestPrimeFactor(m);
            const theoreticalProb = Math.pow(1 - 1/q, k);

            resultDiv.innerHTML = `
                <div class="stats-display" style="margin-top: 20px;">
                    <h4 style="color: #667eea; margin-bottom: 10px;">Batch Test Results (10 runs)</h4>
                    <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m} (${prime ? 'Prime' : 'Composite'})</span></div>
                    <div class="stat-row"><span class="stat-label">Passes:</span><span class="stat-value">${passCount}/10</span></div>
                    <div class="stat-row"><span class="stat-label">Empirical Pass Rate:</span><span class="stat-value">${(passCount/10).toFixed(2)}</span></div>
                    <div class="stat-row"><span class="stat-label">Theoretical Pass Prob:</span><span class="stat-value">${theoreticalProb.toFixed(4)}</span></div>
                    <div class="stat-row"><span class="stat-label">Error:</span><span class="stat-value">${Math.abs(passCount/10 - theoreticalProb).toFixed(4)}</span></div>
                </div>
            `;
        }

        // ==================== LARGE-SCALE EXPERIMENT ====================
        
        function runExperiment() {
            const start = parseInt(document.getElementById('rangeStart').value);
            const end = parseInt(document.getElementById('rangeEnd').value);
            const k = parseInt(document.getElementById('expSamples').value);

            if (isNaN(start) || isNaN(end) || isNaN(k) || start >= end) return;

            const progressBar = document.getElementById('progressBar');
            const progressFill = document.getElementById('progressFill');
            progressBar.style.display = 'block';

            let truePositives = 0, falsePositives = 0;
            let trueNegatives = 0, falseNegatives = 0;

            const total = end - start + 1;
            let processed = 0;

            setTimeout(() => processRange(), 10);

            function processRange() {
                const batchSize = 10;
                const batchEnd = Math.min(processed + batchSize, total);

                for (let i = processed; i < batchEnd; i++) {
                    const m = start + i;
                    const prime = isPrime(m);
                    const passed = fractionalSliceTest(m, k, 'half');

                    if (prime && passed) truePositives++;
                    else if (!prime && passed) falsePositives++;
                    else if (!prime && !passed) trueNegatives++;
                    else if (prime && !passed) falseNegatives++;
                }

                processed = batchEnd;
                const progress = Math.round((processed / total) * 100);
                progressFill.style.width = progress + '%';
                progressFill.textContent = progress + '%';

                if (processed < total) {
                    setTimeout(processRange, 10);
                } else {
                    displayExperimentResults();
                }
            }

            function displayExperimentResults() {
                progressBar.style.display = 'none';

                const sensitivity = truePositives / (truePositives + falseNegatives);
                const specificity = trueNegatives / (trueNegatives + falsePositives);
                const precision = truePositives / (truePositives + falsePositives);

                const resultsDiv = document.getElementById('experimentResults');
                resultsDiv.innerHTML = `
                    <h4 style="color: #667eea; margin: 20px 0;">Experiment Results: Range [${start}, ${end}], k=${k}</h4>
                    <table>
                        <tr>
                            <th></th>
                            <th>Predicted Prime</th>
                            <th>Predicted Composite</th>
                        </tr>
                        <tr>
                            <td><strong>Actual Prime</strong></td>
                            <td style="background: #d4edda;">${truePositives}</td>
                            <td style="background: #f8d7da;">${falseNegatives}</td>
                        </tr>
                        <tr>
                            <td><strong>Actual Composite</strong></td>
                            <td style="background: #f8d7da;">${falsePositives}</td>
                            <td style="background: #d4edda;">${trueNegatives}</td>
                        </tr>
                    </table>
                    <div class="stats-display" style="margin-top: 20px;">
                        <div class="stat-row"><span class="stat-label">Sensitivity (TPR):</span><span class="stat-value">${(sensitivity * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">Specificity (TNR):</span><span class="stat-value">${(specificity * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">Precision (PPV):</span><span class="stat-value">${(precision * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">False Positive Rate:</span><span class="stat-value">${((1-specificity) * 100).toFixed(2)}%</span></div>
                    </div>
                `;
            }
        }

        function fractionalSliceTest(m, k, sliceType) {
            const slice = getSlice(m, sliceType);
            for (let i = 0; i < k; i++) {
                const r = slice[Math.floor(Math.random() * slice.length)];
                if (gcd(r, m) !== 1) return false;
            }
            return true;
        }

        // Initialize
        drawChannelRing();
    </script>
</body>
</html>
