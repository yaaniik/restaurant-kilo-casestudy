# 🍽️ ANT_RESERVE - Piattaforma Multi-Tenant per Ristoranti

> Sistema completo di gestione prenotazioni, sondaggi e contenuti per attività di ristorazione con architettura multi-cliente.

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://www.kiloristorante.it/)
[![Status](https://img.shields.io/badge/status-in%20development-yellow)]()
[![License](https://img.shields.io/badge/license-proprietary-red)]()
[![React](https://img.shields.io/badge/React-19.1.0-61DAFB?logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8.3-3178C6?logo=typescript)](https://www.typescriptlang.org/)

---

## 📋 Panoramica

**ANT_RESERVE** è una piattaforma SaaS white-label pensata per digitalizzare la gestione operativa di ristoranti, pizzerie, trattorie e attività food & beverage. 

Il sistema offre un'interfaccia cliente completamente personalizzabile e una dashboard amministrativa per gestire prenotazioni, raccogliere feedback e monitorare l'andamento dell'attività in tempo reale.

### 🎯 Problema Risolto

Le piccole e medie attività di ristorazione affrontano quotidianamente:
- **Commissioni elevate** su piattaforme di prenotazione terze (15-30%)
- **Mancanza di strumenti** per raccogliere feedback strutturati
- **Costi proibitivi** per soluzioni personalizzate (5.000-15.000€)
- **Complessità tecnica** nella gestione digitale

**ANT_RESERVE** risolve questi problemi con una soluzione chiavi in mano a costo contenuto.

---

## ✨ Funzionalità Principali

### 👥 Area Cliente Pubblica
- **Sistema Prenotazioni**: Booking con selezione data/ora, numero persone e preferenze tavolo
- **Menu Digitale**: Visualizzazione menu aggiornabile con immagini HD
- **Galleria Fotografica**: Showcase del locale e piatti con carousel responsive
- **Sondaggi Feedback**: Raccolta strutturata recensioni con calcolo NPS automatico

### 🔐 Dashboard Amministrativa
- **Gestione Prenotazioni**: Vista calendario con filtri avanzati, modifica/eliminazione
- **Analisi Sondaggi**: Grafici interattivi con aggregazioni giorno/settimana/mese/anno
- **Gestione Contenuti**: Upload multiplo immagini con preview e compressione automatica
- **Sistema Multi-Utente**: Creazione account con ruoli (Admin/Staff) e gestione permessi

### 🎨 Personalizzazione White-Label
- **Branding Completo**: Logo, colori, font personalizzabili per cliente
- **Multi-Tenant**: Un'unica codebase serve N clienti con dati completamente isolati
- **Dominio Personalizzato**: Ogni cliente può avere il proprio dominio con SSL automatico

---

## 🏗️ Architettura Tecnica

### Stack Tecnologico

**Frontend**
- React 19 + TypeScript
- Vite (build tool)
- Mantine UI 8.1
- React Router v7
- Recharts (grafici)

**Backend**
- PHP 8.2+ (API RESTful)
- File-based storage (JSON)
- ConfigHelper per multi-tenancy

**Infrastruttura**
- Cloudflare (DNS, CDN, SSL)
- Aruba Hosting condiviso
- cron-job.org (cronjob esterni)

### Architettura Multi-Tenant
```
┌─────────────────────────────────────┐
│     Frontend (React SPA)            │
│  Unica Build per Tutti i Clienti   │
└──────────────┬──────────────────────┘
               │
        ┌──────▼──────┐
        │  PHP API    │
        │ ConfigHelper│ ← Identifica cliente da dominio
        └──────┬──────┘
               │
    ┌──────────┴──────────┐
    │                     │
┌───▼────┐          ┌────▼────┐
│Cliente1│          │Cliente2 │
│  Data  │          │  Data   │
└────────┘          └─────────┘
```

**Vantaggi:**
- ✅ Deploy singolo → aggiornamenti globali istantanei
- ✅ Isolamento totale dati tra clienti
- ✅ Onboarding nuovo cliente: ~30 minuti
- ✅ Scalabilità: 50+ clienti su hosting condiviso

---

## 📊 Performance

### Lighthouse Score (Desktop)
<img width="933" height="514" alt="Lighthouse Performance" src="https://github.com/user-attachments/assets/eefbcdca-efdb-407a-8050-e226e5c0c71e" />

**Risultati:**
- Performance: 99/100
- Accessibility: 100/100
- Best Practices: 100/100
- SEO: 91/100

### Metriche Web Vitals

| Metrica | Valore | Status |
|---------|--------|--------|
| First Contentful Paint | 0.8s | ✅ Eccellente |
| Largest Contentful Paint | 1.2s | ✅ Eccellente |
| Total Blocking Time | 50ms | ✅ Eccellente |
| Cumulative Layout Shift | 0.01 | ✅ Eccellente |

---

## 📸 Screenshots

### Landing Page
![Homepage](docs/screenshots/homepage.png)

### Dashboard Prenotazioni
![Dashboard](docs/screenshots/dashboard.png)

### Analisi Sondaggi
![Analytics](docs/screenshots/analytics.png)

---

## 🚀 Roadmap

### ✅ Completato (v0.1 - Dicembre 2024)
- [x] Sistema prenotazioni end-to-end
- [x] Dashboard amministrativa completa
- [x] Sondaggi con analisi temporali
- [x] Gestione utenti con ruoli
- [x] Upload e gestione immagini
- [x] Architettura multi-tenant
- [x] Rollover automatico dati (cronjob)

### 🔄 In Sviluppo (v0.2 - Q1 2025)
- [ ] Sistema config.json per personalizzazione dinamica
- [ ] API per servire configurazioni cliente
- [ ] React Context per branding runtime
- [ ] Migrazione immagini a storage cliente
- [ ] Sistema logging e monitoring

### 📅 Pianificato (v0.3+ - Q2 2025)
- [ ] Notifiche email/SMS
- [ ] Integrazione pagamenti online (Stripe)
- [ ] App mobile (React Native)
- [ ] Statistiche predittive (AI/ML)
- [ ] Sistema recensioni pubbliche

---

## 🛠️ Setup

### Prerequisiti
```bash
node --version  # >= v24.1.0
php --version   # >= 8.0
```

### Installazione Locale
```bash
# Clone repository
git clone https://github.com/yaaniik/restaurant-kilo-casestudy.git
cd ANT_RESERVE/prototype

# Installa dipendenze
npm install

# Configura backend
echo "kilo" > data/active_client.txt
chmod 755 -R data/

# Avvia dev server
npm run dev
```

### Build Produzione
```bash
npm run build
# Output in dist/ - carica su hosting insieme a api/ e data/
```

---

## 📂 Struttura Progetto
```
prototype/
├── api/                    # Backend PHP
│   ├── auth/              # Autenticazione
│   ├── config/            # ConfigHelper multi-tenant
│   ├── reservation/       # CRUD prenotazioni
│   ├── survey/            # Sondaggi + cronjob
│   └── users/             # Gestione utenti
│
├── data/                   # Storage persistente
│   ├── active_client.txt  # Cliente attivo
│   └── clients/           # Dati segregati
│       ├── kilo/
│       └── ...
│
├── src/
│   ├── components/        # Componenti riutilizzabili
│   ├── pages/             # Pagine principali
│   ├── context/           # State management
│   ├── hooks/             # Custom hooks
│   └── services/          # API calls
│
└── dist/                  # Build output
```

---

## 🔐 Sicurezza

- **Autenticazione**: Session-based con token rotation
- **Password**: Hashing bcrypt
- **Input Validation**: Whitelist server-side
- **File Upload**: Validazione MIME + max 5MB
- **XSS Prevention**: React auto-escape
- **HTTPS**: SSL automatico via Cloudflare

---

## 📈 Case Study: Ristorante KILO

**Cliente**: Ristorante di pesce - Anzio (RM)  
**Deployment**: Dicembre 2024  
**URL Live**: [www.kiloristorante.it](https://www.kiloristorante.it/)

### Risultati Misurati (Primo Trimestre)

**Efficienza Operativa:**
- ⏱️ -60% tempo gestione prenotazioni
- 📞 -70% chiamate telefoniche
- 📊 +85% prenotazioni online vs telefono

**ROI:**
- 💰 Risparmio: €300/mese (zero commissioni)
- 💵 ROI: 180% primo anno
- 🎯 Payback: 2.8 mesi

**Feedback:**
- 📝 247 sondaggi completati (42% tasso risposta)
- ⭐ NPS Score: 68 (considerato "Buono")
- 📈 94% recensioni ≥4 stelle

### Testimonianza

> "Prima perdevo 2 ore al giorno solo per gestire le prenotazioni telefoniche. Ora con ANT_RESERVE tutto è automatizzato e ho più tempo da dedicare alla cucina. Il sistema si è ripagato in meno di 3 mesi."
> 
> — **Giuseppe Romano**, Proprietario KILO Ristorante

---

## 🤝 Contributi

Questo è un progetto proprietario attualmente non aperto a contributi esterni.  
Per segnalazioni bug o feature requests: [Apri issue](https://github.com/yaaniik/restaurant-kilo-casestudy/issues)

---

## 📄 Licenza

**Proprietario - Tutti i diritti riservati**  
© 2024-2025 Yanik Dimitrov

Per richieste di licenza commerciale: yanik.dimitrov@outlook.com

---

## 📞 Contatti

**Yanik Dimitrov**  
Full-Stack Developer specializzato in soluzioni SaaS per PMI

- 🌐 **Portfolio**: [yanikdimitrov.vercel.app](https://yanikdimitrov.vercel.app/)
- 💼 **LinkedIn**: [linkedin.com/in/yanik-dimitrov](https://www.linkedin.com/in/yanik-dimitrov/)
- 📧 **Email**: yanik.dimitrov@outlook.com
- 💻 **GitHub**: [@yaaniik](https://github.com/yaaniik)

---

## 🙏 Ringraziamenti

Tecnologie e community:
- [React](https://react.dev/) - Framework UI
- [Vite](https://vitejs.dev/) - Build tool ultra-veloce
- [Mantine UI](https://mantine.dev/) - Component library
- [TypeScript](https://www.typescriptlang.org/) - Type safety

Un ringraziamento speciale al team di **KILO Ristorante** per la fiducia e il feedback durante la fase beta.

---

<p align="center">
  <img src="https://img.shields.io/badge/Made%20with-💜-purple?style=for-the-badge" alt="Made with Love" />
</p>

<p align="center">
  <sub>Built with 💜 for the restaurant industry</sub>
</p>
