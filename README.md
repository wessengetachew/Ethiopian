import React, { useState, useEffect, useRef } from 'react';
import { Download, Settings, Zap } from 'lucide-react';

const ModularRingVisualizer = () => {
  const canvasRef = useRef(null);
  const [config, setConfig] = useState({
    modStart: 1,
    modEnd: 10,
    visualMode: 'concentric',
    showLabels: true,
    showConnections: true,
    connectionGap: 2,
    showPrimes: true,
    rangeStart: 0,
    rangeEnd: 100,
    dynadicBase: 30,
    dynadicExp: 3,
    useDynadic: false,
    colorScheme: 'viridis'
  });
  
  const [primes, setPrimes] = useState([]);
  const [gapAnalysis, setGapAnalysis] = useState([]);

  // Sieve of Eratosthenes
  const sieveOfEratosthenes = (max) => {
    const sieve = new Array(max + 1).fill(true);
    sieve[0] = sieve[1] = false;
    
    for (let i = 2; i * i <= max; i++) {
      if (sieve[i]) {
        for (let j = i * i; j <= max; j += i) {
          sieve[j] = false;
        }
      }
    }
    
    return sieve.map((isPrime, num) => isPrime ? num : -1).filter(n => n > 0);
  };

  // Analyze prime gaps
  const analyzeGaps = (primeList, targetGap) => {
    const gaps = [];
    for (let i = 0; i < primeList.length - 1; i++) {
      const gap = primeList[i + 1] - primeList[i];
      if (gap === targetGap) {
        gaps.push({ p1: primeList[i], p2: primeList[i + 1], gap });
      }
    }
    return gaps;
  };

  useEffect(() => {
    const maxRange = Math.max(config.rangeEnd, 1000);
    const primeList = sieveOfEratosthenes(maxRange);
    setPrimes(primeList);
    setGapAnalysis(analyzeGaps(primeList, config.connectionGap));
  }, [config.rangeEnd, config.connectionGap]);

  // Get color based on scheme
  const getColor = (index, total, scheme) => {
    const hue = (index / total) * 360;
    switch (scheme) {
      case 'viridis':
        return `hsl(${240 + hue * 0.5}, 70%, ${30 + (index / total) * 40}%)`;
      case 'rainbow':
        return `hsl(${hue}, 80%, 50%)`;
      case 'plasma':
        return `hsl(${280 - hue * 0.7}, 90%, ${40 + (index / total) * 30}%)`;
      default:
        return `hsl(${hue}, 70%, 50%)`;
    }
  };

  // Calculate optimal spacing
  const calculateSpacing = (mod, radius, totalMods) => {
    const circumference = 2 * Math.PI * radius;
    return circumference / mod;
  };

  // Draw visualization
  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;
    
    const ctx = canvas.getContext('2d');
    const width = canvas.width;
    const height = canvas.height;
    const centerX = width / 2;
    const centerY = height / 2;
    
    // Clear canvas
    ctx.fillStyle = '#0a0a0a';
    ctx.fillRect(0, 0, width, height);
    
    // Calculate moduli to display
    let moduli = [];
    if (config.useDynadic) {
      for (let n = 0; n <= config.dynadicExp; n++) {
        moduli.push(config.dynadicBase * Math.pow(2, n));
      }
    } else {
      for (let m = config.modStart; m <= config.modEnd; m++) {
        moduli.push(m);
      }
    }
    
    const totalMods = moduli.length;
    const maxRadius = Math.min(width, height) * 0.42;
    const radiusStep = maxRadius / totalMods;
    
    moduli.forEach((mod, modIndex) => {
      const radius = (modIndex + 1) * radiusStep;
      const color = getColor(modIndex, totalMods, config.colorScheme);
      
      // Draw ring
      ctx.strokeStyle = color;
      ctx.lineWidth = 2;
      ctx.globalAlpha = 0.3;
      ctx.beginPath();
      ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
      ctx.stroke();
      
      // Draw points on ring
      ctx.globalAlpha = 1;
      const spacing = calculateSpacing(mod, radius, totalMods);
      const primeSet = new Set(primes);
      
      for (let r = config.rangeStart; r <= Math.min(config.rangeEnd, mod - 1); r++) {
        const angle = (2 * Math.PI * r) / mod;
        const x = centerX + radius * Math.cos(angle - Math.PI / 2);
        const y = centerY + radius * Math.sin(angle - Math.PI / 2);
        
        // Check if r is prime and in range
        const isPrime = config.showPrimes && primeSet.has(r);
        
        ctx.beginPath();
        ctx.arc(x, y, isPrime ? 5 : 3, 0, 2 * Math.PI);
        ctx.fillStyle = isPrime ? '#ffff00' : color;
        ctx.fill();
        
        // Draw labels
        if (config.showLabels && modIndex < 5) {
          ctx.fillStyle = '#ffffff';
          ctx.font = '10px monospace';
          ctx.fillText(r.toString(), x + 8, y + 3);
        }
        
        // Draw connections for gap analysis
        if (config.showConnections && r + config.connectionGap < mod) {
          const r2 = r + config.connectionGap;
          const angle2 = (2 * Math.PI * r2) / mod;
          const x2 = centerX + radius * Math.cos(angle2 - Math.PI / 2);
          const y2 = centerY + radius * Math.sin(angle2 - Math.PI / 2);
          
          // Check GCD and prime gap
          const gcd = (a, b) => b === 0 ? a : gcd(b, a % b);
          const isGapPair = gapAnalysis.some(g => g.p1 === r && g.p2 === r2);
          
          if (gcd(r, mod) === 1 || isGapPair) {
            ctx.strokeStyle = isGapPair ? '#ff0000' : color;
            ctx.lineWidth = isGapPair ? 2 : 0.5;
            ctx.globalAlpha = isGapPair ? 0.8 : 0.2;
            ctx.beginPath();
            ctx.moveTo(x, y);
            ctx.lineTo(x2, y2);
            ctx.stroke();
          }
        }
      }
      
      // Draw mod label
      ctx.globalAlpha = 1;
      ctx.fillStyle = '#ffffff';
      ctx.font = 'bold 14px monospace';
      const labelX = centerX + radius * Math.cos(-Math.PI / 2) + 10;
      const labelY = centerY + radius * Math.sin(-Math.PI / 2);
      ctx.fillText(`mod ${mod}`, labelX, labelY);
    });
    
    // Draw legend
    ctx.globalAlpha = 1;
    ctx.fillStyle = 'rgba(0, 0, 0, 0.8)';
    ctx.fillRect(10, 10, 200, 140);
    ctx.strokeStyle = '#ffffff';
    ctx.strokeRect(10, 10, 200, 140);
    
    ctx.fillStyle = '#ffffff';
    ctx.font = '12px monospace';
    ctx.fillText('Legend:', 20, 30);
    ctx.fillStyle = '#ffff00';
    ctx.fillText('● Prime numbers', 20, 50);
    ctx.fillStyle = '#ff0000';
    ctx.fillText('— Prime gaps', 20, 70);
    ctx.fillStyle = '#ffffff';
    ctx.fillText(`Gap size: ${config.connectionGap}`, 20, 90);
    ctx.fillText(`Primes found: ${primes.length}`, 20, 110);
    ctx.fillText(`Gap pairs: ${gapAnalysis.length}`, 20, 130);
    
  }, [config, primes, gapAnalysis]);

  const downloadImage = () => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    
    // Add watermark
    ctx.globalAlpha = 0.7;
    ctx.fillStyle = '#ffffff';
    ctx.font = 'bold 20px monospace';
    ctx.fillText('© WessenGetachew', canvas.width - 220, canvas.height - 20);
    ctx.globalAlpha = 1;
    
    // Download
    const link = document.createElement('a');
    link.download = `modular_rings_${Date.now()}.jpg`;
    link.href = canvas.toDataURL('image/jpeg', 0.95);
    link.click();
  };

  return (
    <div className="w-full h-screen bg-gray-900 text-white p-4 overflow-auto">
      <div className="max-w-7xl mx-auto">
        <h1 className="text-3xl font-bold mb-4 text-center">
          Advanced Modular Arithmetic Ring Visualizer
        </h1>
        
        <div className="grid grid-cols-1 lg:grid-cols-4 gap-4 mb-4">
          {/* Controls */}
          <div className="lg:col-span-1 bg-gray-800 p-4 rounded-lg space-y-4">
            <div className="flex items-center gap-2 mb-2">
              <Settings className="w-5 h-5" />
              <h2 className="text-xl font-bold">Controls</h2>
            </div>
            
            <div>
              <label className="flex items-center gap-2 mb-2">
                <input
                  type="checkbox"
                  checked={config.useDynadic}
                  onChange={(e) => setConfig({...config, useDynadic: e.target.checked})}
                  className="w-4 h-4"
                />
                <span>Use Dyadic Family</span>
              </label>
            </div>
            
            {config.useDynadic ? (
              <>
                <div>
                  <label className="block mb-1">Base (m):</label>
                  <input
                    type="number"
                    value={config.dynadicBase}
                    onChange={(e) => setConfig({...config, dynadicBase: parseInt(e.target.value) || 1})}
                    className="w-full bg-gray-700 p-2 rounded"
                    min="1"
                  />
                </div>
                <div>
                  <label className="block mb-1">Max Exponent (n):</label>
                  <input
                    type="number"
                    value={config.dynadicExp}
                    onChange={(e) => setConfig({...config, dynadicExp: parseInt(e.target.value) || 0})}
                    className="w-full bg-gray-700 p-2 rounded"
                    min="0"
                    max="8"
                  />
                </div>
              </>
            ) : (
              <>
                <div>
                  <label className="block mb-1">Start Mod:</label>
                  <input
                    type="number"
                    value={config.modStart}
                    onChange={(e) => setConfig({...config, modStart: parseInt(e.target.value) || 1})}
                    className="w-full bg-gray-700 p-2 rounded"
                    min="1"
                  />
                </div>
                <div>
                  <label className="block mb-1">End Mod:</label>
                  <input
                    type="number"
                    value={config.modEnd}
                    onChange={(e) => setConfig({...config, modEnd: parseInt(e.target.value) || 1})}
                    className="w-full bg-gray-700 p-2 rounded"
                    min="1"
                  />
                </div>
              </>
            )}
            
            <div>
              <label className="block mb-1">Range Start (r):</label>
              <input
                type="number"
                value={config.rangeStart}
                onChange={(e) => setConfig({...config, rangeStart: parseInt(e.target.value) || 0})}
                className="w-full bg-gray-700 p-2 rounded"
                min="0"
              />
            </div>
            
            <div>
              <label className="block mb-1">Range End:</label>
              <input
                type="number"
                value={config.rangeEnd}
                onChange={(e) => setConfig({...config, rangeEnd: parseInt(e.target.value) || 1})}
                className="w-full bg-gray-700 p-2 rounded"
                min="1"
              />
            </div>
            
            <div>
              <label className="block mb-1">Connection Gap (2n):</label>
              <input
                type="number"
                value={config.connectionGap}
                onChange={(e) => setConfig({...config, connectionGap: parseInt(e.target.value) || 1})}
                className="w-full bg-gray-700 p-2 rounded"
                min="1"
              />
            </div>
            
            <div>
              <label className="block mb-1">Color Scheme:</label>
              <select
                value={config.colorScheme}
                onChange={(e) => setConfig({...config, colorScheme: e.target.value})}
                className="w-full bg-gray-700 p-2 rounded"
              >
                <option value="viridis">Viridis</option>
                <option value="rainbow">Rainbow</option>
                <option value="plasma">Plasma</option>
              </select>
            </div>
            
            <div>
              <label className="flex items-center gap-2">
                <input
                  type="checkbox"
                  checked={config.showLabels}
                  onChange={(e) => setConfig({...config, showLabels: e.target.checked})}
                  className="w-4 h-4"
                />
                <span>Show Labels</span>
              </label>
            </div>
            
            <div>
              <label className="flex items-center gap-2">
                <input
                  type="checkbox"
                  checked={config.showConnections}
                  onChange={(e) => setConfig({...config, showConnections: e.target.checked})}
                  className="w-4 h-4"
                />
                <span>Show Connections</span>
              </label>
            </div>
            
            <div>
              <label className="flex items-center gap-2">
                <input
                  type="checkbox"
                  checked={config.showPrimes}
                  onChange={(e) => setConfig({...config, showPrimes: e.target.checked})}
                  className="w-4 h-4"
                />
                <span>Highlight Primes</span>
              </label>
            </div>
            
            <button
              onClick={downloadImage}
              className="w-full bg-blue-600 hover:bg-blue-700 p-3 rounded-lg flex items-center justify-center gap-2 font-bold"
            >
              <Download className="w-5 h-5" />
              Download 8K JPEG
            </button>
          </div>
          
          {/* Canvas */}
          <div className="lg:col-span-3 bg-gray-800 p-4 rounded-lg">
            <canvas
              ref={canvasRef}
              width={7680}
              height={4320}
              className="w-full h-auto border border-gray-600 rounded"
              style={{ maxHeight: '80vh' }}
            />
          </div>
        </div>
        
        {/* Gap Analysis */}
        {gapAnalysis.length > 0 && (
          <div className="bg-gray-800 p-4 rounded-lg">
            <div className="flex items-center gap-2 mb-2">
              <Zap className="w-5 h-5 text-yellow-400" />
              <h2 className="text-xl font-bold">Prime Gap Analysis (Gap = {config.connectionGap})</h2>
            </div>
            <div className="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-2 max-h-40 overflow-y-auto">
              {gapAnalysis.slice(0, 100).map((gap, i) => (
                <div key={i} className="bg-gray-700 p-2 rounded text-sm">
                  {gap.p1} → {gap.p2}
                </div>
              ))}
            </div>
            {gapAnalysis.length > 100 && (
              <p className="text-sm text-gray-400 mt-2">
                Showing first 100 of {gapAnalysis.length} gap pairs
              </p>
            )}
          </div>
        )}
      </div>
    </div>
  );
};

export default ModularRingVisualizer;
