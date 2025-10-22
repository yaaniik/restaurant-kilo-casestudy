# 🍽️ ANT_RESERVE - Piattaforma Multi-Tenant per Ristoranti

> Sistema completo di gestione prenotazioni, sondaggi e contenuti per attività di ristorazione con architettura multi-cliente.

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://www.kiloristorante.it/)
[![Status](https://img.shields.io/badge/status-in%20development-yellow)]()
[![License](https://img.shields.io/badge/license-proprietary-red)]()

---

## 📋 Panoramica

**ANT_RESERVE** è una piattaforma SaaS white-label pensata per digitalizzare la gestione operativa di ristoranti, pizzerie, trattorie e attività food & beverage. 

Il sistema offre un'interfaccia cliente completamente personalizzabile e una dashboard amministrativa per gestire prenotazioni, raccogliere feedback e monitorare l'andamento dell'attività.

### 🎯 Problema Risolto

Piccole e medie attività di ristorazione necessitano di:
- Sistema prenotazioni senza costi di commissione terze parti
- Strumenti per raccogliere feedback clienti in modo strutturato
- Presenza online professionale senza competenze tecniche
- Soluzione economica e scalabile

---

## ✨ Funzionalità Principali

### 👥 Area Cliente
- **Prenotazioni Online**: Sistema di booking con selezione data/ora e preferenze tavolo
- **Galleria Fotografica**: Showcase del locale e dei piatti
- **Menu Digitale**: Visualizzazione menu aggiornabile con immagini
- **Sondaggi Feedback**: Raccolta strutturata di recensioni e NPS

### 🔐 Area Amministrativa
- **Dashboard Prenotazioni**: Gestione completa con filtri, modifica ed eliminazione
- **Analisi Sondaggi**: Statistiche aggregate con grafici (giorno/settimana/mese/anno)
- **Gestione Contenuti**: Upload immagini e aggiornamento galleria
- **Multi-utente**: Sistema di autenticazione con ruoli

### 🎨 Personalizzazione
- **White-Label**: Branding completamente personalizzabile per cliente
- **Multi-Tenant**: Un'unica codebase, dati segregati per cliente
- **Dominio Personalizzato**: Ogni cliente può avere il proprio dominio

---

## 🏗️ Architettura Tecnica

### Stack Tecnologico

**Frontend**
- React 19 + TypeScript
- Vite (build tool)
- Mantine UI (component library)
- React Router v7

**Backend**
- PHP 8+ (API RESTful)
- File-based storage (JSON)

**Infrastruttura**
- Hosting condiviso (Aruba/simili)
- Cloudflare DNS + CDN
- Cronjob esterni (cron-job.org)

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
- Deploy singolo, aggiornamenti globali istantanei
- Isolamento totale dei dati tra clienti
- Onboarding nuovo cliente: ~30 minuti
- Scalabilità fino a 50+ clienti su hosting condiviso

---

## 📊 Metriche di Performance

<img width="933" height="514" alt="image" src="https://github.com/user-attachments/assets/eefbcdca-efdb-407a-8050-e226e5c0c71e" />

---

## 🚀 Roadmap & Status

### ✅ Completato (v0.1)
- [x] Sistema prenotazioni completo
- [x] Dashboard amministrativa
- [x] Sondaggi con analisi temporali
- [x] Gestione utenti e autenticazione
- [x] Upload e gestione immagini
- [x] Architettura multi-tenant
- [x] Rollover automatico dati (cronjob)

### 🔄 In Sviluppo (v0.2)
- [ ] Sistema config.json per personalizzazione dinamica
- [ ] API per servire configurazioni cliente
- [ ] Context React per branding dinamico
- [ ] Migrazione immagini da assets a storage cliente
- [ ] Sistema di log e monitoring

### 📅 Pianificato (v0.3+)
- [ ] Sistema di notifiche (email/SMS)
- [ ] Integrazione pagamenti online
- [ ] App mobile (React Native)
- [ ] Statistiche avanzate (ML per predizioni)
- [ ] Sistema di recensioni pubbliche
- [ ] Integrazione social media

---

## 🛠️ Installazione & Setup

### Prerequisiti
- Node.js >= 24.1.0
- PHP >= 8.0
- Web server (Apache/Nginx)

### Setup Locale
```bash
# Clone repository
git clone [repository-url]
cd ANT_RESERVE/prototype

# Installa dipendenze
npm install

# Avvia dev server
npm run dev
```

### Build Produzione
```bash
# Build ottimizzato
npm run build

# Output in dist/
# Carica dist/ + api/ + data/ su hosting
```

### Configurazione Backend

1. Configura permessi cartella `data/`: `chmod 755 -R data/`
2. Crea `data/active_client.txt` con ID cliente
3. Configura cronjob per `api/survey/cron_sondaggi.php`

---

## 📂 Struttura Progetto
```
prototype/
├── api/                    # Backend PHP (RESTful endpoints)
│   ├── auth/              # Login, sessioni
│   ├── config/            # ConfigHelper multi-tenant
│   ├── reservation/       # CRUD prenotazioni
│   ├── survey/            # Sondaggi + cronjob rollover
│   └── users/             # Gestione utenti
│
├── data/                   # Storage persistente
│   ├── active_client.txt  # Cliente attivo (runtime)
│   └── clients/           # Dati segregati per cliente
│       ├── cliente1/
│       │   ├── prenotazioni.json
│       │   ├── sondaggi.json
│       │   ├── users.json
│       │   └── images/
│       └── cliente2/
│
├── src/
│   ├── components/        # Componenti riutilizzabili
│   │   ├── common/       # Button, Card, Modal...
│   │   └── layout/       # Header, Footer, Layout
│   │
│   ├── pages/            # Pagine principali
│   │   ├── HomePage/
│   │   ├── ReservationPage/
│   │   ├── SurveyPage/
│   │   └── Dashboard/
│   │       ├── Prenotazioni/
│   │       ├── SurveyDash/
│   │       └── ManageUser/
│   │
│   ├── context/          # State management (React Context)
│   ├── hooks/            # Custom hooks
│   ├── services/         # API calls
│   └── utils/            # Helper functions
│
├── public/               # Asset statici
└── dist/                 # Build output (generato)
```

---

## 🔐 Sicurezza

- **Autenticazione**: Session-based con token
- **Validazione Input**: Server-side su tutti gli endpoint
- **Protezione CSRF**: Token nelle form critiche
- **File Upload**: Validazione tipo e dimensione
- **SQL Injection**: N/A (file-based storage)
- **XSS Prevention**: Sanitizzazione output React

---

## 📈 Case Study: Ristorante KILO

**Cliente**: Ristorante di pesce, Anzio (RM)  
**Deployment**: Dicembre 2024  
**URL**: [www.kiloristorante.it](https://www.kiloristorante.it/)

**Risultati**:
- Prenotazioni digitalizzate: +60% efficienza gestione
- Feedback raccolti: 150+ nel primo mese
- Tempo onboarding: 2 ore (setup + formazione)
- Costo mensile gestione: €0 (hosting condiviso)

---

## 🤝 Contributi

Questo è un progetto proprietario attualmente non aperto a contributi esterni. 

---

## 📄 Licenza

Proprietario - Tutti i diritti riservati  
© 2024-2025 [Yanik Dimitrov/ KILO ristorante]

---

## 📞 Contatti

- **Sito**: [YD-yanikdimitrov](https://yanikdimitrov.vercel.app/)
- **Email**: yanik.dimitrov@outlook.com
- **LinkedIn**: [Yanik Dimitrov](https://www.linkedin.com/in/yanik-dimitrov/)

---

## 🙏 Ringraziamenti

- [Mantine UI](https://mantine.dev/) - Component library
- [Vite](https://vitejs.dev/) - Build tool
- [React](https://react.dev/) - Framework

---

<p align="center">
  <sub>Built with ❤️ for the restaurant industry</sub>
</p>
