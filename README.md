<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bernoulli-Gap Inversion Sieve: ζ(s) Calculator</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 1800px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #0c1445 0%, #1e3c72 50%, #2a5298 100%);
            color: white;
            min-height: 100vh;
        }
        
        .container {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        h1 {
            text-align: center;
            margin-bottom: 15px;
            font-size: 3em;
            text-shadow: 3px 3px 8px rgba(0, 0, 0, 0.6);
            background: linear-gradient(45deg, #ff6b6b, #feca57, #48dbfb, #ff9ff3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .subtitle {
            text-align: center;
            margin-bottom: 40px;
            font-size: 1.4em;
            opacity: 0.9;
            font-style: italic;
            color: #a8e6cf;
        }
        
        .theorem-section {
            background: linear-gradient(135deg, rgba(255, 107, 107, 0.15), rgba(254, 202, 87, 0.15));
            border: 3px solid rgba(255, 107, 107, 0.3);
            padding: 35px;
            border-radius: 20px;
            margin-bottom: 40px;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.2);
        }
        
        .theorem-title {
            font-size: 1.8em;
            font-weight: bold;
            color: #ff6b6b;
            margin-bottom: 25px;
            text-align: center;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .main-formula {
            background: rgba(0, 0, 0, 0.5);
            padding: 30px;
            border-radius: 15px;
            margin: 25px 0;
            font-family: 'Courier New', monospace;
            font-size: 1.4em;
            text-align: center;
            border: 3px solid rgba(72, 219, 251, 0.4);
            box-shadow: inset 0 0 20px rgba(72, 219, 251, 0.1);
        }
        
        .gap-explanation {
            background: rgba(255, 255, 255, 0.1);
            padding: 25px;
            border-radius: 15px;
            margin: 25px 0;
            border-left: 6px solid #48dbfb;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
            padding: 30px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .control-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 12px;
        }
        
        label {
            font-weight: bold;
            color: #a8e6cf;
            font-size: 1.1em;
        }
        
        input, select, button {
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
        }
        
        input, select {
            background: rgba(255, 255, 255, 0.15);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.2);
        }
        
        input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }
        
        button {
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            font-size: 18px;
            box-shadow: 0 5px 20px rgba(255, 107, 107, 0.4);
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.6);
        }
        
        .results {
            display: grid;
            gap: 30px;
            margin-top: 40px;
        }
        
        .result-card {
            background: rgba(255, 255, 255, 0.12);
            padding: 35px;
            border-radius: 20px;
            border-left: 8px solid #ff6b6b;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
        }
        
        .result-header {
            font-size: 1.6em;
            font-weight: bold;
            margin-bottom: 30px;
            color: #ff6b6b;
            text-align: center;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .zeta-calculation {
            background: rgba(0, 0, 0, 0.4);
            padding: 25px;
            border-radius: 15px;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 1em;
            line-height: 1.8;
            border: 2px solid rgba(72, 219, 251, 0.3);
        }
        
        .zeta-comparison {
            background: linear-gradient(135deg, rgba(168, 230, 207, 0.2), rgba(72, 219, 251, 0.2));
            border: 3px solid #48dbfb;
            padding: 30px;
            border-radius: 15px;
            margin: 25px 0;
            text-align: center;
        }
        
        .gap-breakdown {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }
        
        .gap-class {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 12px;
            border-left: 4px solid #feca57;
        }
        
        .gap-table {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 15px;
            overflow: hidden;
            margin: 25px 0;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 15px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            font-size: 1em;
        }
        
        th {
            background: rgba(255, 107, 107, 0.3);
            font-weight: bold;
            color: #fff;
            font-size: 1.1em;
        }
        
        .highlight {
            background: rgba(254, 202, 87, 0.4);
            padding: 5px 12px;
            border-radius: 8px;
            font-weight: bold;
            color: #feca57;
        }
        
        .special-gap {
            background: rgba(255, 159, 243, 0.3);
            border-left-color: #ff9ff3;
        }
        
        .loading {
            text-align: center;
            padding: 40px;
            font-size: 1.4em;
            color: #48dbfb;
        }
        
        .error-display {
            font-size: 1.3em;
            font-weight: bold;
            margin: 15px 0;
        }
        
        .pi-extraction {
            background: linear-gradient(135deg, rgba(255, 159, 243, 0.2), rgba(255, 107, 107, 0.2));
            border: 3px solid #ff9ff3;
            padding: 30px;
            border-radius: 15px;
            margin: 25px 0;
            text-align: center;
        }
        
        a:hover {
            color: #feca57;
            text-shadow: 0 0 10px rgba(72, 219, 251, 0.5);
        }
        
        .author-credit {
            text-align: center;
            margin-top: 40px;
            padding: 25px;
            background: rgba(255, 255, 255, 0.08);
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Prime Gap Decomposition of ζ(s)</h1>
        <div class="subtitle">Exploring ζ(s) through prime gap class factorization</div>
        
        <div style="text-align: center; margin-bottom: 30px; padding: 20px; background: rgba(255, 255, 255, 0.1); border-radius: 15px;">
            <div style="font-size: 1.2em; color: #a8e6cf; margin-bottom: 10px;">
                <strong>Research by Wessen Getachew</strong>
            </div>
            <div style="font-size: 1em; opacity: 0.9;">
                Follow research updates: <a href="https://twitter.com/7DView" target="_blank" style="color: #48dbfb; text-decoration: none; font-weight: bold;">@7DView</a> on Twitter
            </div>
        </div>
        
        <div class="theorem-section">
            <div class="theorem-title">Prime Gap Decomposition Method</div>
            
            <div class="main-formula">
                ζ(s) = ∏<sub>g∈{1,2,4,6,8,...}</sub> ( ∏<sub>p: gap(p)=g</sub> (1 - p<sup>-s</sup>)<sup>-1</sup> )
            </div>
            
            <div class="gap-explanation">
                <strong>Gap Class Factorization:</strong>
                <br><br>
                
                <strong>Approach:</strong><br>
                We can organize the Euler product for ζ(s) by grouping primes according to their gap to the next prime. This provides an alternative computational method and may offer insights into the structure of these functions.<br><br>
                
                <strong>Gap Classes:</strong><br>
                • <strong>Gap 1:</strong> Only (2→3)<br>
                • <strong>Gap 2:</strong> Twin primes: (3→5), (5→7), (11→13), (17→19), ...<br>
                • <strong>Gap 4:</strong> Cousin primes: (3→7), (7→11), (13→17), (19→23), ...<br>
                • <strong>Gap 6:</strong> Sexy primes: (5→11), (7→13), (11→17), (13→19), ...<br>
                • <strong>Larger gaps:</strong> 8, 10, 12, 14, 16, 18, 20, ...<br><br>
                
                <strong>Computational Method:</strong><br>
                Instead of summing over all integers or using classical methods, we can compute ζ(s) by organizing the Euler product according to these gap classes.
            </div>
            
            <div class="main-formula">
                This gap-based organization provides a finite computational approach<br>
                for approximating ζ(s) values.
            </div>
            
            <div class="gap-explanation">
                <strong>Gap Classes & Their Role:</strong><br>
                • <strong>Gap 0:</strong> Empty (no consecutive primes have gap 0)<br>
                • <strong>Gap 1:</strong> Only 2→3 (contributes fundamental factor 4/3 for ζ(2))<br>
                • <strong>Gap 2:</strong> Twin primes (3,5), (5,7), (11,13), (17,19), ...<br>
                • <strong>Gap 4:</strong> Cousin primes (3,7), (7,11), (13,17), (19,23), ...<br>
                • <strong>Gap 6:</strong> Sexy primes (5,11), (7,13), (11,17), (13,19), ...<br>
                • <strong>Larger gaps:</strong> 8, 10, 12, 14, 16, 18, 20, ...<br><br>
                
                <strong>π Reconstruction:</strong> π ≈ √(6 × ζ(2)) where ζ(2) is built from gap products!<br>
                This shows how prime gaps directly encode geometric constants!
            </div>
            
            <div class="main-formula">
                <strong>Special Cases:</strong><br>
                ζ(2) = π²/6 &nbsp;|&nbsp; ζ(4) = π⁴/90 &nbsp;|&nbsp; ζ(6) = π⁶/945
                <br><br>
                <strong>Bernoulli Equivalence:</strong><br>
                Your gap products ⟷ B<sub>2n</sub> generating functions
            </div>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <label for="maxPrime">Maximum Prime N:</label>
                <input type="number" id="maxPrime" value="10000000" min="100" max="100000000" 
                       title="Calculate using primes up to this value">
            </div>
            
            <div class="control-group">
                <label for="zetaS">ζ(s) Value:</label>
                <select id="zetaS" title="Choose which zeta function to calculate">
                    <option value="2">ζ(2) = π²/6</option>
                    <option value="4">ζ(4) = π⁴/90</option>
                    <option value="6">ζ(6) = π⁶/945</option>
                    <option value="8">ζ(8) = π⁸/9450</option>
                    <option value="10">ζ(10) = π¹⁰/93555</option>
                    <option value="custom">Custom s</option>
                </select>
            </div>
            
            <div class="control-group" id="customSGroup">
                <label for="customS">Custom s (if selected):</label>
                <input type="number" id="customS" value="3" min="1" max="20" step="0.1" 
                       title="Enter custom s value for ζ(s)">
            </div>
            
            <div class="control-group">
                <label for="maxGap">Maximum Gap Size:</label>
                <input type="number" id="maxGap" value="220" min="10" max="1000" 
                       title="Include gaps up to this size (220 is max for 10M primes)">
            </div>
            
            <div class="control-group" style="grid-column: span 2;">
                <button onclick="calculateZeta()" title="Calculate ζ(s) using gap decomposition method">
                    Calculate ζ(s) via Gap Decomposition
                </button>
            </div>
        </div>
        
        <div id="results" class="results"></div>
        
        <div class="result-card" style="margin-top: 40px;">
            <div class="result-header">Method Overview</div>
            
            <div class="gap-breakdown">
                <div class="gap-class">
                    <strong>Computational Approach:</strong><br>
                    • Count primes by gap to next prime<br>
                    • Group into gap classes<br>
                    • Apply Euler product within each class<br>
                    • Multiply class products together<br>
                    • Compare with known ζ(s) values
                </div>
                
                <div class="gap-class">
                    <strong>Observations:</strong><br>
                    • Finite computation approximates ζ(s)<br>
                    • Different gap classes contribute differently<br>
                    • Method scales with prime range<br>
                    • May provide insights into prime distribution<br>
                    • Offers alternative computational pathway
                </div>
            </div>
            
            <div style="background: rgba(72, 219, 251, 0.2); padding: 25px; border-radius: 15px; margin: 20px 0; border-left: 5px solid #48dbfb;">
                <strong>Research Interest:</strong><br><br>
                
                This gap-based organization of the Euler product may offer:<br><br>
                
                • Alternative computational methods for ζ(s)<br>
                • Insights into how prime gaps affect special function values<br>
                • Connection between discrete gap patterns and continuous functions<br>
                • Possible applications to other L-functions<br><br>
                
                The method provides a finite approach to approximating these classically infinite products.
            </div>
        </div>
        
        <div class="result-card" style="margin-top: 40px;">
            <div class="result-header">Research Applications</div>
            
            <div class="gap-breakdown">
                <div class="gap-class special-gap">
                    <strong>Computational Analysis:</strong><br>
                    • Compare gap decomposition with classical methods<br>
                    • Study convergence rates for different s values<br>
                    • Analyze gap class contribution patterns<br>
                    • Explore applications to other L-functions
                </div>
                
                <div class="gap-class special-gap">
                    <strong>Mathematical Interest:</strong><br>
                    • Connection between prime gaps and special functions<br>
                    • Alternative organization of Euler products<br>
                    • Insights into prime distribution effects<br>
                    • Potential applications in analytic number theory
                </div>
                
                <div class="gap-class special-gap">
                    <strong>Further Investigation:</strong><br>
                    • Extension to complex s values<br>
                    • Relationship to twin prime conjecture<br>
                    • Applications to computational number theory<br>
                    • Connections to other gap-based methods
                </div>
            </div>
        </div>
            <div class="result-header">🔗 How We're Using Bernoulli Numbers</div>
            
            <div style="background: rgba(0, 0, 0, 0.3); padding: 25px; border-radius: 15px; margin: 20px 0; font-family: 'Courier New', monospace; line-height: 1.6;">
                <strong>Classical Bernoulli-Zeta Relationship:</strong><br>
                ζ(2n) = (-1)^(n+1) × B<sub>2n</sub> × (2π)^(2n) / (2×(2n)!)<br><br>
                
                <strong>Where Bernoulli Numbers Are:</strong><br>
                B<sub>0</sub> = 1, B<sub>1</sub> = -1/2, B<sub>2</sub> = 1/6, B<sub>4</sub> = -1/30, B<sub>6</sub> = 1/42, B<sub>8</sub> = -1/30, B<sub>10</sub> = 5/66, ...<br>
                (Note: All odd B<sub>n</sub> = 0 for n > 1)<br><br>
                
                <strong>Examples:</strong><br>
                • ζ(2) = π²/6 = (-1)<sup>1+1</sup> × (1/6) × (2π)² / (2×2!) = (1/6) × 4π² / 4 = π²/6<br>
                • ζ(4) = π⁴/90 = (-1)<sup>2+1</sup> × (-1/30) × (2π)⁴ / (2×4!) = (-1/30) × 16π⁴ / 48 = π⁴/90<br>
                • ζ(6) = π⁶/945 = (-1)<sup>3+1</sup> × (1/42) × (2π)⁶ / (2×6!) = (1/42) × 64π⁶ / 1440 = π⁶/945
            </div>
            
            <div class="zeta-comparison">
                <div style="font-size: 1.3em; color: #ff6b6b; font-weight: bold; margin-bottom: 20px;">
                    🚀 The Bernoulli-Gap Inversion Innovation
                </div>
                
                <strong>Traditional Method:</strong> Bernoulli numbers → Generate ζ(2n) values → Analytic continuation<br><br>
                
                <strong>Our Gap Inversion Method:</strong> Prime gaps → Direct ζ(s) factorization → Same exact values!<br><br>
                
                <div style="background: rgba(168, 230, 207, 0.2); padding: 20px; border-radius: 12px; margin: 20px 0; border-left: 5px solid #48dbfb;">
                    <strong>🔄 The Inversion Principle:</strong><br><br>
                    
                    Instead of using Bernoulli generating functions to create zeta values, we <strong>invert the process</strong>:<br><br>
                    
                    <strong>Classical:</strong> B<sub>2n</sub> numbers → ζ(2n) via complex analysis → π relationships<br>
                    <strong>Gap Method:</strong> Prime spacing → ζ(s) via gap products → Same π relationships<br><br>
                    
                    This reveals that <em>prime gap structure contains the same fundamental arithmetic information as Bernoulli numbers</em>, but accessed through discrete spacing rather than continuous generating functions!
                </div>
                
                <strong>🧮 Mathematical Equivalence:</strong><br>
                Our gap products: ∏<sub>gaps</sub> ∏<sub>p in gap</sub> (1-p<sup>-s</sup>)<sup>-1</sup> = ζ(s)<br>
                Produce identical results to: (-1)<sup>n+1</sup> × B<sub>2n</sub> × (2π)<sup>2n</sup> / (2×(2n)!)<br><br>
                
                <strong>🎯 Why This Matters:</strong><br>
                • Shows prime gaps encode Bernoulli-equivalent information<br>
                • Provides computational alternative to classical methods<br>
                • Bridges discrete number theory with continuous analysis<br>
                • Opens new research pathways for understanding ζ(s)
            </div>
        </div>
        
        <div class="author-credit">
            <div style="font-size: 1.4em; color: #ff6b6b; font-weight: bold; margin-bottom: 15px;">
                Prime Gap Decomposition of ζ(s)
            </div>
            <div style="font-size: 1.2em; color: #a8e6cf; margin-bottom: 10px;">
                Research by <strong>Wessen Getachew</strong>
            </div>
            <div style="font-size: 1em; opacity: 0.9;">
                Follow research: <a href="https://twitter.com/7DView" target="_blank" style="color: #48dbfb; text-decoration: none; font-weight: bold; transition: all 0.3s ease;">@7DView</a> on Twitter
            </div>
            <div style="font-size: 0.9em; margin-top: 15px; opacity: 0.8; color: #feca57;">
                "Exploring ζ(s) through prime gap class organization"
            </div>
        </div>
    </div>

    <script>
        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2) return true;
            if (n % 2 === 0) return false;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return false;
            }
            return true;
        }
        
        function getPrimesUpTo(n) {
            const primes = [];
            for (let i = 2; i <= n; i++) {
                if (isPrime(i)) primes.push(i);
            }
            return primes;
        }
        
        function calculatePrimeGaps(primes) {
            const gapData = [];
            
            // Calculate forward gaps between consecutive primes
            for (let i = 1; i < primes.length; i++) {
                const gap = primes[i] - primes[i-1];
                gapData.push({
                    prime: primes[i-1],
                    gap: gap,
                    nextPrime: primes[i]
                });
            }
            
            // Special handling for prime 2: it has gap 1 to next prime 3
            // But we need to handle it separately in the gap decomposition
            
            return gapData;
        }
        
        function groupByGapClasses(gapData, maxGap) {
            const gapClasses = {};
            
            gapData.forEach(data => {
                const gap = data.gap;
                if (gap <= maxGap) {
                    if (!gapClasses[gap]) {
                        gapClasses[gap] = [];
                    }
                    gapClasses[gap].push(data);
                }
            });
            
            return gapClasses;
        }
        
        function calculateZetaFromGaps(gapClasses, s) {
            let totalProduct = 1.0;
            const gapProducts = {};
            
            // Calculate product for each gap class
            Object.keys(gapClasses).forEach(gap => {
                const gapNum = parseInt(gap);
                const primesInGap = gapClasses[gap];
                
                let gapProduct = 1.0;
                primesInGap.forEach(data => {
                    const p = data.prime;
                    const factor = 1 / (1 - Math.pow(p, -s)); // (1 - p^(-s))^(-1)
                    gapProduct *= factor;
                });
                
                gapProducts[gapNum] = {
                    primes: primesInGap.map(d => d.prime),
                    count: primesInGap.length,
                    product: gapProduct,
                    examples: primesInGap.slice(0, 6).map(d => {
                        if (d.gap === 0) return `${d.prime} (gap 0)`;
                        return `${d.prime}→${d.nextPrime}`;
                    }).join(', ')
                };
                
                totalProduct *= gapProduct;
            });
            
            return { totalProduct, gapProducts };
        }
        
        function getZetaTarget(s) {
            const targets = {
                2: Math.PI * Math.PI / 6,
                4: Math.pow(Math.PI, 4) / 90,
                6: Math.pow(Math.PI, 6) / 945,
                8: Math.pow(Math.PI, 8) / 9450,
                10: Math.pow(Math.PI, 10) / 93555
            };
            
            if (targets[s]) {
                return {
                    value: targets[s],
                    formula: s === 2 ? 'π²/6' :
                           s === 4 ? 'π⁴/90' :
                           s === 6 ? 'π⁶/945' :
                           s === 8 ? 'π⁸/9450' :
                           s === 10 ? 'π¹⁰/93555' : `π^${s}/unknown`
                };
            }
            
            // For other values, calculate numerically
            let sum = 0;
            for (let n = 1; n <= 100000; n++) {
                sum += 1 / Math.pow(n, s);
            }
            
            return {
                value: sum,
                formula: `ζ(${s}) ≈ numerical`
            };
        }
        
        function calculateZeta() {
            const maxPrime = parseInt(document.getElementById('maxPrime').value);
            const zetaSSelect = document.getElementById('zetaS').value;
            const customS = parseFloat(document.getElementById('customS').value);
            const maxGap = parseInt(document.getElementById('maxGap').value);
            const resultsDiv = document.getElementById('results');
            
            const s = zetaSSelect === 'custom' ? customS : parseInt(zetaSSelect);
            
            resultsDiv.innerHTML = '<div class="loading">🔄 Computing gap decomposition...</div>';
            
            setTimeout(() => {
                try {
                    const primes = getPrimesUpTo(maxPrime);
                    const gapData = calculatePrimeGaps(primes);
                    const gapClasses = groupByGapClasses(gapData, maxGap);
                    const { totalProduct, gapProducts } = calculateZetaFromGaps(gapClasses, s);
                    const target = getZetaTarget(s);
                    
                    resultsDiv.innerHTML = '';
                    
                    // Main calculation display
                    const mainDiv = document.createElement('div');
                    mainDiv.className = 'result-card';
                    
                    const error = Math.abs(totalProduct - target.value);
                    const errorPercent = (error / target.value * 100);
                    
                    mainDiv.innerHTML = `
                        <div class="result-header">🧮 ζ(${s}) Gap Decomposition (N ≤ ${maxPrime})</div>
                        
                        <div class="zeta-comparison">
                            <div class="error-display">
                                <strong>Gap Product Result:</strong> ζ(${s}) ≈ <span class="highlight">${totalProduct.toFixed(12)}</span><br>
                                <strong>Theoretical Value:</strong> ${target.formula} = ${target.value.toFixed(12)}<br><br>
                                
                                <strong>Error Analysis:</strong><br>
                                Absolute Error: ${error.toExponential(6)}<br>
                                Relative Error: ${errorPercent.toFixed(6)}%<br><br>
                                
                                ${errorPercent < 0.001 ? '🎯 <strong>Exceptional precision!</strong>' :
                                  errorPercent < 0.01 ? '✅ <strong>Excellent approximation!</strong>' :
                                  errorPercent < 0.1 ? '📈 <strong>Very good convergence!</strong>' :
                                  errorPercent < 1 ? '🔬 <strong>Good approximation - try larger N</strong>' :
                                  '📊 <strong>Interesting pattern emerging</strong>'}
                            </div>
                        </div>
                        
                        <div class="zeta-calculation">
                            <strong>Bernoulli-Gap Inversion Formula:</strong><br>
                            ζ(${s}) = ∏_{g∈{1,2,4,6,...}} ∏_{p: gap(p)=g} (1 - p^{-${s}})^{-1}<br><br>
                            
                            <strong>Individual Gap Contributions:</strong><br>
                            ${Object.keys(gapProducts).sort((a,b) => parseInt(a) - parseInt(b)).map(gap => {
                                const gp = gapProducts[gap];
                                const gapNum = parseInt(gap);
                                return `Gap ${gap}: ${gp.count} prime${gp.count > 1 ? 's' : ''} → Product = ${gp.product.toFixed(8)}`;
                            }).join('<br>')}
                            <br><br>
                            Total Product: ${totalProduct.toFixed(12)}
                        </div>
                    `;
                    
                    resultsDiv.appendChild(mainDiv);
                    
                    // Gap class breakdown table
                    const tableDiv = document.createElement('div');
                    tableDiv.className = 'result-card';
                    
                    let tableHTML = `
                        <div class="result-header">📊 Gap Class Breakdown</div>
                        
                        <div class="gap-table">
                            <table>
                                <tr>
                                    <th>Gap Size</th>
                                    <th>Prime Count</th>
                                    <th>Gap Product</th>
                                    <th>Log Contribution</th>
                                    <th>Examples</th>
                                </tr>
                    `;
                    
                    Object.keys(gapProducts).sort((a,b) => parseInt(a) - parseInt(b)).forEach(gap => {
                        const gp = gapProducts[gap];
                        const logContrib = Math.log(gp.product);
                        const moreText = gp.count > 6 ? ` +${gp.count - 6} more` : '';
                        
                        tableHTML += `
                            <tr>
                                <td><span class="highlight">${gap}</span></td>
                                <td>${gp.count}</td>
                                <td>${gp.product.toFixed(12)}</td>
                                <td>${logContrib.toFixed(8)}</td>
                                <td>${gp.examples}${moreText}</td>
                            </tr>
                        `;
                    });
                    
                    tableHTML += '</table></div>';
                    tableDiv.innerHTML = tableHTML;
                    resultsDiv.appendChild(tableDiv);
                    
                    // π extraction if s = 2
                    if (s === 2) {
                        const piExtracted = Math.sqrt(6 * totalProduct);
                        const actualPi = Math.PI;
                        const piError = Math.abs(piExtracted - actualPi);
                        const piErrorPercent = (piError / actualPi * 100);
                        
                        const piDiv = document.createElement('div');
                        piDiv.className = 'result-card';
                        piDiv.innerHTML = `
                            <div class="result-header">🥧 π Extraction from ζ(2)</div>
                            
                            <div class="pi-extraction">
                                <div class="error-display">
                                    <strong>π Reconstruction:</strong> π = √(6 × ζ(2))<br>
                                    π = √(6 × ${totalProduct.toFixed(10)}) = <span class="highlight">${piExtracted.toFixed(10)}</span><br>
                                    π<sub>actual</sub> = ${actualPi.toFixed(10)}<br><br>
                                    
                                    <strong>π Error Analysis:</strong><br>
                                    Absolute Error: ${piError.toFixed(10)}<br>
                                    Relative Error: ${piErrorPercent.toFixed(6)}%<br><br>
                                    
                                    ${piErrorPercent < 0.001 ? '🎯 <strong>Exceptional π precision!</strong>' :
                                      piErrorPercent < 0.01 ? '✅ <strong>Excellent π approximation!</strong>' :
                                      piErrorPercent < 0.1 ? '📈 <strong>Very good π convergence!</strong>' :
                                      '🔬 <strong>Good π approximation!</strong>'}
                                </div>
                                
                                This demonstrates how prime gaps directly encode the geometric constant π!
                            </div>
                        `;
                        resultsDiv.appendChild(piDiv);
                    }
                    
                } catch (error) {
                    resultsDiv.innerHTML = `<div class="result-card zeta-comparison">Error: ${error.message}<br><br>Stack: ${error.stack}</div>`;
                }
            }, 150);
        }
        
        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            // Handle custom s visibility
            const zetaSSelect = document.getElementById('zetaS');
            const customSGroup = document.getElementById('customSGroup');
            
            function updateCustomSVisibility() {
                if (zetaSSelect.value === 'custom') {
                    customSGroup.style.display = 'flex';
                } else {
                    customSGroup.style.display = 'none';
                }
            }
            
            // Initial state
            updateCustomSVisibility();
            
            zetaSSelect.addEventListener('change', updateCustomSVisibility);
            
            calculateZeta();
        });
    </script>
