## tehtävä x)

## tehtävä a)

Asensin tehtävää varten chrony paketin, ja testasin sen asennuksen käyttämällä komentoa `sudo systemctl status chrony`

<img width="821" height="287" alt="image" src="https://github.com/user-attachments/assets/d00200b8-d8a8-4ced-9e71-5d3a22f1bd29" />

## tehtävä b)

Jotta chrony asennus voitaisiin tehdä puhtaalta pöydältä ansiblella poistin vielä chronyn komennolla `sudo apt purge chrony`

Tämän jälkeen tein kansiot ansiblea varten komennolla `mkdir -p roles/chrony/tasks/main.yml`.
Muokkasin tiedoston näyttämään seuraavalta:

<img width="256" height="116" alt="image" src="https://github.com/user-attachments/assets/355e338c-a76a-4bcc-82e7-f205bb19be13" />

Jonka jälkeen lisäsin uuden roolin site tiedostoon ja ajoin playbookin. Viimeselle riville tuli tuon taskin kohdalle changed eli oletettavasti kaikki onnistui, mutta tarkastetaan vielä tilanne komennolla `sudo systemctl status chrony`.

<img width="827" height="309" alt="image" src="https://github.com/user-attachments/assets/4535fe10-ae39-4c8e-aee1-1c14e38d8305" />

Ja niinkuin kuvasta näkyy chrony on asennettu ja päällä.

## tehtävä c)

Tätä tehtävää varten tein chrony rooliin lisäyksinä kansiot files ja handlers.
Files kansioon lisäsin chrony.conf tiedoston jota muokkasin niin, että käytetään perus debian ntp poolin sijasta poolia osoitteesta fi.pool.ntp.org.

<img width="283" height="41" alt="image" src="https://github.com/user-attachments/assets/03267f17-c1a4-4d67-b6b2-85e148567cb9" />

Handlers kansioon loin tiedoston `main.yml`, johon kirjoitin seuraavanlaisen rakenteen:

<img width="245" height="102" alt="image" src="https://github.com/user-attachments/assets/a17e82dd-2de6-4d9b-adbb-9b398e380bad" />

Ja tämän jälkeen muokkasin `roles/chrony/tasks/main.yml` tiedostoa seuraavanlaiseksi:

<img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/a18ce065-66fb-432c-8f22-facafac88ba7" />

tämän jälkeen ajoin playbookin uudelleen ja sain seuraavanlaisen tulosteen:

<img width="400" height="166" alt="image" src="https://github.com/user-attachments/assets/b5ea11de-fdc8-43b7-be6d-e12d769ffaaf" />

eli conf tiedosto on kopioitu onnistuneesti. Tämä voidaan tarkistaa vielä katsomalla sijainnista /etc/chrony/chrony.conf tiedostosta, että oikea rivi on muuttunut. Tai vaihtoehtoisesti komennolla `chronyc -N sources` voidaan nähdä, että sourcet ovat juuri tuolta fi.pool.ntp.org

<img width="725" height="144" alt="image" src="https://github.com/user-attachments/assets/b3c4646b-5955-4884-bcc7-0160ff7f220e" />

## tehtävä d)

Jotta tilanne saadaan rikkinäiseksi käytin komentoa `sudo apt purge chrony`, joka poistaa chronyn ja sen mukana tulevat tiedostot. Ja palautin vielä alkuperäisen aikasynkronointi demonin komennolla `sudo apt install systemd-timesyncd`, jolla päästiin ihan alkutilanteeseen ennen kaikkia asennuksia.
Varmistin vielä, että chrony ei ole enää asennettuna.

<img width="467" height="52" alt="image" src="https://github.com/user-attachments/assets/59f933bf-968c-4fb1-9615-0f0d4fda9d04" />

Tämän jälkeen ajoin taas playbookin seuraavalla tuloksella:

<img width="441" height="262" alt="image" src="https://github.com/user-attachments/assets/71b4227f-d8b6-43c1-a37a-b5f94346a6bd" />

Ja vielä varmistuksena, että chrony löytyy nyt ja asetustiedosto on myös käytössä, komennot `sudo systemctl status chrony && chronyc -N sources`

<img width="837" height="613" alt="image" src="https://github.com/user-attachments/assets/334b2964-70ac-48bc-9453-0c9e029582c0" />

## tehtävä e)

Yksi tapa osoittaa, että tilanne on idempotentti, on ajaa playbook nyt muutama kerta uudelleen ja katsoa muuttuko tila vaikka ei pitäisi.
Käytin komentoa `ansible-playbook site.yml | grep -A 2 "^PLAY RECAP"`, jolla sain konsoliin tulostumaan vain rivit play recap osiosta, jotta sain yhteen kuvaan mahdutettua 3 ajokertaa:

<img width="926" height="290" alt="image" src="https://github.com/user-attachments/assets/41453344-ad0e-4fa0-ba2a-67420726a9f4" />


## Lähteet:

