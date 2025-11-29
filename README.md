# reabitt-tokrn-mining
<!DOCTYPE html>
<html lang="bn">
<head>
<script src="https://telegram.org/js/telegram-web-app.js"></script>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rabbit Coin Miner - Official</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%);
            /* নতুন ব্যাকগ্রাউন্ড ইমেজ যোগ করা হয়েছে */
            background-image: url('rabbit-mining-bg.png'); /* আপনার দেওয়া ফটোটি 'rabbit-mining-bg.png' নামে সেভ করে একই ফোল্ডারে রাখুন */
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
            min-height: 100vh; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            padding: 20px; 
        }
        .app-container { background: rgba(255, 255, 255, 0.95); /* অ্যাপ কনটেইনারকে সামান্য ট্রান্সপারেন্ট করে ইমেজ দেখা যাবে */ border-radius: 30px; box-shadow: 0 20px 60px rgba(0,0,0,0.3); max-width: 400px; width: 100%; overflow: hidden; animation: slideUp 0.5s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        
        /* Registration Styles */
        .registration-container { padding: 40px 30px; text-align: center; min-height: 500px; display: flex; flex-direction: column; justify-content: center; background: linear-gradient(135deg, rgba(255, 159, 243, 0.9) 0%, rgba(254, 202, 87, 0.9) 100%); /* ট্রান্সপারেন্ট করে ইমেজ দেখা যাবে */ }
        .registration-container h2 { color: white; margin-bottom: 20px; font-size: 28px; text-shadow: 2px 2px 4px rgba(0,0,0,0.2); }
        .rabbit-logo { font-size: 80px; margin-bottom: 20px; animation: bounce 2s infinite; }
        @keyframes bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
        .telegram-section { background: rgba(255,255,255,0.95); border-radius: 20px; padding: 25px; margin: 20px 0; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        .telegram-section h3 { color: #0088cc; margin-bottom: 15px; font-size: 20px; }
        .telegram-button { display: inline-flex; align-items: center; gap: 10px; background: #0088cc; color: white; padding: 15px 30px; border-radius: 25px; text-decoration: none; font-weight: bold; font-size: 16px; transition: all 0.3s ease; margin: 15px 0; }
        .telegram-button:hover { transform: scale(1.05); box-shadow: 0 10px 25px rgba(0,136,204,0.3); }
        .status-check { background: #f8f9fa; border-radius: 15px; padding: 15px; margin: 15px 0; }
        .status-indicator { display: flex; align-items: center; gap: 10px; justify-content: center; margin: 10px 0; }
        .status-dot { width: 12px; height: 12px; border-radius: 50%; background: #dc3545; animation: pulse 2s infinite; }
        .status-dot.verified { background: #28a745; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(40, 167, 69, 0.7); } 70% { box-shadow: 0 0 0 10px rgba(40, 167, 69, 0); } 100% { box-shadow: 0 0 0 0 rgba(40, 167, 69, 0); } }
        .verify-button { background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%); color: white; border: none; padding: 12px 25px; border-radius: 20px; font-weight: bold; cursor: pointer; transition: all 0.3s ease; outline: none; }
        .verify-button:hover:not(:disabled) { transform: scale(1.05); box-shadow: 0 5px 15px rgba(255,107,107,0.3); }
        .verify-button:disabled { opacity: 0.5; cursor: not-allowed; }
        
        .header { background: linear-gradient(135deg, rgba(255, 107, 107, 0.9) 0%, rgba(254, 202, 87, 0.9) 100%); /* ট্রান্সপারেন্ট করে ইমেজ দেখা যাবে */ color: white; padding: 30px 20px; text-align: center; position: relative; overflow: hidden; }
        .header::before { content: ''; position: absolute; top: -50%; right: -50%; width: 200%; height: 200%; background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%); animation: rotate 20s linear infinite; }
        @keyframes rotate { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
        .header h1 { font-size: 32px; margin-bottom: 10px; display: flex; align-items: center; justify-content: center; gap: 10px; position: relative; z-index: 1; }
        .rabbit-coin { width: 50px; height: 50px; background: linear-gradient(135deg, #fff 0%, #f0f0f0 100%); border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 30px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); position: relative; }
        .rabbit-coin::after { content: '🐰'; position: absolute; font-size: 25px; }
        .balance-section { background: rgba(255,255,255,0.15); border-radius: 15px; padding: 20px; margin-top: 20px; backdrop-filter: blur(10px); position: relative; z-index: 1; }
        .balance-label { font-size: 14px; opacity: 0.9; margin-bottom: 5px; }
        .balance-amount { font-size: 36px; font-weight: bold; margin-bottom: 10px; text-shadow: 2px 2px 4px rgba(0,0,0,0.1); }
        .mining-rate { font-size: 14px; opacity: 0.9; }
        .main-content { padding: 30px 20px; }
        .mining-button-container { text-align: center; margin: 30px 0; }
        .mining-button { width: 200px; height: 200px; border-radius: 50%; background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%); border: none; color: white; font-size: 18px; font-weight: bold; cursor: pointer; position: relative; transition: all 0.3s ease; box-shadow: 0 10px 30px rgba(255,107,107,0.4); outline: none; }
        .mining-button:hover { transform: scale(1.05); box-shadow: 0 15px 40px rgba(255,107,107,0.5); }
        .mining-button.active { animation: rabbitPulse 2s infinite; background: linear-gradient(135deg, #ff9ff3 0%, #feca57 100%); }
        @keyframes rabbitPulse { 0% { box-shadow: 0 0 0 0 rgba(255,159,243,0.7); } 70% { box-shadow: 0 0 0 20px rgba(255,159,243,0); } 100% { box-shadow: 0 0 0 0 rgba(255,159,243,0); } }
        .button-text { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); text-align: center; }
        .timer { font-size: 24px; margin-top: 10px; }
        .stats-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; margin: 30px 0; }
        .stat-card { background: #f8f9fa; padding: 15px; border-radius: 15px; text-align: center; transition: transform 0.3s ease; border: 2px solid transparent; }
        .stat-card:hover { transform: translateY(-5px); border-color: #ff6b6b; }
        .stat-label { font-size: 12px; color: #666; margin-bottom: 5px; }
        .stat-value { font-size: 20px; font-weight: bold; color: #333; }

        /* Background Mining Status */
        .background-mining-status { background: linear-gradient(135deg, rgba(255, 159, 243, 0.9) 0%, rgba(254, 202, 87, 0.9) 100%); /* ট্রান্সপারেন্ট */ border-radius: 15px; padding: 15px; margin: 20px 0; color: white; text-align: center; }
        .background-mining-status h4 { margin-bottom: 10px; font-size: 16px; }
        .status-indicator { display: inline-flex; align-items: center; gap: 8px; font-size: 14px; }
        .status-dot { width: 8px; height: 8px; background: #28a745; border-radius: 50%; animation: blink 2s infinite; }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }

        /* Withdraw Section Styles */
        .withdraw-section { background: linear-gradient(135deg, rgba(40, 167, 69, 0.9) 0%, rgba(32, 201, 151, 0.9) 100%); /* ট্রান্সপারেন্ট */ border-radius: 15px; padding: 20px; margin: 20px 0; color: white; }
        .withdraw-header { text-align: center; margin-bottom: 20px; }
        .withdraw-header h3 { font-size: 20px; margin-bottom: 10px; }
        .withdraw-status { font-size: 14px; opacity: 0.9; }
        .countdown { background: rgba(255,255,255,0.2); padding: 8px 12px; border-radius: 20px; display: inline-block; margin-top: 5px; }
        .withdraw-form { display: none; }
        .withdraw-form.active { display: block; animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .payment-methods { display: flex; justify-content: space-around; margin-bottom: 20px; }
        .payment-method { display: flex; flex-direction: column; align-items: center; cursor: pointer; padding: 10px; border-radius: 10px; transition: all 0.3s ease; }
        .payment-method:hover { background: rgba(255,255,255,0.1); }
        .payment-method input[type="radio"] { display: none; }
        .payment-method input[type="radio"]:checked + .payment-icon { transform: scale(1.2); }
        .payment-icon { font-size: 24px; margin-bottom: 5px; transition: transform 0.3s ease; }
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; margin-bottom: 5px; font-size: 14px; }
        .form-group input { width: 100%; padding: 12px; border: none; border-radius: 8px; font-size: 14px; outline: none; }
        .withdraw-info { background: rgba(255,255,255,0.1); padding: 15px; border-radius: 10px; margin-bottom: 15px; }
        .info-row { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 13px; }
        .info-row:last-child { margin-bottom: 0; }
        .withdraw-button { width: 100%; padding: 15px; background: white; color: #28a745; border: none; border-radius: 10px; font-weight: bold; cursor: pointer; transition: all 0.3s ease; outline: none; }
        .withdraw-button:hover:not(:disabled) { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(0,0,0,0.2); }
        .withdraw-button:disabled { opacity: 0.5; cursor: not-allowed; }

        .daily-bonus { background: linear-gradient(135deg, rgba(255, 159, 243, 0.9) 0%, rgba(254, 202, 87, 0.9) 100%); /* ট্রান্সপারেন্ট */ border-radius: 15px; padding: 20px; margin: 20px 0; text-align: center; color: white; }
        .bonus-button { background: white; color: #ff6b6b; border: none; padding: 12px 30px; border-radius: 25px; font-weight: bold; cursor: pointer; margin-top: 10px; transition: all 0.3s ease; outline: none; }
        .bonus-button:hover:not(:disabled) { transform: scale(1.05); box-shadow: 0 5px 15px rgba(255,107,107,0.2); }
        .bonus-button:disabled { opacity: 0.5; cursor: not-allowed; }
        .referral-section { background: #f8f9fa; border-radius: 15px; padding: 20px; margin: 20px 0; }
        .referral-code { background: white; padding: 10px; border-radius: 10px; display: flex; justify-content: space-between; align-items: center; margin-top: 10px; }
        .copy-button { background: #ff6b6b; color: white; border: none; padding: 8px 15px; border-radius: 8px; cursor: pointer; font-size: 12px; transition: all 0.3s ease; outline: none; }
        .copy-button:hover { background: #ff5252; }
        .notification { position: fixed; top: 20px; right: 20px; background: #4caf50; color: white; padding: 15px 20px; border-radius: 10px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); display: none; animation: slideIn 0.3s ease-out; z-index: 1000; max-width: 300px; }
        @keyframes slideIn { from { transform: translateX(100%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
        .notification.show { display: block; }
        .footer { text-align: center; padding: 20px; background: #f8f9fa; font-size: 12px; color: #666; }
        .disclaimer { background: #fff3cd; border: 1px solid #ffc107; border-radius: 10px; padding: 15px; margin: 20px; font-size: 12px; color: #856404; }
        .release-info { background: #d1ecf1; border: 1px solid #bee5eb; border-radius: 10px; padding: 15px; margin: 20px; font-size: 12px; color: #0c5460; text-align: center; font-weight: bold; }
        .hidden { display: none !important; }
        @media (max-width: 480px) { .app-container { border-radius: 0; min-height: 100vh; } .mining-button { width: 150px; height: 150px; } }
        
        /* Rabbit Coin Animation */
        .coin-animation { position: fixed; font-size: 30px; pointer-events: none; z-index: 9999; animation: floatUp 3s ease-out forwards; }
        @keyframes floatUp { 0% { transform: translateY(100vh) rotate(0deg); opacity: 1; } 100% { transform: translateY(-100px) rotate(360deg); opacity: 0; } }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Registration Section -->
        <div class="registration-container" id="registrationSection">
            <div class="rabbit-logo">🐰</div>
            <h2>Rabbit Coin Miner</h2>
            <div class="telegram-section">
                <h3>📱 টেলিগ্রামে যোগ দিন</h3>
                <p style="margin-bottom: 15px; color: #666;">Rabbit Token অফিসিয়াল চ্যানেলে যোগ দিন</p>
                <a href="https://t.me/rabitttoken" target="_blank" class="telegram-button" id="telegramButton">
                    <span>✈️</span>
                    <span>চ্যানেলে যোগ দিন</span>
                </a>
                <div class="status-check">
                    <div class="status-indicator">
                        <span class="status-dot" id="statusDot"></span>
                        <span id="statusText">যাচাই করা হচ্ছে...</span>
                    </div>
                    <button class="verify-button" id="verifyButton" disabled>
                        যাচাই করুন
                    </button>
                </div>
            </div>
            <p style="margin-top: 20px; font-size: 12px; color: white; opacity: 0.8;">
                চ্যানেলে যোগ দেওয়ার পর যাচাই করুন
            </p>
        </div>

        <!-- Main App Section (Initially Hidden) -->
        <div id="mainAppSection" class="hidden">
            <div class="header">
                <h1><span class="rabbit-coin"></span> Rabbit Coin</h1>
                <div class="balance-section">
                    <div class="balance-label">আপনার ব্যালেন্স</div>
                    <div class="balance-amount" id="balance">0.0000 RBC</div>
                    <div class="mining-rate">মাইনিং রেট: <span id="miningRate">0.25</span> RBC/ঘন্টা</div>
                </div>
            </div>
            <div class="main-content">
                <!-- Background Mining Status -->
                <div class="background-mining-status">
                    <h4>🔄 ব্যাকগ্রাউন্ড মাইনিং</h4>
                    <div class="status-indicator">
                        <span class="status-dot"></span>
                        <span id="backgroundMiningStatus">অটো মাইনিং চলছে</span>
                    </div>
                </div>

                <div class="mining-button-container">
                    <button class="mining-button" id="miningButton">
                        <div class="button-text">
                            <div id="buttonStatus">মাইনিং শুরু করুন</div>
                            <div class="timer" id="timer"></div>
                        </div>
                    </button>
                </div>
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">আজকের মাইনিং</div>
                        <div class="stat-value" id="todayMining">0.0000 RBC</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">মোট মাইনিং</div>
                        <div class="stat-value" id="totalMining">0.0000 RBC</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">রেফারেল</div>
                        <div class="stat-value" id="referralCount">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">লেভেল</div>
                        <div class="stat-value" id="userLevel">বাচ্চা খরগোশ</div>
                    </div>
                </div>
                
                <!-- Withdraw Section -->
                <div class="withdraw-section">
                    <div class="withdraw-header">
                        <h3>💰 উইথড্র করুন</h3>
                        <div class="withdraw-status" id="withdrawStatus">
                            <div class="countdown" id="withdrawCountdown"></div>
                        </div>
                    </div>
                    
                    <div class="withdraw-form" id="withdrawForm">
                        <div class="payment-methods">
                            <label class="payment-method">
                                <input type="radio" name="payment" value="bkash" checked>
                                <span class="payment-icon">📱</span>
                                <span>বিকাশ</span>
                            </label>
                            <label class="payment-method">
                                <input type="radio" name="payment" value="nagad">
                                <span class="payment-icon">💵</span>
                                <span>নগদ</span>
                            </label>
                            <label class="payment-method">
                                <input type="radio" name="payment" value="rocket">
                                <span class="payment-icon">🚀</span>
                                <span>রকেট</span>
                            </label>
                        </div>
                        
                        <div class="form-group">
                            <label>মোবাইল নম্বর</label>
                            <input type="tel" id="phoneNumber" placeholder="01xxxxxxxxx" maxlength="11">
                        </div>
                        
                        <div class="form-group">
                            <label>পরিমাণ (RBC)</label>
                            <input type="number" id="withdrawAmount" placeholder="ন্যূনতম 10 RBC" min="10" step="0.0001">
                        </div>
                        
                        <div class="withdraw-info">
                            <div class="info-row">
                                <span>কনভার্শন রেট:</span>
                                <span>1 RBC = 100 টাকা</span>
                            </div>
                            <div class="info-row">
                                <span>পাবেন:</span>
                                <span id="withdrawAmountBDT">0 টাকা</span>
                            </div>
                            <div class="info-row">
                                <span>চার্জ:</span>
                                <span>2% (ন্যূনতম 5 টাকা)</span>
                            </div>
                        </div>
                        
                        <button class="withdraw-button" id="withdrawButton" disabled>
                            উইথড্র রিকোয়েস্ট
                        </button>
                    </div>
                </div>
                
                <div class="daily-bonus">
                    <div>🎁 ডেইলি বোনাস</div>
                    <div style="font-size: 12px; margin-top: 5px;">প্রতিদিন 0.1 RBC বোনাস পান</div>
                    <button class="bonus-button" id="bonusButton">ক্লেম করুন</button>
                </div>
                <div class="referral-section">
                    <div style="font-weight: bold; margin-bottom: 10px;">👥 রেফারেল কোড</div>
                    <div class="referral-code">
                        <span id="referralCode">RBC2024</span>
                        <button class="copy-button" id="copyButton">কপি করুন</button>
                    </div>
                </div>
                <div class="release-info">
                    🚀 <strong>অফিসিয়াল রিলিজ ডেট: ১০ নভেম্বর, ২০২৬</strong> 🚀
                </div>
                <div class="disclaimer">
                    <strong>Rabitt tokine
https://t.me/rabitttoken।⛏️🪙নতুন নতুন তথ্য আর আপডেট পেতে আমাদে চ্যানেলে জয়েন হয়ে পাশে থাকুন 🎉🎊
                </div>
            </div>
            <div class="footer">
                <p>© 2024 Rabbit Coin Miner | Educational Purpose Only</p>
            </div>
        </div>
    </div>
    <div class="notification" id="notification"></div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const RabbitCoinApp = {
                state: { 
                    isRegistered: false,
                    telegramJoined: false,
                    username: '',
                    registrationDate: null,
                    balance: 0, 
                    isMining: false, 
                    miningStartTime: null, 
                    lastActiveTime: null,
                    todayMining: 0, 
                    totalMining: 0, 
                    referralCount: 0, 
                    lastBonusClaim: null, 
                    miningRate: 0.25, 
                    level: 'বাচ্চা খরগোশ', 
                    referralCode: 'RBC2024',
                    withdrawHistory: [],
                    backgroundMiningEnabled: true
                },
                
                withdrawReleaseDate: new Date('2026-11-10T00:00:00'),
                conversionRate: 100, // 1 RBC = 100 BDT
                
                init: function() { 
                    this.loadState(); 
                    this.createFloatingCoins();
                    
                    if (this.state.isRegistered) {
                        this.showMainApp();
                        this.calculateBackgroundMining();
                        this.setupEventListeners(); 
                        this.updateUI(); 
                        this.startPeriodicChecks();
                        this.updateWithdrawStatus();
                        this.startBackgroundMining();
                    } else {
                        this.setupRegistrationListeners();
                        this.checkTelegramStatus();
                    }
                },
                
                createFloatingCoins: function() {
                    setInterval(() => {
                        if (Math.random() > 0.7) {
                            const coin = document.createElement('div');
                            coin.className = 'coin-animation';
                            coin.textContent = '🐰';
                            coin.style.left = Math.random() * window.innerWidth + 'px';
                            document.body.appendChild(coin);
                            
                            setTimeout(() => coin.remove(), 3000);
                        }
                    }, 5000);
                },
                
                setupRegistrationListeners: function() {
                    const telegramButton = document.getElementById('telegramButton');
                    const verifyButton = document.getElementById('verifyButton');
                    
                    telegramButton.addEventListener('click', () => {
                        setTimeout(() => {
                            this.state.telegramJoined = true;
                            this.updateTelegramStatus();
                            this.showNotification('✅ টেলিগ্রাম চ্যানেলে যোগ দেওয়া হয়েছে!');
                        }, 2000);
                    });
                    
                    verifyButton.addEventListener('click', () => {
                        this.handleTelegramVerification();
                    });
                },
                
                checkTelegramStatus: function() {
                    setInterval(() => {
                        this.updateTelegramStatus();
                    }, 2000);
                },
                
                updateTelegramStatus: function() {
                    const statusDot = document.getElementById('statusDot');
                    const statusText = document.getElementById('statusText');
                    const verifyButton = document.getElementById('verifyButton');
                    
                    if (this.state.telegramJoined) {
                        statusDot.classList.add('verified');
                        statusText.textContent = 'চ্যানেলে যোগ দেওয়া হয়েছে';
                        verifyButton.disabled = false;
                    } else {
                        statusDot.classList.remove('verified');
                        statusText.textContent = 'যাচাই করা হচ্ছে...';
                        verifyButton.disabled = true;
                    }
                },
                
                handleTelegramVerification: function() {
                    if (!this.state.telegramJoined) {
                        this.showNotification('❌ প্রথমে টেলিগ্রাম চ্যানেলে যোগ দিন!');
                        return;
                    }
                    
                    // Simulate verification process
                    this.showNotification('🔍 যাচাই করা হচ্ছে...');
                    
                    setTimeout(() => {
                        // Save registration data
                        this.state.isRegistered = true;
                        this.state.username = 'Rabbit Miner ' + Math.floor(Math.random() * 10000);
                        this.state.registrationDate = new Date().toISOString();
                        this.state.miningStartTime = Date.now();
                        this.state.lastActiveTime = Date.now();
                        
                        // Generate unique referral code
                        this.state.referralCode = 'RBC' + Math.random().toString(36).substr(2, 6).toUpperCase();
                        
                        this.saveState();
                        
                        // Show success notification
                        this.showNotification(`🎉 স্বাগতম! রেজিস্ট্রেশন সম্পন্ন হয়েছে!`);
                        
                        // Show main app
                        this.showMainApp();
                        this.setupEventListeners();
                        this.updateUI();
                        this.startPeriodicChecks();
                        this.updateWithdrawStatus();
                        this.startBackgroundMining();
                    }, 2000);
                },
                
                showMainApp: function() {
                    document.getElementById('registrationSection').classList.add('hidden');
                    document.getElementById('mainAppSection').classList.remove('hidden');
                },
                
                calculateBackgroundMining: function() {
                    if (!this.state.lastActiveTime || !this.state.backgroundMiningEnabled) return;
                    
                    const now = Date.now();
                    const timeDiff = now - this.state.lastActiveTime;
                    const hoursDiff = timeDiff / (1000 * 60 * 60);
                    
                    if (hoursDiff > 0) {
                        const backgroundMined = hoursDiff * this.state.miningRate;
                        this.state.balance += backgroundMined;
                        this.state.todayMining += backgroundMined;
                        this.state.totalMining += backgroundMined;
                        
                        // Show notification about background mining
                        if (backgroundMined > 0.001) {
                            this.showNotification(`🔄 ব্যাকগ্রাউন্ডে ${backgroundMined.toFixed(4)} RBC মাইন হয়েছে!`);
                        }
                        
                        this.checkLevelUp();
                    }
                    
                    this.state.lastActiveTime = now;
                    this.state.miningStartTime = now;
                    this.saveState();
                },
                
                startBackgroundMining: function() {
                    // Update last active time periodically
                    setInterval(() => {
                        if (this.state.backgroundMiningEnabled) {
                            this.state.lastActiveTime = Date.now();
                            this.saveState();
                        }
                    }, 30000); // Update every 30 seconds
                },
                
                setupEventListeners: function() {
                    document.getElementById('miningButton').addEventListener('click', () => this.toggleMining());
                    document.getElementById('bonusButton').addEventListener('click', () => this.claimDailyBonus());
                    document.getElementById('copyButton').addEventListener('click', () => this.copyReferralCode());
                    
                    // Withdraw form listeners
                    const withdrawAmount = document.getElementById('withdrawAmount');
                    const phoneNumber = document.getElementById('phoneNumber');
                    const withdrawButton = document.getElementById('withdrawButton');
                    
                    if (withdrawAmount) {
                        withdrawAmount.addEventListener('input', () => this.calculateWithdrawAmount());
                    }
                    
                    if (phoneNumber) {
                        phoneNumber.addEventListener('input', () => this.validateWithdrawForm());
                    }
                    
                    if (withdrawButton) {
                        withdrawButton.addEventListener('click', () => this.processWithdraw());
                    }
                    
                    // Payment method listeners
                    document.querySelectorAll('input[name="payment"]').forEach(radio => {
                        radio.addEventListener('change', () => this.validateWithdrawForm());
                    });
                },
                
                toggleMining: function() { 
                    this.state.isMining ? this.stopMining() : this.startMining(); 
                },
                
                startMining: function() {
                    this.state.isMining = true; 
                    this.state.miningStartTime = Date.now();
                    document.getElementById('miningButton').classList.add('active');
                    document.getElementById('buttonStatus').textContent = 'মাইনিং চলছে...';
                    this.showNotification('✅ মাইনিং শুরু হয়েছে!'); 
                    this.saveState(); 
                    this.updateMiningProgress();
                },
                
                stopMining: function() {
                    if (this.state.isMining && this.state.miningStartTime) {
                        const minedTime = (Date.now() - this.state.miningStartTime) / 1000;
                        const minedAmount = (minedTime / 3600) * this.state.miningRate;
                        this.state.balance += minedAmount; 
                        this.state.todayMining += minedAmount; 
                        this.state.totalMining += minedAmount;
                        this.checkLevelUp();
                    }
                    this.state.isMining = false; 
                    this.state.miningStartTime = null;
                    document.getElementById('miningButton').classList.remove('active');
                    document.getElementById('buttonStatus').textContent = 'মাইনিং শুরু করুন';
                    document.getElementById('timer').textContent = '';
                    this.showNotification('⏸️ মাইনিং বন্ধ হয়েছে'); 
                    this.updateUI(); 
                    this.saveState();
                },
                
                updateMiningProgress: function() {
                    if (!this.state.isMining) return;
                    const elapsed = (Date.now() - this.state.miningStartTime) / 1000;
                    const hours = Math.floor(elapsed / 3600); 
                    const minutes = Math.floor((elapsed % 3600) / 60); 
                    const seconds = Math.floor(elapsed % 60);
                    document.getElementById('timer').textContent = `\( {hours.toString().padStart(2, '0')}: \){minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                    const minedAmount = (elapsed / 3600) * this.state.miningRate;
                    document.getElementById('balance').textContent = (this.state.balance + minedAmount).toFixed(4) + ' RBC';
                    requestAnimationFrame(() => this.updateMiningProgress());
                },
                
                claimDailyBonus: function() {
                    const now = Date.now(); 
                    const lastClaim = this.state.lastBonusClaim || 0; 
                    const hoursSinceLastClaim = (now - lastClaim) / (1000 * 60 * 60);
                    if (hoursSinceLastClaim >= 24) {
                        this.state.balance += 0.1; 
                        this.state.todayMining += 0.1; 
                        this.state.totalMining += 0.1; 
                        this.state.lastBonusClaim = now;
                        this.showNotification('🎉 ডেইলি বোনাস ক্লেম করা হয়েছে! +0.1 RBC');
                        this.updateUI(); 
                        this.saveState(); 
                        this.checkBonusAvailability();
                    } else {
                        const hoursLeft = 24 - hoursSinceLastClaim;
                        this.showNotification(`⏰ আপনি ${Math.floor(hoursLeft)} ঘন্টা পরে আবার বোনাস ক্লেম করতে পারবেন`);
                    }
                },
                
                copyReferralCode: function() {
                    navigator.clipboard.writeText(this.state.referralCode).then(() => {
                        this.showNotification('📋 রেফারেল কোড কপি হয়েছে!');
                        this.state.referralCount++; 
                        this.updateUI(); 
                        this.saveState();
                    });
                },
                
                checkLevelUp: function() {
                    if (this.state.totalMining >= 10 && this.state.level === 'বাচ্চা খরগোশ') {
                        this.state.level = 'তরুণ খরগোশ'; 
                        this.state.miningRate = 0.35;
                        this.showNotification('🎊 লেভেল আপ! আপনি এখন তরুণ খরগোশ!');
                    } else if (this.state.totalMining >= 25 && this.state.level === 'তরুণ খরগোশ') {
                        this.state.level = 'প্রাপ্তবয়স্ক খরগোশ'; 
                        this.state.miningRate = 0.5;
                        this.showNotification('🎊 লেভেল আপ! আপনি এখন প্রাপ্তবয়স্ক খরগোশ!');
                    } else if (this.state.totalMining >= 50 && this.state.level === 'প্রাপ্তবয়স্ক খরগোশ') {
                        this.state.level = 'খরগোশ রাজা'; 
                        this.state.miningRate = 0.75;
                        this.showNotification('👑 লেভেল আপ! আপনি এখন খরগোশ রাজা!');
                    }
                },
                
                updateUI: function() {
                    document.getElementById('balance').textContent = this.state.balance.toFixed(4) + ' RBC';
                    document.getElementById('todayMining').textContent = this.state.todayMining.toFixed(4) + ' RBC';
                    document.getElementById('totalMining').textContent = this.state.totalMining.toFixed(4) + ' RBC';
                    document.getElementById('referralCount').textContent = this.state.referralCount;
                    document.getElementById('userLevel').textContent = this.state.level;
                    document.getElementById('miningRate').textContent = this.state.miningRate.toFixed(2);
                    document.getElementById('referralCode').textContent = this.state.referralCode;
                },
                
                showNotification: function(message) {
                    const notification = document.getElementById('notification');
                    notification.textContent = message; 
                    notification.classList.add('show');
                    setTimeout(() => notification.classList.remove('show'), 3000);
                },
                
                loadState: function() {
                    const savedState = localStorage.getItem('rabbitCoinState');
                    if (savedState) { 
                        this.state = JSON.parse(savedState); 
                        this.updateUI(); 
                    }
                    this.checkBonusAvailability();
                },
                
                saveState: function() { 
                    localStorage.setItem('rabbitCoinState', JSON.stringify(this.state)); 
                },
                
                checkBonusAvailability: function() {
                    const now = Date.now(); 
                    const lastClaim = this.state.lastBonusClaim || 0; 
                    const hoursSinceLastClaim = (now - lastClaim) / (1000 * 60 * 60);
                    const bonusButton = document.getElementById('bonusButton');
                    if (bonusButton) {
                        if (hoursSinceLastClaim >= 24) { 
                            bonusButton.disabled = false; 
                            bonusButton.textContent = 'ক্লেম করুন'; 
                        } else { 
                            bonusButton.disabled = true; 
                            const hoursLeft = Math.floor(24 - hoursSinceLastClaim); 
                            bonusButton.textContent = `${hoursLeft}ঘন্টা পরে`; 
                        }
                    }
                },
                
                simulateReferral: function() {
                    if (Math.random() > 0.95) {
                        this.state.referralCount++; 
                        this.state.balance += 0.05;
                        this.showNotification('👥 নতুন রেফারেল যোগ হয়েছে! +0.05 RBC');
                        this.updateUI(); 
                        this.saveState();
                    }
                },
                
                startPeriodicChecks: function() {
                    setInterval(() => this.simulateReferral(), 30000);
                    setInterval(() => this.checkBonusAvailability(), 60000);
                    setInterval(() => this.updateWithdrawStatus(), 1000);
                    setInterval(() => {
                        if (this.state.isMining) {
                            const elapsed = (Date.now() - this.state.miningStartTime) / 1000;
                            const minedAmount = (elapsed / 3600) * this.state.miningRate;
                            this.state.balance += minedAmount; 
                            this.state.todayMining += minedAmount; 
                            this.state.totalMining += minedAmount;
                            this.saveState();
                        }
                    }, 5000);
                },
                
                // Withdraw Functions
                updateWithdrawStatus: function() {
                    const now = new Date();
                    const countdown = document.getElementById('withdrawCountdown');
                    const withdrawForm = document.getElementById('withdrawForm');
                    
                    if (!countdown || !withdrawForm) return;
                    
                    if (now >= this.withdrawReleaseDate) {
                        countdown.textContent = 'উইথড্র চালু হয়েছে!';
                        withdrawForm.classList.add('active');
                    } else {
                        const timeLeft = this.withdrawReleaseDate - now;
                        const days = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
                        const hours = Math.floor((timeLeft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                        const minutes = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
                        
                        countdown.textContent = `চালু হবে: \( {days}দিন \){hours}ঘন্টা`;
                        withdrawForm.classList.remove('active');
                    }
                },
                
                calculateWithdrawAmount: function() {
                    const amount = parseFloat(document.getElementById('withdrawAmount').value) || 0;
                    const bdtAmount = amount * this.conversionRate;
                    const charge = Math.max(bdtAmount * 0.02, 5);
                    const finalAmount = bdtAmount - charge;
                    
                    document.getElementById('withdrawAmountBDT').textContent = `${finalAmount.toFixed(2)} টাকা`;
                    this.validateWithdrawForm();
                },
                
                validateWithdrawForm: function() {
                    const phoneNumber = document.getElementById('phoneNumber').value;
                    const amount = parseFloat(document.getElementById('withdrawAmount').value) || 0;
                    const withdrawButton = document.getElementById('withdrawButton');
                    
                    if (!withdrawButton) return;
                    
                    const isValidPhone = /^01[3-9]\d{8}$/.test(phoneNumber);
                    const isValidAmount = amount >= 10 && amount <= this.state.balance;
                    
                    withdrawButton.disabled = !(isValidPhone && isValidAmount);
                },
                
                processWithdraw: function() {
                    const phoneNumber = document.getElementById('phoneNumber').value;
                    const amount = parseFloat(document.getElementById('withdrawAmount').value);
                    const paymentMethod = document.querySelector('input[name="payment"]:checked').value;
                    
                    if (amount > this.state.balance) {
                        this.showNotification('❌ অপর্যাপ্ত ব্যালেন্স!');
                        return;
                    }
                    
                    // Process withdrawal (demo)
                    this.state.balance -= amount;
                    this.state.withdrawHistory.push({
                        amount: amount,
                        phoneNumber: phoneNumber,
                        paymentMethod: paymentMethod,
                        date: new Date().toISOString(),
                        status: 'pending'
                    });
                    
                    this.showNotification(`✅ ${amount} RBC উইথড্র রিকোয়েস্ট পাঠানো হয়েছে!`);
                    
                    // Reset form
                    document.getElementById('withdrawAmount').value = '';
                    document.getElementById('phoneNumber').value = '';
                    document.getElementById('withdrawAmountBDT').textContent = '0 টাকা';
                    
                    this.updateUI();
                    this.saveState();
                }
            };
            
            RabbitCoinApp.init();
        });
    </script>
</body>
</html>
