import React, { useState, useEffect, useCallback, useRef } from 'react';
import { 
  Play, BookOpen, Keyboard, MousePointerClick, Shuffle, 
  RotateCcw, Check, X, Heart, Pause, Zap, Clock, 
  ArrowLeft, Home, Trophy, Star, Moon, Sun, Award, BarChart3, Settings,
  Globe, Cloud, CloudOff, Volume2, Bookmark, Flame, Gift, ShoppingBag, Shield, Crown, UserCog, Lock, Swords, Users
} from 'lucide-react';

// --- Firebase 雲端模組引入 ---
import { initializeApp } from 'firebase/app';
import { getAuth, signInWithCustomToken, signInAnonymously, onAuthStateChanged } from 'firebase/auth';
import { getFirestore, collection, doc, setDoc, getDoc, updateDoc, onSnapshot } from 'firebase/firestore';

// ==========================================
// 0. Firebase 初始化 (安全機制)
// ==========================================
let app, auth, db, appId;
try {
  if (typeof __firebase_config !== 'undefined') {
    const firebaseConfig = JSON.parse(__firebase_config);
    app = initializeApp(firebaseConfig);
    auth = getAuth(app);
    db = getFirestore(app);
    appId = typeof __app_id !== 'undefined' ? __app_id : 'boyo-800-app';
  } else {
    // 💡 Netlify 部署提示：將您的 Firebase 專案設定貼在這裡
    /*
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    app = initializeApp(firebaseConfig);
    auth = getAuth(app);
    db = getFirestore(app);
    appId = 'boyo-800-app';
    */
  }
} catch (e) {
  console.warn("Firebase 未初始化，將以單機模式運行");
}

// ==========================================
// 1. 遊戲資料與常數設定
// ==========================================
const VOCABULARY = {
  1: [
    { en: "apple", zh: "蘋果" }, { en: "book", zh: "書本" }, 
    { en: "cat", zh: "貓" }, { en: "dog", zh: "狗" }, 
    { en: "egg", zh: "蛋" }, { en: "fish", zh: "魚" },
    { en: "girl", zh: "女孩" }, { en: "hand", zh: "手" },
    { en: "ice", zh: "冰" }, { en: "juice", zh: "果汁" }
  ],
  2: [
    { en: "key", zh: "鑰匙" }, { en: "lion", zh: "獅子" },
    { en: "monkey", zh: "猴子" }, { en: "nose", zh: "鼻子" },
    { en: "orange", zh: "橘子" }, { en: "pig", zh: "豬" },
    { en: "queen", zh: "皇后" }, { en: "rabbit", zh: "兔子" },
    { en: "sun", zh: "太陽" }, { en: "tree", zh: "樹" }
  ],
  3: [
    { en: "umbrella", zh: "雨傘" }, { en: "van", zh: "箱型車" },
    { en: "water", zh: "水" }, { en: "x-ray", zh: "X光" },
    { en: "yellow", zh: "黃色" }, { en: "zoo", zh: "動物園" },
    { en: "boy", zh: "男孩" }, { en: "cup", zh: "杯子" },
    { en: "desk", zh: "書桌" }, { en: "eye", zh: "眼睛" }
  ]
};

for (let i = 4; i <= 40; i++) {
  VOCABULARY[i] = Array(10).fill(null).map((_, idx) => ({
    en: `word${i}_${idx}`, zh: `第${i}課單字${idx+1}`
  }));
}

const MODES = {
  recognition: { id: 'recognition', name: '認讀測驗', icon: MousePointerClick, desc: '看英文選中文', color: 'bg-blue-500' },
  scramble: { id: 'scramble', name: '字母重組', icon: Shuffle, desc: '拼湊散落的字母', color: 'bg-purple-500' },
  spelling: { id: 'spelling', name: '拼字測驗', icon: Keyboard, desc: '看中文打英文', color: 'bg-rose-500' }
};

const DIFFICULTIES = {
  easy: { id: 'easy', name: '簡單', timeRatio: 1.5, lives: 5, scoreMultiplier: 1, color: 'text-green-500' },
  normal: { id: 'normal', name: '普通', timeRatio: 1.0, lives: 3, scoreMultiplier: 1.5, color: 'text-blue-500' },
  hard: { id: 'hard', name: '困難', timeRatio: 0.6, lives: 2, scoreMultiplier: 2.5, color: 'text-rose-500' }
};

const ACHIEVEMENTS = [
  { id: 'first_win', name: '初試啼聲', desc: '完成第一場遊戲', icon: '🎮' },
  { id: 'streak_10', name: '十連勝', desc: '連續完成 10 場遊戲', icon: '🔥' },
  { id: 'perfect', name: '完美無缺', desc: '滿血通關一個課程', icon: '✨' },
  { id: 'all_modes', name: '全能戰士', desc: '完成所有三種模式', icon: '🏆' },
  { id: 'collector_50', name: '集卡達人', desc: '獲得 50 個星星', icon: '⭐' },
  { id: 'cloud_sync', name: '連接世界', desc: '成功同步至雲端排行榜', icon: '🌍' },
  { id: 'battle_winner', name: '競技場贏家', desc: '在多人連線對戰中獲勝', icon: '⚔️' }
];

const REWARDS = [
  { id: 'title_master', name: '稱號：單字大師', cost: 15, icon: '👑', desc: '在排行榜顯示尊貴稱號', type: 'cosmetic' },
  { id: 'gold_avatar', name: '黃金大頭貼', cost: 30, icon: '🖼️', desc: '將您的頭像框升級為黃金版', type: 'cosmetic' },
  { id: 'lucky_star', name: '幸運星加成', cost: 60, icon: '🌟', desc: '永久獲得額外 10% 遊戲分數', type: 'buff' },
  { id: 'extra_life', name: '生命護身符', cost: 100, icon: '❤️', desc: '所有遊戲模式初始生命永久 +1', type: 'buff' }
];

// ==========================================
// 2. 輔助與音效函式
// ==========================================
const shuffleArray = (array) => {
  const newArr = [...array];
  for (let i = newArr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [newArr[i], newArr[j]] = [newArr[j], newArr[i]];
  }
  return newArr;
};

const playSound = (type) => {
  try {
    const ctx = new (window.AudioContext || window.webkitAudioContext)();
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.connect(gain);
    gain.connect(ctx.destination);
    
    if (type === 'correct') {
      osc.type = 'sine';
      osc.frequency.setValueAtTime(600, ctx.currentTime);
      osc.frequency.exponentialRampToValueAtTime(1200, ctx.currentTime + 0.1);
      gain.gain.setValueAtTime(0.2, ctx.currentTime);
      gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.1);
      osc.start(); osc.stop(ctx.currentTime + 0.1);
    } else if (type === 'wrong') {
      osc.type = 'sawtooth';
      osc.frequency.setValueAtTime(300, ctx.currentTime);
      osc.frequency.exponentialRampToValueAtTime(150, ctx.currentTime + 0.2);
      gain.gain.setValueAtTime(0.2, ctx.currentTime);
      gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.2);
      osc.start(); osc.stop(ctx.currentTime + 0.2);
    }
  } catch(e) {}
};

const speakWord = (text) => {
  if ('speechSynthesis' in window) {
    window.speechSynthesis.cancel();
    const msg = new SpeechSynthesisUtterance(text);
    msg.lang = 'en-US';
    msg.rate = 0.9;
    window.speechSynthesis.speak(msg);
  }
};

// 生成隨機房號
const generateRoomCode = () => {
  return Math.floor(1000 + Math.random() * 9000).toString();
};

