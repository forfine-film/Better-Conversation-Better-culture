<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Better Conversations, Better Culture - สื่อสารให้ดี วัฒนธรรมองค์กรจะดีขึ้น</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary-blue': '#1D4ED8', // Navy Blue
                        'secondary-blue': '#3B82F6', // Lighter Blue
                        'accent-sky': '#93C5FD', // Sky Blue
                        'white-bg': '#F9FAFB', // Light Gray/White Background
                    }
                }
            }
        }
    </script>
    
    <style>
        body {
            font-family: 'Sukhumvit Set', 'Kanit', sans-serif;
        }
    </style>
</head>
<body class="bg-white-bg">

    <div id="root"></div>

    <script type="text/babel">
        // ==========================================================
        // types.ts (TypeScript Definitions)
        // ==========================================================
        
        // กำหนด Enum สำหรับสถานะต่างๆ ในโรงเรียน
        const SchoolRole = {
            HIGH_EXECUTIVE: 'ผู้บริหารระดับสูง',
            PEER_EXECUTIVE: 'ผู้บริหารระดับเดียวกัน',
            SENIOR_TEACHER: 'หัวหน้างาน/ครูอาวุโส',
            TEACHER: 'ครู',
            PARENT: 'ผู้ปกครอง',
            STUDENT: 'นักเรียน',
            EVERYONE: 'ทุกคนในองค์กร',
        };

        // กำหนด Enum สำหรับวัตถุประสงค์ในการสื่อสาร
        const Purpose = {
            GIVE_FEEDBACK: 'ให้ข้อเสนอแนะที่สร้างสรรค์',
            RESOLVE_CONFLICT: 'ไกล่เกลี่ย/แก้ปัญหาความขัดแย้ง',
            SHARE_VISION: 'ถ่ายทอดวิสัยทัศน์/เป้าหมาย',
            ASK_FOR_HELP: 'ขอความช่วยเหลือ/การสนับสนุน',
            MOTIVATE: 'ให้กำลังใจ/สร้างแรงจูงใจ',
            ANNOUNCE_CHANGE: 'แจ้งการเปลี่ยนแปลง/นโยบายใหม่',
        };

        // กำหนด Enum สำหรับโทนภาษา
        const Tone = {
            FORMAL_WRITTEN: 'ภาษาเขียน (เป็นทางการ)',
            SEMI_FORMAL_SPOKEN: 'ภาษาสื่อสาร (กึ่งทางการ)',
            CASUAL_SPOKEN: 'ภาษาพูด (กันเอง)',
        };

        // กำหนด Enum สำหรับช่องทางการสื่อสาร
        const Format = {
            FACE_TO_FACE: 'พูดคุยต่อหน้า',
            EMAIL: 'อีเมล/ข้อความ',
            MEETING: 'การประชุมกลุ่ม',
        };

        // รูปแบบข้อมูลที่คาดหวังจาก Gemini API
        const CommunicationGuideSchema = {
            type: 'object',
            properties: {
                strategy: {
                    type: 'string',
                    description: 'แนวคิดและหลักการสื่อสารที่ควรใช้ (ภาษาไทย)',
                },
                script: {
                    type: 'string',
                    description: 'ข้อความ/คำพูดที่แนะนำให้ใช้ (ภาษาไทย) มีอิโมจิเล็กน้อย',
                },
                example: {
                    type: 'string',
                    description: 'ตัวอย่างสถานการณ์จำลองหรือบทสนทนาที่สอดคล้อง (ภาษาไทย)',
                },
                tips: {
                    type: 'array',
                    description: 'คำแนะนำเพิ่มเติมในการสื่อสาร (เช่น ท่าทาง น้ำเสียง เวลาที่เหมาะสม) (ภาษาไทย)',
                    items: {
                        type: 'string',
                    },
                },
            },
            required: ['strategy', 'script', 'example', 'tips'],
        };


        // ==========================================================
        // services/geminiService.ts (API Service)
        // ต้องมี Global Variable: GEMINI_API_KEY
        // ==========================================================

        const generateCommunicationGuide = async (sender, receiver, purpose, tone, format) => {
            const apiKey = window.GEMINI_API_KEY; // ใช้ Key จากตัวแปร Global
            if (!apiKey) {
                throw new Error("GEMINI_API_KEY is not set. Please set the API key in the code.");
            }

            const prompt = `
            คุณคือโค้ชด้านการสื่อสารมืออาชีพสำหรับสถาบันการศึกษา ภารกิจของคุณคือการสร้างแนวทางการสื่อสารที่เป็นธรรมชาติ มีความยาวพอสมควร (2-3 ย่อหน้า), มีตัวอย่างประกอบ, และเหมาะสมกับบริบทของโรงเรียน โดยต้องรวมอิโมจิเพื่อให้ข้อความน่าสนใจ

            **โจทย์:**
            1. **ผู้ส่ง (ฉันคือใคร):** ${sender}
            2. **ผู้รับ (ต้องการสื่อสารกับใคร):** ${receiver}
            3. **วัตถุประสงค์:** ${purpose}
            4. **โทนและรูปแบบภาษา:** ${tone}
            5. **ช่องทางการสื่อสาร:** ${format}

            **คำสั่งเพิ่มเติม:**
            * สร้างข้อความ/คำพูดที่ดูเป็นธรรมชาติและใช้ได้จริงในภาษาไทย
            * ความยาวของ 'script' และ 'example' ควรยาวพอสมควร โดยรวมกันประมาณ 150-200 คำ เพื่อให้มีรายละเอียด
            * ให้ผลลัพธ์เป็น JSON Object ที่ตรงตาม Schema ที่กำหนดเท่านั้น
            `;

            try {
                const response = await fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=' + apiKey, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{ role: "user", parts: [{ text: prompt }] }],
                        config: {
                            responseMimeType: "application/json",
                            responseSchema: CommunicationGuideSchema,
                        }
                    })
                });

                if (!response.ok) {
                    const errorBody = await response.json();
                    throw new Error(`API call failed: ${response.status} - ${errorBody.error.message}`);
                }

                const data = await response.json();
                
                // ตรวจสอบและแปลง JSON string ภายใน text เป็น Object
                if (data.candidates && data.candidates[0] && data.candidates[0].content.parts[0].text) {
                    const jsonString = data.candidates[0].content.parts[0].text;
                    return JSON.parse(jsonString);
                }

                throw new Error("Invalid response format from API.");

            } catch (error) {
                console.error("Error calling Gemini API:", error);
                // ส่ง Error กลับไปที่ Component
                throw new Error(error.message || "เกิดข้อผิดพลาดในการเชื่อมต่อกับ Gemini API");
            }
        };


        // ==========================================================
        // components/InputForm.tsx (Input Form Component)
        // ==========================================================

        const InputForm = ({ onGenerate, isLoading }) => {
            const [sender, setSender] = React.useState(SchoolRole.TEACHER);
            const [receiver, setReceiver] = React.useState(SchoolRole.STUDENT);
            const [purpose, setPurpose] = React.useState(Purpose.MOTIVATE);
            const [tone, setTone] = React.useState(Tone.SEMI_FORMAL_SPOKEN);
            const [format, setFormat] = React.useState(Format.FACE_TO_FACE);

            const handleSubmit = (e) => {
                e.preventDefault();
                onGenerate({ sender, receiver, purpose, tone, format });
            };

            const SelectGroup = ({ label, value, onChange, options }) => (
                <div className="w-full">
                    <label className="block text-primary-blue text-sm font-semibold mb-2">
                        {label}
                    </label>
                    <div className="relative">
                        <select
                            value={value}
                            onChange={(e) => onChange(e.target.value)}
                            className="block appearance-none w-full bg-white border border-accent-sky hover:border-secondary-blue px-4 py-2 pr-8 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-secondary-blue focus:border-transparent transition duration-150 ease-in-out text-gray-700 cursor-pointer"
                        >
                            {Object.values(options).map((option) => (
                                <option key={option} value={option}>{option}</option>
                            ))}
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
                        <div className="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                            <SelectGroup label="ฉันคือใคร (ผู้ส่ง)" value={sender} onChange={setSender} options={SchoolRole} />
                        </div>
                        <div className="w-full md:w-1/2 px-3">
                            <SelectGroup label="ต้องการสื่อสารกับใคร (ผู้รับ)" value={receiver} onChange={setReceiver} options={SchoolRole} />
                        </div>
                    </div>

                    <div className="w-full">
                        <SelectGroup label="วัตถุประสงค์ในการสื่อสาร" value={purpose} onChange={setPurpose} options={Purpose} />
                    </div>

                    <div className="flex flex-wrap -mx-3">
                        <div className="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                            <SelectGroup label="โทนและรูปแบบภาษา" value={tone} onChange={setTone} options={Tone} />
                        </div>
                        <div className="w-full md:w-1/2 px-3">
                            <SelectGroup label="ช่องทางการสื่อสาร" value={format} onChange={setFormat} options={Format} />
                        </div>
                    </div>

                    <button
                        type="submit"
                        disabled={isLoading}
                        className={`w-full py-3 rounded-xl text-white font-bold transition duration-300 ease-in-out flex justify-center items-center ${
                            isLoading ? 'bg-secondary-blue/70 cursor-not-allowed' : 'bg-primary-blue hover:bg-secondary-blue shadow-md'
                        }`}
                    >
                        {isLoading ? (
                            <svg className="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                                <circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4"></circle>
                                <path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                            </svg>
                        ) : (
                            'สร้างแนวทางการสื่อสาร ✨'
                        )}
                    </button>
                </form>
            );
        };


        // ==========================================================
        // components/ResultCard.tsx (Result Display Component)
        // ==========================================================

        const ResultCard = ({ result }) => {
            const [isExpanded, setIsExpanded] = React.useState(false);

            if (!result) return null;

            const toggleExpand = () => setIsExpanded(!isExpanded);

            const renderContent = (title, content) => (
                <div className="mb-6">
                    <h3 className="text-lg font-bold text-secondary-blue border-b-2 border-accent-sky pb-1 mb-2">
                        {title}
                    </h3>
                    <div className="whitespace-pre-line text-gray-800">
                        {content}
                    </div>
                </div>
            );

            return (
                <div className="bg-white p-6 rounded-xl shadow-lg border border-gray-100 mt-8">
                    <h2 className="text-2xl font-extrabold text-primary-blue mb-4">
                        💡 แนวทางการสื่อสารที่แนะนำ
                    </h2>
                    
                    {renderContent("แนวคิด/หลักการ (Strategy)", result.strategy)}
                    
                    {renderContent("คำพูด/ข้อความ (Script)", result.script)}

                    {renderContent("ตัวอย่างการสนทนา (Example)", result.example)}
                    
                    <div className="mb-6">
                        <h3 className="text-lg font-bold text-secondary-blue border-b-2 border-accent-sky pb-1 mb-2">
                            เคล็ดลับการสื่อสาร (Tips)
                        </h3>
                        <ul className="list-disc list-inside space-y-1 text-gray-800">
                            {result.tips.map((tip, index) => (
                                <li key={index}>{tip}</li>
                            ))}
                        </ul>
                    </div>

                    <button
                        onClick={toggleExpand}
                        className="w-full mt-4 py-2 text-sm font-semibold text-secondary-blue border border-secondary-blue rounded-lg hover:bg-secondary-blue hover:text-white transition duration-200"
                    >
                        {isExpanded ? 'ย่อรายละเอียด ⬆️' : 'ขยายเพื่อดูรายละเอียดทั้งหมด ⬇️'}
                    </button>
                </div>
            );
        };


        // ==========================================================
        // App.tsx (Main Application Component)
        // ==========================================================
        
        const App = () => {
            const { useState } = React;
            const [result, setResult] = useState(null);
            const [isLoading, setIsLoading] = useState(false);
            const [error, setError] = useState(null);

            // **สำคัญ: กรุณาใส่ Gemini API Key ของคุณที่นี่**
            // คุณสามารถรับ Key ได้จาก Google AI Studio
            window.GEMINI_API_KEY = "YOUR_GEMINI_API_KEY_HERE"; // <-- เปลี่ยนตรงนี้!

            const handleGenerate = async ({ sender, receiver, purpose, tone, format }) => {
                setIsLoading(true);
                setError(null);
                setResult(null);

                if (window.GEMINI_API_KEY === "YOUR_GEMINI_API_KEY_HERE") {
                    setError("กรุณาใส่ Gemini API Key ของคุณในโค้ด (บรรทัดที่ 400 โดยประมาณ) ก่อนใช้งาน");
                    setIsLoading(false);
                    return;
                }

                try {
                    const guide = await generateCommunicationGuide(sender, receiver, purpose, tone, format);
                    setResult(guide);
                } catch (err) {
                    setError(err.message);
                } finally {
                    setIsLoading(false);
                }
            };

            return (
                <div className="min-h-screen bg-white-bg p-4 md:p-8">
                    <div className="max-w-4xl mx-auto">
                        
                        <header className="text-center py-8 mb-8">
                            <h1 className="text-4xl md:text-5xl font-extrabold text-primary-blue mb-2">
                                Better Conversations, Better Culture
                            </h1>
                            <h2 className="text-xl md:text-2xl font-semibold text-secondary-blue mb-4">
                                สื่อสารให้ดี วัฒนธรรมองค์กรจะดีขึ้น
                            </h2>
                            <p className="text-gray-600 text-sm italic">
                                Tagline: A supportive space for ideas and voices.
                            </p>
                            <div className="mt-4 p-4 bg-accent-sky/20 rounded-lg text-primary-blue border-l-4 border-primary-blue">
                                พื้นที่ที่ช่วยให้ผู้นำและทีมพูดคุยกันอย่างสร้างสรรค์ นำไปสู่วัฒนธรรมที่เข้มแข็งในโรงเรียนของคุณ
                            </div>
                        </header>

                        <main>
                            <InputForm onGenerate={handleGenerate} isLoading={isLoading} />
                            
                            {error && (
                                <div className="mt-8 p-4 bg-red-100 border-l-4 border-red-500 text-red-700 rounded-lg" role="alert">
                                    <p className="font-bold">เกิดข้อผิดพลาด 🚨</p>
                                    <p>{error}</p>
                                    <p className="text-sm mt-1">
                                        **โปรดตรวจสอบ:** 1) คุณได้ใส่ API Key แล้วหรือยัง 2) API Key ของคุณถูกต้องหรือไม่ และ 3) เครือข่ายอินเทอร์เน็ตของคุณใช้งานได้หรือไม่
                                    </p>
                                </div>
                            )}

                            {result && <ResultCard result={result} />}

                        </main>
                    </div>
                </div>
            );
        };


        // ==========================================================
        // index.tsx (App Entry Point)
        // ==========================================================
        
        const container = document.getElementById('root');
        if (container) {
            const root = ReactDOM.createRoot(container);
            root.render(<App />);
        }
    </script>
</body>
</html># Better-Conversation-Better-culture
