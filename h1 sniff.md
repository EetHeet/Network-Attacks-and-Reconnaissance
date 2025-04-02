# H1 Sniff

## [Tehtävät](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff)

#### x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
- [Karvinen 2025: Wireshark - Getting Started](https://terokarvinen.com/wireshark-getting-started/)
- [Karvinen 2025: Network Interface Names on Linux](https://terokarvinen.com/network-interface-linux/)

#### a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. (Tätä alakohtaa ei poikkeuksellisesti tarvitse raportoida, jos sinulla ei ole mitään ongelmia. Jos on mitään haasteita, tee täsmällinen raportti)

#### b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.

#### c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).

#### d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Voit selityksen tueksi laatikoida ne ruutukaappauksesta.

#### e) Mitäs tuli surffattua? Avaa [surfing-secure.pcap](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/surfing-secure.pcap) . Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.

#### f) Vapaaehtoinen, vaikea: Mitä selainta käyttäjä käyttää? [surfing-secure.pcap](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/surfing-secure.pcap) (Päivitys 2025-03-31 w14 ma - muutin tehtävän vapaaehtoiseksi Giang:n suosituksesta)

#### g) Minkä merkkinen verkkokortti käyttäjällä on? [surfing-secure.pcap](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/surfing-secure.pcap) 

#### h) Millä weppipalvelimella käyttäjä on surffaillut? [surfing-secure.pcap](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/surfing-secure.pcap) 
- Huonoja uutisia: yhteys on suojattu TLS-salauksella.

#### i)  Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)

## Vastaukset

### X.

#### Karvinen 2025: Wireshark - Getting Started

- Tässä kerrotaan miten asennetaan **wireshark** `sudo apt-get install wireshark`
- Kerrotaan että asennuksessa täytyy valita että paketteja voidaan napata myös ilman sudo oikeuksia
- kerrotaan että lisätään oma käyttäjä wireshark ryhmään, jotta paketteja voidaan napata
- Sitten kerrotaan miten napataan paketteja
    - Valitaan verkkokortti
    - ja alotetaan tallennus
- Jos paketteja ei näy neuvotaan tarkistamaan onko käyttäjä wireshark ryhmässä
- Kerrotaan miten tallennetaan ja ladataan kaappauksia
- Kerrotaan statistic valikosta
    - Endpoints: nähdään hostit
    - I/O Graphs: milloin paketit napattiin ja kuinka kauan kaappaus kesti
    - Procol hierarchy: nähdään mitä protokollia käytettiin
- Sitten kerrotaan fillttereistä
- Ja viimeiseksi kerrotaan Follow TCP Streamista, jolla voidaan vaikka lukea salaamaton keskustelu helposti tekstinä

#### Karvinen 2025: Network Interface Names on Linux

- Selitettän mikä Network interface on
- Selitetään mitä eri prefixit tarkottaa Linuxissa
    - en: ethernet
    - wl: wlan
    - lo: Loopback
- Kerrotaan kommennot joilla voi nähdä omat network interfacet
    - `ip a`
    - `ip route`

### A.

Kali asennettu hyperv:hen

### B.

Saan poistettua internet yhteyden hyprv:n asetuksista

![image](https://github.com/user-attachments/assets/3d8ae6d3-0e37-4bce-872e-dc0a8af42532)

![image-1](https://github.com/user-attachments/assets/c8475817-4348-41a8-a05d-6f107f51c1fb)

![image-2](https://github.com/user-attachments/assets/b64203e3-14d7-4d8b-ab47-6ca514f6d6de)

![image-3](https://github.com/user-attachments/assets/f3e8d449-879b-4869-8c96-3fffa682a2ed)

### C.

Wireshark on jo valmiiksi asennettuna kalissa

Voidaan siepata sillä omaa liikennettä painamalla "Start capturing packets"

![image-4](https://github.com/user-attachments/assets/1e5f2c8c-2f7b-45dd-9475-2d1eee57da76)

![image-5](https://github.com/user-attachments/assets/f241ba1f-3eb2-4412-a4ff-048f86769a97)

### D.

Tein `curl` komennolla pyynnön google.com

**Application Layer**

![image-8](https://github.com/user-attachments/assets/761a61c4-f787-45ad-9d9e-e5c144d1d6ea)

Tässä nähdään data joka lähetetään

**Transport Layer**

![image-9](https://github.com/user-attachments/assets/de060372-05b2-495f-a82c-11904aecc054)

Tässä nähdään että dataan lisätään lähde portti **38968** ja kohde portti joka on **80**

**Network Layer**

![image-10](https://github.com/user-attachments/assets/82a323ff-2aa0-4034-9e56-fc538523146b)

Tässä Segmenttiin lisätään mm. lähde ip **172.18.175.65** ja kohde ip **216.58.211.238**

**Link Layer**

![image-11](https://github.com/user-attachments/assets/b3234cbf-634d-4e6e-99e5-b5e314505297)

Tässä pakettiin lisätään mm. lähde MAC osoite **00:15:5d:63:36:05** ja kohde MAC osoite **00:15:5d:10:3f:c0**

### E.

Kaappauksessa on 283 eri pakettia ja kaappaus kesti 7 sekuntia

![image-30](https://github.com/user-attachments/assets/01b2b2d9-d8f9-4c61-a77c-5abb7cdbb441)

Kaapauksessa löytyviä protokolli on mm. tcp, dns, TLSv1.3

![image-31](https://github.com/user-attachments/assets/1e4a2e77-ada1-43da-9495-73a3d54f7ef6)

Ensimmäisenä pistää silmään protkolla **QUIC**, koska en tiedä mikä se on

![image-32](https://github.com/user-attachments/assets/4926df77-782e-478d-99d9-40f7de1b8b88)

### F.

Tästä en ole aivan varma toimiiko näin, mutta tässä videossa https://www.youtube.com/watch?v=G2skyNJosCA selitettiin että **JA3 Signature** sisältää ClientHello parametrejä ja että tietyt ClientHello parametrit yleensä osoittavat johonkin tiettyyn selaimeen, koska siinä kerrottaan muunmuas mitä TLS versiota client tukee ja mitä "cipher suites" client tukee https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/

Ja näitä kun on kerätty tarpeeksi ja nähdään esim että firefox tukee aina näitä ja näitä asioita niin voidaan **JA3 Signaturesta** päätellä mikä selain on käytössä

Kaappauksesta löytyy tämmöinen paketti

![image-27](https://github.com/user-attachments/assets/256b99e4-fe16-4208-800d-b49db3a34287)

Ja tämä paketti sisältää

![image-28](https://github.com/user-attachments/assets/97c88fcb-2699-494c-851c-e4716e99926f)

Löysin tämän sivun https://ja3.zone/ jonka pitäisi tunnistaa mitä selainta käytetään

Törkkäsin **JA3 Signature** sinne ja sain tämän

![image-29](https://github.com/user-attachments/assets/a2f0b6ef-e9fc-447e-bcdc-2d0177f9fefa)

Ja suurin osa tuloksista näyttää Firefoxia, joten vastaan että käyttäjä käyttää Firefoxia

### G.

Koska verkkokortin valmistaja näkyy mac osoitteen kolmesta ensimmäisestä oktetista ja kaikki lähetetyt paketit alkava `52:54:00` niin tällä saadaan selville valmistaja

Mutta koska mitkään "mac address lookup" sivut eivät antaneet suoraan mitään vastausta

![image-6](https://github.com/user-attachments/assets/dfa51127-ee5a-4ce0-aa88-434e0e47664a)

Niin tein hieman selvittelyä ja löysin tämän sivun https://macaddress.io/faq/how-to-detect-a-virtual-machine-by-its-mac-address

Ja täällä kerrotaan että `54:52` alkuiset mac osoitteet ovat KVM (proxmox) 

![image-7](https://github.com/user-attachments/assets/88ca36dd-80cd-4491-8776-0bb04000aeca)

Niin tästä voidaan päätellä että käyttäjä käyttää virtuaalikonetta

### H.

Käyttäjä on surffaillut terokarvinen.com 

![image-33](https://github.com/user-attachments/assets/c81d9859-4bcc-496d-9e4c-6251894ce1f9)

Ja terokarvinen.com käyttää apachea

![image-34](https://github.com/user-attachments/assets/6afd6ed1-1378-47b2-936a-51c773f53ea2)

### I.

Tässä esimerkissä on napattu TCP kättely

![image-12](https://github.com/user-attachments/assets/aa5604c0-a1bf-46a1-9eca-29c5c5464439)

Tässä on ensimmäinen **SYN** viesti

![image-13](https://github.com/user-attachments/assets/4b9b7f29-15d4-4fa7-819b-1ddba1727b74)

Tästä nähdään esimerkiksi että paketin koko on 74 tavua ja että verkkoliitäntänä toimii eth0 eli Ethernet

![image-14](https://github.com/user-attachments/assets/7f8dfef4-c5a2-49b8-b775-092bcefdb913)

Tässä nähdään lähtö ja kohde mac osoitteet

![image-15](https://github.com/user-attachments/assets/cb8cd302-085a-429c-80fe-dcebfe12ec80)

Tässä nähdään esim kohde ja lähtö ip osoitteet sekä ttl(time to live), joka tarkoittaa sitä että niin monta hyppyä paketti tekee ja jos se ei löydä kohde serveriä sen jälkeen paketti hylätään tässä tapauksessa ttl on 64

Nähdään myös, että ip protokollana toimii ipv4

![image-16](https://github.com/user-attachments/assets/81f1fd1c-7ae0-4c03-a8f8-41f53120d970)

Tässä nähdään lähtö ja kohde portit ja nähdään myös että kyseessä on SYN viesti

![image-17](https://github.com/user-attachments/assets/7a091262-6e07-4467-8493-b7fbc746a34f)

Tässä on toinen **SYN/ACK** viesti

![image-18](https://github.com/user-attachments/assets/41054e3b-6708-4be4-ad3d-132be56dd45a)

Tässä on about samat tiedot kuin edellisessä mutta koska vastaus on serveriltä niin on lahtö/kohde ip, lähtö/kohde portti ja lähtö/kohde mac osoite ovat toisten päin

Tästä viestistä voidaan myös analysoida, että ttl on 58 niin serveri on kuuden hypyn päässä meistä

Tässä viimein **ACK** viesti

![image-19](https://github.com/user-attachments/assets/cac37c83-976c-4071-9b4c-191e6fe0f4cf)

Näissä kaikissa on vielä huomioitavaa **Sequence number** ja **Acknowledgment number**

Eli kun lähetämme ensimmäisen **SYN** viestin niin lähetämme siinä **Sequence number** joka meidän tapauksessa on ![image-21](https://github.com/user-attachments/assets/5b106e88-ecde-418e-8be0-f30ca8494ac1)

Ja kun serveri vastaa niin siinä on mukana **Acknowledgment number** joka on edellinen numero mutta korotettu yhdellä ![image-22](https://github.com/user-attachments/assets/85c7f7a2-3653-4972-995a-5cd20e8e496e)

Tämä kertoo meille että serveri sai viestin ja tässä viestissä on myös oma Sequence number ![image-23](https://github.com/user-attachments/assets/5119640b-d528-4649-b60a-bfc15cdf65ca)

Johon meidän viimeinen **ACK** viesti korottaa taas yhden kertoen serverille että saimme edellisen viestin ![image-24](https://github.com/user-attachments/assets/7c428172-925d-421d-9aef-50b2969d7133)

### Lähteet

Offensive JA3 – Max Harley (SO-CON 2020): https://www.youtube.com/watch?v=G2skyNJosCA

What happens in a TLS handshake? | SSL handshake: https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/

How to detect a Virtual Machine by its MAC address?: https://macaddress.io/faq/how-to-detect-a-virtual-machine-by-its-mac-address

MAC Address Lookup: https://maclookup.app/

