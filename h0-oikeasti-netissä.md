## tehtävä x)

Aloitin tehtävän lukemalla linkatut github sivut ja tein näistä tiivistelmän

Tiiviste Niemi 2025: H4, linkki: https://github.com/AONCODES/linux-course/blob/main/h4.md

- Tekstissä kuvataan sitä miten uusi palvelin saadaan asennettua ja siihen liittyviä tärkeäitä setup komentoja.
- Alkutoimina täytyy luoda uusi käyttäjä ja siirtää .ssh kansio uudelle käyttäjälle ja asettaa sille oikeudet kuntoon
- Seuraavaksi asennetaan palomuuri sekä avataan palomuuriin reikä ssh:ta varten portille 22, komennoilla `sudo apt install ufw` ja `ufw allow 22/tcp`
- Tämän jälkeen root tili voidaan poistaa komennolla `sudo usermod --lock root`

Tiiviste Partanen 2025: Harjoitus 5: Nimekäs: a) Nimi, linkki: https://partanennn.github.io/linux-servers/practices/fifth-week.html

- Domain tarjoajia löytyy paljon mutta harjoituksessa valittiin namecheap.com sen kilpailukykyisen hinnan takia.
- Valitulta Domain sivustolta löytää useita valintoja sille, minkä päätteen sivulleen haluaa
- sivulta pystyy helposti asettamaan mihin osoitteeseen halutaan nimen osoittavan

## tehtävä a)

Asensin aluksi debianin heidän sivultaan ja valitsin debian-13.7.0-amd64-netinst.iso, ja avasin tällä imagella uuden virtuaalikoneen virtualbox sovellukseen. Asetin virtualboxin ikkunasta asetukset kuvan mukaisella tavallaja <img width="525" height="718" alt="image" src="https://github.com/user-attachments/assets/4a343459-5c62-4775-b3c1-d1336781f19b" />

Käytin virtualboxissa unattended guest installation vaihtoehtoa, joten hetken odottelun jälkeen uusi kone avautui kirjautumis ruutuun <img width="1273" height="792" alt="image" src="https://github.com/user-attachments/assets/cc9978cb-1584-40f0-af2b-10f5ea3bf70e" />

Asetin myöhemmin asetuksista keyboard välilehdeltä oikean näppäimistö asettelun käyttöön joka sopi paremmin omalle näppäimistölle <img width="619" height="210" alt="image" src="https://github.com/user-attachments/assets/4f464df0-913e-4c9e-a97f-953ba61fadca" />

## tehtävä b)

Vuokrasin virtuaali palvelimen upcloudilta tunnilla ja valitsin sille aikalailla kaikki halvimmat vaihtoehdot ja lopulliseksi hinnaksi tuli 3 euroa kuukaudessa. Valitsin serverille debian 13 asennuksen. Loin myös serveriä varten ssh avain parin komennolla `ssh-keygen` ja asetin siitä saamani public avaimen sivulle, jolla saisin myöhemmin yhteyden palvelimeen ssh:lla. 
Tässä vielä kuva serverin spekseistä <img width="845" height="204" alt="image" src="https://github.com/user-attachments/assets/9ecc507f-434f-41ee-9c7f-2b6b2f01ec69" />


## tehtävä c)

Aloitin asentamalla palomuurin, luomalla säännön jolla ssh yhteys sallitaan portista 22 ja laittamalla palomuurin päälle: <img width="734" height="235" alt="image" src="https://github.com/user-attachments/assets/499e5f23-afe3-4212-bc43-a9aadd8b2c66" />
