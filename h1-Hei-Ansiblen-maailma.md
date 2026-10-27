# H1 Tehtävät

## x) Karvinen 2026: SSH public key - Login without password

- SSH avaimella voidaan kirjautua Linux-koneeseen ilman salasanaa.
- Komennolla "ssh-keygen" luodaan julkinen ja yksityinen avain. Yksityinen avain pidetään salassa, koska sillä tunnistaudutaan palvelimelle.
- Komennolla "ssh-copy-id" kopioidaan julkinen SSH-avain palvelimelle, johon halutaan kirjautua. Avain tallennetaan käyttäjän "~/.ssh/authorized_keys" tiedostoon, jolloin palvelin voi tunnistaa vastaavalla yksityisellä avaimella kirjautuvan käyttäjän.
- SSH-yhteyden toiminta kokeillaan komennolla "ssh localhost".

Huomio: SSH-avaimet helpottavat ja nopeuttavat kirjautumista ja sopivat hyvin palvelinten hallintaan.

## Karvinen 2026: Hello Ansible

- Ansible on työkalu, jolla voidaan automatisoida Linux-palvelinten hallintaa.
- Ansiblella voidaan esimerkiksi tehdä asetuksia useille koneille ilman, että jokainen vaihe täytyy suorittaa käsin.
- Ansible käyttää SSH-yhteyttä muodostaakseen yhteyden hallittaviin koneisiin.
- Ansible-rooleilla voidaan järjestää automatisointitehtävät osiin, joissa määritellään esim. tiedostot ja toiminnot, joita koneella halutaan toteuttaa.
- Ansiblella määritellään haluttu lopputulos, jolloin sama tehtävä voidaan suorittaa uudelleen ilman muutoksia.

Huomio: Ansible on erityisen hyödyllinen silloin, kun hallittavia palvelimia on useita, koska samat asetukset voidaan toteuttaa automaattisesti.

## a) Debian 13 paikallisesti virtuaalikoneeseen

Linuxin asennuksessa hyödynsin Thomas Punnalan raportin ohjeita VirtualBoxin asetusten määrittämiseen ja Debian 13:n asentamiseen ja tein samat asiat kuin hänen raportissa.

- Virtualisointiohjelma: Oracle VirtualBox.
- Käyttöjärjestelmä: Debian 13 (amd64).
- Virtuaalikoneen RAM-muisti: 4096 MB.
- Suoritinytimet: 2.
- Virtuaalilevyn koko: 20 GB.
- Levytyyppi: VDI.
- Asennuskuva: debian-live-13.7.0-amd64-xfce.iso.

## b) Sshecrets

Asensin SSH-palvelimen komennolla "sudo apt-get -y install ssh".

Käynnistin palvelun komennolla "sudo systemctl enable --now ssh" Komennolla SSH demoni menee päälle myös jokaisella uudelleenkäynnistyksellä.
Tarkistin, että palvelu on käynnissä komennolla "sudo systemctl status ssh".
![SSH-palvelun tila](ssh-status.png)

Testasin SSH-yhteyttä komennolla "ssh localhost". Kirjautuminen onnistui Debian-käyttäjän salasanalla.
![SSH-kirjautuminen](ssh-localhost.png)
