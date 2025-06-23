import React from 'react';

import { Plus, X, Calendar, Clock, MapPin, Bus, Briefcase, Trash2, Pencil, Hotel, Save, Sparkles, LoaderCircle, Languages } from 'lucide-react';



// --- Helper function to get dates between a range (Timezone-safe) ---

const getDatesInRange = (startDate, endDate) => {

  if (!startDate || !endDate) return [];

  const dates = [];

  const startParts = startDate.split('-').map(Number);

  const endParts = endDate.split('-').map(Number);

  

  let currentDate = new Date(Date.UTC(startParts[0], startParts[1] - 1, startParts[2]));

  const lastDate = new Date(Date.UTC(endParts[0], endParts[1] - 1, endParts[2]));



  while (currentDate <= lastDate) {

    const year = currentDate.getUTCFullYear();

    const month = String(currentDate.getUTCMonth() + 1).padStart(2, '0');

    const day = String(currentDate.getUTCDate()).padStart(2, '0');

    dates.push(`${year}-${month}-${day}`);

    currentDate.setUTCDate(currentDate.getUTCDate() + 1);

  }

  return dates;

};



// --- Seed Data (Initial Data) - Updated with Budapest & Oslo Trip ---

const initialTrip = {

  id: 'trip1',

  title: 'åçå©èæªå¨éåé',

  destination: 'åçå©å¸éä½©æ¯ & æªå¨å¥§æ¯é¸',

  accommodations: [

    {

      id: 1,

      name: 'Budapest, TÅ±zoltÃ³ u. 50-56, 1094 åçå©',

      checkInDate: '2025-07-04',

      checkOutDate: '2025-07-06',

      dailyTimes: {

        '2025-07-04': { wakeUp: '09:00', return: '21:30' },

        '2025-07-05': { wakeUp: '08:00', return: '23:00' },

        '2025-07-06': { wakeUp: '08:00', return: '17:30' },

      }

    },

    {

      id: 2,

      name: 'å®¿è (å¥§æ¯é¸)',

      checkInDate: '2025-07-06',

      checkOutDate: '2025-07-12',

      dailyTimes: {

        '2025-07-06': { wakeUp: 'N/A', return: '23:59' },

        '2025-07-07': { wakeUp: '09:00', return: '22:00' },

        '2025-07-08': { wakeUp: '09:00', return: '22:00' },

        '2025-07-09': { wakeUp: '09:00', return: '22:00' },

        '2025-07-10': { wakeUp: '09:00', return: '22:00' },

        '2025-07-11': { wakeUp: '09:00', return: '22:00' },

        '2025-07-12': { wakeUp: '09:00', return: 'N/A' },

      }

    }

  ],

  itinerary: [

    { id: 1, date: '2025-07-04', time: '09:00', location: 'âï¸ æµéå¸éä½©æ¯ææ¯ç¹Â·è²»å«è¨åéæ©å ´', transport: 'åªåå¨æ©å ´å¯å­è¡æ' },

    { id: 2, date: '2025-07-04', time: '10:00', location: 'æ©å ´åå¾å¸å (DeÃ¡k Ferenc tÃ©r)', transport: '100E æ©å ´å·´å£« (è²»ç¨: 2200 HUF)' },

    { id: 3, date: '2025-07-04', time: '11:00', location: 'å¸éä½©æ¯ä¸­å¤®å¸å ´', transport: 'å¾DeÃ¡k Ferenc tÃ©ræ­ä¹M3å°éµè³KÃ¡lvin tÃ©rç«' },

    { id: 4, date: '2025-07-04', time: '13:00', location: 'åé¤ï¼ ä¸­å¤®å¸å ´å§', transport: 'ç¶å°ç¾é£' },

    { id: 5, date: '2025-07-04', time: '14:30', location: 'å¡åå°¼æº«æ³æµ´å ´', transport: 'å°éµM3è½M1è³SzÃ©chenyi fÃ¼rdÅç«' },

    { id: 6, date: '2025-07-04', time: '18:00', location: 'æé¤', transport: 'å¡åå°¼æµ´å ´éè¿' },

    { id: 7, date: '2025-07-04', time: '20:00', location: 'ð¢ å¤çæ²³éè¹ (çªæ ¼éºç¹æ©)', transport: 'å°éµM1è½è¼è»4/6èç·' },

    { id: 8, date: '2025-07-05', time: '08:00', location: 'âï¸ æ©é¤', transport: 'é£¯åºæéè¿åå¡é¤¨' },

    { id: 9, date: '2025-07-05', time: '09:00', location: 'ð° å¸éåå ¡', transport: 'å°éµM3è½å·´å£«16è' },

    { id: 10, date: '2025-07-05', time: '11:00', location: 'ð­ æ¼äººå ¡', transport: 'å¾å¸éåå ¡æ­¥è¡' },

    { id: 11, date: '2025-07-05', time: '12:30', location: 'åé¤', transport: 'å¸éåå ¡åéè¿æ¯è§é¤å»³' },

    { id: 12, date: '2025-07-05', time: '14:00', location: 'âªï¸ é¦¬å ä»æå ', transport: 'å¾æ¼äººå ¡æ­¥è¡' },

    { id: 13, date: '2025-07-05', time: '15:30', location: 'ð° Ruszwurm Confectionery å³çµ±çé»', transport: 'å¾é¦¬å ä»æå æ­¥è¡' },

    { id: 14, date: '2025-07-05', time: '18:00', location: 'æé¤', transport: 'ç¶å¤ªåéè¿' },

    { id: 15, date: '2025-07-05', time: '20:00', location: 'ð» é«é©å»¢å¢éå§ (Szimpla Kert)', transport: 'å¾åå ¡åæ­å·´å£«16è' },

    { id: 16, date: '2025-07-06', time: '09:00', location: 'ðï¸ é£¯åºéæ¿ä¸¦å¯æ¾è¡æ', transport: '' },

    { id: 17, date: '2025-07-06', time: '09:30', location: 'ðï¸ åçå©åæå¤§å»', transport: 'æ­ä¹å°éµM3ç·' },

    { id: 18, date: '2025-07-06', time: '11:30', location: 'åé¤ï¼ Madal åå¡é¤¨', transport: 'å¾åæå¤§å»æ­¥è¡' },

    { id: 19, date: '2025-07-06', time: '13:30', location: 'âªï¸ èä¼ä»ç¹è¬èæ®¿', transport: 'å¾Madal åå¡é¤¨æ­¥è¡' },

    { id: 20, date: '2025-07-06', time: '16:30', location: 'ð è¿åé£¯åºæ¿è¡æ', transport: 'æ­ä¹å°éµM3ç·' },

    { id: 21, date: '2025-07-06', time: '17:30', location: 'ð« å¾é£¯åºåºç¼åå¾æ©å ´', transport: 'å°éµM3è½200Eå·´å£«' },

    { id: 22, date: '2025-07-06', time: '18:30', location: 'âï¸ æµéå¸éä½©æ¯æ©å ´', transport: 'æºåç»æ©' },

    { id: 23, date: '2025-07-06', time: '21:25', location: 'âï¸ é£æ©èµ·é£ (åå¾å¥§æ¯é¸)', transport: '' },

    { id: 24, date: '2025-07-06', time: '23:30', location: 'ð¬ æµéå¥§æ¯é¸æ©å ´', transport: '' },

    { id: 25, date: '2025-07-12', time: '10:00', location: 'å¾ãå®¿èãåºç¼åå¾æ©å ´', transport: '' },

    { id: 26, date: '2025-07-12', time: '13:05', location: 'âï¸ é£æ©èµ·é£ (è¿åå°ç£)', transport: 'æéæå¿«ï¼' },

  ],

  packingList: [

    { id: 101, name: 'éè¦æéï¼åæå¤§å»ãéè¹ãæº«æ³å»ºè­°æåé è¨', packed: false },

    { id: 102, name: 'äº¤éæéï¼å»ºè­°è³¼è²·å¸éä½©æ¯72å°æäº¤éå¡', packed: false },

    { id: 103, name: 'å®å¨æéï¼æ³¨æææï¼çæåäººè²¡ç©', packed: false },

    { id: 104, name: 'è¡æå¯å­ï¼æ©å ´å¯é è¨ Lalalocker æ KKday', packed: false },

    { id: 105, name: 'è­·ç§ & ç°½è­', packed: false },

    { id: 106, name: 'ç¦æ (HUF) & æªå¨åæ (NOK) ç¾é & ä¿¡ç¨å¡', packed: false },

    { id: 107, name: 'æ³³è¡£ (æº«æ³ç¨)', packed: false },

    { id: 108, name: 'è¡£ç©ï¼çºæªå¨æºåä¿æè¡£ç©', packed: false },

  ]

};