// ==========================================
// 3. 主應用程式組件
// ==========================================
export default function App() {
  const [screen, setScreen] = useState('home'); 
  const [theme, setTheme] = useState('dark');
  const [selectedLesson, setSelectedLesson] = useState(1);
  const [selectedMode, setSelectedMode] = useState('recognition');
  const [difficulty, setDifficulty] = useState('normal');

  // Firebase 與雲端狀態
  const [user, setUser] = useState(null);
  const [isSyncing, setIsSyncing] = useState(false);
  const [leaderboard, setLeaderboard] = useState([]);
  
  // 對戰系統狀態
  const [roomId, setRoomId] = useState('');
  const [battleRole, setBattleRole] = useState(null); // 'host' or 'guest'

  // 本地進度狀態
  const [progress, setProgress] = useState({
    playerName: `Student_${Math.floor(Math.random()*1000)}`,
    totalScore: 0,
    stars: 0,
    spentStars: 0,
    unlockedRewards: [],
    gamesPlayed: 0,
    gamesWon: 0,
    winStreak: 0,
    lessonStars: {}, 
    achievements: [], 
    history: [],
    wrongWordsList: {} 
  });

  const availableStars = Math.max(0, progress.stars - (progress.spentStars || 0));

  useEffect(() => {
    if (!auth) return;
    const initAuth = async () => {
      try {
        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
          await signInWithCustomToken(auth, __initial_auth_token);
        } else {
          await signInAnonymously(auth);
        }
      } catch (error) {
        console.error("認證失敗:", error);
      }
    };
    initAuth();

    const unsubscribe = onAuthStateChanged(auth, (currentUser) => setUser(currentUser));
    return () => unsubscribe();
  }, []);

  useEffect(() => {
    const loadProgress = async () => {
      const saved = localStorage.getItem('boyoGameProgressOnline_v4');
      let currentProgress = progress;
      if (saved) {
        try { 
          currentProgress = JSON.parse(saved);
          setProgress(currentProgress); 
        } catch (e) {}
      }

      if (user && db) {
        setIsSyncing(true);
        try {
          const saveRef = doc(collection(db, 'artifacts', appId, 'users', user.uid, 'saves'), 'progress');
          const docSnap = await getDoc(saveRef);
          if (docSnap.exists()) {
            const cloudData = docSnap.data();
            if (cloudData.totalScore > currentProgress.totalScore) {
              setProgress({ ...cloudData, spentStars: cloudData.spentStars || 0, unlockedRewards: cloudData.unlockedRewards || [] });
              localStorage.setItem('boyoGameProgressOnline_v4', JSON.stringify(cloudData));
            }
          }
          if (!currentProgress.achievements.includes('cloud_sync')) {
             checkAchievements({...currentProgress}, null, true);
          }
        } catch (e) {
          console.error("讀取雲端失敗", e);
        }
        setIsSyncing(false);
      }
    };
    loadProgress();
  }, [user]);

  useEffect(() => {
    if (!user || !db) return;
    const lbRef = collection(db, 'artifacts', appId, 'public', 'data', 'leaderboard');
    const unsubscribe = onSnapshot(lbRef, (snapshot) => {
      const topPlayers = [];
      snapshot.forEach(doc => topPlayers.push({ id: doc.id, ...doc.data() }));
      topPlayers.sort((a, b) => b.totalScore - a.totalScore);
      setLeaderboard(topPlayers);
    }, (error) => console.error("排行榜讀取失敗:", error));
    
    return () => unsubscribe();
  }, [user]);

  const saveProgress = async (newProgress) => {
    setProgress(newProgress);
    localStorage.setItem('boyoGameProgressOnline_v4', JSON.stringify(newProgress));

    if (user && db) {
      setIsSyncing(true);
      try {
        const saveRef = doc(collection(db, 'artifacts', appId, 'users', user.uid, 'saves'), 'progress');
        await setDoc(saveRef, newProgress);

        const topWrongWords = Object.values(newProgress.wrongWordsList)
          .sort((a,b) => b.count - a.count)
          .slice(0, 3)
          .map(w => w.en);

        const publicLBPRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'leaderboard'), user.uid);
        await setDoc(publicLBPRef, {
          displayName: newProgress.playerName,
          totalScore: newProgress.totalScore,
          stars: newProgress.stars,
          achievementsCount: newProgress.achievements.length,
          unlockedRewards: newProgress.unlockedRewards || [],
          topWrongWords: topWrongWords,
          updatedAt: new Date().toISOString()
        });
      } catch (error) {
        console.error("雲端同步失敗", error);
      }
      setIsSyncing(false);
    }
  };

  const changePlayerName = (newName) => {
    if(!newName.trim()) return;
    saveProgress({...progress, playerName: newName.substring(0,10)});
  };

  const purchaseReward = (reward) => {
    if (availableStars >= reward.cost && !progress.unlockedRewards.includes(reward.id)) {
      const newProgress = {
        ...progress,
        spentStars: (progress.spentStars || 0) + reward.cost,
        unlockedRewards: [...(progress.unlockedRewards || []), reward.id]
      };
      saveProgress(newProgress);
      alert(`🎉 成功兌換：${reward.name}！`);
    } else {
      alert('星星不足或已兌換過！');
    }
  };

  const checkAchievements = (currentProgress, gameResult = null, forceCloud = false, isBattleWin = false) => {
    const unlocked = new Set(currentProgress.achievements);

    if (currentProgress.gamesPlayed >= 1 && !unlocked.has('first_win')) unlocked.add('first_win');
    if (currentProgress.winStreak >= 10 && !unlocked.has('streak_10')) unlocked.add('streak_10');
    if (gameResult && gameResult.lives === DIFFICULTIES[gameResult.difficulty].lives && gameResult.won && !unlocked.has('perfect')) unlocked.add('perfect');
    if (currentProgress.stars >= 50 && !unlocked.has('collector_50')) unlocked.add('collector_50');
    if (forceCloud && !unlocked.has('cloud_sync')) unlocked.add('cloud_sync');
    if (isBattleWin && !unlocked.has('battle_winner')) unlocked.add('battle_winner');
    
    const playedModes = new Set(currentProgress.history.map(h => h.mode));
    if (playedModes.size >= 3 && !unlocked.has('all_modes')) unlocked.add('all_modes');

    return Array.from(unlocked);
  };

  const handleGameOver = (result) => {
    const isWin = result.lives > 0;
    const lessonKey = `${selectedLesson}_${selectedMode}`;
    const currentStars = progress.lessonStars[lessonKey] || 0;
    const newStars = isWin ? Math.max(currentStars, result.stars) : currentStars;
    const starDiff = newStars - currentStars;

    const newWrongWordsList = { ...progress.wrongWordsList };
    result.wrongWords.forEach(w => {
      if (newWrongWordsList[w.en]) newWrongWordsList[w.en].count += 1;
      else newWrongWordsList[w.en] = { ...w, count: 1 };
    });

    const newProgress = {
      ...progress,
      totalScore: progress.totalScore + result.score,
      stars: progress.stars + starDiff,
      gamesPlayed: progress.gamesPlayed + 1,
      gamesWon: progress.gamesWon + (isWin ? 1 : 0),
      winStreak: isWin ? progress.winStreak + 1 : 0,
      lessonStars: { ...progress.lessonStars, [lessonKey]: newStars },
      wrongWordsList: newWrongWordsList,
      history: [...progress.history, { date: new Date().toISOString(), ...result }]
    };

    newProgress.achievements = checkAchievements(newProgress, result);
    saveProgress(newProgress);
  };

  const handleBattleGameOver = (isWin, scoreEarned) => {
    const newProgress = {
      ...progress,
      totalScore: progress.totalScore + scoreEarned,
      stars: progress.stars + (isWin ? 2 : 0) // 對戰勝利額外給 2 顆星
    };
    newProgress.achievements = checkAchievements(newProgress, null, false, isWin);
    saveProgress(newProgress);
  };

  const renderScreen = () => {
    switch (screen) {
      case 'home': return <ScreenHome setScreen={setScreen} progress={progress} availableStars={availableStars} changePlayerName={changePlayerName} user={user} isSyncing={isSyncing} theme={theme} setTheme={setTheme} />;
      case 'lesson': return <ScreenLesson setScreen={setScreen} onSelect={setSelectedLesson} progress={progress} theme={theme} />;
      case 'mode': return <ScreenMode setScreen={setScreen} lesson={selectedLesson} onSelect={setSelectedMode} difficulty={difficulty} setDifficulty={setDifficulty} theme={theme} />;
      case 'game': return <ScreenGame setScreen={setScreen} lesson={selectedLesson} mode={selectedMode} difficulty={difficulty} onGameOver={handleGameOver} progress={progress} theme={theme} />;
      case 'stats': return <ScreenStats setScreen={setScreen} progress={progress} theme={theme} />;
      case 'achievements': return <ScreenAchievements setScreen={setScreen} progress={progress} theme={theme} />;
      case 'leaderboard': return <ScreenLeaderboard setScreen={setScreen} leaderboard={leaderboard} currentUserId={user?.uid} theme={theme} />;
      case 'vocab_book': return <ScreenVocabBook setScreen={setScreen} progress={progress} onSelectLesson={setSelectedLesson} onSelectMode={setSelectedMode} theme={theme} />;
      case 'rewards': return <ScreenRewards setScreen={setScreen} progress={progress} availableStars={availableStars} purchaseReward={purchaseReward} theme={theme} />;
      case 'admin_login': return <ScreenAdminLogin setScreen={setScreen} theme={theme} />;
      case 'admin_dashboard': return <ScreenAdminDashboard setScreen={setScreen} leaderboard={leaderboard} theme={theme} />;
      
      // 對戰系統畫面
      case 'battle_lobby': return <ScreenBattleLobby setScreen={setScreen} user={user} db={db} appId={appId} playerName={progress.playerName} setRoomId={setRoomId} setBattleRole={setBattleRole} theme={theme} />;
      case 'battle_game': return <ScreenBattleGame setScreen={setScreen} user={user} db={db} appId={appId} roomId={roomId} role={battleRole} theme={theme} onBattleGameOver={handleBattleGameOver} progress={progress} />;
      
      default: return <ScreenHome setScreen={setScreen} progress={progress} availableStars={availableStars} theme={theme} setTheme={setTheme} />;
    }
  };

  const bgClass = theme === 'dark' ? 'bg-slate-900 text-white' : 'bg-slate-50 text-slate-900';

  return (
    <div className={`min-h-screen transition-colors duration-300 font-sans ${bgClass} overflow-hidden flex flex-col`}>
      {renderScreen()}
    </div>
  );
}

// ==========================================
// 4. 各個畫面組件 (Screens)
// ==========================================

