# Serverbeheer

Welkom bij de serverbeheerdocumentatie voor bedrijven. Deze handleiding biedt uitgebreide begeleiding voor het opzetten, configureren en beheren van servers voor een organisatie. Het serverbeheer begint bij de door Telesur, Digicel of ParboNet aangeboden ADSL-modem voor internetverbinding. Houd er rekening mee dat de verbindingsnelheid (Upload en Download) afhankelijk is van het aangekochte internetpakket van de klant.

Door deze documentatie te volgen, kunt u een veilige, betrouwbare en schaalbare IT-infrastructuur implementeren en onderhouden. We behandelen verschillende aspecten van serverbeheer, waaronder virtualisatie, firewallconfiguratie, Windows Server 2019 R2 en Linux Server.

1. [Virtualisatie](#virtualisatie)
2. [Firewall (pfSense)](#firewall-pfsense)
3. [Windows Server 2019 R2](#windows-server-2019-r2)
4. [Linux Server](#linux-server)

---

## Virtualisatie

In de servervirtualisatie wereld zijn er verschillende platforms beschikbaar, waaronder VMWare, Hyper-V, KVM en Proxmox. Elk van deze platforms heeft zijn eigen kenmerken, voordelen en toepassingsgebieden.

VMware is een van de meest bekende en gevestigde virtualisatieplatformen, maar het vereist vaak licenties en kan duur zijn voor kleine en middelgrote bedrijven. Hyper-V, ontwikkeld door Microsoft, is een ander populair platform dat vaak wordt gebruikt in Windows-omgevingen.

Proxmox, aan de andere kant, is een open-source virtualisatieplatform dat gebaseerd is op KVM (Kernel-based Virtual Machine) en LXC (Linux Containers). Het biedt een kosteneffectieve oplossing met een breed scala aan functies, waaronder krachtige virtualisatie, clusterondersteuning voor hoge beschikbaarheid en een gebruiksvriendelijke webinterface. Daarom hebben we ervoor gekozen om Proxmox te gebruiken in deze documentatie vanwege zijn flexibiliteit, gebruiksgemak en kosteneffectiviteit voor kleine en middelgrote bedrijven.

### Hardwarevereisten (standaard en aanbevolen)

Om Proxmox succesvol te kunnen installeren en uitvoeren, zijn er bepaalde hardwarevereisten waaraan moet worden voldaan. Deze omvatten:

- **Processor:** Een moderne multi-core processor met virtualisatieondersteuning (bijvoorbeeld Intel VT-x of AMD-V).
- **Geheugen (RAM):** Minimaal 4 GB RAM voor de hostserver, maar aanbevolen wordt 8 GB of meer voor optimale prestaties.
- **Opslag:** Voldoende opslagruimte voor het besturingssysteem van de hostserver, evenals voor de opslag van virtuele machines (aanbevolen wordt SSD-opslag voor betere prestaties).
- **Netwerk:** Ten minste één Ethernet-netwerkinterfacekaart voor netwerkconnectiviteit.

### Installatie van Proxmox

??? Note "Voorbereiding van het opstartbaar USB-flashstation"

    * Download de nieuwste versie van Proxmox VE van de officiële website op een computer met internettoegang.
    * Sluit een USB-flashstation aan op de computer. Zorg ervoor dat het USB-flashstation voldoende capaciteit heeft om de installatiebestanden van Proxmox te bevatten (minimaal 4 GB wordt aanbevolen).

    === "Windows: Gebruik van Rufus"
        
        Download Rufus, een gratis tool voor het maken van opstartbare USB-flashstations, vanaf de officiële website en start het programma.

        1. Selecteer het aangesloten USB-flashstation onder 'Apparaat'.
        2. Klik op 'Selecteren' naast 'Opstartselectie' en navigeer naar het gedownloade ISO-bestand van Proxmox VE.
        3. Klik op 'Start' om het proces te starten. Rufus zal het USB-flashstation formatteren en de nodige bestanden kopiëren om het opstartbaar te maken met Proxmox VE.
        4. Wacht tot het proces is voltooid en sluit Rufus af.

    === "macOS of Linux: Gebruik van Etcher"
    
        Download Etcher, een open-source tool voor het maken van opstartbare USB-flashstations, vanaf de officiële website en installeer het programma.

        1. Open Etcher en klik op 'Selecteer image' om het gedownloade ISO-bestand van Proxmox VE te selecteren.
        2. Selecteer het aangesloten USB-flashstation onder 'Select target'.
        3. Klik op 'Flash!' om het proces te starten. Etcher zal het USB-flashstation formatteren en de nodige bestanden kopiëren om het opstartbaar te maken met Proxmox VE.
        4. Wacht tot het proces is voltooid en sluit Etcher af.

    Nu het USB-flashstation is voorbereid met de installatiebestanden van Proxmox VE, kunt u doorgaan met het opstarten van de server en het installeren van Proxmox zoals eerder beschreven.


#### Stap 1: Voorbereiding

* Zet de server onder elektrische stroom. Het wordt aanbevolen om de server aan te sluiten op een UPS (Uninterruptible Power Supply) om stroomonderbrekingen te voorkomen tijdens het installatieproces.

   ![Server met UPS](link-naar-afbeelding)

* Start de server op en wacht tot het BIOS/UEFI-scherm verschijnt.

#### Stap 2: Opstarten vanaf de installatiemedia

* Plaats het opstartbare USB-flashstation met Proxmox in een USB-poort van de server.

* Start de server opnieuw op en druk op de juiste toets (bijvoorbeeld F12, DEL, of ESC, afhankelijk van het moederbord) om het opstartmenu te openen.

* Selecteer het USB-flashstation als opstartapparaat en druk op Enter.

   ![Opstartmenu](link-naar-afbeelding)


#### Stap 3: Proxmox installatiewizard

* Na het opstarten vanaf het USB-flashstation wordt de Proxmox installatiewizard geladen. Selecteer 'Install Proxmox VE' en druk op Enter.

   ![Proxmox installatiewizard](link-naar-afbeelding)

* Kies de gewenste taal voor de installatie en druk op Enter. In dit geval Nederlands.

   ![Taal selecteren](link-naar-afbeelding)

* Selecteer uw land of regio en druk op Enter. In dit geval Suriname.

   ![Land selecteren](link-naar-afbeelding)

* Kies het English International toetsenbordindeling en druk op Enter.

   ![Toetsenbordindeling](link-naar-afbeelding)

* Proxmox detecteert de beschikbare schijven op de server. Selecteer de doelschijf waarop u Proxmox wilt installeren en druk op Enter.

   ![Schijfselectie](link-naar-afbeelding)

* Bevestig dat u de geselecteerde schijf wilt gebruiken door 'Ja' te selecteren en op Enter te drukken.

   ![Bevestiging](link-naar-afbeelding)

#### Stap 4: Installatie voltooien

1. Wacht tot de installatie van Proxmox is voltooid. Dit kan enkele minuten duren, afhankelijk van de prestaties van uw server.

2. Nadat de installatie is voltooid, wordt u gevraagd om een wachtwoord in te stellen voor de 'root'-gebruiker van Proxmox. Voer een sterk wachtwoord in en bevestig het.

   ![Wachtwoord instellen](link-naar-afbeelding)

3. Wanneer de installatie is voltooid, wordt u begroet met het Proxmox inlogscherm. U kunt nu inloggen met de gebruikersnaam 'root' en het wachtwoord dat u hebt ingesteld tijdens de installatie.

   ![Inlogscherm](link-naar-afbeelding)


### Proxmox setup

Voordat we beginnen met het configureren van Proxmox, is het belangrijk om enkele best practices te bespreken met betrekking tot netwerkconfiguratie. Voor een efficiënte en veilige werking van uw Proxmox-omgeving is het aan te raden om gebruik te maken van private IP-adressen binnen een betrouwbaar IP-bereik, zoals gedefinieerd in RFC 1918. Overweeg om de volgende IP-bereiken te gebruiken:

WAN-interface: U kunt een publiek IP-adres toewijzen dat is verstrekt door uw internetprovider. Als u een privénetwerk gebruikt voor de WAN-interface, kies dan een IP-adres uit het publieke IP-bereik dat niet overlapt met IP-adressen die door andere netwerken worden gebruikt.
LAN-interface: Voor het LAN-netwerk kunt u een privé IP-bereik uit de volgende RFC 1918-adresruimtes gebruiken:

```
* 10.0.0.0/8
* 172.16.0.0/12
* 192.168.0.0/16
```

Zorg ervoor dat u subnetmaskers toepast die geschikt zijn voor uw netwerkvereisten en vermijd het gebruik van IP-adressen die mogelijk conflicteren met andere apparaten in uw netwerk.

#### Stap 1: Eerste login

1. Open een webbrowser (Edge of Chrome) op een computer in hetzelfde netwerk als de Proxmox-server.

2. Typ het IP-adres van de Proxmox-server in de adresbalk van de browser en druk op Enter.

3. U wordt begroet met het Proxmox inlogscherm. Log in met de gebruikersnaam 'root' en het wachtwoord dat u hebt ingesteld tijdens de installatie.

   ![Inlogscherm Proxmox](link-naar-afbeelding)

#### Stap 2: Root wachtwoord wijzigen

1. Nadat u bent ingelogd, wordt u gevraagd om het wachtwoord voor de 'root'-gebruiker te wijzigen. Voer een nieuw sterk wachtwoord in en bevestig het.

2. Het nieuwe wachtwoord is nu ingesteld voor de 'root'-gebruiker. Documenteer en zorg ervoor dat u dit wachtwoord opslaat in een veilige password manager voor toekomstig gebruik.

#### Stap 3: Aanmaken van een storage pool

1. Klik in de linkerzijbalk van de Proxmox webinterface op 'Datacenter' en vervolgens op 'Storage'.

2. Klik op de knop 'Add' om een nieuwe storage pool toe te voegen.

3. Voer een naam in voor de storage pool en selecteer het gewenste type opslag (bijvoorbeeld 'ZFS', 'LVM', 'Directory', etc.).

4. Configureer de gewenste opties voor de storage pool, zoals de locatie van de opslag, grootte, compressie-instellingen, enzovoort.

5. Klik op 'Create' om de storage pool aan te maken.

#### Stap 4: Configuratie van netwerkinterfaces

1. Klik in de linkerzijbalk van de Proxmox webinterface op 'Datacenter' en vervolgens op 'Network'.

2. Klik op de knop 'Create' om een nieuwe netwerkinterface te configureren.

3. Voer een naam in voor de netwerkinterface (bijvoorbeeld 'WAN') en selecteer het gewenste netwerkmodel (bijvoorbeeld 'Bridge' voor een fysieke interface of 'OVSBridge' voor een virtuele interface).

4. Configureer de gewenste netwerkinstellingen, zoals het toewijzen van de juiste fysieke netwerkadapter en het instellen van het IP-adres en de subnetmaskers voor de WAN-interface.

5. Herhaal dezelfde stappen om een tweede netwerkinterface te configureren voor het LAN-netwerk.

6. Zodra beide netwerkinterfaces zijn geconfigureerd, kunt u verder gaan met het instellen van de firewallregels en het routeren van verkeer tussen de WAN- en LAN-netwerken.

### Clusterconfiguratie voor hoge beschikbaarheid

De configuratie van een cluster voor hoge beschikbaarheid in Proxmox omvat:

- Het toevoegen van extra Proxmox-hosts aan het cluster.
- Configuratie van gedeelde opslag (bijv. via NFS of Ceph) voor het delen van virtuele machinebestanden tussen de hosts.
- Het configureren van failover-instellingen om automatische herstart van virtuele machines op beschikbare hosts mogelijk te maken bij uitval van een host.

### Opslagconfiguratie en -optimalisatie

- Gebruik van RAID-opstellingen voor redundantie en gegevensbescherming.
- Optimalisatie van opslagprestaties door gebruik te maken van SSD-cache of tiering.
- Implementatie van thin provisioning om efficiënter gebruik te maken van opslagruimte.

### Migratie van virtuele machines

- Gebruik van Proxmox-migratiefuncties om virtuele machines naadloos te verplaatsen tussen verschillende hosts binnen het cluster.
- Planning van migraties tijdens periodes van lage werkbelasting om de impact op de prestaties te minimaliseren.

### Integratie met monitoringtools voor prestatiebewaking

- Configuratie van Proxmox-integratie met monitoringtools zoals Prometheus en Grafana voor het bewaken van de prestaties van hosts en virtuele machines.
- Instellen van waarschuwingen en meldingen voor kritieke gebeurtenissen en prestatieproblemen.

---

## Firewall (pfSense)

   pfSense is een populaire open-source firewalloplossing die krachtige functies biedt voor netwerkbeveiliging en -beheer. Hier volgen gedetailleerde instructies voor beginners om pfSense te installeren en in te stellen binnen de Proxmox-omgeving:

### Installatie van pfSense in Proxmox

   1. Maak een nieuwe virtuele machine aan in Proxmox met de volgende specificaties:
      - CPU: Minimaal 1 core
      - RAM: Minimaal 1 GB
      - Opslag: Minimaal 8 GB
   2. Download het ISO-image van pfSense vanaf de officiële website: [https://www.pfsense.org/download/](https://www.pfsense.org/download/)
   3. Wijs het gedownloade ISO-image toe aan de nieuwe virtuele machine als het installatiemedium.
   4. Start de virtuele machine op en volg de installatiewizard van pfSense:
      - Kies "Install" in het bootmenu van pfSense.
      - Selecteer de optie om te installeren op de aangewezen harde schijf.
      - Bevestig de installatie en wacht tot het proces is voltooid.

### Setup van pfSense

   1. Nadat de installatie is voltooid, start de virtuele machine opnieuw op en volg de setup-wizard van pfSense:
      - Kies de gewenste configuratieoptie (bijv. "Quick/Easy Install").
      - Configureer de netwerkinterfaces:
         - Wijs het WAN-interface toe aan het externe netwerk (bijvoorbeeld de internetverbinding).
         - Wijs het LAN-interface toe aan het interne netwerk (bijvoorbeeld het lokale LAN).
      - Configureer het LAN IP-adres en subnetmasker.
   2. Voltooi de setup-wizard en log in op de webinterface van pfSense met de standaard referenties (standaard gebruikersnaam: "admin", standaard wachtwoord: "pfsense").

### Definiëren van toegangsregels en -beleid

   1. Navigeer naar het "Firewall" menu en selecteer "Rules".
   2. Voeg nieuwe firewallregels toe om het inkomende en uitgaande verkeer te beheren:
      - Maak regels voor het toestaan of blokkeren van specifieke poorten of protocollen.
      - Configureer regels voor het toestaan van verkeer van specifieke bronnen naar specifieke bestemmingen.
   3. Controleer en pas de standaard firewallregels aan volgens de beveiligingsvereisten van uw netwerk.

### Instellen van VPN-verbindingen

   1. Navigeer naar het "VPN" menu en selecteer "IPsec" of "OpenVPN" afhankelijk van uw voorkeur voor VPN-protocol.
   2. Configureer een nieuwe VPN-server of -client volgens uw vereisten:
      - Voor IPsec: Configureer fase 1 en fase 2 instellingen, evenals gebruikersaccounts.
      - Voor OpenVPN: Genereer en distribueer certificaten, configureer VPN-profielen en gebruikersauthenticatie.

### Monitoring en logboekregistratie

   1. Navigeer naar het "Diagnostics" menu en selecteer "System Logs" om systeem- en firewalllogboeken te bekijken.
   2. Configureer logging-niveaus en bewaar instellingen voor het bijhouden van gebeurtenissen en het oplossen van problemen.

### IDS en IPS configuratie

   1. Navigeer naar het "Services" menu en selecteer "Intrusion Detection".
   2. Configureer de IDS/IPS-instellingen, inclusief regelsets en detectieprofielen, om potentiële bedreigingen te identificeren en te blokkeren.

### Configuratie van verkeersvorming (QoS)

   1. Navigeer naar het "Firewall" menu en selecteer "Traffic Shaper" om Quality of Service (QoS) regels te configureren.
   2. Wijs prioriteiten toe aan specifieke soorten verkeer (bijv. VoIP, video, web) om de netwerkprestaties te verbeteren.

### Configuratie van netwerksegmentatie en VLAN's

   1. Navigeer naar het "Interfaces" menu en selecteer "VLANs" om virtuele LAN's te maken en netwerksegmentatie te implementeren.
   2. Wijs VLAN-tags toe aan specifieke interfaces en configureer VLAN-firewallregels om het verkeer tussen VLAN's te beheren.

---

## Windows Server 2019 R2

### Installatie van Windows Server 2019 R2 in Proxmox

1. Creëren van een nieuwe virtuele machine:

   - Log in op de Proxmox-beheerinterface.
   - Navigeer naar het gewenste opslagapparaat en klik op "Create VM" om een nieuwe virtuele machine te maken.
   - Volg de wizard en configureer de VM met de volgende specificaties:
      - Naam: Kies een beschrijvende naam voor de VM, bijvoorbeeld "Windows_Server_2019_R2".
      - OS: Selecteer "Microsoft Windows" en kies "Windows Server 2019 R2" als het besturingssysteem.
      - CPU: Wijs het gewenste aantal CPU-kernen toe aan de VM.
      - RAM: Bepaal de hoeveelheid RAM-geheugen voor de VM (bijvoorbeeld 4 GB).
      - Opslag: Wijs voldoende opslagruimte toe voor het besturingssysteem en eventuele toepassingen.
      - Netwerk: Selecteer het gewenste netwerkinterface-model (bijvoorbeeld 'VirtIO').
   - Klik op "Next" en vervolgens op "Finish" om de virtuele machine aan te maken.

2. Toewijzen van het ISO-image:

   - Selecteer de nieuwe virtuele machine in de lijst met VM's.
   - Klik op "Hardware" en vervolgens op "CD/DVD Drive".
   - Kies "Use CD/DVD disc image file (iso)" en selecteer het ISO-image van Windows Server 2019 R2 dat je eerder hebt gedownload.
   - Klik op "OK" om de wijzigingen op te slaan.

 3. Opstarten en doorlopen van de installatiestappen:

   - Start de virtuele machine op door erop te klikken en vervolgens op "Start" te drukken.
   - Volg de installatiewizard van Windows Server 2019 R2:
      - Kies de gewenste taal, tijd- en valutainstellingen en klik op "Next".
      - Klik op "Install now" om de installatie te starten.
      - Accepteer de licentievoorwaarden en klik op "Next".
      - Selecteer de installatietype (bij voorkeur "Custom: Install Windows only (advanced)").
      - Kies de doelschijf waarop je Windows Server 2019 R2 wilt installeren en klik op "Next".
      - Wacht tot de installatie is voltooid en volg de verdere instructies om de configuratie van het besturingssysteem te voltooien.

### Setup van Domain Controller en DHCP Server

1. Promoveren van de server tot een domeincontroller:

   - Na de installatie en eerste configuratie, log in op de Windows Server 2019 R2 VM met de juiste referenties.
   - Open de "Server Manager" en klik op "Add roles and features".
   - Selecteer "Active Directory Domain Services" en "DHCP Server" in de rolselectiewizard.
   - Volg de wizard om de rollen te installeren en start de server opnieuw op indien nodig.
   - Na het opnieuw opstarten, open de "Server Manager" opnieuw en klik op "Promote this server to a domain controller".
   - Kies "Add a new forest" als je een nieuw domein wilt maken, of selecteer "Add a domain controller to an existing domain" als je wilt toetreden tot een bestaand domein.
   - Volg de wizard en voer de nodige informatie in, inclusief het domeinnaam en de gebruikersreferenties.
   - Configureer de gewenste opties voor de DNS-server en voltooi de promotie van de domeincontroller.

2. Configuratie van DHCP-serverrollen en -bereiken:

   - Nadat de server is gepromoveerd tot een domeincontroller, open de "Server Manager" opnieuw.
   - Klik op "Add roles and features" en selecteer "DHCP Server" in de rolselectiewizard.
   - Volg de wizard om de DHCP-serverrol te installeren en start de server opnieuw op indien nodig.
   - Na het opnieuw opstarten, open de "DHCP Manager" en configureer de DHCP-bereiken voor het toewijzen van IP-adressen aan clients.
   - Voeg DHCP-bereiken toe voor het interne netwerk en configureer de relevante opties, zoals IP-bereiken, standaardgateways, DNS-servers, enzovoort.
   - Activeer de DHCP-server en controleer of deze correct werkt door clients aan te sluiten op het netwerk en te controleren of ze IP-adressen ontvangen van de DHCP-server.

### Setup van Active Directory

1. Aanmaken van gebruikers en groepen binnen Active Directory:

   - Log in op de Windows Server 2019 R2 VM met beheerdersrechten.
   - Open de "Server Manager" en klik op "Add roles and features".
   - Selecteer "Active Directory Domain Services" in de rolselectiewizard en volg de wizard om de rol te installeren.
   - Na de installatie, open "Active Directory Users and Computers" vanuit het "Tools" menu.
   - Maak nieuwe gebruikersaccounts aan door met de rechtermuisknop te klikken op de domeinnaam en te kiezen voor "New" > "User".
   - Volg de instructies om de benodigde informatie in te voeren, zoals gebruikersnaam, wachtwoord en gebruikersgroep.

2. Configuratie van groepsbeleid voor gebruikersinstellingen en toegangscontrole:

   - Open de "Group Policy Management" console vanuit het "Tools" menu.
   - Maak een nieuwe groepsbeleidsobject (GPO) aan en koppel deze aan de juiste organisatie-eenheid (OU) of het domein.
   - Bewerk het GPO om gebruikersinstellingen te configureren, zoals beperkingen voor software-installatie, bureaubladachtergrond, enzovoort.
   - Bewerk ook het GPO om toegangscontrole-instellingen te configureren, zoals het beheren van toegang tot gedeelde bronnen.

### Setup van File Server

1. Aanmaken van gedeelde mappen:

   - Open de "Server Manager" en klik op "File and Storage Services" > "Shares".
   - Klik op "Tasks" en selecteer "New Share".
   - Selecteer het pad naar de map die je wilt delen en configureer de gewenste machtigingen voor gebruikers en groepen.

2. Configuratie van toegangscontrole voor bestands- en maptoegang:

   - Ga terug naar "File and Storage Services" > "Shares".
   - Klik met de rechtermuisknop op de gedeelde map en kies "Properties".
   - Navigeer naar het tabblad "Security" en klik op "Edit" om de machtigingen voor gebruikers en groepen te configureren.
   - Voeg gebruikers en groepen toe en wijs de gewenste machtigingen toe, zoals lezen, schrijven, uitvoeren, enzovoort.

### Beveiligingsbeleid en gebruikersrechten

1. Configuratie van wachtwoordbeleid, accountvergrendeling en auditbeleid:

   - Open de "Group Policy Management" console en bewerk het relevante GPO.
   - Ga naar "Computer Configuration" > "Windows Settings" > "Security Settings" > "Account Policies".
   - Configureer het wachtwoordbeleid, accountvergrendeling en auditbeleid volgens de beveiligingsvereisten van je organisatie.

2. Toewijzen van specifieke gebruikersrechten:

   - Binnen dezelfde GPO, navigeer naar "Computer Configuration" > "Windows Settings" > "Security Settings" > "Local Policies" > "User Rights Assignment".
   - Wijs specifieke gebruikersrechten toe aan gebruikers en groepen, zoals het recht om de computer af te sluiten, het recht om de tijd te wijzigen, enzovoort.

### Back-up en herstelprocedures

1. Configuratie van Windows Server-back-up:

   - Open de "Server Manager" en navigeer naar "Windows Server Backup".
   - Klik op "Local Backup" en volg de wizard om een back-upschema te maken voor het regelmatig maken van back-ups van belangrijke gegevens.

2. Testen van herstelprocedures:

   - Maak een testomgeving of virtuele machine en probeer een herstel uit met behulp van de gemaakte back-ups.
   - Documenteer de herstelprocedure en zorg ervoor dat alle belangrijke gegevens met succes kunnen worden hersteld in geval van een noodsituatie.

---

