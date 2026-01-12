# Návod na nasadenie na Vercel a prepojenie s doménou

## Krok 1: Vytvorenie účtu na Vercel

1. Prejdite na https://vercel.com
2. Kliknite na **"Sign Up"** alebo **"Log In"** ak už máte účet
3. Prihláste sa pomocou GitHub účtu (odporúčané, pretože máte projekt na GitHub)

## Krok 2: Import projektu z GitHub

1. Po prihlásení kliknite na **"Add New..."** → **"Project"**
2. V sekcii **"Import Git Repository"** nájdite alebo vyhľadajte **"websolution4you/LeutschauCafeStartPage"**
3. Kliknite na **"Import"**

## Krok 3: Konfigurácia projektu

1. V sekcii **"Configure Project"**:
   - **Project Name**: `leutschau-cafe` (alebo akýkoľvek názov)
   - **Framework Preset**: Vyberte **"Other"** alebo **"Static HTML"**
   - **Root Directory**: Ponechajte prázdne (`.`)
   - **Build Command**: Ponechajte prázdne (statický web nepotrebuje build)
   - **Output Directory**: Ponechajte prázdne alebo zadajte `.`

2. Kliknite na **"Deploy"**

## Krok 4: Čakanie na nasadenie

- Vercel automaticky nasadí váš projekt
- Po dokončení (cca 1-2 minúty) uvidíte URL typu: `leutschau-cafe.vercel.app`
- Kliknite na tento odkaz a overte, že stránka funguje

## Krok 5: Pridanie vlastnej domény

1. V dashboarde Vercel kliknite na váš projekt
2. Prejdite do sekcie **"Settings"** → **"Domains"**
3. Kliknite na **"Add Domain"**
4. Zadajte: `www.leutschau.sk`
5. Kliknite na **"Add"**

## Krok 6: Konfigurácia DNS na WebSupport

Vercel vám zobrazí DNS záznamy, ktoré musíte pridať na WebSupport:

### Možnosť A: CNAME záznam (odporúčané)
1. Prihláste sa do WebSupport administrácie
2. Prejdite do **DNS nastavení** pre doménu `leutschau.sk`
3. Pridajte CNAME záznam:
   - **Názov**: `www`
   - **Typ**: `CNAME`
   - **Hodnota**: `cname.vercel-dns.com` (alebo hodnotu, ktorú vám Vercel poskytne)
   - **TTL**: `3600` (alebo predvolené)

### Možnosť B: A záznam (ak CNAME nie je podporovaný)
1. V WebSupport DNS nastaveniach pridajte A záznam:
   - **Názov**: `www`
   - **Typ**: `A`
   - **Hodnota**: IP adresu, ktorú vám poskytne Vercel (zvyčajne `76.76.21.21`)
   - **TTL**: `3600`

## Krok 7: Overenie a aktivácia

1. Po pridaní DNS záznamov počkajte 5-60 minút na propagáciu DNS
2. Vercel automaticky overí doménu a aktivuje SSL certifikát
3. Keď bude doména overená, uvidíte zelenú značku v sekcii Domains
4. Vaša stránka bude dostupná na `www.leutschau.sk`

## Krok 8: (Voliteľné) Pridanie root domény

Ak chcete, aby fungovala aj `leutschau.sk` (bez www):

1. V Vercel pridajte aj doménu `leutschau.sk` (bez www)
2. V WebSupport pridajte A záznam:
   - **Názov**: `@` alebo prázdne
   - **Typ**: `A`
   - **Hodnota**: IP adresu od Vercel (`76.76.21.21`)
   - **TTL**: `3600`

## Poznámky

- DNS zmeny môžu trvať až 48 hodín, ale zvyčajne sú aktívne do 1 hodiny
- Vercel automaticky poskytuje SSL certifikát (HTTPS)
- Všetky budúce pushy na GitHub automaticky nasadia novú verziu na Vercel
- Vercel je zadarmo pre osobné projekty

## Riešenie problémov

**Doména sa neoveruje:**
- Skontrolujte, či sú DNS záznamy správne nastavené
- Počkajte na propagáciu DNS (môže trvať až 48 hodín)
- Skontrolujte, či hodnoty v DNS zodpovedajú tým, ktoré poskytol Vercel

**Stránka sa nezobrazuje:**
- Overte, či je doména overená v Vercel dashboarde
- Skontrolujte DNS záznamy pomocou nástroja ako `nslookup` alebo `dig`
