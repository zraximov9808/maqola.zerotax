# ZeroTax — Maqolalar sayti va admin panel

## Qanday ishlaydi

```
Admin panel (/admin)  ──commit──▶  GitHub repo  ──avto deploy──▶  maqola.zerotax.uz
   maqola yozasiz                data/articles.json                 1–2 daqiqada yangilanadi
                                 images/*.jpg
```

- Server ham, baza ham kerak emas. Barcha maqolalar `data/articles.json` faylida saqlanadi.
- «E'lon qilish» tugmasi shu faylni GitHub'ga commit qiladi. Hosting (Netlify yoki GitHub Pages) commitni ko'rib, saytni o'zi yangilaydi.
- Admin panelga faqat GitHub tokeni bor odam kira oladi. Token kodda saqlanmaydi, faqat sizning brauzeringizda turadi.

## Fayllar

| Fayl | Vazifasi |
|---|---|
| `index.html` | Ommaviy sayt: maqolalar ro'yxati, qidiruv, maqola sahifasi |
| `admin/index.html` | Admin panel |
| `data/articles.json` | Barcha maqolalar va bo'limlar (panel o'zi yangilaydi) |
| `images/` | Panel orqali yuklangan rasmlar |

## Bir martalik sozlash (taxminan 15 daqiqa)

### 1. GitHub repo yaratish
1. https://github.com/new → nomi: `zerotax-maqolalar` → **Private** → Create.
2. «uploading an existing file» → shu papkadagi hamma narsani (index.html, admin, data, images, README.md) sudrab tashlang → Commit.

### 2. Hosting: Netlify (tavsiya)
1. https://app.netlify.com → **Add new site → Import an existing project → GitHub** → `zerotax-maqolalar` ni tanlang.
2. Build command: bo'sh qoldiring. Publish directory: `/` (yoki bo'sh). → **Deploy**.
3. **Domain management → Add a domain** → `maqola.zerotax.uz`.
4. Domen DNS panelida: `CNAME  maqola  →  <sayt-nomi>.netlify.app` yozuvini qo'shing. HTTPS o'zi yoqiladi.

> Muqobil: GitHub Pages (repo **Public** bo'lishi kerak): Settings → Pages → Branch: `main` / root. DNS: `CNAME maqola → zraximov9808.github.io`.
> Eslatma: public repoda qoralamalar ham `data/articles.json` ichida ko'rinib turadi (saytda chiqmaydi). Shuning uchun Private + Netlify yaxshiroq.

### 3. Token yaratish
1. https://github.com/settings/personal-access-tokens/new
2. Token name: `zerotax-admin`, Expiration: 1 yil.
3. Repository access: **Only select repositories** → `zerotax-maqolalar`.
4. Permissions → Repository permissions → **Contents: Read and write**. Boshqa hech narsa kerak emas.
5. Generate → tokenni nusxalang (bir marta ko'rsatiladi).

### 4. Admin panelga kirish
`https://maqola.zerotax.uz/admin/` → repo nomi va tokenni kiriting → Kirish.

### 5. Asosiy saytga link qo'shish
`buxplatform` loyihasidagi header menyusiga: `Maqolalar → https://maqola.zerotax.uz`

## Kundalik ish

1. `/admin/` → **+ Yangi maqola**
2. Sarlavha yozing (manzil o'zi hosil bo'ladi), qisqa tavsif, bo'lim.
3. Matnni yozing yoki Word/Telegramdan nusxalang. Ortiqcha formatlash o'zi tozalanadi.
   - **H2** sarlavhalar saytda mundarijaga tushadi.
   - **⚠ Eslatma**, **ƒ Formula**, **▦ Jadval**, **🖼 Rasm** tugmalari.
   - Rasmni muharrirga sudrab tashlasa ham bo'ladi. Katta rasmlar o'zi kichraytiriladi.
4. **Qoralama saqlash**: saytda ko'rinmaydi. **E'lon qilish**: 1–2 daqiqada saytda chiqadi.
5. `Ctrl+S`: tez saqlash.

## Xavfsizlik
- Tokenni hech kimga bermang va kodga yozmang.
- Begona kompyuterda «Eslab qolish» belgisini olib tashlang yoki ishdan keyin **Chiqish** ni bosing.
- Token o'g'irlansa: GitHub → Settings → Personal access tokens → tokenni **Revoke** qiling va yangisini yarating.