// --- Main App Component ---

export default function App() {

  const [trip, setTrip] = React.useState(initialTrip);

  const [activeView, setActiveView] = React.useState('itinerary');

  const [displayedItinerary, setDisplayedItinerary] = React.useState([]);

  const [modalState, setModalState] = React.useState({ isOpen: false, mode: 'add', type: 'itinerary', data: null });

  

  // State for AI Features

  const [isAISuggestionModalOpen, setIsAISuggestionModalOpen] = React.useState(false);

  const [aiSuggestions, setAiSuggestions] = React.useState(null);

  const [isAILoading, setIsAILoading] = React.useState(false);

  const [aiError, setAiError] = React.useState('');

  

  const [isTranslateModalOpen, setIsTranslateModalOpen] = React.useState(false);

  const [isTranslating, setIsTranslating] = React.useState(false);

  const [translatedContent, setTranslatedContent] = React.useState('');

  const [translateError, setTranslateError] = React.useState('');





  // --- Theming ---

  const colors = {

    bg: 'bg-[#FDF6E3]', // Papyrus

    cardBg: 'bg-white/70',

    navBg: 'bg-[#F3EAD8]',

    primary: 'text-[#C84B31]', // Paprika Red

    primaryBg: 'bg-[#C84B31]',

    secondary: 'text-[#2E4F4F]', // Danube Green

    secondaryBg: 'bg-[#2E4F4F]',

    accent: 'text-[#EC9B3B]', // Goulash Gold

    accentBg: 'bg-[#EC9B3B]',

    textPrimary: 'text-stone-800',

    textSecondary: 'text-stone-600'

  };



  React.useEffect(() => {

    const { accommodations, itinerary: userItinerary } = trip;

    let autoEvents = [];



    accommodations.forEach(acc => {

      if (!acc.name || !acc.checkInDate || !acc.checkOutDate) return;

      const dateRange = getDatesInRange(acc.checkInDate, acc.checkOutDate);

      dateRange.forEach(currentDateStr => {

        const dayTimes = acc.dailyTimes[currentDateStr] || { wakeUp: '09:00', return: '22:00' };

        const isCheckInDay = currentDateStr === acc.checkInDate;

        const isCheckOutDay = currentDateStr === acc.checkOutDate;

        const isIntermediateDay = !isCheckInDay && !isCheckOutDay;



        if (isCheckInDay && isCheckOutDay) {

            autoEvents.push({ id: `auto-depart-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.wakeUp, location: `å¾ ${acc.name} åºç¼`, isAuto: true });

            autoEvents.push({ id: `auto-return-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.return, location: `è¿å ${acc.name} (éæ¿)`, isAuto: true });

        } else if (isCheckInDay) {

            autoEvents.push({ id: `auto-return-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.return, location: `è¿å ${acc.name} (å¥ä½)`, isAuto: true });

        } else if (isCheckOutDay) {

            autoEvents.push({ id: `auto-depart-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.wakeUp, location: `å¾ ${acc.name} åºç¼ (éæ¿)`, isAuto: true });

        } else if (isIntermediateDay) {

            autoEvents.push({ id: `auto-depart-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.wakeUp, location: `å¾ ${acc.name} åºç¼ (æ¯æ¥)`, isAuto: true });

            autoEvents.push({ id: `auto-return-${acc.id}-${currentDateStr}`, date: currentDateStr, time: dayTimes.return, location: `è¿å ${acc.name} (æ¯æ¥)`, isAuto: true });

        }

      });

    });



    const combined = [...userItinerary, ...autoEvents];

    combined.sort((a, b) => new Date(`${a.date}T${a.time}`) - new Date(`${b.date}T${b.time}`));

    setDisplayedItinerary(combined);

  }, [trip.itinerary, trip.accommodations]);

  

  const handleDestinationChange = (newDestination) => setTrip(prev => ({...prev, destination: newDestination}));

  const handleTitleChange = (newTitle) => setTrip(prev => ({ ...prev, title: newTitle }));

  const handleSaveAccommodations = (newAccommodations) => setTrip(prev => ({ ...prev, accommodations: newAccommodations }));



  const handleSaveItem = (item) => {

    const { mode, type } = modalState;

    if (type === 'itinerary') {

        if (mode === 'add') setTrip(prev => ({ ...prev, itinerary: [...prev.itinerary, { ...item, id: Date.now() }]}));

        else setTrip(prev => ({ ...prev, itinerary: prev.itinerary.map(i => i.id === item.id ? item : i) }));

    } else {

        if (mode === 'add') setTrip(prev => ({ ...prev, packingList: [...prev.packingList, { ...item, id: Date.now(), packed: false }] }));

        else setTrip(prev => ({ ...prev, packingList: prev.packingList.map(p => p.id === item.id ? { ...item, packed: p.packed } : p) }));

    }

    closeModal();

  };

  

  // --- AI Feature Functions ---

  const handleGetAIPackingSuggestions = async () => {

    setIsAILoading(true);

    setAiError('');



    const { destination, accommodations } = trip;

    const checkIn = accommodations[0]?.checkInDate;

    const checkOut = accommodations[accommodations.length - 1]?.checkOutDate;



    if (!destination || !checkIn || !checkOut) {

        setAiError("è«åè¨­å®æéç®çå°ãå¥ä½èéæ¿æ¥æã");

        setIsAILoading(false);

        return;

    }

    

    const prompt = `çºä¸è¶åå¾ã${destination}ãçæç¨ï¼ç¢çä¸ä»½å»ºè­°çè¡ææ¸å®ãæéæ¥æçº ${checkIn} å° ${checkOut}ãè«èæ®éåå°é»èå­£ç¯çå¸åå¤©æ°£ãå°æ¸å®åçºãå¿éåãåãé¸å¸¶åãå©é¡ã`;



    try {

        const payload = { 

            contents: [{ role: "user", parts: [{ text: prompt }] }],

            generationConfig: {

                responseMimeType: "application/json",

                responseSchema: { type: "OBJECT", properties: { essentials: { type: "ARRAY", items: { type: "STRING" } }, optional: { type: "ARRAY", items: { type: "STRING" } } }, required: ["essentials", "optional"] }

            }

        };

        const apiKey = "";

        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

        const response = await fetch(apiUrl, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });

        if (!response.ok) throw new Error(`API request failed with status ${response.status}`);

        const result = await response.json();

        if (result.candidates && result.candidates.length > 0) {

            const text = result.candidates[0].content.parts[0].text;

            const suggestions = JSON.parse(text);

            setAiSuggestions(suggestions);

            setIsAISuggestionModalOpen(true);

        } else { throw new Error("æªè½å¾ AI æ¶å°ææçå»ºè­°ã"); }

    } catch (error) {

        setAiError(`ç¡æ³ç²å AI å»ºè­°ï¼${error.message}`);

    } finally {

        setIsAILoading(false);

    }

  };



  const handleAddSuggestedItems = (itemsToAdd) => {

    const existingNames = new Set(trip.packingList.map(item => item.name));

    const newItems = itemsToAdd.filter(name => !existingNames.has(name)).map(name => ({ id: Date.now() + Math.random(), name, packed: false }));

    setTrip(prev => ({ ...prev, packingList: [...prev.packingList, ...newItems] }));

    setIsAISuggestionModalOpen(false);

    setAiSuggestions(null);

  };

  

  const handleTranslateTrip = async (targetLanguage) => {

    if (!targetLanguage) {

        setTranslateError("è«è¼¸å¥è¦ç¿»è­¯çèªè¨ã");

        return;

    }

    setIsTranslating(true);

    setTranslateError('');

    setTranslatedContent('');



    let fullTripDetails = `æéè¨ç«: ${trip.title}\nç®çå°: ${trip.destination}\n\n`;

    fullTripDetails += "ä½å®¿è³è¨:\n";

    trip.accommodations.forEach(acc => {

        fullTripDetails += `- ${acc.name} (${acc.checkInDate} to ${acc.checkOutDate})\n`;

    });

    fullTripDetails += "\nè¡ç¨ç´°ç¯:\n";

    displayedItinerary.forEach(item => {

        fullTripDetails += `- ${item.date} ${item.time}: ${item.location} (äº¤é: ${item.transport || 'N/A'})\n`;

    });

    fullTripDetails += "\nè¡ææ¸å®:\n";

    trip.packingList.forEach(item => {

        fullTripDetails += `- ${item.name}\n`;

    });



    const prompt = `Translate the following travel itinerary into ${targetLanguage}. Keep the original structure, dates, and times. Only translate the descriptive text like locations, transport methods, and notes.\n\n${fullTripDetails}`;

    

    try {

        const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };

        const apiKey = "";

        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

        const response = await fetch(apiUrl, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });

        if (!response.ok) throw new Error(`API request failed with status ${response.status}`);

        const result = await response.json();

        if (result.candidates && result.candidates[0]?.content.parts[0]?.text) {

            setTranslatedContent(result.candidates[0].content.parts[0].text);

        } else {

            throw new Error("æ¶å°çç¿»è­¯å§å®¹ç¡æã");

        }

    } catch (error) {

        setTranslateError(`ç¿»è­¯å¤±æï¼${error.message}`);

    } finally {

        setIsTranslating(false);

    }

  };





  const handleEditItem = (item, type) => setModalState({ isOpen: true, mode: 'edit', type, data: item });

  const handleDeleteItem = (id, type) => {

      if (type === 'itinerary') setTrip(prev => ({ ...prev, itinerary: prev.itinerary.filter(i => i.id !== id) }));

      else setTrip(prev => ({ ...prev, packingList: prev.packingList.filter(p => p.id !== id) }));

  };

  const togglePackedStatus = (id) => setTrip(prev => ({ ...prev, packingList: prev.packingList.map(i => i.id === id ? { ...i, packed: !i.packed } : i)}));

  const openAddModal = () => setModalState({ isOpen: true, mode: 'add', type: activeView, data: null });

  const closeModal = () => setModalState({ isOpen: false, mode: 'add', type: 'itinerary', data: null });



  return (

    <div className={`${colors.bg} ${colors.textPrimary} min-h-screen font-sans`}>

      <div className="container mx-auto max-w-2xl p-4">

        <Header title={trip.title} destination={trip.destination} onTitleChange={handleTitleChange} onDestinationChange={handleDestinationChange} onTranslate={() => setIsTranslateModalOpen(true)} colors={colors} />

        <Nav activeView={activeView} setActiveView={setActiveView} colors={colors} />

        

        <main className={`${colors.cardBg} rounded-xl shadow-lg p-4 sm:p-6 mt-4 backdrop-blur-sm border border-white/20`}>

          {activeView === 'itinerary' && <ItineraryView itinerary={displayedItinerary} onDelete={handleDeleteItem} onEdit={(item) => handleEditItem(item, 'itinerary')} colors={colors} />}

          {activeView === 'packing' && <PackingListView packingList={trip.packingList} onTogglePacked={togglePackedStatus} onDelete={(id) => handleDeleteItem(id, 'packing')} onEdit={(item) => handleEditItem(item, 'packing')} onGetAISuggestions={handleGetAIPackingSuggestions} isAILoading={isAILoading} aiError={aiError} colors={colors}/>}

          {activeView === 'accommodation' && <AccommodationManager accommodations={trip.accommodations} onSave={handleSaveAccommodations} colors={colors} />}

        </main>

        

        {activeView !== 'accommodation' && (

          <div className="mt-6 text-center">

            <button onClick={openAddModal} className={`${colors.primaryBg} text-white font-bold py-3 px-6 rounded-full shadow-lg hover:opacity-90 transition-all duration-200 transform hover:scale-105 flex items-center justify-center mx-auto`}>

              <Plus className="mr-2" size={20} />{activeView === 'itinerary' ? 'æ°å¢è¡ç¨' : 'æ°å¢è¡æ'}

            </button>

          </div>

        )}

      </div>

      

      {modalState.isOpen && <ItemModal mode={modalState.mode} type={modalState.type} initialData={modalState.data} onClose={closeModal} onSave={handleSaveItem} colors={colors} />}

      {isAISuggestionModalOpen && <AISuggestionModal suggestions={aiSuggestions} onClose={() => setIsAISuggestionModalOpen(false)} onAddItems={handleAddSuggestedItems} colors={colors} />}

      {isTranslateModalOpen && <TranslateModal destination={trip.destination} onClose={() => setIsTranslateModalOpen(false)} onTranslate={handleTranslateTrip} isLoading={isTranslating} translatedText={translatedContent} error={translateError} colors={colors}/>}

    </div>

  );

}



// --- Sub-components ---

const Header = ({ title, destination, onTitleChange, onDestinationChange, onTranslate, colors }) => {

    const hiddenRef = React.useRef(null);

    const [inputWidth, setInputWidth] = React.useState(0);



    React.useEffect(() => {

        if (hiddenRef.current) {

            setInputWidth(hiddenRef.current.offsetWidth + 8); 

        }

    }, [destination]);



    return (

        <header className="text-center my-8 relative">

            <input type="text" value={title} onChange={(e) => onTitleChange(e.target.value)} className={`text-4xl font-extrabold ${colors.textPrimary} tracking-tight text-center bg-transparent border-none w-full focus:outline-none focus:ring-0`}/>

            <div className="flex justify-center items-center mt-2 w-full px-12 h-8">

               <MapPin size={16} className={`${colors.textSecondary} mr-2 flex-shrink-0`}/>

               <span ref={hiddenRef} className="text-lg absolute invisible whitespace-pre">{destination}</span>

               <input 

                 type="text" 

                 value={destination} 

                 onChange={(e) => onDestinationChange(e.target.value)} 

                 placeholder="æéç®çå°" 

                 style={{ width: `${inputWidth}px`, minWidth: '15ch' }}

                 className={`text-lg ${colors.textSecondary} text-center bg-transparent border-none focus:outline-none focus:ring-0 transition-all duration-200`}

               />

            </div>

            <button onClick={onTranslate} title="AI ç¿»è­¯è¡ç¨" className={`${colors.secondaryBg} text-white hover:opacity-80 p-2 rounded-full absolute top-0 right-0`}>

                <Languages size={24} />

            </button>

        </header>

    );

};



const Nav = ({ activeView, setActiveView, colors }) => (

  <div className={`${colors.navBg} rounded-full p-1 mt-4`}>

    <button onClick={() => setActiveView('itinerary')} className={`w-1/3 py-2 px-4 rounded-full text-center font-semibold transition-colors duration-300 ${activeView === 'itinerary' ? `${colors.primaryBg} text-white shadow` : `${colors.textSecondary} hover:bg-white/50`}`}>è¡ç¨è¦å</button>

    <button onClick={() => setActiveView('packing')} className={`w-1/3 py-2 px-4 rounded-full text-center font-semibold transition-colors duration-300 ${activeView === 'packing' ? `${colors.primaryBg} text-white shadow` : `${colors.textSecondary} hover:bg-white/50`}`}>è¡ææ¸å®</button>

    <button onClick={() => setActiveView('accommodation')} className={`w-1/3 py-2 px-4 rounded-full text-center font-semibold transition-colors duration-300 ${activeView === 'accommodation' ? `${colors.primaryBg} text-white shadow` : `${colors.textSecondary} hover:bg-white/50`}`}>ä½å®¿è¨­å®</button>

  </div>

);



const AccommodationManager = ({ accommodations, onSave, colors }) => {

    const [localAccommodations, setLocalAccommodations] = React.useState(accommodations);

    const [saved, setSaved] = React.useState(false);

    const handleUpdate = (updatedAcc) => setLocalAccommodations(prev => prev.map(acc => acc.id === updatedAcc.id ? updatedAcc : acc));

    const handleAdd = () => setLocalAccommodations(prev => [...prev, { id: Date.now(), name: '', checkInDate: '', checkOutDate: '', dailyTimes: {} }]);

    const handleDelete = (id) => setLocalAccommodations(prev => prev.filter(acc => acc.id !== id));

    const handleSave = () => { onSave(localAccommodations); setSaved(true); setTimeout(() => setSaved(false), 2000); };



    return (

        <div>

            <div className="flex justify-between items-center mb-4"><h2 className={`text-2xl font-bold flex items-center ${colors.textPrimary}`}><Hotel className={`mr-3 ${colors.primary}`}/>ä½å®¿è¨­å®</h2>{saved && <span className="text-green-600 text-sm transition-opacity duration-300">å·²å²å­ï¼</span>}</div>

            <div className="space-y-6">{localAccommodations.map((acc) => (<AccommodationEditor key={acc.id} accommodation={acc} onUpdate={handleUpdate} onDelete={handleDelete} colors={colors}/>))}</div>

            <div className="mt-6 flex justify-between items-center"><button onClick={handleAdd} className={`bg-gray-200 ${colors.textSecondary} font-bold py-2 px-4 rounded-lg hover:bg-gray-300 transition-all flex items-center`}><Plus size={18} className="mr-2"/>æ°å¢ä½å®¿</button><button onClick={handleSave} className={`${colors.primaryBg} text-white font-bold py-2 px-4 rounded-lg hover:opacity-90 transition-all flex items-center`}><Save size={18} className="mr-2"/>å²å­ææè®æ´</button></div>

        </div>

    );

};



const AccommodationEditor = ({ accommodation, onUpdate, onDelete, colors }) => {

  const handleInfoChange = (e) => onUpdate({ ...accommodation, [e.target.name]: e.target.value });

  const handleDailyTimeChange = (date, type, value) => onUpdate({...accommodation, dailyTimes: {...accommodation.dailyTimes, [date]: { ...(accommodation.dailyTimes[date] || { wakeUp: '09:00', return: '22:00' }), [type]: value }}});

  const dateRange = getDatesInRange(accommodation.checkInDate, accommodation.checkOutDate);



  return (

    <div className={`p-4 border rounded-lg ${colors.navBg}/50`}>

      <div className="flex justify-between items-start"><input type="text" name="name" value={accommodation.name} onChange={handleInfoChange} placeholder="è«è¼¸å¥ä½å®¿å°é»" className={`text-lg font-bold w-full bg-transparent focus:outline-none ${colors.textPrimary}`}/><button onClick={() => onDelete(accommodation.id)} className="text-gray-400 hover:text-red-500 ml-2"><Trash2 size={20}/></button></div>

      <div className="space-y-4 mt-4">

        <div className="grid grid-cols-1 sm:grid-cols-2 gap-4"><div><label className={`block text-sm font-medium ${colors.textSecondary} mb-1`}>å¥ä½æ¥æ</label><input type="date" name="checkInDate" value={accommodation.checkInDate} onChange={handleInfoChange} className="w-full p-2 border border-gray-300 rounded-md"/></div><div><label className={`block text-sm font-medium ${colors.textSecondary} mb-1`}>éæ¿æ¥æ</label><input type="date" name="checkOutDate" value={accommodation.checkOutDate} onChange={handleInfoChange} className="w-full p-2 border border-gray-300 rounded-md"/></div></div>

        <div className="space-y-3 max-h-48 overflow-y-auto pr-2">

            {dateRange.map(date => {

                const dayTimes = accommodation.dailyTimes[date] || { wakeUp: '09:00', return: '22:00' };

                const dateLabel = new Date(date + 'T00:00:00Z').toLocaleDateString('zh-TW', { month: 'numeric', day: 'numeric', timeZone: 'UTC' });

                const isCheckIn = date === accommodation.checkInDate;

                const isCheckOut = date === accommodation.checkOutDate;

                return (

                    <div key={date} className="grid grid-cols-3 gap-2 items-center">

                        <label className={`font-medium ${colors.textSecondary} text-sm`}>{dateLabel}</label>

                        <div className="w-full">{!isCheckIn && <input type="time" value={dayTimes.wakeUp} onChange={(e) => handleDailyTimeChange(date, 'wakeUp', e.target.value)} className="w-full p-2 border border-gray-300 rounded-md" title={`${dateLabel} èµ·åºæé`}/>}</div>

                        <div className="w-full">{!isCheckOut && <input type="time" value={dayTimes.return} onChange={(e) => handleDailyTimeChange(date, 'return', e.target.value)} className="w-full p-2 border border-gray-300 rounded-md" title={`${dateLabel} è¿åæé`}/>}</div>

                    </div>

                )

            })}

        </div>

      </div>

    </div>

  );

};



const ItineraryView = ({ itinerary, onDelete, onEdit, colors }) => {

  const groupedByDate = itinerary.reduce((acc, item) => { if (!acc[item.date]) acc[item.date] = []; acc[item.date].push(item); return acc; }, {});

  return (

    <div>

       <h2 className="text-2xl font-bold mb-4 flex items-center"><Calendar className={`mr-3 ${colors.primary}`}/>è¡ç¨ç´°ç¯</h2>

       {Object.keys(groupedByDate).length === 0 ? <p className={`${colors.textSecondary} text-center py-8`}>ç®åæ²æè¡ç¨</p> : Object.entries(groupedByDate).map(([date, items]) => (<ItineraryDateGroup key={date} date={date} items={items} onDelete={onDelete} onEdit={onEdit} colors={colors} />))}

    </div>

  );

};



const ItineraryDateGroup = ({ date, items, onDelete, onEdit, colors }) => {

    const formatDate = (d) => new Date(d + 'T00:00:00Z').toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long', timeZone: 'UTC' });

    return (

        <div className="mb-6 last:mb-0">

            <div className={`${colors.navBg}/80 p-3 rounded-lg text-left`}><h3 className={`text-lg font-bold ${colors.textPrimary}`}>{formatDate(date)}</h3></div>

            <div className={`border-l-2 border-red-200 ml-4 mt-2 pl-6 space-y-4`}>

            {items.map((item) => (

                <div key={item.id} className={`relative group pt-1 ${item.isAuto ? 'p-2' : ''}`}>

                    <div className={`absolute -left-[34px] top-2 h-4 w-4 bg-white border-2 ${item.isAuto ? 'border-gray-400' : colors.primary.replace('text-','border-')} rounded-full`}></div>

                    <p className={`font-bold text-lg ${item.isAuto ? colors.textSecondary : colors.textPrimary} flex items-center`}><Clock size={16} className={`mr-2 ${colors.textSecondary}`} />{item.time}</p>

                    <p className={`my-1 flex items-center ${item.isAuto ? `italic ${colors.secondary}` : colors.textPrimary}`}><MapPin size={16} className={`mr-2 ${colors.textSecondary}`} />{item.location}</p>

                    {!item.isAuto && item.transport && <p className={`text-sm ${colors.textSecondary} flex items-center`}><Bus size={16} className="mr-2" />äº¤éæ¹å¼ï¼{item.transport}</p>}

                    {!item.isAuto && <div className="absolute top-0 right-0 flex items-center opacity-0 group-hover:opacity-100 transition-opacity"><button onClick={() => onEdit(item)} className="p-1 text-gray-400 hover:text-blue-500"><Pencil size={18} /></button><button onClick={() => onDelete(item.id, 'itinerary')} className="p-1 text-gray-400 hover:text-red-500"><Trash2 size={18} /></button></div>}

                </div>

            ))}

            </div>

        </div>

    );

}



const PackingListView = ({ packingList, onTogglePacked, onDelete, onEdit, onGetAISuggestions, isAILoading, aiError, colors }) => (

  <div>

    <div className="flex justify-between items-center mb-4">

        <h2 className="text-2xl font-bold flex items-center"><Briefcase className={`mr-3 ${colors.primary}`}/>è¡ææ¸å®</h2>

        <button onClick={onGetAISuggestions} disabled={isAILoading} className={`bg-gradient-to-r from-amber-500 to-red-600 text-white font-bold py-2 px-4 rounded-lg hover:opacity-90 transition-all flex items-center disabled:opacity-50 disabled:cursor-not-allowed`}>

            {isAILoading ? <LoaderCircle size={20} className="animate-spin mr-2"/> : <Sparkles size={20} className="mr-2"/>}

            {isAILoading ? 'æèä¸­...' : 'AI æºæ§è¡æå»ºè­°'}

        </button>

    </div>

    {aiError && <p className="text-red-500 text-sm text-center mb-4">{aiError}</p>}

    {packingList.length === 0 ? <p className={`${colors.textSecondary} text-center py-8`}>éæ²å å¥ä»»ä½è¡æåï¼</p> : (

    <div className="space-y-3">

      {packingList.map((item) => (

        <div key={item.id} className={`flex items-center justify-between ${colors.navBg}/80 p-3 rounded-lg group`}>

          <label className="flex items-center cursor-pointer w-full"><input type="checkbox" checked={item.packed} onChange={() => onTogglePacked(item.id)} className={`h-5 w-5 rounded border-gray-300 ${colors.secondary} focus:ring-green-800`}/><span className={`ml-3 text-lg ${item.packed ? `${colors.textSecondary} line-through` : colors.textPrimary}`}>{item.name}</span></label>

           <div className="flex items-center opacity-0 group-hover:opacity-100 transition-opacity"><button onClick={() => onEdit(item)} className="p-1 text-gray-400 hover:text-blue-500"><Pencil size={18} /></button><button onClick={() => onDelete(item.id, 'packing')} className="p-1 text-gray-400 hover:text-red-500"><Trash2 size={18} /></button></div>

        </div>

      ))}

    </div>

    )}

  </div>

);



const AISuggestionModal = ({ suggestions, onClose, onAddItems, colors }) => {

    const [selectedItems, setSelectedItems] = React.useState({});



    const handleSelect = (item, category) => {

        setSelectedItems(prev => {

            const newCategory = new Set(prev[category] || []);

            if (newCategory.has(item)) newCategory.delete(item);

            else newCategory.add(item);

            return { ...prev, [category]: newCategory };

        });

    };



    const handleAddSelected = () => {

        const itemsToAdd = Object.values(selectedItems).flatMap(set => Array.from(set));

        onAddItems(itemsToAdd);

    };



    const renderList = (title, items, category) => (

        <div>

            <h4 className={`font-bold text-lg mb-2 ${colors.textPrimary}`}>{title}</h4>

            <div className="space-y-2 max-h-48 overflow-y-auto pr-2">

                {items.map(item => (

                    <label key={item} className="flex items-center p-2 bg-gray-100 rounded-md cursor-pointer hover:bg-gray-200">

                        <input type="checkbox" onChange={() => handleSelect(item, category)} className={`h-4 w-4 rounded border-gray-300 ${colors.primary} focus:ring-red-500`} />

                        <span className="ml-3 text-gray-800">{item}</span>

                    </label>

                ))}

            </div>

        </div>

    );



    return (

        <div className="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center p-4 z-50">

            <div className={`${colors.cardBg} rounded-xl shadow-2xl w-full max-w-lg backdrop-blur-md border border-white/20`}>

                <div className="flex justify-between items-center p-4 border-b">

                    <h3 className="text-xl font-bold flex items-center"><Sparkles size={20} className={`mr-2 ${colors.accent}`}/>AI æºæ§å»ºè­°</h3>

                    <button onClick={onClose} className="text-gray-400 hover:text-gray-600"><X size={24} /></button>

                </div>

                <div className="p-6 space-y-6">

                    {suggestions.essentials && renderList('å¿éå', suggestions.essentials, 'essentials')}

                    {suggestions.optional && renderList('é¸å¸¶å', suggestions.optional, 'optional')}

                </div>

                <div className="p-4 bg-gray-50/50 flex justify-end">

                    <button onClick={handleAddSelected} className={`${colors.primaryBg} text-white font-bold py-2 px-5 rounded-lg hover:opacity-90 transition-colors`}>å å¥å·²é¸é ç®</button>

                </div>

            </div>

        </div>

    );

};





const ItemModal = ({ mode, type, initialData, onClose, onSave, colors }) => {

  const [formData, setFormData] = React.useState({});

  React.useEffect(() => {

    if (mode === 'edit' && initialData) setFormData(initialData); 

    else if (mode === 'add') setFormData(type === 'itinerary' ? { date: '', time: '', location: '', transport: '' } : { name: '' });

  }, [mode, type, initialData]);



  const handleChange = (e) => setFormData(prev => ({ ...prev, [e.target.name]: e.target.value }));

  const handleSubmit = (e) => { e.preventDefault(); onSave(formData); };

  const isItinerary = type === 'itinerary';

  const title = mode === 'add' ? (isItinerary ? 'æ°å¢è¡ç¨' : 'æ°å¢è¡æ') : (isItinerary ? 'ç·¨è¼¯è¡ç¨' : 'ç·¨è¼¯è¡æ');

  return (

    <div className="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center p-4 z-50">

      <div className={`${colors.cardBg} rounded-xl shadow-2xl w-full max-w-md backdrop-blur-md border border-white/20`}>

        <div className="flex justify-between items-center p-4 border-b"><h3 className="text-xl font-bold">{title}</h3><button onClick={onClose} className="text-gray-400 hover:text-gray-600"><X size={24} /></button></div>

        <form onSubmit={handleSubmit} className="p-6 space-y-4">

          {isItinerary ? (

            <><input type="date" name="date" value={formData.date || ''} onChange={handleChange} required className="w-full p-2 border border-gray-300 rounded-md"/><input type="time" name="time" value={formData.time || ''} onChange={handleChange} required className="w-full p-2 border border-gray-300 rounded-md"/><input type="text" name="location" value={formData.location || ''} onChange={handleChange} required placeholder="å°é» / æ´»å" className="w-full p-2 border border-gray-300 rounded-md"/><input type="text" name="transport" value={formData.transport || ''} onChange={handleChange} placeholder="äº¤éæ¹å¼" className="w-full p-2 border border-gray-300 rounded-md"/></>

          ) : ( <input type="text" name="name" value={formData.name || ''} onChange={handleChange} required placeholder="è¡æåç¨±" className="w-full p-2 border border-gray-300 rounded-md"/> )}

          <div className="pt-4"><button type="submit" className={`${colors.primaryBg} text-white font-bold py-3 px-4 rounded-lg hover:opacity-90 w-full`}>{mode === 'add' ? 'ç¢ºèªæ°å¢' : 'å²å­è®æ´'}</button></div>

        </form>

      </div>

    </div>

  );

};



const TranslateModal = ({ destination, onClose, onTranslate, isLoading, translatedText, error, colors }) => {

    const [selectedLanguage, setSelectedLanguage] = React.useState('');

    const [customLanguage, setCustomLanguage] = React.useState('');

    const [suggestedLanguages, setSuggestedLanguages] = React.useState([]);

    const [isLangLoading, setIsLangLoading] = React.useState(false);



    React.useEffect(() => {

        const getLanguages = async () => {

            if (!destination) return;

            setIsLangLoading(true);

            const prompt = `List the primary official spoken languages for the following destination(s): ${destination}. Return only a simple JSON array of strings. For example, for "Switzerland", return ["German", "French", "Italian"].`;

            try {

                const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };

                const apiKey = "";

                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                const response = await fetch(apiUrl, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });

                if (!response.ok) throw new Error(`API request failed with status ${response.status}`);

                const result = await response.json();

                 if (result.candidates && result.candidates[0]?.content.parts[0]?.text) {

                    let parsedLangs = [];

                    try {

                        const textResponse = result.candidates[0].content.parts[0].text;

                        const jsonString = textResponse.match(/```(?:json)?\n([\s\S]*?)\n```/)?.[1] || textResponse;

                        parsedLangs = JSON.parse(jsonString);

                    } catch (e) {

                         console.error("Could not parse languages from AI response:", e);

                         parsedLangs = [];

                    }

                    setSuggestedLanguages(parsedLangs);

                }

            } catch (e) {

                console.error("Failed to fetch language suggestions:", e);

            } finally {

                setIsLangLoading(false);

            }

        };

        getLanguages();

    }, [destination]);



    const handleTranslate = () => {

        const targetLanguage = selectedLanguage === 'other' ? customLanguage : selectedLanguage;

        onTranslate(targetLanguage);

    };



    return (

        <div className="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center p-4 z-50">

            <div className={`${colors.cardBg} rounded-xl shadow-2xl w-full max-w-2xl backdrop-blur-md border border-white/20`}>

                <div className="flex justify-between items-center p-4 border-b">

                    <h3 className="text-xl font-bold flex items-center"><Languages size={20} className={`mr-2 ${colors.secondary}`}/>AI å¨æç¿»è­¯</h3>

                    <button onClick={onClose} className="text-gray-400 hover:text-gray-600"><X size={24} /></button>

                </div>

                <div className="p-6">

                    <div className="grid grid-cols-1 sm:grid-cols-3 gap-2 mb-4">

                        <div className="sm:col-span-2">

                             <select value={selectedLanguage} onChange={(e) => setSelectedLanguage(e.target.value)} className="w-full p-2 border border-gray-300 rounded-md">

                                <option value="" disabled>è«é¸æèªè¨...</option>

                                <option value="Traditional Chinese">ç¹é«ä¸­æ</option>

                                <option value="English">English</option>

                                {isLangLoading ? <option disabled>è¼å¥å»ºè­°èªè¨...</option> : suggestedLanguages.map(lang => <option key={lang} value={lang}>{lang}</option>)}

                                <option value="other">å¶ä»...</option>

                            </select>

                        </div>

                        <button onClick={handleTranslate} disabled={isLoading || !selectedLanguage} className={`${colors.secondaryBg} text-white font-bold py-2 px-4 rounded-lg hover:opacity-90 flex items-center justify-center disabled:opacity-50`}>

                            {isLoading ? <LoaderCircle size={20} className="animate-spin mr-2"/> : null}

                            ç¿»è­¯

                        </button>

                    </div>

                     {selectedLanguage === 'other' && (

                        <input 

                            type="text" 

                            value={customLanguage}

                            onChange={(e) => setCustomLanguage(e.target.value)}

                            placeholder="è«è¼¸å¥ç®æ¨èªè¨"

                            className="w-full p-2 border border-gray-300 rounded-md mb-4"

                        />

                    )}

                    {error && <p className="text-red-500 text-sm">{error}</p>}

                    <div className="mt-4 p-4 bg-gray-100 rounded-md max-h-80 overflow-y-auto">

                        {isLoading ? (

                            <div className="text-center text-gray-500">ç¿»è­¯ä¸­ï¼è«ç¨å...</div>

                        ) : (

                            <pre className="whitespace-pre-wrap font-sans text-sm text-gray-800">{translatedText || 'ç¿»è­¯çµæå°æé¡¯ç¤ºå¨æ­¤èã'}</pre>

                        )}

                    </div>

                </div>

            </div>

        </div>

    );

};

