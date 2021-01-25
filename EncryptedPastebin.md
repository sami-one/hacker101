# Encrypted Pastebin

Tehtävä alkaa web-lomakkeesta, johon voi syöttää otsikkokenttään otsikon ja tekstikenttään jotain tekstiä.
Testimielessä laitoin otsikkokenttään oman nimeni ja nappasin Post-nappulaa.
Selain menee sivulle, jossa url-kentässä on enkoodattuna jotain tietoa.
Omalla kohdallani seuraavanlaita
x0EzJ3lR08HFUMaYrc8J5NcLKMbxlmA5sFUmbnh3RafvOIO75GWGCnrSjMzaUM86OwOsEMMdSVYTgjig7SS1OE4qM02NsbKc36NDn0!dm6FbWACL!5uBe12cgTipkh2USNFbiAvmvSebjUr3ESE2IRNkbNYYUftbnrAP0e19XvBImPvGd9ZqWGdEdaSs7iQC7U3x!34kAAylj1Yqyr8vlw~~

Rivin lopussa olevat tildet olivat epäilyttävän näköisiä, niin ilman kummempaa miettimistä poistin niistä toisen ja nappasin url:n latautumaan uudelleen.

Sivu lataa virheilmoituksen, josta löytyy myös ensimmäinen lippu.

Virheilmoituksesta löytyy myös jatkon kannalta oleellista tietoa:
Enkoodaus näyttäisi olevan base64 ja lisäksi merkkijonosta on vaihdettu merkkejä, =/+ on vaihdettu ~!- merkkeihin.
Kopioin tuon rimpsun url-kentästä ja nakkasin Cyberchefiin.
Reseptiksi otin Substitute ja arvoiksi nuo aiemmin merkityt.
Koitin samalla, että mitä sillisalaattia tuosta saisi auki muutamilla eri resepteillä.
Ei oikein mitään.

Huomasin myös, että tuo kohdesivu antoi virheeksi incorrect padding.
Pienellä googlettelulla törmäsin alla olevaan kirjoitukseen:
https://blog.gdssecurity.com/labs/2010/9/14/automated-padding-oracle-attacks-with-padbuster.html

Eli ei muuta kuin Padbusteria testamaan
Syntaksi padbusteriin pienen tutkiskelun jälkeen oli:
padbuster *url-konvertoiduilla merkeillä* *pelkkä cipheri konvertoiduilla merkeillä* 16 -encoding 0
Jossa 16 on blokin pituus ja -encoding 0 tarkoittaa base64:sta.
Aika pitkän pyörittelyn jälkeen padbusterilla ratkesi lippu numero kaksi.

