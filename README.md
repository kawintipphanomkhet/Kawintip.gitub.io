<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบสารสนเทศ - Paramedic Student SCPHUB</title>
    <meta name="description" content="วิทยาลัยการสาธารณสุขสิรินธร จังหวัดอุบลราชธานี">
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <script src="https://resource.trickle.so/vendor_lib/unpkg/react@18/umd/react.production.min.js"></script>
    <script src="https://resource.trickle.so/vendor_lib/unpkg/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://resource.trickle.so/vendor_lib/unpkg/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>

    <style type="text/tailwindcss">
    @layer theme {
        :root {
            --cra-dark-blue: #091524; 
            --cra-menu-blue: #102a5e; 
            --cra-orange: #ff5e00; 
            --cra-orange-light: #ff8c42; 
            --footer-blue: #003876;
            --footer-orange: #ff6600;
        }
    }
    @layer base {
        html, body, #root {
            height: 100%;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Prompt', sans-serif;
            background-color: #f4f7f9;
        }
    }
    ::-webkit-scrollbar { width: 8px; }
    ::-webkit-scrollbar-track { background: #f1f1f1; }
    ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
    ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    .overflow-x-auto::-webkit-scrollbar { display: none; }
    @keyframes fadeInUp {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }
    .animate-fade-in-up {
        animation: fadeInUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }
    </style>
</head>
<body>
    <div id="root"></div>
    
    <script type="text/babel">
        const { useState } = React;

        const Header = ({ currentPage, setCurrentPage }) => {
            const topMenuLinks = [
                "บุคลากร", "ผู้สนใจเข้าศึกษา", "นักศึกษาปัจจุบัน", 
                "ศิษย์เก่า", "ระบบสารสนเทศ", "ดาวน์โหลดเอกสาร", "ร้องเรียน/ข้อเสนอแนะ"
            ];
            const bottomMenuLinks = [
                "หน้าแรก", "เกี่ยวกับเรา", "หลักสูตร", "การจัดการศึกษา", 
                "กิจกรรมนักศึกษา", "ข่าวสารและประกาศ", "ติดต่อเรา"
            ];

            return (
                <header className="relative w-full z-50 min-w-[1200px]">
                    <div className="bg-gradient-to-r from-[var(--cra-dark-blue)] to-[#112540] h-[44px] flex items-center pr-8 w-full border-b border-white/10 shadow-sm">
                        <div className="w-[calc(8%+210px)]"></div>
                        
                        <div className="flex-1 flex justify-start pl-[170px]"> 
                            <div className="flex items-center h-full text-white/80 text-[13px] font-light tracking-wide">
                                {topMenuLinks.map((link, index) => {
                                    const isActive = currentPage === link;
                                    return (
                                        <div key={index} className="flex items-center h-full relative group">
                                            <button 
                                                onClick={() => setCurrentPage(link)}
                                                className={`relative py-1 text-left transition-all duration-300 ${index === 0 ? 'pr-4' : 'px-4'} ${
                                                    isActive 
                                                    ? 'text-[var(--cra-orange-light)] font-medium' 
                                                    : 'hover:text-white text-white/70'
                                                }`}
                                            >
                                                {link}
                                            </button>
                                            {index < topMenuLinks.length - 1 && (
                                                <span className="text-white/20 text-[11px] font-extralight select-none">|</span>
                                            )}
                                        </div>
                                    )
                                })}
                            </div>
                        </div>

                        <div className="flex items-center ml-auto gap-3">
                            {['Facebook', 'Line', 'YouTube'].map((social, idx) => (
                                <a key={idx} href="#" className="text-white/60 hover:text-[var(--cra-orange-light)] hover:scale-110 transition-all duration-300">
                                    {idx === 0 && <svg className="w-[18px] h-[18px]" fill="currentColor" viewBox="0 0 24 24"><path d="M22.675 0h-21.35c-.732 0-1.325.593-1.325 1.325v21.351c0 .731.593 1.324 1.325 1.324h11.495v-9.294h-3.128v-3.622h3.128v-2.671c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.795.143v3.24l-1.918.001c-1.504 0-1.795.715-1.795 1.763v2.313h3.587l-.467 3.622h-3.12v9.293h6.116c.73 0 1.323-.593 1.323-1.325v-21.35c0-.732-.593-1.325-1.325-1.325z"/></svg>}
                                    {idx === 1 && <svg className="w-[18px] h-[18px]" fill="currentColor" viewBox="0 0 24 24"><path d="M24 10.304c0-5.369-5.383-9.738-12-9.738-6.616 0-12 4.369-12 9.738 0 4.814 4.269 8.846 10.036 9.608.391.084.922.258 1.057.592.122.303.079.778.039 1.085l-.171 1.027c-.053.303-.242 1.186 1.039.647 1.281-.54 6.911-4.069 9.428-6.967 1.739-1.907 2.572-3.843 2.572-5.992zm-18.988 2.595h-2.604c-.334 0-.606-.272-.606-.606v-3.705c0-.334.272-.606.606-.606h2.604c.334 0 .605.272.605.606v1.246h-1.999v1.213h1.999v1.246c0 .334-.271.606-.605.606zm3.328 0h-1.298c-.334 0-.606-.272-.606-.606v-3.705c0-.334.272-.606.606-.606h1.298c.333 0 .605.272.605.606v3.705c0 .334-.272.606-.605.606zm6.348 0h-1.332c-.179 0-.348-.078-.466-.214l-2.072-2.394v2.002c0 .334-.272.606-.606.606h-1.298c-.334 0-.606-.272-.606-.606v-3.705c0-.334.272-.606.606-.606h1.331c.179 0 .348.078.466.214l2.072 2.394v-2.002c0-.334.272-.606.606-.606h1.299c.333 0 .605.272.605.606v3.705c0 .334-.272.606-.605.606zm5.823-2.459h-1.999v1.213h1.999c.334 0 .606.272.606.606v.034c0 .334-.272.606-.606.606h-2.604c-.334 0-.606-.272-.606-.606v-3.705c0-.334.272-.606.606-.606h2.604c.334 0 .606.272.606.606v.034c0 .334-.272.606-.606.606h-1.999v1.213z"/></svg>}
                                    {idx === 2 && <svg className="w-[18px] h-[18px]" fill="currentColor" viewBox="0 0 24 24"><path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/></svg>}
                                </a>
                            ))}
                            <button className="bg-white/10 backdrop-blur-md text-white border border-white/20 rounded-full w-[30px] h-[30px] ml-1 flex items-center justify-center font-semibold text-[11px] hover:bg-gradient-to-r hover:from-[var(--cra-orange)] hover:to-[#ff7a29] hover:border-transparent transition-all duration-300 shadow-sm hover:shadow-[0_0_10px_rgba(255,94,0,0.5)]">
                                EN
                            </button>
                        </div>
                    </div>

                    <div className="bg-white/90 backdrop-blur-xl h-[65px] flex items-center pr-8 border-b border-gray-200/60 shadow-[0_10px_30px_-10px_rgba(0,0,0,0.05)] w-full relative z-40">
                        <div className="w-[calc(8%+210px)]"></div>

                        <nav className="flex-1 flex items-center h-full w-full justify-between pl-[170px]">
                            <div className="flex items-center h-full">
                                {bottomMenuLinks.map((link, index) => {
                                    const isActive = currentPage === link;
                                    return (
                                        <div key={index} className="flex items-center h-full relative group">
                                            <button 
                                                onClick={() => setCurrentPage(link)}
                                                className={`text-[var(--cra-menu-blue)] font-medium text-[15px] transition-all duration-300 hover:text-[var(--cra-orange)] h-full flex items-center ${
                                                    index === 0 ? 'pr-5' : 'px-5'
                                                } ${isActive ? 'text-[var(--cra-orange)] font-semibold' : ''}`}
                                            >
                                                {link}
                                            </button>
                                            {isActive && (
                                                <span className="absolute bottom-[10px] left-1/2 -translate-x-1/2 w-1.5 h-1.5 rounded-full bg-[var(--cra-orange)] shadow-[0_0_8px_rgba(255,94,0,0.8)]"></span>
                                            )}
                                        </div>
                                    )
                                })}
                            </div>
                            
                            <div className="ml-auto pl-5 border-l border-gray-200/60 h-[30px] flex items-center">
                                <button className="text-gray-400 hover:text-[var(--cra-orange)] hover:scale-110 transition-all duration-300 bg-gray-50 hover:bg-orange-50 p-2 rounded-full" aria-label="Search">
                                    <svg className="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" strokeWidth="2">
                                        <path strokeLinecap="round" strokeLinejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                                    </svg>
                                </button>
                            </div>
                        </nav>
                    </div>

                    <div className="absolute top-0 left-[8%] w-[220px] h-[145px] bg-gradient-to-b from-[var(--cra-dark-blue)] to-[#152a45] flex flex-col items-center justify-center shadow-[0_15px_40px_rgba(11,26,46,0.35)] rounded-b-2xl border-t-0 border-x border-b border-white/10 z-50">
                        <div className="relative group p-1 mb-1">
                            <div className="absolute inset-0 bg-[var(--cra-orange)] blur-2xl opacity-0 group-hover:opacity-30 transition-opacity duration-500 rounded-full"></div>
                            <img 
                                src="app-icon.png" 
                                alt="Paramedic SCPHUB Logo" 
                                className="relative w-[88px] h-[88px] object-contain drop-shadow-[0_8px_16px_rgba(0,0,0,0.4)] transition-transform duration-500 group-hover:scale-105" 
                            />
                        </div>
                        <div className="text-center z-10">
                            <div className="text-[13px] font-bold tracking-[0.08em] bg-clip-text text-transparent bg-gradient-to-r from-[#ff9d
