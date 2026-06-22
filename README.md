# FitinFlow
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reset - สุขภาพดีในแบบของคุณ</title>
    <!-- นำเข้า Tailwind CSS เพื่อความสวยงามและเปิดบนมือถือได้ดี -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Kanit', sans-serif; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <!-- Header / Navigation -->
    <header class="bg-white shadow-xs py-4 px-6 flex justify-between items-center sticky top-0 z-50">
        <h1 class="text-2xl font-bold text-emerald-600 flex items-center gap-2">
            🌱 Reset <span class="text-xs font-normal text-slate-500 bg-slate-100 px-2 py-0.5 rounded-full">FitInFlow</span>
        </h1>
        <div class="flex gap-4 items-center">
            <span class="text-sm font-medium text-slate-600">คะแนนวันนี้: <strong class="text-emerald-600 text-base">85%</strong></span>
            <div class="w-8 h-8 rounded-full bg-emerald-100 flex items-center justify-center text-sm font-bold text-emerald-700">👤</div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1 max-w-4xl w-full mx-auto p-4 md:p-6 space-y-6">

        <!-- SECTION 1: ฟังก์ชันหลัก - จัดสรรเวลาว่าง (SlotFit) -->
        <section class="bg-gradient-to-br from-emerald-500 to-teal-600 rounded-2xl p-6 md:p-8 text-white shadow-md">
            <h2 class="text-xl md:text-2xl font-bold mb-2">⏱️ ตอนนี้คุณมีเวลาว่างกี่นาที?</h2>
            <p class="text-emerald-100 text-sm mb-6">กรอกเวลาว่างตอนนี้ แล้วเราจะหาภารกิจสุขภาพที่เหมาะกับคุณให้เอง</p>
            
            <div class="flex flex-col sm:flex-row gap-3 mb-6">
                <input type="number" id="timeInput" placeholder="ใส่จำนวนนาที (เช่น 5)" class="flex-1 px-4 py-3 rounded-xl text-slate-800 focus:outline-none focus:ring-2 focus:ring-emerald-300 font-medium">
                <button onclick="getTask()" class="bg-slate-900 hover:bg-slate-800 text-white font-medium px-6 py-3 rounded-xl transition duration-200 shadow-sm cursor-pointer">
                    รับภารกิจด่วน
                </button>
            </div>

            <!-- ปุ่มด่วน (Quick Select) -->
            <div class="flex flex-wrap gap-2 items-center">
                <span class="text-xs text-emerald-100">ปุ่มด่วน:</span>
                <button onclick="quickTime(3)" class="bg-white/20 hover:bg-white/30 text-xs px-3 py-1.5 rounded-lg transition cursor-pointer">3 นาที</button>
                <button onclick="quickTime(5)" class="bg-white/20 hover:bg-white/30 text-xs px-3 py-1.5 rounded-lg transition cursor-pointer">5 นาที</button>
                <button onclick="quickTime(15)" class="bg-white/20 hover:bg-white/30 text-xs px-3 py-1.5 rounded-lg transition cursor-pointer">15 นาที</button>
                <button onclick="quickTime(30)" class="bg-white/20 hover:bg-white/30 text-xs px-3 py-1.5 rounded-lg transition cursor-pointer">30 นาที</button>
            </div>

            <!-- กล่องแสดงผลลัพธ์ภารกิจ -->
            <div id="taskResult" class="hidden mt-6 bg-white/10 backdrop-blur-md rounded-xl p-4 border border-white/20">
                <h3 class="font-semibold text-lg mb-1" id="taskTitle">✨ ภารกิจของคุณคือ:</h3>
                <p class="text-emerald-50 text-sm" id="taskDesc">รายละเอียดภารกิจจะแสดงตรงนี้</p>
            </div>
        </section>

        <!-- Two Column Layout สำหรับ กิน และ นอน -->
        <div class="grid md:grid-cols-2 gap-6">
            
            <!-- SECTION 2: การกิน (Smart Nutrition) -->
            <section class="bg-white p-6 rounded-2xl shadow-xs border border-slate-100 flex flex-col justify-between">
                <div>
                    <h2 class="text-lg font-bold text-slate-800 mb-1 flex items-center gap-2">
                        🍽️ เครื่องมือแปลงเมนู "สั่งยังไงให้ผอม"
                    </h2>
                    <p class="text-slate-500 text-xs mb-4">พิมพ์เมนูตามสั่งหรือเซเว่นที่คุณอยากกินตอนนี้</p>
                    
                    <div class="space-y-3">
                        <select id="foodSelect" class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-slate-700 text-sm focus:outline-emerald-500 bg-white">
                            <option value="">-- เลือกเมนูอาหารที่ต้องการสั่ง --</option>
                            <option value="กะเพราไข่ดาว">ข้าวกะเพราหมูสับไข่ดาว</option>
                            <option value="ข้าวขาหมู">ข้าวขาหมู</option>
                            <option value="ชาไข่มุก">ชานมไข่มุก</option>
                        </select>
                        <button onclick="convertFood()" class="w-full bg-emerald-50 hover:bg-emerald-100 text-emerald-700 text-sm font-medium py-2.5 rounded-xl transition cursor-pointer">
                            ขอสูตรสั่งแบบเฮลตี้
                        </button>
                    </div>

                    <!-- ผลลัพธ์การแปลงเมนู -->
                    <div id="foodResult" class="hidden mt-4 bg-emerald-50/50 rounded-xl p-4 border border-emerald-100 text-sm text-slate-700">
                        <p class="font-medium text-emerald-800 mb-1">💡 แนะนำให้สั่งแบบนี้:</p>
                        <p id="foodDesc"></p>
                    </div>
                </div>
            </section>

            <!-- SECTION 3: การพักผ่อน (Quality Sleep) -->
            <section class="bg-white p-6 rounded-2xl shadow-xs border border-slate-100 flex flex-col justify-between">
                <div>
                    <h2 class="text-lg font-bold text-slate-800 mb-1 flex items-center gap-2">
                        🛌 เครื่องมือคำนวณเวลานอน (Sleep Cycle)
                    </h2>
                    <p class="text-slate-500 text-xs mb-4">ตื่นเวลาไหนให้สมองโล่ง ไม่เพลียตอนตื่น</p>
                    
                    <div class="space-y-3">
                        <label class="text-xs text-slate-600 block">ระบุเวลาที่คุณต้องการตื่นนอน:</label>
                        <input type="time" id="wakeTime" value="06:30" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-slate-700 focus:outline-emerald-500 font-medium">
                        <button onclick="calculateSleep()" class="w-full bg-slate-900 hover:bg-slate-800 text-white text-sm font-medium py-2.5 rounded-xl transition cursor-pointer">
                            คำนวณเวลานอนที่ควรเข้านอน
                        </button>
                    </div>

                    <!-- ผลลัพธ์เวลาเข้านอน -->
                    <div id="sleepResult" class="hidden mt-4 bg-indigo-50 rounded-xl p-4 border border-indigo-100 text-sm text-slate-700">
                        <p class="font-medium text-indigo-900 mb-1">⏰ เวลาเข้านอนที่แนะนำ (หลับครบตื่นไม่เบลอ):</p>
                        <p id="sleepDesc" class="font-mono font-bold text-indigo-700"></p>
                    </div>
                </div>
            </section>

        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-slate-100 border-t border-slate-200 py-4 px-6 text-center text-xs text-slate-500">
        © 2026 Reset App. ทุกคนสุขภาพดีได้แม้ไม่มีเวลา
    </footer>

    <!-- Logic ทำงานต่างๆ ด้วย JavaScript -->
    <script>
        // 1. ฟังก์ชันสุ่มภารกิจตามเวลาว่าง
        function quickTime(minutes) {
            document.getElementById('timeInput').value = minutes;
            getTask();
        }

        function getTask() {
            const mins = parseInt(document.getElementById('timeInput').value);
            const resultDiv = document.getElementById('taskResult');
            const title = document.getElementById('taskTitle');
            const desc = document.getElementById('taskDesc');

            if (!mins || mins <= 0) {
                alert('กรุณากรอกเวลาว่างที่เป็นตัวเลขมากกว่า 0 ครับ');
                return;
            }

            resultDiv.classList.remove('hidden');

            if (mins <= 4) {
                title.innerText = "🧘‍♂️ ภารกิจยืดเหยียดออฟฟิศซินโดรม (เวลาที่ใช้: 2 นาที)";
                desc.innerText = "ลุกขึ้นยืนตรง ประสานมือแล้วยืดขึ้นเหนือศีรษะให้สุด จากนั้นเอียงตัวไปทางซ้ายและขวาค้างไว้ข้างละ 15 วินาที เพื่อคลายกล้ามเนื้อบ่าและหลัง";
            } else if (mins <= 10) {
                title.innerText = "🚶‍♂️ ภารกิจกระตุ้นเผาผลาญ ไร้เหงื่อ (เวลาที่ใช้: 5 นาที)";
                desc.innerText = "เดินไปเติมน้ำเปล่าใส่แก้วใบใหญ่ ลุกขึ้นยืนเขย่งปลายเท้าขึ้น-ลง 20 ครั้ง และเดินรอบที่ทำงานเบาๆ เพื่อกระตุ้นหัวใจและการไหลเวียนเลือด";
            } else if (mins <= 20) {
                title.innerText = "💪 ภารกิจบอดี้เวทด่วนฉบับเก้าอี้เดียว (เวลาที่ใช้: 12 นาที)";
                desc.innerText = "ทำท่า Chair Squat (ลุกนั่งจากเก้าอี้) 15 ครั้ง ทำท่า Wall Push-up (ดันพื้นกับกำแพง) 15 ครั้ง ทำทั้งหมด 3 รอบ ได้กล้ามเนื้อขาและอกแบบไม่ต้องใช้อุปกรณ์!";
            } else {
                title.innerText = "🏃‍♂️ ภารกิจคาร์ดิโอรีเซ็ตหุ่น (เวลาที่ใช้: 25 นาที)";
                desc.innerText = "สวมรองเท้าผ้าใบแล้วออกไปเดินเร็วรอบๆ พื้นที่ หรือสลับกับการเดินขึ้นบันไดแทนลิฟต์ พร้อมเปิดพอดแคสต์ฟังความรู้เพลินๆ ไปด้วย";
            }
        }

        // 2. ฟังก์ชันแปลงอาหารเฮลตี้
        function convertFood() {
            const food = document.getElementById('foodSelect').value;
            const resultDiv = document.getElementById('foodResult');
            const desc = document.getElementById('foodDesc');

            if (!food) {
                alert('กรุณาเลือกเมนูอาหารก่อนครับ');
                return;
            }

            resultDiv.classList.remove('hidden');

            if (food === "กะเพราไข่ดาว") {
                desc.innerHTML = "สั่งว่า: <strong>'ข้าวกะเพราอกไก่ชิ้น ไม่เอาน้ำมัน (หรือน้ำมันน้อยมาก) เปลี่ยนไข่ดาวเป็นไข่ต้ม'</strong><br><span class="text-xs text-slate-500">*ช่วยลดพลังงานจากน้ำมันและไขมันทรานส์ลงได้กว่า 200-250 แคลอรี!*</span>";
            } else if (food === "ข้าวขาหมู") {
                desc.innerHTML = "สั่งว่า: <strong>'ข้าวขาหมูเนื้อล้วน ไม่เอาหนัง ไม่เอาไส้ ขอน้ำราดนิดเดียว เพิ่มคะน้าเยอะๆ'</strong><br><span class="text-xs text-slate-500">*ลดไขมันอิ่มตัวตัวร้ายออกไปได้เกือบทั้งหมด แถมอิ่มโปรตีนเต็มๆ*</span>";
            } else if (food === "ชาไข่มุก") {
                desc.innerHTML = "สั่งว่า: <strong>'ชานมหวาน 25% (หรือหวานน้อยที่สุด) ไม่ใส่ไขุ่มก เปลี่ยนเป็นบุกหรือวุ้นแทน'</strong><br><span class="text-xs text-slate-500">*ลดการรับน้ำตาลเกินความจำเป็น ตัดแคลอรีจากแป้งไข่มุกเม็ดโต*</span>";
            }
        }

        // 3. ฟังก์ชันคำนวณเวลานอนอิงตาม Sleep Cycle (รอบละ 1.5 ชั่วโมง + เผื่อเวลาหลับ 15 นาที)
        function calculateSleep() {
            const wakeTime = document.getElementById('wakeTime').value;
            const resultDiv = document.getElementById('sleepResult');
            const desc = document.getElementById('sleepDesc');

            if (!wakeTime) return;

            const [hours, minutes] = wakeTime.split(':').map(Number);
            let wakeDate = new Date();
            wakeDate.setHours(hours, minutes, 0, 0);

            // คำนวณถอยหลัง 5 รอบ และ 6 รอบของวัฏจักรการนอน (รอบละ 90 นาที) + เผื่อเวลากล่อมตัวนอน 15 นาที
            let sleepTime5Cycles = new Date(wakeDate.getTime() - (5 * 90 * 60 * 1000) - (15 * 60 * 1000));
            let sleepTime6Cycles = new Date(wakeDate.getTime() - (6 * 90 * 60 * 1000) - (15 * 60 * 1000));

            const formatTime = (date) => {
                return date.toTimeString().substring(0, 5) + " น.";
            };

            resultDiv.classList.remove('hidden');
            desc.innerHTML = `😴 ควรเข้านอนตอน <strong>${formatTime(sleepTime6Cycles)}</strong> (นอน 9 ชม.) <br>หรือช้าสุดตอน <strong>${formatTime(sleepTime5Cycles)}</strong> (นอน 7.5 ชม.)`;
        }
    </script>
</body>
</html>
