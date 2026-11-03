# H2 Tehtävät

## x) Karvinen 2026: Sudo without password

- Sudo ilman salasanaa mahdollistaa komentojen suorittamisen pääkäyttäjän oikeuksilla.
- Salasanaton sudo määritetään luomalla lisäämällä käyttäjä käyttäjäryhmään "sudoless". Tämän jälkeen luodaan uusi sudoers-sääntö komennolla ```sudo visudo /etc/sudoers.d/sudoless.```
- Sudoers tiedostoon lisätään ```%sudoless ALL = (ALL) NOPASSWD: ALL```. Tämä komento sallii ryhmän jäsenille kaikkien komentojen suorittamisen ilman salasanaa.
- Toimivuus kokeillaan kirjautumalla ulos, uudelleen sisään ja suorittamalla jokin sudo-komento.
- ```sudo -k``` poistaa aiemmin tallennetut kirjautumistiedot.

Kysymys: Mitä riskejä salasanattomasta sudon käytöstä aiheutuu, jos käyttäjätili joutuu ulkopuolisen haltuun?

## Munroe 2006: xkcd 149: Sandwich

- Sarjakuvassa henkilö pyytää toista tekemään hänelle voileivän. Kun toinen kieltäytyy, ensimmäinen lisää pyyntöön sanan sudo, minkä jälkeen toinen suostuu.
- Huumori perustuu sudoon, jolla voidaan suorittaa komentoja pääkäyttäjän oikeuksilla.

## Karvinen 2026: Passwordless Sudo with Ansible

- Artikkelissa esitellään Ansibleen tehty Antero-rooli, jolla automatisoidaan salasanattoman sudon käyttöönotto. Rooli luo uuden käyttäjän sudoless ryhmään.
- Ennen automatisointia kannattaa aina kokeilla ensin manuaalisesti.
- Main.yml:iin lisätään group-, user-, authorized_key- ja copy kohdat. Niillä luodaan ryhmä ja käyttäjä, lisätään SSH-avain ja luodaan sudoers-tiedosto.
- Ensimmäisellä ajokerralla tarvitaan sudo-oikeudet. Tämä toteutetaan lisäämällä ```become: true``` site.yml tiedostoon.

Kysymys: Miten salasanaton sudo voidaan ottaa käyttöön Ansiblella usealla palvelimella samaan aikaan?

## Ansible-doc

### Ansible-doc copy

- Voi kopioida tiedostoja tai hakemistorakenteita paikalliselta tai etäkoneelta kohdekoneelle.
- Voi määrittää tiedostojen ja hakemistojen käyttöoikeuksia ja omistajuutta.

#### Content
- Määrittää tiedoston sisällön. Toimii vain, kun ```dest``` osoittaa tiedostoon. Luo tiedoston, jos sitä ei vielä ole olemassa.

#### Dest
- Määrittää kohteen polun, johon tiedosto kopioidaan.

#### Src
- Määrittää kopioitavan tiedoston tai hakemiston.

#### Owner
- Määrittää käyttäjän, joka omistaa tiedoston tai tiedostojärjestelmän.
- Jos asetusta ei käytetä, käyttää nykyistä käyttäjää.

#### Group
- Määrittää ryhmän, jolle tiedosto tai tiedostojärjestelmän kohde kuuluu.
- Jos asetusta ei käytetä, käytetään nykyisen käyttäjän ryhmää.

#### Mode
- Määrittää tiedoston tai hakemiston käyttöoikeudet.
- Oikeudet voidaan määrittää oktaalilukuina, kuten 0644 tai 0777 tai symbolisesti, kuten esim. u=rw,g=r,o=r
- Preserve-asetuksella tiedostolle annetaan samat käyttöoikeudet kuin lähdetiedostolla.

#### Copy esimerkki

```
- name: Copy file with owner and permissions
  ansible.builtin.copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: '0644'
```

### Ansible-doc apt

- Hallitsee apt-paketteja esimerkiksi Debian- ja Ubuntu-käyttöjärjestelmissä.

#### Name
- Määrittää käsiteltävän apt-paketin nimen. Dokumentaatiosta ei löytynyt suoraa selitystä, joten käyttötarkoituksen päättelin esimerkkien perusteella.

#### State
- Määrittää paketin halutun tilan. Esimerkeissä käytetään arvoja "present", "absent" ja "latest".

#### Update_cache
- Päivittää apt-pakettien välimuistin. Esimerkeissä käytetään arvoa "yes". Dokumentaatiosta en löytynyt selitystä, joten käyttötarkoituksen päättelin esimerkkien perusteella.

#### Apt esimerkki

```
- name: Install apache httpd (state=present is optional)
  ansible.builtin.apt:
    name: apache2
    state: present
```

### Ansible-doc file

- Voi määrittää tiedostojen, hakemistojen ja symbolisten linkkien ominaisuuksia.
- Voi myös luoda ja poistaa tiedostoja, symbolisia linkkejä tai hakemistoja.

#### Path
- Määrittää hallittavan tiedoston polun.

#### Recurse
- Määrittää tiedostojen ominaisuudet rekursiivisesti hakemiston tiedostoille ja hakemistoille.
- Toimii vain silloin, kun state-asetuksena on directory.

#### Src
- Määrittää linkitettävän tiedoston polun.
- Käytetään vain, kun state=link tai state=hard.

#### State
- 
