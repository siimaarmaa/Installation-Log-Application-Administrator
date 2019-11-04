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

###### 2. Tomcat lisamine süsteemi ja seadistus
- Muudame `sudo nano /opt/tomcat/conf/tomcat-users.xml` , et saaksime veebihalduse kaudu hallata rakendusi. Muudatuste [Contribution guidelines for this project](conf/tomcat-users.xml)
