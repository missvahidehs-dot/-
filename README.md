<!doctype html>
<html lang="fa" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>آزمون دانستنی‌های فسیل‌ها</title>
<style>
:root{--bg:#f4f8f2;--card:#fff;--ink:#18352d;--green:#287a58;--mint:#e4f4e9;--gold:#f3c969;--muted:#60746c;--line:#dce8df}
*{box-sizing:border-box}
body{margin:0;font-family:Tahoma,Arial,sans-serif;background:linear-gradient(135deg,#eff8f0,#fff7e6);color:var(--ink);min-height:100vh}
header{padding:26px 16px 12px;text-align:center}
.logo{font-size:48px}
h1{font-size:clamp(25px,5vw,38px);margin:8px 0;color:#205d45}
.subtitle{color:var(--muted);line-height:1.9;margin:8px auto;max-width:680px}
main{max-width:850px;margin:0 auto;padding:16px}
.panel{background:var(--card);border:1px solid var(--line);border-radius:22px;padding:clamp(18px,4vw,32px);box-shadow:0 12px 35px #234d3310}
.pills{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin:20px 0}
.pill{background:var(--mint);border-radius:999px;padding:8px 13px;font-size:14px}
button{font:inherit;cursor:pointer;border:0;border-radius:13px;padding:13px 20px;transition:transform .12s,filter .12s}
button:hover{filter:brightness(.97);transform:translateY(-1px)}
.primary{background:var(--green);color:white;font-weight:bold}
.secondary{background:#edf3ef;color:var(--ink);border:1px solid var(--line)}
.center{text-align:center}
.hidden{display:none!important}
.note{font-size:13px;color:var(--muted);line-height:1.9}
.progress-wrap{height:9px;background:#e7eee9;border-radius:99px;overflow:hidden;margin:15px 0 22px}
.progress{height:100%;width:0;background:linear-gradient(90deg,#287a58,#8bcf9f);transition:width .25s}
.qtop{display:flex;justify-content:space-between;gap:12px;align-items:center;flex-wrap:wrap;color:var(--muted);font-size:14px}
.question{font-size:clamp(19px,3.5vw,24px);line-height:1.9;margin:18px 0}
.options{display:grid;gap:11px}
.option{width:100%;text-align:right;background:#fbfdfb;border:1.5px solid var(--line);color:var(--ink);line-height:1.8}
.option .letter{display:inline-flex;align-items:center;justify-content:center;width:30px;height:30px;border-radius:9px;background:var(--mint);margin-left:9px;font-weight:bold}
.option.selected{border-color:var(--green);background:#eaf6ed}
.option.correct{border-color:#27834e;background:#e5f6e9}
.option.wrong{border-color:#c75b50;background:#fff0ed}
.feedback{margin-top:14px;padding:12px 14px;border-radius:12px;line-height:1.8}
.actions{display:flex;justify-content:space-between;gap:10px;flex-wrap:wrap;margin-top:22px}
.actions button{flex:1;min-width:130px}
.result-score{font-size:54px;font-weight:bold;color:var(--green);margin:12px 0}
footer{text-align:center;padding:22px 14px 35px;color:var(--muted);font-size:14px;line-height:1.9}
@media(max-width:520px){.actions{flex-direction:column}.actions button{width:100%}}
</style>
</head>
<body>
<header>
  <div class="logo" aria-hidden="true">🦕🪨</div>
  <h1>آزمون دانستنی‌های فسیل‌ها</h1>
  <p class="subtitle">به دنیای شگفت‌انگیز گذشته سفر کن و دانش خودت را دربارهٔ فسیل‌ها بسنج!</p>
</header>
<main>
<section id="intro" class="panel center">
  <h2>آماده‌ای پژوهشگر کوچک؟ 🔎</h2>
  <p class="subtitle">به ۳۰ پرسش چهارگزینه‌ای پاسخ بده. در پایان، امتیاز و پاسخ‌های درست را می‌بینی.</p>
  <div class="pills">
    <span class="pill">📝 ۳۰ سؤال</span><span class="pill">🎯 چهارگزینه‌ای</span><span class="pill">🌋 سفر به گذشته</span>
  </div>
  <button id="startBtn" class="primary">شروع آزمون</button>
  <p class="note">پژوهشگر: سید طاها سجادیان</p>
</section>

<section id="quiz" class="panel hidden" aria-live="polite">
  <div class="qtop"><span id="counter">سؤال ۱ از ۳۰</span><span id="answered">پاسخ داده‌شده: ۰</span></div>
  <div class="progress-wrap"><div id="progress" class="progress"></div></div>
  <h2 id="question" class="question"></h2>
  <div id="options" class="options"></div>
  <div id="feedback" class="feedback hidden"></div>
  <div class="actions">
    <button id="nextBtn" class="primary" disabled>سؤال بعدی</button>
    <button id="exitBtn" class="secondary">بازگشت به آغاز</button>
  </div>
</section>

<section id="result" class="panel center hidden">
  <div class="logo">🏆</div>
  <h2>آفرین! آزمون تمام شد</h2>
  <p>امتیاز تو از ۳۰ سؤال:</p>
  <div id="score" class="result-score">۰ از ۳۰</div>
  <p id="message" class="subtitle"></p>
  <button id="reviewBtn" class="primary">دیدن پاسخ‌ها</button>
  <button id="retryBtn" class="secondary">شرکت دوباره در آزمون</button>
  <div id="review" class="hidden" style="text-align:right;margin-top:22px"></div>
</section>
</main>
<footer>طراحی آموزشی با موضوع فسیل‌ها<br><strong>پژوهشگر: سید طاها سجادیان</strong></footer>
<script>
const questions = [
{q:"فسیل چیست؟",o:["باقی‌مانده یا اثر جاندار قدیمی","سنگی که تازه ساخته شده","هر نوع بلور معدنی","یک گیاه زنده"],a:0,e:"فسیل، باقی‌مانده یا نشانه‌ای از جانداران گذشته است که در سنگ‌ها یا رسوبات حفظ شده است."},
{q:"علم مطالعهٔ فسیل‌ها چه نام دارد؟",o:["هواشناسی","دیرینه‌شناسی","ستاره‌شناسی","اقیانوس‌شناسی"],a:1,e:"دیرینه‌شناسان با بررسی فسیل‌ها دربارهٔ زندگی در گذشتهٔ زمین اطلاعات به دست می‌آورند."},
{q:"کدام مورد می‌تواند فسیل شود؟",o:["فقط دایناسورها","فقط درختان","استخوان، صدف یا ردپا","فقط سنگ‌های آتشفشانی"],a:2,e:"استخوان، دندان، صدف، برگ و حتی ردپا می‌توانند به شکل فسیل حفظ شوند."},
{q:"فسیل‌ها بیشتر در چه نوع سنگی پیدا می‌شوند؟",o:["سنگ رسوبی","سنگ مذاب","همهٔ سنگ‌ها به یک اندازه","فلز خالص"],a:0,e:"فسیل‌ها بیشتر در سنگ‌های رسوبی یافت می‌شوند؛ گرما و فشار زیاد می‌تواند آثار را از بین ببرد."},
{q:"چرا بسیاری از جانداران پس از مرگ فسیل نمی‌شوند؟",o:["چون همه به سنگ تبدیل می‌شوند","چون بقایا ممکن است تجزیه یا نابود شوند","چون فسیل فقط در شب تشکیل می‌شود","چون خاک وجود ندارد"],a:1,e:"فسیل‌شدن شرایط ویژه‌ای می‌خواهد؛ بسیاری از بقایا پیش از حفظ‌شدن تجزیه یا تخریب می‌شوند."},
{q:"کدام شرایط به حفظ بقایای جاندار کمک می‌کند؟",o:["دفن‌شدن سریع زیر رسوبات","ماندن طولانی روی سطح زمین","شسته‌شدن پیوسته با آب","قرارگرفتن در آتش"],a:0,e:"دفن سریع می‌تواند بقایا را از لاشخورها، هوا و عوامل تخریب‌کننده دور کند."},
{q:"ردپای فسیلی چه چیزی را نشان می‌دهد؟",o:["رنگ واقعی جاندار","رفتار یا حرکت جاندار","صدای جاندار","وزن دقیق جاندار"],a:1,e:"ردپاها و مسیرها از فسیل‌های اثری‌اند و می‌توانند دربارهٔ حرکت یا رفتار جانداران سرنخ بدهند."},
{q:"دایناسورها در کدام دوران زمین‌شناسی زندگی می‌کردند؟",o:["مزوزوئیک","نوزیستی","فقط دوران کنونی","پیش از تشکیل زمین"],a:0,e:"دایناسورها در دوران مزوزوئیک زندگی می‌کردند؛ این دوران به سه دورهٔ تریاس، ژوراسیک و کرتاسه تقسیم می‌شود."},
{q:"آمبر یا کهربا چگونه می‌تواند فسیل بسازد؟",o:["با گیر افتادن جاندار در رزین درخت","با یخ‌زدن آب دریا","با تبدیل ماسه به شیشه در خانه","با سوختن برگ"],a:0,e:"رزین چسبناک درخت می‌تواند حشرات یا بخش‌های کوچک جانداران را در خود گرفتار و حفظ کند."},
{q:"کدام مورد یک فسیل اثری است؟",o:["ردپای جانور","دندان حفظ‌شده","صدف سنگ‌شده","استخوان سنگ‌شده"],a:0,e:"فسیل اثری، نشانهٔ فعالیت جاندار مانند ردپا، لانه یا مسیر حرکت است."},
{q:"چه کسی فسیل‌ها را بررسی می‌کند؟",o:["دیرینه‌شناس","آشپز","خلبان","نقاش ساختمان"],a:0,e:"دیرینه‌شناس با مطالعهٔ فسیل‌ها زندگی و محیط‌های گذشته را بررسی می‌کند."},
{q:"فسیل‌ها چه کمکی به دانشمندان می‌کنند؟",o:["شناخت جانداران و محیط‌های گذشته","پیش‌بینی دقیق همهٔ رویدادهای فردا","ساختن آب از سنگ","تعیین رنگ همهٔ جانداران"],a:0,e:"فسیل‌ها شواهدی دربارهٔ شکل زندگی، تغییرات جانداران و محیط‌های قدیمی فراهم می‌کنند."},
{q:"کدام بخش بدن معمولاً راحت‌تر فسیل می‌شود؟",o:["بخش سخت مانند دندان یا استخوان","بافت نرم همیشه و در همه‌جا","صدای جانور","گرمای بدن"],a:0,e:"بخش‌های سخت معمولاً دوام بیشتری دارند؛ بااین‌حال، در شرایط ویژه بافت‌های نرم هم ممکن است حفظ شوند."},
{q:"آیا گیاهان هم می‌توانند فسیل شوند؟",o:["بله، مانند برگ و چوب","نه، فقط جانوران فسیل می‌شوند","فقط گیاهان امروزی","فقط گیاهان دریایی زنده"],a:0,e:"برگ‌ها، دانه‌ها، چوب و گردهٔ گیاهان می‌توانند در شرایط مناسب حفظ شوند."},
{q:"فسیل صدف‌های دریایی در کوهستان ممکن است چه چیزی را نشان دهد؟",o:["آن منطقه زمانی زیر آب بوده است","کوهستان همیشه آتشفشان فعال است","صدف‌ها روی قله زندگی می‌کنند","زمین هرگز تغییر نکرده است"],a:0,e:"وجود فسیل‌های دریایی در ارتفاعات می‌تواند نشان دهد که آن منطقه در گذشته زیر آب بوده یا بعداً بالا آمده است."},
{q:"فسیل‌های راهنما چه کاربردی دارند؟",o:["کمک به مقایسه و تعیین سن نسبی لایه‌های سنگی","اندازه‌گیری دمای امروز","پیداکردن همهٔ فلزات","پیش‌بینی آب‌وهوا"],a:0,e:"فسیل‌های راهنما به زمین‌شناسان کمک می‌کنند لایه‌های سنگی هم‌سن را در مناطق مختلف مقایسه کنند."},
{q:"سن نسبی یک فسیل یعنی چه؟",o:["مقایسهٔ قدیمی‌تر یا جوان‌تر بودن آن","سن دقیق به تعداد روز","وزن آن بر حسب کیلوگرم","اندازهٔ بدن جاندار"],a:0,e:"سن نسبی مشخص می‌کند چیزی نسبت به چیز دیگر قدیمی‌تر یا جوان‌تر است، نه سن دقیق آن."},
{q:"در لایه‌های دست‌نخوردهٔ رسوبی، معمولاً کدام لایه قدیمی‌تر است؟",o:["لایهٔ پایینی","لایهٔ بالایی","همه همیشه هم‌سن‌اند","لایه‌ای که رنگ روشن‌تری دارد"],a:0,e:"در لایه‌های رسوبی دست‌نخورده، لایه‌های پایین‌تر معمولاً زودتر تشکیل شده‌اند."},
{q:"کدام جاندار گروهی از جانوران دریایی با صدف مارپیچی بود که فسیل‌هایش پیدا می‌شود؟",o:["آمونیت","گنجشک","گربه","قورباغه"],a:0,e:"آمونیت‌ها جانوران دریایی منقرض‌شده‌ای بودند که صدف مارپیچی داشتند."},
{q:"آیا همهٔ فسیل‌ها استخوان هستند؟",o:["خیر؛ فسیل می‌تواند اثر یا بخش‌های دیگری باشد","بله، فقط استخوان فسیل می‌شود","فقط دندان فسیل است","فقط ردپای دایناسور فسیل است"],a:0,e:"فسیل‌ها می‌توانند صدف، برگ، دندان، چوب، ردپا و آثار دیگر جانداران باشند."},
{q:"کدام گزینه دربارهٔ فسیل‌شدن درست است؟",o:["معمولاً فرایندی طولانی و وابسته به شرایط است","همیشه در چند دقیقه رخ می‌دهد","فقط در یخچال رخ می‌دهد","همهٔ جانوران حتماً فسیل می‌شوند"],a:0,e:"فسیل‌شدن معمولاً فرایندی طولانی است و به عواملی مانند رسوب، مواد معدنی و محیط بستگی دارد."},
{q:"فسیل ماموت یخ‌زده ممکن است چه چیزی را حفظ کند؟",o:["بخش‌هایی از بافت نرم و مو","فقط گدازهٔ آتشفشانی","نور خورشید","صدای ماموت"],a:0,e:"سرمای شدید می‌تواند در شرایط مناسب بخش‌هایی از بدن، مانند مو و بافت نرم، را حفظ کند."},
{q:"چرا دانشمندان فسیل‌ها را با دقت از سنگ جدا می‌کنند؟",o:["تا به فسیل آسیب نرسد و اطلاعاتش حفظ شود","تا فسیل فوراً زنده شود","تا رنگ سنگ عوض شود","تا سن زمین کم شود"],a:0,e:"استخراج دقیق کمک می‌کند شکل و جزئیات فسیل آسیب نبیند و اطلاعات علمی آن حفظ شود."},
{q:"کدام مورد معمولاً فسیل واقعی به شمار نمی‌رود؟",o:["اسباب‌بازی دایناسور که در کارخانه ساخته شده","ردپای جانور باستانی در سنگ","برگ حفظ‌شده در سنگ","صدف سنگ‌شده"],a:0,e:"اسباب‌بازی ساختهٔ انسان فسیل نیست؛ فسیل از بقایا یا فعالیت جانداران گذشته به وجود می‌آید."},
{q:"سنگواره واژه‌ای دیگر برای چیست؟",o:["فسیل","ابر","ماسهٔ روان","مواد غذایی"],a:0,e:"سنگواره واژه‌ای فارسی برای فسیل است."},
{q:"چه چیزی می‌تواند بقایای جاندار را به‌تدریج جایگزین کند و آن را سنگی کند؟",o:["مواد معدنی","نور چراغ","هوای گرم به‌تنهایی","رنگ نقاشی"],a:0,e:"در برخی فرایندهای فسیل‌شدن، مواد معدنی وارد بقایا می‌شوند یا جای بخش‌هایی از آن را می‌گیرند."},
{q:"چرا فسیل‌ها برای شناخت انقراض مهم‌اند؟",o:["نشان می‌دهند چه جاندارانی در گذشته وجود داشته‌اند و دیگر دیده نمی‌شوند","همهٔ علت‌های انقراض را دقیقاً ثابت می‌کنند","نشان می‌دهند هیچ جانداری تغییر نکرده","فقط تعداد جانوران امروزی را می‌شمارند"],a:0,e:"فسیل‌ها حضور جانداران گذشته و تغییرات آن‌ها را نشان می‌دهند؛ دانشمندان با شواهد مختلف علت‌های انقراض را بررسی می‌کنند."},
{q:"کدام جمله دربارهٔ دایناسورها درست است؟",o:["همهٔ دایناسورها پرواز می‌کردند","پرندگان امروزی از نسل دایناسورهای تروپود هستند","همهٔ دایناسورها در آب زندگی می‌کردند","دایناسورها و انسان‌ها همیشه هم‌زمان بوده‌اند"],a:1,e:"شواهد علمی نشان می‌دهد پرندگان امروزی از شاخه‌ای از دایناسورهای تروپود به وجود آمده‌اند."},
{q:"اگر فسیل یک جاندار در چند لایهٔ سنگی پیدا شود، دانشمند چه کاری می‌تواند انجام دهد؟",o:["لایه‌ها را با کمک شواهد دیگر مقایسه کند","بدون هیچ بررسی سن دقیق را حدس بزند","نتیجه بگیرد همهٔ سنگ‌ها یکسان‌اند","از روی رنگ فسیل دمای امروز را بفهمد"],a:0,e:"فسیل‌ها همراه با ترتیب لایه‌ها و شواهد دیگر برای مقایسه و بررسی سن نسبی به کار می‌روند."},
{q:"بهترین کار هنگام پیدا کردن فسیل احتمالی در طبیعت چیست؟",o:["محل را ثبت کنیم و از یک بزرگ‌تر یا متخصص کمک بگیریم","آن را با ابزار تیز به‌سرعت جدا کنیم","آن را بشکنیم تا داخلش را ببینیم","محل پیدا شدن را فراموش کنیم"],a:0,e:"ثبت محل و کمک گرفتن از بزرگ‌تر یا متخصص باعث می‌شود نمونه و اطلاعات مهم آن آسیب نبیند."}
];
const faDigits = n => String(n).replace(/\d/g,d=>"۰۱۲۳۴۵۶۷۸۹"[d]);
let index=0, answers=Array(questions.length).fill(null), checked=Array(questions.length).fill(false);
const $=id=>document.getElementById(id);
function show(id){["intro","quiz","result"].forEach(x=>$(x).classList.toggle("hidden",x!==id));}
function start(){index=0;answers=Array(questions.length).fill(null);checked=Array(questions.length).fill(false);show("quiz");renderQuestion();}
function renderQuestion(){
 const item=questions[index];$("counter").textContent=`سؤال ${faDigits(index+1)} از ${faDigits(questions.length)}`;
 $("answered").textContent=`پاسخ داده‌شده: ${faDigits(answers.filter(x=>x!==null).length)}`;
 $("progress").style.width=`${(index/questions.length)*100}%`;
 $("question").textContent=item.q;$("options").innerHTML="";$("feedback").classList.add("hidden");$("feedback").textContent="";
 item.o.forEach((opt,i)=>{const b=document.createElement("button");b.className="option";b.innerHTML=`<span class="letter">${"الف ب ج د".split(" ")[i]}</span>`;const t=document.createTextNode(opt);b.appendChild(t);if(answers[index]===i)b.classList.add("selected");if(checked[index]){b.disabled=true;if(i===item.a)b.classList.add("correct");else if(answers[index]===i)b.classList.add("wrong");}b.addEventListener("click",()=>choose(i));$("options").appendChild(b);});
 if(checked[index]){$("feedback").textContent=item.e;$("feedback").classList.remove("hidden");}
 $("nextBtn").disabled=answers[index]===null;
 $("nextBtn").textContent=index===questions.length-1?(checked[index]?"دیدن نتیجه":"ثبت پاسخ و پایان"):"سؤال بعدی";
 $("progress").style.width=`${((index+(checked[index]?1:0))/questions.length)*100}%`;
}
function choose(i){if(checked[index])return;answers[index]=i;checked[index]=true;renderQuestion();}
function next(){if(answers[index]===null)return;if(index<questions.length-1){index++;renderQuestion();}else showResult();}
function showResult(){show("result");const score=answers.reduce((s,a,i)=>s+(a===questions[i].a?1:0),0);$("score").textContent=`${faDigits(score)} از ${faDigits(questions.length)}`;$("message").textContent=score>=25?"فوق‌العاده بود! تو یک فسیل‌شناس کنجکاوی.":score>=18?"آفرین! اطلاعات خوبی دربارهٔ فسیل‌ها داری.":"خوب تلاش کردی! پاسخ‌ها را مرور کن و دوباره امتحان کن.";$("progress").style.width="100%";$("review").classList.add("hidden");$("review").innerHTML="";}
function review(){const box=$("review");box.innerHTML="<h3>مرور پاسخ‌ها</h3>";questions.forEach((q,i)=>{const d=document.createElement("div");d.style.cssText="padding:12px 0;border-bottom:1px solid #dce8df;line-height:1.9";const title=document.createElement("strong");title.textContent=`${faDigits(i+1)}. ${q.q}`;const ans=document.createElement("p");ans.textContent=`پاسخ درست: ${q.o[q.a]}${answers[i]===q.a?" — پاسخ تو درست بود.":` — پاسخ تو: ${answers[i]===null?"بدون پاسخ":q.o[answers[i]]}.`}`;const exp=document.createElement("p");exp.className="note";exp.textContent=q.e;d.append(title,ans,exp);box.appendChild(d);});box.classList.remove("hidden");}
$("startBtn").addEventListener("click",start);$("nextBtn").addEventListener("click",next);$("exitBtn").addEventListener("click",()=>show("intro"));$("retryBtn").addEventListener("click",start);$("reviewBtn").addEventListener("click",review);
</script>
</body>
</html> 
