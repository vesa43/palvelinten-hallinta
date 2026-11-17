## tehtävä x)

## tehtävä y)

## tehtävä a)

Asensin apachen komennolla `sudo apt install apache2`

<img width="719" height="415" alt="image" src="https://github.com/user-attachments/assets/7db4e75f-62bc-4be9-b663-61fd676579ab" />

siirryin html sivun lokaatioon eli `cd /var/www/html` ja katsoin että sieltä löytyy default sivu komennolla `micro index.html`

<img width="720" height="401" alt="image" src="https://github.com/user-attachments/assets/74a4d606-8d49-40ab-937b-f4eb8b73de17" />

kirjoitin debianin selaimeen localhost ja se näytti default sivun.

<img width="1145" height="652" alt="image" src="https://github.com/user-attachments/assets/d5d709a4-8f0e-44de-96b9-b257ca33f48b" />

## tehtävä b)

Asensin NginX komennolla `sudo apt install nginx`
Laitoin tässä kohtaa apachen taustalta pois komennolla `sudo systemctl stop apache2`
Tämän jälkeen köytin vielä komentoa `sudo systemctl reload nginx` en kuitenkaan saanut nginx default sivua näkymään vaan apachen sivu näkyi edelleen.
Tässä kohtaa selvisi, että nginx näyttää nyt localhostissa index.html tiedostoa, eikä nginx tiedostoa index.nginx-debian.html
Seuraavaksi keksin vaihtaa index.html sivun nimeä väliaikaisesti index.html2, ja tämän jälkeen sain sivun näkyviin.

<img width="656" height="282" alt="image" src="https://github.com/user-attachments/assets/23773149-66ab-41fc-8303-c81e51d1229d" />

## tehtävä c)

Aloitin tehtävän luomalla kansio rakenteen.

<img width="419" height="475" alt="image" src="https://github.com/user-attachments/assets/85524bf8-7940-456f-a98a-a325b69a20a7" />

lisäsin kansioon `roles/nginx/tasks/` tiedoston `main.yml` ja siihen seuraavana sisällön.

<img width="886" height="491" alt="image" src="https://github.com/user-attachments/assets/e007dab2-d00c-4da2-a420-688df2a7d67c" />



## tehtävä d)

## tehtävä e)
