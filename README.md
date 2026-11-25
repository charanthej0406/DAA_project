<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Algorithm Explorer: Cargo & Cloud Resource Packing (0/1 Knapsack)</title>
  <!-- Tailwind CSS via CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
        },
      },
    };
  </script>
</head>
<body class="bg-slate-50 text-slate-900 antialiased selection:bg-indigo-100 selection:text-indigo-900">

  <!-- Top Navigation / Header -->
  <header class="bg-slate-900 text-white border-b border-slate-800 sticky top-0 z-30 shadow-md">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-3">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-indigo-600 flex items-center justify-center shadow-inner shrink-0">
          <!-- Box/Package SVG Icon -->
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
          </svg>
        </div>
        <div>
          <span class="text-xs font-mono uppercase tracking-wider text-indigo-400 font-semibold block">Algorithm Explorer • CS Project</span>
          <h1 class="text-lg sm:text-xl font-bold tracking-tight text-white">Cargo &amp; Cloud Resource Packing (0/1 Knapsack)</h1>
        </div>
      </div>

      <div class="flex items-center gap-2 self-start sm:self-auto">
        <button id="copySourceBtn" type="button" class="inline-flex items-center gap-1.5 px-3 py-2 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-medium border border-slate-700 transition">
          <svg class="w-4 h-4 text-indigo-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
          </svg>
          <span id="copyBtnLabel">Copy HTML for GitHub</span>
        </button>
      </div>
    </div>
  </header>

  <!-- Toast Notification Banner (Replaces alert()) -->
  <div id="toastBanner" class="hidden fixed bottom-5 right-5 z-50 max-w-sm bg-slate-900 text-white px-4 py-3 rounded-xl shadow-xl border border-slate-700 flex items-center gap-3 text-sm transition-all">
    <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 shrink-0"></span>
    <span id="toastMessage">Copied source code to clipboard!</span>
  </div>

  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">

    <!-- Section 1: Problem Overview (What, Why, What it Computes) -->
    <section class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 sm:p-8">
      <div class="flex flex-col md:flex-row md:items-center justify-between gap-2 pb-4 border-b border-slate-100">
        <div>
          <h2 class="text-xl font-bold text-slate-900">Problem Overview &amp; Real-World Motivation</h2>
          <p class="text-sm text-slate-500 mt-0.5">Comparing four classic algorithmic paradigms on the exact same combinatorial optimization dataset.</p>
        </div>
        <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-indigo-50 text-indigo-700 border border-indigo-100 self-start md:self-auto">
          Combinatorial Optimization • NP-Complete
        </span>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
        <!-- Card 1: What the problem is -->
        <div class="bg-slate-50 rounded-xl p-5 border border-slate-200/80">
          <div class="flex items-center gap-2.5 mb-2.5">
            <span class="w-8 h-8 rounded-lg bg-blue-100 text-blue-700 flex items-center justify-center font-bold text-sm">01</span>
            <h3 class="font-bold text-slate-900 text-base">What is the Problem?</h3>
          </div>
          <p class="text-sm text-slate-600 leading-relaxed">
            The <strong>0/1 Knapsack Optimization Problem</strong> asks: given a fixed maximum weight capacity <em>W</em> and a set of <em>n</em> indivisible items—each with a weight (or size) and a value (or priority)—which subset of items should be chosen to <strong>maximize total value</strong> without exceeding <em>W</em>?
          </p>
        </div>

        <!-- Card 2: Why it matters in real life -->
        <div class="bg-slate-50 rounded-xl p-5 border border-slate-200/80">
          <div class="flex items-center gap-2.5 mb-2.5">
            <span class="w-8 h-8 rounded-lg bg-emerald-100 text-emerald-700 flex items-center justify-center font-bold text-sm">02</span>
            <h3 class="font-bold text-slate-900 text-base">Why It Matters in Real Life</h3>
          </div>
          <p class="text-sm text-slate-600 leading-relaxed">
            Resource-constrained packing is everywhere: scheduling Docker containers onto RAM-limited cloud virtual machines, loading air-cargo pallets or emergency relief drones with strict payload limits, and selecting high-ROI R&amp;D projects under a fixed capital budget.
          </p>
        </div>

        <!-- Card 3: What the program computes -->
        <div class="bg-slate-50 rounded-xl p-5 border border-slate-200/80">
          <div class="flex items-center gap-2.5 mb-2.5">
            <span class="w-8 h-8 rounded-lg bg-purple-100 text-purple-700 flex items-center justify-center font-bold text-sm">03</span>
            <h3 class="font-bold text-slate-900 text-base">What This Program Computes</h3>
          </div>
          <p class="text-sm text-slate-600 leading-relaxed">
            Given your capacity limit and custom item list, the engine runs <strong>Brute Force</strong>, <strong>Greedy Heuristic</strong>, <strong>Backtracking (Branch &amp; Bound)</strong>, and <strong>Dynamic Programming</strong>—computing the selected items, total value, capacity utilization, execution time, and asymptotic complexity.
          </p>
        </div>
      </div>
    </section>

    <!-- Main Interactive Workspace: Left (Input Form) + Right (Algorithm Tabs & Output) -->
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">

      <!-- Left Column (5 cols): Interactive Data Form & Presets -->
      <section class="lg:col-span-5 bg-white rounded-2xl border border-slate-200 shadow-sm p-6 space-y-6">
        <div>
          <h2 class="text-lg font-bold text-slate-900">1. Configure Problem Input</h2>
          <p class="text-xs text-slate-500 mt-1">Load a real-world preset or enter custom items and capacity below.</p>
        </div>

        <!-- Preset Scenario Buttons -->
        <div>
          <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 mb-2">Quick-Load Scenarios</label>
          <div class="grid grid-cols-1 sm:grid-cols-3 lg:grid-cols-1 xl:grid-cols-3 gap-2">
            <button type="button" onclick="loadPreset('cloud')" class="px-3 py-2 rounded-xl text-xs font-semibold bg-indigo-50 hover:bg-indigo-100 text-indigo-700 border border-indigo-200 transition text-left sm:text-center">
              ☁️ Cloud VM RAM
            </button>
            <button type="button" onclick="loadPreset('drone')" class="px-3 py-2 rounded-xl text-xs font-semibold bg-emerald-50 hover:bg-emerald-100 text-emerald-700 border border-emerald-200 transition text-left sm:text-center">
              🚁 Rescue Drone
            </button>
            <button type="button" onclick="loadPreset('trap')" class="px-3 py-2 rounded-xl text-xs font-semibold bg-amber-50 hover:bg-amber-100 text-amber-800 border border-amber-200 transition text-left sm:text-center" title="Demonstrates where Greedy fails to find the optimal solution">
              ⚠️ Greedy Trap
            </button>
          </div>
        </div>

        <!-- Capacity Input -->
        <div>
          <label for="capacityInput" class="block text-sm font-semibold text-slate-700 mb-1.5">
            Maximum Capacity <span class="text-slate-400 font-normal">(e.g., GB RAM or kg)</span>
          </label>
          <div class="relative">
            <input
              id="capacityInput"
              type="number"
              min="1"
              max="500"
              step="1"
              value="15"
              class="w-full rounded-xl border border-slate-300 px-3.5 py-2.5 text-sm font-mono font-semibold text-slate-900 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 transition"
              placeholder="Enter positive integer capacity..."
            />
            <span class="absolute right-3.5 top-2.5 text-xs font-mono text-slate-400">MAX UNITS</span>
          </div>
        </div>

        <!-- Dynamic Item List -->
        <div class="space-y-3">
          <div class="flex items-center justify-between">
            <label class="block text-sm font-semibold text-slate-700">
              Candidate Items (<span id="itemCountBadge">0</span>/18)
            </label>
            <button type="button" onclick="addItemRow()" class="inline-flex items-center gap-1 px-3 py-1.5 rounded-lg bg-slate-900 hover:bg-slate-800 text-white text-xs font-semibold transition">
              <span>+ Add Item</span>
            </button>
          </div>

          <!-- Column Headers -->
          <div class="grid grid-cols-12 gap-2 px-1 text-[11px] font-semibold uppercase tracking-wider text-slate-400">
            <div class="col-span-5">Item Name</div>
            <div class="col-span-3">Weight</div>
            <div class="col-span-3">Value</div>
            <div class="col-span-1 text-center">Del</div>
          </div>

          <!-- Dynamic Rows Container -->
          <div id="itemsContainer" class="space-y-2 max-h-[340px] overflow-y-auto pr-1">
            <!-- Populated via JS -->
          </div>
        </div>

        <!-- Validation Error Alert Box -->
        <div id="validationErrorBox" class="hidden rounded-xl bg-red-50 border border-red-200 p-4 text-sm text-red-800 space-y-1">
          <div class="flex items-center gap-2 font-bold text-red-900">
            <svg class="w-4 h-4 text-red-600 shrink-0" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <span>Invalid Input Detected</span>
          </div>
          <ul id="validationErrorList" class="list-disc list-inside text-xs space-y-0.5 text-red-700 pl-1"></ul>
        </div>

        <!-- Exponential Warning Box (if n > 15) -->
        <div id="performanceWarningBox" class="hidden rounded-xl bg-amber-50 border border-amber-200 p-3 text-xs text-amber-800">
          <strong>Heads up:</strong> With more than 15 items, Brute Force checks up to <span class="font-mono font-bold">2^n</span> combinations. Maximum items are capped at 18 so your browser stays responsive.
        </div>

        <!-- Solve Button -->
        <button id="solveBtn" type="button" onclick="handleSolve()" class="w-full py-3 px-4 rounded-xl bg-indigo-600 hover:bg-indigo-700 active:bg-indigo-800 text-white font-semibold text-sm shadow-sm hover:shadow transition flex items-center justify-center gap-2">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <span>Run All 4 Algorithms</span>
        </button>
      </section>

      <!-- Right Column (7 cols): Interactive Algorithm Tabs & Detailed Results -->
      <section class="lg:col-span-7 space-y-6">

        <!-- Algorithm Switcher Tabs -->
        <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
          <div class="border-b border-slate-200 bg-slate-50/70 p-2">
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2" role="tablist" aria-label="Algorithm Approaches">
              <button type="button" role="tab" id="tab-bruteforce" onclick="switchTab('bruteforce')" class="algo-tab px-3 py-2.5 rounded-xl text-xs sm:text-sm font-semibold transition text-center">
                1. Brute Force
              </button>
              <button type="button" role="tab" id="tab-greedy" onclick="switchTab('greedy')" class="algo-tab px-3 py-2.5 rounded-xl text-xs sm:text-sm font-semibold transition text-center">
                2. Greedy Ratio
              </button>
              <button type="button" role="tab" id="tab-backtracking" onclick="switchTab('backtracking')" class="algo-tab px-3 py-2.5 rounded-xl text-xs sm:text-sm font-semibold transition text-center">
                3. Backtracking
              </button>
              <button type="button" role="tab" id="tab-dp" onclick="switchTab('dp')" class="algo-tab px-3 py-2.5 rounded-xl text-xs sm:text-sm font-semibold transition text-center">
                4. Dynamic Prog.
              </button>
            </div>
          </div>

          <!-- Active Algorithm Content Panel -->
          <div id="activeAlgorithmPanel" class="p-6 space-y-6">
            <!-- Header & Complexity Badges -->
            <div class="flex flex-col sm:flex-row sm:items-start justify-between gap-4 pb-4 border-b border-slate-100">
              <div>
                <div class="flex items-center gap-2 flex-wrap">
                  <h2 id="algoTitle" class="text-xl font-bold text-slate-900">Brute Force (Exhaustive Search)</h2>
                  <span id="optimalityBadge" class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800">
                    Guaranteed Optimal
                  </span>
                </div>
                <p id="algoSubtitle" class="text-xs text-slate-500 mt-1">Evaluates every possible subset combination to find the true global maximum.</p>
              </div>

              <!-- Big-O Complexity Pills -->
              <div class="flex flex-wrap sm:flex-col gap-2 shrink-0">
                <div class="inline-flex items-center justify-between gap-2 px-3 py-1.5 rounded-lg bg-slate-900 text-white text-xs font-mono">
                  <span class="text-slate-400">Time:</span>
                  <span id="timeComplexityBadge" class="font-bold text-amber-300">O(2^n)</span>
                </div>
                <div class="inline-flex items-center justify-between gap-2 px-3 py-1.5 rounded-lg bg-slate-100 text-slate-800 text-xs font-mono border border-slate-200">
                  <span class="text-slate-500">Space:</span>
                  <span id="spaceComplexityBadge" class="font-bold text-indigo-700">O(n)</span>
                </div>
              </div>
            </div>

            <!-- Plain-Text Step-by-Step Explanation -->
            <div class="bg-slate-50 rounded-xl p-5 border border-slate-200/80 space-y-2.5">
              <h3 class="text-xs font-bold uppercase tracking-wider text-slate-500 flex items-center gap-1.5">
                <svg class="w-4 h-4 text-indigo-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
                <span>Step-by-Step Algorithmic Logic</span>
              </h3>
              <ol id="algoStepsList" class="list-decimal list-inside space-y-1.5 text-sm text-slate-700 leading-relaxed">
                <!-- Populated dynamically -->
              </ol>
            </div>

            <!-- Computed Output Metrics Grid -->
            <div class="space-y-4">
              <h3 class="text-xs font-bold uppercase tracking-wider text-slate-500">Computed Output for Your Input</h3>

              <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
                <div class="bg-indigo-50/70 border border-indigo-100 rounded-xl p-3.5">
                  <span class="text-[11px] font-semibold text-indigo-600 uppercase block">Total Value</span>
                  <span id="metricTotalValue" class="text-2xl font-extrabold font-mono text-indigo-950 mt-0.5 block">0</span>
                </div>
                <div class="bg-slate-50 border border-slate-200/80 rounded-xl p-3.5">
                  <span class="text-[11px] font-semibold text-slate-500 uppercase block">Weight Used</span>
                  <span id="metricWeightUsed" class="text-xl font-bold font-mono text-slate-900 mt-0.5 block">0 / 15</span>
                </div>
                <div class="bg-slate-50 border border-slate-200/80 rounded-xl p-3.5">
                  <span class="text-[11px] font-semibold text-slate-500 uppercase block">Execution Time</span>
                  <span id="metricExecTime" class="text-xl font-bold font-mono text-slate-900 mt-0.5 block">0.00 ms</span>
                </div>
                <div class="bg-slate-50 border border-slate-200/80 rounded-xl p-3.5">
                  <span id="metricOpsLabel" class="text-[11px] font-semibold text-slate-500 uppercase block">Subsets Checked</span>
                  <span id="metricOpsCount" class="text-xl font-bold font-mono text-slate-900 mt-0.5 block">0</span>
                </div>
              </div>

              <!-- Visual Capacity Progress Bar -->
              <div class="bg-white border border-slate-200 rounded-xl p-4 space-y-2">
                <div class="flex items-center justify-between text-xs font-semibold">
                  <span class="text-slate-600">Knapsack Capacity Utilization</span>
                  <span id="capacityPercentLabel" class="font-mono text-indigo-600">0%</span>
                </div>
                <div class="w-full h-3.5 bg-slate-100 rounded-full overflow-hidden border border-slate-200/70">
                  <div id="capacityProgressBar" class="h-full bg-indigo-600 rounded-full transition-all duration-300" style="width: 0%"></div>
                </div>
              </div>

              <!-- Selected Items Chips/Table -->
              <div class="bg-white border border-slate-200 rounded-xl p-4 space-y-3">
                <div class="flex items-center justify-between">
                  <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Selected Items Packed</span>
                  <span id="selectedCountLabel" class="text-xs font-mono text-slate-500">0 items</span>
                </div>
                <div id="selectedItemsContainer" class="flex flex-wrap gap-2">
                  <!-- Populated dynamically -->
                </div>
              </div>

              <!-- Optional Dynamic Programming Table Preview (Shown only when DP tab is active) -->
              <div id="dpTablePreviewWrapper" class="hidden bg-slate-900 text-slate-100 rounded-xl p-4 space-y-2.5 overflow-hidden">
                <div class="flex items-center justify-between">
                  <span class="text-xs font-mono font-semibold text-indigo-300">DP Tabulation Matrix Preview (dp[i][w])</span>
                  <span class="text-[11px] text-slate-400">Bottom-right cell = Optimal Value</span>
                </div>
                <div id="dpTableScrollArea" class="overflow-x-auto max-h-56 text-xs font-mono">
                  <!-- Rendered dynamically for DP -->
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Side-by-Side Comparison Summary Table -->
        <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 space-y-4">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2">
            <div>
              <h3 class="text-base font-bold text-slate-900">Side-by-Side Benchmark Comparison</h3>
              <p class="text-xs text-slate-500">Click any row to inspect that algorithm's step-by-step execution above.</p>
            </div>
          </div>

          <div class="overflow-x-auto">
            <table class="w-full text-left border-collapse text-xs sm:text-sm">
              <thead>
                <tr class="border-b border-slate-200 text-[11px] font-bold uppercase tracking-wider text-slate-500 bg-slate-50">
                  <th class="py-3 px-3 rounded-tl-lg">Approach</th>
                  <th class="py-3 px-3">Time</th>
                  <th class="py-3 px-3">Space</th>
                  <th class="py-3 px-3">Total Value</th>
                  <th class="py-3 px-3">Weight</th>
                  <th class="py-3 px-3">Runtime</th>
                  <th class="py-3 px-3 rounded-tr-lg">Status</th>
                </tr>
              </thead>
              <tbody id="comparisonTableBody" class="divide-y divide-slate-100">
                <!-- Populated dynamically -->
              </tbody>
            </table>
          </div>
        </div>

      </section>
    </div>
  </main>

  <!-- Footer -->
  <footer class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 text-center text-xs text-slate-400 border-t border-slate-200 mt-8">
    Algorithm Explorer: 0/1 Knapsack Optimization • Built as a self-contained single-file web application ready for GitHub Pages, Vercel, or Netlify deployment.
  </footer>

  <script>
    // =========================================================================
    // 1. STATE & PRESET DATASETS
    // =========================================================================
    const PRESETS = {
      cloud: {
        capacity: 16,
        items: [
          { name: 'Auth Microservice', weight: 4, value: 45 },
          { name: 'Redis Cache Node', weight: 3, value: 35 },
          { name: 'ML Inference Worker', weight: 8, value: 95 },
          { name: 'Analytics Pipeline', weight: 5, value: 50 },
          { name: 'Billing API', weight: 2, value: 25 },
          { name: 'Search Indexer', weight: 6, value: 65 }
        ]
      },
      drone: {
        capacity: 15,
        items: [
          { name: 'Trauma MedKit', weight: 5, value: 60 },
          { name: 'Satellite Beacon', weight: 3, value: 45 },
          { name: 'Thermal Blanket Pack', weight: 4, value: 30 },
          { name: 'Water Purification', weight: 6, value: 55 },
          { name: 'Portable Defibrillator', weight: 7, value: 85 },
          { name: 'Emergency Rations', weight: 2, value: 20 }
        ]
      },
      trap: {
        // Classic Greedy Counterexample:
        // Capacity = 10.
        // Item A: weight 6, value 60 (ratio = 10.0 -> Greedy picks this first!)
        // Item B: weight 5, value 48 (ratio = 9.6)
        // Item C: weight 5, value 48 (ratio = 9.6)
        // Greedy picks A (value 60, weight 6) and cannot fit B or C -> Total = 60.
        // Optimal (DP / Brute Force / Backtracking) picks B + C -> Total = 96, weight 10!
        capacity: 10,
        items: [
          { name: 'Heavy Server Blade (High Ratio)', weight: 6, value: 60 },
          { name: 'Database Replica A', weight: 5, value: 48 },
          { name: 'Database Replica B', weight: 5, value: 48 },
          { name: 'Logging Daemon', weight: 3, value: 20 }
        ]
      }
    };

    const ALGORITHM_METADATA = {
      bruteforce: {
        title: 'Brute Force (Exhaustive Search)',
        subtitle: 'Recursively explores every include/exclude branch (2^n subsets) to guarantee the exact optimum.',
        timeComplexity: 'O(2^n)',
        spaceComplexity: 'O(n)',
        opsLabel: 'Subsets Evaluated',
        steps: [
          'Start at item index i = 0 with current weight = 0 and current value = 0.',
          'For each item, branch into two recursive decisions: EXCLUDE the item, or INCLUDE the item (if currentWeight + item.weight <= capacity).',
          'Continue branching down to the leaf nodes (i == n), evaluating all 2^n possible subset combinations.',
          'Track and return the valid subset that produces the highest cumulative value without exceeding capacity.'
        ]
      },
      greedy: {
        title: 'Greedy Approach (Value-to-Weight Ratio)',
        subtitle: 'Sorts items by density (value ÷ weight) and packs the highest-ratio items first.',
        timeComplexity: 'O(n log n)',
        spaceComplexity: 'O(n)',
        opsLabel: 'Items Scanned',
        steps: [
          'Compute the efficiency ratio (value / weight) for every candidate item.',
          'Sort all items in descending order based on their value-to-weight ratio in O(n log n) time.',
          'Iterate through the sorted list once: if the current item fits within the remaining capacity, pack it immediately.',
          'Note: Because 0/1 items cannot be split into fractions, Greedy is fast but can miss the global optimum (try the "Greedy Trap" preset!).'
        ]
      },
      backtracking: {
        title: 'Backtracking (Branch & Bound Pruning)',
        subtitle: 'Explores the decision tree but prunes branches that exceed capacity or cannot beat the best solution found so far.',
        timeComplexity: 'O(2^n) worst / pruned',
        spaceComplexity: 'O(n)',
        opsLabel: 'Branches Pruned',
        steps: [
          'Sort items by value-to-weight ratio descending so high-value solutions are discovered early.',
          'Traverse the binary decision tree (Include vs. Exclude) while tracking the best total value found so far (bestValue).',
          'Before exploring a branch, compute a fractional upper bound of the maximum possible value achievable from remaining items.',
          'If remaining weight exceeds capacity OR upperBound <= bestValue, immediately PRUNE (cut off) that entire subtree.'
        ]
      },
      dp: {
        title: 'Dynamic Programming (Bottom-Up Tabulation)',
        subtitle: 'Solves overlapping subproblems once and stores optimal sub-capacities in a 2D table dp[i][w].',
        timeComplexity: 'O(n × W)',
        spaceComplexity: 'O(n × W)',
        opsLabel: 'DP States Computed',
        steps: [
          'Create a 2D table dp of size (n + 1) × (W + 1), initialized to 0, where dp[i][w] represents the max value using the first i items with capacity w.',
          'For each item i from 1 to n and each capacity w from 1 to W: if item weight > w, copy dp[i - 1][w].',
          'Otherwise, take max(dp[i - 1][w], item.value + dp[i - 1][w - item.weight])—choosing the better of excluding or including item i.',
          'Reconstruct the chosen items by backtracking from dp[n][W] wherever dp[i][w] != dp[i - 1][w].'
        ]
      }
    };

    let currentItems = [];
    let activeTab = 'bruteforce';
    let latestResults = null;

    // =========================================================================
    // 2. DOM INITIALIZATION & DYNAMIC FORM MANAGEMENT
    // =========================================================================
    window.addEventListener('DOMContentLoaded', () => {
      loadPreset('cloud');
      setupCopySourceButton();
    });

    function loadPreset(presetKey) {
      const preset = PRESETS[presetKey];
      if (!preset) return;
      document.getElementById('capacityInput').value = preset.capacity;
      currentItems = preset.items.map((item, idx) => ({
        id: Date.now() + idx,
        name: item.name,
        weight: item.weight,
        value: item.value
      }));
      renderItemRows();
      handleSolve();
    }

    function addItemRow() {
      if (currentItems.length >= 18) {
        showToast('Maximum of 18 items reached to keep exponential algorithms responsive.');
        return;
      }
      currentItems.push({
        id: Date.now() + Math.random(),
        name: `Module ${currentItems.length + 1}`,
        weight: 3,
        value: 30
      });
      renderItemRows();
    }

    function removeItemRow(index) {
      if (currentItems.length <= 1) {
        showToast('At least one item is required.');
        return;
      }
      currentItems.splice(index, 1);
      renderItemRows();
    }

    function syncItemsFromDOM() {
      const rows = document.querySelectorAll('.item-row');
      const updated = [];
      rows.forEach((row, idx) => {
        const nameVal = row.querySelector('.item-name').value;
        const weightVal = row.querySelector('.item-weight').value;
        const valueVal = row.querySelector('.item-value').value;
        updated.push({
          id: currentItems[idx]?.id || idx,
          name: nameVal,
          weight: weightVal === '' ? '' : Number(weightVal),
          value: valueVal === '' ? '' : Number(valueVal)
        });
      });
      currentItems = updated;
    }

    function renderItemRows() {
      const container = document.getElementById('itemsContainer');
      container.innerHTML = '';

      currentItems.forEach((item, index) => {
        const row = document.createElement('div');
        row.className = 'item-row grid grid-cols-12 gap-2 items-center bg-slate-50 p-2 rounded-xl border border-slate-200/80';
        row.innerHTML = `
          <div class="col-span-5">
            <input type="text" value="${escapeHtml(item.name)}" placeholder="Item name"
              oninput="syncItemsFromDOM()"
              class="item-name w-full rounded-lg border border-slate-300 bg-white px-2.5 py-1.5 text-xs font-medium text-slate-800 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </div>
          <div class="col-span-3">
            <input type="number" min="1" step="1" value="${item.weight}" placeholder="Wt"
              oninput="syncItemsFromDOM()"
              class="item-weight w-full rounded-lg border border-slate-300 bg-white px-2 py-1.5 text-xs font-mono text-slate-800 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </div>
          <div class="col-span-3">
            <input type="number" min="1" step="1" value="${item.value}" placeholder="Val"
              oninput="syncItemsFromDOM()"
              class="item-value w-full rounded-lg border border-slate-300 bg-white px-2 py-1.5 text-xs font-mono text-slate-800 focus:outline-none focus:ring-2 focus:ring-indigo-500" />
          </div>
          <div class="col-span-1 flex justify-center">
            <button type="button" onclick="removeItemRow(${index})" title="Remove item"
              class="p-1.5 rounded-lg text-slate-400 hover:text-red-600 hover:bg-red-50 transition">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        `;
        container.appendChild(row);
      });

      document.getElementById('itemCountBadge').textContent = currentItems.length;
      const warnBox = document.getElementById('performanceWarningBox');
      if (currentItems.length > 15) {
        warnBox.classList.remove('hidden');
      } else {
        warnBox.classList.add('hidden');
      }
    }

    // =========================================================================
    // 3. STRICT INPUT VALIDATION
    // =========================================================================
    function validateInputs() {
      syncItemsFromDOM();
      const errors = [];
      const capacityRaw = document.getElementById('capacityInput').value;
      const capacity = Number(capacityRaw);

      if (capacityRaw === '' || isNaN(capacity) || !Number.isInteger(capacity) || capacity <= 0) {
        errors.push('Maximum Capacity must be a positive whole integer (e.g., 15).');
      } else if (capacity > 500) {
        errors.push('Maximum Capacity cannot exceed 500 units so the 2D DP table remains crisp and readable.');
      }

      if (currentItems.length === 0) {
        errors.push('Please add at least one candidate item.');
      } else if (currentItems.length > 18) {
        errors.push('Please keep the item count at 18 or fewer so O(2^n) algorithms complete instantaneously.');
      }

      currentItems.forEach((item, idx) => {
        const rowNum = idx + 1;
        if (!item.name || item.name.trim() === '') {
          errors.push(`Row #${rowNum}: Item Name cannot be empty.`);
        }
        if (item.weight === '' || isNaN(item.weight) || !Number.isInteger(item.weight) || item.weight <= 0) {
          errors.push(`Row #${rowNum} (${item.name || 'Unnamed'}): Weight must be a positive integer (> 0).`);
        }
        if (item.value === '' || isNaN(item.value) || item.value <= 0) {
          errors.push(`Row #${rowNum} (${item.name || 'Unnamed'}): Value must be a positive number (> 0).`);
        }
      });

      const errorBox = document.getElementById('validationErrorBox');
      const errorList = document.getElementById('validationErrorList');

      if (errors.length > 0) {
        errorList.innerHTML = errors.map(err => `<li>${escapeHtml(err)}</li>`).join('');
        errorBox.classList.remove('hidden');
        return null;
      } else {
        errorBox.classList.add('hidden');
        errorList.innerHTML = '';
        return {
          capacity,
          items: currentItems.map((it, idx) => ({
            index: idx,
            name: it.name.trim(),
            weight: Number(it.weight),
            value: Number(it.value)
          }))
        };
      }
    }

    // =========================================================================
    // 4. FOUR ALGORITHMIC IMPLEMENTATIONS
    // =========================================================================

    // Approach 1: Brute Force (Exhaustive Recursion over 2^n subsets)
    function solveBruteForce(items, capacity) {
      const start = performance.now();
      let subsetsEvaluated = 0;
      let bestValue = 0;
      let bestWeight = 0;
      let bestSubset = [];

      function dfs(index, currentWeight, currentValue, chosen) {
        if (index === items.length) {
          subsetsEvaluated++;
          if (currentValue > bestValue) {
            bestValue = currentValue;
            bestWeight = currentWeight;
            bestSubset = [...chosen];
          }
          return;
        }

        // Branch 1: Exclude items[index]
        dfs(index + 1, currentWeight, currentValue, chosen);

        // Branch 2: Include items[index] if within capacity
        if (currentWeight + items[index].weight <= capacity) {
          chosen.push(items[index]);
          dfs(index + 1, currentWeight + items[index].weight, currentValue + items[index].value, chosen);
          chosen.pop();
        }
      }

      dfs(0, 0, 0, []);
      const execTime = performance.now() - start;

      return {
        key: 'bruteforce',
        selectedItems: bestSubset,
        totalValue: bestValue,
        totalWeight: bestWeight,
        execTimeMs: execTime,
        opsCount: subsetsEvaluated
      };
    }

    // Approach 2: Greedy Heuristic (Sort by Value/Weight Ratio)
    function solveGreedy(items, capacity) {
      const start = performance.now();
      let itemsScanned = 0;

      // Sort descending by value-to-weight ratio
      const sorted = [...items].sort((a, b) => (b.value / b.weight) - (a.value / a.weight));

      let currentWeight = 0;
      let totalValue = 0;
      const selected = [];

      for (const item of sorted) {
        itemsScanned++;
        if (currentWeight + item.weight <= capacity) {
          selected.push(item);
          currentWeight += item.weight;
          totalValue += item.value;
        }
      }

      const execTime = performance.now() - start;
      return {
        key: 'greedy',
        selectedItems: selected,
        totalValue,
        totalWeight: currentWeight,
        execTimeMs: execTime,
        opsCount: itemsScanned
      };
    }

    // Approach 3: Backtracking with Branch & Bound Pruning
    function solveBacktracking(items, capacity) {
      const start = performance.now();
      // Sort by value/weight ratio descending to tighten upper bounds early
      const sorted = [...items].sort((a, b) => (b.value / b.weight) - (a.value / a.weight));
      const n = sorted.length;

      let bestValue = 0;
      let bestWeight = 0;
      let bestSubset = [];
      let branchesPruned = 0;

      // Fractional relaxation upper bound from index `idx`
      function computeUpperBound(idx, currentWeight, currentValue) {
        let bound = currentValue;
        let remCap = capacity - currentWeight;
        for (let i = idx; i < n; i++) {
          if (sorted[i].weight <= remCap) {
            remCap -= sorted[i].weight;
            bound += sorted[i].value;
          } else {
            bound += (sorted[i].value / sorted[i].weight) * remCap;
            break;
          }
        }
        return bound;
      }

      function backtrack(idx, currentWeight, currentValue, chosen) {
        if (currentValue > bestValue) {
          bestValue = currentValue;
          bestWeight = currentWeight;
          bestSubset = [...chosen];
        }
        if (idx === n) return;

        // Upper bound check before exploring children
        const bound = computeUpperBound(idx, currentWeight, currentValue);
        if (bound <= bestValue) {
          branchesPruned++;
          return;
        }

        // 1. Explore INCLUDE branch first (if valid)
        if (currentWeight + sorted[idx].weight <= capacity) {
          chosen.push(sorted[idx]);
          backtrack(idx + 1, currentWeight + sorted[idx].weight, currentValue + sorted[idx].value, chosen);
          chosen.pop();
        } else {
          branchesPruned++;
        }

        // 2. Explore EXCLUDE branch (only if remaining bound still beats bestValue)
        const excludeBound = computeUpperBound(idx + 1, currentWeight, currentValue);
        if (excludeBound > bestValue) {
          backtrack(idx + 1, currentWeight, currentValue, chosen);
        } else {
          branchesPruned++;
        }
      }

      backtrack(0, 0, 0, []);
      const execTime = performance.now() - start;

      return {
        key: 'backtracking',
        selectedItems: bestSubset,
        totalValue: bestValue,
        totalWeight: bestWeight,
        execTimeMs: execTime,
        opsCount: branchesPruned
      };
    }

    // Approach 4: Dynamic Programming (Bottom-Up 2D Tabulation)
    function solveDynamicProgramming(items, capacity) {
      const start = performance.now();
      const n = items.length;
      const dp = Array.from({ length: n + 1 }, () => Array(capacity + 1).fill(0));
      let statesComputed = 0;

      for (let i = 1; i <= n; i++) {
        const { weight, value } = items[i - 1];
        for (let w = 0; w <= capacity; w++) {
          statesComputed++;
          if (weight <= w) {
            dp[i][w] = Math.max(dp[i - 1][w], value + dp[i - 1][w - weight]);
          } else {
            dp[i][w] = dp[i - 1][w];
          }
        }
      }

      // Backtrack through table to recover selected items
      const selected = [];
      let w = capacity;
      let totalWeight = 0;
      for (let i = n; i > 0; i--) {
        if (dp[i][w] !== dp[i - 1][w]) {
          const item = items[i - 1];
          selected.push(item);
          w -= item.weight;
          totalWeight += item.weight;
        }
      }
      selected.reverse();

      const execTime = performance.now() - start;

      return {
        key: 'dp',
        selectedItems: selected,
        totalValue: dp[n][capacity],
        totalWeight,
        execTimeMs: execTime,
        opsCount: statesComputed,
        dpTable: dp
      };
    }

    // =========================================================================
    // 5. EXECUTION CONTROLLER & UI RENDERING
    // =========================================================================
    function handleSolve() {
      const validData = validateInputs();
      if (!validData) return;

      const { capacity, items } = validData;

      const bf = solveBruteForce(items, capacity);
      const gr = solveGreedy(items, capacity);
      const bt = solveBacktracking(items, capacity);
      const dp = solveDynamicProgramming(items, capacity);

      const globalOptimalValue = dp.totalValue;

      latestResults = {
        capacity,
        items,
        globalOptimalValue,
        algorithms: {
          bruteforce: { ...bf, isOptimal: bf.totalValue === globalOptimalValue },
          greedy: { ...gr, isOptimal: gr.totalValue === globalOptimalValue },
          backtracking: { ...bt, isOptimal: bt.totalValue === globalOptimalValue },
          dp: { ...dp, isOptimal: true }
        }
      };

      renderActiveTab();
      renderComparisonTable();
    }

    function switchTab(tabKey) {
      activeTab = tabKey;
      renderActiveTab();
    }

    function renderActiveTab() {
      // Update Tab Styling
      document.querySelectorAll('.algo-tab').forEach(btn => {
        btn.classList.remove('bg-indigo-600', 'text-white', 'shadow-sm');
        btn.classList.add('text-slate-600', 'hover:bg-slate-200/70');
      });
      const activeBtn = document.getElementById(`tab-${activeTab}`);
      if (activeBtn) {
        activeBtn.classList.remove('text-slate-600', 'hover:bg-slate-200/70');
        activeBtn.classList.add('bg-indigo-600', 'text-white', 'shadow-sm');
      }

      if (!latestResults) return;

      const meta = ALGORITHM_METADATA[activeTab];
      const res = latestResults.algorithms[activeTab];
      const cap = latestResults.capacity;

      // Update Metadata
      document.getElementById('algoTitle').textContent = meta.title;
      document.getElementById('algoSubtitle').textContent = meta.subtitle;
      document.getElementById('timeComplexityBadge').textContent = meta.timeComplexity;
      document.getElementById('spaceComplexityBadge').textContent = meta.spaceComplexity;
      document.getElementById('metricOpsLabel').textContent = meta.opsLabel;

      // Optimality Badge
      const optBadge = document.getElementById('optimalityBadge');
      if (res.isOptimal) {
        optBadge.className = 'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800';
        optBadge.textContent = '✓ Optimal Solution';
      } else {
        const diff = latestResults.globalOptimalValue - res.totalValue;
        optBadge.className = 'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-amber-100 text-amber-800';
        optBadge.textContent = `Suboptimal (−${diff} value vs Optimal)`;
      }

      // Steps List
      const stepsEl = document.getElementById('algoStepsList');
      stepsEl.innerHTML = meta.steps.map(step => `<li>${escapeHtml(step)}</li>`).join('');

      // Metrics
      document.getElementById('metricTotalValue').textContent = res.totalValue;
      document.getElementById('metricWeightUsed').textContent = `${res.totalWeight} / ${cap}`;
      document.getElementById('metricExecTime').textContent = `${res.execTimeMs.toFixed(3)} ms`;
      document.getElementById('metricOpsCount').textContent = res.opsCount.toLocaleString();

      // Capacity Bar
      const pct = Math.min(100, Math.round((res.totalWeight / cap) * 100));
      document.getElementById('capacityPercentLabel').textContent = `${pct}% (${res.totalWeight} of ${cap} units)`;
      const bar = document.getElementById('capacityProgressBar');
      bar.style.width = `${pct}%`;
      bar.className = `h-full rounded-full transition-all duration-300 ${res.isOptimal ? 'bg-indigo-600' : 'bg-amber-500'}`;

      // Selected Items
      const selContainer = document.getElementById('selectedItemsContainer');
      document.getElementById('selectedCountLabel').textContent = `${res.selectedItems.length} item(s)`;

      if (res.selectedItems.length === 0) {
        selContainer.innerHTML = `<span class="text-xs text-slate-400 italic">No items fit within the specified capacity.</span>`;
      } else {
        selContainer.innerHTML = res.selectedItems.map(item => `
          <div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-xl bg-indigo-50 border border-indigo-200 text-xs">
            <span class="font-semibold text-slate-900">${escapeHtml(item.name)}</span>
            <span class="font-mono text-[11px] px-1.5 py-0.5 rounded bg-white text-slate-600 border border-slate-200">Wt: ${item.weight}</span>
            <span class="font-mono text-[11px] px-1.5 py-0.5 rounded bg-indigo-600 text-white font-semibold">Val: ${item.value}</span>
          </div>
        `).join('');
      }

      // DP Table Preview (only on DP tab)
      const dpWrapper = document.getElementById('dpTablePreviewWrapper');
      if (activeTab === 'dp' && res.dpTable) {
        dpWrapper.classList.remove('hidden');
        renderDpMiniTable(res.dpTable, latestResults.items, cap);
      } else {
        dpWrapper.classList.add('hidden');
      }
    }

    function renderDpMiniTable(dp, items, capacity) {
      const container = document.getElementById('dpTableScrollArea');
      if (capacity > 35) {
        container.innerHTML = `<p class="text-xs text-slate-400 py-2">Capacity W = ${capacity} is large; full 2D grid preview is condensed for readability. Optimal value at dp[${items.length}][${capacity}] = <strong class="text-emerald-400">${dp[items.length][capacity]}</strong>.</p>`;
        return;
      }

      let html = '<table class="w-full text-center border-collapse">';
      html += '<thead><tr class="text-slate-400 border-b border-slate-700"><th class="py-1 px-2 text-left">Item \\ Cap</th>';
      for (let w = 0; w <= capacity; w++) {
        html += `<th class="py-1 px-1.5">${w}</th>`;
      }
      html += '</tr></thead><tbody>';

      for (let i = 0; i <= items.length; i++) {
        const label = i === 0 ? '0 (Base)' : `${items[i - 1].name.slice(0, 10)} (${items[i - 1].weight}w)`;
        html += `<tr class="border-b border-slate-800/80"><td class="py-1 px-2 text-left text-slate-300 whitespace-nowrap">${escapeHtml(label)}</td>`;
        for (let w = 0; w <= capacity; w++) {
          const isFinal = i === items.length && w === capacity;
          const cellClass = isFinal
            ? 'bg-emerald-500/20 text-emerald-300 font-bold ring-1 ring-emerald-400 rounded'
            : 'text-slate-300';
          html += `<td class="py-1 px-1.5 ${cellClass}">${dp[i][w]}</td>`;
        }
        html += '</tr>';
      }
      html += '</tbody></table>';
      container.innerHTML = html;
    }

    function renderComparisonTable() {
      if (!latestResults) return;
      const tbody = document.getElementById('comparisonTableBody');
      const keys = ['bruteforce', 'greedy', 'backtracking', 'dp'];

      tbody.innerHTML = keys.map(key => {
        const meta = ALGORITHM_METADATA[key];
        const res = latestResults.algorithms[key];
        const isSelected = key === activeTab;

        return `
          <tr onclick="switchTab('${key}')" class="cursor-pointer transition ${isSelected ? 'bg-indigo-50/70' : 'hover:bg-slate-50'}">
            <td class="py-3 px-3 font-semibold text-slate-900 whitespace-nowrap">${meta.title.split(' (')[0]}</td>
            <td class="py-3 px-3 font-mono text-xs text-slate-700 whitespace-nowrap">${meta.timeComplexity}</td>
            <td class="py-3 px-3 font-mono text-xs text-slate-700 whitespace-nowrap">${meta.spaceComplexity}</td>
            <td class="py-3 px-3 font-mono font-bold text-indigo-700">${res.totalValue}</td>
            <td class="py-3 px-3 font-mono text-xs text-slate-600">${res.totalWeight}/${latestResults.capacity}</td>
            <td class="py-3 px-3 font-mono text-xs text-slate-600">${res.execTimeMs.toFixed(3)} ms</td>
            <td class="py-3 px-3 whitespace-nowrap">
              ${res.isOptimal
                ? '<span class="inline-flex items-center px-2 py-0.5 rounded-full text-[11px] font-semibold bg-emerald-100 text-emerald-800">Optimal</span>'
                : '<span class="inline-flex items-center px-2 py-0.5 rounded-full text-[11px] font-semibold bg-amber-100 text-amber-800">Suboptimal</span>'
              }
            </td>
          </tr>
        `;
      }).join('');
    }

    // =========================================================================
    // 6. UTILITIES (COPY HTML FOR GITHUB & TOASTS)
    // =========================================================================
    function setupCopySourceButton() {
      const btn = document.getElementById('copySourceBtn');
      btn.addEventListener('click', () => {
        try {
          const fullHtml = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
          const textarea = document.createElement('textarea');
          textarea.value = fullHtml;
          textarea.style.position = 'fixed';
          textarea.style.opacity = '0';
          document.body.appendChild(textarea);
          textarea.select();
          document.execCommand('copy');
          document.body.removeChild(textarea);
          showToast('Complete HTML copied! Paste into index.html and push to GitHub.');
        } catch (err) {
          showToast('Could not copy automatically. Use Ctrl+S / Cmd+S to save this page.');
        }
      });
    }

    let toastTimeout = null;
    function showToast(message) {
      const banner = document.getElementById('toastBanner');
      const msgEl = document.getElementById('toastMessage');
      msgEl.textContent = message;
      banner.classList.remove('hidden');
      clearTimeout(toastTimeout);
      toastTimeout = setTimeout(() => {
        banner.classList.add('hidden');
      }, 3500);
    }

    function escapeHtml(str) {
      return String(str)
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
    }
  </script>
</body>
</html>
