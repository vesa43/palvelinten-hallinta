## tehtävä x)

Tiivistelmä. Karvinen 2026: Sudo without password (https://terokarvinen.com/passwordless-sudo/)
- Tässä tekstissä kerrotaan kuinka saadaan tehtyä uusi käyttäjä, joka ei tarvitse sudon käyttämiseen salasanaa.
- visudo komennolla voidaan muokata joitain tärkeitä konfiguraatio tiedostoja ilman, että ne menevät rikki.


Tiivistelmä. Karvinen 2026: Passwordless Sudo with Ansible (https://terokarvinen.com/passwordless-sudo-with-ansible/)
- Tässä tektissä kerrotaan miten voidaan luoda käyttäjä, jolla voi käyttää sudoa ilman salasanaa ansiblea varten.
- Ensimmäisellä kerralla pitää käyttää -K lippua, jotta ohjelma osaa kysyä sudo salasanaa, jotta käyttäjä voidaan luoda.

## tehtävä a)

Etenin tässä tehtävässä teron ohjeiden mukaisesti (https://terokarvinen.com/passwordless-sudo/)

Aluksi loin käyttäjän `anvesa` ja ryhmän `sudoless`, komennoilla `sudo adduser anvesa` ja `sudo addgroup sudoless`.

<img width="472" height="270" alt="image" src="https://github.com/user-attachments/assets/7b83caf1-6fa1-44a7-a2ca-b35386c8945a" />

Tämän jälkeen vielä lisäsin uuden käyttäjän luotuun ryhmään komennolla `sudo adduser anvesa sudoless`.
Sen jälkeen käytin komentoa `sudo visudo /etc/sudoers.d/sudoless`, ja lisäsin tähän uuteen sääntöön komennon jolla käyttäjä voi käyttää sudoa ilman salasanaa `%sudoless ALL = (ALL) NOPASSWD: ALL`.

<img width="448" height="76" alt="image" src="https://github.com/user-attachments/assets/0c97f88e-d39e-493a-a5af-454a0715f5ac" />

Testasin vielä, että käyttäjä pystyy nyt käyttämään sudoa ilman salasanaa ottamalla ssh yhteyden `ssh anvesa@localhost`, ja tämän jälkeen `sudo echo "toimiiko?"`.

<img width="729" height="269" alt="image" src="https://github.com/user-attachments/assets/d9058776-4d59-4cc6-b0b0-0a71bcbd5203" />

Ja niin kuin kuvasta näkyy sudo komento ei kysynyt salasanaa joten kaikki näyttää toimivan.

## tehtävä b)

Aloitin tehtävän luomalla uuden roolin ansiblelle mihin laitoin uuden tiedoston nimellä `main.yml`.

Tämän jälkeen muokkasin `main.yml` tiedoston seuraavanlaiseksi 

```yaml
- group:
    name: "sudoless"
    state: present
- user:
    name: "anvesa"
    state: present
    groups: ["sudoless", "sudo", "adm"]
- authorized_key:
    user: "anvesa"
    key: "oma public key"
- copy:
    dest: "/etc/sudoers.d/sudoless"
    content: "%sudoless ALL = (ALL) NOPASSWD: ALL\n"
    owner: "root"
    group: "root"
    mode: "0644"
```

Muokkasin vielä `site.yml` tiedoston sisältämään uuden roolin 

<img width="216" height="123" alt="image" src="https://github.com/user-attachments/assets/cafa8746-c85e-492d-a922-b9a03c359c83" />

Ajoin tiedoston komennolla `ansible-playbook site.yml -K`.
Tämän jälkeen yritin ajaa komentoa uudelleen ilman `-K` lippua, mutta tässä kohtaa tuli ongelma, että sudo salasana tarvitaan. 
Kysyin vähän kaverilta neuvoa ja pohdin hänen kanssaan, miten Tero oli tunnilla saanut sen toimimaan ilman lippua. Tajusimme lopulta, että hosts.ini tiedostoon täytyi laittaa pelkän localhostin sijasta tuo uusi käyttäjä eli omassa tapauksessa `anvesa@localhost`.
Kun olin muokannut tiedoston ajoin komentoa pari kertaa uudelleen ilman lippua ja kaikki näytti nyt toimivan.

<img width="841" height="416" alt="image" src="https://github.com/user-attachments/assets/5bebf47a-9da0-4bd0-b9ea-2719087ee824" />

## tehtävä c)

Tätä tehtävää varten selailin esimerkkejä, joita löytyi komennolla `ansible-doc apt`.

Muokkasin uuden roolin `main.yml` tiedostoa niin, että se sisältää paketit tree ja curl ja lisäsin vielä option update_cache, joka doc:in mukaan päivittää paketti listauksen samalla tavalla kuin `sudo apt update` tekisi.

<img width="302" height="154" alt="image" src="https://github.com/user-attachments/assets/3dd8076d-7db8-4dd3-a729-9ef08a64888a" />

Ajoin tämän jälkeen `site.yml`, johon olin lisännyt tämän uuden roolin ja kaikki toimi ja paketit asennettiin onnistuneesti.

## tehtävä d)

Loin uuden roolin nimeltä file ja sen `site.yml` tiedostoon kirjoitin seuraavat asiat:

```yaml
- name: "Monirivinen tiedosto"
  copy:
    dest: "/etc/salainen.txt"
    content: |
      Tämä on ensimmäinen rivi.
      Tässä toinen rivi.
      Ja kolmas rivi.
    owner: "anvesa"
    group: "sudoless"
    mode: "0700"
```

Ja lisäsin tämän roolin taas `site.yml` tiedostoon, ja ajoin komennolla `ansible-playbook site.yml`.
Kaikki meni läpi ja tiedosto saatiin onnistuneesti luotua.

<img width="455" height="146" alt="image" src="https://github.com/user-attachments/assets/74b8d2d6-a89b-4ebd-9e53-3fe8aa79106f" />

`main.yml` tiedostossa käytetyt oikeudet (`mode: "0700"`) tarkoittaa sitä, että pelkästään omistajalla on kaikki oikeudet eli read, write ja execute, mutta muilla käyttäjillä ei ole oikeuksia. Tämän myös voi huomata aikasemmasta kuvasta kun laitoin aluksi ilman sudoa `cat /etc/salainen.txt`, tuli vastaan virhe että ei ole permejä. Kun taas käytin sudoa sain luettua tiedoston. Oikeudet numeerisesti voi laskea yhteen eli 4 = read, 2 = write ja 1 = execute. Tässä tapauksessa oli käytössä 7 eli 4+2+1 = 7. Ja missä kohtaa oikeudet täytyy olla numeroissa? Ensimmäinen numero koskee omistajaa, seuraava koskee ryhmää ja viimeinen koskee kaikkia.

## tehtävä e)



## tehtävä f)
