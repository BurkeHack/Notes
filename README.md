#RECOPILACIÓN PASIVA

Aplicamos técnicas de OSINT.

Buscamos información en internet con google hacking y comando booleanos (existe una base de datos de google hacking).

Buscar información en Shodan, en Censys.

Whois, archive.org, Theharvester, Maltego, Recon-ng.




#RECOPILACIÓN SEMI-PASIVA

FOCA: descarga y análisis de metadatos

CentralOPS y DNSdumpster, Wireshark.



#RECOPILACIÓN ACTIVA

Transferencia fichero de zona: dnsrecon -d [dominio] -t axfr

##Nmap:

Descubrimiento de Hosts: nmap -sN [IP] esta opción utiliza el protocolo TCP intentando establecer conexiones (mas intrusiva)
                         sudo nmap -sN [IP] esta opción utiliza el protocolo ARP (menos intrusiva)

Escaneo de Puertos TCP: sudo -sS [IP] -p [Puerto] primero utiliza el protocolo ARP para identificar hosts y luego TCP para probar puertos pero no establece la conexión
                    sudo -sT [IP] -p [Puerto] establece una conexión TCP

Realizar un Reporte: sudo nmap -v --reason -sS -oX [nombre fichero].xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" [IP a escanear]

Escaneo de Puertos UDP: sudo -sU [IP] -p [puerto] utiliza el protocolo UDP

Escaneo de Servicios: sudo nmap -sV [IP] -p [Puerto] ARP-TCP sin establecer conexión

Identificación del SO: sudo nmap -v -O [IP]

Realizar un Reporte completo: sudo nmap -v --reason -sS -O -sV -oX [nombre fichero].xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" [IP a escanear]

Enumeración SMB: sudo nmap -v -sS -p 139,445 [IP]

Scripts: /usr/share/nmap/scripts/ ls smb* (keyword y *)

Enumeración SMB utilizando Scripts: sudo nmap -v -sS -p 139,445 --script=[nombre del script] [IP] 

Enumeración SNMP: sudo nmap -v -sU -p 161 [IP]

Enumeración SNMP utilizando Scripts: sudo nmap -v -sU -p 161 --script=[nombre del script] [IP]



#ANÁLISIS DE VULNERABILIDADES:

De forma manual tomamos le imput de la fase anterior, como puede ser el fichero .xsl creado por nmap con los servicios y versiones que corren en el sistema objetivo, y buscamos estos servicios y versión en una base de datos como cve details, cve mitre, cvss. En estas bases de datos identificamos si efectivamente existen vulnerabilidades conocidas en esos sistemas y ahí poder buscar exploits ya sea en exploitdb vulmon, o google.

Análisis de vulnerabilidades con Nmap puertos TCP: sudo nmap -v -sS -oX [nombre fichero].xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" --script=vuln [IP]

Análisis de vulnerabilidades con Nmap puertos UDP: sudo nmap -v -sU -oX [nombre fichero].xml --stylesheet="https://svn.nmap.org/nmap/docs/nmap.xsl" --script=vuln [IP]
