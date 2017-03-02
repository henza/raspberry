#Raspberry robot 

##Roboti komplekteerimine

Veendu et sul on olemas kõik vajalikud osad. Kui midagi on puudu anna sellest teada CodeSchool juhendajale.

![Komponendid](http://i68.tinypic.com/1z5kd41.jpg)

![Esimene](http://i65.tinypic.com/2akh0l5.jpg)

![Teine](http://i64.tinypic.com/2vtwsh0.jpg)

![Chassis](https://raw.githubusercontent.com/simonmonk/wiki_images/master/rrb_robot_chassis_parts.jpg)

Roboti komplektiga oli kaasas ka juhend mootorite ja rataste kinnitamiseks

##Python tarkvara installimine

Kõigepealt veendu et sinu Raspberry on ühendatud internetiga. Siis ava terminal ja sisesta järgnevad käsklused.
```
$cd ~
git clone https://github.com/henza/raspberry.git
cd raspberry/python
sudo python setup.py install
```

### Todo
- [ ] Script Automation
- [ ] Add updated python script to repo

Auto Login Setup (optional)

The first step is to enable the Pi to login automatically without requiring any user intervention. This step is optional.

At the command prompt or in a terminal window type :

sudo raspi-config
followed by Enter.

Select “Boot Options” then “Desktop/CLI” then “Console Autologin”


Auto-run Script Setup

Now we need to tell the operating system to run the script for the Pi user. In the command prompt or in a terminal window type :

sudo nano /etc/profile
Scroll to the bottom and add the following line :

sudo python ~/Desktop/examples/rover_avoiding.py

