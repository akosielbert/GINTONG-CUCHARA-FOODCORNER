```
<!-- Top Header -->
<header class="bg-slate-900 text-white shadow-md sticky top-0 z-30">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
            <!-- Brand Title -->
            <div class="flex items-center gap-3">
                <div class="bg-brand-500 text-white p-2.5 rounded-xl shadow-lg shadow-brand-500/30 flex items-center justify-center">
                    <i class="fa-solid font-bold fa-utensils text-xl"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-lg sm:text-xl tracking-tight text-white flex items-center gap-2">
                        <span>Kusina POS</span>
                        <span class="bg-brand-500/20 text-brand-500 text-xs px-2 py-0.5 rounded-full font-semibold border border-brand-500/30">Carinderia Edition</span>
                    </h1>
                    <p class="text-xs text-slate-400 hidden sm:block" id="current-date-time">Loading date...</p>
                </div>
            </div>

            <!-- Live Quick Stats -->
            <div class="hidden lg:flex items-center gap-6 text-sm">
                <div class="bg-slate-800/80 px-3.5 py-1.5 rounded-lg border border-slate-700 flex items-center gap-2.5">
                    <i class="fa-solid fa-receipt text-emerald-400"></i>
                    <div>
                        <span class="text-slate-400 text-xs block leading-tight">Today's Orders</span>
                        <span class="font-bold text-white text-base" id="header-total-orders">0</span>
                    </div>
                </div>
                <div class="bg-slate-800/80 px-3.5 py-1.5 rounded-lg border border-slate-700 flex items-center gap-2.5">
                    <i class="fa-solid fa-coins text-amber-400"></i>
                    <div>
                        <span class="text-slate-400 text-xs block leading-tight">Today's Revenue</span>
                        <span class="font-bold text-emerald-400 text-base">₱<span id="header-total-sales">0.00</span></span>
                    </div>
                </div>
            </div>

            <!-- Navigation Tabs -->
            <nav class="flex space-x-1 sm:space-x-2 bg-slate-800/70 p-1 rounded-xl border border-slate-700/60">
                <button id="nav-pos" onclick="switchTab('pos')" class="px-3 sm:px-4 py-2 rounded-lg font-semibold text-xs sm:text-sm transition-all duration-150 flex items-center gap-2 bg-brand-500 text-white shadow">
                    <i class="fa-solid fa-cash-register"></i>
                    <span>POS Register</span>
                </button>
                <button id="nav-menu" onclick="switchTab('menu')" class="px-3 sm:px-4 py-2 rounded-lg font-semibold text-xs sm:text-sm text-slate-300 hover:text-white hover:bg-slate-700/50 transition-all duration-150 flex items-center gap-2">
                    <i class="fa-solid fa-utensils"></i>
                    <span>Manage Menu</span>
                </button>
                <button id="nav-reports" onclick="switchTab('reports')" class="px-3 sm:px-4 py-2 rounded-lg font-semibold text-xs sm:text-sm text-slate-300 hover:text-white hover:bg-slate-700/50 transition-all duration-150 flex items-center gap-2">
                    <i class="fa-solid fa-chart-pie"></i>
                    <span>Sales & Inventory</span>
                </button>
            </nav>
        </div>
    </div>
</header>

<!-- Main Content Container -->
<main class="flex-grow max-w-7xl w-full mx-auto p-3 sm:p-6">

    <!-- SECTION 1: POS CASHIER TAB -->
    <div id="tab-pos" class="tab-content grid grid-cols-1 lg:grid-cols-12 gap-6">
        
        <!-- Left Side: Menu Grid & Category Filters -->
        <div class="lg:col-span-7 xl:col-span-8 flex flex-col gap-4">
            
            <!-- Search & Category Filters -->
            <div class="bg-white p-3.5 rounded-2xl shadow-sm border border-slate-200 flex flex-col sm:flex-row gap-3 items-center justify-between">
                <!-- Category Pills -->
                <div class="flex items-center gap-1.5 overflow-x-auto w-full sm:w-auto pb-1 sm:pb-0 scrollbar-none" id="category-filter-container">
                    <button onclick="filterCategory('All')" class="category-btn active px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-brand-500 text-white shadow-sm">All Items</button>
                    <button onclick="filterCategory('Ulam')" class="category-btn px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-slate-100 text-slate-600 hover:bg-slate-200">🍲 Ulam</button>
                    <button onclick="filterCategory('Sabaw')" class="category-btn px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-slate-100 text-slate-600 hover:bg-slate-200">🥣 Sabaw</button>
                    <button onclick="filterCategory('Extra')" class="category-btn px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-slate-100 text-slate-600 hover:bg-slate-200">🍚 Extras / Kanin</button>
                    <button onclick="filterCategory('Drinks')" class="category-btn px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-slate-100 text-slate-600 hover:bg-slate-200">🥤 Drinks</button>
                </div>

                <!-- Search Input -->
                <div class="relative w-full sm:w-48 flex-shrink-0">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                    <input type="text" id="pos-search-input" onkeyup="searchMenuItems()" placeholder="Search food..." class="w-full pl-8 pr-3 py-1.5 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-brand-500 focus:bg-white transition-all">
                </div>
            </div>

            <!-- Food Grid -->
            <div id="pos-food-grid" class="grid grid-cols-2 sm:grid-cols-3 xl:grid-cols-4 gap-3.5 overflow-y-auto max-h-[calc(100vh-210px)] pr-1">
                <!-- Dynamic Food Cards populated by JS -->
            </div>
        </div>

        <!-- Right Side: Order Cart Panel -->
        <div class="lg:col-span-5 xl:col-span-4 flex flex-col h-[calc(100vh-140px)] sticky top-20">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 flex flex-col h-full overflow-hidden">
                
                <!-- Cart Header -->
                <div class="p-4 bg-slate-50 border-b border-slate-200 flex items-center justify-between">
                    <div class="flex items-center gap-2">
                        <i class="fa-solid fa-cart-shopping text-brand-500"></i>
                        <h2 class="font-bold text-slate-800">Current Order</h2>
                        <span id="cart-item-count" class="bg-brand-100 text-brand-700 font-bold text-xs px-2 py-0.5 rounded-full">0 items</span>
                    </div>
                    <button onclick="clearCart()" class="text-xs text-rose-500 hover:text-rose-700 font-semibold hover:bg-rose-50 px-2 py-1 rounded-lg transition-colors">
                        <i class="fa-solid fa-trash-can mr-1"></i> Clear
                    </button>
                </div>

                <!-- Cart Item List -->
                <div id="cart-items-container" class="flex-grow overflow-y-auto p-4 divide-y divide-slate-100">
                    <!-- Dynamic Cart items -->
                </div>

                <!-- Cart Footer / Checkout Summary -->
                <div class="p-4 bg-slate-50 border-t border-slate-200 flex flex-col gap-3">
                    <div class="space-y-1.5 text-sm">
                        <div class="flex justify-between text-slate-500">
                            <span>Subtotal</span>
                            <span class="font-medium text-slate-700">₱<span id="cart-subtotal">0.00</span></span>
                        </div>
                        <div class="flex justify-between text-slate-500 text-xs">
                            <span>Tax / Service (0%)</span>
                            <span>₱0.00</span>
                        </div>
                        <div class="flex justify-between items-center pt-2 border-t border-slate-200 text-base font-extrabold text-slate-900">
                            <span>Grand Total</span>
                            <span class="text-brand-600 text-xl">₱<span id="cart-total">0.00</span></span>
                        </div>
                    </div>

                    <!-- Tender Cash Input -->
                    <div class="pt-2">
                        <label class="block text-xs font-semibold text-slate-600 mb-1">Cash Received (₱):</label>
                        <div class="relative">
                            <span class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 font-bold">₱</span>
                            <input type="number" id="cash-tendered" placeholder="Enter amount..." oninput="calculateChange()" class="w-full pl-8 pr-3 py-2 text-base font-bold bg-white border border-slate-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-brand-500">
                        </div>
                        <!-- Quick Cash Buttons -->
                        <div class="grid grid-cols-4 gap-1.5 mt-2">
                            <button onclick="quickCash(50)" class="py-1 bg-white border border-slate-200 hover:bg-slate-100 rounded-lg text-xs font-semibold text-slate-700 transition">₱50</button>
                            <button onclick="quickCash(100)" class="py-1 bg-white border border-slate-200 hover:bg-slate-100 rounded-lg text-xs font-semibold text-slate-700 transition">₱100</button>
                            <button onclick="quickCash(200)" class="py-1 bg-white border border-slate-200 hover:bg-slate-100 rounded-lg text-xs font-semibold text-slate-700 transition">₱200</button>
                            <button onclick="quickCash(500)" class="py-1 bg-white border border-slate-200 hover:bg-slate-100 rounded-lg text-xs font-semibold text-slate-700 transition">₱500</button>
                        </div>
                    </div>

                    <!-- Change Display -->
                    <div class="flex justify-between items-center px-3 py-2 bg-slate-200/60 rounded-xl text-sm font-bold">
                        <span class="text-slate-600">Change Due:</span>
                        <span class="text-emerald-700 text-lg">₱<span id="cart-change">0.00</span></span>
                    </div>

                    <!-- Checkout Button -->
                    <button id="checkout-btn" onclick="processCheckout()" disabled class="w-full py-3 bg-slate-300 text-slate-500 font-bold rounded-xl shadow transition-all duration-200 flex items-center justify-center gap-2 cursor-not-allowed">
                        <i class="fa-solid fa-circle-check"></i>
                        <span>Complete Sale & Print Receipt</span>
                    </button>
                </div>

            </div>
        </div>

    </div>

    <!-- SECTION 2: MENU MANAGEMENT TAB -->
    <div id="tab-menu" class="tab-content hidden flex-col gap-6">
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
            <div>
                <h2 class="text-xl font-bold text-slate-900">Customizable Food Menu</h2>
                <p class="text-xs text-slate-500">Add, edit, or remove menu items, adjust prices, and update pictures for your carinderia.</p>
            </div>
            <button onclick="openMenuModal()" class="px-4 py-2.5 bg-brand-500 hover:bg-brand-600 text-white font-bold text-sm rounded-xl shadow-md transition flex items-center gap-2">
                <i class="fa-solid fa-plus"></i>
                <span>Add New Meal / Item</span>
            </button>
        </div>

        <!-- Menu Table / Cards -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-slate-50 text-slate-500 uppercase text-[11px] font-bold tracking-wider border-b border-slate-200">
                            <th class="py-3.5 px-4">Item Details</th>
                            <th class="py-3.5 px-4">Category</th>
                            <th class="py-3.5 px-4">Price</th>
                            <th class="py-3.5 px-4 text-right">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="menu-table-body" class="divide-y divide-slate-100 text-sm">
                        <!-- Dynamic menu rows dynamically generated -->
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- SECTION 3: SALES & INVENTORY REPORT TAB -->
    <div id="tab-reports" class="tab-content hidden flex-col gap-6">
        
        <!-- Header Summary Bar -->
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
            <div>
                <h2 class="text-xl font-bold text-slate-900">Daily Inventory & Sales Summary</h2>
                <p class="text-xs text-slate-500">Real-time stats of food units sold and gross income per dish today.</p>
            </div>
            <div class="flex items-center gap-2">
                <button onclick="exportSalesSummary()" class="px-3.5 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold text-xs rounded-xl border border-slate-300 transition flex items-center gap-2">
                    <i class="fa-solid fa-download"></i>
                    <span>Export CSV</span>
                </button>
                <button onclick="resetDailyData()" class="px-3.5 py-2 bg-rose-50 hover:bg-rose-100 text-rose-600 font-bold text-xs rounded-xl border border-rose-200 transition flex items-center gap-2">
                    <i class="fa-solid fa-arrows-rotate"></i>
                    <span>Reset Today's Sales</span>
                </button>
            </div>
        </div>

        <!-- Summary Key Metrics Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center gap-4">
                <div class="p-3.5 bg-emerald-100 text-emerald-600 rounded-2xl">
                    <i class="fa-solid fa-sack-dollar text-2xl"></i>
                </div>
                <div>
                    <span class="text-xs font-semibold text-slate-500 uppercase">Total Sales Today</span>
                    <h3 class="text-2xl font-extrabold text-emerald-600">₱<span id="report-total-revenue">0.00</span></h3>
                </div>
            </div>

            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center gap-4">
                <div class="p-3.5 bg-brand-100 text-brand-600 rounded-2xl">
                    <i class="fa-solid fa-bowl-rice text-2xl"></i>
                </div>
                <div>
                    <span class="text-xs font-semibold text-slate-500 uppercase">Total Dishes / Units Sold</span>
                    <h3 class="text-2xl font-extrabold text-slate-800"><span id="report-total-units">0</span> <span class="text-sm font-normal text-slate-500">orders</span></h3>
                </div>
            </div>

            <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex items-center gap-4">
                <div class="p-3.5 bg-amber-100 text-amber-600 rounded-2xl">
                    <i class="fa-solid fa-trophy text-2xl"></i>
                </div>
                <div>
                    <span class="text-xs font-semibold text-slate-500 uppercase">Top Seller Dish</span>
                    <h3 class="text-lg font-bold text-slate-800 truncate" id="report-top-seller">--</h3>
                </div>
            </div>
        </div>

        <!-- Clean Per-Item Sales Inventory Breakdown Table -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="p-4 border-b border-slate-200 bg-slate-50/50 flex justify-between items-center">
                <h3 class="font-bold text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-list-check text-brand-500"></i>
                    <span>Itemized Inventory & Revenue Breakdown</span>
                </h3>
                <span class="text-xs text-slate-500">Shows total quantity sold & total revenue per meal</span>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-slate-100/70 text-slate-600 uppercase text-[11px] font-bold tracking-wider border-b border-slate-200">
                            <th class="py-3 px-4">Menu Item</th>
                            <th class="py-3 px-4">Category</th>
                            <th class="py-3 px-4">Unit Price</th>
                            <th class="py-3 px-4 text-center">Total Orders Sold</th>
                            <th class="py-3 px-4 text-right">Total Revenue (₱)</th>
                        </tr>
                    </thead>
                    <tbody id="inventory-breakdown-body" class="divide-y divide-slate-100 text-sm">
                        <!-- Dynamic row insertion for inventory -->
                    </tbody>
                    <tfoot>
                        <tr class="bg-slate-50 font-extrabold text-slate-900 border-t-2 border-slate-200">
                            <td colspan="3" class="py-3.5 px-4 text-right uppercase text-xs">Total Overall Sales Today:</td>
                            <td class="py-3.5 px-4 text-center text-brand-600" id="foot-total-orders">0 orders</td>
                            <td class="py-3.5 px-4 text-right text-emerald-600 text-base" id="foot-total-revenue">₱0.00</td>
                        </tr>
                    </tfoot>
                </table>
            </div>
        </div>

        <!-- Transaction History Log -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
            <div class="p-4 border-b border-slate-200 bg-slate-50/50">
                <h3 class="font-bold text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-clock-rotate-left text-slate-500"></i>
                    <span>Today's Transactions Log</span>
                </h3>
            </div>
            <div class="overflow-x-auto max-h-96">
                <table class="w-full text-left border-collapse text-xs">
                    <thead class="sticky top-0 bg-slate-100">
                        <tr class="text-slate-600 uppercase font-bold border-b border-slate-200">
                            <th class="py-3 px-4">Order ID</th>
                            <th class="py-3 px-4">Time</th>
                            <th class="py-3 px-4">Items Summary</th>
                            <th class="py-3 px-4 text-right">Total</th>
                            <th class="py-3 px-4 text-right">Cash / Change</th>
                        </tr>
                    </thead>
                    <tbody id="transactions-log-body" class="divide-y divide-slate-100">
                        <!-- Dynamic transactions content -->
                    </tbody>
                </table>
            </div>
        </div>

    </div>

</main>

<!-- MODAL 1: ADD / EDIT MENU ITEM -->
<div id="menu-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full overflow-hidden border border-slate-100 transform transition-all">
        <div class="bg-slate-900 text-white p-4 flex justify-between items-center">
            <h3 class="font-bold text-lg" id="modal-title">Add New Dish</h3>
            <button onclick="closeMenuModal()" class="text-slate-400 hover:text-white transition"><i class="fa-solid fa-xmark text-lg"></i></button>
        </div>
        <form id="menu-form" onsubmit="saveMenuItem(event)" class="p-5 space-y-4">
            <input type="hidden" id="edit-item-id">
            
            <div>
                <label class="block text-xs font-bold text-slate-700 mb-1">Dish / Item Name *</label>
                <input type="text" id="item-name" required placeholder="e.g. Pork Adobo, Giniling, Extra Rice" class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-300 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none">
            </div>

            <div class="grid grid-cols-2 gap-3">
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Price (₱) *</label>
                    <input type="number" step="0.5" id="item-price" required placeholder="60.00" class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-300 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Category *</label>
                    <select id="item-category" class="w-full px-3 py-2 text-sm bg-slate-50 border border-slate-300 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none">
                        <option value="Ulam">Ulam</option>
                        <option value="Sabaw">Sabaw</option>
                        <option value="Extra">Extra / Rice</option>
                        <option value="Drinks">Drinks</option>
                    </select>
                </div>
            </div>

            <div>
                <label class="block text-xs font-bold text-slate-700 mb-1">Image Source</label>
                <div class="space-y-2">
                    <input type="url" id="item-image-url" placeholder="Paste Image URL (https://...)" class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-300 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none">
                    <div class="text-center text-xs text-slate-400 font-semibold">- OR -</div>
                    <input type="file" id="item-image-file" accept="image/*" onchange="handleImageUpload(event)" class="w-full text-xs text-slate-500 file:mr-3 file:py-1.5 file:px-3 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-brand-50 file:text-brand-700 hover:file:bg-brand-100">
                </div>
            </div>

            <div id="image-preview-container" class="hidden">
                <span class="block text-xs font-bold text-slate-700 mb-1">Image Preview:</span>
                <img id="image-preview" src="" alt="Preview" class="w-full h-32 object-cover rounded-xl border border-slate-200">
            </div>

            <div class="pt-3 flex justify-end gap-2">
                <button type="button" onclick="closeMenuModal()" class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-bold rounded-xl transition">Cancel</button>
                <button type="submit" class="px-4 py-2 bg-brand-500 hover:bg-brand-600 text-white text-xs font-bold rounded-xl shadow transition">Save Menu Item</button>
            </div>
        </form>
    </div>
</div>

<!-- MODAL 2: RECEIPT MODAL -->
<div id="receipt-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-2xl shadow-2xl max-w-sm w-full overflow-hidden border border-slate-100">
        
        <!-- Receipt Printable Content -->
        <div id="printable-receipt" class="p-6 bg-white text-slate-800 font-mono text-xs">
            <div class="text-center mb-4 pb-3 border-b border-dashed border-slate-300">
                <h2 class="text-base font-extrabold uppercase tracking-widest text-slate-900">KUSINA CARINDERIA</h2>
                <p class="text-[10px] text-slate-500">Delicious Homecooked Filipino Meals</p>
                <p class="text-[10px] text-slate-500" id="receipt-timestamp">2026-10-08 12:00 PM</p>
                <p class="text-[10px] font-bold text-slate-700 mt-1">Receipt #: <span id="receipt-id">ORD-0000</span></p>
            </div>

            <!-- Receipt Items List -->
            <div class="space-y-1.5 mb-4 border-b border-dashed border-slate-300 pb-3" id="receipt-items-list">
                <!-- Dynamic Receipt Line Items -->
            </div>

            <!-- Total Breakdown -->
            <div class="space-y-1 text-xs">
                <div class="flex justify-between font-bold text-sm text-slate-900">
                    <span>TOTAL:</span>
                    <span>₱<span id="receipt-total">0.00</span></span>
                </div>
                <div class="flex justify-between text-slate-600">
                    <span>CASH TENDERED:</span>
                    <span>₱<span id="receipt-cash">0.00</span></span>
                </div>
                <div class="flex justify-between text-slate-600 font-bold">
                    <span>CHANGE:</span>
                    <span>₱<span id="receipt-change">0.00</span></span>
                </div>
            </div>

            <div class="text-center mt-6 pt-3 border-t border-dashed border-slate-300 text-[10px] text-slate-500">
                <p class="font-bold text-slate-700">Salamat sa Pagtangkilik!</p>
                <p>Please Come Again!</p>
            </div>
        </div>

        <!-- Modal Action Footer -->
        <div class="p-4 bg-slate-50 border-t border-slate-200 flex gap-2">
            <button onclick="printReceipt()" class="flex-1 py-2.5 bg-slate-800 hover:bg-slate-900 text-white font-bold text-xs rounded-xl transition flex items-center justify-center gap-2">
                <i class="fa-solid fa-print"></i> Print
            </button>
            <button onclick="closeReceiptModal()" class="flex-1 py-2.5 bg-brand-500 hover:bg-brand-600 text-white font-bold text-xs rounded-xl transition">
                Done / Next Sale
            </button>
        </div>

    </div>
</div>

<script>
    const DEFAULT_MENU = [
        { id: '1', name: 'Pork Adobo', price: 60, category: 'Ulam', image: 'https://images.unsplash.com/photo-1541832676-9b763b0239ab?auto=format&fit=crop&w=400&q=80' },
        { id: '2', name: 'Giniling na Baboy', price: 50, category: 'Ulam', image: 'https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=400&q=80' },
        { id: '3', name: 'Sinigang na Baboy', price: 70, category: 'Sabaw', image: 'https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&w=400&q=80' },
        { id: '4', name: 'Beef Menudo', price: 65, category: 'Ulam', image: 'https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?auto=format&fit=crop&w=400&q=80' },
        { id: '5', name: 'Extra Rice', price: 12, category: 'Extra', image: 'https://images.unsplash.com/photo-1516684732162-798a0062be99?auto=format&fit=crop&w=400&q=80' },
        { id: '6', name: 'Coke / Softdrinks 290ml', price: 20, category: 'Drinks', image: 'https://images.unsplash.com/photo-1622483767028-3f66f32aef97?auto=format&fit=crop&w=400&q=80' },
        { id: '7', name: 'Pritong Tilapia', price: 55, category: 'Ulam', image: 'https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?auto=format&fit=crop&w=400&q=80' },
        { id: '8', name: 'Cold Iced Tea', price: 15, category: 'Drinks', image: 'https://images.unsplash.com/photo-1556679343-c7306c1976bc?auto=format&fit=crop&w=400&q=80' }
    ];

    let menuItems = [];
    let cart = [];
    let salesLog = [];
    let activeCategory = 'All';

    const PLACEHOLDER_IMG = 'https://placehold.co/400x300/f97316/ffffff?text=Carinderia+Meal';

    window.onload = function() {
        loadLocalStorageData();
        updateLiveClock();
        setInterval(updateLiveClock, 1000);
        renderMenuGrid();
        renderCart();
        renderMenuManagementTable();
        renderReportsData();
    };

    function updateLiveClock() {
        const now = new Date();
        const options = { weekday: 'short', year: 'numeric', month: 'short', day: 'numeric', hour: '2-digit', minute: '2-digit', second: '2-digit' };
        document.getElementById('current-date-time').innerText = now.toLocaleDateString('en-US', options);
    }

    function loadLocalStorageData() {
        const savedMenu = localStorage.getItem('carinderia_pos_menu');
        menuItems = savedMenu ? JSON.parse(savedMenu) : DEFAULT_MENU;

        const savedSales = localStorage.getItem('carinderia_pos_sales');
        salesLog = savedSales ? JSON.parse(savedSales) : [];
    }

    function saveMenuToStorage() {
        localStorage.setItem('carinderia_pos_menu', JSON.stringify(menuItems));
    }

    function saveSalesToStorage() {
        localStorage.setItem('carinderia_pos_sales', JSON.stringify(salesLog));
    }

    function switchTab(tab) {
        document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
        
        ['pos', 'menu', 'reports'].forEach(t => {
            const btn = document.getElementById(`nav-${t}`);
            if (btn) {
                btn.className = "px-3 sm:px-4 py-2 rounded-lg font-semibold text-xs sm:text-sm text-slate-300 hover:text-white hover:bg-slate-700/50 transition-all duration-150 flex items-center gap-2";
            }
        });

        document.getElementById(`tab-${tab}`).classList.remove('hidden');
        if (tab === 'pos') document.getElementById(`tab-${tab}`).classList.add('grid');
        else document.getElementById(`tab-${tab}`).classList.add('flex');

        const activeBtn = document.getElementById(`nav-${tab}`);
        if (activeBtn) {
            activeBtn.className = "px-3 sm:px-4 py-2 rounded-lg font-semibold text-xs sm:text-sm transition-all duration-150 flex items-center gap-2 bg-brand-500 text-white shadow";
        }

        if (tab === 'reports') {
            renderReportsData();
        }
    }

    function filterCategory(cat) {
        activeCategory = cat;
        document.querySelectorAll('.category-btn').forEach(btn => {
            btn.className = "category-btn px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-slate-100 text-slate-600 hover:bg-slate-200";
        });
        event.target.className = "category-btn active px-3.5 py-1.5 rounded-xl text-xs font-bold whitespace-nowrap transition-all bg-brand-500 text-white shadow-sm";
        renderMenuGrid();
    }

    function searchMenuItems() {
        renderMenuGrid();
    }

    function renderMenuGrid() {
        const grid = document.getElementById('pos-food-grid');
        const searchVal = document.getElementById('pos-search-input').value.toLowerCase().trim();
        grid.innerHTML = '';

        const filtered = menuItems.filter(item => {
            const matchesCat = (activeCategory === 'All') || (item.category === activeCategory);
            const matchesSearch = item.name.toLowerCase().includes(searchVal);
            return matchesCat && matchesSearch;
        });

        if (filtered.length === 0) {
            grid.innerHTML = `
                <div class="col-span-full py-12 text-center text-slate-400">
                    <i class="fa-solid fa-utensils text-4xl mb-2 text-slate-300"></i>
                    <p class="text-sm font-semibold">No food items found</p>
                </div>
            `;
            return;
        }

        filtered.forEach(item => {
            const card = document.createElement('div');
            card.className = "bg-white rounded-2xl overflow-hidden border border-slate-200/80 hover:shadow-md transition duration-200 flex flex-col group cursor-pointer select-none";
            card.onclick = () => addToCart(item.id);

            card.innerHTML = `
                <div class="relative h-28 sm:h-32 w-full bg-slate-100 overflow-hidden">
                    <img src="${item.image || PLACEHOLDER_IMG}" onerror="this.src='${PLACEHOLDER_IMG}'" class="w-full h-full object-cover group-hover:scale-105 transition duration-300" alt="${item.name}">
                    <span class="absolute top-2 right-2 bg-slate-900/80 text-white text-[10px] font-bold px-2 py-0.5 rounded-full backdrop-blur-sm">
                        ${item.category}
                    </span>
                </div>
                <div class="p-3 flex flex-col flex-grow justify-between">
                    <div>
                        <h3 class="font-bold text-slate-800 text-sm line-clamp-1 group-hover:text-brand-600 transition">${item.name}</h3>
                        <p class="font-extrabold text-brand-600 text-base mt-0.5">₱${item.price.toFixed(2)}</p>
                    </div>
                    <button class="mt-2 w-full py-1.5 bg-slate-100 group-hover:bg-brand-500 group-hover:text-white text-slate-700 font-bold text-xs rounded-xl transition flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-plus text-[10px]"></i>
                        <span>Add Order</span>
                    </button>
                </div>
            `;
            grid.appendChild(card);
        });
    }

    function addToCart(itemId) {
        const item = menuItems.find(m => m.id === itemId);
        if (!item) return;

        const existing = cart.find(c => c.id === itemId);
        if (existing) {
            existing.qty += 1;
        } else {
            cart.push({ ...item, qty: 1 });
        }
        renderCart();
    }

    function updateCartQty(itemId, delta) {
        const existing = cart.find(c => c.id === itemId);
        if (!existing) return;

        existing.qty += delta;
        if (existing.qty <= 0) {
            cart = cart.filter(c => c.id !== itemId);
        }
        renderCart();
    }

    function clearCart() {
        cart = [];
        document.getElementById('cash-tendered').value = '';
        renderCart();
    }

    function renderCart() {
        const container = document.getElementById('cart-items-container');
        container.innerHTML = '';

        let subtotal = 0;
        let totalItemCount = 0;

        if (cart.length === 0) {
            container.innerHTML = `
                <div class="h-full flex flex-col items-center justify-center text-slate-400 py-12 text-center">
                    <i class="fa-solid fa-basket-shopping text-4xl mb-2 text-slate-300"></i>
                    <p class="text-xs font-semibold">No items in customer cart</p>
                    <p class="text-[11px] text-slate-400">Click any dish from the left to add</p>
                </div>
            `;
        } else {
            cart.forEach(item => {
                const itemTotal = item.price * item.qty;
                subtotal += itemTotal;
                totalItemCount += item.qty;

                const row = document.createElement('div');
                row.className = "py-2.5 flex items-center justify-between gap-2";
                row.innerHTML = `
                    <div class="flex-grow min-w-0">
                        <h4 class="font-bold text-slate-800 text-xs truncate">${item.name}</h4>
                        <p class="text-[11px] text-slate-500">₱${item.price.toFixed(2)} × ${item.qty} = <span class="font-semibold text-slate-700">₱${itemTotal.toFixed(2)}</span></p>
                    </div>
                    <div class="flex items-center gap-1 bg-slate-100 p-1 rounded-lg">
                        <button onclick="updateCartQty('${item.id}', -1)" class="w-6 h-6 bg-white hover:bg-slate-200 text-slate-700 rounded-md font-bold text-xs flex items-center justify-center shadow-sm">-</button>
                        <span class="w-6 text-center text-xs font-bold text-slate-800">${item.qty}</span>
                        <button onclick="updateCartQty('${item.id}', 1)" class="w-6 h-6 bg-white hover:bg-slate-200 text-slate-700 rounded-md font-bold text-xs flex items-center justify-center shadow-sm">+</button>
                    </div>
                `;
                container.appendChild(row);
            });
        }

        document.getElementById('cart-item-count').innerText = `${totalItemCount} items`;
        document.getElementById('cart-subtotal').innerText = subtotal.toFixed(2);
        document.getElementById('cart-total').innerText = subtotal.toFixed(2);

        calculateChange();
    }

    function quickCash(amount) {
        document.getElementById('cash-tendered').value = amount;
        calculateChange();
    }

    function calculateChange() {
        const total = parseFloat(document.getElementById('cart-total').innerText) || 0;
        const cash = parseFloat(document.getElementById('cash-tendered').value) || 0;
        const change = cash - total;

        const changeEl = document.getElementById('cart-change');
        const checkoutBtn = document.getElementById('checkout-btn');

        if (change >= 0) {
            changeEl.innerText = change.toFixed(2);
            changeEl.className = "text-emerald-700 text-lg font-bold";
        } else {
            changeEl.innerText = "0.00";
            changeEl.className = "text-rose-500 text-lg font-bold";
        }

        if (total > 0 && cash >= total) {
            checkoutBtn.disabled = false;
            checkoutBtn.className = "w-full py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl shadow-lg shadow-emerald-600/20 transition-all duration-200 flex items-center justify-center gap-2 cursor-pointer";
        } else {
            checkoutBtn.disabled = true;
            checkoutBtn.className = "w-full py-3 bg-slate-300 text-slate-500 font-bold rounded-xl shadow transition-all duration-200 flex items-center justify-center gap-2 cursor-not-allowed";
        }
    }

    function processCheckout() {
        const total = parseFloat(document.getElementById('cart-total').innerText);
        const cash = parseFloat(document.getElementById('cash-tendered').value);
        const change = cash - total;

        if (cart.length === 0 || cash < total) return;

        const orderId = 'ORD-' + Math.floor(1000 + Math.random() * 9000);
        const now = new Date();
        const timestamp = now.toLocaleDateString() + ' ' + now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

        const transaction = {
            id: orderId,
            timestamp: timestamp,
            items: [...cart],
            totalAmount: total,
            cashTendered: cash,
            change: change
        };

        salesLog.unshift(transaction);
        saveSalesToStorage();

        document.getElementById('receipt-id').innerText = orderId;
        document.getElementById('receipt-timestamp').innerText = timestamp;
        document.getElementById('receipt-total').innerText = total.toFixed(2);
        document.getElementById('receipt-cash').innerText = cash.toFixed(2);
        document.getElementById('receipt-change').innerText = change.toFixed(2);

        const receiptList = document.getElementById('receipt-items-list');
        receiptList.innerHTML = '';
        cart.forEach(i => {
            const line = document.createElement('div');
            line.className = "flex justify-between";
            line.innerHTML = `
                <span>${i.qty}x ${i.name}</span>
                <span>₱${(i.price * i.qty).toFixed(2)}</span>
            `;
            receiptList.appendChild(line);
        });

        document.getElementById('receipt-modal').classList.remove('hidden');

        clearCart();
        renderHeaderSummary();
    }

    function closeReceiptModal() {
        document.getElementById('receipt-modal').classList.add('hidden');
    }

    function printReceipt() {
        window.print();
    }

    function renderMenuManagementTable() {
        const tbody = document.getElementById('menu-table-body');
        tbody.innerHTML = '';

        menuItems.forEach(item => {
            const tr = document.createElement('tr');
            tr.className = "hover:bg-slate-50/80 transition";
            tr.innerHTML = `
                <td class="py-3 px-4 flex items-center gap-3">
                    <img src="${item.image || PLACEHOLDER_IMG}" onerror="this.src='${PLACEHOLDER_IMG}'" class="w-10 h-10 object-cover rounded-lg border border-slate-200">
                    <span class="font-bold text-slate-800 text-sm">${item.name}</span>
                </td>
                <td class="py-3 px-4">
                    <span class="bg-slate-100 text-slate-700 text-xs font-semibold px-2.5 py-1 rounded-full border border-slate-200">${item.category}</span>
                </td>
                <td class="py-3 px-4 font-bold text-brand-600">₱${item.price.toFixed(2)}</td>
                <td class="py-3 px-4 text-right space-x-2">
                    <button onclick="editMenuItem('${item.id}')" class="px-2.5 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold text-xs rounded-lg transition">
                        <i class="fa-solid fa-pen-to-square"></i> Edit
                    </button>
                    <button onclick="deleteMenuItem('${item.id}')" class="px-2.5 py-1.5 bg-rose-50 hover:bg-rose-100 text-rose-600 font-semibold text-xs rounded-lg transition">
                        <i class="fa-solid fa-trash"></i> Delete
                    </button>
                </td>
            `;
            tbody.appendChild(tr);
        });
    }

    function openMenuModal(editId = null) {
        const modal = document.getElementById('menu-modal');
        const form = document.getElementById('menu-form');
        form.reset();
        document.getElementById('image-preview-container').classList.add('hidden');

        if (editId) {
            const item = menuItems.find(m => m.id === editId);
            if (item) {
                document.getElementById('modal-title').innerText = "Edit Menu Item";
                document.getElementById('edit-item-id').value = item.id;
                document.getElementById('item-name').value = item.name;
                document.getElementById('item-price').value = item.price;
                document.getElementById('item-category').value = item.category;
                document.getElementById('item-image-url').value = item.image;

                if (item.image) {
                    document.getElementById('image-preview').src = item.image;
                    document.getElementById('image-preview-container').classList.remove('hidden');
                }
            }
        } else {
            document.getElementById('modal-title').innerText = "Add New Dish";
            document.getElementById('edit-item-id').value = '';
        }

        modal.classList.remove('hidden');
    }

    function closeMenuModal() {
        document.getElementById('menu-modal').classList.add('hidden');
    }

    function handleImageUpload(e) {
        const file = e.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(event) {
                document.getElementById('item-image-url').value = event.target.result;
                document.getElementById('image-preview').src = event.target.result;
                document.getElementById('image-preview-container').classList.remove('hidden');
            };
            reader.readAsDataURL(file);
        }
    }

    function saveMenuItem(e) {
        e.preventDefault();
        const editId = document.getElementById('edit-item-id').value;
        const name = document.getElementById('item-name').value.trim();
        const price = parseFloat(document.getElementById('item-price').value);
        const category = document.getElementById('item-category').value;
        let image = document.getElementById('item-image-url').value.trim();

        if (!image) image = PLACEHOLDER_IMG;

        if (editId) {
            const index = menuItems.findIndex(m => m.id === editId);
            if (index !== -1) {
                menuItems[index] = { id: editId, name, price, category, image };
            }
        } else {
            const newItem = {
                id: Date.now().toString(),
                name,
                price,
                category,
                image
            };
            menuItems.push(newItem);
        }

        saveMenuToStorage();
        renderMenuGrid();
        renderMenuManagementTable();
        closeMenuModal();
    }

    function editMenuItem(id) {
        openMenuModal(id);
    }

    function deleteMenuItem(id) {
        if (confirm("Are you sure you want to delete this menu item?")) {
            menuItems = menuItems.filter(m => m.id !== id);
            saveMenuToStorage();
            renderMenuGrid();
            renderMenuManagementTable();
        }
    }

    function renderReportsData() {
        renderHeaderSummary();

        let totalRevenue = 0;
        let totalUnitsSold = 0;
        const itemStats = {};

        menuItems.forEach(item => {
            itemStats[item.name] = {
                name: item.name,
                category: item.category,
                unitPrice: item.price,
                qtySold: 0,
                revenue: 0
            };
        });

        salesLog.forEach(tx => {
            totalRevenue += tx.totalAmount;
            tx.items.forEach(item => {
                totalUnitsSold += item.qty;
                if (!itemStats[item.name]) {
                    itemStats[item.name] = {
                        name: item.name,
                        category: item.category || 'Other',
                        unitPrice: item.price,
                        qtySold: 0,
                        revenue: 0
                    };
                }
                itemStats[item.name].qtySold += item.qty;
                itemStats[item.name].revenue += (item.price * item.qty);
            });
        });

        document.getElementById('report-total-revenue').innerText = totalRevenue.toFixed(2);
        document.getElementById('report-total-units').innerText = totalUnitsSold;

        let topSeller = '--';
        let maxQty = 0;
        Object.values(itemStats).forEach(s => {
            if (s.qtySold > maxQty) {
                maxQty = s.qtySold;
                topSeller = `${s.name} (${s.qtySold} sold)`;
            }
        });
        document.getElementById('report-top-seller').innerText = topSeller;

        const breakdownBody = document.getElementById('inventory-breakdown-body');
        breakdownBody.innerHTML = '';

        const statsArray = Object.values(itemStats);
        statsArray.sort((a, b) => b.qtySold - a.qtySold);

        statsArray.forEach(stat => {
            const tr = document.createElement('tr');
            tr.className = stat.qtySold > 0 ? "bg-amber-50/30 font-medium" : "text-slate-500";
            tr.innerHTML = `
                <td class="py-3 px-4 font-bold text-slate-800">${stat.name}</td>
                <td class="py-3 px-4 text-xs">
                    <span class="bg-slate-100 text-slate-600 px-2 py-0.5 rounded-md border">${stat.category}</span>
                </td>
                <td class="py-3 px-4 text-slate-600">₱${stat.unitPrice.toFixed(2)}</td>
                <td class="py-3 px-4 text-center">
                    <span class="px-2.5 py-1 rounded-full ${stat.qtySold > 0 ? 'bg-brand-100 text-brand-800 font-bold' : 'bg-slate-100 text-slate-400'} text-xs">
                        ${stat.qtySold} orders
                    </span>
                </td>
                <td class="py-3 px-4 text-right font-bold ${stat.revenue > 0 ? 'text-emerald-600' : 'text-slate-400'}">
                    ₱${stat.revenue.toFixed(2)}
                </td>
            `;
            breakdownBody.appendChild(tr);
        });

        document.getElementById('foot-total-orders').innerText = `${totalUnitsSold} orders`;
        document.getElementById('foot-total-revenue').innerText = `₱${totalRevenue.toFixed(2)}`;

        const txBody = document.getElementById('transactions-log-body');
        txBody.innerHTML = '';

        if (salesLog.length === 0) {
            txBody.innerHTML = `
                <tr>
                    <td colspan="5" class="py-6 text-center text-slate-400">No completed sales recorded today yet.</td>
                </tr>
            `;
        } else {
            salesLog.forEach(tx => {
                const itemsSummary = tx.items.map(i => `${i.qty}x ${i.name}`).join(', ');
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50";
                tr.innerHTML = `
                    <td class="py-2.5 px-4 font-bold text-slate-700">${tx.id}</td>
                    <td class="py-2.5 px-4 text-slate-500">${tx.timestamp}</td>
                    <td class="py-2.5 px-4 text-slate-800 font-medium truncate max-w-xs" title="${itemsSummary}">${itemsSummary}</td>
                    <td class="py-2.5 px-4 text-right font-bold text-emerald-600">₱${tx.totalAmount.toFixed(2)}</td>
                    <td class="py-2.5 px-4 text-right text-slate-500">Cash: ₱${tx.cashTendered.toFixed(0)} | Chg: ₱${tx.change.toFixed(0)}</td>
                `;
                txBody.appendChild(tr);
            });
        }
    }

    function renderHeaderSummary() {
        let totalSales = 0;
        let totalOrders = salesLog.length;

        salesLog.forEach(tx => {
            totalSales += tx.totalAmount;
        });

        document.getElementById('header-total-orders').innerText = totalOrders;
        document.getElementById('header-total-sales').innerText = totalSales.toFixed(2);
    }

    function exportSalesSummary() {
        if (salesLog.length === 0) {
            alert("No sales recorded to export.");
            return;
        }

        let csvContent = "data:text/csv;charset=utf-8,Transaction ID,Date Time,Total Amount,Cash Tendered,Change,Items Summary\n";

        salesLog.forEach(tx => {
            const itemsSummary = tx.items.map(i => `${i.qty}x ${i.name}`).join(' | ');
            csvContent += `"${tx.id}","${tx.timestamp}","${tx.totalAmount}","${tx.cashTendered}","${tx.change}","${itemsSummary}"\n`;
        });

        const encodedUri = encodeURI(csvContent);
        const link = document.createElement("a");
        link.setAttribute("href", encodedUri);
        link.setAttribute("download", `Carinderia_Sales_${new Date().toISOString().slice(0,10)}.csv`);
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    }

    function resetDailyData() {
        if (confirm("Are you sure you want to reset all today's sales and inventory stats? This cannot be undone.")) {
            salesLog = [];
            saveSalesToStorage();
            renderReportsData();
        }
    }
</script>



```