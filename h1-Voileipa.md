# H2 Tehtävät

## x) Karvinen 2026: Sudo without password

- Sudo ilman salasanaa mahdollistaa komentojen suorittamisen pääkäyttäjän oikeuksilla.
- Salasanaton sudo määritetään luomalla lisäämällä käyttäjä käyttäjäryhmään "sudoless". Tämän jälkeen luodaan uusi sudoers-sääntö komennolla ```sudo visudo /etc/sudoers.d/sudoless.```
- Sudoers tiedostoon lisätään ```%sudoless ALL = (ALL) NOPASSWD: ALL```. Tämä komento sallii ryhmän jäsenille kaikkien komentojen suorittamisen ilman salasanaa.
- Toimivuus kokeillaan kirjautumalla ulos, uudelleen sisään ja suorittamalla jokin sudo-komento.
- ```sudo -k``` poistaa aiemmin tallennetut kirjautumistiedot.
  
