<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexusForge | Ultra-Premium Esports & Top-Up Portal</title>
    <!-- Tailwind CSS Modern CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts Premium Gaming Aesthetic -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Rajdhani:wght@500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome for Premium Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        display: ['Rajdhani', 'sans-serif'],
                    },
                    colors: {
                        nexus: {
                            dark: '#050508',
                            panel: '#0f0f16',
                            border: '#1f1f2e',
                            purple: '#8b5cf6',
                            purpleGlow: 'rgba(139, 92, 246, 0.5)',
                            blue: '#06b6d4',
                            blueGlow: 'rgba(6, 182, 212, 0.5)',
                            textMut: '#94a3b8'
                        }
                    },
                    backgroundImage: {
                        'neon-gradient': 'linear-gradient(to right, #8b5cf6, #06b6d4)',
                        'panel-gradient': 'linear-gradient(145deg, rgba(255,255,255,0.03) 0%, rgba(255,255,255,0.01) 100%)'
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #050508;
            color: #f8fafc;
            overflow-x: hidden;
        }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #050508; }
        ::-webkit-scrollbar-thumb { background: #1f1f2e; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #8b5cf6; }

        .glass-panel {
            background: rgba(15, 15, 22, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .neon-border:hover {
            border-color: #06b6d4;
            box-shadow: 0 0 15px rgba(6, 182, 212, 0.3);
            transform: translateY(-2px);
        }
        .text-neon {
            background: linear-gradient(to right, #8b5cf6, #06b6d4);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .animate-pulse-slow {
            animation: pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
        
        .view-section { display: none; }
        .view-section.active { display: block; animation: fadeIn 0.4s ease-in-out; }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Animasi khusus untuk angka statistik */
        .stat-update {
            animation: colorFlash 1s ease-out;
        }
        @keyframes colorFlash {
            0% { color: #06b6d4; text-shadow: 0 0 10px #06b6d4; }
            100% { color: white; text-shadow: none; }
        }
    </style>
</head>
<body class="antialiased min-h-screen flex flex-col relative">

    <!-- Background Atmospheric Glow -->
    <div class="fixed top-0 left-0 w-full h-full overflow-hidden -z-10 pointer-events-none">
        <div class="absolute top-[-10%] left-[-10%] w-[40%] h-[40%] bg-nexus-purple rounded-full blur-[150px] opacity-20 animate-pulse-slow"></div>
        <div class="absolute bottom-[-10%] right-[-10%] w-[40%] h-[40%] bg-nexus-blue rounded-full blur-[150px] opacity-20"></div>
    </div>

    <!-- Header Navigation -->
    <header class="glass-panel sticky top-0 z-50 border-b border-nexus-border">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <div class="flex-shrink-0 cursor-pointer" onclick="app.navigate('home')">
                    <h1 class="font-display font-bold text-3xl tracking-wider text-white">
                        NEXUS<span class="text-neon">FORGE</span>
                    </h1>
                </div>
                
                <nav class="hidden md:flex space-x-8">
                    <button onclick="app.navigate('home')" class="text-gray-300 hover:text-nexus-blue transition-colors font-medium text-sm tracking-wide bg-transparent border-none cursor-pointer">DIRECTORY</button>
                    <button onclick="app.navigate('marketplace')" class="text-gray-300 hover:text-nexus-blue transition-colors font-medium text-sm tracking-wide bg-transparent border-none cursor-pointer">MARKETPLACE</button>
                </nav>

                <div class="flex items-center space-x-4 md:space-x-6">
                    <button onclick="app.toggleCart()" class="text-gray-400 hover:text-white transition-colors relative bg-transparent border-none cursor-pointer">
                        <i class="fas fa-shopping-cart text-xl"></i>
                        <span id="cart-badge" class="absolute -top-2 -right-2 bg-nexus-purple text-white text-[10px] font-bold px-1.5 py-0.5 rounded-full hidden">0</span>
                    </button>
                    <!-- Tambahan Tombol Registrasi Akun -->
                    <button onclick="app.navigate('register')" class="hidden sm:flex items-center bg-nexus-dark border border-nexus-purple text-white px-4 py-2 rounded-lg hover:bg-nexus-purple hover:border-transparent transition-all duration-300 cursor-pointer text-sm font-bold tracking-wide">
                        <i class="fas fa-user-circle mr-2"></i> FORGE ID
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Dynamic Wrapper -->
    <main class="flex-grow w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- ================= 1. HOME VIEW ================= -->
        <section id="view-home" class="view-section active">
            <!-- Premium Banner Carousel Space -->
            <div class="relative rounded-2xl overflow-hidden glass-panel border-nexus-border mb-8 group">
                <div class="absolute inset-0 bg-gradient-to-r from-nexus-dark via-nexus-dark/60 to-transparent z-10"></div>
                <img src="https://placehold.co/1200x400/0a0a0f/8b5cf6?text=NEXUSFORGE+ELITE+HUB" alt="Hero Banner" class="w-full h-64 md:h-96 object-cover object-center opacity-40 group-hover:opacity-50 transition-opacity duration-700">
                <div class="absolute inset-0 z-20 flex flex-col justify-center px-8 md:px-16 w-full md:w-2/3">
                    <span class="text-nexus-blue font-display tracking-widest text-sm mb-2 uppercase">Welcome to the Nexus</span>
                    <h2 class="text-4xl md:text-6xl font-display font-bold text-white mb-4 leading-tight">FORGE YOUR <span class="text-neon">LEGACY</span></h2>
                    <p class="text-nexus-textMut text-sm md:text-base mb-6 max-w-lg leading-relaxed">Platform transaksi aset digital Esports paling aman, mewah, dan terpercaya. Penuhi kebutuhan tempur arena kompetitifmu sekarang.</p>
                </div>
            </div>

            <!-- FITUR BARU: Live Analytics Dashboard -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-12">
                <!-- Stat: Total Pengunjung -->
                <div class="glass-panel p-5 rounded-xl border border-nexus-border flex items-center justify-between relative overflow-hidden group">
                    <div class="absolute top-0 left-0 w-1 h-full bg-nexus-blue"></div>
                    <div>
                        <p class="text-nexus-textMut text-xs font-display tracking-widest mb-1 uppercase">Total Pengunjung</p>
                        <h4 class="text-2xl font-bold text-white font-display tracking-wider" id="stat-visitors">0</h4>
                    </div>
                    <div class="w-12 h-12 rounded-full bg-nexus-blue/10 flex items-center justify-center text-nexus-blue group-hover:scale-110 transition-transform">
                        <i class="fas fa-users text-xl"></i>
                    </div>
                </div>
                <!-- Stat: Live Pageviews -->
                <div class="glass-panel p-5 rounded-xl border border-nexus-border flex items-center justify-between relative overflow-hidden group">
                    <div class="absolute top-0 left-0 w-1 h-full bg-nexus-purple"></div>
                    <div>
                        <p class="text-nexus-textMut text-xs font-display tracking-widest mb-1 uppercase flex items-center">
                            <span class="w-2 h-2 bg-red-500 rounded-full mr-2 animate-pulse"></span> Live Penonton
                        </p>
                        <h4 class="text-2xl font-bold text-white font-display tracking-wider" id="stat-views">0</h4>
                    </div>
                    <div class="w-12 h-12 rounded-full bg-nexus-purple/10 flex items-center justify-center text-nexus-purple group-hover:scale-110 transition-transform">
                        <i class="fas fa-eye text-xl"></i>
                    </div>
                </div>
                <!-- Stat: Akun Terdaftar -->
                <div class="glass-panel p-5 rounded-xl border border-nexus-border flex items-center justify-between relative overflow-hidden group">
                    <div class="absolute top-0 left-0 w-1 h-full bg-amber-500"></div>
                    <div>
                        <p class="text-nexus-textMut text-xs font-display tracking-widest mb-1 uppercase">Akun Terdaftar</p>
                        <h4 class="text-2xl font-bold text-white font-display tracking-wider" id="stat-accounts">0</h4>
                    </div>
                    <div class="w-12 h-12 rounded-full bg-amber-500/10 flex items-center justify-center text-amber-500 group-hover:scale-110 transition-transform">
                        <i class="fas fa-user-shield text-xl"></i>
                    </div>
                </div>
            </div>

            <!-- Game Directory Grid -->
            <div class="mb-6">
                <div class="flex items-center justify-between mb-8">
                    <h3 class="text-2xl font-display font-bold text-white border-l-4 border-nexus-purple pl-3">GAME DIRECTORY</h3>
                    <div class="h-[1px] flex-grow bg-gradient-to-r from-nexus-border to-transparent ml-6"></div>
                </div>
                <div id="game-directory-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                    <!-- Loaded dynamically via JavaScript -->
                </div>
            </div>

            <!-- Sponsor Placement Area -->
            <div class="w-full h-24 glass-panel border border-dashed border-nexus-border rounded-xl flex items-center justify-center mt-12 opacity-50 hover:opacity-100 transition-opacity">
                <span class="text-nexus-textMut text-sm tracking-widest font-display"><i class="fas fa-ad mr-2"></i> PREMIUM SPONSOR PLACEMENT</span>
            </div>
        </section>

        <!-- ================= 2. GAME DETAIL VIEW (TOP-UP) ================= -->
        <section id="view-game-detail" class="view-section">
            <button onclick="app.navigate('home')" class="text-nexus-textMut hover:text-white mb-6 flex items-center text-sm font-medium transition-colors bg-transparent border-none cursor-pointer">
                <i class="fas fa-arrow-left mr-2"></i> Back to Directory
            </button>

            <!-- Dynamic Game Profile Header -->
            <div id="game-detail-header" class="flex flex-col md:flex-row items-center md:items-end gap-6 glass-panel p-6 rounded-2xl mb-12 border-nexus-border relative overflow-hidden">
                <!-- Loaded dynamically via JavaScript -->
            </div>

            <div class="flex flex-col lg:flex-row gap-8">
                <!-- Catalog Lists Container -->
                <div class="w-full lg:w-3/4">
                    <h3 class="text-2xl font-display font-bold text-white mb-6 flex items-center">
                        <i class="fas fa-bolt text-nexus-blue mr-3"></i> TOP-UP CATALOGUE
                    </h3>
                    <div id="topup-tiers-container" class="space-y-12">
                        <!-- Loaded dynamically via JavaScript -->
                    </div>
                </div>

                <!-- Right Quick Marketplace Nav -->
                <div class="w-full lg:w-1/4">
                    <div class="sticky top-28 glass-panel p-6 rounded-2xl border-nexus-border">
                        <h4 class="font-display font-bold text-lg mb-4 text-white">Butuh Akun Game?</h4>
                        <p class="text-sm text-nexus-textMut mb-6">Jelajahi pasar akun premium kami khusus untuk game ini. Mulai dari aset starter hingga akun Sultan koleksi terbatas.</p>
                        <button onclick="app.navigateToMarketplaceForCurrentGame()" class="w-full bg-transparent border border-nexus-purple text-nexus-purple hover:bg-nexus-purple hover:text-white font-bold py-3 px-4 rounded-xl transition-all duration-300 flex items-center justify-center cursor-pointer">
                            Buka Marketplace <i class="fas fa-external-link-alt ml-2"></i>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- ================= 3. MARKETPLACE VIEW ================= -->
        <section id="view-marketplace" class="view-section">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10 gap-4">
                <div>
                    <h2 class="text-3xl md:text-4xl font-display font-bold text-white mb-2">ELITE <span class="text-neon">MARKETPLACE</span></h2>
                    <p class="text-nexus-textMut">Pusat jual-beli akun game tersertifikasi tingkat tinggi berdasarkan kasta harga.</p>
                </div>
                <!-- Dropdown Filter -->
                <div class="glass-panel px-4 py-2 rounded-lg border-nexus-border flex items-center">
                    <i class="fas fa-filter text-nexus-textMut mr-3"></i>
                    <select id="marketplace-game-filter" onchange="app.filterMarketplace(this.value)" class="bg-transparent text-white border-none focus:ring-0 outline-none cursor-pointer pr-4">
                        <option value="all" class="bg-nexus-panel">Semua Game</option>
                    </select>
                </div>
            </div>

            <div id="marketplace-container" class="space-y-16">
                <!-- Loaded dynamically via JavaScript -->
            </div>
        </section>

        <!-- ================= 4. COMPLAINT CENTER VIEW ================= -->
        <section id="view-complaint" class="view-section">
            <div class="max-w-3xl mx-auto">
                <div class="text-center mb-10">
                    <h2 class="text-3xl font-display font-bold text-white mb-4">PUSAT ADUAN & BANTUAN KLIEN</h2>
                    <p class="text-nexus-textMut text-sm">NexusForge menjamin keamanan mutlak di setiap transaksi. Laporkan kendala administrasi, pembayaran, atau serah terima aset Anda di bawah ini.</p>
                </div>

                <div class="glass-panel p-8 rounded-2xl border-nexus-border relative overflow-hidden">
                    <div class="absolute top-0 left-0 w-1 h-full bg-gradient-to-b from-red-500 to-nexus-purple"></div>
                    
                    <form id="complaint-form" onsubmit="app.submitComplaint(event)" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-sm font-medium text-gray-400 mb-2">ID Invoice / Transaksi</label>
                                <input type="text" required class="w-full bg-nexus-dark border border-nexus-border rounded-lg px-4 py-3 text-white focus:outline-none focus:border-nexus-purple focus:ring-1 focus:ring-nexus-purple transition-colors" placeholder="INV-XXXX-XXXX">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-400 mb-2">Kategori Masalah</label>
                                <select required class="w-full bg-nexus-dark border border-nexus-border rounded-lg px-4 py-3 text-white focus:outline-none focus:border-nexus-purple transition-colors">
                                    <option value="" class="bg-nexus-panel">Pilih Kategori Kendala...</option>
                                    <option value="topup" class="bg-nexus-panel">Top-Up Gagal / Belum Masuk</option>
                                    <option value="account" class="bg-nexus-panel">Spesifikasi Akun Tidak Cocok</option>
                                    <option value="gateway" class="bg-nexus-panel">Kendala Sistem Pembayaran</option>
                                </select>
                            </div>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-400 mb-2">Alamat Email Aktif</label>
                            <input type="email" required class="w-full bg-nexus-dark border border-nexus-border rounded-lg px-4 py-3 text-white focus:outline-none focus:border-nexus-purple transition-colors" placeholder="player@domain.com">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-400 mb-2">Deskripsi Detail Kronologi</label>
                            <textarea required rows="5" class="w-full bg-nexus-dark border border-nexus-border rounded-lg px-4 py-3 text-white focus:outline-none focus:border-nexus-purple transition-colors resize-none" placeholder="Tuliskan kendala Anda dengan lengkap..."></textarea>
                        </div>
                        <button type="submit" class="w-full bg-gradient-to-r from-nexus-purple to-nexus-blue text-white font-bold py-4 px-6 rounded-xl hover:shadow-[0_0_20px_rgba(139,92,246,0.4)] transition-all duration-300 cursor-pointer">
                            Kirim Laporan Resmi
                        </button>
                    </form>
                </div>
            </div>
        </section>

        <!-- ================= 5. FITUR BARU: REGISTER VIEW ================= -->
        <section id="view-register" class="view-section">
            <div class="max-w-md mx-auto mt-10">
                <div class="glass-panel p-8 rounded-2xl border-nexus-border relative overflow-hidden shadow-2xl">
                    <!-- Ornamen Desain -->
                    <div class="absolute -top-10 -right-10 w-32 h-32 bg-nexus-purple rounded-full blur-[50px] opacity-20 pointer-events-none"></div>
                    <div class="absolute -bottom-10 -left-10 w-32 h-32 bg-nexus-blue rounded-full blur-[50px] opacity-20 pointer-events-none"></div>
                    
                    <div class="text-center mb-8 relative z-10">
                        <div class="w-16 h-16 bg-nexus-dark border border-nexus-border rounded-full flex items-center justify-center mx-auto mb-4 shadow-lg">
                            <i class="fas fa-user-astronaut text-2xl text-nexus-blue"></i>
                        </div>
                        <h2 class="text-3xl font-display font-bold text-white mb-2">FORGE YOUR <span class="text-neon">ID</span></h2>
                        <p class="text-nexus-textMut text-sm">Daftar sekarang untuk mendapatkan akses prioritas ke aset sultan dan history transaksi.</p>
                    </div>

                    <form id="register-form" onsubmit="app.registerAccount(event)" class="space-y-5 relative z-10">
                        <div>
                            <label class="block text-xs font-bold tracking-wider text-gray-400 mb-2 uppercase">Username Gaming</label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                    <i class="fas fa-gamepad text-gray-500"></i>
                                </div>
                                <input type="text" required id="reg-username" class="w-full bg-nexus-dark border border-nexus-border rounded-lg pl-11 pr-4 py-3 text-white focus:outline-none focus:border-nexus-blue transition-colors" placeholder="ProPlayer99">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-bold tracking-wider text-gray-400 mb-2 uppercase">Alamat Email</label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                    <i class="fas fa-envelope text-gray-500"></i>
                                </div>
                                <input type="email" required id="reg-email" class="w-full bg-nexus-dark border border-nexus-border rounded-lg pl-11 pr-4 py-3 text-white focus:outline-none focus:border-nexus-blue transition-colors" placeholder="email@domain.com">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-bold tracking-wider text-gray-400 mb-2 uppercase">Password Keamanan</label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                    <i class="fas fa-lock text-gray-500"></i>
                                </div>
                                <input type="password" required id="reg-password" class="w-full bg-nexus-dark border border-nexus-border rounded-lg pl-11 pr-4 py-3 text-white focus:outline-none focus:border-nexus-blue transition-colors" placeholder="••••••••">
                            </div>
                        </div>
                        
                        <div class="pt-4">
                            <button type="submit" class="w-full bg-gradient-to-r from-nexus-purple to-nexus-blue text-white font-bold py-3.5 px-6 rounded-xl hover:shadow-[0_0_20px_rgba(6,182,212,0.4)] transition-all duration-300 cursor-pointer flex justify-center items-center">
                                Ciptakan Akun Nexus <i class="fas fa-arrow-right ml-2"></i>
                            </button>
                        </div>
                        <p class="text-center text-xs text-nexus-textMut mt-4">
                            Sudah memiliki Forge ID? <span onclick="app.showToast('Sistem login sedang dalam maintenance.')" class="text-nexus-blue cursor-pointer hover:underline">Masuk di sini</span>.
                        </p>
                    </form>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer Space -->
    <footer class="bg-[#050508] border-t border-nexus-border mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div>
                    <h3 class="font-display font-bold text-2xl text-white mb-4">NEXUS<span class="text-neon">FORGE</span></h3>
                    <p class="text-nexus-textMut text-sm mb-4">Gerbang utama menuju ekosistem aset Esports premium modern. Aman, Instan, Mewah.</p>
                    <div class="flex space-x-4">
                        <span class="text-gray-500 hover:text-white cursor-pointer"><i class="fab fa-instagram text-xl"></i></span>
                        <span class="text-gray-500 hover:text-white cursor-pointer"><i class="fab fa-discord text-xl"></i></span>
                        <span class="text-gray-500 hover:text-white cursor-pointer"><i class="fab fa-twitter text-xl"></i></span>
                    </div>
                </div>
                <div>
                    <h4 class="text-white font-bold mb-4 font-display tracking-wider">LEGALITAS</h4>
                    <ul class="space-y-2 text-sm text-nexus-textMut">
                        <li><span class="hover:text-nexus-blue transition-colors cursor-pointer">Terms of Service</span></li>
                        <li><span class="hover:text-nexus-blue transition-colors cursor-pointer">Privacy Policy</span></li>
                        <li><span class="hover:text-nexus-blue transition-colors cursor-pointer">Refund Guarantee</span></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-white font-bold mb-4 font-display tracking-wider">LAYANAN ADUAN</h4>
                    <p class="text-sm text-nexus-textMut mb-4">Mengalami masalah pengiriman produk atau sistem checkout? Tim resolusi kami aktif membantu.</p>
                    <button onclick="app.navigate('complaint')" class="bg-red-500/10 border border-red-500/50 text-red-400 hover:bg-red-500 hover:text-white text-sm font-bold py-2.5 px-4 rounded-lg transition-all duration-300 flex items-center cursor-pointer">
                        <i class="fas fa-headset mr-2"></i> Pusat Aduan & Bantuan Klien
                    </button>
                </div>
            </div>
            <div class="border-t border-nexus-border mt-10 pt-6 text-center text-xs text-nexus-textMut">
                &copy; 2026 NexusForge Portal. All Rights Reserved. Built for Elite Gamers.
            </div>
        </div>
    </footer>

    <!-- Premium Shopping Cart Sidebar Modal -->
    <div id="cart-modal" class="fixed inset-0 z-[100] hidden">
        <div class="absolute inset-0 bg-black/70 backdrop-blur-sm" onclick="app.toggleCart()"></div>
        <div class="absolute right-0 top-0 h-full w-full max-w-md bg-nexus-panel border-l border-nexus-border shadow-2xl flex flex-col transform translate-x-full transition-transform duration-300" id="cart-sidebar">
            <div class="p-6 border-b border-nexus-border flex justify-between items-center">
                <h3 class="text-xl font-display font-bold text-white flex items-center"><i class="fas fa-shopping-cart text-nexus-purple mr-3"></i> TACTICAL CART</h3>
                <button onclick="app.toggleCart()" class="text-gray-400 hover:text-white bg-transparent border-none cursor-pointer"><i class="fas fa-times text-xl"></i></button>
            </div>
            
            <div id="cart-items" class="flex-grow overflow-y-auto p-6 space-y-4">
                <!-- Cart Content loaded dynamically -->
            </div>
            
            <div class="p-6 border-t border-nexus-border bg-nexus-dark">
                <div class="flex justify-between items-center mb-6">
                    <span class="text-gray-400">Total Tagihan</span>
                    <span id="cart-total" class="text-2xl font-bold text-white">Rp 0</span>
                </div>
                <button onclick="app.checkout()" class="w-full bg-gradient-to-r from-nexus-purple to-nexus-blue text-white font-bold py-4 rounded-xl hover:shadow-[0_0_15px_rgba(6,182,212,0.4)] transition-all duration-300 cursor-pointer">
                    Proses Pembayaran Manual
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification Injected Element -->
    <div id="toast-container" class="fixed bottom-6 right-6 z-[200] flex flex-col gap-3 pointer-events-none"></div>

    <!-- Custom Modal Replacement for Native Window Alert -->
    <div id="custom-alert" class="fixed inset-0 z-[250] hidden flex items-center justify-center">
        <div class="absolute inset-0 bg-black/80 backdrop-blur-sm"></div>
        <div class="relative glass-panel border border-nexus-border p-8 rounded-2xl max-w-sm w-full mx-4 text-center transform scale-95 opacity-0 transition-all duration-300" id="custom-alert-box">
            <div id="alert-icon" class="text-4xl mb-4 text-nexus-blue"><i class="fas fa-info-circle"></i></div>
            <h3 id="alert-title" class="text-xl font-display font-bold text-white mb-2">Sistem Notifikasi</h3>
            <p id="alert-message" class="text-nexus-textMut text-sm mb-6">Pesan peringatan sistem.</p>
            <button onclick="app.closeAlert()" class="bg-nexus-dark border border-nexus-border hover:border-nexus-blue text-white font-bold py-2.5 px-6 rounded-lg transition-colors w-full cursor-pointer">Mengerti</button>
        </div>
    </div>

    <!-- Core Interactive Application Logic Script -->
    <script>
        // Secure In-Memory Object Encapsulated Database
        const database = {
            games: [
                { id: 'mlbb', name: 'Mobile Legends', developer: 'Moonton', type: 'MOBA', image: 'https://placehold.co/400x600/10101a/8b5cf6?text=MLBB', bg: 'https://placehold.co/1200x400/050508/8b5cf6?text=MOBILE+LEGENDS+BANG+BANG', icon: 'fas fa-shield-alt' },
                { id: 'valorant', name: 'Valorant', developer: 'Riot Games', type: 'FPS Tactical', image: 'https://placehold.co/400x600/10101a/06b6d4?text=VALORANT', bg: 'https://placehold.co/1200x400/050508/06b6d4?text=VALORANT+ESPORTS', icon: 'fas fa-crosshairs' },
                { id: 'pubgm', name: 'PUBG Mobile', developer: 'Tencent Games', type: 'Battle Royale', image: 'https://placehold.co/400x600/10101a/f59e0b?text=PUBGM', bg: 'https://placehold.co/1200x400/050508/f59e0b?text=PUBG+MOBILE+GLOBAL', icon: 'fas fa-parachute-box' },
                { id: 'ff', name: 'Free Fire', developer: 'Garena', type: 'Survival Shooter', image: 'https://placehold.co/400x600/10101a/ef4444?text=FREE+FIRE', bg: 'https://placehold.co/1200x400/050508/ef4444?text=FREE+FIRE+ARENA', icon: 'fas fa-fire' }
            ],
            topups: {
                'mlbb': {
                    casual: [{ id: 't_m1', name: '86 Diamonds', price: 21500, desc: 'Bonus Ekstra +8 DM' }, { id: 't_m2', name: '172 Diamonds', price: 43000, desc: 'Bonus Ekstra +16 DM' }],
                    grinder: [{ id: 't_m3', name: '706 Diamonds', price: 165000, desc: 'Termasuk Akses Starlight Pass' }, { id: 't_m4', name: '1050 Diamonds', price: 242000, desc: 'Paket Elite Pass Kompetitif' }],
                    highroller: [{ id: 't_m5', name: '4000 Diamonds', price: 950000, desc: 'Bonus Vault Collector Skin' }, { id: 't_m6', name: '9288 Diamonds', price: 2100000, desc: 'Paket Alokasi Turnamen Sultan' }]
                },
                'valorant': {
                    casual: [{ id: 't_v1', name: '475 Points', price: 52000, desc: 'Instan Masuk Akun' }, { id: 't_v2', name: '1000 Points', price: 109000, desc: 'Aset Minimalis Agen Baru' }],
                    grinder: [{ id: 't_v3', name: '2050 Points', price: 219000, desc: 'Cukup Untuk Aktifkan Battlepass' }],
                    highroller: [{ id: 't_v4', name: '5350 Points', price: 549000, desc: 'Skin Senjata Klasik Bundling' }, { id: 't_v5', name: '11000 Points', price: 1085000, desc: 'Paket Kolektor Melee Skin Upgrade' }]
                },
                'pubgm': {
                    casual: [{ id: 't_p1', name: '60 Unknown Cash', price: 15000, desc: '' }, { id: 't_p2', name: '325 Unknown Cash', price: 73000, desc: '' }],
                    grinder: [{ id: 't_p3', name: '1800 Unknown Cash', price: 370000, desc: 'Akses Royale Pass Aktif' }],
                    highroller: [{ id: 't_p4', name: '8100 Unknown Cash', price: 1450000, desc: 'Sultan Crate Opening Allocation' }]
                },
                'ff': {
                    casual: [{ id: 't_f1', name: '140 Diamonds', price: 22000, desc: '' }],
                    grinder: [{ id: 't_f2', name: '720 Diamonds', price: 110000, desc: 'Elite Pass Bundling' }],
                    highroller: [{ id: 't_f3', name: '7290 Diamonds', price: 1050000, desc: 'Koleksi Senjata Evolution Maksimal' }]
                }
            },
            accounts: {
                'mlbb': {
                    bronze: [{ id: 'a_m1', title: 'Smurf Account Starter', specs: 'Level 23 | 12 Heroes Unlocked | Winrate Tinggi 84%', price: 45000, img: 'https://placehold.co/300x200/151525/8b5cf6?text=Bronze+Asset' }],
                    silver: [{ id: 'a_m2', title: 'Mythical Glory Core', specs: 'Rank Mythic | 58 Heroes | 35 Premium Skins (Epic & Limited Lineup)', price: 320000, img: 'https://placehold.co/300x200/151525/94a3b8?text=Silver+Vanguard' }],
                    golden: [{ id: 'a_m3', title: 'Immortal Whale Account', specs: 'Rank Mythic Immortal 120 Stars | Full Heroes Maxed | 320 Skins (Legend, Collector, Prime FullSet)', price: 5400000, img: 'https://placehold.co/300x200/151525/fbbf24?text=Golden+Paragon' }]
                },
                'valorant': {
                    bronze: [{ id: 'a_v1', title: 'Competitive Ready Smurf', specs: 'Level 25 | Selesai Penempatan Rank | Siap Ranked Match', price: 75000, img: 'https://placehold.co/300x200/151525/8b5cf6?text=Bronze+Asset' }],
                    silver: [{ id: 'a_v2', title: 'Diamond Tier Main', specs: 'Rank Diamond 2 | Agen Terbuka Semua | Skin Vandal Reaver & Phantom Oni Full Efek', price: 480000, img: 'https://placehold.co/300x200/151525/94a3b8?text=Silver+Vanguard' }],
                    golden: [{ id: 'a_v3', title: 'Radiant Stack Absolute Account', specs: 'Rank Radiant Mantan Pro Client | 62 Premium Skin Senjata | Champions Knife & Kuronami Bundle Upgrade', price: 8900000, img: 'https://placehold.co/300x200/151525/fbbf24?text=Golden+Paragon' }]
                },
                'pubgm': {
                    bronze: [], silver: [],
                    golden: [{ id: 'a_p1', title: 'God Tier Conqueror', specs: 'Mantan Rank Conqueror Season Lama | M416 Glacier Max Level Efek | Set Baju Langka Mumi & X-Suit', price: 12500000, img: 'https://placehold.co/300x200/151525/fbbf24?text=Golden+Paragon' }]
                },
                'ff': { bronze: [], silver: [], golden: [] }
            }
        };

        const formatRp = (num) => {
            return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', maximumFractionDigits: 0 }).format(num);
        };
        const formatNumber = (num) => {
            return new Intl.NumberFormat('id-ID').format(num);
        };

        class NexusApp {
            constructor() {
                this.currentView = 'home';
                this.currentGame = null;
                this.cart = [];
                
                // Variabel simulasi statistik
                this.stats = {
                    visitors: 142580,
                    views: 342,
                    accounts: 18534
                };
                
                this.init();
            }

            init() {
                this.renderHomeGames();
                this.populateMarketplaceFilters();
                this.initAnalyticsSimulation();
                
                const savedCart = localStorage.getItem('nexusCart');
                if (savedCart) {
                    this.cart = JSON.parse(savedCart);
                    this.updateCartBadge();
                }
                
                // Load saved accounts stat if exists
                const savedAccounts = localStorage.getItem('nexusAccounts');
                if(savedAccounts) this.stats.accounts = parseInt(savedAccounts);
                this.updateStatsUI();
            }
            
            // FITUR BARU: Simulasi Analitik Animasi
            initAnalyticsSimulation() {
                setInterval(() => {
                    // Randomizer: Simulasi penonton bertambah/berkurang sedikit demi sedikit
                    const viewChange = Math.floor(Math.random() * 5) - 2; 
                    this.stats.views = Math.max(120, this.stats.views + viewChange);
                    
                    // Simulasi pengunjung baru sesekali
                    if(Math.random() > 0.7) {
                        this.stats.visitors += Math.floor(Math.random() * 3) + 1;
                        this.animateStatElement('stat-visitors');
                    }
                    
                    this.updateStatsUI();
                }, 3500); // Update setiap 3.5 detik
            }
            
            updateStatsUI() {
                document.getElementById('stat-visitors').textContent = formatNumber(this.stats.visitors);
                document.getElementById('stat-views').textContent = formatNumber(this.stats.views);
                document.getElementById('stat-accounts').textContent = formatNumber(this.stats.accounts);
            }
            
            animateStatElement(id) {
                const el = document.getElementById(id);
                el.classList.remove('stat-update');
                void el.offsetWidth; // trigger reflow
                el.classList.add('stat-update');
            }

            // FITUR BARU: Fungsi Pendaftaran Akun
            registerAccount(e) {
                e.preventDefault();
                const username = document.getElementById('reg-username').value;
                
                // Update statistik akun (Simulasi)
                this.stats.accounts += 1;
                localStorage.setItem('nexusAccounts', this.stats.accounts);
                this.updateStatsUI();
                
                // Reset form
                e.target.reset();
                
                // Notifikasi sukses dan kembali ke home
                this.showAlert('Pendaftaran Berhasil!', `Selamat datang di Nexus, ${username}. Forge ID Anda telah aktif dan tersinkronisasi.`, 'fa-user-check', 'text-green-400');
                this.navigate('home');
            }

            navigate(viewId, gameId = null) {
                document.querySelectorAll('.view-section').forEach(el => {
                    el.classList.remove('active');
                    el.style.display = 'none';
                });

                const targetEl = document.getElementById(`view-${viewId}`);
                if(targetEl) {
                    targetEl.style.display = 'block';
                    void targetEl.offsetWidth; 
                    targetEl.classList.add('active');
                }

                window.scrollTo({ top: 0, behavior: 'smooth' });
                this.currentView = viewId;

                if (viewId === 'game-detail' && gameId) {
                    this.currentGame = gameId;
                    this.renderGameDetail(gameId);
                } else if (viewId === 'marketplace') {
                    const filterVal = gameId || 'all';
                    document.getElementById('marketplace-game-filter').value = filterVal;
                    this.filterMarketplace(filterVal);
                }
            }

            navigateToMarketplaceForCurrentGame() {
                if (this.currentGame) {
                    this.navigate('marketplace', this.currentGame);
                }
            }

            renderHomeGames() {
                const grid = document.getElementById('game-directory-grid');
                grid.innerHTML = database.games.map(game => `
                    <div onclick="app.navigate('game-detail', '${game.id}')" class="glass-panel border-nexus-border rounded-xl overflow-hidden cursor-pointer neon-border group relative">
                        <div class="h-48 overflow-hidden relative">
                            <div class="absolute inset-0 bg-gradient-to-t from-nexus-panel to-transparent z-10"></div>
                            <img src="${game.image}" alt="${game.name}" class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-500">
                        </div>
                        <div class="p-5 relative z-20 -mt-10">
                            <div class="w-12 h-12 bg-nexus-dark border border-nexus-border rounded-lg flex items-center justify-center mb-3 shadow-lg">
                                <i class="${game.icon} text-xl text-nexus-blue"></i>
                            </div>
                            <h4 class="text-xl font-bold text-white font-display">${game.name}</h4>
                            <p class="text-nexus-textMut text-sm">${game.developer}</p>
                        </div>
                    </div>
                `).join('');
            }

            renderGameDetail(gameId) {
                const game = database.games.find(g => g.id === gameId);
                if (!game) return;

                document.getElementById('game-detail-header').innerHTML = `
                    <div class="absolute inset-0 z-0">
                        <img src="${game.bg}" alt="Background ${game.name}" class="w-full h-full object-cover opacity-10">
                        <div class="absolute inset-0 bg-gradient-to-r from-nexus-panel via-nexus-panel/90 to-transparent"></div>
                    </div>
                    <div class="relative z-10 w-24 h-32 rounded-lg overflow-hidden border border-nexus-border shadow-[0_0_15px_rgba(139,92,246,0.2)] shrink-0">
                        <img src="${game.image}" alt="${game.name}" class="w-full h-full object-cover">
                    </div>
                    <div class="relative z-10 flex-grow">
                        <span class="bg-nexus-purple/20 text-nexus-purple text-xs font-bold px-2 py-1 rounded-md uppercase tracking-wide border border-nexus-purple/30">${game.type}</span>
                        <h2 class="text-3xl md:text-5xl font-display font-bold text-white mt-2 tracking-tight">${game.name}</h2>
                        <p class="text-nexus-textMut mt-1 flex items-center"><i class="fas fa-shield-alt text-nexus-blue mr-2 text-xs"></i> Portal Kategori Ketat & Terverifikasi Aman</p>
                    </div>
                `;

                const topups = database.topups[gameId] || { casual:[], grinder:[], highroller:[] };
                const buildTierHTML = (tierName, badgeStyle, desc, items) => `
                    <div class="mb-8">
                        <div class="flex items-center mb-4">
                            <div class="${badgeStyle} text-xs font-bold px-3 py-1.5 rounded-md uppercase tracking-wider mr-4 shadow-md border">
                                ${tierName}
                            </div>
                            <div class="h-[1px] flex-grow bg-gradient-to-r from-nexus-border to-transparent"></div>
                        </div>
                        <p class="text-nexus-textMut text-sm mb-4">${desc}</p>
                        ${items.length === 0 ? '<p class="text-gray-600 italic text-sm pl-2">Katalog produk belum diisi untuk tier ini.</p>' : `
                            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4">
                                ${items.map(item => `
                                    <div onclick="app.addToCart({ id: '${item.id}', name: '${item.name}', price: ${item.price}, type: 'Top-Up', game: '${game.name}' })" class="glass-panel border-nexus-border hover:border-nexus-blue rounded-xl p-4 cursor-pointer transition-all duration-300 hover:bg-white/5 relative group overflow-hidden">
                                        <h5 class="text-white font-bold text-sm md:text-base">${item.name}</h5>
                                        ${item.desc ? `<p class="text-[11px] text-nexus-purple mt-1 line-clamp-1">${item.desc}</p>` : ''}
                                        <div class="mt-4 flex justify-between items-end">
                                            <span class="text-nexus-blue font-bold text-sm">${formatRp(item.price)}</span>
                                            <i class="fas fa-plus-circle text-gray-500 group-hover:text-nexus-blue transition-colors"></i>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        `}
                    </div>
                `;

                const container = document.getElementById('topup-tiers-container');
                container.innerHTML = `
                    ${buildTierHTML('Casual Tier (Paket Pemula)', 'bg-gray-800 text-gray-300 border-gray-600', 'Nominal hemat dan kecil terjangkau untuk amunisi darurat harian.', topups.casual)}
                    ${buildTierHTML('Grinder Tier (Paket Pro)', 'bg-nexus-purple/20 text-nexus-purple border-nexus-purple/40', 'Nominal menengah paling populer untuk alokasi event bulanan atau seasonal pass.', topups.grinder)}
                    ${buildTierHTML('High Roller Tier (Paket Sultan)', 'bg-yellow-500/10 text-yellow-500 border-yellow-500/40 shadow-[0_0_10px_rgba(234,179,8,0.1)]', 'Nominal maksimal paling mewah khusus untuk pemain yang mengejar kepuasan mutlak.', topups.highroller)}
                `;
            }

            populateMarketplaceFilters() {
                const select = document.getElementById('marketplace-game-filter');
                database.games.forEach(g => {
                    select.innerHTML += `<option value="${g.id}" class="bg-nexus-panel">${g.name}</option>`;
                });
            }

            filterMarketplace(gameId) {
                const container = document.getElementById('marketplace-container');
                container.innerHTML = ''; 

                let targetGames = gameId === 'all' ? database.games.map(g => g.id) : [gameId];

                targetGames.forEach(id => {
                    const accData = database.accounts[id];
                    const gameInfo = database.games.find(g => g.id === id);
                    if (!accData || !gameInfo) return;

                    const buildCasteHTML = (casteName, ui, items) => {
                        if(!items || items.length === 0) return '';
                        return `
                            <div class="mb-8">
                                <h4 class="text-lg font-display font-bold ${ui.textColor} mb-4 flex items-center">
                                    <i class="fas ${ui.icon} mr-2"></i> ${casteName}
                                </h4>
                                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                                    ${items.map(item => `
                                        <div class="glass-panel border-nexus-border rounded-xl overflow-hidden group hover:border-${ui.borderHover} transition-colors flex flex-col h-full">
                                            <div class="h-40 overflow-hidden relative bg-nexus-dark">
                                                <img src="${item.img}" alt="${item.title}" class="w-full h-full object-cover opacity-80 group-hover:scale-102 transition-transform duration-500">
                                                <span class="absolute top-3 right-3 bg-nexus-dark/80 backdrop-blur-md px-2.5 py-1 rounded text-[11px] font-bold text-white border border-white/10">
                                                    ${gameInfo.name}
                                                </span>
                                            </div>
                                            <div class="p-5 flex flex-col flex-grow">
                                                <h5 class="text-white font-bold text-base mb-1 truncate">${item.title}</h5>
                                                <p class="text-xs text-nexus-textMut mb-4 line-clamp-2">${item.specs}</p>
                                                <div class="flex items-center justify-between mt-auto pt-2 border-t border-nexus-border/40">
                                                    <span class="font-display font-bold text-lg ${ui.priceColor}">${formatRp(item.price)}</span>
                                                    <button onclick="app.addToCart({ id: '${item.id}', name: '${item.title}', price: ${item.price}, type: 'Account', game: '${gameInfo.name}' })" class="${ui.btnBg} hover:opacity-90 text-white px-4 py-2 rounded-lg text-xs font-bold transition-all cursor-pointer">
                                                        Secure Asset
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    `).join('')}
                                </div>
                            </div>
                        `;
                    };

                    const sectionHtml = `
                        <div class="bg-nexus-panel/30 rounded-2xl p-6 border border-nexus-border">
                            <h3 class="text-xl font-bold font-display text-white mb-6 border-b border-nexus-border pb-4 flex items-center"><i class="fas fa-gamepad mr-2 text-nexus-blue"></i> DIREKTORI ${gameInfo.name.toUpperCase()}</h3>
                            ${buildCasteHTML('Bronze Asset (Starter)', { textColor: 'text-amber-600', icon: 'fa-shield-alt', borderHover: 'amber-700', priceColor: 'text-amber-500', btnBg: 'bg-amber-800' }, accData.bronze)}
                            ${buildCasteHTML('Silver Vanguard (Mid-Tier)', { textColor: 'text-slate-300', icon: 'fa-award', borderHover: 'slate-400', priceColor: 'text-slate-300', btnBg: 'bg-slate-600' }, accData.silver)}
                            ${buildCasteHTML('Golden Paragon (Premium Sultan)', { textColor: 'text-yellow-400', icon: 'fa-crown', borderHover: 'yellow-400', priceColor: 'text-yellow-400', btnBg: 'bg-gradient-to-r from-yellow-600 to-amber-500' }, accData.golden)}
                        </div>
                    `;
                    container.innerHTML += sectionHtml;
                });

                if (container.innerHTML === '') {
                    container.innerHTML = `<div class="text-center py-20 text-gray-600"><i class="fas fa-box-open text-4xl mb-4"></i><p class="text-sm">Belum ada listing akun game untuk kategori terpilh.</p></div>`;
                }
            }

            toggleCart() {
                const modal = document.getElementById('cart-modal');
                const sidebar = document.getElementById('cart-sidebar');
                
                if (modal.classList.contains('hidden')) {
                    modal.classList.remove('hidden');
                    this.renderCartItems();
                    setTimeout(() => sidebar.classList.remove('translate-x-full'), 10);
                } else {
                    sidebar.classList.add('translate-x-full');
                    setTimeout(() => modal.classList.add('hidden'), 300);
                }
            }

            addToCart(item) {
                this.cart.push(item);
                localStorage.setItem('nexusCart', JSON.stringify(this.cart));
                this.updateCartBadge();
                this.showToast(`<b>${item.name}</b> berhasil dikunci ke keranjang.`);
            }

            removeFromCart(idx) {
                this.cart.splice(idx, 1);
                localStorage.setItem('nexusCart', JSON.stringify(this.cart));
                this.updateCartBadge();
                this.renderCartItems();
            }

            updateCartBadge() {
                const badge = document.getElementById('cart-badge');
                if (this.cart.length > 0) {
                    badge.textContent = this.cart.length;
                    badge.classList.remove('hidden');
                } else {
                    badge.classList.add('hidden');
                }
            }

            renderCartItems() {
                const container = document.getElementById('cart-items');
                const totalEl = document.getElementById('cart-total');
                let subtotal = 0;

                if (this.cart.length === 0) {
                    container.innerHTML = `<div class="h-full flex flex-col items-center justify-center text-gray-600 py-12"><i class="fas fa-shopping-basket text-4xl mb-3"></i><p class="text-sm">Keranjang taktis kosong.</p></div>`;
                } else {
                    container.innerHTML = this.cart.map((item, idx) => {
                        subtotal += item.price;
                        return `
                            <div class="bg-nexus-dark p-3 rounded-lg border border-nexus-border flex justify-between items-center">
                                <div>
                                    <span class="text-[9px] bg-nexus-purple/20 text-nexus-purple px-1.5 py-0.5 rounded font-bold uppercase tracking-wider">${item.type}</span>
                                    <h5 class="text-white font-medium text-sm mt-1">${item.name}</h5>
                                    <span class="text-nexus-blue font-bold text-xs mt-0.5 block">${formatRp(item.price)}</span>
                                </div>
                                <button onclick="app.removeFromCart(${idx})" class="text-gray-500 hover:text-red-400 transition-colors bg-transparent border-none p-2 cursor-pointer">
                                    <i class="fas fa-trash-alt text-sm"></i>
                                </button>
                            </div>
                        `;
                    }).join('');
                }
                totalEl.textContent = formatRp(subtotal);
            }

            checkout() {
                if(this.cart.length === 0) {
                    this.showAlert('Keranjang Kosong', 'Tambahkan voucher, diamond, atau akun ke keranjang belanja Anda terlebih dahulu.', 'fa-shopping-cart', 'text-amber-500');
                    return;
                }
                this.toggleCart();
                this.showAlert('Checkout Berhasil', 'Sistem mengalihkan Anda secara aman menuju Invoice Payment Gateway manual.', 'fa-lock', 'text-nexus-blue');
                this.cart = [];
                localStorage.removeItem('nexusCart');
                this.updateCartBadge();
            }

            submitComplaint(e) {
                e.preventDefault();
                this.showAlert('Laporan Masuk', 'Pusat bantuan berhasil mencatat keluhan Anda. Invoice terkait akan diverifikasi secara manual oleh administrator dalam 1x24 jam.', 'fa-check-circle', 'text-green-400');
                e.target.reset();
            }

            showToast(msg) {
                const container = document.getElementById('toast-container');
                const toast = document.createElement('div');
                toast.className = 'glass-panel border-l-4 border-nexus-blue p-4 rounded-r-lg shadow-lg flex items-center transform translate-x-full transition-transform duration-300 pointer-events-auto';
                toast.innerHTML = `
                    <div class="text-nexus-blue mr-3"><i class="fas fa-check-circle"></i></div>
                    <div class="text-xs text-white tracking-wide">${msg}</div>
                `;
                container.appendChild(toast);
                requestAnimationFrame(() => toast.classList.remove('translate-x-full'));
                setTimeout(() => {
                    toast.classList.add('translate-x-full');
                    toast.addEventListener('transitionend', () => toast.remove());
                }, 3000);
            }

            showAlert(title, msg, icon = 'fa-info-circle', color = 'text-nexus-blue') {
                const modal = document.getElementById('custom-alert');
                const box = document.getElementById('custom-alert-box');
                document.getElementById('alert-title').textContent = title;
                document.getElementById('alert-message').textContent = msg;
                document.getElementById('alert-icon').className = `text-4xl mb-4 ${color}`;
                document.getElementById('alert-icon').innerHTML = `<i class="fas ${icon}"></i>`;
                modal.classList.remove('hidden');
                setTimeout(() => box.classList.remove('scale-95', 'opacity-0'), 10);
            }

            closeAlert() {
                const modal = document.getElementById('custom-alert');
                const box = document.getElementById('custom-alert-box');
                box.classList.add('scale-95', 'opacity-0');
                setTimeout(() => modal.classList.add('hidden'), 300);
            }
        }

        let app;
        window.onload = () => { app = new NexusApp(); };
    </script>
</body>
</html>
