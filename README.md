<!--
  This file mirrors https://fromcodetocloud.uz — same claims, same numbers.

  RULE, inherited from that page: every number here is one that can be pointed
  at. Test counts come from counting the repositories, not from memory; the
  Davomat figures come from its own admin dashboard. Nothing is estimated or
  rounded up, because one invented figure would make the real ones look
  invented too.

  The previous version of this file was 24KB of animated banners, badge rows
  and a profile-view counter — plus links to a dev.to and a Stack Overflow
  profile that both returned 404. That is the opposite of the point.
-->

# Firdavs Kholov

**O‘lchanadigan tizimlar quraman — va o‘lchov qarshi chiqsa, to‘xtataman.**

Tadqiqot qiladigan backend muhandisman. Python, PostgreSQL, Docker — vosita;
asosiy ishim gipotezani tekshirish. Quyidagi hamma narsa — ishlab turgan tizim
yoki o‘lchov natijasi.

[**fromcodetocloud.uz**](https://fromcodetocloud.uz) — to‘liq portfolio: o‘lchangan
qarorlar, arxitektura tanlovlari va nima uchun ba’zi ishlar to‘xtatilgani.

---

## Ishlab turgan tizimlar

| Tizim | Holat | Nima qiladi |
|---|---|---|
| **Davomat tizimi** | `production` | Buxoro tuman 1-son texnikumi — **784 talaba**, kuniga **3 136 davomat yozuvi** |
| **Texnikum rasmiy sayti** | `public` | Davlat ta’lim muassasasining onlayn vakolatxonasi |
| [**TradeSift**](https://tradesift.org) | `live` | Kripto bozorini saralaydigan skaner — SaaS tadqiqot platformasi |

TradeSift signal sotmaydi — u **skaner**. Minglab coin ichidan tuzilishi tahlilga
yaroqlilarini saralaydi: likvidlik, bozor sifati, tekshirilgan tarix. Signallar —
skaner ustidagi ikkinchi qatlam, va ularning natijasi, **salbiysi ham**,
o‘zgartirilmasdan e’lon qilinadi.

<details>
<summary><b>Tizim ichidan — raqamlar repozitoriyni sanashdan chiqadi</b></summary>

<br>

| | |
|---|---|
| **39 315** | qator ilova kodi (`app/`) |
| **1 521** | test, 158 faylda |
| **37** | migratsiya — tizim vaqt bilan o‘sgan |
| **40** | rejalashtirilgan fon jarayoni |
| **48** | sprint hujjati |
| **3** | til: en / ru / uz |

- Har push oldidan: **mypy** (tiplar) + **ruff** (lint) + to‘liq test to‘plami. Yashil bo‘lmasa — chiqarilmaydi.
- Tashqi API’lar **7 ta adapter** ortida izolyatsiyada. Bittasi o‘zgarsa, tahlil kodiga tegilmaydi.
- Mikrostruktura yozuvchisi har **5 soniyada** order book va savdo oqimini yozadi — uzilishlarni va uptime’ni o‘zi hisoblab boradi.
- Sirlar va ma’lumotlar bazasi hech qachon repozitoriyga tushmagan — butun git tarixi bo‘yicha tekshirilgan.

</details>

---

## Qurilgan tizimlar — foydalanuvchisiz

Bular tugallangan tizimlar, chala emas. Ular *“buni kim ishlatadi?”* degan savolga
javob bermaydi — lekin sohalar bo‘yicha qamrovni aynan shular ko‘rsatadi.

| **5** ekotizim | **3** LLM provayderi | **5** klient bitta API’da | **12** xizmatli kuzatuv steki |
|---|---|---|---|
| Python · C#/.NET · Dart · TypeScript · Vue | bitta interfeys ortida (WordFix) | Bukhara Restaurant | ExamPro |

### [WordFix](https://github.com/firdavs244/WordFix) — eng katta loyiham
AI bilan ingliz tili lug‘atini o‘rganish platformasi.
Django 5 + DRF + PostgreSQL 16 + Redis 7 + Celery/Beat; React 19 + TypeScript + Vite 6 SPA.
Uchta LLM provayderi bitta interfeys ortida (Gemini asosiy, Groq va OpenAI zaxira).
Sifat darvozasi: mypy + django-stubs, flake8, black, structlog, OpenAPI.
Monolitdan ajratish boshlangan: [api-gateway va auth-service](https://github.com/firdavs244/WordFix/tree/docs/audit-and-fix/services),
gRPC protolari, [RabbitMQ va Kubernetes manifestlari](https://github.com/firdavs244/WordFix/tree/docs/audit-and-fix/k8s).

> **1 147 test, o‘lchangan 96% qamrov** — eng katta test to‘plamim. Va bitta
> ta’minotchiga bog‘lanib qolmaslik: LLM tushsa, ikkinchisiga o‘tadi.

### [ExamPro](https://github.com/firdavs244/ExamPro)
Onlayn imtihon platformasi: yuzni tanish orqali kirish, jonli nazorat.
ASP.NET Core 9 MVC + EF Core 9 + PostgreSQL 16 + Redis 7, SignalR, face-api.js.
Docker Compose’da **12 xizmat**: Prometheus, Grafana, Seq va to‘rtta eksporter.

> Boshqa ekotizim (**C#/.NET**) va production darajasidagi kuzatuv steki —
> metrika, log va dashboard alohida xizmat sifatida.

### [RealTalk Simulator](https://github.com/firdavs244/RealTalkSim)
AI bilan ingliz tilini mashq qilish: 10 ta real vaziyat, PvP jang.
FastAPI + async SQLAlchemy 2.0 + PostgreSQL + Redis; GPT-4o-mini; React 18 +
TypeScript (strict); WebSocket orqali real vaqt ko‘p o‘yinchi rejimi.

> AI mahsulotini boshidan oxirigacha: **255 test** (167 pytest + 88 Vitest),
> freemium limitlari, real vaqt raqobat.

### [Bukhara Restaurant](https://github.com/firdavs244/BukharaRestaurant)
Restoran uchun to‘liq ekotizim: buyurtma, admin, yetkazib berish.
Django REST Framework + PostgreSQL + Redis + Celery — bitta API ustida **beshta
klient**: Flutter mijoz ilovasi, Flutter kuryer ilovasi, Vue.js admin paneli,
Telegram bot (aiogram) va web.

> Tizim integratsiyasi: bir nechta mustaqil klient bitta shartnoma ortida —
> versiyalash va mos kelish muammosi shu yerda boshlanadi.

### [Alpha Hunter](https://github.com/firdavs244/AlphaHunter)
TradeSift’dan oldingi qadam: ko‘p manbali token filtri.
FastAPI + HTMX + APScheduler; Gemini 2.0 Flash (faqat sentiment uchun),
Etherscan V2 orqali on-chain ma’lumot.

> TradeSift shu yerdan o‘sib chiqqan — va o‘sha paytdayoq README’da
> *“bu pul topish mashinasi emas”* deb yozilgan.

---

## AI agent bilan qanday ishlayman

Bu kodning katta qismi AI agent bilan yozilgan. Savol baribir beriladi, shuning
uchun javobini o‘zim yozib qo‘yaman: **muhimi kim yozgani emas — cheklovni kim
qo‘ygani va u tekshiriladimi.**

**01 · Yozma shartnoma — kod yozilishidan oldin.** Agent uchun ikkita hujjat:
qaysi fayllarni qaysi tartibda o‘qish, nimaga ruxsat yo‘q, qachon to‘xtash. Eng
muhim qatori: *ikki hujjat kelishmasa — TO‘XTA va so‘ra, taxmin qilma.*

**02 · Bitta sessiya = bitta sprint.** 48 ta sprint spetsifikatsiyasi, 38 ta
bajarilgan hisobot. Agent qamrovni o‘zi kengaytirmaydi.

**03 · Qoidalar ishonch bilan emas, test bilan majburlanadi.** Qaror qabul
qiluvchi funksiya kelajakdagi shamni ko‘ra olmaydi — har bunday funksiya
“kelajakni ko‘rmaydi” testi bilan chiqadi. Qoidani men qo‘yaman, testlar tekshiradi.

**04 · Kodbaza agent adashmaydigan qilib bo‘lingan.** Fayl medianasi — 131 qator;
59 ta tahlil modulidan 44 tasi PURE: ma’lumotlar bazasi ham, tarmoq ham yo‘q.

> Bu — “AI’dan foydalanish” emas, AI ishonchli ishlaydigan kodbaza va shartnoma
> qurish. Shuning uchun usul men bilmagan ekotizimlarga ham ko‘chdi: C#/.NET’da
> kuzatuv steki bilan platforma, Flutter’da qatlamli mobil ilova, Vue’da admin
> panel. **Til o‘zgaradi — cheklov, sprint va test bilan tekshirish o‘zgarmaydi.**

---

## Nimani qurmayman

- Nomi bor, ichida hech narsa yo‘q “AI”.
- Sinalmagan, lekin ishonchli qilib ko‘rsatilgan signal.
- Marketing uchun yashirilgan statistika.
- Faqat zamonaviy ko‘rinsin deb qurilgan murakkab arxitektura.

---

## Stack

`Python` `FastAPI` `Django / DRF` `PHP / Laravel` `C# / ASP.NET Core`
`TypeScript` `React` `Vue` `Flutter / Dart`
`PostgreSQL` `MySQL` `Redis` `RabbitMQ` `Celery`
`Docker` `Docker Swarm` `Kubernetes` `gRPC` `Nginx` `Linux` `GitHub Actions`
`Prometheus` `Grafana` `aiogram`

Stack — vosita. Qaysi biri ishlab turgan tizimda, qaysi biri o‘quv loyihasida
ekani [portfolioda](https://fromcodetocloud.uz) aniq yozilgan.

---

## Aloqa

Sizga shunchaki kod emas, natijasi o‘lchanadigan tizim kerak bo‘lsa — yozing.

[xolovfirdavs9@gmail.com](mailto:xolovfirdavs9@gmail.com) ·
[LinkedIn](https://www.linkedin.com/in/firdavs-kholov-0143902a3/) ·
[Telegram](https://t.me/firdavs_kholov) ·
[fromcodetocloud.uz](https://fromcodetocloud.uz)

<!--
  LinkedIn note: HTTP verification is impossible here — linkedin.com returns 999
  to every automated request, including for profiles that certainly exist, and
  serves a signup wall to logged-out browsers. So this uses the URL Firdavs
  himself provided, which is the only one with evidence behind it.

  The portfolio currently links to /in/firdavs-kholov (no numeric suffix). Those
  are two different URLs and one of them is probably wrong — worth checking
  while logged in, and fixing in whichever place is stale.
-->

