#Raspberry robot 

##Roboti komplekteerimine

Veendu et sul on olemas kõik vajalikud osad.

- Mälukaart
- Raspberry
- Roboti raam, rattad, kaks mootorit
- RaspiBoard
- Sensor

Vajalikud kaablid ja muud pisiajsad jagame jooksvalt. 


Roboti komplektiga oli kaasas ka juhend mootorite ja rataste kinnitamiseks. Järgi seda juhendit ja alusta komplekteerimist.

###Tinutamine

Kui sul on juhtmed ühendatud, leia üles Indrek, kes aitab tinutada. 



##Python tarkvara installimine

Kõigepealt veendu et sinu Raspberry on ühendatud internetiga. Siis ava terminal ja sisesta järgnevad käsklused.

Esimene käsklus navigeerib Raspberry Deskptop kausta
```
cd Desktop
```
Teise käsklusena sisesta "ls", mis kuvab Desktop kaustas kõik failid, hetkel peaks see tühi olema
```
ls
```

Järgmine käsklus kopeerib Githubist roboti jaoks vaja minevad failid
```
git clone https://github.com/henza/raspberry.git
```
Kui nüüd sisestada uuesti käsklus "ls" siis kuvab terminal sulle kõik failid Desktop kaustas ja sinna peaks olema tekkinud uus kaust nimega raspberry
```
ls
```
Nüüd avame raspberry kaustas oleva faili python
```
cd raspberry/python
```
Enne kui saame Python faile oma Raspberrys kasutada peame installima vajaliku tarkvara. 
```
sudo python setup.py install
```
Nüüd testime, kas oleme roboti õigesti kokku pannud ja kas mootorid hakkavad tööle
Selleks navigeerime kausta examples ja käivitame faili rover_avoiding.py. 

```
cd examples
ls
python rover_avoiding.py
```
Kui kõik töötab, siis peaks ekraanil hakkama jooksma numbrid, mis tulevad sensorist ja kui takistusi pole hakkavad mootorid tööle.

Programmi töö katkestamiseks vajuta Crtl+C



##Auto login seadistamine

Ava terminal ja sisesta :
```
sudo raspi-config
```
ja vajuta enter

Vali “Boot Options” ja siis “Desktop/CLI” ning “Console Autologin”. Kui see on valitud, siis vali "Finish" ja "Reboot now"


##Python programmi automaatne käivitamine

Ava terminal ja sisesta :
```
sudo nano /etc/profile
```
Faili lõppu lisa järgnev rida:
```
sudo python ~/Desktop/raspberry/python/examples/rover_avoiding.py
```
Nano editorist väljumiseks vajuta klaviatuuril Ctrl+O ja siis Enter, väljumiseks Ctrl+X


Nüüd testime, kas script hakkab automaatselt tööle kui Raspberry käivitub. Selleks sisesta järgmine käsklust Raspberry taaskäivitamiseks:

```
sudo reboot now
```

