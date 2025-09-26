# h6-Salataampa


## Sisältö
[x) Artikkeli](#x-artikkeli)

[a) Let's](#a-Let's)

[b) A-rating](#b-A-rating)

[c) Vapaaehtoinen](#c-Vapaaehtoinen)

### Koneen tekniset tiedot
Prosessori: Intel Core i5-8265U CPU @ 1.60 GHz (1.80 GHz turbo, 8 ydintä)
RAM: 16 GB (15,7 GB käytettävissä)
Järjestelmä: Windows 11 Pro 64-bittinen (x64-suoritin)
Näytönohjain: Intel UHD Graphics 620
Tallennustila: 237 GB, josta 158 GB vapaana
DirectX-versio: DirectX 12

# x) Artikkeli 




# a) Let's

Lähdin aloittamaan raporttia 26.09.2025 kello 21:11. 

Kirjauduin ensin virtuaalikoneelle ja avasin valmiiksi Let's Encryptin verkkosivut. Minulta löytyy virtuaalipalvelin ja domain `Liljasharifi.com` jonne aion asentaa salauksen.

Otin tunnilta muistiinpanoja ja hyödyllinen ohje löytyi myös DigitalOceanilta (2024), sekä certbotin instructions sivustolta.


### Aloitus

* Asensin certbotin
  - **`sudo apt update`** - päivittelin paketit
  
  - **`sudo apt install certbot python3-certbot-apache`** - asennettiin certbot
 
  ![1](images/1.png)

_Onnistunut certbotin asennus_
 
* **´sudo certbot --apache --domains liljasharifi.com,www.liljasharifi.com`** - komento jolla sertifikaatti ladataan

### Virhetilanne 

"Hint: The Certificate Authority failed to verify the temporary Apache configuration changes made by Certbot. Ensure that the listed domains point to this Apache server and that it is accessible from the internet."

  ![3](images/3.png)

 _sertifikaatin hankinta epäonnistuu_

* **`curl -l liljasharifi.com`** komennolla vinkkejä virhetilanteeseen

  ![4](images/4.png)

_vinkki virhetilanteesta_

Virheilmoitus:
"curl: (7) Failed to connect to liljasharifi.com port 80 after 21003 ms: Could not connect to server"

Tästä heräsi kysymys oliko portin asetukset kunnossa. Lähdin tarkistamaan seuraavasti, tästä oli tunnilta muistiinpanoja jossa virhetilannetta selviteltiin.

### Palomuurin tarkistusta

* **`sudo ufw status`**

* **`sudo ufw allow 80/tcp`**
  
* **`sudo ufw reload`**

Olihan se kunnossa. Lähdin hieman tutkimaan verkkoa ja tässä vierähtikin jo tovi. 

* **`ping liljasharifi.com`**
  - Ei vastausta. 

### Ratkaisu 

Ja sitten heureka -hetki. Tajusin että olen tehnyt nämä edellä mainitut komennot **paikalliskoneella.** Ehkä olisi järkevämpi tehdä raporttia muulloin kuin myöhään yöllä.

Toisaalta tuntui hyvältä, kun hoksasin itse asian. Lueskelin muutamia sivustoja läpi mutta heräsi ajatus, että jokin oleellinen menee tässä väärin.

No loppu hyvin kaikki hyvin - eli lähdetään alusta:

### Muodostetaan SSH- yhteys palvelimelle:

* **`ssh lilja-web-01-fin@178.62.231.96`**

### Asennetaan uudelleen certbot mutta oikeaan paikkaan: 
* **`sudo apt update`** 
* **`sudo apt install certbot python3-certbot-apache`** 

### Kohtalon hetki eli ajetaan certbot ja kysytään sertifikaattia
* **`sudo certbot --apache --domains liljasharifi.com,www.liljasharifi.com`** 

![7](images/7.png)

_Onnistunut lopputulos_

Tässä kohtaa ehkä hieman ihmetytti miten tuollainen yksinkertainen asia jäi huomaamatta. No toisaalta mielummin yksinkertainen ratkaisu kuin monimutkainen ongelma.

Kello oli tässä kohtaa 23:02 ja siirryin seuraavaan vaiheeseen.

# b) A-Rating 

* Avasin ohjeistuksen mukaisesti sivuston: `https://www.ssllabs.com/ssltest/`

* Syötin hakukenttään domainin eli liljasharifi.com


# c) Vapaaehtoinen





# Lähteet

Horcasitas, J & Heidi, E. &  & Walia, A. (2024). Digitalocean. Verkkosivu. _How To Secure Apache with Let's Encrypt on Ubuntu_  Luettavissa: https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu/ Luettu: 26.09.2025.

Karvinen, T. 2017. Verkkosivu. _First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS_ Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ Luettu 13.09.2025.

Karvinen, T. 2025. Verkkosivu. _Linux Palvelimet 2025_ Luettavissa: https://terokarvinen.com/linux-palvelimet/ Luettu 13.09.2025.

Let's Emcrypt. 2018. Keskustelufoorumi. _Multiple virtual hosts, multiple domains in host one cert for each host_ Luettavissa: https://community.letsencrypt.org/t/multiple-virtual-hosts-multiple-domains-in-host-one-cert-for-each-host/ Luettu: 26.09.2025.

Heidi, E. DigitalOcean. Verkkosivu. _How to Set Up Let’s Encrypt Certificates for Multiple Apache Virtual Hosts on Ubuntu 14.04_ Luettavissa: https://www.digitalocean.com/community/tutorials/how-to-set-up-let-s-encrypt-certificates-for-multiple-apache-virtual-hosts-on-ubuntu-14-04/ Luettu 26.09.2025.
