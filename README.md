import React, { useState, useEffect } from 'react';
import { Heart, Sun, Coffee, Sparkles, MessageCircle, Music, Star, ArrowRight } from 'lucide-react';

const AviaMorningApp = () => {
  const [activeTab, setActiveTab] = useState('home');
  const [coffeeProgress, setCoffeeProgress] = useState(0);
  const [aiResponse, setAiResponse] = useState('');
  const [isTyping, setIsTyping] = useState(false);
  const [mood, setMood] = useState(null);

  // מילון המחמאות של "הבינה המלאכותית"
  const aiCompliments = [
    "ניתוח נתונים הושלם: רמת היופי של אביה הבוקר חורגת מהסקאלה.",
    "סריקת מערכת: החיוך של אביה הוא מקור האנרגיה החלופי היעיל ביותר בעולם.",
    "התראה: זוהתה רמת חמידות בלתי חוקית. נא להמשיך כך.",
    "חישוב הסתברות: הסיכוי שהיום שלך יהיה מושלם עומד על 99.9%.",
    "עובדה יומית: את הסיבה שהשמש החליטה לזרוח גם היום.",
    "סטטוס נוכחי: מלכת העולם. נא לשתות קפה בהתאם."
  ];

  const handleCoffeeMake = () => {
    let progress = 0;
    const interval = setInterval(() => {
      progress += 5;
      setCoffeeProgress(progress);
      if (progress >= 100) {
        clearInterval(interval);
      }
    }, 50);
  };

  const generateAICompliment = () => {
    setIsTyping(true);
    setAiResponse('');
    
    setTimeout(() => {
      const randomCompliment = aiCompliments[Math.floor(Math.random() * aiCompliments.length)];
      setAiResponse(randomCompliment);
      setIsTyping(false);
    }, 1500);
  };

  const renderContent = () => {
    switch (activeTab) {
      case 'home':
        return (
          <div className="space-y-6 text-center animate-fadeIn">
            <div className="bg-white/80 backdrop-blur-sm p-6 rounded-3xl shadow-xl border border-pink-100">
              <Sun className="w-16 h-16 text-yellow-400 mx-auto mb-4 animate-bounce" />
              <h1 className="text-3xl font-bold text-gray-800 mb-2">בוקר טוב אביה! ❤️</h1>
              <p className="text-gray-600">המערכת מוכנה להתחיל את היום שלך.</p>
              
              <div className="mt-8 grid grid-cols-2 gap-4">
                <button onClick={() => setActiveTab('coffee')} className="p-4 bg-orange-50 rounded-2xl hover:bg-orange-100 transition flex flex-col items-center gap-2 shadow-sm">
                  <Coffee className="text-orange-500" />
                  <span className="font-medium text-gray-700">קפה וירטואלי</span>
                </button>
                <button onClick={() => setActiveTab('ai')} className="p-4 bg-purple-50 rounded-2xl hover:bg-purple-100 transition flex flex-col items-center gap-2 shadow-sm">
                  <Sparkles className="text-purple-500" />
                  <span className="font-medium text-gray-700">Avia AI</span>
                </button>
                <button onClick={() => setActiveTab('mood')} className="p-4 bg-blue-50 rounded-2xl hover:bg-blue-100 transition flex flex-col items-center gap-2 shadow-sm">
                  <MessageCircle className="text-blue-500" />
                  <span className="font-medium text-gray-700">מד מצב רוח</span>
                </button>
                <button onClick={() => setActiveTab('fortune')} className="p-4 bg-pink-50 rounded-2xl hover:bg-pink-100 transition flex flex-col items-center gap-2 shadow-sm">
                  <Star className="text-pink-500" />
                  <span className="font-medium text-gray-700">מסר יומי</span>
                </button>
              </div>
            </div>
          </div>
        );

      case 'coffee':
        return (
          <div className="text-center space-y-6 animate-fadeIn">
            <div className="bg-white/90 p-8 rounded-3xl shadow-lg">
              <h2 className="text-2xl font-bold text-gray-800 mb-4">הקפה של הבוקר ☕</h2>
              <div className="h-48 w-32 mx-auto bg-gray-100 rounded-b-2xl border-4 border-gray-300 relative overflow-hidden mb-6">
                <div 
                  className="absolute bottom-0 left-0 right-0 bg-amber-700 transition-all duration-300 ease-out opacity-80"
                  style={{ height: `${coffeeProgress}%` }}
                >
                   {coffeeProgress > 90 && (
                     <div className="absolute top-0 left-0 right-0 h-4 bg-amber-200 opacity-50 blur-sm animate-pulse"></div>
                   )}
                </div>
                <div className="absolute top-1/2 left-0 right-0 text-center z-10">
                   {coffeeProgress === 0 && <span className="text-gray-400 text-sm">ריק...</span>}
                </div>
              </div>
              
              {coffeeProgress < 100 ? (
                <button 
                  onClick={handleCoffeeMake}
                  className="w-full bg-amber-600 text-white py-3 rounded-xl font-bold hover:bg-amber-700 transition shadow-lg transform active:scale-95"
                >
                  הכיני לי קפה
                </button>
              ) : (
                <div className="animate-pulse text-amber-700 font-bold text-lg">
                  הקפה מוכן נסיכה! תזהרי זה חם 🔥
                </div>
              )}
            </div>
            <button onClick={() => setActiveTab('home')} className="text-gray-500 flex items-center justify-center gap-2 mx-auto hover:text-gray-700">
              חזרה לתפריט
            </button>
          </div>
        );

      case 'ai':
        return (
          <div className="space-y-4 animate-fadeIn">
            <div className="bg-white/90 p-6 rounded-3xl shadow-lg min-h-[300px] flex flex-col">
              <div className="flex items-center gap-3 mb-6 border-b pb-4">
                <div className="w-10 h-10 bg-gradient-to-tr from-purple-500 to-pink-500 rounded-full flex items-center justify-center text-white">
                  <Sparkles size={20} />
                </div>
                <div>
                  <h2 className="font-bold text-gray-800">Avia GPT 4.0</h2>
                  <p className="text-xs text-green-500 flex items-center gap-1">
                    <span className="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span>
                    מחובר ללב שלך
                  </p>
                </div>
              </div>

              <div className="flex-1 bg-gray-50 rounded-2xl p-4 mb-4 relative overflow-hidden">
                {aiResponse ? (
                  <p className="text-gray-700 leading-relaxed font-medium">
                    {aiResponse}
                  </p>
                ) : (
                  <div className="flex flex-col items-center justify-center h-full text-gray-400 text-sm">
                    <Sparkles className="mb-2 opacity-50" />
                    ממתין לפקודה...
                  </div>
                )}
                
                {isTyping && (
                  <div className="absolute bottom-4 left-4 flex gap-1">
                    <span className="w-2 h-2 bg-purple-400 rounded-full animate-bounce"></span>
                    <span className="w-2 h-2 bg-purple-400 rounded-full animate-bounce delay-75"></span>
                    <span className="w-2 h-2 bg-purple-400 rounded-full animate-bounce delay-150"></span>
                  </div>
                )}
              </div>

              <button 
                onClick={generateAICompliment}
                disabled={isTyping}
                className="w-full bg-gradient-to-r from-purple-600 to-pink-600 text-white py-3 rounded-xl font-bold shadow-lg transform active:scale-95 transition hover:shadow-xl disabled:opacity-70"
              >
                {aiResponse ? 'עוד עובדה עליי' : 'נתח את המצב שלי'}
              </button>
            </div>
            <button onClick={() => setActiveTab('home')} className="text-gray-500 flex items-center justify-center gap-2 mx-auto">
              חזרה לתפריט
            </button>
          </div>
        );

      case 'mood':
        return (
          <div className="space-y-4 animate-fadeIn">
            <div className="bg-white/90 p-6 rounded-3xl shadow-lg text-center">
              <h2 className="text-2xl font-bold text-gray-800 mb-6">איך קמת הבוקר? 😴</h2>
              
              {!mood ? (
                <div className="grid grid-cols-2 gap-4">
                  <button onClick={() => setMood('tired')} className="p-4 border-2 border-gray-100 rounded-2xl hover:border-blue-300 hover:bg-blue-50 transition">
                    <div className="text-4xl mb-2">🥱</div>
                    <div className="font-medium text-gray-600">גמורה מעייפות</div>
                  </button>
                  <button onClick={() => setMood('happy')} className="p-4 border-2 border-gray-100 rounded-2xl hover:border-yellow-300 hover:bg-yellow-50 transition">
                    <div className="text-4xl mb-2">🤩</div>
                    <div className="font-medium text-gray-600">אנרגטית</div>
                  </button>
                  <button onClick={() => setMood('grumpy')} className="p-4 border-2 border-gray-100 rounded-2xl hover:border-red-300 hover:bg-red-50 transition">
                    <div className="text-4xl mb-2">😤</div>
                    <div className="font-medium text-gray-600">אל תדברו איתי</div>
                  </button>
                  <button onClick={() => setMood('love')} className="p-4 border-2 border-gray-100 rounded-2xl hover:border-pink-300 hover:bg-pink-50 transition">
                    <div className="text-4xl mb-2">🥰</div>
                    <div className="font-medium text-gray-600">מאוהבת בך</div>
                  </button>
                </div>
              ) : (
                <div className="py-8 animate-fadeInUp">
                  <div className="text-6xl mb-4">
                    {mood === 'tired' && '☕'}
                    {mood === 'happy' && '✨'}
                    {mood === 'grumpy' && '🍫'}
                    {mood === 'love' && '❤️'}
                  </div>
                  <h3 className="text-xl font-bold text-gray-800 mb-2">
                    {mood === 'tired' && 'המרשם: קפה כפול וחיבוק ממני בערב.'}
                    {mood === 'happy' && 'ישש! איזה כיף שהתחלת ככה את היום!'}
                    {mood === 'grumpy' && 'אוקיי, שולח לך שוקולד וירטואלי ושקט תעשייתי.'}
                    {mood === 'love' && 'גם אני מאוהב בך! יום מושלם שיהיה!'}
                  </h3>
                  <button onClick={() => setMood(null)} className="mt-6 text-blue-500 underline text-sm">שני סטטוס</button>
                </div>
              )}
            </div>
            <button onClick={() => setActiveTab('home')} className="text-gray-500 flex items-center justify-center gap-2 mx-auto">
              חזרה לתפריט
            </button>
          </div>
        );
        
      case 'fortune':
        return (
          <div className="space-y-4 animate-fadeIn">
             <div className="bg-gradient-to-br from-indigo-500 to-purple-700 p-8 rounded-3xl shadow-lg text-white text-center min-h-[300px] flex flex-col justify-center items-center relative overflow-hidden">
                <Star className="absolute top-4 right-4 text-white/20 w-12 h-12 animate-spin-slow" />
                <div className="absolute top-0 left-0 w-full h-full bg-[url('https://www.transparenttextures.com/patterns/stardust.png')] opacity-30"></div>
                
                <h2 className="text-2xl font-bold mb-6 relative z-10">המסר היומי לאביה</h2>
                <div className="bg-white/10 backdrop-blur-md p-6 rounded-xl border border-white/20 relative z-10">
                  <p className="text-lg leading-relaxed font-light">
                    "היום זה יום מצוין להזכיר לעצמך שאת מסוגלת להרבה יותר ממה שנדמה לך. והכי חשוב - את לא לבד, יש מישהו שחושב עלייך ברגע זה ממש."
                  </p>
                </div>
                <div className="mt-8 text-sm opacity-70">נכתב במיוחד בשבילך</div>
             </div>
             <button onClick={() => setActiveTab('home')} className="text-gray-500 flex items-center justify-center gap-2 mx-auto">
              חזרה לתפריט
            </button>
          </div>
        )

      default:
        return null;
    }
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-100 to-blue-100 p-4 font-sans" dir="rtl">
      <div className="max-w-md mx-auto min-h-[600px] flex flex-col">
        {/* Header */}
        <div className="flex justify-between items-center mb-6 pt-2 px-2">
          <div className="flex items-center gap-2">
            <div className="w-8 h-8 bg-pink-500 rounded-full flex items-center justify-center text-white font-bold text-xs">A</div>
            <span className="font-bold text-gray-700 text-sm">AviaOS 1.0</span>
          </div>
          <div className="text-xs text-gray-500 bg-white/50 px-3 py-1 rounded-full">
            {new Date().toLocaleTimeString('he-IL', { hour: '2-digit', minute: '2-digit' })}
          </div>
        </div>

        {/* Main Content Area */}
        <div className="flex-1 relative">
          {renderContent()}
        </div>

        {/* Bottom Bar */}
        <div className="mt-8 text-center pb-6">
          <p className="text-xs text-gray-400 flex items-center justify-center gap-1">
            Developed with <Heart size={12} className="text-red-500 fill-red-500" /> specifically for her
          </p>
        </div>
      </div>
      
      <style>{`
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(10px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fadeIn {
          animation: fadeIn 0.5s ease-out forwards;
        }
        .animate-spin-slow {
            animation: spin 8s linear infinite;
        }
        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
      `}</style>
    </div>
  );
};

export default AviaMorningApp;


