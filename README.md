# WorkHub-Official
WorkHub Official: A next-generation hyperlocal service marketplace &amp; micro-earning platform. Empowering users with seamless switching between Client and Provider modes, integrated NID verification, real-time location-based job filtering, and an advanced chat system.
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreelanceBD - সেরা ফ্রিল্যান্স প্ল্যাটফর্ম</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background: #f5f7fa; }
        .hidden { display: none !important; }
        
        /* Auth Pages */
        .auth-container { min-height: 100vh; display: flex; align-items: center; justify-content: center; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .auth-card { background: white; padding: 3rem; border-radius: 20px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); width: 100%; max-width: 400px; }
        .auth-title { text-align: center; color: #333; margin-bottom: 2rem; font-size: 2rem; }
        .form-group { margin-bottom: 1.5rem; }
        .form-group input { width: 100%; padding: 15px; border: 2px solid #e9ecef; border-radius: 10px; font-size: 1rem; transition: 0.3s; }
        .form-group input:focus { outline: none; border-color: #667eea; }
        .btn-primary { width: 100%; background: #667eea; color: white; padding: 15px; border: none; border-radius: 10px; font-size: 1.1rem; cursor: pointer; transition: 0.3s; }
        .btn-primary:hover { background: #5a67d8; }
        .toggle-link { text-align: center; margin-top: 1rem; color: #667eea; cursor: pointer; text-decoration: underline; }
        
        /* Dashboard */
        .dashboard { padding: 20px; max-width: 1400px; margin: 0 auto; }
        .header { display: flex; justify-content: space-between; align-items: center; background: white; padding: 1rem 2rem; border-radius: 15px; margin-bottom: 2rem; box-shadow: 0 5px 15px rgba(0,0,0,0.08); }
        .mode-switch { background: #ff6b6b; color: white; border: none; padding: 10px 20px; border-radius: 25px; font-weight: bold; cursor: pointer; transition: 0.3s; }
        .mode-switch.active { background: #51cf66; }
        
        /* Location Filter */
        .location-filter { background: white; padding: 1.5rem 2rem; border-radius: 15px; margin-bottom: 2rem; box-shadow: 0 5px 15px rgba(0,0,0,0.08); }
        .filter-row { display: flex; gap: 1rem; flex-wrap: wrap; }
        .filter-select { padding: 12px 15px; border: 2px solid #e9ecef; border-radius: 10px; font-size: 1rem; min-width: 150px; }
        
        /* Gigs List */
        .gigs-container { display: grid; grid-template-columns: repeat(auto-fill, minmax(350px, 1fr)); gap: 1.5rem; }
        .gig-card { background: white; border-radius: 15px; padding: 1.5rem; box-shadow: 0 10px 25px rgba(0,0,0,0.1); transition: 0.3s; cursor: pointer; }
        .gig-card:hover { transform: translateY(-5px); box-shadow: 0 15px 35px rgba(0,0,0,0.15); }
        .gig-title { font-size: 1.3rem; font-weight: bold; color: #333; margin-bottom: 0.5rem; }
        .gig-price { font-size: 1.5rem; color: #51cf66; font-weight: bold; margin-bottom: 0.5rem; }
        .gig-location { color: #666; margin-bottom: 1rem; }
        .gig-actions { display: flex; gap: 0.5rem; }
        .btn-apply { background: #51cf66; color: white; border: none; padding: 8px 15px; border-radius: 20px; cursor: pointer; font-size: 0.9rem; }
        
        /* Sidebar */
        .sidebar { position: fixed; right: 20px; top: 100px; background: white; padding: 1.5rem; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); width: 300px; z-index: 100; }
        .balance-card { background: linear-gradient(135deg, #51cf66, #40c057); color: white; padding: 2rem; border-radius: 15px; text-align: center; margin-bottom: 1rem; }
        .balance-amount { font-size: 2.5rem; font-weight: bold; margin-bottom: 0.5rem; }
        .btn-withdraw { background: white; color: #51cf66; border: none; padding: 12px 25px; border-radius: 25px; font-weight: bold; cursor: pointer; width: 100%; margin-top: 1rem; }
        .menu-item { display: flex; align-items: center; padding: 1rem; border-radius: 10px; cursor: pointer; transition: 0.3s; margin-bottom: 0.5rem; }
        .menu-item:hover { background: #f8f9fa; }
        .menu-icon { margin-right: 1rem; font-size: 1.2rem; }
        
        /* Chat */
        .chat-window { position: fixed; bottom: 20px; right: 20px; width: 350px; height: 500px; background: white; border-radius: 15px; box-shadow: 0 20px 40px rgba(0,0,0,0.2); display: none; flex-direction: column; }
        .chat-header { background: #667eea; color: white; padding: 1rem; border-radius: 15px 15px 0 0; }
        .chat-messages { flex: 1; padding: 1rem; overflow-y: auto; }
        .chat-input { padding: 1rem; border-top: 1px solid #e9ecef; }
        .chat-input input { width: 100%; padding: 10px; border: 1px solid #e9ecef; border-radius: 20px; }
        
        @media (max-width: 768px) { .sidebar { right: -320px; transition: 0.3s; } .sidebar.open { right: 20px; } }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="loginPage" class="auth-container">
        <div class="auth-card">
            <h2 class="auth-title"><i class="fas fa-sign-in-alt"></i> লগইন</h2>
            <form id="loginForm">
                <div class="form-group">
                    <input type="text" id="loginEmail" placeholder="ইমেইল / মোবাইল" required>
                </div>
                <div class="form-group">
                    <input type="password" id="loginPassword" placeholder="পাসওয়ার্ড" required>
                </div>
                <button type="submit" class="btn-primary">লগইন করুন</button>
            </form>
            <div class="toggle-link" onclick="showSignup()">নতুন অ্যাকাউন্ট? সাইনআপ করুন</div>
        </div>
    </div>

    <!-- Signup Page -->
    <div id="signupPage" class="auth-container hidden">
        <div class="auth-card">
            <h2 class="auth-title"><i class="fas fa-user-plus"></i> সাইনআপ</h2>
            <form id="signupForm">
                <div class="form-group">
                    <input type="text" id="fullName" placeholder="পূর্ণ নাম (NID অনুযায়ী)" required>
                </div>
                <div class="form-group">
                    <input type="tel" id="phone" placeholder="মোবাইল নম্বর" required>
                </div>
                <div class="form-group">
                    <input type="email" id="signupEmail" placeholder="জিমেইল" required>
                </div>
                <div class="form-group">
                    <input type="text" id="nid" placeholder="NID নম্বর" required>
                </div>
                <div class="form-group">
                    <input type="password" id="signupPassword" placeholder="পাসওয়ার্ড" required>
                </div>
                <button type="submit" class="btn-primary">অ্যাকাউন্ট তৈরি করুন</button>
            </form>
            <div class="toggle-link" onclick="showLogin()">ইতিমধ্যে অ্যাকাউন্ট আছে? লগইন করুন</div>
        </div>
    </div>

    <!-- Dashboard -->
    <div id="dashboard" class="hidden">
        <div class="dashboard">
            <!-- Header -->
            <div class="header">
                <h1><i class="fas fa-briefcase"></i> FreelanceBD Dashboard</h1>
                <button class="mode-switch active" id="modeSwitch" onclick="toggleMode()">
                    <i class="fas fa-users"></i> ক্লায়েন্ট মোড
                </button>
            </div>

            <!-- Location Filter -->
            <div class="location-filter">
                <div class="filter-row">
                    <select class="filter-select" id="division">
                        <option>বিভাগ সিলেক্ট করুন</option>
                        <option>ঢাকা</option>
                        <option>চট্টগ্রাম</option>
                        <option>রাজশাহী</option>
                    </select>
                    <select class="filter-select" id="district">
                        <option>জেলা সিলেক্ট করুন</option>
                    </select>
                    <select class="filter-select" id="upazila">
                        <option>উপজেলা সিলেক্ট করুন</option>
                    </select>
                    <select class="filter-select" id="union">
                        <option>গ্রাম/ইউনিয়ন</option>
                    </select>
                </div>
            </div>

            <!-- Gigs List -->
            <div class="gigs-container" id="gigsList">
                <!-- Gigs will load here -->
            </div>
        </div>

        <!-- Sidebar (Account Dashboard) -->
        <div class="sidebar" id="sidebar">
            <div class="balance-card">
                <div class="balance-amount" id="mainBalance">৳ ০</div>
                <div>মোট ব্যালেন্স</div>
                <button class="btn-withdraw" onclick="withdraw()">Withdraw</button>
            </div>
            <div class="menu-item" onclick="showSection('deposit')">
                <i class="fas fa-plus-circle menu-icon"></i> Deposit
            </div>
            <div class="menu-item" onclick="showSection('history')">
                <i class="fas fa-history menu-icon"></i> Transaction History
            </div>
            <div class="menu-item" onclick="showSection('earnings')">
                <i class="fas fa-chart-line menu-icon"></i> Earnings
            </div>
            <div class="menu-item" onclick="showSection('profile')">
                <i class="fas fa-user menu-icon"></i> Profile Settings
            </div>
            <div class="menu-item" onclick="logout()">
                <i class="fas fa-sign-out-alt menu-icon" style="color: #ff6b6b;"></i> Logout
            </div>
        </div>

        <!-- Chat Window -->
        <div class="chat-window" id="chatWindow">
            <div class="chat-header">
                <i class="fas fa-comments"></i> চ্যাট
                <button onclick="closeChat()" style="float: right; background: none; border: none; color: white; font-size: 1.2rem;">×</button>
            </div>
            <div class="chat-messages" id="chatMessages"></div>
            <div class="chat-input">
                <input type="text" placeholder="টাইপ করুন..." onkeypress="sendMessage(event)">
            </div>
        </div>
    </div>

    <script>
        // Demo Users (Real app এ Firebase Auth ব্যবহার করবে)
        const demoUsers = {
            'user@example.com': { password: '123456', balance: 12500, name: 'রকি আহমেদ', nid: '1234567890' }
        };

        let currentUser = null;
        let currentMode = 'client'; // 'client' or 'provider'

        // Show/Hide Pages
        function showLogin() {
            document.getElementById('loginPage').classList.remove('hidden');
            document.getElementById('signupPage').classList.add('hidden');
            document.getElementById('dashboard').classList.add('hidden');
        }

        function showSignup() {
            document.getElementById('signupPage').classList.remove('hidden');
            document.getElementById('loginPage').classList.add('hidden');
            document.getElementById('dashboard').classList.add('hidden');
        }

        // Login
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            if (demoUsers[email] && demoUsers[email].password === password) {
                currentUser = demoUsers[email];
                showDashboard();
            } else {
                alert('ভুল ইমেইল বা পাসওয়ার্ড!');
            }
        });

        // Signup
        document.getElementById('signupForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = document.getElementById('signupEmail').value;
            if (demoUsers[email]) {
                alert('এই ইমেইল ইতিমধ্যে রেজিস্টার্ড!');
                return;
            }
            demoUsers[email] = {
                password: document.getElementById('signupPassword').value,
                balance: 0,
                name: document.getElementById('fullName').value,
                phone: document.getElementById('phone').value,
                nid: document.getElementById('nid').value
            };
            alert('অ্যাকাউন্ট তৈরি হয়েছে! লগইন করুন।');
            showLogin();
        });

        function showDashboard() {
            document.getElementById('loginPage').classList.add('hidden');
            document.getElementById('signupPage').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('mainBalance').textContent = `৳ ${currentUser.balance}`;
            loadGigs();
        }

        // Mode Switch
        function toggleMode() {
            const switchBtn = document.getElementById('modeSwitch');
            currentMode = currentMode === 'client' ? 'provider' : 'client';
            switchBtn.innerHTML = currentMode === 'client' ? 
                '<i class="fas fa-users"></i> ক্লায়েন্ট মোড' : 
                '<i class="fas fa-briefcase"></i> প্রোভাইডার মোড';
            switchBtn.classList.toggle('active');
            loadGigs();
        }

        // Load Gigs (Demo Data)
        function loadGigs() {
            const gigsList = document.getElementById('gigsList');
            const demoGigs = [
                { id: 1, title: 'ওয়েবসাইট তৈরি করব', price: 5000, location: 'ঢাকা - মিরপুর', provider: 'রহিম' },
                { id: 2, title: 'লোগো ডিজাইন', price: 1000, location: 'চট্টগ্রাম - পাহাড়পুর', provider: 'করিম' },
                { id: 3, title: 'ভিডিও এডিটিং', price: 2000, location: 'ঢাকা - ধানমন্ডি', provider: 'জহির' },
                { id: 4, title: 'Facebook Marketing', price: 3000, location: 'রাজশাহী', provider: 'সালমান' }
            ];

            gigsList.innerHTML = demoGigs.map(gig => `
                <div class="gig-card" onclick="openChat(${gig.id})">
                    <div class="gig-title">${gig.title}</div>
                    <div class="gig-price">৳ ${gig.price}</div>
                    <div class="gig-location"><i class="fas fa-map-marker-alt"></i> ${gig.location}</div>
