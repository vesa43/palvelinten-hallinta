## tehtävä x)

Tiivistelmä. Karvinen 2026: SSH public key - Login without password (https://terokarvinen.com/ssh-public-key-login-without-password/)

- Tällä sivulla kerrotaan kuinka ssh voidaan asentaa, avainpari luoda ja miten automaattinen ssh kirjautuminen voidaan konfiguroida.
- ssh asennut tapahtuu komennolla `sudo apt install ssh`
- Komennolla `sudo systemctl enable --now ssh` saa ssh daemonin käynnistymään käyttöjärjestelmän kanssa.
- ssh avain parin saa luotua komennolla `ssh-keygen`

Tiivistelmä. karvinen 2026: Hello ansible (https://terokarvinen.com/hello-ansible/)

- Tällä sivulla kerrotaan siitä miten Ansible saadaan asennettua ja miten sitä voidaan konfiguroida.
- Ansiblea käytetään eri koneiden keskitettyyn hallintaan ja se toimii ssh kautta.
- 

## tehtävä a)

Latasin debian 13 version imagen ja käytin sitä debianin asennukseen virtualboxiin. valitsin virtualboxista virtuaalikoneelle 4GB ram muistia, 4 corea, ja 50GB tallennustilaa. Käytin unattended guest installationia ja laitoin käyttäjänimen ja salasanan jo virtualboxissa.

## tehtävä b)

Asensin ssh komennolla `sudo apt install ssh`

<img width="628" height="317" alt="image" src="https://github.com/user-attachments/assets/bc343fe5-d094-4b57-bbdd-7b0c402c5cea" />

Katsoin komennolla `sudo systemctl status ssh`, että ssh oli nyt päällä jonka jälkeen käytin komentoa `ssh localhost` ja laitoin seuraavaan kohtaan yes ja annoin salasanan. Tämän jälkeen olin sisällä ssh kautta.

<img width="778" height="304" alt="image" src="https://github.com/user-attachments/assets/db61328f-6129-45fd-a0c9-3af2ae5bb8e5" />

## tehtävä c)

Käytin aluksi komentoa `ssh-keygen` jolla sain ssh avaimet luotua. tämän jälkeen käytin komentoa `ssh-copy-id localhost`, jolla sain ssh avaimet asetettua localhostille, niin että salasanaton kirjautuminen lähti toimimaan. Kokeilin vielä, että kaikki toimii käyttämällä komentoa `ssh localhost` uudelleen ja tällä kertaa salasanaa ei kysytty ja pääsin heti sisään.

<img width="719" height="447" alt="image" src="https://github.com/user-attachments/assets/aa5b427e-1274-4b07-9a3b-299677012ff3" />


## tehtävä d)

## tehtävä e)

