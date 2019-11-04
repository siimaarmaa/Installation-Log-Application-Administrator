Paigalduslogi ülesande täitmiseks on kasutatud Ubuntu 18.04 LTS serverit ja Tomcat 8.5.47.

# Paigalduslogi (rak.admin)


- [x] __Paigaldusega alustatud:__ 18:27, 04.11.2019
- [x] __Paigaldus lõpetatud:__ n-a
- [x] __Paigalduse teostas:__ Siim Aarmaa


__1. Serveri ettevalmistus__
- Paigaldame operatsioonisüsteemi poolsed parandused kõige pealt: `sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y`
- Süsteemi lisatud OpenJDK: `sudo apt install default-jdk`
- Tomcat lisatud serveisse oma grupp: `sudo groupadd tomcat`
- Lisame kasutaja ja paneme __tomcat__ gruppi: `sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat`

__2. Tomcat lisamine süsteemi ja seadistus__
- 
