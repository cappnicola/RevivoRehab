# Guida al Deployment su Netlify

Ho configurato il sito per funzionare su Netlify. Ecco tutto quello che è stato modificato e come procedere.

## 🔧 Modifiche Implementate

### 1. **Dati Statici**
- Creati file JSON statici in `client/src/data/`:
  - `blog-posts.json` - Articoli del blog
  - `testimonials.json` - Testimonianze clienti  
  - `availability.json` - Orari di disponibilità

### 2. **Frontend Modificato**
- Nuovo query client (`client/src/lib/staticQueryClient.ts`) che usa dati statici
- App aggiornata per usare il nuovo sistema di dati
- Form di contatto convertito per Netlify Forms

### 3. **Build Script per Netlify**
- Script automatico in `scripts/build-netlify.js`
- Genera solo il frontend statico (senza backend)
- Ottimizzato per deployment su Netlify

### 4. **Configurazione Netlify**
- File `netlify.toml` con tutte le impostazioni necessarie
- Redirect SPA per routing client-side
- Headers di sicurezza e cache
- Configurazione Netlify Forms

## 🚀 Come Fare il Deploy

### 1. **Preparazione Repository GitHub**
```bash
# 1. Inizializza git (se non già fatto)
git init

# 2. Aggiungi tutti i file
git add .

# 3. Fai il commit
git commit -m "Setup per deployment Netlify"

# 4. Aggiungi il repository GitHub
git remote add origin https://github.com/TUO-USERNAME/TUO-REPOSITORY.git

# 5. Push su GitHub
git push -u origin main
```

### 2. **Setup su Netlify**
1. Vai su [netlify.com](https://netlify.com) e accedi
2. Clicca "New site from Git"
3. Connetti il tuo repository GitHub
4. Le impostazioni saranno automatiche grazie al file `netlify.toml`:
   - **Build command**: `node scripts/build-netlify.js`
   - **Publish directory**: `dist`
5. Clicca "Deploy site"

### 3. **Verifica Deployment**
- Il sito sarà disponibile su un URL tipo: `https://nome-sito.netlify.app`
- I form di contatto funzioneranno automaticamente con Netlify Forms
- Tutte le sezioni (blog, testimoniali, contatti) funzioneranno con dati statici

## 📋 Differenze tra Versione Locale e Netlify

| Funzione | Locale (Replit) | Netlify |
|----------|-----------------|---------|
| **Blog Posts** | Database PostgreSQL | File JSON statico |
| **Testimoniali** | Database PostgreSQL | File JSON statico |
| **Form Contatti** | Backend Express.js | Netlify Forms |
| **Newsletter** | Backend Express.js | Netlify Forms |
| **Prenotazioni** | Database PostgreSQL | Netlify Forms |

## ✅ Cosa Funziona su Netlify

- ✅ Tutte le sezioni del sito
- ✅ Navigazione e design completo
- ✅ Blog con articoli e filtri
- ✅ Testimoniali e recensioni
- ✅ Form di contatto (via Netlify Forms)
- ✅ Responsive design
- ✅ Performance ottimizzate
- ✅ WhatsApp integration

## 📧 Gestione Form Netlify

I form inviati tramite il sito verranno:
1. Salvati nel pannello Netlify sotto "Forms"
2. Inviati via email all'indirizzo configurato
3. Disponibili per integrazione con servizi esterni

Per configurare notifiche email:
1. Vai nel pannello Netlify > Site Settings > Forms
2. Imposta notifiche email
3. Aggiungi integrazioni (Zapier, etc.) se necessario

## 🔄 Aggiornamenti Futuri

Per aggiornare contenuti:
1. **Blog Posts**: Modifica `client/src/data/blog-posts.json`
2. **Testimoniali**: Modifica `client/src/data/testimonials.json`
3. **Push su GitHub**: Il sito si aggiorna automaticamente

## 🚨 Note Importanti

- ⚠️ Su Netlify **NON** hai accesso al database PostgreSQL
- ⚠️ I form usano Netlify Forms invece del backend Express
- ⚠️ Per funzioni avanzate potresti dover usare Netlify Functions
- ✅ Tutti i contenuti principali funzionano perfettamente

Il sito è ora pronto per il deployment su Netlify! 🎉