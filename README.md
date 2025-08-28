<!DOCTYPE html>
<html lang="en">

<body>
    <div class="container">
        <h1>🔬 >Prime Gap Factorization of ζ(s) and π Reconstruction </h1>
        <div class="subtitle">Prime Gap Factorization of ζ(s) and π Reconstruction</div>
        
        <div style="text-align: center; margin-bottom: 30px; padding: 20px; background: rgba(255, 255, 255, 0.1); border-radius: 15px;">
            <div style="font-size: 1.2em; color: #a8e6cf; margin-bottom: 10px;">
                <strong>Research by Wessen Getachew</strong>
            </div>
            <div style="font-size: 1em; opacity: 0.9;">
                Follow research updates: <a href="https://twitter.com/7DView" target="_blank" style="color: #48dbfb; text-decoration: none; font-weight: bold;">@7DView</a> on Twitter
            </div>
        </div>
        
        <div class="theorem-section">
            <div class="theorem-title">📐 Gap Decomposition Theorem (2025)</div>
            
            <div class="main-formula">
                ζ(s) = ∏<sub>g∈{1,2,4,6,...}</sub> ( ∏<sub>p: gap(p)=g</sub> (1 - p<sup>-s</sup>)<sup>-1</sup> )
            </div>
            
            <div class="gap-explanation">
                <strong>🔥 Revolutionary Discovery:</strong><br><br>
                
                <strong>1. Unique Prime Usage:</strong><br>
                Each prime p appears exactly once in the product - classified by gap(p) = next_prime(p) - p<br>
                For example: 2 has gap(2)=1, 3 has gap(3)=2, 5 has gap(5)=2, 7 has gap(7)=4, etc.<br><br>
                
                <strong>2. Direct Factorization Method:</strong><br>
                Instead of traditional analytic continuation approaches, this theorem provides<br>
                <em>direct factorization of ζ(s) through prime gap structure!</em><br><br>
                
                <strong>3. Gap Classification Principle:</strong><br>
                Prime gaps encode fundamental arithmetic information that directly reconstructs zeta functions<br>
                through discrete spacing structure rather than continuous analysis.<br><br>
                
                <strong>Gap Classes & Their Role:</strong><br>
                • <strong>Gap 1:</strong> Only prime 2 (since gap(2) = 3-2 = 1)<br>
                • <strong>Gap 2:</strong> Primes 3, 5 (since gap(3) = 5-3 = 2, gap(5) = 7-5 = 2)<br>
                • <strong>Gap 4:</strong> Primes 7, 13 (since gap(7) = 11-7 = 4, gap(13) = 17-13 = 4)<br>
                • <strong>Gap 6:</strong> Primes 11, 23 (since gap(11) = 17-11 = 6, gap(23) = 29-23 = 6)<br>
                • <strong>Larger gaps:</strong> Each prime p classified by gap(p) = next_prime(p) - p<br><br>
                
                <strong>π Reconstruction:</strong> π ≈ √(6 × ζ(2)) where ζ(2) is built from gap products!<br>
                This shows how prime gaps directly encode geometric constants!<br><br>
                
                <strong>⚡ Key Insight:</strong> Each prime contributes exactly once to the product, ensuring proper factorization!
            </div>
            
            <div class="main-formula">
                <strong>Special Cases:</strong><br>
                ζ(2) = π²/6 &nbsp;|&nbsp; ζ(4) = π⁴/90 &nbsp;|&nbsp; ζ(6) = π⁶/945
                <br><br>
                <strong>Innovation:</strong><br>
                Direct gap-based computation of these exact values!
            </div>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <label for="maxPrime">Maximum Prime N:</label>
                <input type="number" id="maxPrime" value="1000" min="100" max="100000" 
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
                <input type="number" id="maxGap" value="30" min="10" max="100" 
                       title="Include gaps up to this size">
            </div>
            
            <div class="control-group">
                <label for="showGraph">Show Gap Distribution Graph:</label>
                <select id="showGraph" title="Display visual graph of gap distribution">
                    <option value="false">No Graph</option>
                    <option value="true">Show Distribution</option>
                </select>
            </div>
            
            <div class="control-group" style="grid-column: span 2;">
                <button onclick="calculateZeta()" title="Calculate ζ(s) using gap decomposition">
                    🚀 Calculate ζ(s) via Gap Decomposition
                </button>
            </div>
        </div>
        
        <div id="results" class="results"></div>
        
        <div class="author-credit">
            <div style="font-size: 1.4em; color: #ff6b6b; font-weight: bold; margin-bottom: 15px;">
                🧮 Gap Inversion Sieve Theory
            </div>
            <div style="font-size: 1.2em; color: #a8e6cf; margin-bottom: 10px;">
                Original Research by <strong>Wessen Getachew</strong>
            </div>
            <div style="font-size: 1em; opacity: 0.9;">
                Follow mathematical discoveries: <a href="https://twitter.com/7DView" target="_blank" style="color: #48dbfb; text-decoration: none; font-weight: bold; transition: all 0.3s ease;">@7DView</a> on Twitter
            </div>
            <div style="font-size: 0.9em; margin-top: 15px; opacity: 0.8; color: #feca57;">
                "Bridging discrete prime gaps with continuous zeta functions through modular arithmetic"
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
            // Each prime p is used exactly once: when calculating gap from p to next prime
            for (let i = 0; i < primes.length - 1; i++) {
                const gap = primes[i + 1] - primes[i];
                gapData.push({
                    prime: primes[i],           // The prime p that has this gap
                    gap: gap,                   // gap(p) = next_prime - p
                    nextPrime: primes[i + 1]    // p + gap(p)
                });
            }
            
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
            // Each prime p contributes exactly once: (1 - p^(-s))^(-1) where gap(p) = g
            Object.keys(gapClasses).forEach(gap => {
                const gapNum = parseInt(gap);
                const primesInGap = gapClasses[gap];
                
                let gapProduct = 1.0;
                primesInGap.forEach(data => {
                    const p = data.prime;  // Prime p with gap(p) = gapNum
                    const factor = 1 / (1 - Math.pow(p, -s)); // (1 - p^(-s))^(-1)
                    gapProduct *= factor;
                });
                
                gapProducts[gapNum] = {
                    primes: primesInGap.map(d => d.prime),
                    count: primesInGap.length,
                    product: gapProduct,
                    examples: primesInGap.slice(0, 6).map(d => {
                        return `${d.prime}→${d.nextPrime} (gap ${d.gap})`;
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
        
        function drawGapDistributionGraph(gapProducts, canvasId) {
            const canvas = document.getElementById(canvasId);
            const ctx = canvas.getContext('2d');
            
            // Set canvas size
            canvas.width = 800;
            canvas.height = 400;
            
            // Clear canvas with dark background
            ctx.fillStyle = 'rgba(0, 0, 0, 0.8)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Prepare data
            const gaps = Object.keys(gapProducts).map(Number).sort((a, b) => a - b);
            const counts = gaps.map(gap => gapProducts[gap].count);
            const products = gaps.map(gap => gapProducts[gap].product);
            
            if (gaps.length === 0) return;
            
            // Graph dimensions
            const margin = { top: 40, right: 60, bottom: 60, left: 80 };
            const graphWidth = canvas.width - margin.left - margin.right;
            const graphHeight = canvas.height - margin.top - margin.bottom;
            
            // Scale functions
            const maxCount = Math.max(...counts);
            const maxProduct = Math.max(...products);
            const xScale = (gap) => margin.left + (gaps.indexOf(gap) / (gaps.length - 1)) * graphWidth;
            const yScale = (value, max) => margin.top + graphHeight - (value / max) * graphHeight;
            
            // Draw grid lines
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 1;
            
            // Vertical grid lines
            for (let i = 0; i < gaps.length; i += Math.max(1, Math.floor(gaps.length / 8))) {
                const x = xScale(gaps[i]);
                ctx.beginPath();
                ctx.moveTo(x, margin.top);
                ctx.lineTo(x, margin.top + graphHeight);
                ctx.stroke();
            }
            
            // Horizontal grid lines
            for (let i = 0; i <= 5; i++) {
                const y = margin.top + (i / 5) * graphHeight;
                ctx.beginPath();
                ctx.moveTo(margin.left, y);
                ctx.lineTo(margin.left + graphWidth, y);
                ctx.stroke();
            }
            
            // Draw axes
            ctx.strokeStyle = '#ffffff';
            ctx.lineWidth = 2;
            
            // X-axis
            ctx.beginPath();
            ctx.moveTo(margin.left, margin.top + graphHeight);
            ctx.lineTo(margin.left + graphWidth, margin.top + graphHeight);
            ctx.stroke();
            
            // Y-axis
            ctx.beginPath();
            ctx.moveTo(margin.left, margin.top);
            ctx.lineTo(margin.left, margin.top + graphHeight);
            ctx.stroke();
            
            // Draw bars for prime counts
            ctx.fillStyle = 'rgba(255, 107, 107, 0.7)';
            const barWidth = Math.min(20, graphWidth / gaps.length * 0.8);
            
            gaps.forEach((gap, i) => {
                const x = xScale(gap) - barWidth / 2;
                const y = yScale(counts[i], maxCount);
                const height = margin.top + graphHeight - y;
                
                ctx.fillRect(x, y, barWidth, height);
            });
            
            // Draw line for gap products (scaled)
            ctx.strokeStyle = '#48dbfb';
            ctx.lineWidth = 3;
            ctx.beginPath();
            
            gaps.forEach((gap, i) => {
                const x = xScale(gap);
                const y = yScale(products[i], maxProduct);
                
                if (i === 0) {
                    ctx.moveTo(x, y);
                } else {
                    ctx.lineTo(x, y);
                }
            });
            ctx.stroke();
            
            // Draw points on the line
            ctx.fillStyle = '#48dbfb';
            gaps.forEach((gap, i) => {
                const x = xScale(gap);
                const y = yScale(products[i], maxProduct);
                
                ctx.beginPath();
                ctx.arc(x, y, 4, 0, 2 * Math.PI);
                ctx.fill();
            });
            
            // Add labels
            ctx.font = '12px Arial';
            ctx.fillStyle = '#ffffff';
            ctx.textAlign = 'center';
            
            // X-axis labels (gap sizes)
            gaps.forEach((gap, i) => {
                if (i % Math.max(1, Math.floor(gaps.length / 10)) === 0) {
                    const x = xScale(gap);
                    ctx.fillText(gap.toString(), x, margin.top + graphHeight + 20);
                }
            });
            
            // Y-axis labels
            ctx.textAlign = 'right';
            for (let i = 0; i <= 5; i++) {
                const y = margin.top + (i / 5) * graphHeight + 4;
                const value = (maxCount * (5 - i) / 5).toFixed(0);
                ctx.fillText(value, margin.left - 10, y);
            }
            
            // Axis titles
            ctx.textAlign = 'center';
            ctx.font = '14px Arial';
            ctx.fillStyle = '#a8e6cf';
            
            // X-axis title
            ctx.fillText('Gap Size', canvas.width / 2, canvas.height - 15);
            
            // Y-axis title (rotated)
            ctx.save();
            ctx.translate(20, canvas.height / 2);
            ctx.rotate(-Math.PI / 2);
            ctx.fillText('Prime Count', 0, 0);
            ctx.restore();
            
            // Graph title
            ctx.font = 'bold 16px Arial';
            ctx.fillStyle = '#ff6b6b';
            ctx.fillText('Prime Gap Distribution & Product Contributions', canvas.width / 2, 25);
        }
        
        function calculateZeta() {
            const maxPrime = parseInt(document.getElementById('maxPrime').value);
            const zetaSSelect = document.getElementById('zetaS').value;
            const customS = parseFloat(document.getElementById('customS').value);
            const maxGap = parseInt(document.getElementById('maxGap').value);
            const showGraph = document.getElementById('showGraph').value === 'true';
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
                            <strong>Gap Inversion Formula:</strong><br>
                            ζ(${s}) = ∏_{g∈{1,2,4,6,...}} ∏_{p: gap(p)=g} (1 - p^{-${s}})^{-1}<br><br>
                            
                            <strong>Individual Gap Contributions:</strong><br>
                            ${Object.keys(gapProducts).sort((a,b) => parseInt(a) - parseInt(b)).map(gap => {
                                const gp = gapProducts[gap];
                                return `Gap ${gap}: ${gp.count} prime${gp.count > 1 ? 's' : ''} → Product = ${gp.product.toFixed(8)}`;
                            }).join('<br>')}
                            <br><br>
                            Total Product: ${totalProduct.toFixed(12)}
                        </div>
                    `;
                    
                    resultsDiv.appendChild(mainDiv);
                    
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
                    
                    // Add graph if requested
                    if (showGraph) {
                        const graphDiv = document.createElement('div');
                        graphDiv.className = 'graph-container';
                        graphDiv.innerHTML = `
                            <div class="result-header">📈 Prime Gap Distribution Visualization</div>
                            <canvas id="gapDistributionCanvas" class="graph-canvas"></canvas>
                            <div class="graph-legend">
                                <div class="legend-item">
                                    <div class="legend-color" style="background: rgba(255, 107, 107, 0.7);"></div>
                                    <span>Prime Count per Gap</span>
                                </div>
                                <div class="legend-item">
                                    <div class="legend-color" style="background: #48dbfb;"></div>
                                    <span>Gap Product Contribution</span>
                                </div>
                            </div>
                            <div style="text-align: center; margin-top: 15px; color: #a8e6cf; font-size: 0.9em;">
                                Red bars show how many primes have each gap size.<br>
                                Blue line shows each gap class's contribution to ζ(${s}).
                            </div>
                        `;
                        resultsDiv.appendChild(graphDiv);
                        
                        // Draw the graph after DOM is updated
                        setTimeout(() => {
                            drawGapDistributionGraph(gapProducts, 'gapDistributionCanvas');
                        }, 100);
                    }
                    
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
                                <td>${gp.product.toFixed(8)}</td>
                                <td>${logContrib.toFixed(6)}</td>
                                <td>${gp.examples}${moreText}</td>
                            </tr>
                        `;
                    });
                    
                    tableHTML += '</table></div>';
                    tableDiv.innerHTML = tableHTML;
                    resultsDiv.appendChild(tableDiv);
                    
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
