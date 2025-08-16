# Daily-Story
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Daily Stories — रोज़ नई कहानी</title>
  <meta name="description" content="रोज़ एक नई, छोटी और प्रेरक कहानी पढ़िए। मोबाइल-फ्रेंडली, तेज़ और साफ़ डिज़ाइन।" />
  <style>
    :root { --bg:#0f172a; --card:#0b1224; --ink:#e5e7eb; --muted:#9ca3af; --accent:#60a5fa; }
    *{box-sizing:border-box}
    body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;
         background:linear-gradient(120deg,#0b1020,#0f172a 40%,#0a1022);
         color:var(--ink);}
    .wrap{max-width:860px;margin:auto;padding:24px}
    header{display:flex;gap:12px;align-items:center;justify-content:space-between;margin-bottom:16px}
    .brand{font-weight:800;letter-spacing:.4px}
    .card{background:var(--card);border:1px solid #1f2a44; border-radius:18px; padding:22px; box-shadow:0 10px 30px rgba(0,0,0,.35)}
    h1{font-size:28px;margin:0 0 10px}
    h2{font-size:22px;margin:0 0 6px}
    .meta{color:var(--muted);font-size:14px;margin-bottom:12px}
    .content{white-space:pre-wrap;line-height:1.75;font-size:18px}
    .controls{display:flex;gap:10px;flex-wrap:wrap;margin-top:18px}
    button{background:#0f1b36;border:1px solid #243657;color:var(--ink);padding:10px 14px;border-radius:12px;cursor:pointer}
    button:hover{border-color:var(--accent)}
    .archive{margin-top:18px}
    details{background:#0b1328;border:1px solid #1f2a44;border-radius:14px;padding:10px}
    summary{cursor:pointer;color:var(--accent);font-weight:600;margin:6px 0}
    ul{list-style:none;padding:0;margin:8px 0 0}
    li{padding:10px;border-top:1px solid #1b2542}
    li:first-child{border-top:none}
    li a{color:var(--ink);text-decoration:none}
    li a:hover{color:var(--accent)}
    footer{opacity:.7;font-size:13px;margin-top:16px;text-align:center}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="brand">📖 Daily Stories</div>
      <div class="meta" id="todayLabel"></div>
    </header>

    <main class="card">
      <h1 id="title">Loading…</h1>
      <div class="meta" id="byline"></div>
      <div class="content" id="story"></div>

      <div class="controls">
        <button id="prevBtn">← Previous</button>
        <button id="todayBtn">Today’s Pick</button>
        <button id="nextBtn">Next →</button>
        <button id="randomBtn">Shuffle 🔀</button>
        <button id="copyBtn">Copy Story 📋</button>
      </div>

      <div class="archive">
        <details>
          <summary>📚 Archive (titles)</summary>
          <ul id="archiveList"></ul>
        </details>
      </div>
      <footer id="counter"></footer>
    </main>
  </div>

  <script>
  // ------------ 10 FULL HINDI SHORT STORIES ------------
  const STORIES = [
    {
      title: "दीये की लौ",
      author: "Team Daily Stories",
      text: `नन्ही रेशमा के घर में बिजली अक्सर चली जाती थी। वह परीक्षा की तैयारी दीये की लौ में करती।
एक रात हवा बहुत तेज़ चली और दीया बुझ गया। रेशमा ने किताब बंद करने की बजाय खिड़की खोली,
चाँदनी को अंदर आने दिया और पढ़ाई जारी रखी। अगले दिन उसने टॉपर बनकर सबको बताया—
रोशनी बाहर से नहीं, इरादे के भीतर से आती है।`
    },
    {
      title: "पुराना रेडियो",
      author: "Team Daily Stories",
      text: `दादाजी का टूटा-फूटा रेडियो घर के कोने में पड़ा रहता था। आरव ने उसे खोलकर देखा—तार उलझे हुए,
स्पीकर फटा हुआ। कई दिन तक यूट्यूब, किताबें और कोशिश। अंत में रेडियो बोल उठा!
दादाजी मुस्कुराए, “मशीन नहीं, तुमने मेरी यादें ठीक कर दीं।” उस दिन आरव ने सीखा कि हर चीज़ की मरम्मत
स्क्रू-ड्राइवर से नहीं, धैर्य से होती है।`
    },
    {
      title: "आधी टिकट",
      author: "Team Daily Stories",
      text: `मीरा रोज़ बस से स्कूल जाती थी और आधी टिकट लेती थी। एक दिन कंडक्टर ने कहा,
“अब तुम बड़ी हो गई हो।” मीरा ने पर्स देखा—पूरे पैसों की कमी थी। बगल में बैठी सब्ज़ीवाली ने
चुपचाप पाँच रुपये बढ़ा दिए। मीरा ने धन्यवाद कहा तो औरत बोली, “कल तुम किसी और की मदद कर देना।”
मीरा ने उस दिन से ‘आधी टिकट’ नहीं, ‘पूरी मदद’ शुरू कर दी।`
    },
    {
      title: "खाली गमला",
      author: "Team Daily Stories",
      text: `कोच ने सभी बच्चों को एक-एक गमला और बीज दिया। “जिसका पौधा सबसे अच्छा होगा, वही कप्तान बनेगा।”
महीने भर बाद सारे बच्चे फूल-पत्तों के साथ आए। रवि का गमला खाली था।
उसने सच बता दिया—“मैंने खूब पानी और धूप दी, फिर भी कुछ नहीं उगा।” कोच मुस्कुराए,
“बीज उबले हुए थे। कप्तान वही जो ईमानदार है।” रवि चुना गया।`
    },
    {
      title: "बारिश की चिट्ठी",
      author: "Team Daily Stories",
      text: `कस्बे में महीनों से बारिश नहीं हुई थी। नन्हा साहिल रोज़ आसमान को देखता और बादलों को चिट्ठी लिखता—
“प्रिय बादल, मेरी माँ की खोई मुस्कान लौटा दो।” एक शाम डाकिया आया—हाथ में पानी की टंकी की चाबी।
गाँव ने मिलकर पुराना कुआँ साफ़ किया, पाइप जोड़े, और उसी रात पहली फुहार पड़ी।
साहिल ने समझा—कभी-कभी चिट्ठियाँ आसमान नहीं, पड़ोस तक जाती हैं।`
    },
    {
      title: "लाइब्रेरी का आख़िरी पन्ना",
      author: "Team Daily Stories",
      text: `ज़ैनब की स्कूल लाइब्रेरी बंद होने वाली थी। उसने आख़िरी किताब उठाई—अंदर एक पन्ना फँसा था:
“अगर यह पढ़ रहे हो तो एक किताब दान करो।” ज़ैनब ने घर-घर बात फैलाई।
सप्ताह भर में सैकड़ों किताबें आ गईं और लाइब्रेरी बच गई। उसने सीखा—पन्ने छोटे होते हैं,
पर कहानियाँ बड़ी।`
    },
    {
      title: "नक्शे की गलती",
      author: "Team Daily Stories",
      text: `ट्रेकिंग के दिन आर्या ने नक्शे में रास्ता गलत पढ़ लिया। टीम भटक गई और शाम घिर आई।
उसने स्वीकार किया, “गलती मेरी थी।” सबने मिलकर शांत दिमाग से दिशा देखी, नदी का बहाव समझा,
और सुरक्षित लौट आए। कोच ने कहा, “जो गलती मान ले, वही अगली बार सही राह दिखाता है।”`
    },
    {
      title: "नीम का झूला",
      author: "Team Daily Stories",
      text: `गली के बच्चों ने खाली जगह में झूला लगाने की सोची। किसी के पास रस्सी नहीं, किसी के पास लकड़ी नहीं।
दादी ने पुराने साड़ी के किनारे दिए, मोची काका ने गांठें सिखाईं, और कारपेंटर चाचा ने सीट बना दी।
एक शाम में ‘नीम का झूला’ तैयार। सबको एहसास हुआ—मोहल्ले का असली खेल सहयोग है।`
    },
    {
      title: "काँच का टुकड़ा",
      author: "Team Daily Stories",
      text: `रीना को सड़क पर चमकता काँच मिला। वह उसे फेंकने लगी, फिर सोचा—किसी का पैर कट सकता है।
उसने काँच डस्टबिन में डाला और पास की 'लॉस्ट & फाउंड' पेटी में एक नोट छोड़ा:
“छोटी सावधानियाँ बड़े हादसे रोकती हैं।” अगले दिन स्कूल में ‘सेफ्टी डे’ मनाया गया,
रीना मुख्य अतिथि थी—क्योंकि नायक कभी-कभी बस झुककर उठाते हैं।`
    },
    {
      title: "दूसरी घंटी",
      author: "Team Daily Stories",
      text: `समय से पहले पहुँचना अनिकेत की आदत थी। इंटरव्यू में पहली घंटी बजी—उम्मीदवार हड़बड़ा गए।
अनिकेत ने फॉर्म्स बाँटे, पानी रखा और मुस्कुराया। पैनल अंदर से देख रहा था।
दूसरी घंटी पर उसका नाम पुकारा गया। इंटरव्यू छोटा था—सवाल बस एक:
“जब सिस्टम नहीं चलता, तुम क्या करते हो?” उसने कहा, “लोगों को चलने में मदद।” नौकरी मिल गई।`
    }
  ];

  // ---------- Helpers ----------
  const $ = (id) => document.getElementById(id);
  const bylineEl = $("byline"), titleEl = $("title"), storyEl = $("story");
  const todayLabel = $("todayLabel"), archiveList = $("archiveList"), counter = $("counter");

  function formatDate(d){
    return d.toLocaleDateString("hi-IN", { weekday:"long", year:"numeric", month:"long", day:"numeric" });
  }

  // Daily pick based on date, but allow user navigation (persist)
  const todayIndex = new Date().getDate() % STORIES.length;
  let index = Number(localStorage.getItem("ds_index"));
  if (!Number.isInteger(index)) index = todayIndex;

  function render(i){
    const s = STORIES[i];
    titleEl.textContent = s.title;
    bylineEl.textContent = `लेखक: ${s.author} • #${i+1} / ${STORIES.length}`;
    storyEl.textContent = s.text;
    counter.textContent = "Tip: ऊपर Archive पर क्लिक करके किसी भी कहानी पर सीधे जा सकते हैं।";
    localStorage.setItem("ds_index", i);
    // Update page title (tab)
    document.title = `${s.title} — Daily Stories`;
  }

  function buildArchive(){
    archiveList.innerHTML = "";
    STORIES.forEach((s, i) => {
      const li = document.createElement("li");
      const a = document.createElement("a");
      a.href = "javascript:void(0)";
      a.textContent = s.title;
      a.onclick = () => { index = i; render(index); };
      li.appendChild(a);
      archiveList.appendChild(li);
    });
  }

  // Buttons
  $("prevBtn").onclick = () => { index = (index - 1 + STORIES.length) % STORIES.length; render(index); };
  $("nextBtn").onclick = () => { index = (index + 1) % STORIES.length; render(index); };
  $("todayBtn").onclick = () => { index = todayIndex; render(index); };
  $("randomBtn").onclick = () => { index = Math.floor(Math.random()*STORIES.length); render(index); };
  $("copyBtn").onclick = async () => {
    try{
      await navigator.clipboard.writeText(`${STORIES[index].title}\n\n${STORIES[index].text}`);
      alert("कहानी कॉपी हो गई ✅");
    }catch{ alert("कॉपी करने में समस्या आई—ब्राउज़र अनुमति दें।"); }
  };

  // Init
  todayLabel.textContent = "आज: " + formatDate(new Date());
  buildArchive();
  render(index);
  </script>
</body>
</html>
