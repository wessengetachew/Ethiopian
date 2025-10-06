<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Sieve: π and ζ(2n) Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ffd700, #ffed4e);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .subtitle {
            text-align: center;
            font-size: 1.1em;
            opacity: 0.9;
            margin-bottom: 30px;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .control-group {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .control-group h3 {
            margin-bottom: 15px;
            color: #ffd700;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        input, select, button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 15px;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
        }
        
        button {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(238, 90, 82, 0.3);
        }
        
        .results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .result-card {
            background: rgba(255, 255, 255, 0.08);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-card h4 {
            color: #ffd700;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
        
        .value {
            font-family: 'Courier New', monospace;
            font-size: 1.2em;
            background: rgba(0, 0, 0, 0.3);
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            word-break: break-all;
        }
        
        .error-info {
            font-size: 0.9em;
            opacity: 0.8;
            margin-top: 10px;
        }
        
        .gap-analysis {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .gap-analysis h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .gap-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }
        
        .gap-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }
        
        .gap-value {
            font-size: 1.1em;
            font-weight: bold;
            color: #4ecdc4;
        }
        
        .channel-analysis {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .channel-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 10px;
        }
        
        .channel-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            font-size: 0.9em;
        }
        
        .loading {
            text-align: center;
            font-style: italic;
            opacity: 0.7;
        }
        
        .chart-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .chart-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
            text-align: center;
        }
        
        #channelChart {
            width: 100%;
            height: 400px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        
        .chart-legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
            font-size: 0.9em;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 2px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Modular Sieve Calculator</h1>
        <div class="subtitle">Computing π and ζ(2n) via Gap-Class and Residue-Channel Decompositions</div>
        
        <div class="controls">
            <div class="control-group">
                <h3>Target Accuracy</h3>
                <label for="epsilon">Relative Error (ε):</label>
                <input type="number" id="epsilon" value="0.001" step="0.0001" min="0.0001" max="0.1">
                
                <label for="constant">Constant to Compute:</label>
                <select id="constant">
                    <option value="pi">π (from ζ(2))</option>
                    <option value="zeta4">ζ(4)</option>
                    <option value="zeta6">ζ(6)</option>
                    <option value="zeta8">ζ(8)</option>
                    <option value="zeta10">ζ(10)</option>
                </select>
            </div>
            
            <div class="control-group">
                <h3>Computation Method</h3>
                <label for="method">Decomposition:</label>
                <select id="method">
                    <option value="standard">Standard Euler Product</option>
                    <option value="gap">Gap-Class Analysis</option>
                    <option value="residue">Residue Channels (mod 30)</option>
                    <option value="both">Gap + Residue Combined</option>
                </select>
                
                <button onclick="compute()">Calculate</button>
            </div>
        </div>
        
        <div id="results" class="results" style="display: none;">
            <div class="result-card">
                <h4>Computed Value</h4>
                <div id="computed-value" class="value"></div>
                <div id="error-bound" class="error-info"></div>
                <div id="prime-count" class="error-info"></div>
            </div>
            
            <div class="result-card">
                <h4>Exact Reference</h4>
                <div id="exact-value" class="value"></div>
                <div id="actual-error" class="error-info"></div>
            </div>
        </div>
        
        <div id="gap-analysis" class="gap-analysis" style="display: none;">
            <h3>Gap-Class Decomposition</h3>
            <div id="gap-grid" class="gap-grid"></div>
        </div>
        
        <div id="channel-analysis" class="channel-analysis" style="display: none;">
            <h3>Residue Channels (mod 30)</h3>
            <div id="channel-grid" class="channel-grid"></div>
        </div>
        
        <div id="chart-section" class="chart-container" style="display: none;">
            <h3>Residue Channel Contributions (ℤ_a(s;30))</h3>
            <canvas id="channelChart"></canvas>
            <div class="chart-legend" id="chartLegend"></div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <script>
        // Sieve of Eratosthenes optimized for our needs
        function sieveOfEratosthenes(limit) {
            if (limit < 2) return [];
            
            const isPrime = new Array(limit + 1).fill(true);
            isPrime[0] = isPrime[1] = false;
            
            for (let i = 2; i * i <= limit; i++) {
                if (isPrime[i]) {
                    for (let j = i * i; j <= limit; j += i) {
                        isPrime[j] = false;
                    }
                }
            }
            
            const primes = [];
            for (let i = 2; i <= limit; i++) {
                if (isPrime[i]) primes.push(i);
            }
            return primes;
        }
        
        // Compute gap classes
        function computeGapClasses(primes) {
            const gapClasses = {};
            
            for (let i = 1; i < primes.length; i++) {
                const gap = primes[i] - primes[i-1];
                if (!gapClasses[gap]) gapClasses[gap] = [];
                gapClasses[gap].push(primes[i]);
            }
            
            return gapClasses;
        }
        
        // Compute residue channels mod 30
        function computeResidueChannels(primes) {
            const phi30 = [1, 7, 11, 13, 17, 19, 23, 29];
            const channels = {};
            
            phi30.forEach(a => channels[a] = []);
            
            primes.forEach(p => {
                if (p > 5) { // Skip 2, 3, 5 (handled separately)
                    const residue = p % 30;
                    if (phi30.includes(residue)) {
                        channels[residue].push(p);
                    }
                }
            });
            
            return channels;
        }
        
        // Compute Y cutoff for given epsilon and constant type
        function computeCutoff(epsilon, constantType) {
            if (constantType === 'pi') {
                return Math.ceil(1 + 1 / Math.log(1 + epsilon));
            } else {
                const n = parseInt(constantType.replace('zeta', '')) / 2;
                const power = 1 / (2 * n - 1);
                return Math.ceil(Math.pow(2 / ((2 * n - 1) * Math.log(1 + epsilon)), power));
            }
        }
        
        // Compute truncated product
        function computeTruncatedProduct(primes, exponent) {
            let product = 1;
            for (const p of primes) {
                product *= 1 / (1 - Math.pow(p, -exponent));
            }
            return product;
        }
        
        // Exact values for reference
        const exactValues = {
            'pi': Math.PI,
            'zeta4': Math.PI ** 4 / 90,
            'zeta6': Math.PI ** 6 / 945,
            'zeta8': Math.PI ** 8 / 9450,
            'zeta10': Math.PI ** 10 / 93555
        };
        
        function compute() {
            const epsilon = parseFloat(document.getElementById('epsilon').value);
            const constantType = document.getElementById('constant').value;
            const method = document.getElementById('method').value;
            
            // Show loading
            document.getElementById('results').style.display = 'block';
            document.getElementById('computed-value').innerHTML = '<div class="loading">Computing...</div>';
            
            setTimeout(() => {
                try {
                    // Compute required cutoff
                    const Y = computeCutoff(epsilon, constantType);
                    const primes = sieveOfEratosthenes(Y - 1);
                    
                    let computedValue;
                    let analysisHtml = '';
                    
                    if (constantType === 'pi') {
                        // π = √6 * ∏(1-p^-2)^-1/2
                        const zetaProduct = computeTruncatedProduct(primes, 2);
                        computedValue = Math.sqrt(6 * zetaProduct);
                    } else {
                        // ζ(2n) = ∏(1-p^-2n)^-1
                        const n = parseInt(constantType.replace('zeta', '')) / 2;
                        computedValue = computeTruncatedProduct(primes, 2 * n);
                    }
                    
                    // Display results
                    document.getElementById('computed-value').textContent = computedValue.toFixed(12);
                    document.getElementById('exact-value').textContent = exactValues[constantType].toFixed(12);
                    
                    const actualError = Math.abs(computedValue - exactValues[constantType]) / exactValues[constantType];
                    document.getElementById('actual-error').innerHTML = `Actual relative error: ${(actualError * 100).toFixed(6)}%`;
                    document.getElementById('error-bound').innerHTML = `Guaranteed error ≤ ${(epsilon * 100).toFixed(4)}%`;
                    document.getElementById('prime-count').innerHTML = `Using ${primes.length} primes up to ${Y-1}`;
                    
                    // Method-specific analysis
                    if (method === 'gap' || method === 'both') {
                        showGapAnalysis(primes, constantType);
                    } else {
                        document.getElementById('gap-analysis').style.display = 'none';
                    }
                    
                    if (method === 'residue' || method === 'both') {
                        showResidueAnalysis(primes, constantType);
                    } else {
                        document.getElementById('channel-analysis').style.display = 'none';
                        document.getElementById('chart-section').style.display = 'none';
                    }
                    
                } catch (error) {
                    document.getElementById('computed-value').innerHTML = `<span style="color: #ff6b6b;">Error: ${error.message}</span>`;
                }
            }, 100);
        }
        
        function showGapAnalysis(primes, constantType) {
            const gapClasses = computeGapClasses(primes);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            
            let html = '';
            const sortedGaps = Object.keys(gapClasses).map(Number).sort((a, b) => a - b);
            
            for (const gap of sortedGaps.slice(0, 12)) { // Show first 12 gap classes
                const gapPrimes = gapClasses[gap];
                const contribution = computeTruncatedProduct(gapPrimes, exponent);
                const logContrib = Math.log(contribution);
                
                html += `
                    <div class="gap-item">
                        <div>Gap ${gap}</div>
                        <div class="gap-value">R_${gap} = ${contribution.toFixed(6)}</div>
                        <div style="font-size: 0.8em; opacity: 0.8;">${gapPrimes.length} primes</div>
                        <div style="font-size: 0.8em; opacity: 0.8;">log R = ${logContrib.toFixed(4)}</div>
                    </div>
                `;
            }
            
            document.getElementById('gap-grid').innerHTML = html;
            document.getElementById('gap-analysis').style.display = 'block';
        }
        
        function showResidueAnalysis(primes, constantType) {
            const channels = computeResidueChannels(primes);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            const phi30 = [1, 7, 11, 13, 17, 19, 23, 29];
            
            let html = '';
            const channelData = [];
            
            // Handle small primes separately
            const smallPrimes = primes.filter(p => p <= 5);
            const smallProduct = computeTruncatedProduct(smallPrimes, exponent);
            
            html += `
                <div class="channel-item" style="grid-column: span 2; background: rgba(255, 215, 0, 0.2);">
                    <div>Small Primes</div>
                    <div style="font-weight: bold;">${smallProduct.toFixed(4)}</div>
                    <div style="font-size: 0.8em;">{2, 3, 5}</div>
                </div>
            `;
            
            for (const a of phi30) {
                const channelPrimes = channels[a];
                let contribution = 1;
                
                if (channelPrimes.length > 0) {
                    contribution = computeTruncatedProduct(channelPrimes, exponent);
                    
                    html += `
                        <div class="channel-item">
                            <div>≡ ${a} (mod 30)</div>
                            <div style="font-weight: bold; color: #4ecdc4;">${contribution.toFixed(4)}</div>
                            <div style="font-size: 0.8em;">${channelPrimes.length} primes</div>
                        </div>
                    `;
                } else {
                    html += `
                        <div class="channel-item" style="opacity: 0.5;">
                            <div>≡ ${a} (mod 30)</div>
                            <div>1.0000</div>
                            <div style="font-size: 0.8em;">0 primes</div>
                        </div>
                    `;
                }
                
                channelData.push({
                    residue: a,
                    contribution: contribution,
                    primeCount: channelPrimes.length,
                    logContribution: Math.log(contribution)
                });
            }
            
            document.getElementById('channel-grid').innerHTML = html;
            document.getElementById('channel-analysis').style.display = 'block';
            
            // Create chart
            createChannelChart(channelData, smallProduct);
        }
        
        let channelChart = null;
        
        function createChannelChart(channelData, smallPrimesContrib) {
            const ctx = document.getElementById('channelChart').getContext('2d');
            
            // Destroy existing chart if it exists
            if (channelChart) {
                channelChart.destroy();
            }
            
            // Prepare data for chart
            const labels = ['Small Primes (2,3,5)', ...channelData.map(d => `≡ ${d.residue} (mod 30)`)];
            const contributions = [smallPrimesContrib, ...channelData.map(d => d.contribution)];
            const logContributions = [Math.log(smallPrimesContrib), ...channelData.map(d => d.logContribution)];
            const primeCounts = [3, ...channelData.map(d => d.primeCount)];
            
            // Create gradient colors
            const colors = [
                'rgba(255, 215, 0, 0.8)', // Gold for small primes
                'rgba(255, 99, 132, 0.8)',
                'rgba(54, 162, 235, 0.8)', 
                'rgba(255, 205, 86, 0.8)',
                'rgba(75, 192, 192, 0.8)',
                'rgba(153, 102, 255, 0.8)',
                'rgba(255, 159, 64, 0.8)',
                'rgba(199, 199, 199, 0.8)',
                'rgba(83, 102, 255, 0.8)'
            ];
            
            channelChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Channel Contribution',
                        data: contributions,
                        backgroundColor: colors,
                        borderColor: colors.map(c => c.replace('0.8', '1')),
                        borderWidth: 2,
                        borderRadius: 8,
                        borderSkipped: false,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            titleColor: '#fff',
                            bodyColor: '#fff',
                            borderColor: 'rgba(255, 255, 255, 0.3)',
                            borderWidth: 1,
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const contrib = contributions[idx];
                                    const logContrib = logContributions[idx];
                                    const count = primeCounts[idx];
                                    
                                    return [
                                        `Contribution: ${contrib.toFixed(6)}`,
                                        `log(Contribution): ${logContrib.toFixed(4)}`,
                                        `Prime count: ${count}`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            ticks: {
                                color: '#fff',
                                maxRotation: 45,
                                font: {
                                    size: 10
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            }
                        },
                        y: {
                            ticks: {
                                color: '#fff',
                                callback: function(value) {
                                    return value.toFixed(3);
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            title: {
                                display: true,
                                text: 'ℤₐ(s;30) Contribution',
                                color: '#fff',
                                font: {
                                    size: 14,
                                    weight: 'bold'
                                }
                            }
                        }
                    },
                    animation: {
                        duration: 1500,
                        easing: 'easeOutQuart'
                    }
                }
            });
            
            // Show chart section
            document.getElementById('chart-section').style.display = 'block';
            
            // Create legend
            createChartLegend(labels, colors, primeCounts);
        }
        
        function createChartLegend(labels, colors, primeCounts) {
            let legendHtml = '';
            
            for (let i = 0; i < labels.length; i++) {
                legendHtml += `
                    <div class="legend-item">
                        <div class="legend-color" style="background-color: ${colors[i]};"></div>
                        <span>${labels[i]} (${primeCounts[i]} primes)</span>
                    </div>
                `;
            }
            
            document.getElementById('chartLegend').innerHTML = legendHtml;
        }
        
        // Initialize with default computation
        window.onload = () => {
            compute();
        };
    </script>
</body>
</html>
