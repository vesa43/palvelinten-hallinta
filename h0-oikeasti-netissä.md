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

Ennen kuin pääsin aloittamaan tehtävän tajusin, että olin tehnyt ssh avainparin läppärillä koulussa ja halusin saada yhteyden serveriin omalta kotikoneelta, jolla ei tietysti ollut aiemmin luotua private avainta. Päätin ratkoa ongelman luomalla uuden parin kotikoneella, ja syöttää saatu public avain authorized_keys tiedostoon ssh yhteydellä. tämä kävi helposti käyttämällä komentoa `echo "Oma public key" >> ~/.ssh/authorized_keys`. Tämän jälkeen sain otettua toiselta koneelta yhteyden ssh kautta ja pääsin itse tehtävään käsiksi.

Aloitin tehtävän asentamalla palomuurin, luomalla säännön jolla ssh yhteys sallitaan portista 22 ja laittamalla palomuurin päälle. Tässä kuva jälkeen päin annetuista komennoista 

<img width="734" height="235" alt="image" src="https://github.com/user-attachments/assets/499e5f23-afe3-4212-bc43-a9aadd8b2c66" />


Seuraavaksi tein käyttäjän komennolla `sudo adduser vesa` ja käytin komentoa `sudo adduser vesa sudo`, jolloin käyttäjä myös lisättiin sudo listaan eli se saa sudo oikeudet.

Seuraavan kopioin .ssh kansion sisältöineen juuri luodulle käyttäjälle "vesa" komennolla `cp -R .ssh /home/vesa/.ssh`. tarkistin vielä että haluttu tulos saatiin aikaseksi.

<img width="541" height="232" alt="image" src="https://github.com/user-attachments/assets/e7b0cbc5-4e65-492f-8e9e-346997caa0f9" />

Tämän jälkeen käytin komentoja `chmod 700 /home/vesa/.ssh` ja `chmod 600 /home/vesa/.ssh/authorized_keys`, joilla asetettiin oikeudet oikeiksi. Ja vielä viimeiksi vaihdoin kansion omistajuuden uudelle käyttäjälle komennolla `chown -R vesa:vesa /home/vesa/.ssh`.

Lopuksi vielä testasin että kaikki toimii kirjatumalla uudelle käyttäjälle sekä ajamalla yhden sudo komennon, jotta sekin varmasti toimii.

<img width="1034" height="466" alt="image" src="https://github.com/user-attachments/assets/68853027-a40b-42f3-923b-7a2047c137d7" />

Tämän jälkeen käytin komentoa `sudo usermod --lock root` jolla salasana kirjautuminen root käyttäjälle pystyttiin disabloimaan, sekä vaihdoin config tiedostosta kohdan "PermitRootLogin yes -> no" .

## tehtävä d)

Asensin tätä tehtävää varten apache2 paketin komennolla `sudo apt install apache2`. Muuta ei oikeastaan tarvinnut tehdä apache meni suoraan päälle ja sen löysi kirjoittamalla selaimeen "http://palvelimen_ip", ja seuraava default apache sivu ponnahti näytölle <img width="1016" height="920" alt="image" src="https://github.com/user-attachments/assets/caa8931f-5f8c-482e-a04d-488e545533d8" />
