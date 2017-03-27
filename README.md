#CodeSchool - Raspberry robot 

##Roboti komplekteerimine

Veendu et sul on olemas kõik vajalikud osad.

- Mälukaart
- Raspberry
- Roboti raam, rattad, kaks mootorit
- RaspiBoard
- Sensor

Vajalikud kaablid ja muud pisiajsad jagame jooksvalt. 


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

Kui oled robotit nüüd mõnd aega testinud märkad, et robot pöörab suhteliselt kaootiliselt. Selleks, et seda muuta, peame konfigureerima Python skripti mis käsib robotil pöörata kui takistus teele jääb. 

Proovi nüüd terminalis navigeeride kausta Examples ja sisesta järgmine käsklus. Siinkohal mainin ka et kui sul tekib küsimus mida mingi käsklus tähendab siis pane sama käsklus Googlesse. 

```
sudo nano rover_avoiding.py
```
Nüüd peaksid nägema järgmist koodi. Nagu sa võisid aimata, siis käsklus `nano` avab skripti tekstina mida saab muuta, aga käsklus `python` käivitab faili.

```
# Attach: SR-04 Range finder, switch on SW1, and of course motors.

# The switch SW2 stops and starts the robot

from rrb3 import *
import time, random

BATTERY_VOLTS = 9
MOTOR_VOLTS = 6

rr = RRB3(BATTERY_VOLTS, MOTOR_VOLTS)

# if you dont have a switch, change the value below to True
running = False

def turn_randomly():
    turn_time = random.randint(1, 3)
    if random.randint(1, 2) == 1:
        rr.left(turn_time, 0.5) # turn at half speed
    else:
        rr.right(turn_time, 0.5)
    rr.stop()

try:
    while True:
        distance = rr.get_distance()
        print(distance)
        if distance < 15 and running:
            turn_randomly()
        if running:
            rr.reverse(0)
        if rr.sw2_closed():
            running = False
        if not rr.sw2_closed():
            running = True
        if not running:
            rr.stop()
        time.sleep(0.2)
finally:
    print("Exiting")
    rr.cleanup()
```

#Esimene ülesanne!

Eesmärk: Robot peab iseseivalt sõitma kolmnurkselt marsuudil. 

Alustuseks joonista põrandale võrdkülgne kolmnurk, mille üks külg on 1m. Hetkel me ei pane robotit joont järgima, vaid kirjutame skripti, mis juhib robotit. 

Skripti alguses me impordime `from rrb3 import *` tarkvara, mis aitab meil mootoreid kontrollida. Peamised käsklused on `forward`, `reverse`, `left`, `right`, `stop`.

Näiteks, kuime tahame et robot hakkaks otse liikuma, kasutame `rr.forward()`. See käsklus käivitab roboti mõlemad mootorid ja kui juhtmed on õigesti ühendatud, hakkab robot otse edasi liikuma kuni järgmine käsklus sisestada. 

Kui sa soovid, et robot liiguks otse ainult teatud aja, siis seda saame täpsustada esimese argumendiga `rr.forward(aeg, kiirus(0-1))`. Teine argument on kiirus, mis vaikimisi on 0.5 ehk pool maksimaalsest kiirusest. 

Mõned näited:

rr.forward()       # Robot liigub otse, kuni järgmise käskluseni, poole kiirusega
rr.forward(5)      # Robot liigub otse, 5 sekundit, poole kiirusega
rr.forward(5, 1)   # Robot liigub otse, 5 sekundit, täis kiirusega
Käsklused `left`, `right`, `reverse` töötavad samamoodi.

`rr.stop()` käsklus peatab mõlemad mootorid.


Ultraheli sensor

Kasutades funktsiooni `rr.get_distance()` mõõdab sensor kauguse otse ees asuvast objektist sentimeetrites. Hetkel meil ei ole sensorit tarvis, aga võid igaksjuhuks lisada tingimuse, et kui kaugus objektist on väheb kui 15cm, siis pöörab robot ennast ümber.

Nüüd on aeg katsetada