function ScreenHome({ setScreen, progress, availableStars, changePlayerName, user, isSyncing, theme, setTheme }) {
  const isDark = theme === 'dark';
  const cardBg = isDark ? 'bg-slate-800' : 'bg-white shadow-lg';
  const [editingName, setEditingName] = useState(false);
  const [tempName, setTempName] = useState(progress.playerName);

  const clickTimerRef = useRef(null);
  const clickCountRef = useRef(0);
  
  const handleTitleClick = () => {
    clickCountRef.current += 1;
    if (clickCountRef.current === 3) {
      setScreen('admin_login');
      clickCountRef.current = 0;
    }
    clearTimeout(clickTimerRef.current);
    clickTimerRef.current = setTimeout(() => { clickCountRef.current = 0; }, 1500);
  };

  const handleNameSubmit = (e) => {
    e.preventDefault();
    changePlayerName(tempName);
    setEditingName(false);
  };

  const hasGoldAvatar = progress.unlockedRewards?.includes('gold_avatar');
  const hasMasterTitle = progress.unlockedRewards?.includes('title_master');

  return (
    <div className="flex-1 flex flex-col items-center justify-center p-6 max-w-md mx-auto w-full relative">
      <div className="absolute top-6 w-full px-6 flex justify-between items-center box-border left-0">
        <div className="flex items-center gap-2 text-xs font-bold px-3 py-1.5 rounded-full bg-slate-800/20">
          {user ? (
            isSyncing ? <Cloud className="w-4 h-4 text-blue-400 animate-pulse" /> : <Cloud className="w-4 h-4 text-green-500" />
          ) : (
            <CloudOff className="w-4 h-4 text-slate-400" />
          )}
          <span className={isDark ? 'text-slate-300' : 'text-slate-600'}>
            {user ? (isSyncing ? '同步中...' : '已連線') : '離線模式'}
          </span>
        </div>
        <button onClick={() => setTheme(isDark ? 'light' : 'dark')} className="p-2 rounded-full hover:bg-slate-500/20 transition-colors">
          {isDark ? <Sun className="text-yellow-400" /> : <Moon className="text-slate-600" />}
        </button>
      </div>

      <div className="text-center mb-6 mt-8 animate-fade-in-up">
        <div className="inline-flex items-center justify-center w-24 h-24 rounded-3xl bg-gradient-to-br from-blue-500 to-purple-600 mb-4 shadow-xl transform hover:scale-105 transition-transform">
          <BookOpen className="w-12 h-12 text-white" />
        </div>
        <h1 onClick={handleTitleClick} className="text-4xl font-black mb-2 tracking-tight cursor-default select-none">博幼 800 單</h1>
        <p className={`text-lg font-medium ${isDark ? 'text-blue-400' : 'text-blue-600'} flex items-center justify-center gap-2`}>
          <Globe className="w-5 h-5" /> 線上對戰版
        </p>
      </div>

      <div className={`w-full ${cardBg} rounded-3xl p-5 mb-5 border ${isDark ? 'border-slate-700' : 'border-slate-100'} animate-fade-in-up delay-100`}>
        <div className="flex justify-between items-center mb-4 pb-4 border-b border-slate-700/30">
          {editingName ? (
            <form onSubmit={handleNameSubmit} className="flex flex-1 gap-2">
              <input 
                type="text" value={tempName} onChange={e=>setTempName(e.target.value)} maxLength={10}
                className={`flex-1 px-3 py-1 rounded-lg ${isDark ? 'bg-slate-900 border-slate-700' : 'bg-slate-100 border-slate-300'} border focus:outline-none focus:border-blue-500`}
                autoFocus
              />
              <button type="submit" className="px-3 py-1 bg-blue-600 text-white rounded-lg text-sm font-bold">儲存</button>
            </form>
          ) : (
            <div className="flex items-center gap-3 cursor-pointer group" onClick={() => setEditingName(true)}>
              <div className={`w-10 h-10 rounded-full flex items-center justify-center text-white font-bold text-lg
                ${hasGoldAvatar ? 'bg-gradient-to-br from-yellow-300 via-yellow-500 to-amber-600 border-2 border-yellow-200 shadow-lg shadow-yellow-500/50' : 'bg-gradient-to-r from-blue-400 to-indigo-500'}
              `}>
                {progress.playerName.charAt(0).toUpperCase()}
              </div>
              <div className="flex flex-col">
                <div className="flex items-center gap-1">
                  <span className="font-bold text-lg">{progress.playerName}</span>
                  {hasMasterTitle && <Crown className="w-4 h-4 text-yellow-500" />}
                </div>
                {hasMasterTitle && <span className="text-[10px] text-yellow-500 font-bold">單字大師</span>}
              </div>
              <Settings className="w-4 h-4 text-slate-400 opacity-0 group-hover:opacity-100 transition-opacity ml-auto" />
            </div>
          )}
        </div>

        <div className="grid grid-cols-3 gap-4 text-center">
          <div>
            <div className={`text-xs ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>總分</div>
            <div className="text-lg font-bold flex items-center justify-center gap-1 text-blue-500">
              <Trophy className="w-3.5 h-3.5" /> {progress.totalScore.toLocaleString()}
            </div>
          </div>
          <div className={`border-x ${isDark ? 'border-slate-700' : 'border-slate-200'}`}>
            <div className={`text-xs ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>星幣</div>
            <div className="text-lg font-bold flex items-center justify-center gap-1 text-yellow-500">
              <Star className="w-3.5 h-3.5" /> {availableStars}
            </div>
          </div>
          <div>
            <div className={`text-xs ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>錯題</div>
            <div className="text-lg font-bold flex items-center justify-center gap-1 text-rose-500">
              <Flame className="w-3.5 h-3.5" /> {Object.keys(progress.wrongWordsList).length}
            </div>
          </div>
        </div>
      </div>

      <div className="w-full space-y-3 animate-fade-in-up delay-200">
        <div className="grid grid-cols-2 gap-3">
          <button onClick={() => setScreen('lesson')} className="w-full relative overflow-hidden bg-blue-600 hover:bg-blue-500 text-white font-bold text-lg py-4 rounded-2xl transition-all shadow-lg flex items-center justify-center gap-2">
            <Play className="w-5 h-5 fill-current" /> 單人闖關
          </button>
          
          <button onClick={() => setScreen('battle_lobby')} className="w-full relative overflow-hidden bg-rose-600 hover:bg-rose-500 text-white font-bold text-lg py-4 rounded-2xl transition-all shadow-lg flex items-center justify-center gap-2">
            <Swords className="w-5 h-5" /> 多人對戰
          </button>
        </div>

        <div className="grid grid-cols-2 gap-3">
          <button onClick={() => setScreen('rewards')} className={`w-full bg-gradient-to-br from-amber-400 to-orange-500 hover:from-amber-300 hover:to-orange-400 text-white shadow-sm font-bold py-3 px-4 rounded-2xl transition-all flex flex-col items-center gap-2`}>
            <Gift className="w-6 h-6" /> 兌換獎勵
          </button>
          <button onClick={() => setScreen('leaderboard')} className={`w-full ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-white shadow-sm hover:bg-slate-50'} font-bold py-3 px-4 rounded-2xl transition-all flex flex-col items-center gap-2 border ${isDark?'border-transparent':'border-slate-200'}`}>
            <Globe className="w-6 h-6 text-emerald-500" /> 世界排行
          </button>
          <button onClick={() => setScreen('vocab_book')} className={`w-full ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-white shadow-sm hover:bg-slate-50'} font-bold py-3 px-4 rounded-2xl transition-all flex flex-col items-center gap-2 border ${isDark?'border-transparent':'border-slate-200'}`}>
            <Bookmark className="w-6 h-6 text-rose-500" /> 單字本
          </button>
          <button onClick={() => setScreen('stats')} className={`w-full ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-white shadow-sm hover:bg-slate-50'} font-bold py-3 px-4 rounded-2xl transition-all flex flex-col items-center gap-2 border ${isDark?'border-transparent':'border-slate-200'}`}>
            <BarChart3 className="w-6 h-6 text-blue-500" /> 學習進度
          </button>
        </div>
      </div>
      
      <style dangerouslySetInnerHTML={{__html: `
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .animate-fade-in-up { animation: fadeInUp 0.4s ease-out forwards; opacity: 0; }
        .delay-100 { animation-delay: 100ms; }
        .delay-200 { animation-delay: 200ms; }
      `}} />
    </div>
  );
}

// --- 雙人對戰大廳 (Multiplayer Lobby) ---
function ScreenBattleLobby({ setScreen, user, db, appId, playerName, setRoomId, setBattleRole, theme }) {
  const isDark = theme === 'dark';
  const [inputCode, setInputCode] = useState('');
  const [statusMsg, setStatusMsg] = useState('');
  const [isWaiting, setIsWaiting] = useState(false);
  const [myRoomCode, setMyRoomCode] = useState('');

  // 監聽房間狀態
  useEffect(() => {
    if (!isWaiting || !myRoomCode || !db || !user) return;
    
    const roomRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'battles'), myRoomCode);
    const unsubscribe = onSnapshot(roomRef, (snapshot) => {
      if (snapshot.exists()) {
        const data = snapshot.data();
        if (data.status === 'playing') {
          setRoomId(myRoomCode);
          setBattleRole('host');
          setScreen('battle_game');
        }
      }
    });
    return () => unsubscribe();
  }, [isWaiting, myRoomCode, db, user, appId, setRoomId, setBattleRole, setScreen]);

  const createRoom = async () => {
    if (!user || !db) return setStatusMsg('尚未連接雲端服務');
    const code = generateRoomCode();
    
    // 隨機抽取 10 個單字作為對戰題目
    let allWords = [];
    for(let i=1; i<=3; i++) allWords = [...allWords, ...VOCABULARY[i]];
    const battleWords = shuffleArray(allWords).slice(0, 10);

    try {
      setStatusMsg('建立房間中...');
      const roomRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'battles'), code);
      await setDoc(roomRef, {
        status: 'waiting',
        words: battleWords,
        host: { uid: user.uid, name: playerName, score: 0, progress: 0, finished: false },
        guest: null,
        createdAt: new Date().toISOString()
      });
      setMyRoomCode(code);
      setIsWaiting(true);
      setStatusMsg('');
    } catch (e) {
      console.error(e);
      setStatusMsg('建立失敗，請稍後再試');
    }
  };

  const joinRoom = async (e) => {
    e.preventDefault();
    if (!inputCode || inputCode.length !== 4) return setStatusMsg('請輸入 4 位數代碼');
    if (!user || !db) return setStatusMsg('尚未連接雲端服務');

    setStatusMsg('尋找房間中...');
    try {
      const roomRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'battles'), inputCode);
      const snapshot = await getDoc(roomRef);
      
      if (!snapshot.exists()) return setStatusMsg('找不到該房間！');
      
      const data = snapshot.data();
      if (data.status !== 'waiting') return setStatusMsg('遊戲已經開始或已結束！');

      // 加入房間
      await updateDoc(roomRef, {
        status: 'playing',
        guest: { uid: user.uid, name: playerName, score: 0, progress: 0, finished: false }
      });

      setRoomId(inputCode);
      setBattleRole('guest');
      setScreen('battle_game');
    } catch (e) {
      console.error(e);
      setStatusMsg('加入失敗，請確認代碼是否正確');
    }
  };

  if (isWaiting) {
    return (
      <div className="flex-1 flex flex-col items-center justify-center p-6 w-full text-center">
        <div className={`p-8 rounded-3xl shadow-xl w-full max-w-sm ${isDark ? 'bg-slate-800' : 'bg-white'}`}>
          <div className="w-20 h-20 mx-auto bg-blue-500/20 rounded-full flex items-center justify-center mb-6">
            <Clock className="w-10 h-10 text-blue-500 animate-spin-slow" />
          </div>
          <h2 className="text-2xl font-bold mb-2">等待對手加入...</h2>
          <p className={`text-sm mb-6 ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>請將房間代碼分享給您的朋友</p>
          
          <div className={`text-5xl font-black tracking-[0.2em] py-6 rounded-2xl mb-8 ${isDark ? 'bg-slate-900 text-blue-400' : 'bg-slate-100 text-blue-600'}`}>
            {myRoomCode}
          </div>
          
          <button 
            onClick={() => { setIsWaiting(false); setStatusMsg(''); }}
            className={`w-full font-bold py-4 rounded-xl ${isDark ? 'bg-slate-700 text-white hover:bg-slate-600' : 'bg-slate-200 text-slate-800 hover:bg-slate-300'}`}
          >
            取消並離開
          </button>
        </div>
      </div>
    );
  }

  return (
    <div className="flex-1 flex flex-col p-6 max-w-md mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-10 pt-2 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}>
          <ArrowLeft className="w-6 h-6" />
        </button>
        <h2 className="text-2xl font-bold flex-1 flex items-center gap-2">
          <Swords className="text-rose-500 w-7 h-7" /> 多人對戰大廳
        </h2>
      </div>

      <div className="flex-1 flex flex-col justify-center space-y-8">
        <div className={`p-6 rounded-3xl border-2 ${isDark ? 'bg-slate-800 border-slate-700' : 'bg-white border-slate-200 shadow-sm'}`}>
          <h3 className="text-xl font-bold mb-4 flex items-center gap-2"><Users className="w-6 h-6 text-blue-500" /> 加入好友的房間</h3>
          <form onSubmit={joinRoom} className="flex gap-2">
            <input 
              type="text" placeholder="輸入 4 位數代碼..." maxLength={4}
              value={inputCode} onChange={e => {setInputCode(e.target.value.toUpperCase()); setStatusMsg('');}}
              className={`flex-1 text-center text-xl font-bold p-4 rounded-2xl outline-none ${isDark ? 'bg-slate-900 border-slate-700' : 'bg-slate-100 border-slate-300'} border-2 focus:border-blue-500 tracking-widest`}
            />
            <button type="submit" disabled={!inputCode} className="bg-blue-600 hover:bg-blue-500 disabled:opacity-50 text-white font-bold px-6 rounded-2xl transition-colors">
              加入
            </button>
          </form>
          {statusMsg && <p className="text-rose-500 text-sm font-bold mt-3 text-center">{statusMsg}</p>}
        </div>

        <div className="relative flex items-center justify-center">
          <div className={`border-t w-full ${isDark ? 'border-slate-700' : 'border-slate-300'}`}></div>
          <div className={`absolute px-4 text-sm font-bold ${isDark ? 'bg-slate-900 text-slate-500' : 'bg-slate-50 text-slate-400'}`}>或</div>
        </div>

        <div className={`p-6 rounded-3xl border-2 ${isDark ? 'bg-slate-800 border-slate-700' : 'bg-white border-slate-200 shadow-sm'} text-center`}>
          <h3 className="text-xl font-bold mb-2">自己開房當關主</h3>
          <p className={`text-sm mb-6 ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>建立房間並將代碼分享給好友，一起比拚單字力！</p>
          <button onClick={createRoom} className="w-full bg-rose-600 hover:bg-rose-500 text-white text-lg font-bold py-4 rounded-2xl shadow-lg shadow-rose-500/30 flex justify-center items-center gap-2">
            <Crown className="w-6 h-6" /> 建立新房間
          </button>
        </div>
      </div>
    </div>
  );
}

// --- 雙人對戰遊戲區 (Multiplayer Battle) ---
function ScreenBattleGame({ setScreen, user, db, appId, roomId, role, theme, onBattleGameOver, progress }) {
  const isDark = theme === 'dark';
  
  const [roomData, setRoomData] = useState(null);
  const [currentIndex, setCurrentIndex] = useState(0);
  const [options, setOptions] = useState([]);
  const [feedback, setFeedback] = useState(null);
  const [shake, setShake] = useState(false);
  const [score, setScore] = useState(0);

  // 初始化與監聽房間資料
  useEffect(() => {
    if (!user || !db || !roomId) return;
    
    const roomRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'battles'), roomId);
    const unsubscribe = onSnapshot(roomRef, (snapshot) => {
      if (snapshot.exists()) {
        const data = snapshot.data();
        setRoomData(data);
      }
    });

    return () => unsubscribe();
  }, [roomId, user, db, appId]);

  // 準備題目
  useEffect(() => {
    if (!roomData || !roomData.words || currentIndex >= roomData.words.length) return;
    const currentWord = roomData.words[currentIndex];
    speakWord(currentWord.en);
    setFeedback(null);
    
    // 從大題庫中隨機抓 3 個混淆選項
    let allWords = [];
    for(let i=1; i<=3; i++) allWords = [...allWords, ...VOCABULARY[i]];
    const otherWords = shuffleArray(allWords.filter(w => w.en !== currentWord.en)).slice(0, 3);
    setOptions(shuffleArray([currentWord, ...otherWords]));
  }, [currentIndex, roomData]);

  const updateServerProgress = async (newScore, newProgress, finished = false) => {
    if (!user || !db || !roomId) return;
    const roomRef = doc(collection(db, 'artifacts', appId, 'public', 'data', 'battles'), roomId);
    try {
      await updateDoc(roomRef, {
        [`${role}.score`]: newScore,
        [`${role}.progress`]: newProgress,
        [`${role}.finished`]: finished
      });
    } catch (e) {
      console.error(e);
    }
  };

  const handleOptionClick = (opt) => {
    if (feedback || !roomData) return;
    const currentWord = roomData.words[currentIndex];
    
    if (opt.en === currentWord.en) {
      setFeedback('correct');
      playSound('correct');
      const newScore = score + (progress.unlockedRewards?.includes('lucky_star') ? 110 : 100);
      setScore(newScore);
      
      setTimeout(() => {
        const nextIdx = currentIndex + 1;
        setCurrentIndex(nextIdx);
        updateServerProgress(newScore, nextIdx, nextIdx >= roomData.words.length);
      }, 800);
    } else {
      setFeedback('wrong');
      playSound('wrong');
      setShake(true); setTimeout(() => setShake(false), 500);
      setTimeout(() => {
        setFeedback(null);
      }, 800);
    }
  };

  if (!roomData) return <div className="flex-1 flex items-center justify-center font-bold text-xl">載入對戰資料中...</div>;

  const me = role === 'host' ? roomData.host : roomData.guest;
  const opponent = role === 'host' ? roomData.guest : roomData.host;
  const totalWords = roomData.words.length;
  
  // 如果雙方都完成了，顯示對戰結果
  if (me?.finished && opponent?.finished) {
    const isWin = me.score > opponent.score;
    const isTie = me.score === opponent.score;
    
    return (
      <div className="flex-1 flex flex-col items-center justify-center p-6 max-w-md mx-auto w-full text-center">
        <div className={`w-full p-8 rounded-3xl shadow-2xl mb-8 relative overflow-hidden ${isDark ? 'bg-slate-800' : 'bg-white border border-slate-200'}`}>
          <div className={`absolute top-0 left-0 w-full h-3 ${isWin ? 'bg-green-500' : (isTie ? 'bg-yellow-500' : 'bg-rose-500')}`}></div>
          
          <div className="mb-8">
            {isWin ? <Trophy className="w-24 h-24 mx-auto text-yellow-500 mb-4 animate-bounce" /> : <RotateCcw className="w-24 h-24 mx-auto text-slate-500 mb-4" />}
            <h2 className="text-4xl font-black mb-2">{isWin ? '你贏了！' : (isTie ? '平手！' : '惜敗...')}</h2>
          </div>

          <div className="flex justify-between items-center bg-slate-900/10 p-4 rounded-2xl mb-4">
            <div className="text-center w-1/3">
              <div className="text-sm font-bold text-blue-500 mb-1">你 ({me.name})</div>
              <div className="text-3xl font-black">{me.score}</div>
            </div>
            <div className="text-2xl font-black text-slate-400">VS</div>
            <div className="text-center w-1/3">
              <div className="text-sm font-bold text-rose-500 mb-1">對手 ({opponent.name})</div>
              <div className="text-3xl font-black">{opponent.score}</div>
            </div>
          </div>
        </div>
        
        <button 
          onClick={() => {
            onBattleGameOver(isWin, me.score);
            setScreen('home');
          }} 
          className="w-full bg-blue-600 hover:bg-blue-500 text-white text-xl font-bold py-4 rounded-2xl shadow-lg transition-all"
        >
          領取分數並返回
        </button>
      </div>
    );
  }

  // 等待對方完成
  if (me?.finished) {
    return (
      <div className="flex-1 flex flex-col items-center justify-center p-6 text-center">
        <Clock className="w-20 h-20 text-blue-500 animate-spin-slow mb-6" />
        <h2 className="text-3xl font-black mb-4">等待對手完成...</h2>
        <div className={`p-6 rounded-2xl w-full max-w-sm ${isDark ? 'bg-slate-800' : 'bg-white shadow-lg'}`}>
          <div className="mb-4">
            <div className="flex justify-between mb-1 text-sm font-bold text-blue-500">
              <span>你 ({me.name})</span><span>{me.score} 分</span>
            </div>
          </div>
          <div>
            <div className="flex justify-between mb-1 text-sm font-bold text-rose-500">
              <span>對手 ({opponent.name})</span><span>{opponent.progress} / {totalWords} 題</span>
            </div>
            <div className="w-full h-3 bg-slate-700 rounded-full overflow-hidden">
              <div className="h-full bg-rose-500 transition-all duration-300" style={{width: `${(opponent.progress/totalWords)*100}%`}}></div>
            </div>
          </div>
        </div>
      </div>
    );
  }

  const currentWord = roomData.words[currentIndex];

  return (
    <div className={`flex-1 flex flex-col max-w-2xl mx-auto w-full h-screen ${shake ? 'animate-shake' : ''}`}>
      {/* 雙方進度 HUD */}
      <div className={`${isDark ? 'bg-slate-800' : 'bg-white shadow-sm'} p-4 z-10 rounded-b-3xl mb-6 space-y-3 border-b-4 border-blue-500/20`}>
        {/* 我的進度 */}
        <div>
          <div className="flex justify-between text-xs font-bold mb-1 text-blue-500">
            <span>你 ({me.name})</span>
            <span>{score} 分</span>
          </div>
          <div className={`w-full h-2 rounded-full overflow-hidden ${isDark ? 'bg-slate-900' : 'bg-slate-200'}`}>
            <div className="h-full bg-blue-500 transition-all duration-300" style={{width: `${(currentIndex/totalWords)*100}%`}}></div>
          </div>
        </div>
        
        {/* 對手進度 */}
        <div>
          <div className="flex justify-between text-xs font-bold mb-1 text-rose-500">
            <span>對手 ({opponent?.name || '等待中...'})</span>
            <span>{opponent?.score || 0} 分</span>
          </div>
          <div className={`w-full h-2 rounded-full overflow-hidden ${isDark ? 'bg-slate-900' : 'bg-slate-200'}`}>
            <div className="h-full bg-rose-500 transition-all duration-300" style={{width: `${((opponent?.progress || 0)/totalWords)*100}%`}}></div>
          </div>
        </div>
      </div>

      <div className="flex-1 flex flex-col px-4 pb-6 overflow-hidden">
        <div className="flex-1 flex flex-col items-center justify-center mb-8 relative">
          {feedback && (
            <div className="absolute inset-0 flex items-center justify-center z-20 bg-slate-900/50 backdrop-blur-sm rounded-3xl animate-fade-in">
              <div className={`text-center p-6 rounded-2xl ${feedback === 'correct' ? 'bg-green-500' : 'bg-rose-500'} text-white shadow-2xl transform scale-110`}>
                {feedback === 'correct' ? <Check className="w-16 h-16 mx-auto mb-2" /> : <X className="w-16 h-16 mx-auto mb-2" />}
                <div className="text-2xl font-bold">{feedback === 'correct' ? '答對了！' : '答錯了！'}</div>
              </div>
            </div>
          )}
          <div className="text-center w-full relative">
             <button onClick={() => speakWord(currentWord.en)} className="absolute -top-12 right-0 p-2 rounded-full bg-blue-500/10 text-blue-500 hover:bg-blue-500 hover:text-white transition-colors">
              <Volume2 className="w-6 h-6" />
            </button>
            <span className="inline-block px-4 py-1 rounded-full text-sm font-bold mb-6 bg-purple-500 text-white">競技模式 ⚔️</span>
            <h2 className="text-5xl md:text-6xl font-black mb-4 tracking-tight">{currentWord?.en}</h2>
          </div>
        </div>

        <div className="w-full shrink-0 grid grid-cols-2 gap-3">
          {options.map((opt, i) => (
            <button key={i} onClick={() => handleOptionClick(opt)} disabled={!!feedback} className={`p-5 rounded-2xl text-xl font-bold transition-all active:scale-95 ${isDark ? 'bg-slate-800 hover:bg-blue-600 border border-slate-700' : 'bg-white shadow border border-slate-200 hover:border-blue-500 hover:bg-blue-50 text-slate-800'}`}>
              {opt.zh}
            </button>
          ))}
        </div>
      </div>
      <style dangerouslySetInnerHTML={{__html: `@keyframes shake { 0%, 100% { transform: translateX(0); } 25% { transform: translateX(-10px); } 50% { transform: translateX(10px); } 75% { transform: translateX(-10px); } } .animate-shake { animation: shake 0.4s cubic-bezier(.36,.07,.19,.97) both; } @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } } .animate-fade-in { animation: fadeIn 0.2s ease-out forwards; }`}} />
    </div>
  );
}

