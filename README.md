# pemesanan
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu & Pemesanan Makanan</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 pb-24 md:pb-8">

    <!-- Header / Banner Restoran -->
    <header class="relative bg-amber-600 text-white">
        <div class="h-48 md:h-64 w-full bg-cover bg-center opacity-40" style="background-image: url('https://images.unsplash.com/photo-1555396273-367ea4eb4db5?auto=format&fit=crop&w=1200&q=80');"></div>
        <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent"></div>
        
        <div class="absolute bottom-0 inset-x-0 max-w-5xl mx-auto p-4 md:p-6 flex flex-col md:flex-row items-start md:items-end justify-between gap-4">
            <div class="flex items-center gap-4">
                <div class="w-20 h-20 md:w-24 md:h-24 rounded-2xl bg-white p-1 shadow-xl overflow-hidden flex-shrink-0">
                    <img src="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=300&q=80" alt="Logo Restoran" class="w-full h-full object-cover rounded-xl">
                </div>
                <div>
                    <span class="inline-block bg-amber-500/80 text-xs px-2.5 py-0.5 rounded-full font-semibold uppercase tracking-wider mb-1">Restoran & Cafe</span>
                    <h1 class="text-2xl md:text-3xl font-extrabold text-white" id="restaurant-name">Dapur Kuliner Nusantara</h1>
                    <p class="text-xs md:text-sm text-gray-200 mt-1 flex items-center gap-2">
                        <span><i class="fa-solid me-1 fa-location-dot text-amber-400"></i> Buka Setiap Hari (10.00 - 22.00 WIB)</span>
                        <span>•</span>
                        <span><i class="fa-solid fa-star text-yellow-400"></i> 4.8 (500+ ulasan)</span>
                    </p>
                </div>
            </div>
            
            <a href="https://maps.app.goo.gl/7Cehz7fHiNoTdNzK6" target="_blank" class="bg-white/20 hover:bg-white/30 backdrop-blur-md text-white px-4 py-2 rounded-xl text-xs font-semibold flex items-center gap-2 border border-white/30 transition">
                <i class="fa-solid fa-map-location-dot"></i> Lihat di Google Maps
            </a>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-5xl mx-auto px-4 py-6">

        <!-- Search Bar & Filter Kategori -->
        <div class="sticky top-0 z-20 bg-gray-50/95 backdrop-blur-md py-3 -mx-4 px-4 border-b border-gray-200">
            <div class="relative mb-3">
                <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                <input type="text" id="search-input" onkeyup="filterMenu()" placeholder="Cari makanan atau minuman favorit..." class="w-full pl-11 pr-4 py-2.5 bg-white border border-gray-300 rounded-xl shadow-sm focus:outline-none focus:ring-2 focus:ring-amber-500 text-sm">
            </div>

            <!-- Category Pills -->
            <div class="flex items-center gap-2 overflow-x-auto no-scrollbar py-1" id="category-container">
                <button onclick="setCategory('all')" class="category-btn active px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap bg-amber-600 text-white shadow-sm transition">
                    Semua Menu
                </button>
                <button onclick="setCategory('makanan')" class="category-btn px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap bg-white text-gray-600 border border-gray-200 hover:bg-gray-100 shadow-sm transition">
                    🍔 Makanan Utama
                </button>
                <button onclick="setCategory('minuman')" class="category-btn px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap bg-white text-gray-600 border border-gray-200 hover:bg-gray-100 shadow-sm transition">
                    🥤 Minuman Segar
                </button>
                <button onclick="setCategory('camilan')" class="category-btn px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap bg-white text-gray-600 border border-gray-200 hover:bg-gray-100 shadow-sm transition">
                    🍟 Camilan & Dessert
                </button>
                <button onclick="setCategory('paket')" class="category-btn px-4 py-2 rounded-xl text-xs font-bold whitespace-nowrap bg-white text-gray-600 border border-gray-200 hover:bg-gray-100 shadow-sm transition">
                    🔥 Paket Hemat
                </button>
            </div>
        </div>

        <!-- Menu Grid -->
        <section class="mt-6">
            <h2 class="text-lg font-bold text-gray-900 mb-4 flex items-center justify-between">
                <span>Daftar Menu</span>
                <span class="text-xs font-normal text-gray-500" id="item-count">Menampilkan semua menu</span>
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4" id="menu-grid">
                <!-- Menu items akan dirender secara dinamis melalui JavaScript -->
            </div>
        </section>

    </main>

    <!-- Floating Order Bar (Tampilan Mobile) -->
    <div id="floating-cart" class="fixed bottom-0 inset-x-0 bg-white border-t border-gray-200 p-4 shadow-2xl z-30 hidden md:hidden">
        <div class="flex items-center justify-between gap-4">
            <div>
                <p class="text-xs text-gray-500"><span id="cart-total-items">0</span> Item dipilih</p>
                <p class="text-lg font-extrabold text-amber-600" id="cart-total-price">Rp 0</p>
            </div>
            <button onclick="toggleCartModal()" class="bg-amber-600 hover:bg-amber-700 text-white font-bold px-6 py-3 rounded-xl shadow-lg flex items-center gap-2 text-sm">
                <i class="fa-solid fa-shopping-bag"></i> Lihat Pesanan
            </button>
        </div>
    </div>

    <!-- Floating Order Button (Desktop) -->
    <button onclick="toggleCartModal()" class="hidden md:flex fixed bottom-6 right-6 bg-amber-600 hover:bg-amber-700 text-white font-bold px-5 py-3.5 rounded-2xl shadow-2xl z-30 items-center gap-3 border-2 border-white transition-all transform hover:scale-105">
        <div class="relative">
            <i class="fa-solid fa-cart-shopping text-lg"></i>
            <span id="desktop-badge" class="absolute -top-2 -right-2 bg-red-500 text-white text-[10px] w-5 h-5 rounded-full flex items-center justify-center font-extrabold border-2 border-white">0</span>
        </div>
        <span>Keranjang Pesanan</span>
        <span id="desktop-price-badge" class="bg-amber-700/60 px-2.5 py-1 rounded-lg text-xs">Rp 0</span>
    </button>

    <!-- Cart Modal / Sidebar Pemesanan -->
    <div id="cart-modal" class="fixed inset-0 z-50 hidden bg-black/60 backdrop-blur-sm flex justify-end">
        <div class="bg-white w-full max-w-md h-full flex flex-col justify-between p-6 shadow-2xl overflow-y-auto transform transition-transform">
            <div>
                <div class="flex items-center justify-between pb-4 border-b border-gray-200">
                    <h3 class="text-xl font-bold text-gray-900 flex items-center gap-2">
                        <i class="fa-solid fa-receipt text-amber-600"></i> Ringkasan Pesanan
                    </h3>
                    <button onclick="toggleCartModal()" class="w-8 h-8 rounded-full bg-gray-100 hover:bg-gray-200 text-gray-600 flex items-center justify-center">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>

                <!-- Tipe Pemesanan -->
                <div class="my-4 p-1.5 bg-gray-100 rounded-xl flex gap-1">
                    <button onclick="setOrderType('dine_in')" id="btn-dine-in" class="flex-1 py-2 text-xs font-bold rounded-lg bg-white text-amber-600 shadow-sm">Makan di Tempat</button>
                    <button onclick="setOrderType('takeaway')" id="btn-takeaway" class="flex-1 py-2 text-xs font-bold rounded-lg text-gray-600">Bawa Pulang (Takeaway)</button>
                </div>

                <!-- Form Informasi Pelanggan -->
                <div class="space-y-3 mb-6">
                    <div>
                        <label class="block text-xs font-semibold text-gray-600 mb-1">Nama Pemesan</label>
                        <input type="text" id="customer-name" placeholder="Masukkan nama Anda" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none">
                    </div>
                    <div id="table-number-container">
                        <label class="block text-xs font-semibold text-gray-600 mb-1">Nomor Meja</label>
                        <input type="text" id="table-number" placeholder="Contoh: Meja 05" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:ring-2 focus:ring-amber-500 focus:outline-none">
                    </div>
                </div>

                <!-- List Items di Keranjang -->
                <div class="space-y-3 mb-4 max-h-60 overflow-y-auto pr-1" id="cart-items-list">
                    <p class="text-center text-sm text-gray-400 py-8">Keranjang Anda masih kosong.</p>
                </div>
            </div>

            <!-- Total & Tombol Checkout -->
            <div class="border-t border-gray-200 pt-4 space-y-3">
                <div class="flex justify-between text-sm text-gray-600">
                    <span>Subtotal</span>
                    <span id="summary-subtotal">Rp 0</span>
                </div>
                <div class="flex justify-between text-sm text-gray-600">
                    <span>Pajak & Layanan (10%)</span>
                    <span id="summary-tax">Rp 0</span>
                </div>
                <div class="flex justify-between text-base font-bold text-gray-900 pt-2 border-t border-gray-100">
                    <span>Total Bayar</span>
                    <span class="text-amber-600" id="summary-total">Rp 0</span>
                </div>

                <button onclick="submitOrderViaWhatsApp()" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3.5 rounded-xl shadow-lg flex items-center justify-center gap-2 text-sm transition">
                    <i class="fa-brands fa-whatsapp text-lg"></i> Kirim Pesanan via WhatsApp
                </button>
            </div>
        </div>
    </div>

    <!-- Script JavaScript -->
    <script>
        // Data Menu Restoran
        const menuData = [
            {
                id: 1,
                name: "Nasi Goreng Spesial Dapur",
                category: "makanan",
                price: 28000,
                desc: "Nasi goreng khas dengan sosis, ayam suwir, telur mata sapi, dan keripik udang.",
                image: "https://images.unsplash.com/photo-1603133872878-684f208fb84b?auto=format&fit=crop&w=500&q=80",
                badge: "Populer"
            },
            {
                id: 2,
                name: "Ayam Bakar Madu Pedas",
                category: "makanan",
                price: 32000,
                desc: "Ayam paha/dada pilihan dibakar dengan olesan madu murni dan bumbu pedas manis.",
                image: "https://images.unsplash.com/photo-1598515214211-89d3c73ae83b?auto=format&fit=crop&w=500&q=80",
                badge: "Rekomendasi"
            },
            {
                id: 3,
                name: "Mie Goreng Jawa Seafood",
                category: "makanan",
                price: 30000,
                desc: "Mie telur kenyal ditumis dengan udang segar, cumi, bakso ikan, dan sayuran.",
                image: "https://images.unsplash.com/photo-1612927601601-6638404737ce?auto=format&fit=crop&w=500&q=80",
                badge: ""
            },
            {
                id: 4,
                name: "Es Teh Manis Jumbo",
                category: "minuman",
                price: 7000,
                desc: "Teh melati pilihan dengan rasa manis pas dan porsi segar jumbo.",
                image: "https://images.unsplash.com/photo-1556679343-c7306c1976bc?auto=format&fit=crop&w=500&q=80",
                badge: "Segar"
            },
            {
                id: 5,
                name: "Kopi Susu Gula Aren",
                category: "minuman",
                price: 18000,
                desc: "Espresso arabika dipadu susu segar gurih dan gula aren asli.",
                image: "https://images.unsplash.com/photo-1541167760496-1628856ab772?auto=format&fit=crop&w=500&q=80",
                badge: "Best Seller"
            },
            {
                id: 6,
                name: "Jus Alpukat Kocok Keju",
                category: "minuman",
                price: 22000,
                desc: "Alpukat mentega asli dengan topping kental manis cokelat dan parutan keju.",
                image: "https://images.unsplash.com/photo-1553530666-ba11a7da3888?auto=format&fit=crop&w=500&q=80",
                badge: ""
            },
            {
                id: 7,
                name: "Pisang Goreng Cokelat Keju",
                category: "camilan",
                price: 18000,
                desc: "Pisang kepok renyah dengan taburan meses cokelat dan keju melimpah.",
                image: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af?auto=format&fit=crop&w=500&q=80",
                badge: ""
            },
            {
                id: 8,
                name: "Paket Hemat Kenyang A",
                category: "paket",
                price: 35000,
                desc: "1 Nasi Goreng Spesial + 1 Es Teh Manis Jumbo (Hemat Rp 3.000)",
                image: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&w=500&q=80",
                badge: "Hemat"
            }
        ];

        // State Aplikasi
        let cart = {};
        let currentCategory = 'all';
        let orderType = 'dine_in';
        const WHATSAPP_NUMBER = "6281234567890"; // Ganti dengan nomor WhatsApp Restoran Anda

        // Format Rupiah
        function formatRupiah(number) {
            return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', maximumFractionDigits: 0 }).format(number);
        }

        // Render Menu
        function renderMenu(items) {
            const grid = document.getElementById('menu-grid');
            document.getElementById('item-count').innerText = `Menampilkan ${items.length} menu`;

            if (items.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center py-12 text-gray-400">Menu tidak ditemukan.</div>`;
                return;
            }

            grid.innerHTML = items.map(item => {
                const qty = cart[item.id] ? cart[item.id].qty : 0;
                return `
                <div class="bg-white rounded-2xl p-3 shadow-sm border border-gray-100 flex flex-col justify-between hover:shadow-md transition">
                    <div>
                        <div class="relative h-40 w-full mb-3 rounded-xl overflow-hidden bg-gray-100">
                            <img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover">
                            ${item.badge ? `<span class="absolute top-2 left-2 bg-amber-600 text-white text-[10px] font-bold px-2.5 py-1 rounded-md uppercase shadow">${item.badge}</span>` : ''}
                        </div>
                        <h3 class="font-bold text-gray-900 text-base leading-snug">${item.name}</h3>
                        <p class="text-xs text-gray-500 mt-1 line-clamp-2">${item.desc}</p>
                    </div>

                    <div class="flex items-center justify-between mt-4 pt-2 border-t border-gray-50">
                        <span class="font-extrabold text-amber-600 text-base">${formatRupiah(item.price)}</span>
                        
                        <div id="btn-container-${item.id}">
                            ${qty > 0 ? `
                                <div class="flex items-center gap-2 bg-amber-50 rounded-xl p-1 border border-amber-200">
                                    <button onclick="updateQty(${item.id}, -1)" class="w-7 h-7 bg-white rounded-lg text-amber-600 font-bold shadow-sm hover:bg-amber-100 flex items-center justify-center">-</button>
                                    <span class="text-xs font-extrabold px-1 text-gray-800">${qty}</span>
                                    <button onclick="updateQty(${item.id}, 1)" class="w-7 h-7 bg-amber-600 rounded-lg text-white font-bold shadow-sm hover:bg-amber-700 flex items-center justify-center">+</button>
                                </div>
                            ` : `
                                <button onclick="updateQty(${item.id}, 1)" class="bg-amber-600 hover:bg-amber-700 text-white font-bold text-xs px-3.5 py-2 rounded-xl flex items-center gap-1 shadow-sm transition">
                                    <i class="fa-solid fa-plus"></i> Tambah
                                </button>
                            `}
                        </div>
                    </div>
                </div>
            `}).join('');
        }

        // Update Kuantitas Cart
        function updateQty(itemId, change) {
            const item = menuData.find(m => m.id === itemId);
            if (!cart[itemId]) {
                cart[itemId] = { ...item, qty: 0 };
            }

            cart[itemId].qty += change;

            if (cart[itemId].qty <= 0) {
                delete cart[itemId];
            }

            updateUI();
        }

        // Update Seluruh Tampilan UI
        function updateUI() {
            // Re-render menu sesuai filter aktif
            filterMenu();

            // Hitung total items & harga
            let totalItems = 0;
            let subtotal = 0;

            Object.values(cart).forEach(item => {
                totalItems += item.qty;
                subtotal += (item.price * item.qty);
            });

            const tax = subtotal * 0.10;
            const grandTotal = subtotal + tax;

            // Update Floating Bar
            const floatingCart = document.getElementById('floating-cart');
            if (totalItems > 0) {
                floatingCart.classList.remove('hidden');
            } else {
                floatingCart.classList.add('hidden');
            }

            document.getElementById('cart-total-items').innerText = totalItems;
            document.getElementById('cart-total-price').innerText = formatRupiah(grandTotal);
            document.getElementById('desktop-badge').innerText = totalItems;
            document.getElementById('desktop-price-badge').innerText = formatRupiah(grandTotal);

            // Update Cart Modal List
            const cartList = document.getElementById('cart-items-list');
            if (Object.keys(cart).length === 0) {
                cartList.innerHTML = `<p class="text-center text-sm text-gray-400 py-8">Keranjang Anda masih kosong.</p>`;
            } else {
                cartList.innerHTML = Object.values(cart).map(item => `
                    <div class="flex items-center justify-between bg-gray-50 p-3 rounded-xl">
                        <div class="flex-1 pr-2">
                            <h4 class="font-bold text-xs text-gray-800">${item.name}</h4>
                            <p class="text-xs text-gray-500">${formatRupiah(item.price)} x ${item.qty}</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="updateQty(${item.id}, -1)" class="w-6 h-6 bg-white border border-gray-300 rounded text-xs font-bold">-</button>
                            <span class="text-xs font-bold">${item.qty}</span>
                            <button onclick="updateQty(${item.id}, 1)" class="w-6 h-6 bg-amber-600 text-white rounded text-xs font-bold">+</button>
                        </div>
                    </div>
                `).join('');
            }

            document.getElementById('summary-subtotal').innerText = formatRupiah(subtotal);
            document.getElementById('summary-tax').innerText = formatRupiah(tax);
            document.getElementById('summary-total').innerText = formatRupiah(grandTotal);
        }

        // Category Filter
        function setCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('bg-amber-600', 'text-white');
                btn.classList.add('bg-white', 'text-gray-600');
            });
            event.currentTarget.classList.remove('bg-white', 'text-gray-600');
            event.currentTarget.classList.add('bg-amber-600', 'text-white');
            filterMenu();
        }

        // Filter Menu berdasarkan Kategori & Search Input
        function filterMenu() {
            const query = document.getElementById('search-input').value.toLowerCase();
            const filtered = menuData.filter(item => {
                const matchCat = (currentCategory === 'all' || item.category === currentCategory);
                const matchQuery = item.name.toLowerCase().includes(query) || item.desc.toLowerCase().includes(query);
                return matchCat && matchQuery;
            });
            renderMenu(filtered);
        }

        // Order Type Toggle
        function setOrderType(type) {
            orderType = type;
            const btnDine = document.getElementById('btn-dine-in');
            const btnTake = document.getElementById('btn-takeaway');
            const tableContainer = document.getElementById('table-number-container');

            if (type === 'dine_in') {
                btnDine.className = "flex-1 py-2 text-xs font-bold rounded-lg bg-white text-amber-600 shadow-sm";
                btnTake.className = "flex-1 py-2 text-xs font-bold rounded-lg text-gray-600";
                tableContainer.classList.remove('hidden');
            } else {
                btnTake.className = "flex-1 py-2 text-xs font-bold rounded-lg bg-white text-amber-600 shadow-sm";
                btnDine.className = "flex-1 py-2 text-xs font-bold rounded-lg text-gray-600";
                tableContainer.classList.add('hidden');
            }
        }

        // Toggle Modal Cart
        function toggleCartModal() {
            const modal = document.getElementById('cart-modal');
            modal.classList.toggle('hidden');
        }

        // Submit Pesanan via WhatsApp
        function submitOrderViaWhatsApp() {
            const name = document.getElementById('customer-name').value.trim();
            const table = document.getElementById('table-number').value.trim();

            if (Object.keys(cart).length === 0) {
                alert("Keranjang Anda masih kosong. Pilih menu terlebih dahulu!");
                return;
            }

            if (!name) {
                alert("Harap masukkan Nama Pemesan!");
                return;
            }

            let subtotal = 0;
            let itemListText = "";

            Object.values(cart).forEach((item, index) => {
                const itemTotal = item.price * item.qty;
                subtotal += itemTotal;
                itemListText += `${index + 1}. *${item.name}* (x${item.qty}) = ${formatRupiah(itemTotal)}\n`;
            });

            const tax = subtotal * 0.10;
            const grandTotal = subtotal + tax;

            let message = `*HALO, SAYA INGIN MEMESAN MAKANAN*\n`;
            message += `-----------------------------------\n`;
            message += `👤 *Nama Pemesan:* ${name}\n`;
            message += `📌 *Tipe Pesanan:* ${orderType === 'dine_in' ? 'Makan di Tempat' : 'Bawa Pulang (Takeaway)'}\n`;
            if (orderType === 'dine_in') {
                message += `🪑 *Nomor Meja:* ${table || 'Belum diisi'}\n`;
            }
            message += `-----------------------------------\n\n`;
            message += `📋 *Rincian Pesanan:*\n${itemListText}\n`;
            message += `-----------------------------------\n`;
            message += `Subtotal: ${formatRupiah(subtotal)}\n`;
            message += `Pajak (10%): ${formatRupiah(tax)}\n`;
            message += `💰 *TOTAL BAYAR:* *${formatRupiah(grandTotal)}*\n\n`;
            message += `Mohon segera diproses. Terima kasih!`;

            const encodedMessage = encodeURIComponent(message);
            window.open(`https://wa.me/${WHATSAPP_NUMBER}?text=${encodedMessage}`, '_blank');
        }

        // Inisialisasi Pertama
        renderMenu(menuData);
    </script>
</body>
</html>
