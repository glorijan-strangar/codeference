☀️ Pametni Energetski Pomoćnik (Digitalni Blizanac)
Projekat za Hakaton: Pametni AI sistem za upravljanje solarnim panelima, baterijskim skladištem i električnim vozilom (EV) namenjen malim preduzećima.

📌 O Projektu
Mala preduzeća (pekare, radionice, frizerski saloni, mali hoteli) često poseduju obnovljive izvore energije, ali vlasnici nemaju vremena ni znanja da ručno upravljaju radom baterija i EV punjača.
Cilj projekta: Kreirati digitalnog blizanca male firme koji na osnovu AI predikcija solara i potrošnje, uz laganu i brzu matematiku upravljanja, daje vlasniku jednostavne i jasne preporuke na dnevnom nivou (npr. „Sutra je sunčano, napuni bateriju do podne”) i prikazuje konkretnu finansijsku uštedu u dinarima (RSD).

📐 Arhitektura Rešenja i Principi
Sistem se zasniva na tri brza, stabilna i efikasna stuba:
[ Podaci i Regresija (AI) ] ──► [ Heuristički Mozak (Rules) ] ──► [ Prikaz (React App) ]

1. Brza AI Predikcija (Linearna / Polinomijalna Regresija)
Umesto prekomplikovanih AI modela, koristi se lagana regresija bazirana na pandas i numpy (ili scikit-learn) bibliotekama koja u milisekundi procenjuje vrednosti za naredna 24 časa:
•	Solarna predikcija: Na osnovu doba dana i prognoziranog sunčevog zračenja/oblačnosti ocenjuje generisanu snagu (kW).
•	Predikcija potrošnje: Na osnovu istorijskih podataka, sata u danu i tipa dana (radni dan / vikend) procenjuje profil potrošnje (kW).

2. Mozak Sistema (Rule-Based Heuristika)
Umesto teške visoke matematike i složenog linearnog programiranja, mozak sistema koristi efikasan set 'if-else' pravila koja donose finansijski optimalne odluke:
•	Pravilo 1 (Niža tarifa): Tokom jeftine tarife (noću 00:00h - 08:00h) baterija se dopunjava iz mreže.
•	Pravilo 2 (Višak solara): Kada solarni paneli daju višak u odnosu na potrošnju, energija se preusmerava u bateriju ili EV punjač.
•	Pravilo 3 (Pražnjenje): Tokom skupe tarife i manjka solara, energija se crpi iz baterije umesto iz mreže čime se direktno štede dinari.

3. Pametni Interfejs (UX / UI Principle)
Vlasnik firme dobija jasne akcione preporuke izračunate u backendu na jednostavnom jeziku:
•	🟢 „Danas do 14h napunite dostavno vozilo — solar daje maksimum, ušteda 450 RSD.”
•	🟡 „Noćas u 02h baterija se puni po nižoj tarifi za sutrašnji jutarnji pik.”
•	💰 „Ukupna procenjena ušteda za ovu nedelju: 4.200 RSD.”
🛠 Tech Stack
Backend & AI (Python)
•	Framework: FastAPI (Automatska OpenAPI/Swagger dokumentacija na /docs, visoke performanse)
•	Data & AI: pandas, numpy, scikit-learn (za brzu i laganu regresiju)
•	Optimizacija: Poređenje satne potrošnje, solara i tarifa kroz čistu Python logiku
Frontend (React)
•	Build Tool: React + Vite (brz rad i razvoj)
•	Styling & UI: Tailwind CSS + shadcn/ui (ili Material-UI)
•	Vizuelizacija: Recharts ili Chart.js (grafikoni satne potrošnje, stanja baterije i uštede)

📂 Struktura Repozitorijuma (Monorepo)
 .
 ├── backend/
 │   ├── main.py              # FastAPI ulazna tačka
 │   ├── requirements.txt      # Python zavisnosti (fastapi, pandas, numpy, scikit-learn)
 │   ├── models/              # Regresioni model za predikciju solara i potrošnje
 │   ├── services/            # Rule-based algoritam za preporuke i uštedu
 │   └── data/                # Istorijski podaci i simulator
 ├── frontend/
 │   ├── package.json
 │   ├── vite.config.js
 │   └── src/
 │       ├── components/      # UI kartice sa savetima, grafikoni
 │       └── services/        # Axios/Fetch komunikacija sa API-jem
 └── README.md

⚙️ Uputstvo za Instalaciju i Pokretanje
Prerequisites
•	Git (za kloniranje repozitorijuma)
•	Python 3.10+
•	Node.js 18+ i npm

1. Kloniranje Repozitorijuma
# Klonirajte repozitorijum sa GitHub-a
git clone https://github.com/glorijan-strangar/codeference.git

# Uđite u koren projekta
cd codeference

2. Backend Podešavanje
# Uđi u backend folder
cd backend

# Kreiraj virtuelno okruženje
python -m venv venv

# Aktiviraj virtuelno okruženje
# Windows (Git Bash):
source venv/Scripts/activate
# Windows (CMD):
venv\Scripts\activate.bat
# Linux/macOS:
source venv/bin/activate

# Instaliraj lagane zavisnosti
pip install -r requirements.txt

# Pokreni FastAPI server
uvicorn main:app --reload

Backend API: http://localhost:8000 | Swagger doks: http://localhost:8000/docs

3. Frontend Podešavanje
# Uđi u frontend folder (iz korena projekta)
cd frontend

# Instaliraj zavisnosti
npm install

# Pokreni razvojni server
npm run dev

Frontend aplikacija: http://localhost:5173

📝 Zapisnik / Checklist za Hakaton
•	[x] Definisana arhitektura sistema i monorepo struktura
•	[x] Postavljen GitHub repozitorijum (codeference)
•	[x] Pripravljen jednostavan requirements.txt sa laganim bibliotekama
•	[ ] Analiza dobijenih godišnjih podataka i simulatora
•	[ ] Implementacija regresije za predikciju solara i potrošnje
•	[ ] Izrada Rule-Based algoritma za preporuke i kalkulaciju uštede
•	[ ] Povezivanje FastAPI ruta sa frontendom
•	[ ] Izrada React UI interfejsa sa preporukama i grafikonom
•	[ ] Testiranje na simulatoru i priprema finalne prezentacije
