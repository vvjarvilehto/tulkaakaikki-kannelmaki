# Käyttöönotto-ohje (pääylläpitäjälle)

Sivusto on Jekyll-sivusto, jonka GitHub Pages rakentaa automaattisesti. Sisältöä muokataan hallintapaneelista (Sveltia CMS) osoitteessa `…/admin/`.

## 1. Julkaise sivusto GitHub Pagesissa

1. Avaa repositorio GitHubissa → **Settings → Pages**.
2. Kohdassa *Build and deployment* valitse **Source: Deploy from a branch**, **Branch: main**, kansio **/ (root)** ja paina **Save**.
3. Odota 1–2 minuuttia. Sivu näkyy osoitteessa
   `https://vvjarvilehto.github.io/tulkaakaikki-kannelmaki/`

Rakennuksen tilan näet repositorion **Actions**-välilehdeltä.

## 2. Kirjaudu hallintapaneeliin

1. Avaa `https://vvjarvilehto.github.io/tulkaakaikki-kannelmaki/admin/`
2. Valitse **Kirjaudu sisään access tokenilla**.
3. Tee tunniste GitHubissa: **Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token (classic)**.
   - *Note*: `Tulkaa kaikki -sivusto`
   - *Expiration*: esim. 90 päivää
   - Rasti kohtaan **public_repo** (ei muita)
4. Kopioi tunniste ja liitä se hallintapaneeliin. Tunniste näytetään vain kerran.

Tunniste on kuin salasana: älä lähetä sitä kenellekään.

## 3. Lisää ylläpitäjiä (luvitus)

1. Uusi ylläpitäjä tekee itselleen ilmaisen tunnuksen osoitteessa github.com.
2. Repositoriossa: **Settings → Collaborators → Add people** ja hänen GitHub-tunnuksensa.
3. Hän hyväksyy kutsun sähköpostista ja tekee itselleen tunnisteen kohdan 2 ohjeella.
4. Anna hänelle tiedosto `OHJE-YLLAPITAJILLE.md`.

**Oikeuden poisto:** Settings → Collaborators → Remove. Pääsy hallintapaneeliin loppuu heti.

Jokainen muutos tallentuu historiaan: näet kuka muutti mitä (**Commits**-näkymä), ja minkä tahansa muutoksen voi perua.

## 4. Oma domain (kun testi on onnistunut)

1. Osta domain Domainhotellista.
2. GitHubissa: **Settings → Pages → Custom domain** → kirjoita `www.oma-domain.fi` → Save. Rastita myöhemmin **Enforce HTTPS**.
3. Domainhotellin DNS-asetuksiin:
   - `www` **CNAME** → `vvjarvilehto.github.io`
   - paljas domain (`@`) **A**-tietueet: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   (tarkista ajantasaiset arvot GitHubin ohjeesta *Managing a custom domain for your GitHub Pages site*)
4. Vaihda tiedostossa `_config.yml` rivi `baseurl: /tulkaakaikki-kannelmaki` muotoon `baseurl: ""`.
5. Vaihda tiedostossa `admin/config.yml` `site_url` uudeksi osoitteeksi.

## 5. Helpompi kirjautuminen (valinnainen)

Tunnisteen tekeminen on ylläpitäjille hieman kömpelöä. "Kirjaudu GitHubilla" -napin saa käyttöön ilmaisella
[Sveltia CMS Authenticator](https://github.com/sveltia/sveltia-cms-auth) -palvelulla (Cloudflare Workers):

1. Asenna Authenticator sen ohjeen mukaan ja tee GitHubiin OAuth App.
2. Lisää `admin/config.yml`:n `backend`-kohtaan `base_url: https://<workerin-osoite>` ja poista rivi `auth_methods: [token]`.
