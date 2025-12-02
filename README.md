<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Better Conversations, Better Culture - โหมดสาธิต</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary-blue': '#1D4ED8',
                        'secondary-blue': '#3B82F6',
                        'accent-sky': '#93C5FD',
                        'white-bg': '#F9FAFB',
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Sukhumvit Set', 'Kanit', sans-serif;
        }
        .whitespace-pre-line {
            white-space: pre-line;
        }
    </style>
</head>
<body class="bg-white-bg">

    <div id="root"></div>

    <script type="text/babel">
        const { useState, useCallback } = React;
        // Enum Definitions
        const SchoolRole = {
            HIGH_EXECUTIVE: 'ผู้บริหารระดับสูง', PEER_EXECUTIVE: 'ผู้บริหารระดับเดียวกัน', SENIOR_TEACHER: 'หัวหน้างาน/ครูอาวุโส', TEACHER: 'ครู', PARENT: 'ผู้ปกครอง', STUDENT: 'นักเรียน', EVERYONE: 'ทุกคนในองค์กร',
        };
        const Purpose = {
            GIVE_FEEDBACK: 'ให้ข้อเสนอแนะที่สร้างสรรค์', RESOLVE_CONFLICT: 'ไกล่เกลี่ย/แก้ปัญหาความขัดแย้ง', SHARE_VISION: 'ถ่ายทอดวิสัยทัศน์/เป้าหมาย', ASK_FOR_HELP: 'ขอความช่วยเหลือ/การสนับสนุน', MOTIVATE: 'ให้กำลังใจ/สร้างแรงจูงใจ', ANNOUNCE_CHANGE: 'แจ้งการเปลี่ยนแปลง/นโยบายใหม่',
        };
        const Tone = {
            FORMAL_WRITTEN: 'ภาษาเขียน (เป็นทางการ)', SEMI_FORMAL_SPOKEN: 'ภาษาสื่อสาร (กึ่งทางการ)', CASUAL_SPOKEN: 'ภาษาพูด (กันเอง)',
        };
        const Format = {
            FACE_TO_FACE: 'พูดคุยต่อหน้า', EMAIL: 'อีเมล/ข้อความ', MEETING: 'การประชุมกลุ่ม',
        };

        // 🛑🛑🛑 ฟังก์ชันนี้ถูกแก้ไขให้ส่งกลับ Mock Data แทนการเรียก API 🛑🛑🛑
        const generateCommunicationGuide = async (sender, receiver, purpose, tone, format) => {
            // จำลองการโหลด 1.5 วินาที
            await new Promise(resolve => setTimeout(resolve, 1500));

            // ข้อมูลตัวอย่างที่ถูกกำหนดไว้ล่วงหน้า
            return {
                strategy: "หลักการสื่อสารแบบ **Growth Mindset** โดยเน้นการมองเห็นศักยภาพของบุคลากร หรือ นักเรียน และให้กำลังใจในเชิงของความพยายาม มากกว่าผลลัพธ์ที่ได้ทันที",
                script: "สวัสดีค่ะ/ครับ [ชื่อบุคคล] ครู/ผมอยากขอบคุณที่ทุ่มเทในงาน/การเรียนที่ผ่านมามากเลยนะ (ส่วนที่ดี) ครูเห็นความพยายามในการพัฒนาตัวเองอยู่เสมอนะ! 🌟\n\n(ส่วนที่ต้องปรับปรุง) เพื่อให้งาน/ผลการเรียนดียิ่งขึ้นไปอีก ผม/ครูอยากแนะนำว่าให้ลองมุ่งเน้นที่ [ระบุจุดที่ชัดเจน] ในช่วงสัปดาห์หน้าดูสิ การฝึกฝนจุดนี้จะช่วยให้เราบรรลุเป้าหมายได้อย่างแน่นอน\n\n(ส่วนปิดท้าย) ครู/ผมพร้อมให้การสนับสนุนเสมอ ถ้ามีคำถามหรือต้องการความช่วยเหลือ อย่าลังเลที่จะเข้ามาคุยกันนะ! ขอให้คุณ/เธอมีความมั่นใจว่าทำได้! 💪",
                example: "ครู: 'อรุณสวัสดิ์ค่ะคุณครู A วันนี้อยากคุยเรื่องการบริหารจัดการชั้นเรียนนิดหน่อย (เปิดด้วยความสุภาพ)\n\nครู A: 'ได้เลยค่ะท่าน ผอ.'\n\nครู: 'ฉันชื่นชมที่คุณ A สามารถจัดการให้นักเรียนทุกคนมีส่วนร่วมในกิจกรรมกลุ่มได้เสมอ นั่นเป็นจุดแข็งที่ดีมาก (ชม)\n\nครู A: 'ขอบคุณค่ะ'\n\nครู: 'เพื่อเพิ่มประสิทธิภาพในการเรียนรู้ ฉันขอแนะนำให้เราลองใช้เครื่องมือดิจิทัลสำหรับการประเมินผลในช่วงท้ายคาบเรียนดูสิคะ มันจะช่วยลดเวลาและทำให้คุณ A มีเวลาโฟกัสที่นักเรียนมากขึ้น (เสนอแนวทางที่วัดผลได้)\n\nครู A: 'น่าสนใจค่ะ ฉันจะลองศึกษาดู'\n\nครู: 'ยอดเยี่ยมเลยค่ะ ฉันเชื่อมั่นในวิธีการสอนของคุณเสมอ ขอให้สนุกกับการปรับปรุงนะคะ (ให้กำลังใจ)'",
                tips: [
                    "เลือกใช้ 'ฉัน/ผม' แทน 'เรา' ในประโยคที่ให้ข้อเสนอแนะเพื่อแสดงความรับผิดชอบต่อคำพูด",
                    "เริ่มต้นและจบด้วยการให้กำลังใจหรือการรับฟังเสมอ เพื่อให้บทสนทนาเป็นไปในทิศทางบวก",
                    "เมื่อเสนอแนะ ให้เน้นที่ 'พฤติกรรม' หรือ 'ผลลัพธ์ของงาน' ไม่ใช่ 'ตัวบุคคล'"
                ]
            };
        };

        // InputForm Component (same as previous)
        const InputForm = ({ onGenerate, isLoading }) => { /* ... */ 
            const [sender, setSender] = useState(SchoolRole.TEACHER);
            const [receiver, setReceiver] = useState(SchoolRole.STUDENT);
            const [purpose, setPurpose] = useState(Purpose.MOTIVATE);
            const [tone, setTone] = useState(Tone.SEMI_FORMAL_SPOKEN);
            const [format, setFormat] = useState(Format.FACE_TO_FACE);

            const handleSubmit = (e) => {
                e.preventDefault();
                onGenerate({ sender, receiver, purpose, tone, format });
            };

            const SelectGroup = ({ label, value, onChange, options }) => (
                <div className="w-full">
                    <label className="block text-primary-blue text-sm font-semibold mb-2">{label}</label>
                    <div className="relative">
                        <select value={value} onChange={(e) => onChange(e.target.value)} className="block appearance-none w-full bg-white border border-accent-sky hover:border-secondary-blue px-4 py-2 pr-8 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-secondary-blue focus:border-transparent transition duration-150 ease-in-out text-gray-700 cursor-pointer">
                            {Object.values(options).map((option) => (<option key={option} value={option}>{option}</option>))}
                        </select>
                        <div className="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-primary-blue">
                            <svg className="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
                        </div>
                    </div>
                </div>
            );

            return (
                <form onSubmit={handleSubmit} className="space-y-6 p-6 bg-white rounded-xl shadow-lg border border-gray-100">
                    <div className="flex flex-wrap -mx-3 mb-6">
                        <div className="w-full md:w-1/2 px-3 mb-6 md:mb-0"><SelectGroup label="ฉันคือใคร (ผู้ส่ง)" value={sender} onChange={setSender} options={SchoolRole} /></div>
                        <div className="w-full md:w-1/2 px-3"><SelectGroup label="ต้องการสื่อสารกับใคร (ผู้รับ)" value={receiver} onChange={setReceiver} options={SchoolRole} /></div>
                    </div>
                    <div className="w-full"><SelectGroup label="วัตถุประสงค์ในการสื่อสาร" value={purpose} onChange={setPurpose} options={Purpose} /></div>
                    <div className="flex flex-wrap -mx-3">
                        <div className="w-full md:w-1/2 px-3 mb-6 md:mb-0"><SelectGroup label="โทนและรูปแบบภาษา" value={tone} onChange={setTone} options={Tone} /></div>
                        <div className="w-full md:w-1/2 px-3"><SelectGroup label="ช่องทางการสื่อสาร" value={format} onChange={setFormat} options={Format} /></div>
                    </div>
                    <button type="submit" disabled={isLoading} className={`w-full py-3 rounded-xl text-white font-bold transition duration-300 ease-in-out flex justify-center items-center ${isLoading ? 'bg-secondary-blue/70 cursor-not-allowed' : 'bg-primary-blue hover:bg-secondary-blue shadow-md'}`}>
                        {isLoading ? (
                            <svg className="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"><circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4"></circle><path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path></svg>
                        ) : ('สร้างแนวทางการสื่อสาร ✨')}
                    </button>
                </form>
            );
        };

        // ResultCard Component (same as previous)
        const ResultCard = ({ result }) => { /* ... */ 
            if (!result) return null;
            const renderContent = (title, content) => (
                <div className="mb-6">
                    <h3 className="text-lg font-bold text-secondary-blue border-b-2 border-accent-sky pb-1 mb-2">{title}</h3>
                    <div className="whitespace-pre-line text-gray-800">{content}</div>
                </div>
            );
            return (
                <div className="bg-white p-6 rounded-xl shadow-lg border border-gray-100 mt-8">
                    <h2 className="text-2xl font-extrabold text-primary-blue mb-6">💡 แนวทางการสื่อสารที่แนะนำ</h2>
                    {renderContent("แนวคิด/หลักการ (Strategy)", result.strategy)}
                    {renderContent("คำพูด/ข้อความ (Script)", result.script)}
                    {renderContent("ตัวอย่างการสนทนา (Example)", result.example)}
                    <div className="mb-0">
                        <h3 className="text-lg font-bold text-secondary-blue border-b-2 border-accent-sky pb-1 mb-2">เคล็ดลับการสื่อสาร (Tips)</h3>
                        <ul className="list-disc list-inside space-y-1 text-gray-800">
                            {result.tips.map((tip, index) => (<li key={index}>{tip}</li>))}
                        </ul>
                    </div>
                </div>
            );
        };

        // Main App Component
        const App = () => {
            const [result, setResult] = useState(null);
            const [isLoading, setIsLoading] = useState(false);
            const [error, setError] = useState(null);

            // ⚠️ ไม่ต้องใส่ API Key ตรงนี้แล้ว เพราะเราใช้ Mock Data แทน ⚠️
            const handleGenerate = useCallback(async ({ sender, receiver, purpose, tone, format }) => {
                setIsLoading(true);
                setError(null);
                setResult(null);

                try {
                    // เรียกใช้ฟังก์ชันที่ส่งกลับ Mock Data
                    const guide = await generateCommunicationGuide(sender, receiver, purpose, tone, format);
                    setResult(guide);
                } catch (err) {
                    // หากเกิดข้อผิดพลาดในการโหลด Mock Data (ไม่น่าจะเกิดขึ้น)
                    setError("เกิดข้อผิดพลาดในการแสดงผลโหมดสาธิต: " + err.message);
                } finally {
                    setIsLoading(false);
                }
            }, []);

            return (
                <div className="min-h-screen bg-white-bg p-4 md:p-8">
                    <div className="max-w-4xl mx-auto">
                        
                        <header className="text-center py-8 mb-8">
                            <h1 className="text-4xl md:text-5xl font-extrabold text-primary-blue mb-2">Better Conversations, Better Culture</h1>
                            <h2 className="text-xl md:text-2xl font-semibold text-secondary-blue mb-4">สื่อสารให้ดี วัฒนธรรมองค์กรจะดีขึ้น</h2>
                            <p className="text-gray-600 font-bold text-lg p-2 bg-yellow-100 rounded-lg">
                                📣 โหมดสาธิต (DEMO MODE): โค้ดนี้ใช้งานได้ทันที แต่จะให้ผลลัพธ์ตัวอย่างชุดเดิมเสมอ 📣
                            </p>
                            <p className="text-gray-600 text-sm italic mt-2">Tagline: A supportive space for ideas and voices.</p>
                            <div className="mt-4 p-4 bg-accent-sky/20 rounded-lg text-primary-blue border-l-4 border-primary-blue">พื้นที่ที่ช่วยให้ผู้นำและทีมพูดคุยกันอย่างสร้างสรรค์ นำไปสู่วัฒนธรรมที่เข้มแข็งในโรงเรียนของคุณ</div>
                        </header>

                        <main>
                            <InputForm onGenerate={handleGenerate} isLoading={isLoading} />
                            
                            {error && (
                                <div className="mt-8 p-4 bg-red-100 border-l-4 border-red-500 text-red-700 rounded-lg" role="alert">
                                    <p className="font-bold">เกิดข้อผิดพลาด 🚨</p>
                                    <p>{error}</p>
                                </div>
                            )}

                            {result && <ResultCard result={result} />}
                        </main>
                        
                        <footer className="mt-10 p-4 border-t border-gray-300 text-center text-sm text-gray-500">
                             **วิธีเปิดใช้งาน AI เต็มรูปแบบ:** หากต้องการให้เว็บไซต์สร้างคำแนะนำใหม่ๆ ตามที่คุณเลือกได้ ให้คัดลอก **Gemini API Key** ของคุณไปวางแทนที่ Mock Data ในฟังก์ชัน `generateCommunicationGuide` ในโค้ด HTML นี้
                        </footer>
                    </div>
                </div>
            );
        };

        // App Entry Point
        const container = document.getElementById('root');
        if (container) {
            const root = ReactDOM.createRoot(container);
            root.render(<App />);
        }
    </script>
</body>
</html>
