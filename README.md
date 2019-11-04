Paigalduslogi ülesande täitmiseks on kasutatud Ubuntu 18.04 LTS serverit ja Tomcat 8.5.47.

# Paigalduslogi (rak.admin)


- [x] __Paigaldusega alustatud:__ 18:27, 04.11.2019
- [x] __Paigaldus lõpetatud:__ n-a
- [x] __Paigalduse teostas:__ Siim Aarmaa


###### 1. Serveri ettevalmistus
- Paigaldame operatsioonisüsteemi poolsed parandused kõige pealt: `sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y`
- Süsteemi lisatud OpenJDK: `sudo apt install default-jdk`
- Tomcat lisatud serveisse oma grupp: `sudo groupadd tomcat`
- Lisame kasutaja ja paneme __tomcat__ gruppi: `sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat`
- Tomcat install on ajutiselt laetud tmp kausta: `wget https://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.47/bin/apache-tomcat-8.5.47.tar.gz`
- Teeme kausta kuhu pakkime lahti Tomcati: `sudo mkdir /opt/tomcat` ja pakkime ahriivi lahti `sudo tar xzvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1`
- Anname __/opt/tomcat recursive__ õigused: `sudo chown -R tomcat: /opt/tomcat` ja käivitame tomcat paigalduse `sudo sh -c 'chmod +x /opt/tomcat/bin/*.sh'`

###### 2. Tomcati ettevalmistus
- Muudame `sudo nano /opt/tomcat/conf/tomcat-users.xml` , et saaksime veebihalduse kaudu hallata rakendusi. [Muudatused seadistuses.](conf/tomcat-users.xml)
- [Loome serveri konto Tomcat jaoks.](conf/tomcat.service) - `sudo nano /etc/systemd/system/tomcat.service`
- Lubame Tomcati, Daemon reload: `sudo systemctl daemon-reload` , käivitame tomcati `sudo systemctl start tomcat.service` ja lubame `sudo systemctl enable tomcat.service`
- Peale lubamist, tuleb kinnitus sõnum, conf loodud __Created symlink /etc/systemd/system/multi-user.target.wants/tomcat.service → /etc/systemd/system/tomcat.service.__
- Vaatame __systemctl__ üle kas kõik jookseb kenasti `sudo systemctl status tomcat.service`
```
● tomcat.service - Siim Aarmaa Tomcat
   Loaded: loaded (/etc/systemd/system/tomcat.service; enabled; vendor preset: ena
   Active: active (running) since Mon 2019-11-04 16:59:23 UTC; 1min 20s ago
 Main PID: 20100 (java)
    Tasks: 48 (limit: 2290)
   CGroup: /system.slice/tomcat.service
           └─20100 /usr/lib/jvm/default-java/bin/java -Djava.util.logging.config.f

Nov 04 16:59:23 tomcat systemd[1]: Starting Siim Aarmaa Tomcat...
Nov 04 16:59:23 tomcat startup.sh[20087]: Tomcat started.
Nov 04 16:59:23 tomcat systemd[1]: Started Siim Aarmaa Tomcat.
lines 1-11/11 (END)...skipping...
● tomcat.service - Siim Aarmaa Tomcat
   Loaded: loaded (/etc/systemd/system/tomcat.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2019-11-04 16:59:23 UTC; 1min 20s ago
 Main PID: 20100 (java)
    Tasks: 48 (limit: 2290)
   CGroup: /system.slice/tomcat.service
           └─20100 /usr/lib/jvm/default-java/bin/java -Djava.util.logging.config.file=/opt/tomcat/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djava.security.egd=file:///dev/urandom -Djdk.tls.ephemeralDHKeySize=2048 -Djava.pr

Nov 04 16:59:23 tomcat systemd[1]: Starting Siim Aarmaa Tomcat...
Nov 04 16:59:23 tomcat startup.sh[20087]: Tomcat started.
Nov 04 16:59:23 tomcat systemd[1]: Started Siim Aarmaa Tomcat.
```
- [Näeme, et teenus on püsti.](screenshot/tomcatpüsti.png)
- Teeme muudatused [`sudo nano /opt/tomcat/webapps/manager/META-INF/context.xml`](conf/opt/tomcat/webapps/manager/META-INF/context.xml) ja [`sudo nano /opt/tomcat/webapps/host-manager/META-INF/context.xml`](conf/opt/tomcat/webapps/host-manager/META-INF/context.xml) et saaks igast võrgust ligi.
- 