// --- 兌換所 (Rewards System) ---
function ScreenRewards({ setScreen, progress, availableStars, purchaseReward, theme }) {
  const isDark = theme === 'dark';

  return (
    <div className="flex-1 flex flex-col p-6 max-w-md mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-6 pt-2 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}>
          <ArrowLeft className="w-6 h-6" />
        </button>
        <h2 className="text-2xl font-bold flex-1 flex items-center gap-2">
          <ShoppingBag className="text-amber-500 w-7 h-7" /> 獎勵兌換所
        </h2>
        <div className="font-bold text-yellow-500 bg-yellow-500/10 px-3 py-1 rounded-full flex items-center gap-1">
          <Star className="w-4 h-4 fill-current" /> {availableStars}
        </div>
      </div>

      <div className="flex-1 overflow-y-auto space-y-4 pb-8 custom-scrollbar">
        {REWARDS.map(reward => {
          const isUnlocked = progress.unlockedRewards?.includes(reward.id);
          const canAfford = availableStars >= reward.cost;

          return (
            <div key={reward.id} className={`flex items-center p-4 rounded-3xl border-2 transition-all 
              ${isUnlocked ? (isDark ? 'bg-slate-800 border-slate-700 opacity-70' : 'bg-slate-50 border-slate-200 opacity-70') : 
              (isDark ? 'bg-slate-800 border-slate-700 hover:border-amber-500/50' : 'bg-white border-slate-100 shadow-sm hover:border-amber-400')}`}>
              
              <div className="w-14 h-14 rounded-2xl flex items-center justify-center text-3xl bg-slate-100 dark:bg-slate-900 shrink-0 mr-4 shadow-inner">
                {reward.icon}
              </div>
              
              <div className="flex-1">
                <h3 className="text-lg font-bold mb-1 flex items-center gap-2">
                  {reward.name}
                  {reward.type === 'buff' && <span className="text-[10px] bg-green-500 text-white px-2 py-0.5 rounded-full">增益</span>}
                  {reward.type === 'cosmetic' && <span className="text-[10px] bg-purple-500 text-white px-2 py-0.5 rounded-full">外觀</span>}
                </h3>
                <p className={`text-xs ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-2`}>{reward.desc}</p>
                
                {isUnlocked ? (
                  <div className="text-sm font-bold text-emerald-500 flex items-center gap-1"><Check className="w-4 h-4"/> 已擁有</div>
                ) : (
                  <button 
                    onClick={() => purchaseReward(reward)}
                    disabled={!canAfford}
                    className={`text-sm font-bold px-4 py-1.5 rounded-xl flex items-center gap-1 transition-all
                      ${canAfford ? 'bg-amber-500 hover:bg-amber-400 text-white shadow-md active:scale-95' : 'bg-slate-200 dark:bg-slate-700 text-slate-400 cursor-not-allowed'}`}
                  >
                    <Star className="w-4 h-4 fill-current"/> {reward.cost} 兌換
                  </button>
                )}
              </div>
            </div>
          );
        })}
      </div>
    </div>
  );
}

