## tehtävä x)

Tiivistelmä. Karvinen 2026: SSH public key - Login without password (https://terokarvinen.com/ssh-public-key-login-without-password/)

- Tällä sivulla kerrotaan kuinka ssh voidaan asentaa, avainpari luoda ja miten automaattinen ssh kirjautuminen voidaan konfiguroida.
- ssh asennut tapahtuu komennolla `sudo apt install ssh`
- Komennolla `sudo systemctl enable --now ssh` saa ssh daemonin käynnistymään käyttöjärjestelmän kanssa.
- ssh avain parin saa luotua komennolla `ssh-keygen`

Tiivistelmä. karvinen 2026: Hello ansible (https://terokarvinen.com/hello-ansible/)

- Tällä sivulla kerrotaan siitä miten Ansible saadaan asennettua ja miten sitä voidaan konfiguroida.
- Ansiblea käytetään eri koneiden keskitettyyn hallintaan ja se toimii ssh kautta.
- Ansiblen käyttöön liittyy erilaisia setup tiedostoja, jolla se saadaan toimimaan.
- Ansible toimii tietynlaisella kansio rakenteella.

## tehtävä a)

Latasin debian 13 version imagen ja käytin sitä debianin asennukseen virtualboxiin. valitsin virtualboxista virtuaalikoneelle 4GB ram muistia, 4 corea, ja 50GB tallennustilaa. Käytin unattended guest installationia ja laitoin käyttäjänimen ja salasanan jo virtualboxissa.

## tehtävä b)

Asensin ssh komennolla `sudo apt install ssh`

<img width="628" height="317" alt="image" src="https://github.com/user-attachments/assets/bc343fe5-d094-4b57-bbdd-7b0c402c5cea" />

Katsoin komennolla `sudo systemctl status ssh`, että ssh oli nyt päällä jonka jälkeen käytin komentoa `ssh localhost` ja laitoin seuraavaan kohtaan yes ja annoin salasanan. Tämän jälkeen olin sisällä ssh kautta.

<img width="778" height="304" alt="image" src="https://github.com/user-attachments/assets/db61328f-6129-45fd-a0c9-3af2ae5bb8e5" />

## tehtävä c)

_Käytin tähän tehtävään Teron luennolla näyttämää tapaa._

Käytin aluksi komentoa `ssh-keygen` jolla sain ssh avaimet luotua. tämän jälkeen käytin komentoa `ssh-copy-id localhost`, jolla sain ssh avaimet asetettua localhostille, niin että salasanaton kirjautuminen lähti toimimaan. Kokeilin vielä, että kaikki toimii käyttämällä komentoa `ssh localhost` uudelleen ja tällä kertaa salasanaa ei kysytty ja pääsin heti sisään.

<img width="719" height="447" alt="image" src="https://github.com/user-attachments/assets/aa5b427e-1274-4b07-9a3b-299677012ff3" />

## tehtävä d)

Käytin tätä tehtävää varten Teron artikkelia ohjeena: https://terokarvinen.com/hello-ansible/

Käytin komentoa `sudo apt install ansible -y`. Tällä komennolla sain asennettua ansiblen ja tarkastin vielä komennolla `ansible --version`

<img width="727" height="256" alt="image" src="https://github.com/user-attachments/assets/f41844d1-fdb6-4408-8e54-d15747da6999" />

Tämän jälkeen lisäsin kansion komennolla `mkdir ansible` ja loin tänne hosts.ini tiedoston microlla `micro hosts.ini` ja kirjoitin tiedostoon localhost ja tallensin sen

<img width="201" height="86" alt="image" src="https://github.com/user-attachments/assets/052e3d1a-5ae0-4955-8405-c2f6a92a6f8e" />

Kokeilin ansiblen toiminnan käyttämällä komentoa `ansible all -a 'uptime' -i hosts.ini`

<img width="736" height="182" alt="image" src="https://github.com/user-attachments/assets/674c9fc3-8b04-4000-a997-342f34789ffd" />

kuvasta voidaan nähdä, että komento toimii mutta tulee varoitus pythoniin liittyen.
Tämän varoituksen sai kuitenkin helposti pois laittamalla hosts.ini tiedostoon seuraavan pätkän 
```
[all:vars]
ansible_python_interpreter=/usr/bin/python3
```
Seuraavan kerran ajettuani komennon uudelleen varoitus ei enää tullut.

<img width="563" height="95" alt="image" src="https://github.com/user-attachments/assets/6f20318a-5aa5-4088-a8f2-2f1c5b5d0d4b" />

### Seuraavaksi tein ansiblelle sen vaatiman kansio rakenteen ja tiedostot

Komennolla `mkdir -p roles/hello/tasks` sain luotua kansiot. Tiedostoja varten käytin komentoja `touch ansible.cfg && touch site.yml` ja kansioon tasks `touch main.yml`

rakenne näyttää nyt seuraavalta.

<img width="248" height="216" alt="image" src="https://github.com/user-attachments/assets/ccc3e533-e6d7-4fa7-a61d-53870011a1a8" />

Tämän jälkeen käytin microa ja lisäsin tiedostoihin seuraavat tekstit:

### ansible.cfg
```
[defaults]
inventory = hosts.ini
```

### site.yml

```
- hosts: all
  roles::
    - hello
```

### main.yml

```
- copy
    dest: /tmp/hello-ansible
    content: "Hei Ansiblen maailma"
```

Kun nyt ajoin komennon `ansible-playbook site.yml` kaikki näytti toimivan ja tuli changed 1, eli yhtä tiedostoa on muutettu

<img width="811" height="288" alt="image" src="https://github.com/user-attachments/assets/4e6f74e7-e42e-4686-9022-1f95f45d4fe4" />

Ansiblen toiminta voidaan varmistaa käymällä katsomassa tuliko tuo tiedosto nyt haluttuun sijaintiin, eli ssh yhteys localhostiin ja `cat /tmp/hello-ansible` ja kaikki näytti olevan juuri niinkuin pitää.

<img width="828" height="233" alt="image" src="https://github.com/user-attachments/assets/7b7caf80-a43f-43bf-a295-76024ac5557d" />


## tehtävä e)

## Lähteet

Karvinen, T. 2026. Palvelinten Hallinta. Verkkosivu. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/. Luettu: 3.11.2026
Karvinen, T. 2026. Palvelinten Hallinta. Luento 29.10.2026. Haaga-Helia ammattikorkeakoulu. Helsinki
Karvinen, T. 2026. Hello Ansible. verkkosivu. Luettavissa https://terokarvinen.com/hello-ansible/. Luettu 3.11.2026
Karvinen, T. 2026. SSH public key - Login without password. Verkkosivu. Luettavissa https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu 3.11.2026
