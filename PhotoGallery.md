# Photo gallery. 
Kohteena on jonkinlainen kuvagalleria sivu. Heti alkuun ottaa silmään, että yksi sivun kuvista ei ole latautunut.  \
Kurkasin hiukan lähdekoodia ja sieltä huomasin, että kuvat ladataan "fetch?id=1" urlilla.  \
Mielenkiinnosta koitin mitä noista aukeaa ja id=1 ja id=2 availevat noita kuvia, mutta id=3 tuottaa virheen.\
Ilmeisesti siis on kyse jostain tietokannasta niin, ei muuta kuin sqlmap ajamaan http://url/fetch?id=1 -urliin.  \
Löydökseksenä id on haavoittuvainen SQL-injektiolle.  \
Vinkeistä löytyy "This application runs on the uwsgi-nginx-flask-docker image". \
https://github.com/tiangolo/uwsgi-nginx-flask-docker. linkistä löytyy dokumentaatio tuolle dockerille. \
Vinkeistä löytyy myös: UNION:n käyttöön. Näin ollen voidaan olettaa, että tuohon fetch?id=1 urliin pitää lisätä. \
vielä UNION SELECT ja sitte tiedosto, jonka näillä vinkeillä voisi olettaa löytyvän tuolta kannasta.  \
Dokumentaatiossa tehdään main.py tiedosto ja näin ollen se voisi olla hyvä kanditaatti aloittaa.  \
Testasin muutamilla id= arvoilla ja 4:s oli ensimmäinen jota kannasta ei ilmeisesti löytynyt eli. \
fetch?id=4 UNION SELECT 'main.py' --  \
Nyt selaimeen lävähti sivu, jolta löytyy myös ensimmäinen lippu.  
  
Samaiselta sivulta löytyy myös aika paljon kaikkea muutakin mielenkiintoista.  \
Otetaanpa sitten dumppi sqlmapilla.

sqlmap -u "http://urlfetch?id=1" --method=GET --dump -D level5 -T photos -p id --code=200 --ignore-code=500 --skip-waf --threads=2 -o. \
Saadaan mukavan näköinen käppyrä tuosta photos taulusta ja erityisen kiinnostava on tuo sekasotku id 3:n kohdalla\

3  | Invisible        | 1      | f38d84cb4a9dba7a1703a5fe1a8f3ba5334e87394b7e838c55232c47b3b507ff