// --- 教師後台登入 ---
function ScreenAdminLogin({ setScreen, theme }) {
  const isDark = theme === 'dark';
  const [pwd, setPwd] = useState('');
  const [error, setError] = useState(false);

  const handleLogin = (e) => {
    e.preventDefault();
    if (pwd === 'boyo800') {
      setScreen('admin_dashboard');
    } else {
      setError(true);
      setPwd('');
    }
  };

  return (
    <div className="flex-1 flex flex-col items-center justify-center p-6 max-w-sm mx-auto w-full">
      <div className={`w-full p-8 rounded-3xl text-center shadow-2xl ${isDark ? 'bg-slate-800' : 'bg-white border border-slate-200'}`}>
        <Lock className="w-16 h-16 mx-auto text-blue-500 mb-4" />
        <h2 className="text-2xl font-black mb-2">教師專屬後台</h2>
        <p className={`text-sm mb-6 ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>請輸入管理員密碼以查看學習數據</p>
        
        <form onSubmit={handleLogin} className="space-y-4">
          <input 
            type="password" value={pwd} onChange={e => {setPwd(e.target.value); setError(false);}}
            placeholder="請輸入密碼..." autoFocus
            className={`w-full text-center p-3 rounded-xl outline-none ${isDark ? 'bg-slate-900 border-slate-700' : 'bg-slate-100 border-slate-300'} border-2 focus:border-blue-500`}
          />
          {error && <p className="text-rose-500 text-sm font-bold">密碼錯誤，請重試！</p>}
          <button type="submit" className="w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-3 rounded-xl transition-all">登入系統</button>
          <button type="button" onClick={() => setScreen('home')} className={`w-full font-bold py-3 rounded-xl ${isDark ? 'bg-slate-700' : 'bg-slate-200'}`}>返回首頁</button>
        </form>
      </div>
    </div>
  );
}

// --- 教師數據儀表板 ---
function ScreenAdminDashboard({ setScreen, leaderboard, theme }) {
  const isDark = theme === 'dark';
  
  const globalWrongWords = {};
  leaderboard.forEach(player => {
    if (player.topWrongWords) {
      player.topWrongWords.forEach(word => {
        globalWrongWords[word] = (globalWrongWords[word] || 0) + 1;
      });
    }
  });
  
  const topGlobalMistakes = Object.entries(globalWrongWords)
    .sort((a,b) => b[1] - a[1])
    .slice(0, 5);

  return (
    <div className="flex-1 flex flex-col p-6 max-w-2xl mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-6 pt-2 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}>
          <ArrowLeft className="w-6 h-6" />
        </button>
        <h2 className="text-2xl font-bold flex-1 flex items-center gap-2">
          <UserCog className="text-blue-500 w-7 h-7" /> 教師數據中心
        </h2>
      </div>

      <div className="flex-1 overflow-y-auto space-y-6 pb-8 custom-scrollbar pr-2">
        <div className={`p-5 rounded-3xl border-2 ${isDark ? 'bg-slate-800 border-rose-500/30' : 'bg-white border-rose-200 shadow-md'}`}>
          <h3 className="text-lg font-bold mb-4 flex items-center gap-2 text-rose-500">
            <Flame className="w-5 h-5" /> 全班高頻錯題 (Top 5)
          </h3>
          <div className="flex flex-wrap gap-2">
            {topGlobalMistakes.length > 0 ? topGlobalMistakes.map(([word, count], i) => (
              <div key={word} className={`px-4 py-2 rounded-xl flex items-center gap-2 ${isDark ? 'bg-slate-900' : 'bg-rose-50'}`}>
                <span className="font-bold text-lg">{word}</span>
                <span className="text-xs bg-rose-500 text-white px-2 py-0.5 rounded-full">{count} 人錯過</span>
              </div>
            )) : <div className="text-sm opacity-50">尚無足夠的錯題數據</div>}
          </div>
        </div>

        <div>
          <h3 className="text-lg font-bold mb-3 pl-2">學生學習總表 ({leaderboard.length}人)</h3>
          <div className="space-y-3">
            {leaderboard.length === 0 ? <div className="text-center py-10 opacity-50">尚無學生資料</div> : 
             leaderboard.map((player, idx) => (
              <div key={player.id} className={`p-4 rounded-2xl border ${isDark ? 'bg-slate-800 border-slate-700' : 'bg-white border-slate-200 shadow-sm'}`}>
                <div className="flex justify-between items-center mb-2 border-b border-slate-700/30 pb-2">
                  <div className="font-bold text-lg flex items-center gap-2">
                    <span className="text-slate-400 text-sm">#{idx+1}</span>
                    {player.displayName}
                  </div>
                  <div className="text-blue-500 font-black">{player.totalScore?.toLocaleString() || 0} 分</div>
                </div>
                
                <div className="flex justify-between items-end">
                  <div className={`text-xs ${isDark ? 'text-slate-400' : 'text-slate-500'} flex gap-3`}>
                    <span className="flex items-center gap-1"><Star className="w-3 h-3 text-yellow-500" />{player.stars || 0} 星星</span>
                    <span className="flex items-center gap-1"><Award className="w-3 h-3 text-purple-400" />{player.achievementsCount || 0} 成就</span>
                  </div>
                  <div className="text-xs text-right max-w-[50%]">
                    <div className="text-rose-400 mb-1">最常錯:</div>
                    <div className="truncate opacity-80">{player.topWrongWords?.join(', ') || '無'}</div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
}

// --- 課程選擇 ---
function ScreenLesson({ setScreen, onSelect, progress, theme }) {
  const isDark = theme === 'dark';
  const lessons = Array.from({ length: 40 }, (_, i) => i + 1);

  return (
    <div className="flex-1 flex flex-col p-4 max-w-2xl mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-6 pt-4 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'} transition-colors`}>
          <ArrowLeft className="w-6 h-6" />
        </button>
        <h2 className="text-2xl font-bold flex-1">選擇課程</h2>
      </div>

      <div className="flex-1 overflow-y-auto pr-2 pb-8 custom-scrollbar">
        <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-3">
          {lessons.map(lesson => {
            let lessonStars = 0;
            ['recognition', 'scramble', 'spelling'].forEach(m => {
              lessonStars += progress.lessonStars[`${lesson}_${m}`] || 0;
            });
            const maxStars = 9;
            const progressRatio = lessonStars / maxStars;

            return (
              <button
                key={lesson}
                onClick={() => { onSelect(lesson); setScreen('mode'); }}
                className={`relative p-4 rounded-2xl border-2 text-left transition-all hover:-translate-y-1 overflow-hidden group
                  ${isDark ? 'border-slate-700 bg-slate-800 hover:border-blue-500' : 'border-slate-200 bg-white shadow-sm hover:border-blue-500 hover:shadow-md'}`}
              >
                <div className="absolute bottom-0 left-0 h-1 bg-blue-500 transition-all" style={{ width: `${progressRatio * 100}%` }}></div>
                <div className={`text-sm font-bold ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>Lesson</div>
                <div className="text-3xl font-black mb-2 group-hover:text-blue-500 transition-colors">{lesson}</div>
                <div className="flex items-center gap-1">
                  <Star className={`w-4 h-4 ${lessonStars > 0 ? 'text-yellow-400 fill-yellow-400' : (isDark ? 'text-slate-600' : 'text-slate-300')}`} />
                  <span className={`text-sm font-bold ${lessonStars > 0 ? 'text-yellow-500' : (isDark ? 'text-slate-500' : 'text-slate-400')}`}>
                    {lessonStars}/{maxStars}
                  </span>
                </div>
              </button>
            );
          })}
        </div>
      </div>
      <style dangerouslySetInnerHTML={{__html: `
        .custom-scrollbar::-webkit-scrollbar { width: 6px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: ${isDark ? '#334155' : '#cbd5e1'}; border-radius: 10px; }
      `}} />
    </div>
  );
}

// --- 模式選擇 ---
function ScreenMode({ setScreen, lesson, onSelect, difficulty, setDifficulty, theme }) {
  const isDark = theme === 'dark';

  return (
    <div className="flex-1 flex flex-col p-6 max-w-md mx-auto w-full">
      <div className="flex items-center gap-4 mb-8 pt-2">
        <button onClick={() => setScreen(lesson === 'review' ? 'vocab_book' : 'lesson')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}>
          <ArrowLeft className="w-6 h-6" />
        </button>
        <div>
          <div className={`text-sm font-bold ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>
            {lesson === 'review' ? '錯題特訓' : `Lesson ${lesson}`}
          </div>
          <h2 className="text-2xl font-bold">選擇挑戰模式</h2>
        </div>
      </div>

      <div className="space-y-4 mb-8">
        {Object.values(MODES).map((mode) => {
          const Icon = mode.icon;
          return (
            <button
              key={mode.id}
              onClick={() => { onSelect(mode.id); setScreen('game'); }}
              className={`w-full flex items-center p-4 rounded-2xl border-2 transition-all group hover:-translate-y-1
                ${isDark ? 'border-slate-700 bg-slate-800 hover:border-slate-500' : 'border-slate-200 bg-white shadow-sm hover:border-slate-300'}`}
            >
              <div className={`${mode.color} p-4 rounded-xl mr-4 group-hover:scale-110 transition-transform`}><Icon className="w-8 h-8 text-white" /></div>
              <div className="text-left flex-1">
                <h3 className="text-xl font-bold mb-1">{mode.name}</h3>
                <p className={`text-sm ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>{mode.desc}</p>
              </div>
            </button>
          );
        })}
      </div>

      <div>
        <h3 className="text-lg font-bold mb-3 pl-2">難度設定</h3>
        <div className={`flex rounded-2xl p-1 ${isDark ? 'bg-slate-800' : 'bg-slate-200'}`}>
          {Object.values(DIFFICULTIES).map((diff) => (
            <button
              key={diff.id} onClick={() => setDifficulty(diff.id)}
              className={`flex-1 py-3 text-center rounded-xl font-bold text-sm transition-all
                ${difficulty === diff.id ? (isDark ? 'bg-slate-700 shadow-md text-white' : 'bg-white shadow-md text-slate-800') : (isDark ? 'text-slate-400 hover:text-slate-200' : 'text-slate-500 hover:text-slate-700')}`}
            >
              {diff.name}
            </button>
          ))}
        </div>
        <div className="mt-4 px-2 flex justify-between text-xs font-medium">
          <span className={DIFFICULTIES[difficulty].color}>♥ {DIFFICULTIES[difficulty].lives} 生命</span>
          <span className="text-yellow-500">★ {DIFFICULTIES[difficulty].scoreMultiplier}x 分數</span>
          <span className="text-blue-500">⏱ {DIFFICULTIES[difficulty].timeRatio * 10}秒/題</span>
        </div>
      </div>
    </div>
  );
}

// --- 遊戲核心 (單人) ---
function ScreenGame({ setScreen, lesson, mode, difficulty, onGameOver, progress, theme }) {
  const isDark = theme === 'dark';
  
  const [words, setWords] = useState([]);
  const [currentIndex, setCurrentIndex] = useState(0);
  const [score, setScore] = useState(0);
  const [combo, setCombo] = useState(0);
  const [timeLeft, setTimeLeft] = useState(100);
  const [isPaused, setIsPaused] = useState(false);
  const [wrongWords, setWrongWords] = useState([]);
  const [feedback, setFeedback] = useState(null); 
  const [shake, setShake] = useState(false);

  const [options, setOptions] = useState([]); 
  const [scrambleLetters, setScrambleLetters] = useState([]); 
  const [selectedLetters, setSelectedLetters] = useState([]); 
  const [spellInput, setSpellInput] = useState(''); 

  // --- 套用獎勵增益 (Buffs) ---
  const hasExtraLife = progress.unlockedRewards?.includes('extra_life');
  const hasLuckyStar = progress.unlockedRewards?.includes('lucky_star');
  const initialLives = DIFFICULTIES[difficulty].lives + (hasExtraLife ? 1 : 0);
  const [lives, setLives] = useState(initialLives);

  const timerRef = useRef(null);
  const maxTime = DIFFICULTIES[difficulty].timeRatio * 100;

  useEffect(() => {
    let lessonWords = [];
    if (lesson === 'review') {
      lessonWords = Object.values(progress.wrongWordsList);
      if(lessonWords.length < 5) lessonWords = [...lessonWords, ...VOCABULARY[1]]; // Fallback
    } else {
      lessonWords = VOCABULARY[lesson] || [];
    }
    
    if (lessonWords.length < 5) lessonWords = [...lessonWords, { en: 'error', zh: '資料缺失' }];
    const shuffled = shuffleArray([...lessonWords]).slice(0, 10); 
    setWords(shuffled);
    prepareQuestion(shuffled[0], 0, shuffled);
  }, [lesson, progress.wrongWordsList]);

  const prepareQuestion = useCallback((word, index, allWords = words) => {
    if (!word) return;
    setFeedback(null);
    setTimeLeft(maxTime);
    speakWord(word.en); 
    
    if (mode === 'recognition') {
      const otherWords = shuffleArray(allWords.filter(w => w.en !== word.en)).slice(0, 3);
      setOptions(shuffleArray([word, ...otherWords]));
    } else if (mode === 'scramble') {
      setScrambleLetters(shuffleArray(word.en.split('').map((char, i) => ({ id: i, char }))));
      setSelectedLetters([]);
    } else if (mode === 'spelling') {
      setSpellInput('');
    }
    startTimer();
  }, [mode, words, maxTime]);

  const startTimer = useCallback(() => {
    clearInterval(timerRef.current);
    timerRef.current = setInterval(() => {
      setTimeLeft(prev => {
        if (prev <= 1) {
          clearInterval(timerRef.current);
          handleWrongAnswer('timeout');
          return 0;
        }
        return prev - 1;
      });
    }, 100); 
  }, []);

  useEffect(() => {
    if (isPaused || feedback) clearInterval(timerRef.current);
    else if (words.length > 0 && !feedback) startTimer();
    return () => clearInterval(timerRef.current);
  }, [isPaused, feedback, words, startTimer]);

  const handleCorrectAnswer = () => {
    clearInterval(timerRef.current);
    setFeedback('correct');
    playSound('correct');
    
    // 計算分數與幸運星增益 (10%)
    const basePoints = Math.floor((100 + Math.floor((timeLeft/maxTime)*50) + combo*10) * DIFFICULTIES[difficulty].scoreMultiplier);
    const finalPoints = hasLuckyStar ? Math.floor(basePoints * 1.1) : basePoints;

    setScore(prev => prev + finalPoints);
    setCombo(prev => prev + 1);
    setTimeout(nextQuestion, 1000);
  };

  const handleWrongAnswer = (type = 'wrong') => {
    clearInterval(timerRef.current);
    setFeedback(type);
    playSound('wrong');
    setCombo(0);
    setShake(true); setTimeout(() => setShake(false), 500);

    const currentWord = words[currentIndex];
    if (!wrongWords.find(w => w.en === currentWord.en)) setWrongWords(prev => [...prev, currentWord]);

    const newLives = lives - 1;
    setLives(newLives);

    if (newLives <= 0) setTimeout(() => finishGame(0), 1500); 
    else setTimeout(nextQuestion, 1500);
  };

  const nextQuestion = () => {
    const nextIdx = currentIndex + 1;
    if (nextIdx < words.length) {
      setCurrentIndex(nextIdx);
      prepareQuestion(words[nextIdx], nextIdx);
    } else {
      finishGame(lives);
    }
  };

  const finishGame = (finalLives) => {
    let stars = 0;
    if (finalLives > 0) {
      stars = 1;
      // 以該難度「原始最高血量」為滿血判定標準
      if (finalLives >= DIFFICULTIES[difficulty].lives) stars = 3; 
      else if (finalLives >= DIFFICULTIES[difficulty].lives - 1) stars = 2;
    }
    const result = { score, lives: finalLives, stars, wrongWords, won: finalLives > 0, mode, difficulty, lesson };
    onGameOver(result);
    sessionStorage.setItem('currentResult', JSON.stringify(result));
    setScreen('result_screen');
  };

  const handleOptionClick = (opt) => {
    if (feedback) return;
    if (opt.en === words[currentIndex].en) handleCorrectAnswer(); else handleWrongAnswer();
  };

  const handleScrambleClick = (letterObj) => {
    if (feedback) return;
    const newSelected = [...selectedLetters, letterObj];
    setSelectedLetters(newSelected);
    setScrambleLetters(prev => prev.filter(l => l.id !== letterObj.id));
    if (newSelected.length === words[currentIndex].en.length) {
      if (newSelected.map(l => l.char).join('') === words[currentIndex].en) handleCorrectAnswer(); else handleWrongAnswer();
    }
  };

  const handleScrambleUndo = (letterObj) => {
    if (feedback) return;
    setSelectedLetters(prev => prev.filter(l => l.id !== letterObj.id));
    setScrambleLetters(prev => [...prev, letterObj]);
  };

  const handleSpellingSubmit = (e) => {
    e.preventDefault();
    if (feedback || !spellInput.trim()) return;
    if (spellInput.toLowerCase().trim() === words[currentIndex].en.toLowerCase()) handleCorrectAnswer(); else handleWrongAnswer();
  };

  if (isPaused) {
    return (
      <div className="flex-1 flex items-center justify-center p-6 bg-slate-900/90 backdrop-blur-sm z-50 fixed inset-0">
        <div className={`${isDark ? 'bg-slate-800' : 'bg-white'} p-8 rounded-3xl max-w-sm w-full text-center shadow-2xl`}>
          <h2 className="text-3xl font-black mb-6">遊戲已暫停</h2>
          <div className="space-y-4">
            <button onClick={() => setIsPaused(false)} className="w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-4 rounded-xl text-lg">繼續遊戲</button>
            <button onClick={() => setScreen('mode')} className={`w-full ${isDark?'bg-slate-700 text-white':'bg-slate-200 text-slate-800'} font-bold py-4 rounded-xl text-lg`}>放棄並返回</button>
          </div>
        </div>
      </div>
    );
  }

  if (screen === 'result_screen') {
    return <ScreenResult setScreen={setScreen} result={JSON.parse(sessionStorage.getItem('currentResult'))} theme={theme} />;
  }

  if (words.length === 0) return <div className="flex-1 flex items-center justify-center font-bold">載入中...</div>;

  const currentWord = words[currentIndex] || {};
  const progressPercent = ((currentIndex) / words.length) * 100;
  let timerColor = 'bg-green-500';
  if (timeLeft < maxTime * 0.5) timerColor = 'bg-yellow-500';
  if (timeLeft < maxTime * 0.2) timerColor = 'bg-red-500';

  return (
    <div className={`flex-1 flex flex-col max-w-2xl mx-auto w-full h-screen ${shake ? 'animate-shake' : ''}`}>
      <div className={`${isDark ? 'bg-slate-800' : 'bg-white shadow-sm'} p-4 flex justify-between items-center z-10 rounded-b-2xl mb-4`}>
        <div className="flex flex-col gap-1">
          <div className="flex items-center gap-1 text-rose-500 font-bold">
            <Heart className="w-5 h-5 fill-current" /> {lives}
            {hasExtraLife && lives > DIFFICULTIES[difficulty].lives && <Shield className="w-3 h-3 text-amber-500 ml-1" />}
          </div>
          {combo > 1 && <div className="text-sm font-bold text-orange-500 flex items-center animate-bounce"><Zap className="w-4 h-4 fill-current" /> {combo} 連擊!</div>}
        </div>
        <div className="text-center flex-1">
          <div className="text-2xl font-black text-blue-500 flex items-center justify-center gap-1">
            {score.toLocaleString()}
            {hasLuckyStar && <Star className="w-3 h-3 text-yellow-500 fill-current" />}
          </div>
          <div className={`text-xs font-bold ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>{currentIndex + 1} / {words.length}</div>
        </div>
        <button onClick={() => setIsPaused(true)} className={`p-2 rounded-lg ${isDark ? 'hover:bg-slate-700 text-slate-400' : 'hover:bg-slate-100 text-slate-500'}`}><Pause className="w-6 h-6" /></button>
      </div>

      <div className="px-4 mb-6">
        <div className={`h-2 ${isDark ? 'bg-slate-800' : 'bg-slate-200'} rounded-full overflow-hidden mb-2`}><div className="h-full bg-blue-500 transition-all duration-300" style={{ width: `${progressPercent}%` }}></div></div>
        <div className={`h-3 ${isDark ? 'bg-slate-800' : 'bg-slate-200'} rounded-full overflow-hidden`}><div className={`h-full ${timerColor} transition-all duration-100 linear`} style={{ width: `${(timeLeft / maxTime) * 100}%` }}></div></div>
      </div>

      <div className="flex-1 flex flex-col px-4 pb-6 overflow-hidden">
        <div className="flex-1 flex flex-col items-center justify-center mb-8 relative">
          {feedback && (
            <div className="absolute inset-0 flex items-center justify-center z-20 bg-slate-900/50 backdrop-blur-sm rounded-3xl animate-fade-in">
              <div className={`text-center p-6 rounded-2xl ${feedback === 'correct' ? 'bg-green-500' : 'bg-rose-500'} text-white shadow-2xl transform scale-110`}>
                {feedback === 'correct' ? <Check className="w-16 h-16 mx-auto mb-2" /> : <X className="w-16 h-16 mx-auto mb-2" />}
                <div className="text-2xl font-bold mb-1">{feedback === 'correct' ? '答對了！' : feedback === 'timeout' ? '時間到！' : '答錯了！'}</div>
                {feedback !== 'correct' && <div className="text-lg opacity-90">正確答案: {currentWord.en}</div>}
              </div>
            </div>
          )}
          <div className="text-center w-full relative">
            <button onClick={() => speakWord(currentWord.en)} className="absolute -top-12 right-0 p-2 rounded-full bg-blue-500/10 text-blue-500 hover:bg-blue-500 hover:text-white transition-colors">
              <Volume2 className="w-6 h-6" />
            </button>
            <span className={`inline-block px-4 py-1 rounded-full text-sm font-bold mb-6 ${MODES[mode].color} text-white`}>{MODES[mode].name}</span>
            <h2 className="text-5xl md:text-6xl font-black mb-4 tracking-tight">{mode === 'recognition' ? currentWord.en : currentWord.zh}</h2>
            {mode === 'recognition' && <p className={`text-lg ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>請選擇正確的中文翻譯</p>}
          </div>
        </div>

        <div className="w-full shrink-0">
          {mode === 'recognition' && (
            <div className="grid grid-cols-2 gap-3">
              {options.map((opt, i) => (
                <button key={i} onClick={() => handleOptionClick(opt)} disabled={!!feedback} className={`p-4 md:p-6 rounded-2xl text-lg md:text-xl font-bold transition-all active:scale-95 ${isDark ? 'bg-slate-800 hover:bg-blue-600 border border-slate-700' : 'bg-white shadow border border-slate-200 hover:border-blue-500 hover:bg-blue-50 text-slate-800'}`}>
                  {opt.zh}
                </button>
              ))}
            </div>
          )}
          {mode === 'scramble' && (
            <div className="flex flex-col items-center gap-8 w-full">
              <div className="flex flex-wrap justify-center gap-2 min-h-[60px] p-4 w-full bg-slate-800/50 rounded-2xl border-2 border-dashed border-slate-600">
                {selectedLetters.map((l) => (
                  <button key={l.id} onClick={() => handleScrambleUndo(l)} disabled={!!feedback} className="w-12 h-14 md:w-14 md:h-16 bg-blue-600 text-white rounded-xl text-2xl font-bold shadow-md transform transition active:scale-90">{l.char}</button>
                ))}
              </div>
              <div className="flex flex-wrap justify-center gap-3">
                {scrambleLetters.map((l) => (
                  <button key={l.id} onClick={() => handleScrambleClick(l)} disabled={!!feedback} className={`w-12 h-14 md:w-14 md:h-16 rounded-xl text-2xl font-bold shadow-sm transition-transform active:scale-90 ${isDark ? 'bg-slate-700 text-slate-200 hover:bg-slate-600' : 'bg-white text-slate-800 hover:bg-slate-100 border border-slate-200'}`}>{l.char}</button>
                ))}
              </div>
            </div>
          )}
          {mode === 'spelling' && (
            <form onSubmit={handleSpellingSubmit} className="w-full flex flex-col gap-4">
              <input type="text" autoFocus value={spellInput} onChange={(e) => setSpellInput(e.target.value)} disabled={!!feedback} placeholder="輸入英文單字..." className={`w-full text-center text-3xl p-6 rounded-2xl outline-none transition-all ${isDark ? 'bg-slate-800 text-white focus:ring-2 focus:ring-blue-500 border border-slate-700' : 'bg-white text-slate-900 border-2 border-slate-200 focus:border-blue-500 shadow-inner'}`} autoComplete="off" spellCheck="false" />
              <button type="submit" disabled={!!feedback || !spellInput.trim()} className="w-full bg-rose-600 hover:bg-rose-500 disabled:opacity-50 text-white font-bold py-4 rounded-2xl text-xl transition-all active:scale-95">送出答案</button>
            </form>
          )}
        </div>
      </div>
      <style dangerouslySetInnerHTML={{__html: `@keyframes shake { 0%, 100% { transform: translateX(0); } 25% { transform: translateX(-10px); } 50% { transform: translateX(10px); } 75% { transform: translateX(-10px); } } .animate-shake { animation: shake 0.4s cubic-bezier(.36,.07,.19,.97) both; } @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } } .animate-fade-in { animation: fadeIn 0.2s ease-out forwards; }`}} />
    </div>
  );
}

// --- 結算畫面 (單人) ---
function ScreenResult({ setScreen, result, theme }) {
  const isDark = theme === 'dark';
  const { won, score, stars, wrongWords, lives } = result;

  return (
    <div className="flex-1 flex flex-col items-center justify-center p-6 max-w-md mx-auto w-full text-center">
      <div className={`w-full p-8 rounded-3xl shadow-2xl mb-8 relative overflow-hidden ${isDark ? 'bg-slate-800' : 'bg-white border border-slate-200'}`}>
        <div className={`absolute top-0 left-0 w-full h-2 ${won ? 'bg-green-500' : 'bg-rose-500'}`}></div>
        <div className="mb-6">
          {won ? <Trophy className="w-20 h-20 mx-auto text-yellow-500 mb-4 animate-bounce" /> : <RotateCcw className="w-20 h-20 mx-auto text-rose-500 mb-4" />}
          <h2 className="text-4xl font-black mb-2">{won ? '挑戰成功！' : '遊戲結束'}</h2>
          <div className="flex justify-center gap-2 mb-6">
            {[1, 2, 3].map(star => <Star key={star} className={`w-10 h-10 ${star <= stars ? 'text-yellow-400 fill-yellow-400' : (isDark ? 'text-slate-700' : 'text-slate-200')} transition-all duration-500`} />)}
          </div>
          {stars > 0 && <div className="text-amber-500 font-bold flex justify-center items-center gap-1">+ {stars} 獲得星幣！</div>}
        </div>
        <div className="grid grid-cols-2 gap-4 mb-6">
          <div className={`p-4 rounded-xl ${isDark ? 'bg-slate-900/50' : 'bg-slate-50'}`}>
            <div className={`text-sm ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>最終得分</div>
            <div className="text-2xl font-black text-blue-500">{score.toLocaleString()}</div>
          </div>
          <div className={`p-4 rounded-xl ${isDark ? 'bg-slate-900/50' : 'bg-slate-50'}`}>
            <div className={`text-sm ${isDark ? 'text-slate-400' : 'text-slate-500'} mb-1`}>剩餘生命</div>
            <div className="text-2xl font-black text-rose-500">{lives}</div>
          </div>
        </div>
        {wrongWords.length > 0 && (
          <div className="text-left mt-4">
            <h4 className="font-bold mb-2 flex items-center gap-2 text-rose-500">
              <Bookmark className="w-4 h-4" /> 已加入單字本 ({wrongWords.length})
            </h4>
            <div className={`max-h-32 overflow-y-auto rounded-lg p-3 text-sm space-y-2 ${isDark ? 'bg-slate-900/50' : 'bg-slate-50'}`}>
              {wrongWords.map((w, i) => (
                <div key={i} className="flex justify-between border-b border-slate-700/30 pb-1 last:border-0">
                  <span className="font-bold">{w.en}</span>
                  <span className={isDark ? 'text-slate-400' : 'text-slate-500'}>{w.zh}</span>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
      <div className="w-full space-y-3">
        <button onClick={() => setScreen('mode')} className="w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-4 rounded-2xl text-lg flex justify-center items-center gap-2 transition-all">
          <RotateCcw className="w-5 h-5" /> 再來一局
        </button>
        <button onClick={() => setScreen('home')} className={`w-full font-bold py-4 rounded-2xl text-lg flex justify-center items-center gap-2 transition-all ${isDark ? 'bg-slate-800 hover:bg-slate-700 text-slate-300' : 'bg-slate-200 hover:bg-slate-300 text-slate-700'}`}>
          <Home className="w-5 h-5" /> 返回首頁
        </button>
      </div>
    </div>
  );
}

// --- 進度統計 ---
function ScreenStats({ setScreen, progress, theme }) {
  const isDark = theme === 'dark';
  const winRate = progress.gamesPlayed > 0 ? Math.round((progress.gamesWon / progress.gamesPlayed) * 100) : 0;

  return (
    <div className="flex-1 flex flex-col p-6 max-w-md mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-8 pt-2 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}><ArrowLeft className="w-6 h-6" /></button>
        <h2 className="text-2xl font-bold">進度統計</h2>
      </div>
      <div className="flex-1 overflow-y-auto space-y-4 pb-8">
        <div className="grid grid-cols-2 gap-4">
          <StatCard title="總分數" value={progress.totalScore.toLocaleString()} icon={Trophy} color="text-yellow-500" isDark={isDark} />
          <StatCard title="歷史總星星" value={`${progress.stars}`} icon={Star} color="text-yellow-400" isDark={isDark} />
          <StatCard title="遊玩次數" value={progress.gamesPlayed} icon={Play} color="text-blue-500" isDark={isDark} />
          <StatCard title="勝率" value={`${winRate}%`} icon={Zap} color="text-green-500" isDark={isDark} />
        </div>
        <div className={`mt-8 p-6 rounded-3xl ${isDark ? 'bg-slate-800' : 'bg-white shadow border border-slate-100'}`}>
          <h3 className="text-lg font-bold mb-4 flex items-center gap-2"><Clock className="w-5 h-5 text-blue-500" /> 最近遊戲紀錄</h3>
          <div className="space-y-3">
            {progress.history.slice(-5).reverse().map((record, i) => (
              <div key={i} className={`flex items-center justify-between p-3 rounded-xl ${isDark ? 'bg-slate-900/50' : 'bg-slate-50'}`}>
                <div>
                  <div className="font-bold flex items-center gap-2">Lesson {record.lesson} <span className={`text-[10px] px-2 py-0.5 rounded-full text-white ${MODES[record.mode]?.color || 'bg-slate-500'}`}>{MODES[record.mode]?.name || '未知'}</span></div>
                  <div className={`text-xs mt-1 ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>{new Date(record.date).toLocaleDateString()}</div>
                </div>
                <div className={`font-black ${record.won ? 'text-green-500' : 'text-rose-500'}`}>{record.score}</div>
              </div>
            ))}
            {progress.history.length === 0 && <div className={`text-center py-4 ${isDark ? 'text-slate-500' : 'text-slate-400'}`}>尚無紀錄</div>}
          </div>
        </div>
      </div>
    </div>
  );
}

function StatCard({ title, value, icon: Icon, color, isDark }) {
  return (
    <div className={`p-5 rounded-3xl ${isDark ? 'bg-slate-800' : 'bg-white shadow border border-slate-100'}`}>
      <div className={`text-sm mb-2 ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>{title}</div>
      <div className={`text-2xl font-black flex items-center gap-2 ${color}`}><Icon className="w-6 h-6" /> {value}</div>
    </div>
  );
}

// --- 成就系統 ---
function ScreenAchievements({ setScreen, progress, theme }) {
  const isDark = theme === 'dark';

  return (
    <div className="flex-1 flex flex-col p-6 max-w-md mx-auto w-full h-screen">
      <div className="flex items-center gap-4 mb-8 pt-2 shrink-0">
        <button onClick={() => setScreen('home')} className={`p-2 rounded-xl ${isDark ? 'bg-slate-800 hover:bg-slate-700' : 'bg-slate-200 hover:bg-slate-300'}`}><ArrowLeft className="w-6 h-6" /></button>
        <h2 className="text-2xl font-bold flex-1">成就系統</h2>
        <div className="font-bold text-blue-500 bg-blue-500/10 px-3 py-1 rounded-full">{progress.achievements.length} / {ACHIEVEMENTS.length}</div>
      </div>
      <div className="flex-1 overflow-y-auto space-y-4 pb-8">
        {ACHIEVEMENTS.map(ach => {
          const isUnlocked = progress.achievements.includes(ach.id);
          return (
            <div key={ach.id} className={`flex items-center p-4 rounded-2xl border-2 transition-all ${isUnlocked ? (isDark ? 'bg-slate-800 border-yellow-500/30' : 'bg-white border-yellow-400 shadow') : (isDark ? 'bg-slate-900 border-slate-800 opacity-60' : 'bg-slate-50 border-slate-200 opacity-60 grayscale')}`}>
              <div className={`w-14 h-14 rounded-full flex items-center justify-center text-3xl shrink-0 mr-4 ${isUnlocked ? (isDark ? 'bg-slate-700' : 'bg-yellow-50') : (isDark ? 'bg-slate-800' : 'bg-slate-200')}`}>{ach.icon}</div>
              <div className="flex-1">
                <h3 className={`text-lg font-bold mb-1 ${isUnlocked ? '' : (isDark ? 'text-slate-500' : 'text-slate-400')}`}>{ach.name}</h3>
                <p className={`text-sm ${isDark ? 'text-slate-400' : 'text-slate-500'}`}>{ach.desc}</p>
              </div>
              {isUnlocked && <Check className="w-6 h-6 text-yellow-500 shrink-0" />}
            </div>
          );
        })}
      </div>
    </div>
  );
}