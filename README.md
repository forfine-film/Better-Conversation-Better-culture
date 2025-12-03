<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Better Conversations, Better Culture</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Noto Sans Thai', sans-serif;
        }
        
        @keyframes gradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        .animate-gradient {
            background-size: 200% auto;
            animation: gradient 3s ease infinite;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease-out;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .animate-pulse {
            animation: pulse 2s ease-in-out infinite;
        }
        
        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        
        .animate-spin {
            animation: spin 1s linear infinite;
        }
        
        select {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 24 24' stroke='%233b82f6'%3E%3Cpath stroke-linecap='round' stroke-linejoin='round' stroke-width='2.5' d='M19 9l-7 7-7-7'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1.25rem;
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-50 via-white to-indigo-50">
    
    <div class="max-w-3xl mx-auto px-4 py-8">
        
        <!-- Header -->
        <header class="text-center py-8 mb-8">
            <div class="relative">
                <h1 class="text-4xl md:text-5xl font-black mb-3 tracking-tight">
                    <span class="bg-gradient-to-r from-blue-600 via-indigo-500 to-blue-600 bg-clip-text text-transparent animate-gradient">
                        Better Conversations
                    </span>
                </h1>
                <div class="flex items-center justify-center gap-3 mb-4">
                    <div class="h-0.5 w-12 bg-gradient-to-r from-transparent to-blue-400 rounded-full"></div>
                    <h2 class="text-2xl md:text-3xl font-bold bg-gradient-to-r from-indigo-500 to-blue-500 bg-clip-text text-transparent">
                        Better Culture
                    </h2>
                    <div class="h-0.5 w-12 bg-gradient-to-l from-transparent to-indigo-400 rounded-full"></div>
                </div>
            </div>
            
            <div class="relative inline-block">
                <div class="absolute -left-6 top-1/2 -translate-y-1/2 text-blue-300 text-2xl">✦</div>
                <div class="absolute -right-6 top-1/2 -translate-y-1/2 text-indigo-300 text-2xl">✦</div>
                <p class="text-lg md:text-xl text-slate-600 font-medium px-8 py-3 bg-gradient-to-r from-blue-50 via-white to-indigo-50 rounded-full border border-blue-100 shadow-sm">
                    พื้นที่ปลอดภัยในการสื่อสาร วัฒนธรรมองค์กรที่แข็งแรง
                </p>
            </div>
            
            <div class="mt-5 inline-flex items-center gap-2 px-4 py-2 bg-white/80 backdrop-blur rounded-full border border-blue-100 shadow-lg">
                <span class="w-2 h-2 bg-green-400 rounded-full animate-pulse"></span>
                <span class="text-sm text-slate-500 font-medium">A supportive space for ideas and voices</span>
                <span class="text-blue-400">💬</span>
            </div>
        </header>

        <!-- API Key Modal -->
        <div id="apiKeyModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 p-4 hidden">
            <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full p-6 fade-in">
                <h3 class="text-xl font-bold text-blue-600 mb-4">🔑 ใส่ Gemini API Key</h3>
                
                <div class="bg-blue-50 border-l-4 border-blue-400 p-4 mb-4 rounded-r-lg">
                    <p class="text-sm text-blue-800">
                        <strong>วิธีรับ API Key ฟรี:</strong><br>
                        1. ไปที่ <a href="https://aistudio.google.com/apikey" target="_blank" class="underline font-semibold">Google AI Studio</a><br>
                        2. คลิก "Create API Key"<br>
                        3. คัดลอก Key มาวางที่นี่
                    </p>
                </div>

                <input
                    type="password"
                    id="apiKeyInput"
                    placeholder="AIzaSy..."
                    class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:outline-none mb-4 font-mono text-sm"
                >
                
                <label class="flex items-center gap-2 mb-4 cursor-pointer">
                    <input type="checkbox" id="saveKeyCheckbox" class="w-4 h-4 text-blue-600 rounded">
                    <span class="text-sm text-gray-600">จดจำ API Key ไว้ในเครื่องนี้</span>
                </label>

                <div class="flex gap-3">
                    <button onclick="closeApiModal()" class="flex-1 py-2 px-4 border-2 border-gray-300 rounded-xl text-gray-600 hover:bg-gray-50 transition">
                        ยกเลิก
                    </button>
                    <button onclick="submitApiKey()" class="flex-1 py-2 px-4 bg-blue-600 text-white rounded-xl hover:bg-blue-700 transition">
                        ยืนยัน
                    </button>
                </div>
            </div>
        </div>

        <!-- Form -->
        <div class="bg-white rounded-2xl shadow-xl border border-blue-100 p-6 mb-6">
            
            <!-- Topic Input -->
            <div class="mb-6 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl p-4 border border-blue-100">
                <label class="block text-sm font-semibold mb-2 text-slate-600">
                    <span class="mr-2">📝</span>
                    เรื่องที่ต้องการสื่อสาร
                </label>
                <textarea
                    id="topic"
                    placeholder="เช่น นักเรียนมาสาย, การบ้านไม่ส่ง, ขอเลื่อนประชุม, ขอบคุณที่ช่วยงาน..."
                    rows="3"
                    class="block w-full bg-white border-2 border-blue-100 px-4 py-3 rounded-xl text-slate-700 resize-none transition-all duration-300 hover:border-blue-300 focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 placeholder:text-slate-400"
                ></textarea>
            </div>

            <!-- Selects Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                <div>
                    <label class="block text-sm font-semibold mb-2 text-slate-600">
                        <span class="mr-2">👤</span>ฉันคือใคร
                    </label>
                    <select id="sender" class="block w-full bg-white border-2 border-blue-100 px-4 py-3 pr-12 rounded-xl text-slate-700 font-medium cursor-pointer transition-all duration-300 hover:border-blue-300 hover:shadow-lg focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 appearance-none">
                        <option value="ผู้บริหารระดับสูง">ผู้บริหารระดับสูง</option>
                        <option value="ผู้บริหารระดับเดียวกัน">ผู้บริหารระดับเดียวกัน</option>
                        <option value="หัวหน้างาน/ครูอาวุโส">หัวหน้างาน/ครูอาวุโส</option>
                        <option value="ครู" selected>ครู</option>
                        <option value="บุคลากรสนับสนุน">บุคลากรสนับสนุน</option>
                        <option value="ผู้ปกครอง">ผู้ปกครอง</option>
                        <option value="นักเรียน">นักเรียน</option>
                        <option value="ทุกคนในองค์กร">ทุกคนในองค์กร</option>
                        <option value="แขกผู้มีเกียรติ">แขกผู้มีเกียรติ</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-semibold mb-2 text-slate-600">
                        <span class="mr-2">👥</span>สื่อสารกับใคร
                    </label>
                    <select id="receiver" class="block w-full bg-white border-2 border-blue-100 px-4 py-3 pr-12 rounded-xl text-slate-700 font-medium cursor-pointer transition-all duration-300 hover:border-blue-300 hover:shadow-lg focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 appearance-none">
                        <option value="ผู้บริหารระดับสูง">ผู้บริหารระดับสูง</option>
                        <option value="ผู้บริหารระดับเดียวกัน">ผู้บริหารระดับเดียวกัน</option>
                        <option value="หัวหน้างาน/ครูอาวุโส">หัวหน้างาน/ครูอาวุโส</option>
                        <option value="ครู">ครู</option>
                        <option value="บุคลากรสนับสนุน">บุคลากรสนับสนุน</option>
                        <option value="ผู้ปกครอง">ผู้ปกครอง</option>
                        <option value="นักเรียน" selected>นักเรียน</option>
                        <option value="ทุกคนในองค์กร">ทุกคนในองค์กร</option>
                        <option value="แขกผู้มีเกียรติ">แขกผู้มีเกียรติ</option>
                    </select>
                </div>
            </div>

            <div class="mb-4">
                <label class="block text-sm font-semibold mb-2 text-slate-600">
                    <span class="mr-2">🎯</span>วัตถุประสงค์
                </label>
                <select id="purpose" class="block w-full bg-white border-2 border-blue-100 px-4 py-3 pr-12 rounded-xl text-slate-700 font-medium cursor-pointer transition-all duration-300 hover:border-blue-300 hover:shadow-lg focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 appearance-none">
                    <option value="ให้ข้อเสนอแนะที่สร้างสรรค์">ให้ข้อเสนอแนะที่สร้างสรรค์</option>
                    <option value="ไกล่เกลี่ย/แก้ปัญหาความขัดแย้ง">ไกล่เกลี่ย/แก้ปัญหาความขัดแย้ง</option>
                    <option value="ถ่ายทอดวิสัยทัศน์/เป้าหมาย">ถ่ายทอดวิสัยทัศน์/เป้าหมาย</option>
                    <option value="ขอความช่วยเหลือ/การสนับสนุน">ขอความช่วยเหลือ/การสนับสนุน</option>
                    <option value="ให้กำลังใจ/สร้างแรงจูงใจ" selected>ให้กำลังใจ/สร้างแรงจูงใจ</option>
                    <option value="แจ้งการเปลี่ยนแปลง/นโยบายใหม่">แจ้งการเปลี่ยนแปลง/นโยบายใหม่</option>
                    <option value="ชื่นชม/ขอบคุณ">ชื่นชม/ขอบคุณ</option>
                    <option value="มอบหมายงาน">มอบหมายงาน</option>
                    <option value="ให้คำปรึกษา/โค้ช">ให้คำปรึกษา/โค้ช</option>
                    <option value="รายงานปัญหา/ข้อกังวล">รายงานปัญหา/ข้อกังวล</option>
                    <option value="🎤 กล่าวเปิดงาน">🎤 กล่าวเปิดงาน</option>
                    <option value="🎬 กล่าวปิดงาน">🎬 กล่าวปิดงาน</option>
                </select>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                <div>
                    <label class="block text-sm font-semibold mb-2 text-slate-600">
                        <span class="mr-2">💬</span>โทนภาษา
                    </label>
                    <select id="tone" class="block w-full bg-white border-2 border-blue-100 px-4 py-3 pr-12 rounded-xl text-slate-700 font-medium cursor-pointer transition-all duration-300 hover:border-blue-300 hover:shadow-lg focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 appearance-none">
                        <option value="ภาษาเขียน (เป็นทางการ)">ภาษาเขียน (เป็นทางการ)</option>
                        <option value="ภาษาสื่อสาร (กึ่งทางการ)" selected>ภาษาสื่อสาร (กึ่งทางการ)</option>
                        <option value="ภาษาพูด (กันเอง)">ภาษาพูด (กันเอง)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-semibold mb-2 text-slate-600">
                        <span class="mr-2">📱</span>ช่องทาง
                    </label>
                    <select id="format" class="block w-full bg-white border-2 border-blue-100 px-4 py-3 pr-12 rounded-xl text-slate-700 font-medium cursor-pointer transition-all duration-300 hover:border-blue-300 hover:shadow-lg focus:outline-none focus:border-blue-500 focus:ring-4 focus:ring-blue-50 appearance-none">
                        <option value="พูดคุยต่อหน้า" selected>พูดคุยต่อหน้า</option>
                        <option value="อีเมล/ข้อความ">อีเมล/ข้อความ</option>
                        <option value="การประชุมกลุ่ม">การประชุมกลุ่ม</option>
                        <option value="แชท LINE/Messenger">แชท LINE/Messenger</option>
                        <option value="โทรศัพท์">โทรศัพท์</option>
                        <option value="🎙️ บนเวที/หน้าชุมชน">🎙️ บนเวที/หน้าชุมชน</option>
                    </select>
                </div>
            </div>

            <!-- Submit Button -->
            <button
                id="generateBtn"
                onclick="handleGenerate()"
                class="w-full py-4 rounded-xl font-bold text-lg transition-all duration-300 flex justify-center items-center gap-3 bg-gradient-to-r from-blue-600 to-indigo-600 text-white shadow-lg shadow-blue-200 hover:shadow-xl hover:shadow-blue-300 hover:scale-[1.02] active:scale-[0.98]"
            >
                <span>สร้างแนวทางการสื่อสาร</span>
                <span class="text-xl">✨</span>
            </button>
            
            <!-- Change API Key -->
            <div id="changeKeyBtn" class="mt-3 text-center hidden">
                <button onclick="showApiModal()" class="text-sm text-slate-400 hover:text-blue-500 underline">
                    🔑 เปลี่ยน API Key
                </button>
            </div>
        </div>

        <!-- Error -->
        <div id="errorBox" class="mb-6 p-5 bg-rose-50 border-2 border-rose-200 rounded-xl fade-in hidden">
            <div class="flex items-start gap-3">
                <span class="text-2xl">🚨</span>
                <div>
                    <p class="font-bold text-rose-800">เกิดข้อผิดพลาด</p>
                    <p id="errorMessage" class="mt-1 text-rose-700 text-sm"></p>
                </div>
            </div>
        </div>

        <!-- Result -->
        <div id="resultCard" class="mt-8 fade-in hidden">
            <div class="bg-white rounded-2xl shadow-xl border border-blue-100 overflow-hidden">
                <div class="bg-gradient-to-r from-blue-600 to-indigo-600 px-6 py-4">
                    <div class="flex items-center justify-between">
                        <h2 class="text-xl font-bold text-white flex items-center gap-2">
                            <span class="text-2xl">💡</span>
                            แนวทางการสื่อสารที่แนะนำ
                        </h2>
                        <button
                            onclick="toggleResult()"
                            id="toggleBtn"
                            class="px-3 py-1.5 bg-white/20 hover:bg-white/30 rounded-full text-white text-sm font-semibold transition-all duration-300"
                        >
                            ย่อ ▲
                        </button>
                    </div>
                </div>
                
                <div id="resultContent" class="p-6">
                    <!-- Strategy -->
                    <div class="group mb-5">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="font-bold text-slate-700 flex items-center gap-2">
                                <span class="w-8 h-8 rounded-lg bg-sky-500 flex items-center justify-center text-white text-sm shadow-md">🧠</span>
                                <span>แนวคิด/หลักการ</span>
                            </h3>
                        </div>
                        <div class="bg-slate-50 rounded-xl p-4 border border-slate-100 transition-all duration-300 group-hover:bg-white group-hover:shadow-md group-hover:border-blue-100">
                            <p id="strategyText" class="text-slate-700 leading-relaxed whitespace-pre-line"></p>
                        </div>
                    </div>
                    
                    <!-- Script -->
                    <div class="group mb-5">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="font-bold text-slate-700 flex items-center gap-2">
                                <span class="w-8 h-8 rounded-lg bg-blue-600 flex items-center justify-center text-white text-sm shadow-md">💬</span>
                                <span>คำพูด/ข้อความที่แนะนำ</span>
                            </h3>
                            <button onclick="copyText('scriptText')" class="px-3 py-1.5 text-xs font-semibold rounded-full bg-blue-50 text-blue-600 hover:bg-blue-100 transition-all duration-300">
                                📋 คัดลอก
                            </button>
                        </div>
                        <div class="bg-slate-50 rounded-xl p-4 border border-slate-100 transition-all duration-300 group-hover:bg-white group-hover:shadow-md group-hover:border-blue-100">
                            <p id="scriptText" class="text-slate-800 leading-relaxed whitespace-pre-line text-base font-medium"></p>
                        </div>
                    </div>
                    
                    <!-- Example -->
                    <div class="group mb-5">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="font-bold text-slate-700 flex items-center gap-2">
                                <span class="w-8 h-8 rounded-lg bg-amber-500 flex items-center justify-center text-white text-sm shadow-md">🎭</span>
                                <span>ตัวอย่างบทสนทนา/สถานการณ์</span>
                            </h3>
                            <button onclick="copyText('exampleText')" class="px-3 py-1.5 text-xs font-semibold rounded-full bg-blue-50 text-blue-600 hover:bg-blue-100 transition-all duration-300">
                                📋 คัดลอก
                            </button>
                        </div>
                        <div class="bg-slate-50 rounded-xl p-4 border border-slate-100 transition-all duration-300 group-hover:bg-white group-hover:shadow-md group-hover:border-blue-100">
                            <p id="exampleText" class="text-slate-700 leading-relaxed whitespace-pre-line italic"></p>
                        </div>
                    </div>
                    
                    <!-- Tips & Donts -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- Tips -->
                        <div class="group mb-5">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="font-bold text-slate-700 flex items-center gap-2">
                                    <span class="w-8 h-8 rounded-lg bg-emerald-500 flex items-center justify-center text-white text-sm shadow-md">✅</span>
                                    <span>เคล็ดลับ</span>
                                </h3>
                            </div>
                            <div class="bg-slate-50 rounded-xl p-4 border border-slate-100 transition-all duration-300 group-hover:bg-white group-hover:shadow-md group-hover:border-blue-100">
                                <ul id="tipsList" class="space-y-2"></ul>
                            </div>
                        </div>
                        
                        <!-- Donts -->
                        <div class="group mb-5">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="font-bold text-slate-700 flex items-center gap-2">
                                    <span class="w-8 h-8 rounded-lg bg-rose-500 flex items-center justify-center text-white text-sm shadow-md">⚠️</span>
                                    <span>สิ่งที่ควรหลีกเลี่ยง</span>
                                </h3>
                            </div>
                            <div class="bg-slate-50 rounded-xl p-4 border border-slate-100 transition-all duration-300 group-hover:bg-white group-hover:shadow-md group-hover:border-blue-100">
                                <ul id="dontsList" class="space-y-2"></ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <footer class="mt-10 text-center text-slate-400 text-sm pb-6">
            <p>พัฒนาเพื่อส่งเสริมการสื่อสารที่สร้างสรรค์ในโรงเรียน 💙</p>
            <p class="mt-1 text-xs">Powered by Gemini AI</p>
        </footer>
    </div>

    <script>
        // State
        let apiKey = localStorage.getItem('gemini_api_key') || '';
        let isExpanded = true;
        
        // Show change key button if key exists
        if (apiKey) {
            document.getElementById('changeKeyBtn').classList.remove('hidden');
        }
        
        // API Modal Functions
        function showApiModal() {
            document.getElementById('apiKeyModal').classList.remove('hidden');
            document.getElementById('apiKeyInput').value = apiKey;
            document.getElementById('saveKeyCheckbox').checked = !!apiKey;
        }
        
        function closeApiModal() {
            document.getElementById('apiKeyModal').classList.add('hidden');
        }
        
        function submitApiKey() {
            const key = document.getElementById('apiKeyInput').value.trim();
            const save = document.getElementById('saveKeyCheckbox').checked;
            
            if (key) {
                apiKey = key;
                if (save) {
                    localStorage.setItem('gemini_api_key', key);
                } else {
                    localStorage.removeItem('gemini_api_key');
                }
                document.getElementById('changeKeyBtn').classList.remove('hidden');
                closeApiModal();
            }
        }
        
        // Copy Function
        function copyText(elementId) {
            const text = document.getElementById(elementId).innerText;
            navigator.clipboard.writeText(text).then(() => {
                const btn = event.target;
                btn.innerText = '✓ คัดลอกแล้ว!';
                btn.classList.remove('bg-blue-50', 'text-blue-600');
                btn.classList.add('bg-green-100', 'text-green-700');
                setTimeout(() => {
                    btn.innerText = '📋 คัดลอก';
                    btn.classList.remove('bg-green-100', 'text-green-700');
                    btn.classList.add('bg-blue-50', 'text-blue-600');
                }, 2000);
            });
        }
        
        // Toggle Result
        function toggleResult() {
            isExpanded = !isExpanded;
            const content = document.getElementById('resultContent');
            const btn = document.getElementById('toggleBtn');
            
            if (isExpanded) {
                content.classList.remove('hidden');
                btn.innerText = 'ย่อ ▲';
            } else {
                content.classList.add('hidden');
                btn.innerText = 'ขยาย ▼';
            }
        }
        
        // Show/Hide Loading
        function setLoading(loading) {
            const btn = document.getElementById('generateBtn');
            if (loading) {
                btn.disabled = true;
                btn.classList.remove('bg-gradient-to-r', 'from-blue-600', 'to-indigo-600', 'hover:scale-[1.02]');
                btn.classList.add('bg-slate-300', 'text-slate-500', 'cursor-not-allowed');
                btn.innerHTML = `
                    <svg class="animate-spin h-6 w-6" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" fill="none"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                    </svg>
                    <span>กำลังสร้างแนวทาง...</span>
                `;
            } else {
                btn.disabled = false;
                btn.classList.add('bg-gradient-to-r', 'from-blue-600', 'to-indigo-600', 'hover:scale-[1.02]');
                btn.classList.remove('bg-slate-300', 'text-slate-500', 'cursor-not-allowed');
                btn.innerHTML = `
                    <span>สร้างแนวทางการสื่อสาร</span>
                    <span class="text-xl">✨</span>
                `;
            }
        }
        
        // Show Error
        function showError(message) {
            document.getElementById('errorMessage').innerText = message;
            document.getElementById('errorBox').classList.remove('hidden');
        }
        
        // Hide Error
        function hideError() {
            document.getElementById('errorBox').classList.add('hidden');
        }
        
        // Display Result
        function displayResult(result) {
            document.getElementById('strategyText').innerText = result.strategy || '';
            document.getElementById('scriptText').innerText = result.script || '';
            document.getElementById('exampleText').innerText = result.example || '';
            
            // Tips
            const tipsList = document.getElementById('tipsList');
            tipsList.innerHTML = '';
            (result.tips || []).forEach((tip, index) => {
                tipsList.innerHTML += `
                    <li class="flex items-start gap-2 text-slate-700">
                        <span class="w-5 h-5 rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center text-xs font-bold flex-shrink-0 mt-0.5">${index + 1}</span>
                        <span class="text-sm">${tip}</span>
                    </li>
                `;
            });
            
            // Donts
            const dontsList = document.getElementById('dontsList');
            dontsList.innerHTML = '';
            (result.donts || []).forEach((dont) => {
                dontsList.innerHTML += `
                    <li class="flex items-start gap-2 text-slate-700">
                        <span class="w-5 h-5 rounded-full bg-rose-100 text-rose-600 flex items-center justify-center text-xs flex-shrink-0 mt-0.5">✕</span>
                        <span class="text-sm">${dont}</span>
                    </li>
                `;
            });
            
            document.getElementById('resultCard').classList.remove('hidden');
            isExpanded = true;
            document.getElementById('resultContent').classList.remove('hidden');
            document.getElementById('toggleBtn').innerText = 'ย่อ ▲';
        }
        
        // Generate Communication Guide
        async function handleGenerate() {
            if (!apiKey) {
                showApiModal();
                return;
            }
            
            hideError();
            setLoading(true);
            document.getElementById('resultCard').classList.add('hidden');
            
            const sender = document.getElementById('sender').value;
            const receiver = document.getElementById('receiver').value;
            const purpose = document.getElementById('purpose').value;
            const tone = document.getElementById('tone').value;
            const format = document.getElementById('format').value;
            const topic = document.getElementById('topic').value;
            
            const isSpeech = purpose.includes('กล่าวเปิดงาน') || purpose.includes('กล่าวปิดงาน');
            
            const prompt = `คุณคือโค้ชด้านการสื่อสารมืออาชีพสำหรับสถาบันการศึกษาในประเทศไทย สร้างแนวทางการสื่อสารที่เป็นธรรมชาติ เหมาะสมกับวัฒนธรรมไทย และใช้งานได้จริง

โจทย์:
- ผู้ส่ง: ${sender}
- ผู้รับ: ${receiver}
- วัตถุประสงค์: ${purpose}
- โทนภาษา: ${tone}
- ช่องทาง: ${format}
- เรื่องที่ต้องการสื่อสาร: ${topic || 'ไม่ระบุ (กรุณาสร้างตัวอย่างทั่วไป)'}

${purpose.includes('กล่าวเปิดงาน') ? 'นี่คือการกล่าวเปิดงาน กรุณาสร้างสคริปต์กล่าวเปิดงานที่สมบูรณ์ มีการต้อนรับ แนะนำงาน และเปิดงานอย่างเป็นทางการ' : ''}
${purpose.includes('กล่าวปิดงาน') ? 'นี่คือการกล่าวปิดงาน กรุณาสร้างสคริปต์กล่าวปิดงานที่สมบูรณ์ มีการสรุป ขอบคุณ และกล่าวปิดอย่างประทับใจ' : ''}

ตอบเป็น JSON เท่านั้น ไม่ต้องมีข้อความอื่น:
{
  "strategy": "แนวคิดหลักการสื่อสาร 2-3 ประโยค",
  "script": "คำพูด/ข้อความที่แนะนำ ${isSpeech ? '(สคริปต์เต็มสำหรับกล่าว ความยาวประมาณ 1-2 นาที)' : '3-5 ประโยค'} เขียนเหมือนพูดจริง ใส่อิโมจิเล็กน้อย",
  "example": "ตัวอย่างบทสนทนาจำลอง แสดงทั้งคำพูดและการตอบกลับ หรือตัวอย่างสถานการณ์",
  "tips": ["เคล็ดลับ 1", "เคล็ดลับ 2", "เคล็ดลับ 3"],
  "donts": ["สิ่งที่ไม่ควรทำ 1", "สิ่งที่ไม่ควรทำ 2"]
}`;

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{ 
                            role: "user", 
                            parts: [{ text: prompt }] 
                        }],
                        generationConfig: {
                            temperature: 0.8,
                            topK: 40,
                            topP: 0.95,
                            maxOutputTokens: 2048,
                        }
                    })
                });

                if (!response.ok) {
                    const errorBody = await response.json();
                    throw new Error(errorBody.error?.message || `API Error: ${response.status}`);
                }

                const data = await response.json();
                
                if (data.candidates && data.candidates[0]?.content?.parts[0]?.text) {
                    let jsonString = data.candidates[0].content.parts[0].text;
                    jsonString = jsonString.replace(/```json\n?/g, '').replace(/```\n?/g, '').trim();
                    const result = JSON.parse(jsonString);
                    displayResult(result);
                } else {
                    throw new Error('ไม่สามารถอ่านผลลัพธ์จาก API ได้');
                }
            } catch (error) {
                console.error('Generate error:', error);
                if (error.message.includes('API key')) {
                    showError('API Key ไม่ถูกต้อง กรุณาตรวจสอบและลองใหม่อีกครั้ง');
                    apiKey = '';
                    localStorage.removeItem('gemini_api_key');
                } else {
                    showError(error.message || 'เกิดข้อผิดพลาดในการสร้างแนวทาง');
                }
            } finally {
                setLoading(false);
            }
        }
        
        // Update placeholder based on purpose
        document.getElementById('purpose').addEventListener('change', function() {
            const isSpeech = this.value.includes('กล่าวเปิดงาน') || this.value.includes('กล่าวปิดงาน');
            document.getElementById('topic').placeholder = isSpeech 
                ? "เช่น งานวันวิทยาศาสตร์, พิธีมอบประกาศนียบัตร, กิจกรรมวันแม่..." 
                : "เช่น นักเรียนมาสาย, การบ้านไม่ส่ง, ขอเลื่อนประชุม, ขอบคุณที่ช่วยงาน...";
        });
    </script>
</body>
</html>
