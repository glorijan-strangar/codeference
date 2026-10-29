# codeference

Pametni Energetski Pomoćnik

Projekat za Hakaton: Pametni AI sistem za upravljanje solarnim panelima, baterijskim skladištem i električnim vozilom (EV) namenjen malim preduzećima.

O Projektu
Mala preduzeća (pekare, radionice, frizerski saloni, mali hoteli) često poseduju obnovljive izvore energije, ali vlasnici nemaju vremena ni znanja da ručno upravljaju radom baterija i EV punjača.

Cilj projekta: Kreirati digitalnog blizanca male firme koji na osnovu AI predikcija solara i potrošnje, uz matematičku optimizaciju tarifa, daje vlasniku jednostavne i jasne preporuke na dnevnom nivou (npr. „Sutra je sunčano, napuni bateriju do podne”) i prikazuje konkretnu finansijsku uštedu u dinarima (RSD).

Arhitektura Rešenja i Principi
Sistem se sastoji od tri ključna stuba:
[ Podaci i Prognoza (AI) ] ──► [ Mozak (Optimizator) ] ──► [ Prikaz (React App) ]

1. Predikcija (AI / Time-Series Forecast)
Umesto nagađanja, AI model predviđa parametre za naredna 24 časa:
•	Solarna proizvodnja: Na osnovu vremenske prognoze (zračenje, temperatura) predviđa generisanu snagu (kW).
•	Potrošnja objekta: Na osnovu istorijskih podataka firme, dana u nedelji i doba dana predviđa profil potrošnje (kW).

2. Mozak Sistema (Matematička Optimizacija)
Optimizacija izbegava klasične izvode (f'(x) = 0) zbog nejednakih ograničenja i diskretnih časovnih koraka. Umesto toga koristi Linearno / Dinamičko programiranje ili Rule-Based heuristiku:
•	Funkcija cilja: Minimizacija ukupnog troška električne energije za narednih 24h u dinarima.
•	Ograničenja (Constraints): Kapacitet baterije: 0 ≤ C ≤ C_max
•	Maksimalna snaga punjenja/pražnjenja (kW)
•	Dve cene struje (viša/niža tarifa ili dinamička cena po kWh)
•	Nepomerljiva potrošnja primarne delatnosti firme (npr. peć u pekari)

3. Pametni Interfejs (UX / UI Principle)
Vlasnik firme ne treba biti pretrpan kompleksnim grafikonima sa jednačinama, oni mogu biti u nekom dashboard-u ako vlasnik bas pozeli da ih vidi. Aplikacija prevodi optimizacione rezultate u akcione preporuke na jeziku korisnika:
•	🟢 „Danas do 14h napunite dostavno vozilo — solar daje maksimum, ušteda 450 RSD.”
•	🟡 „Noćas u 02h baterija se puni po nižoj tarifi za sutrašnji jutarnji pik.”
•	💰 „Ukupna procenjena ušteda za ovu nedelju: 4.200 RSD.”
Tech Stack
Backend & AI (Python)
•	Framework: FastAPI (Automatska OpenAPI/Swagger dokumentacija na /docs, visoke performanse)
•	Data & AI: pandas, numpy, scikit-learn / xgboost (za treniranje modela predikcije)
•	Optimizacija: PuLP ili SciPy.optimize (za Mixed-Integer Linear Programming optimizaciju punjenja/pražnjenja)
Frontend (React)
•	Build Tool: React + Vite (brz rad i razvoj)
•	Styling & UI: Tailwind CSS + shadcn/ui (ili Material-UI)
•	Vizuelizacija: Recharts ili Chart.js (grafikoni satne potrošnje, stanja baterije i uštede)

Struktura Repozitorijuma
 .
 ├── backend/
 │   ├── main.py              # FastAPI ulazna tačka
 │   ├── requirements.txt      # Python zavisnosti
 │   ├── models/              # Trenirani AI modeli za predikciju
 │   ├── services/            # Optimizacioni alati (PuLP/SciPy)
 │   └── data/                # Istorijski podaci i simulator
 ├── frontend/
 │   ├── package.json
 │   ├── vite.config.js
 │   └── src/
 │       ├── components/      # UI kartice sa savetima, grafikoni
 │       └── services/        # Axios/Fetch komunikacija sa API-jem
 └── README.md

Uputstvo za Instalaciju i Pokretanje
Prerequisites
•	Python 3.10+
•	Node.js 18+ i npm
1. Backend Podešavanje
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

# Instaliraj zavisnosti
pip install -r requirements.txt

# Pokreni FastAPI server
uvicorn main:app --reload

Backend API: http://localhost:8000 | Swagger doks: http://localhost:8000/docs
2. Frontend Podešavanje
# Uđi u frontend folder (iz korena projekta)
cd frontend

# Instaliraj zavisnosti
npm install

# Pokreni razvojni server
npm run dev

Frontend aplikacija: http://localhost:5173
Zapisnik / Checklist za Hakaton
•	[x] Definisana arhitektura sistema i monorepo struktura
•	[ ] Analiza dobijenih godišnjih podataka i simulatora
•	[ ] Implementacija AI modela za predikciju solara i potrošnje
•	[ ] Izrada optimizacionog algoritma za bateriju i EV punjač (PuLP)
•	[ ] Povezivanje FastAPI ruta sa modelom i optimizatorom
•	[ ] Izrada React UI interfejsa sa prikazom preporuka i grafikona uštede
•	[ ] Testiranje na simulatoru i priprema finalne prezentacije