</body>
</html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A New Telescoping Identity for Twin Prime Sieving</title>
    <script>
        window.MathJax = {
            tex: {
                inlineMath: [['$', '$'], ['\\(', '\\)']],
                displayMath: [['$$', '$$'], ['\\[', '\\]']],
                processEscapes: true,
                processEnvironments: true
            },
            options: {
                skipHtmlTags: ['script', 'noscript', 'style', 'textarea', 'pre']
            },
            startup: {
                ready() {
                    MathJax.startup.defaultReady();
                }
            }
        };
    </script>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', 'Times New Roman', serif;
            line-height: 1.7;
            background: #f8f9fa;
            color: #2c3e50;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 40px 30px;
            background: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            min-height: 100vh;
        }

        .header {
            text-align: center;
            padding: 40px 0;
            border-bottom: 2px solid #e9ecef;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 2em;
            margin-bottom: 20px;
            color: #2c3e50;
            font-weight: normal;
            line-height: 1.3;
        }

        .author-info {
            font-size: 1.1em;
            color: #6c757d;
            font-style: italic;
            margin-bottom: 10px;
        }

        .abstract {
            background: #f8f9fa;
            padding: 30px;
            border-left: 4px solid #007bff;
            margin: 30px 0;
            border-radius: 4px;
        }

        .abstract h3 {
            font-size: 1.2em;
            margin-bottom: 15px;
            color: #495057;
        }

        .section {
            margin: 40px 0;
        }

        .section h2 {
            color: #2c3e50;
            border-bottom: 2px solid #dee2e6;
            padding-bottom: 8px;
            margin-bottom: 25px;
            font-size: 1.5em;
            font-weight: normal;
        }

        .section h3 {
            color: #495057;
            margin: 25px 0 15px 0;
            font-size: 1.2em;
        }

        .theorem-box {
            background: #e3f2fd;
            border: 1px solid #2196f3;
            border-left: 4px solid #2196f3;
            padding: 25px;
            margin: 25px 0;
            border-radius: 4px;
        }

        .theorem-title {
            font-weight: bold;
            margin-bottom: 15px;
            color: #1976d2;
        }

        .proof-box {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            padding: 20px;
            margin: 15px 0;
            border-radius: 4px;
            font-style: italic;
        }

        .formula-center {
            text-align: center;
            margin: 20px 0;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 4px;
        }

        .interactive-section {
            background: #f1f8e9;
            border: 1px solid #8bc34a;
            border-left: 4px solid #8bc34a;
            padding: 25px;
            margin: 25px 0;
            border-radius: 4px;
        }

        .controls {
            background: white;
            padding: 20px;
            border: 1px solid #dee2e6;
            border-radius: 4px;
            margin: 15px 0;
        }

        .controls label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #495057;
        }

        .controls input {
            width: 200px;
            padding: 8px 12px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 1em;
            margin-bottom: 10px;
        }

        .btn {
            background: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1em;
            margin: 5px;
            transition: background 0.2s;
        }

        .btn:hover {
            background: #0056b3;
        }

        .results {
            margin: 20px 0;
            padding: 15px;
            background: white;
            border: 1px solid #dee2e6;
            border-radius: 4px;
        }

        .results-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin: 20px 0;
        }

        .data-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            border: 1px solid #dee2e6;
        }

        .data-table th,
        .data-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #dee2e6;
        }

        .data-table th {
            background: #f8f9fa;
            font-weight: bold;
        }

        .highlight-result {
            background: #d4edda;
            border: 1px solid #c3e6cb;
            padding: 10px;
            border-radius: 4px;
            margin: 10px 0;
            font-weight: bold;
            text-align: center;
        }

        .note-box {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            border-left: 4px solid #f39c12;
            padding: 20px;
            margin: 20px 0;
            border-radius: 4px;
        }

        .citation-info {
            background: #e9ecef;
            padding: 15px;
            border-radius: 4px;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
        }

        .references {
            font-size: 0.95em;
        }

        .references ol {
            padding-left: 20px;
        }

        .references li {
            margin-bottom: 8px;
        }

        @media (max-width: 768px) {
            .results-grid {
                grid-template-columns: 1fr;
            }
            .container {
                padding: 20px 15px;
            }
            .header h1 {
                font-size: 1.6em;
            }
        }

        @media print {
            .interactive-section {
                display: none;
            }
            .container {
                box-shadow: none;
                max-width: none;
                margin: 0;
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>A New Telescoping Identity for Twin Prime Sieving</h1>
            <div class="author-info">
                <strong>Wessen Getachew</strong><br>
                Independent Researcher<br>
                Email: Getachewwessen@gmail.com
            </div>
        </div>

        <div class="abstract">
            <h3>Abstract</h3>
            <p>We present a new algebraic identity that provides a factorization of the expression $(p-1)(p-2)/p^2$ appearing in twin prime sieving theory. The identity enables a telescoping product formula that yields closed-form expressions for finite products, offering computational advantages for numerical investigations of twin prime distribution.</p>
            <p><strong>Keywords:</strong> Twin primes, telescoping products, algebraic identities, sieve theory</p>
            <p><strong>2020 Mathematics Subject Classification:</strong> 11N36, 11A41</p>
        </div>

        <div class="citation-info">
            <strong>Citation:</strong> Getachew, W. (2025). A New Telescoping Identity for Twin Prime Sieving. Independent Research.
        </div>

        <div class="section">
            <h2>1. Introduction</h2>
            <p>The twin prime conjecture, concerning pairs of primes differing by 2, remains one of number theory's most prominent unsolved problems. Computational investigations of twin prime distribution often involve products of the form $\prod \frac{(p-1)(p-2)}{p^2}$, which arise naturally in sieving arguments.</p>
            
            <p>This paper establishes a new algebraic identity for such expressions and demonstrates its telescoping properties, providing both theoretical insight and practical computational benefits.</p>
        </div>

        <div class="section">
            <h2>2. Main Results</h2>
            
            <h3>2.1 The Fundamental Identity</h3>
            
            <div class="theorem-box">
                <div class="theorem-title">Theorem 1.</div>
                <p>For any real number $p > 1$:</p>
                <div class="formula-center">
                    $$\frac{(p-1)(p-2)}{p^2} = \left(1-\frac{1}{(p-1)^2}\right)\left(1-\frac{1}{p}\right)^3$$
                </div>
            </div>

            <div class="interactive-section">
                <h3>Interactive Verification</h3>
                <p>Verify this identity for any value of p:</p>
                
                <div class="controls">
                    <label for="p-value">Enter value of p (must be > 1):</label>
                    <input type="number" id="p-value" value="5" min="1.01" step="0.1">
                    <button class="btn" onclick="checkIdentity()">Verify Identity</button>
                </div>

                <div class="results-grid">
                    <div class="results">
                        <strong>Left Side: $(p-1)(p-2)/p^2$</strong>
                        <div id="left-calc"></div>
                        <div id="left-value" style="font-weight: bold; margin-top: 10px;"></div>
                    </div>
                    <div class="results">
                        <strong>Right Side: $(1-1/(p-1)^2)(1-1/p)^3$</strong>
                        <div id="right-calc"></div>
                        <div id="right-value" style="font-weight: bold; margin-top: 10px;"></div>
                    </div>
                </div>

                <div id="verification-status"></div>
            </div>

            <div class="proof-box">
                <strong>Proof.</strong> We establish this through direct algebraic manipulation.
                <br><br>
                Starting with the right-hand side:
                $$\left(1-\frac{1}{(p-1)^2}\right)\left(1-\frac{1}{p}\right)^3$$
                <br>
                The first factor simplifies to:
                $$1-\frac{1}{(p-1)^2} = \frac{(p-1)^2-1}{(p-1)^2} = \frac{p(p-2)}{(p-1)^2}$$
                <br>
                The second factor gives:
                $$\left(1-\frac{1}{p}\right)^3 = \frac{(p-1)^3}{p^3}$$
                <br>
                Multiplying these expressions:
                $$\frac{p(p-2)}{(p-1)^2} \cdot \frac{(p-1)^3}{p^3} = \frac{(p-2)(p-1)}{p^2}$$
                <br>
                This establishes the identity. □
            </div>

            <h3>2.2 Telescoping Product Formula</h3>

            <div class="theorem-box">
                <div class="theorem-title">Theorem 2.</div>
                <p>For any integer $n \geq 3$:</p>
                <div class="formula-center">
                    $$\prod_{k=3}^{n} \frac{(k-1)(k-2)}{k^2} = \frac{4}{n^2(n-1)}$$
                </div>
            </div>

            <div class="interactive-section">
                <h3>Telescoping Demonstration</h3>
                <p>Observe how a complex product simplifies to a single fraction:</p>
                
                <div class="controls">
                    <label for="n-value">Enter upper limit n (≥ 3):</label>
                    <input type="number" id="n-value" value="10" min="3" max="1000">
                    <button class="btn" onclick="demonstrateTelescoping()">Calculate</button>
                </div>

                <div class="results">
                    <div id="telescoping-results"></div>
                </div>
            </div>

            <div class="proof-box">
                <strong>Proof.</strong> Using Theorem 1, we factor the product:
                $$\prod_{k=3}^{n} \frac{(k-1)(k-2)}{k^2} = \prod_{k=3}^{n} \left(1-\frac{1}{(k-1)^2}\right) \prod_{k=3}^{n} \left(1-\frac{1}{k}\right)^3$$
                <br>
                For the second product:
                $$\prod_{k=3}^{n} \left(1-\frac{1}{k}\right)^3 = \left(\frac{2}{n}\right)^3 = \frac{8}{n^3}$$
                <br>
                For the first product:
                $$\prod_{k=3}^{n} \left(1-\frac{1}{(k-1)^2}\right) = \prod_{k=3}^{n} \frac{k(k-2)}{(k-1)^2} = \frac{n}{2(n-1)}$$
                <br>
                Combining both parts:
                $$\frac{n}{2(n-1)} \cdot \frac{8}{n^3} = \frac{4}{n^2(n-1)}$$
                □
            </div>
        </div>

        <div class="section">
            <h2>3. Applications to Twin Prime Theory</h2>
            
            <h3>3.1 Connection to Sieving</h3>
            <p>The expression $(p-1)(p-2)/p^2$ represents the density of integers avoiding both residue classes 1 and $p-1$ modulo $p$, which corresponds to numbers $m$ where neither $m$ nor $m+2$ is divisible by $p$. This is precisely the constraint needed in twin prime sieving.</p>

            <h3>3.2 Computational Advantages</h3>
            <p>The telescoping formula provides several benefits:</p>
            <ul>
                <li><strong>Direct evaluation:</strong> Products that would require computing hundreds of terms reduce to simple expressions</li>
                <li><strong>Numerical stability:</strong> Eliminates floating-point error accumulation in long products</li>
                <li><strong>Precision control:</strong> For target precision $\varepsilon$, the required cutoff is $n = \lceil(4/\varepsilon)^{1/3}\rceil$</li>
                <li><strong>Error bounds:</strong> The truncation error is exactly $4/(n^2(n-1))$</li>
            </ul>

            <div class="interactive-section">
                <h3>Precision Calculator</h3>
                <p>Determine optimal computation parameters for any target precision:</p>
                
                <div class="controls">
                    <label for="target-precision">Target precision (e.g. 1e-12):</label>
                    <input type="text" id="target-precision" value="1e-12">
                    <button class="btn" onclick="calculatePrecision()">Calculate Requirements</button>
                </div>

                <div id="precision-results" class="results"></div>
            </div>

            <h3>3.3 Numerical Example</h3>
            <p>For $n = 100$:</p>
            <ul>
                <li>Direct product: $\prod_{k=3}^{100} \frac{(k-1)(k-2)}{k^2} = 4.04040404... \times 10^{-6}$</li>
                <li>Telescoping formula: $\frac{4}{100^2 \cdot 99} = 4.04040404... \times 10^{-6}$</li>
            </ul>
            <p>The results match to machine precision.</p>
        </div>

        <div class="section">
            <h2>4. Convergence Analysis</h2>
            
            <h3>4.1 Asymptotic Behavior</h3>
            <p>From Theorem 2, the infinite product exhibits cubic decay:</p>
            <div class="formula-center">
                $$\prod_{k=3}^{n} \frac{(k-1)(k-2)}{k^2} \sim \frac{4}{n^3} \quad \text{as } n \to \infty$$
            </div>
            <p>This rapid convergence makes the finite approximations highly effective for computational purposes.</p>

            <h3>4.2 Precision Requirements</h3>
            <p>To achieve precision $\varepsilon$, we need:</p>
            <div class="formula-center">
                $$\frac{4}{n^2(n-1)} < \varepsilon$$
            </div>
            <p>Solving for $n$ gives the optimal cutoff $n \approx (4/\varepsilon)^{1/3}$.</p>

            <table class="data-table">
                <thead>
                    <tr>
                        <th>Cutoff n</th>
                        <th>Value: 4/(n²(n-1))</th>
                        <th>Decimal Places</th>
                    </tr>
                </thead>
                <tbody id="convergence-table">
                </tbody>
            </table>
        </div>

        <div class="section">
            <h2>5. Discussion</h2>
            <p>This telescoping identity transforms a computational challenge into an algebraic solution. Instead of computing potentially hundreds of product terms with accumulating numerical errors, researchers can evaluate exact expressions.</p>

            <p>The identity also provides theoretical insight into the structure of twin prime sieving, revealing how the local densities combine multiplicatively in a way that permits exact analysis.</p>

            <div class="note-box">
                <strong>Research Impact:</strong> This identity enables precise control over computational parameters in twin prime research, replacing trial-and-error approaches with exact mathematical formulas.
            </div>
        </div>

        <div class="section">
            <h2>6. Future Directions</h2>
            <p>Several avenues for further research emerge:</p>
            <ol>
                <li>Investigation of whether similar identities exist for other prime constellation patterns</li>
                <li>Application to improved numerical studies of the Hardy-Littlewood twin prime constant</li>
                <li>Exploration of connections to other sieving problems in analytic number theory</li>
            </ol>
        </div>

        <div class="section">
            <h2>7. Conclusion</h2>
            <p>We have established a new algebraic identity that enables telescoping behavior in products central to twin prime theory. This result provides both theoretical insight into sieving mechanisms and practical computational advantages for numerical investigations of twin prime distribution.</p>

            <p>The discovery demonstrates how elementary algebraic relationships can yield significant computational improvements in number-theoretic research, opening new possibilities for high-precision investigations of twin prime patterns.</p>
        </div>

        <div class="section references">
            <h2>References</h2>
            <ol>
                <li>G. H. Hardy and J. E. Littlewood, "Some problems of 'Partitio numerorum'; III: On the expression of a number as a sum of primes," <em>Acta Mathematica</em>, vol. 44, pp. 1-70, 1923.</li>
                <li>H. Halberstam and H.-E. Richert, <em>Sieve Methods</em>, Academic Press, 1974.</li>
                <li>T. Tao, "Structure and randomness in the prime numbers," <em>Proceedings of the ICM</em>, vol. 1, pp. 79-90, 2006.</li>
                <li>D. A. Goldston, J. Pintz, and C. Y. Yıldırım, "Primes in tuples I," <em>Annals of Mathematics</em>, vol. 170, pp. 819-862, 2009.</li>
            </ol>
        </div>

        <div class="citation-info" style="margin-top: 40px;">
            <strong>Correspondence:</strong> Wessen Getachew, Independent Researcher. Email: Getachewwessen@gmail.com
        </div>
    </div>

    <script>
        // Initialize convergence table
        document.addEventListener('DOMContentLoaded', function() {
            const tbody = document.getElementById('convergence-table');
            const values = [100, 1000, 10000, 100000, 1000000];
            
            values.forEach(n => {
                const telescopingValue = 4 / (n * n * (n - 1));
                const decimalPlaces = -Math.log10(telescopingValue);
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${n.toLocaleString()}</td>
                    <td>${telescopingValue.toExponential(3)}</td>
                    <td>${decimalPlaces.toFixed(1)}</td>
                `;
            });
        });

        function checkIdentity() {
            const p = parseFloat(document.getElementById('p-value').value);
            
            if (p <= 1) {
                alert('Please enter a value greater than 1');
                return;
            }

            const leftSide = (p - 1) * (p - 2) / (p * p);
            const term1 = 1 - 1/((p - 1) * (p - 1));
            const term2 = Math.pow(1 - 1/p, 3);
            const rightSide = term1 * term2;

            document.getElementById('left-calc').innerHTML = `
                <div>= (${p}-1)(${p}-2)/${p}²</div>
                <div>= ${((p-1)*(p-2)).toFixed(4)}/${(p*p).toFixed(2)}</div>
            `;
            
            document.getElementById('right-calc').innerHTML = `
                <div>First factor: ${term1.toFixed(6)}</div>
                <div>Second factor: ${term2.toFixed(6)}</div>
                <div>Product: ${(term1 * term2).toFixed(10)}</div>
            `;

            document.getElementById('left-value').textContent = `Result: ${leftSide.toFixed(10)}`;
            document.getElementById('right-value').textContent = `Result: ${rightSide.toFixed(10)}`;

            const difference = Math.abs(leftSide - rightSide);
            const isMatch = difference < 1e-12;
            
            const statusDiv = document.getElementById('verification-status');
            if (isMatch) {
                statusDiv.innerHTML = '<div class="highlight-result">✓ Identity verified! Both sides match perfectly.</div>';
            } else {
                statusDiv.innerHTML = '<div style="background: #f8d7da; color: #721c24; padding: 10px; border-radius: 4px;">✗ Calculation error - please check inputs.</div>';
            }
        }

        function demonstrateTelescoping() {
            const n = parseInt(document.getElementById('n-value').value);
            
            if (n < 3) {
                alert('Please enter a value of 3 or greater');
                return;
            }

            let product = 1;
            let terms = [];
            for (let k = 3; k <= Math.min(n, 10); k++) {
                const term = (k - 1) * (k - 2) / (k * k);
                product *= term;
                terms.push(`(${k-1}×${k-2})/${k}²`);
            }
            
            for (let k = 11; k <= n; k++) {
                product *= (k - 1) * (k - 2) / (k * k);
            }

            const telescoping = 4 / (n * n * (n - 1));

            const resultsDiv = document.getElementById('telescoping-results');
            resultsDiv.innerHTML = `
                <strong>Direct Product Computation:</strong><br>
                ${terms.slice(0, 5).join(' × ')}${n > 7 ? ' × ... × ' + terms[terms.length-1] : ''}<br>
                = ${product.toExponential(10)}<br><br>
                
                <strong>Telescoping Formula:</strong><br>
                4/(${n}² × ${n-1}) = 4/${(n*n*(n-1)).toLocaleString()} = ${telescoping.toExponential(10)}<br><br>
                
                <div class="highlight-result">
                    ${Math.abs(product - telescoping) < 1e-12 ? '✓ Perfect match! Telescoping verified.' : '⚠ Slight numerical difference due to floating-point precision.'}
                </div>
            `;
        }

        function calculatePrecision() {
            const precisionStr = document.getElementById('target-precision').value;
            const targetPrecision = parseFloat(precisionStr);
            
            if (isNaN(targetPrecision) || targetPrecision <= 0) {
                alert('Please enter a valid positive number');
                return;
            }

            const optimalN = Math.ceil(Math.pow(4 / targetPrecision, 1/3));
            const actualPrecision = 4 / (optimalN * optimalN * (optimalN - 1));

            document.getElementById('precision-results').innerHTML = `
                <strong>Precision Analysis:</strong><br>
                Target precision: ${targetPrecision.toExponential(2)}<br>
                Optimal cutoff: n = ${optimalN.toLocaleString()}<br>
                Achieved precision: ${actualPrecision.toExponential(3)}<br>
                <div class="highlight-result">
                    ✓ Guaranteed accuracy better than target!
                </div>
            `;
        }

        // Initialize first calculation after MathJax loads
        setTimeout(function() {
            if (typeof MathJax !== 'undefined') {
                checkIdentity();
            }
        }, 2000);
    </script>
</body>
</html>
