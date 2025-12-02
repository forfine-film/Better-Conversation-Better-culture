<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Better Conversations, Better Culture - โหมดสาธิต (ใช้งานได้ทันที)</title>
    
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
        
        // 🛑🛑🛑 ฟังก์ชันโหมดสาธิต: ไม่ใช้ API Key, ส่งกลับ Mock Data 🛑🛑🛑
        const generateCommunicationGuide = async (sender, receiver, purpose, tone, format) => {
            // จำลองการโหลด 1.5 วินาที
            await new Promise(resolve => setTimeout(resolve, 1500));

            // ข้อมูลตัวอย่างที่ถูกกำหนดไว้ล่วงหน้า
            return {
                strategy: "หลักการสื่อสารในสถานการณ์นี้คือ **การรับฟังอย่างลึกซึ้ง (Active Listening)** ตามด้วย **การสะท้อนความรู้สึก (Validation)** ก่อนที่จะนำเสนอแนวทางแก้ไขที่เน้นการเติบโตร่วมกัน (Growth-Oriented Solution)",
                script: "คุณ A: 'สวัสดีค่ะ/ครับ ฉันเห็นความตั้งใจในการทำงานของคุณ A มาตลอดนะ (แสดงความจริงใจ) ฉันอยากจะมาให้กำลังใจและคุยกันเรื่อง [หัวข้อ] สักหน่อย\n\n(ส่วนเนื้อหา) เพื่อให้งานของเราสำเร็จไปได้ด้วยดีมากขึ้น ฉันอยากจะลองเสนอแนวทางให้เราเพิ่ม [ขั้นตอน/เครื่องมือ] เข้าไปในกระบวนการทำงานของเราดูนะคะ\n\n(ส่วนปิดท้าย) ฉันพร้อมที่จะช่วยเหลือเต็มที่เลยนะ ถ้าติดขัดอะไรหรือต้องการคำแนะนำเพิ่มเติม อย่าลังเลที่จะส่งข้อความมาหาฉันได้ตลอดเลยนะ! 😊'",
                example: "ผอ.: 'อรุณสวัสดิ์ครับคุณครู B ผมขอเวลานอกห้องเรียน 5 นาทีได้ไหมครับ (ถามอย่างสุภาพ)\n\nครู B: 'ได้เลยค่ะท่าน'\n\nผอ.: 'ผมทราบว่าการประเมินโครงการวิจัยในครั้งนี้เป็นงานหนัก แต่ผมเห็นชัดเลยว่าคุณครูทุ่มเทมากจริงๆ (ชมเชยความพยายาม)\n\nครู B: 'ขอบคุณค่ะ'\n\nผอ.: 'มีข้อเสนอแนะเล็กน้อยครับ เพื่อให้การส่งรายงานครั้งหน้าเป็นไปอย่างราบรื่น ลองเพิ่มส่วนการสรุปผลเชิงตัวเลข (Data-Driven Summary) เข้าไปในบทนำดูสิครับ มันจะช่วยให้ผู้บริหารท่านอื่นเห็นภาพรวมได้เร็วขึ้นมาก'\n\nครู B: 'เป็นความคิดที่ดีค่ะ!'\n\nผอ.: 'ผมมั่นใจว่าคุณครูทำได้แน่นอนครับ ถ้ามีปัญหาเรื่องสถิติ มาคุยกับทีม ICT ได้เลยนะครับ! 💪'",
                tips: [
                    "รักษาระดับสายตาเมื่อพูดคุยต่อหน้า และใช้ภาษากายที่เปิดเผย (Open Body Language) เพื่อสร้างความสบายใจ",
                    "ตั้งคำถามปลายเปิด (Open-Ended Questions) เช่น 'คุณคิดว่าเราจะแก้ปัญหานี้ได้อย่างไร?' แทนการบอกวิธีแก้ปัญหาโดยตรง",
                    "กำหนดเวลาและสถานที่ที่เหมาะสมในการสื่อสาร โดยเฉพาะการให้ข้อเสนอแนะที่สร้างสรรค์ ควรทำในพื้นที่ส่วนตัว"
                ]
            };
        };

        // InputForm, ResultCard Components (ไม่เปลี่ยนแปลงจากฉบับก่อนหน้า)
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

        const InputForm = ({ onGenerate, isLoading }) => { 
            const [sender, setSender] = useState(SchoolRole.TEACHER);
            const [receiver, setReceiver] = useState(SchoolRole.STUDENT);
            const [purpose, setPurpose] = useState(Purpose.MOTIVATE);
            const [tone, setTone] = useState(Tone.SEMI_FORMAL_SPOKEN);
            const [format, setFormat] = useState(Format.FACE_TO_FACE);

            const handleSubmit = (e) => {
                e.preventDefault();
                onGenerate({ sender, receiver, purpose, tone, format });
            };

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

        const ResultCard = ({ result }) => { 
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

            const handleGenerate = useCallback(async (params) => {
                setIsLoading(true);
                setError(null);
                setResult(null);

                try {
                    // ใช้งานฟังก์ชัน Demo
                    const guide = await generateCommunicationGuide(params.sender, params.receiver, params.purpose, params.tone, params.format);
                    setResult(guide);
                } catch (err) {
                    setError("เกิดข้อผิดพลาดภายในโหมดสาธิต: " + err.message);
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
                                📣 โหมดสาธิต (DEMO MODE): โค้ดนี้ใช้งานได้ทันที 📣
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
                             **หมายเหตุ:** หากคุณต้องการผลลัพธ์ที่ปรับเปลี่ยนตามตัวเลือกที่เลือก (ใช้งาน AI เต็มรูปแบบ) คุณจะต้องไปสร้าง **Gemini API Key** ของคุณและนำไปวางแทนที่ฟังก์ชัน `generateCommunicationGuide` ในโค้ดนี้
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
