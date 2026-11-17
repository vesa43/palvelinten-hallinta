## tehtävä x)

## tehtävä y)

## tehtävä a)

Asensin apachen komennolla `sudo apt install apache2`

<img width="719" height="415" alt="image" src="https://github.com/user-attachments/assets/7db4e75f-62bc-4be9-b663-61fd676579ab" />

siirryin html sivun lokaatioon eli `cd /var/www/html` ja katsoin että sieltä löytyy default sivu komennolla `micro index.html`

<img width="720" height="401" alt="image" src="https://github.com/user-attachments/assets/74a4d606-8d49-40ab-937b-f4eb8b73de17" />

kirjoitin debianin selaimeen localhost ja se näytti default sivun.

<img width="1145" height="652" alt="image" src="https://github.com/user-attachments/assets/d5d709a4-8f0e-44de-96b9-b257ca33f48b" />

Jotta peruskäyttäjä voi muokata sivua pitää sivun tiedostolla olla oikeudet asetettu oikein eli `sudo chmod 777 index.html`

## tehtävä b)

Asensin NginX komennolla `sudo apt install nginx`
Laitoin tässä kohtaa apachen taustalta pois komennolla `sudo systemctl stop apache2`
Tämän jälkeen köytin vielä komentoa `sudo systemctl reload nginx` en kuitenkaan saanut nginx default sivua näkymään vaan apachen sivu näkyi edelleen.
Tässä kohtaa selvisi, että nginx näyttää nyt localhostissa index.html tiedostoa, eikä nginx tiedostoa index.nginx-debian.html
Seuraavaksi keksin vaihtaa index.html sivun nimeä väliaikaisesti index.html2, ja tämän jälkeen sain sivun näkyviin.

<img width="656" height="282" alt="image" src="https://github.com/user-attachments/assets/23773149-66ab-41fc-8303-c81e51d1229d" />

Jotta oikeudet taas saadaan asetettua `sudo chmod 777 index.nginx-debian.html`

## tehtävä c)

Aloitin tehtävän luomalla kansio rakenteen.

<img width="419" height="475" alt="image" src="https://github.com/user-attachments/assets/85524bf8-7940-456f-a98a-a325b69a20a7" />

Lisäsin kansioon `roles/nginx/tasks/` tiedoston `main.yml` ja siihen seuraavana sisällön.

<img width="337" height="548" alt="image" src="https://github.com/user-attachments/assets/6cc1f1ef-5478-466c-a00f-dd040b216bbd" />

"Luodaan index.html" kohdassa kansioon lisätään index.html ja sille annetaan group www-data, jotta nginx pystyy käyttämään sitä, mutta tavallaan oikeuksien ollessa 777 kaikilla on jo muutenkin oikeudet.

Lisäsin vielä lopuksi `site.yml` tiedostoon uuden roolin `nginx`.
Kun uusi rooli ajettiin komennolla `ansible-playbook site.yml` kaikki näytti tulosteen mukaan oikein.

<img width="807" height="366" alt="image" src="https://github.com/user-attachments/assets/48ae05a7-5800-437c-8c20-a8559f9972f5" />

varmistetaan vielä että kaikki meni niin kuin piti eli kansioista `var/www/html/` löytyy oikeat tiedostot ja oikeudet on oikein asetettu.

<img width="534" height="110" alt="image" src="https://github.com/user-attachments/assets/315fa09b-b179-439b-ab6a-c1c9af7d0d50" />

Ja vielä että testisivu nökyy selaimessa

<img width="551" height="292" alt="image" src="https://github.com/user-attachments/assets/8e042976-b274-414f-a74a-ad393bff3c0c" />



## tehtävä d)

## tehtävä e)
