---
title: Palvelukartan upotusohjeet
layout: post
---

Palvelukartan yksittäisiä näkymiä voi upottaa osaksi mitä tahansa
verkkosivua.

# Upotustyökalu

Yksittäiset upotukset on helpointa tehdä Palvelukartan upotustyökalun
avulla. Kun kartta on haluamassasi näkymässä, klikkaa kartan oikeassa
alakulmassa olevaa nappia jossa on upotuskoodin kaltainen kuvake
</>. Pääset esikatselemaan, miltä äskeisen näkymän upotettu versio
näyttäisi. Voit myös säätää upotuksen kokoa ja muita
asetuksia. Lopuksi voit kopioida sivun alalaidassa olevan upotuskoodin
osaksi haluamaasi sivua.

Pääkaupunkiseudun palvelukartta on osoitteessa
[http://palvelukartta.hel.fi](http://palvelukartta.hel.fi). Ruotsinkielinen
versio palvelukartasta löytyy osoitteesta [http://servicekarta.hel.fi](http://servicekarta.hel.fi) ja
englanninkielinen osoitteesta [http://servicemap.hel.fi](http://servicemap.hel.fi).

# Upotusnäkymien osoitteet

Jos on tarvetta luoda automaattisesti useita upotusnäkymiä eri
kriteereillä, kuvaamme seuraavaksi eri upotusnäkymien
URL-osoitteiden muodon ja parametrit eri näkymille. Mallia
upotuskoodin iframen laatimiseen voi ottaa Palvelukartanupotustyökalun
upotuskoodista.

## Upotuksen kieli

Upotuksen kieli määräytyy sen osoitteen subdomainin mukaan, kuten
itse palvelukartallakin. Suomenkieliset upotusosoitteet alkavat siis
 `http://palvelukartta.hel.fi/embed/`, ruotsinkieliset
 `http://servicekarta.hel.fi/embed/` ja englanninkieliset
 `http://servicemap.hel.fi/embed/`

## Yleiset parametrit

Kaikissa upotusnäkymissä voi käyttää seuraavia valinnaisia
query-parametreja URL-osoittessa.

|  Parametri | Oletusarvo | Kuvaus | Arvot | |
|------------|-------------|----------|--------|--|
| `map`      |  `servicemap` | taustakartta | `servicemap` | palvelukartta | 
|            |             |             | `accessible_map` | suurikontrastinen kartta |
|            |             |             | `ortographic` | ortografinen ilmakuva |

Niissä upotusnäkymissä, joissa URL-osoite ei muulla tavoin
määrää näytettäviä toimipisteitä, voidaan lisäksi käyttää
seuraavaa parametria.

| Parametri | Oletusarvo | Kuvaus | Arvot | |
|----------|-------|----------|--------|---|
| `level`    | `none`  | mitä toimipisteitä näytetään | `all` | kaikki |
|     |   | | `none` | ei mitään |
|     |   | | `common` | yleisimmät julkiset palvelut |

Arvoa `all` kannattaa välttää, sillä erilaisia toimipisteitä
tulee helposti kartalle liikaa. Yleisimmät julkiset palvelut
ovat koulut, terveysasemat ja päiväkodit.

Jos haluaa tehdä mielivaltaisen karttarajauksen, siihen
voi käyttää bbox-parametria, joka määrittää koordinaatteina
halutun alueen kartalla, jonka pitää näkyä upotuksessa.
_Parametri toimii vain näkymissä, joihin ei ole valittu
näkyviin katuosoitetta, toimipistettä tai palveluita. Jos
joku näistä on valittu, kartan rajaus mukautuu valittuihin
sisältöihin._

|  Parametri | Oletusarvo | Kuvaus | Arvot | |
|------------|-------------|----------|--------|--|
| `bbox`     |  -    | kartan rajat WGS-koordinaatteina, esim. 60.14294,24.83800,60.20365,24.99757 |  |


`bbox`-parametrin karttarajaus tulkitaan niin, että
upotuksen on pidettävä sisällään _vähintään_ määritellyt
parametrit, mutta upotuksen koosta ja muodosta riippuen
se voi sisältää laajemmankin alueen.


## Näkymät

Seuraavassa kuvataan tiiviisti eri näkymien osoitteiden rakenne.
Rakenne on sama kuin itse palvelukartan URL-osoitteissa.
Palvelukartan osoitteesta saadaan upotusosoite lisäämällä
osoitteeseen `hel.fi` -merkkijonon jälkeen merkkijono `/embed`.
Helpoiten osoitteita voi siis kokeilla palvelukartan
käyttöliittymässä tai upotustyökalussa.

### Yksittäinen toimipiste

    http://palvelukartta.hel.fi/embed/unit/:id

`:id` on toimipisteen tunnus.

### Toimipisteet, jotka tarjoavat tiettyjä palveluita

    http://palvelukartta.hel.fi/embed/unit?service=:id

`:id` on palvelun tunnus.

### Kaupunginosan toimipisteet

    http://palvelukartta.hel.fi/embed/division/:municipality/:id

tai

    http://palvelukartta.hel.fi/embed/division?ocd_id=:ocd_ids

`:municipality` voi tällä hetkellä olla vain `helsinki`.
`:id` on muotoa `kaupunginosa:KAUPUNGINOSAN_NIMI`. Jälkimmäinen
muoto tukee pilkulla eroteltuna useaa kaupunginosaa, esimerkiksi
`helsinki%2Fkaupunginosa:kallio,helsinki%2Fkaupunginosa:sörnäinen`.

### Tekstihaku

    http://palvelukartta.hel.fi/embed/search?q=:hakutermi

`:hakutermi` on vapaatekstihaun parametri.

### Katuosoite

    http://palvelukartta.hel.fi/address/:municipality/:street/:number

`:municipality` on kunta, `:street` kadunnimi ja `:number` osoitteen
numero-osa.

