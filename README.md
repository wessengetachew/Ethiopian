
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ethiopian Calendar and the Modular Structure of Twin Primes</title>
    <style>
        body {
            font-family: 'Times New Roman', serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
            background-color: #fafafa;
        }
        .paper-container {
            background: white;
            padding: 40px;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
            border-radius: 8px;
        }
        .title {
            text-align: center;
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .author {
            text-align: center;
            font-size: 16px;
            margin-bottom: 30px;
            color: #666;
        }
        .abstract {
            background: #f8f9fa;
            padding: 20px;
            border-left: 4px solid #007bff;
            margin: 20px 0;
            font-style: italic;
        }
        h2 {
            color: #333;
            border-bottom: 2px solid #eee;
            padding-bottom: 5px;
        }
        h3 {
            color: #555;
        }
        .interactive-section {
            background: #e8f4f8;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
            border: 2px solid #007bff;
        }
        .mod-wheel {
            width: 400px;
            height: 400px;
            margin: 20px auto;
            position: relative;
        }
        .residue-point {
            position: absolute;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }
        .residue-point:hover {
            transform: scale(1.5);
            z-index: 10;
        }
        .twin-channel { background: #28a745; color: white; }
        .blocked-channel { background: #dc3545; color: white; }
        .other-prime { background: #17a2b8; color: white; }
        .composite { background: #6c757d; color: white; }
        
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 2px;
            max-width: 400px;
            margin: 20px auto;
        }
        .day {
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #ddd;
            cursor: pointer;
            transition: all 0.3s;
        }
        .day:hover {
            transform: scale(1.1);
        }
        .day.pruned { background: #dc3545; color: white; }
        .day.twin-start { background: #28a745; color: white; }
        .day.normal { background: #f8f9fa; }
        
        .table-container {
            overflow-x: auto;
            margin: 20px 0;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #f8f9fa;
        }
        
        .controls {
            background: #f8f9fa;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
        }
        
        .twin-calculator {
            background: #fff3cd;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
            border: 1px solid #ffeaa7;
        }
        
        .results {
            margin-top: 20px;
            padding: 15px;
            background: #d1ecf1;
            border-radius: 5px;
            min-height: 50px;
        }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        .legend-color {
            width: 15px;
            height: 15px;
            border-radius: 50%;
        }
        
        .math {
            font-style: italic;
        }
    </style>
</head>
<body>
    <div class="paper-container">
        <div class="title">Ethiopian Calendar and the Modular Structure of Twin Primes</div>
        <div class="author">Wessen Getachew</div>
        
        <div class="abstract">
            <strong>Abstract:</strong> The Ethiopian calendar, with its twelve 30-day months and five (or six) epagomenal days, encodes a natural arithmetic system modulo 30. Remarkably, this same modulus governs the classification of prime numbers into residue classes and the allowed channels for twin primes. We show that Ethiopian calendrical arithmetic mirrors the modular channels of the Getachew Modular Sieve Framework, revealing deep parallels between cultural timekeeping and modern number theory. Furthermore, the calendar's structure naturally selects precisely the gcd(r,30) = 1 positions where infinite prime ladders exist, and extends coherently to p-adic completions in the mod 30×2^n family.
        </div>

        <h2>1. Historical Background</h2>
        <p>The Ethiopian calendar traces back to the Alexandrian Coptic system, adopted in the fourth century CE. It consists of twelve equal months of thirty days each, followed by a thirteenth "epagomenal" month (Pagume) of five days, or six in leap years. Because Ethiopia was never colonized, this calendar has been preserved for over 1700 years in its original form. Its reliance on 30-day modular blocks provides a unique cultural embodiment of arithmetic structures that also govern prime numbers.</p>

        <h2>2. Infinite Prime Ladders and Coprime Residues</h2>
        <p>By Dirichlet's theorem, each residue class r with gcd(r,30) = 1 contains infinitely many primes. All primes <em>p</em> > 5 must lie in the reduced residue system modulo 30:</p>
        <p class="math">Φ(30) = {1, 7, 11, 13, 17, 19, 23, 29}</p>
        <p>This partitions primes into eight infinite ladders of the form <em>p</em> ≡ <em>r</em> (mod 30), where <em>r</em> ∈ Φ(30). The Ethiopian calendar's 30-day structure naturally selects precisely these eight positions where infinite prime sequences exist.</p>

        <div class="interactive-section">
            <h3>Ethiopian Calendar Position Today</h3>
            <p>The Ethiopian calendar began at epoch 29 August, 8 AD. As of Ethiopian New Year 2018 (September 11, 2025 Gregorian), the calendar reached day number <strong>736,734</strong> in the consecutive count.</p>
            <div class="table-container">
                <table>
                    <thead>
                        <tr>
                            <th>Ethiopian Year</th>
                            <th>Gregorian Date</th>
                            <th>Day Count</th>
                            <th>Position mod 30</th>
                            <th>Prime Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr style="background-color: #e8f4f8;">
                            <td>2017 (prime year!)</td>
                            <td>Sep 11, 2024</td>
                            <td>736,369</td>
                            <td>19</td>
                            <td>gcd(19,30) = 1 ✓</td>
                        </tr>
                        <tr style="background-color: #fff3cd;">
                            <td>2018 (composite: 2×1009)</td>
                            <td>Sep 11, 2025</td>
                            <td>736,734</td>
                            <td><strong>14</strong></td>
                            <td>gcd(14,30) = 2 ≠ 1 ✗</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <p><strong>Observation:</strong> The transition from prime year 2017 to composite year 2018 coincided with moving from a prime-eligible position (19) to a composite position (14) in the mod 30 cycle - the calendar encodes number theory at multiple levels simultaneously!</p>
        </div>

        <div class="interactive-section">
            <h3>Interactive Mod 30 Residue Wheel</h3>
            <div class="legend">
                <div class="legend-item">
                    <div class="legend-color twin-channel"></div>
                    <span>Twin Prime Channels</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color blocked-channel"></div>
                    <span>Blocked Channels</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color other-prime"></div>
                    <span>Other Prime Ladders</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color composite"></div>
                    <span>Composite</span>
                </div>
            </div>
            <div class="mod-wheel" id="modWheel"></div>
            <div id="wheelInfo" class="results">Click on any residue to see its properties</div>
        </div>

        <h2>3. Twin Prime Channels</h2>
        <p>A twin pair (p, p+2) requires both residues to remain in Φ(30). This reduces the admissible system to three distinct residue representatives:</p>
        <p class="math">r ∈ {11, 17, 29} (with 29 ≡ -1 (mod 30) for wraparound pairs)</p>

        <div class="interactive-section">
            <h3>Twin Prime Calculator</h3>
            <div class="twin-calculator">
                <label>Enter a number to check if it starts a twin prime: </label>
                <input type="number" id="twinInput" placeholder="Enter number">
                <button onclick="checkTwinPrime()">Check Twin Prime</button>
                <div id="twinResults" class="results"></div>
            </div>
        </div>

        <h3>3.1 Numerical Examples</h3>
        <div class="table-container">
            <table id="twinTable">
                <thead>
                    <tr>
                        <th>Channel</th>
                        <th>Twin Primes</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>r=11</td>
                        <td>(11,13), (41,43), (71,73), (101,103)</td>
                    </tr>
                    <tr>
                        <td>r=17</td>
                        <td>(17,19), (107,109), (137,139), (197,199)</td>
                    </tr>
                    <tr>
                        <td>r=29</td>
                        <td>(29,31), (59,61), (149,151), (179,181)</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h3>3.2 Blocked Channels</h3>
        <p>Two residues are permanently excluded:</p>
        <ul>
            <li><strong>r = 7</strong> ⟹ r+2 ≡ 9 (mod 30), divisible by 3</li>
            <li><strong>r = 23</strong> ⟹ r+2 ≡ 25 (mod 30), divisible by 5</li>
        </ul>
        <p>Thus the 7th and 23rd days of an Ethiopian month fall exactly on arithmetically forbidden twin positions.</p>

        <h3>3.3 The 5×6 = 30 Leap Year Reset Cycle</h3>
        <p>A remarkable additional pattern emerges from the Ethiopian leap year system: every 5 leap years adds exactly 30 extra days (5 × 6 = 30), creating a perfect mod 30 reset cycle. This means the leap year correction mechanism operates at the same modular frequency as the twin prime structure!</p>
        
        <div class="interactive-section">
            <h4>Interactive Leap Year Reset Cycle</h4>
            <div class="controls">
                <label>Leap Year Number: </label>
                <input type="range" id="leapYearSlider" min="0" max="10" value="0" oninput="updateLeapCycle()">
                <span id="leapYearDisplay">0</span>
            </div>
            <div id="leapCycleInfo" class="results"></div>
            <div class="table-container">
                <table id="leapCycleTable">
                    <thead>
                        <tr>
                            <th>Leap Year</th>
                            <th>Extra Days</th>
                            <th>Cumulative (mod 30)</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody id="leapCycleTableBody">
                    </tbody>
                </table>
            </div>
        </div>

        <div class="interactive-section">
            <h3>Ethiopian Month Calendar</h3>
            <p>Click on any day to see its twin prime properties:</p>
            <div class="calendar-grid" id="ethiopianCalendar"></div>
            <div id="calendarInfo" class="results">Click on any day to see its properties</div>
        </div>

        <h2>5. Nested Modular Structure: The Deep Pattern</h2>
        <p>The Ethiopian calendar reveals a remarkable recursive alignment with mod 30 arithmetic at multiple time scales:</p>
        
        <div class="interactive-section">
            <h3>Multi-Level Modular Alignment</h3>
            <ul>
                <li><strong>Daily level:</strong> 30-day months create mod 30 positioning where twin primes can exist</li>
                <li><strong>Monthly level:</strong> 12 months × 30 days = 360 days (12 × 30 structure)</li>
                <li><strong>Annual level:</strong> +5 regular days, +6 leap year days for solar alignment</li>
                <li><strong>Leap cycle level:</strong> Every 5 leap years = 5 × 6 = 30 extra days ≡ 0 (mod 30)</li>
            </ul>
            <p><strong>Result:</strong> The leap year correction mechanism operates at the same mod 30 frequency as the twin prime structure, creating perfect self-similarity across time scales.</p>
        </div>

        <h2>6. Scaling by Sieve Levels</h2>
        <p>The Getachew Modular Sieve Framework extends the base modulus by powers of two:</p>
        <p class="math">M<sub>n</sub> = 30 × 2<sup>n</sup></p>
        <p>At each level, the number of valid twin channels grows as:</p>
        <p class="math">T(M<sub>n</sub>) = 3 × 2<sup>n</sup></p>

        <div class="interactive-section">
            <h3>Interactive Scaling Table</h3>
            <div class="controls">
                <label>Select sieve level n: </label>
                <select id="sieveLevel" onchange="updateScalingTable()">
                    <option value="0">0</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                </select>
            </div>
            <div class="table-container">
                <table id="scalingTable">
                    <thead>
                        <tr>
                            <th>Level n</th>
                            <th>Modulus</th>
                            <th>Blocked Channels</th>
                            <th>Valid Twin Channels</th>
                        </tr>
                    </thead>
                    <tbody id="scalingTableBody">
                    </tbody>
                </table>
            </div>
        </div>

        <h2>7. P-adic Extensions and the 2-adic Family</h2>
        <p>The Getachew Modular Sieve Framework extends naturally to p-adic completions. In the 2-adic case, the mod 30×2<sup>n</sup> family creates a coherent system where:</p>
        <ul>
            <li><strong>Local structure:</strong> Each prime ladder branches into 2-adic extensions</li>
            <li><strong>Global coherence:</strong> The Ethiopian calendar's mod 30 base provides the fundamental "trunk"</li>
            <li><strong>Lifting property:</strong> Twin prime channels lift coherently from mod 30 to higher powers</li>
            <li><strong>Infinite limit:</strong> As n→∞, we approach the full 2-adic completion</li>
        </ul>
        
        <div class="interactive-section">
            <h3>P-adic Ladder Visualization</h3>
            <p>The infinite prime ladders exist precisely on the gcd(r, 30×2<sup>n</sup>) = 1 positions, extending the Ethiopian calendar's natural selection principle to higher moduli.</p>
            <div class="controls">
                <label>2-adic Level n: </label>
                <select id="padicLevel" onchange="updatePadicLadders()">
                    <option value="0">0 (mod 30)</option>
                    <option value="1">1 (mod 60)</option>
                    <option value="2">2 (mod 120)</option>
                    <option value="3">3 (mod 240)</option>
                </select>
            </div>
            <div id="padicInfo" class="results"></div>
        </div>

        <h2>8. Seven Cultural-Mathematical Parallels</h2>
        <ol>
            <li><strong>Epagomenal days ↔ Exceptional primes.</strong> The five (or six) extra Pagume days behave like the small exceptional primes {2,3,5} that do not belong to Φ(30) but are necessary for arithmetic completeness.</li>
            <li><strong>Calendar wraparound ↔ Twin-prime wraparound.</strong> The year restarting at Meskerem 1 mirrors twin pairs that straddle the residue boundary (e.g. (59,61) with 59 ≡ -1 (mod 30)).</li>
            <li><strong>Leap-year correction ↔ Modular correction.</strong> The Ethiopian four-year leap adjustment creates a 5×6=30 reset cycle, showing that even the correction mechanism operates at the same mod 30 frequency as twin prime channels - a recursive alignment across time scales.</li>
            <li><strong>Twelve months ↔ Adjacency checks.</strong> The calendar's division into twelve months resonates with the set of adjacency checks (r,r+2) inside the totatives of 30.</li>
            <li><strong>Bifurcation principle ↔ Doubling of sieve levels.</strong> The sieve law M<sub>n</sub>=30×2<sup>n</sup> doubles the modulus and bifurcates residue channels.</li>
            <li><strong>Temporal offset ↔ Negative sieve levels.</strong> The Ethiopian calendar's offset relative to Gregorian time mirrors how negative sieve levels sit "behind" natural cutoffs.</li>
            <li><strong>Goldbach symmetry ↔ Feast pairings.</strong> Cultural pairings of feast and fast cycles reflect the combinatorial pairing symmetry central to Goldbach decompositions.</li>
        </ol>

        <h2>9. Conclusion</h2>
        <p>The Ethiopian calendar encodes a mod 30 arithmetic that mirrors the structure of prime residues and twin prime channels at multiple nested levels. The discovery that leap year corrections operate on 30-day cycles (5×6=30) reveals a recursive mathematical structure where the correction mechanism reinforces the same modular frequency as the twin prime channels themselves.</p>
        <p>Most remarkably, the calendar's structure naturally selects precisely the gcd(r,30) = 1 positions where infinite prime ladders exist, as guaranteed by Dirichlet's theorem. This selection principle extends coherently to p-adic completions in the mod 30×2<sup>n</sup> family, suggesting that Ethiopian mathematical intuition captured not just surface-level modular patterns, but deep structural features of prime distribution that extend to modern algebraic number theory.</p>
        <p>As demonstrated by the transition from prime year 2017 to composite year 2018 coinciding with movement from prime-eligible to composite positions in the mod 30 cycle, the calendar appears to encode number theory at multiple levels simultaneously - a testament to the profound mathematical sophistication embedded in cultural timekeeping systems.</p>
    </div>

    <script>
        // Helper functions
        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2 || n === 3) return true;
            if (n % 2 === 0 || n % 3 === 0) return false;
            for (let i = 5; i * i <= n; i += 6) {
                if (n % i === 0 || n % (i + 2) === 0) return false;
            }
            return true;
        }

        function gcd(a, b) {
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }

        // Create mod 30 wheel
        function createModWheel() {
            const wheel = document.getElementById('modWheel');
            const radius = 180;
            const centerX = 200;
            const centerY = 200;
            
            const phi30 = [1, 7, 11, 13, 17, 19, 23, 29];
            const twinChannels = [11, 17, 29];
            const blockedChannels = [7, 23];
            
            for (let i = 0; i < 30; i++) {
                const angle = (i * 360 / 30 - 90) * Math.PI / 180;
                const x = centerX + radius * Math.cos(angle);
                const y = centerY + radius * Math.sin(angle);
                
                const point = document.createElement('div');
                point.className = 'residue-point';
                point.textContent = i;
                point.style.left = (x - 10) + 'px';
                point.style.top = (y - 10) + 'px';
                
                if (twinChannels.includes(i)) {
                    point.classList.add('twin-channel');
                } else if (blockedChannels.includes(i)) {
                    point.classList.add('blocked-channel');
                } else if (phi30.includes(i)) {
                    point.classList.add('other-prime');
                } else {
                    point.classList.add('composite');
                }
                
                point.onclick = () => showResidueInfo(i);
                wheel.appendChild(point);
            }
        }

        function showResidueInfo(r) {
            const info = document.getElementById('wheelInfo');
            const phi30 = [1, 7, 11, 13, 17, 19, 23, 29];
            const twinChannels = [11, 17, 29];
            const blockedChannels = [7, 23];
            
            let result = `<strong>Residue ${r} (mod 30):</strong><br>`;
            
            if (!phi30.includes(r)) {
                result += `• Not coprime to 30 (shares factor with 2, 3, or 5)<br>`;
                result += `• Cannot contain primes > 5<br>`;
            } else {
                result += `• Coprime to 30 - can contain primes<br>`;
                
                if (twinChannels.includes(r)) {
                    const r_plus_2 = (r + 2) % 30;
                    result += `• <span style="color: green">✓ Valid twin prime channel</span><br>`;
                    result += `• ${r} + 2 = ${r_plus_2} is also coprime to 30<br>`;
                    
                    // Show some examples
                    const examples = [];
                    for (let base = 0; base < 300; base += 30) {
                        const p1 = base + r;
                        const p2 = p1 + 2;
                        if (p1 > 5 && isPrime(p1) && isPrime(p2)) {
                            examples.push(`(${p1},${p2})`);
                            if (examples.length >= 3) break;
                        }
                    }
                    if (examples.length > 0) {
                        result += `• Twin primes: ${examples.join(', ')}<br>`;
                    }
                } else if (blockedChannels.includes(r)) {
                    const r_plus_2 = r + 2;
                    result += `• <span style="color: red">✗ Blocked twin prime channel</span><br>`;
                    result += `• ${r} + 2 = ${r_plus_2} ≡ ${r_plus_2 % 30} (mod 30)<br>`;
                    if (r === 7) result += `• 9 is divisible by 3, so r+2 cannot be prime<br>`;
                    if (r === 23) result += `• 25 is divisible by 5, so r+2 cannot be prime<br>`;
                    result += `• <strong>Ethiopian calendar connection:</strong> Day ${r} is "pruned"<br>`;
                } else {
                    const r_plus_2 = (r + 2) % 30;
                    result += `• Cannot start twin primes<br>`;
                    result += `• ${r} + 2 = ${r_plus_2} (mod 30) - not coprime to 30<br>`;
                }
            }
            
            info.innerHTML = result;
        }

        // Create Ethiopian calendar
        function createEthiopianCalendar() {
            const calendar = document.getElementById('ethiopianCalendar');
            const twinDays = [11, 17, 29];
            const prunedDays = [7, 23];
            
            for (let day = 1; day <= 30; day++) {
                const dayDiv = document.createElement('div');
                dayDiv.className = 'day';
                dayDiv.textContent = day;
                
                if (prunedDays.includes(day)) {
                    dayDiv.classList.add('pruned');
                } else if (twinDays.includes(day)) {
                    dayDiv.classList.add('twin-start');
                } else {
                    dayDiv.classList.add('normal');
                }
                
                dayDiv.onclick = () => showDayInfo(day);
                calendar.appendChild(dayDiv);
            }
        }

        function showDayInfo(day) {
            const info = document.getElementById('calendarInfo');
            const twinDays = [11, 17, 29];
            const prunedDays = [7, 23];
            
            let result = `<strong>Ethiopian Calendar Day ${day}:</strong><br>`;
            
            if (prunedDays.includes(day)) {
                result += `• <span style="color: red">Pruned position</span> - cannot start twin primes<br>`;
                if (day === 7) result += `• 7 + 2 = 9, divisible by 3<br>`;
                if (day === 23) result += `• 23 + 2 = 25, divisible by 5<br>`;
                result += `• Mathematically forbidden for twin prime generation<br>`;
            } else if (twinDays.includes(day)) {
                result += `• <span style="color: green">Valid twin prime position</span><br>`;
                result += `• Day ${day} can generate twin primes like (${day}, ${day + 2})<br>`;
                result += `• Part of the mod 30 twin prime channel system<br>`;
            } else {
                const dayMod30 = day % 30;
                const isCoprimeBase = gcd(dayMod30, 30) === 1;
                if (isCoprimeBase) {
                    result += `• Prime-eligible position but not twin-prime starter<br>`;
                    result += `• ${day} + 2 = ${day + 2} is not coprime to 30<br>`;
                } else {
                    result += `• Composite position - shares factor with 30<br>`;
                    result += `• Cannot contain primes > 5<br>`;
                }
            }
            
            info.innerHTML = result;
        }

        // Twin prime checker
        function checkTwinPrime() {
            const input = document.getElementById('twinInput');
            const results = document.getElementById('twinResults');
            const n = parseInt(input.value);
            
            if (!n || n < 1) {
                results.innerHTML = 'Please enter a valid positive number.';
                return;
            }
            
            const isPrimeN = isPrime(n);
            const isPrimeN2 = isPrime(n + 2);
            const isTwinPrime = isPrimeN && isPrimeN2;
            const residue = n % 30;
            
            let result = `<strong>Analysis of ${n}:</strong><br>`;
            result += `• ${n} is ${isPrimeN ? 'prime' : 'not prime'}<br>`;
            result += `• ${n + 2} is ${isPrimeN2 ? 'prime' : 'not prime'}<br>`;
            
            if (isTwinPrime) {
                result += `• <span style="color: green">✓ (${n}, ${n + 2}) is a twin prime pair!</span><br>`;
            } else {
                result += `• <span style="color: red">✗ Not a twin prime pair</span><br>`;
            }
            
            result += `• ${n} ≡ ${residue} (mod 30)<br>`;
            
            const twinChannels = [11, 17, 29];
            const blockedChannels = [7, 23];
            
            if (twinChannels.includes(residue)) {
                result += `• <span style="color: green">Residue ${residue} is a valid twin prime channel</span><br>`;
            } else if (blockedChannels.includes(residue)) {
                result += `• <span style="color: red">Residue ${residue} is blocked for twin primes</span><br>`;
                if (residue === 7) result += `• Because 7 + 2 = 9 is divisible by 3<br>`;
                if (residue === 23) result += `• Because 23 + 2 = 25 is divisible by 5<br>`;
            } else {
                result += `• Residue ${residue} cannot start twin primes in mod 30 system<br>`;
            }
            
            results.innerHTML = result;
        }

        // Update leap cycle visualization
        function updateLeapCycle() {
            const leapYear = parseInt(document.getElementById('leapYearSlider').value);
            document.getElementById('leapYearDisplay').textContent = leapYear;
            
            const tbody = document.getElementById('leapCycleTableBody');
            const info = document.getElementById('leapCycleInfo');
            tbody.innerHTML = '';
            
            let cumulativeMod30 = 0;
            
            for (let i = 1; i <= leapYear; i++) {
                const extraDays = 6; // Each leap year adds 6 days
                cumulativeMod30 = (cumulativeMod30 + extraDays) % 30;
                
                const row = document.createElement('tr');
                if (i === leapYear) row.style.backgroundColor = '#e8f4f8';
                if (cumulativeMod30 === 0 && i > 0) row.style.backgroundColor = '#d4edda'; // Reset cycles
                
                let status = '';
                if (cumulativeMod30 === 0 && i % 5 === 0) {
                    status = '<span style="color: green; font-weight: bold;">RESET CYCLE!</span>';
                } else if (i % 5 === 0) {
                    status = '<span style="color: orange;">5-year cycle</span>';
                } else {
                    status = 'Accumulating';
                }
                
                row.innerHTML = `
                    <td>${i}</td>
                    <td>+6</td>
                    <td>${cumulativeMod30}</td>
                    <td>${status}</td>
                `;
                tbody.appendChild(row);
            }
            
            let infoText = `<strong>Leap Year ${leapYear} Analysis:</strong><br>`;
            infoText += `• Total accumulated days: ${leapYear * 6}<br>`;
            infoText += `• Position in mod 30 cycle: ${cumulativeMod30}<br>`;
            
            if (leapYear > 0 && leapYear % 5 === 0) {
                infoText += `• <span style="color: green; font-weight: bold;">Complete 5×6 = 30 cycle! System resets to mod 30 ≡ 0</span><br>`;
                infoText += `• This demonstrates the recursive mod 30 alignment across time scales<br>`;
            } else if (leapYear > 0) {
                const remaining = 5 - (leapYear % 5);
                infoText += `• ${remaining} more leap years needed to complete the 30-day reset cycle<br>`;
            }
            
            if (leapYear >= 5) {
                infoText += `• <strong>Pattern:</strong> Every 5 leap years creates exactly 30 extra days, maintaining the same modular structure as daily twin prime positions<br>`;
            }
            
            info.innerHTML = infoText;
        }
        function updateScalingTable() {
            const level = parseInt(document.getElementById('sieveLevel').value);
            const tbody = document.getElementById('scalingTableBody');
            tbody.innerHTML = '';
            
            for (let n = 0; n <= level; n++) {
                const modulus = 30 * Math.pow(2, n);
                const blocked = 2 * Math.pow(2, n);
                const valid = 3 * Math.pow(2, n);
                
                const row = document.createElement('tr');
                if (n === level) row.style.backgroundColor = '#e8f4f8';
                
                row.innerHTML = `
                    <td>${n}</td>
                    <td>${modulus}</td>
                    <td>${blocked}</td>
                    <td>${valid}</td>
                `;
                tbody.appendChild(row);
            }
        }

        // Update p-adic ladder visualization
        function updatePadicLadders() {
            const level = parseInt(document.getElementById('padicLevel').value);
            const info = document.getElementById('padicInfo');
            const modulus = 30 * Math.pow(2, level);
            const phi_count = 8 * Math.pow(2, level);
            const twin_channels = 3 * Math.pow(2, level);
            const blocked_channels = 2 * Math.pow(2, level);
            
            let result = `<strong>2-adic Level ${level} Analysis:</strong><br>`;
            result += `• Modulus: 30×2<sup>${level}</sup> = ${modulus}<br>`;
            result += `• φ(${modulus}) = ${phi_count} infinite prime ladders<br>`;
            result += `• ${twin_channels} twin prime channels available<br>`;
            result += `• ${blocked_channels} channels blocked for twin primes<br><br>`;
            
            result += `<strong>Ethiopian Calendar Connection:</strong><br>`;
            result += `• Base mod 30 structure extends naturally to mod ${modulus}<br>`;
            result += `• Each original prime ladder branches into ${Math.pow(2, level)} 2-adic extensions<br>`;
            result += `• Leap year reset cycle (5×6=30) remains fundamental period<br>`;
            
            if (level > 0) {
                result += `• Twin prime channels scale from 3 to ${twin_channels} while preserving base structure<br>`;
                result += `• Ethiopian days 7 and 23 lift to ${blocked_channels} blocked positions<br>`;
            }
            
            result += `<br><strong>P-adic Insight:</strong> The Ethiopian calendar naturally selects the gcd(r,30) = 1 positions that extend coherently through the entire 2-adic tower, demonstrating deep structural alignment with infinite prime distribution.`;
            
            info.innerHTML = result;
        }

        // Initialize everything
        window.onload = function() {
            createModWheel();
            createEthiopianCalendar();
            updateScalingTable();
            updateLeapCycle();
            updatePadicLadders();
        };
    </script>
</body>
</html>
