import React, { useState, useEffect, useRef } from 'react';
import { initializeApp } from 'firebase/app';
import { getAuth, onAuthStateChanged, signInAnonymously, signInWithCustomToken } from 'firebase/auth';
import { getFirestore, collection, addDoc, onSnapshot, query, doc, setDoc } from 'firebase/firestore';
import { Calendar, Timer, BookOpen, Wind, CheckCircle2, Play, Pause, RotateCcw, Volume2, History, Info } from 'lucide-react';

// Konfigurasi Firebase dari Environment
const firebaseConfig = JSON.parse(__firebase_config);
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'zenflow-meditation';

const App = () => {
  const [user, setUser] = useState(null);
  const [activeTab, setActiveTab] = useState('timer');
  const [timerRunning, setTimerRunning] = useState(false);
  const [timeLeft, setTimeLeft] = useState(600);
  const [selectedDuration, setSelectedDuration] = useState(600);
  const [journalEntries, setJournalEntries] = useState([]);
  const [showExplanation, setShowExplanation] = useState(null);
  
  const audioRef = useRef(null);

  // Path file suara untuk GitHub (simpan bowl.mp3 di folder yang sama dengan file ini)
  const bowlPath = "./bowl.mp3";

  // 1. Inisialisasi Auth (Mandatory Rule 3)
  useEffect(() => {
    const initAuth = async () => {
      if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
        await signInWithCustomToken(auth, __initial_auth_token);
      } else {
        await signInAnonymously(auth);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, setUser);
    return () => unsubscribe();
  }, []);

  // 2. Fetch Data Jurnal (Mandatory Rule 1 & 2)
  useEffect(() => {
    if (!user) return;

    // Mengambil data jurnal dari path private user
    const journalRef = collection(db, 'artifacts', appId, 'users', user.uid, 'journal');
    
    const unsubscribe = onSnapshot(journalRef, (snapshot) => {
      const docs = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
      // Sorting manual di memori (Rule 2)
      const sorted = docs.sort((a, b) => b.timestamp - a.timestamp);
      setJournalEntries(sorted);
    }, (error) => {
      console.error("Firestore error:", error);
    });

    return () => unsubscribe();
  }, [user]);

  // 3. Logika Timer
  useEffect(() => {
    let interval;
    if (timerRunning && timeLeft > 0) {
      interval = setInterval(() => {
        setTimeLeft((prev) => prev - 1);
      }, 1000);
    } else if (timeLeft === 0 && timerRunning) {
      setTimerRunning(false);
      saveSession();
      playBowl();
    }
    return () => clearInterval(interval);
  }, [timerRunning, timeLeft]);

  const playBowl = () => {
    if (audioRef.current) {
      audioRef.current.currentTime = 10; // Mulai di detik ke-10 sesuai permintaan
      audioRef.current.play().catch(e => console.log("Audio play failed. Pastikan bowl.mp3 ada di root.", e));
    }
  };

  const toggleTimer = () => {
    if (!timerRunning) {
      playBowl();
      setTimerRunning(true);
    } else {
      setTimerRunning(false);
    }
  };

  const saveSession = async () => {
    if (!user) return;
    const now = new Date();
    const dateStr = now.toISOString().split('T')[0];
    const timeStr = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });

    try {
      const journalRef = collection(db, 'artifacts', appId, 'users', user.uid, 'journal');
      await addDoc(journalRef, {
        date: dateStr,
        time: timeStr,
        duration: selectedDuration / 60,
        timestamp: now.getTime(),
        type: "Sesi Meditasi"
      });
    } catch (err) {
      console.error("Gagal menyimpan jurnal:", err);
    }
  };

  const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60);
    const secs = seconds % 60;
    return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
  };

  // Render Kalender Sederhana
  const getAttendanceMap = () => {
    const map = {};
    journalEntries.forEach(entry => {
      map[entry.date] = true;
    });
    return map;
  };

  const renderCalendar = () => {
    const now = new Date();
    const daysInMonth = new Date(now.getFullYear(), now.getMonth() + 1, 0).getDate();
    const attendanceMap = getAttendanceMap();
    
    const days = [];
    for (let d = 1; d <= daysInMonth; d++) {
      const dateStr = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}-${String(d).padStart(2, '0')}`;
      const isAttended = attendanceMap[dateStr];
      const isToday = d === now.getDate();

      days.push(
        <div key={d} className={`h-10 w-10 flex flex-col items-center justify-center rounded-full border transition-all ${isAttended ? 'bg-orange-100 border-orange-400 text-orange-800' : 'border-stone-100 text-stone-400'} ${isToday ? 'ring-2 ring-orange-500' : ''}`}>
          <span className="text-xs font-sans">{d}</span>
          {isAttended && <div className="w-1 h-1 bg-orange-600 rounded-full mt-0.5 animate-pulse"></div>}
        </div>
      );
    }

    return <div className="grid grid-cols-7 gap-1 place-items-center">{days}</div>;
  };

  return (
    <div className="min-h-screen bg-[#FDFCF8] text-stone-800 font-serif pb-24">
      <div className="fixed top-0 left-0 w-full h-1.5 bg-orange-600 z-50"></div>
      
      {/* Audio Offline */}
      <audio ref={audioRef} src={bowlPath} preload="auto" />

      <header className="pt-12 pb-6 text-center">
        <div className="flex justify-center mb-2">
          <Wind className="text-orange-600" size={32} />
        </div>
        <h1 className="text-3xl font-light tracking-widest text-stone-700 uppercase">ZenFlow</h1>
        <p className="text-stone-400 italic text-xs font-sans">Kesadaran adalah kunci ketenangan.</p>
      </header>

      <main className="max-w-md mx-auto px-6">
        {/* Navigation */}
        <nav className="flex justify-around mb-6 bg-stone-100 p-1 rounded-2xl">
          {['timer', 'guide', 'journal'].map((t) => (
            <button key={t} onClick={() => setActiveTab(t)} className={`flex-1 py-2 rounded-xl text-xs font-sans uppercase tracking-tighter transition-all ${activeTab === t ? 'bg-white shadow text-orange-700 font-bold' : 'text-stone-500'}`}>
              {t === 'journal' ? 'Jurnal' : t}
            </button>
          ))}
        </nav>

        <div className="bg-white rounded-[2rem] p-8 shadow-xl border border-stone-100 min-h-[400px]">
          {activeTab === 'timer' && (
            <div className="flex flex-col items-center space-y-10 animate-in fade-in zoom-in">
              <div className={`w-48 h-48 rounded-full border-2 flex items-center justify-center transition-all duration-1000 ${timerRunning ? 'border-orange-400 scale-105' : 'border-stone-100'}`}>
                <div className="text-center">
                  <p className="text-5xl font-light font-sans text-stone-700">{formatTime(timeLeft)}</p>
                  <Volume2 size={12} className={`mx-auto mt-2 ${timerRunning ? 'text-orange-500 animate-pulse' : 'text-stone-300'}`} />
                </div>
              </div>

              <div className="flex items-center gap-6">
                <button onClick={toggleTimer} className={`w-16 h-16 rounded-full flex items-center justify-center shadow-lg transition-all ${timerRunning ? 'bg-stone-100 text-stone-600' : 'bg-orange-600 text-white'}`}>
                  {timerRunning ? <Pause size={28} /> : <Play size={28} className="ml-1" />}
                </button>
                <button onClick={() => { setTimerRunning(false); setTimeLeft(selectedDuration); }} className="w-12 h-12 rounded-full border border-stone-200 flex items-center justify-center text-stone-400 hover:bg-stone-50">
                  <RotateCcw size={20} />
                </button>
              </div>

              <div className="flex gap-2">
                {[300, 600, 900, 1200].map(s => (
                  <button key={s} onClick={() => { setSelectedDuration(s); setTimeLeft(s); setTimerRunning(false); }} className={`px-3 py-1 rounded-full text-[10px] border ${selectedDuration === s ? 'bg-orange-50 border-orange-200 text-orange-700' : 'border-stone-100 text-stone-400'}`}>
                    {s/60} Menit
                  </button>
                ))}
              </div>
            </div>
          )}

          {activeTab === 'guide' && (
            <div className="space-y-4 animate-in slide-in-from-right">
              <h2 className="text-lg font-medium border-b pb-2">Panduan Meditasi</h2>
              <div className="p-4 bg-stone-50 rounded-xl">
                <h3 className="font-bold text-orange-700 flex items-center gap-2"><Wind size={16}/> Samatha</h3>
                <p className="text-xs text-stone-600 mt-1 leading-relaxed">Fokus satu titik pada napas untuk menenangkan pikiran yang liar. Cocok untuk meredakan stres harian.</p>
              </div>
              <div className="p-4 bg-stone-50 rounded-xl">
                <h3 className="font-bold text-orange-700 flex items-center gap-2"><CheckCircle2 size={16}/> Vipassana</h3>
                <p className="text-xs text-stone-600 mt-1 leading-relaxed">Menyadari sensasi tubuh dan pikiran sebagaimana adanya untuk memahami sifat ketidakkekalan.</p>
              </div>
            </div>
          )}

          {activeTab === 'journal' && (
            <div className="space-y-6 animate-in slide-in-from-right">
              <h2 className="text-lg font-medium">Jurnal Kesadaran</h2>
              <div className="bg-stone-50/50 p-3 rounded-2xl border border-stone-100">
                {renderCalendar()}
              </div>
              <div className="space-y-3">
                <p className="text-[10px] uppercase tracking-widest text-stone-400 font-bold flex items-center gap-2"><History size={12}/> Riwayat Realtime</p>
                <div className="max-h-40 overflow-y-auto pr-2 space-y-2">
                  {journalEntries.length === 0 ? (
                    <p className="text-xs italic text-stone-400">Belum ada catatan.</p>
                  ) : (
                    journalEntries.slice(0, 10).map((entry) => (
                      <div key={entry.id} className="flex justify-between items-center p-2 border-b border-stone-50 text-[11px] font-sans">
                        <span className="text-stone-600 font-medium">{entry.date}</span>
                        <span className="text-stone-400">{entry.time}</span>
                        <span className="text-orange-600 bg-orange-50 px-2 py-0.5 rounded-full">{entry.duration}m</span>
                      </div>
                    ))
                  )}
                </div>
              </div>
            </div>
          )}
        </div>
      </main>

      {/* Footer User Info */}
      <footer className="fixed bottom-0 left-0 w-full p-4 bg-white/80 backdrop-blur-md text-center border-t border-stone-100">
        <p className="text-[9px] text-stone-300 font-sans uppercase tracking-[0.2em]">
          User ID: {user?.uid || 'Mempersiapkan...'}
        </p>
      </footer>
    </div>
  );
};

export default App;

