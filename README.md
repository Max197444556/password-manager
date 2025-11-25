# 🔐 Archivio Password Sicuro

Un password manager moderno e sicuro con interfaccia glassmorphism, autenticazione utente e database cloud.

![Password Manager](https://img.shields.io/badge/Status-Live-success)
![Supabase](https://img.shields.io/badge/Database-Supabase-green)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

## ✨ Caratteristiche

- 🔐 **Autenticazione Sicura** - Login e registrazione con Supabase Auth
- ☁️ **Database Cloud** - Le tue password salvate su database PostgreSQL
- 🎨 **Design Moderno** - Interfaccia glassmorphism con animazioni fluide
- 👁️ **Privacy First** - Row Level Security: ogni utente vede solo le proprie password
- 📱 **Responsive** - Funziona su desktop, tablet e mobile
- 🗑️ **Gestione Completa** - Visualizza, copia, elimina singole password o tutto l'archivio

## 🚀 Demo Live

**[Prova l'app qui →](https://tuousername.github.io/password-manager/)**

## 🖼️ Screenshot

![App Screenshot](screenshot.png)

## 🛠️ Tecnologie Utilizzate

- **Frontend**: HTML5, CSS3 (Vanilla), JavaScript (ES6+)
- **Database**: Supabase (PostgreSQL)
- **Autenticazione**: Supabase Auth
- **Hosting**: GitHub Pages
- **Font**: Outfit (Google Fonts)
- **Icons**: Font Awesome 6

## 📦 Installazione Locale

1. **Clona il repository**
   ```bash
   git clone https://github.com/tuousername/password-manager.git
   cd password-manager
   ```

2. **Configura Supabase**
   - Crea un account su [supabase.com](https://supabase.com)
   - Crea un nuovo progetto
   - Esegui l'SQL per creare la tabella (vedi sotto)
   - Copia URL e Anon Key nel file `supabase-config.js`

3. **Apri l'app**
   ```bash
   # Basta aprire index.html nel browser
   # Oppure usa un server locale:
   npx serve
   ```

## 🗄️ Setup Database (Supabase)

Esegui questo SQL nel **SQL Editor** di Supabase:

```sql
-- Crea la tabella passwords
CREATE TABLE passwords (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE NOT NULL,
  service_name TEXT NOT NULL,
  password TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL
);

-- Abilita Row Level Security
ALTER TABLE passwords ENABLE ROW LEVEL SECURITY;

-- Policy: Gli utenti possono vedere solo le proprie password
CREATE POLICY "Users can view their own passwords"
  ON passwords FOR SELECT
  USING (auth.uid() = user_id);

-- Policy: Gli utenti possono inserire solo le proprie password
CREATE POLICY "Users can insert their own passwords"
  ON passwords FOR INSERT
  WITH CHECK (auth.uid() = user_id);

-- Policy: Gli utenti possono eliminare solo le proprie password
CREATE POLICY "Users can delete their own passwords"
  ON passwords FOR DELETE
  USING (auth.uid() = user_id);

-- Indice per performance
CREATE INDEX idx_passwords_user_id ON passwords(user_id);
```

## 🔒 Sicurezza

- ✅ **Row Level Security (RLS)** abilitata su Supabase
- ✅ Password **NON** salvate nel DOM come attributi
- ✅ Autenticazione gestita da Supabase Auth
- ✅ HTTPS obbligatorio in produzione (GitHub Pages)
- ⚠️ Le password sono salvate in **chiaro** nel database (considera crittografia lato client per maggiore sicurezza)

## 📝 Come Usare

1. **Registrati** con email e password
2. **Accedi** con le tue credenziali
3. **Salva** le tue password per vari servizi
4. **Gestisci** le password: visualizza, copia, elimina

## 🎨 Personalizzazione

Modifica le variabili CSS in `style.css`:

```css
:root {
    --bg-color: #0f172a;
    --primary-color: #38bdf8;
    --danger-color: #ef4444;
    /* ... altre variabili */
}
```

## 📄 Licenza

MIT License - Sentiti libero di usare questo progetto come preferisci!

## 🤝 Contributi

Le pull request sono benvenute! Per modifiche importanti, apri prima un issue per discutere cosa vorresti cambiare.

## 👨‍💻 Autore

Creato con ❤️ da **[Il Tuo Nome]**

---

⭐ Se ti piace questo progetto, lascia una stella su GitHub!
