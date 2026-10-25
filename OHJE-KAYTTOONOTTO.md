# Käyttöönotto-ohje (pääylläpitäjälle)

Sivusto on Jekyll-sivusto, jonka GitHub Pages rakentaa automaattisesti. Sisältöä muokataan Pages CMS -hallintapaneelista (app.pagescms.org). GitHub-käyttäjille on lisäksi Sveltia CMS osoitteessa `…/admin/`.

## 1. Julkaise sivusto GitHub Pagesissa

1. Avaa repositorio GitHubissa → **Settings → Pages**.
2. Kohdassa *Build and deployment* valitse **Source: Deploy from a branch**, **Branch: main**, kansio **/ (root)** ja paina **Save**.
3. Odota 1–2 minuuttia. Sivu näkyy osoitteessa
   `https://tulkaakaikkikannelmaki.fi/`

Julkaisun etenemisen näet repositorion **Actions**-välilehdeltä.

## 2. Hallintapaneeli: Pages CMS (ylläpitäjät ilman GitHub-tunnusta)

Ylläpitäjät kirjautuvat **app.pagescms.org**-palveluun sähköpostiosoitteellaan. GitHub-tunnusta ei tarvita.

**Käyttöönotto (kerran, sinä):**
1. Avaa **https://app.pagescms.org** ja kirjaudu GitHub-tunnuksellasi.
2. Asenna Pages CMS -sovellus GitHubiin, kun palvelu pyytää. Valitse *Only select repositories* → `tulkaakaikki-kannelmaki`.
3. Avaa repositorio Pages CMS:ssä. Vasemmalla näkyvät **Ehdokkaat** ja **Sivuston tekstit** (asetukset ovat tiedostossa `.pages.yml`).

**Ylläpitäjän lisääminen:**
1. Pages CMS:ssä valitse repositorio → **Collaborators**.
2. Kirjoita ylläpitäjän sähköpostiosoite ja lähetä kutsu.
3. Ylläpitäjä saa sähköpostin, avaa linkin ja kirjautuu sähköpostiin tulevalla koodilla.

**Oikeuden poisto:** samasta Collaborators-näkymästä.

Kaikki muutokset tallentuvat GitHubiin kuten ennenkin, joten historia ja palautukset toimivat.

## 3. Vaihtoehtoinen hallintapaneeli GitHub-käyttäjille (Sveltia CMS)

Jos ylläpitäjällä on GitHub-tunnus, hän voi käyttää myös osoitetta `https://tulkaakaikkikannelmaki.fi/admin/`.

1. Lisää hänet repositorioon: **Settings → Collaborators → Add people**.
2. Hän tekee tunnisteen: **Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token (classic)**, rasti vain kohtaan **public_repo**.
3. Hallintapaneelissa valitaan **Kirjaudu sisään access tokenilla** ja liitetään tunniste.

Tunniste on kuin salasana: sitä ei lähetetä kenellekään.

## 4. Oma domain

Sivusto on osoitteessa **tulkaakaikkikannelmaki.fi**. Domainin nimi on tiedostossa `CNAME`, ja `_config.yml`:ssä `baseurl` on tyhjä.

Domainhotellin DNS-asetukset:
- pelkkä domain (`@`), **A**-tietueet: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `www` **CNAME** → `vvjarvilehto.github.io`

GitHubissa **Settings → Pages → Custom domain** on `tulkaakaikkikannelmaki.fi`, ja **Enforce HTTPS** on rastitettu. Osoite `www.tulkaakaikkikannelmaki.fi` ja vanha `vvjarvilehto.github.io/tulkaakaikki-kannelmaki/` ohjautuvat automaattisesti uuteen osoitteeseen.

## 5. Sveltian helpompi kirjautuminen (valinnainen)

"Kirjaudu GitHubilla" -napin saa käyttöön ilmaisella
[Sveltia CMS Authenticator](https://github.com/sveltia/sveltia-cms-auth) -palvelulla (Cloudflare Workers):

1. Asenna Authenticator sen ohjeen mukaan ja tee GitHubiin OAuth App.
2. Lisää `admin/config.yml`:n `backend`-kohtaan `base_url: https://<workerin-osoite>` ja poista rivi `auth_methods: [token]`.
