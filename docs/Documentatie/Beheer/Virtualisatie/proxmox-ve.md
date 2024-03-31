# Virtualisatie

In de servervirtualisatie wereld zijn er verschillende platforms beschikbaar, waaronder VMWare, Hyper-V, KVM en Proxmox. Elk van deze platforms heeft zijn eigen kenmerken, voordelen en toepassingsgebieden.

VMware is een van de meest bekende en gevestigde virtualisatieplatformen, maar het vereist vaak licenties en kan duur zijn voor kleine en middelgrote bedrijven. Hyper-V, ontwikkeld door Microsoft, is een ander populair platform dat vaak wordt gebruikt in Windows-omgevingen.

Proxmox, aan de andere kant, is een open-source virtualisatieplatform dat gebaseerd is op KVM (Kernel-based Virtual Machine) en LXC (Linux Containers). Het biedt een kosteneffectieve oplossing met een breed scala aan functies, waaronder krachtige virtualisatie, clusterondersteuning voor hoge beschikbaarheid en een gebruiksvriendelijke webinterface. Daarom hebben we ervoor gekozen om Proxmox te gebruiken in deze documentatie vanwege zijn flexibiliteit, gebruiksgemak en kosteneffectiviteit voor kleine en middelgrote bedrijven.

## Hardwarevereisten (standaard en aanbevolen)

Om Proxmox succesvol te kunnen installeren en uitvoeren, zijn er bepaalde hardwarevereisten waaraan moet worden voldaan. Deze omvatten:

- **Processor:** Een moderne multi-core processor met virtualisatieondersteuning (bijvoorbeeld Intel VT-x of AMD-V).
- **Geheugen (RAM):** Minimaal 4 GB RAM voor de hostserver, maar aanbevolen wordt 8 GB of meer voor optimale prestaties.
- **Opslag:** Voldoende opslagruimte voor het besturingssysteem van de hostserver, evenals voor de opslag van virtuele machines (aanbevolen wordt SSD-opslag voor betere prestaties).
- **Netwerk:** Ten minste één Ethernet-netwerkinterfacekaart voor netwerkconnectiviteit.

## Installatie van Proxmox

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


### Stap 1: Voorbereiding

* Zet de server onder elektrische stroom. Het wordt aanbevolen om de server aan te sluiten op een UPS (Uninterruptible Power Supply) om stroomonderbrekingen te voorkomen tijdens het installatieproces.

   ![Server met UPS](link-naar-afbeelding)

* Start de server op en wacht tot het BIOS/UEFI-scherm verschijnt.

### Stap 2: Opstarten vanaf de installatiemedia

* Plaats het opstartbare USB-flashstation met Proxmox in een USB-poort van de server.

* Start de server opnieuw op en druk op de juiste toets (bijvoorbeeld F12, DEL, of ESC, afhankelijk van het moederbord) om het opstartmenu te openen.

* Selecteer het USB-flashstation als opstartapparaat en druk op Enter.

   ![Opstartmenu](link-naar-afbeelding)


### Stap 3: Proxmox installatiewizard

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

### Stap 4: Installatie voltooien

1. Wacht tot de installatie van Proxmox is voltooid. Dit kan enkele minuten duren, afhankelijk van de prestaties van uw server.

2. Nadat de installatie is voltooid, wordt u gevraagd om een wachtwoord in te stellen voor de 'root'-gebruiker van Proxmox. Voer een sterk wachtwoord in en bevestig het.

   ![Wachtwoord instellen](link-naar-afbeelding)

3. Wanneer de installatie is voltooid, wordt u begroet met het Proxmox inlogscherm. U kunt nu inloggen met de gebruikersnaam 'root' en het wachtwoord dat u hebt ingesteld tijdens de installatie.

   ![Inlogscherm](link-naar-afbeelding)


## Proxmox setup

Voordat we beginnen met het configureren van Proxmox, is het belangrijk om enkele best practices te bespreken met betrekking tot netwerkconfiguratie. Voor een efficiënte en veilige werking van uw Proxmox-omgeving is het aan te raden om gebruik te maken van private IP-adressen binnen een betrouwbaar IP-bereik, zoals gedefinieerd in RFC 1918. Overweeg om de volgende IP-bereiken te gebruiken:

WAN-interface: U kunt een publiek IP-adres toewijzen dat is verstrekt door uw internetprovider. Als u een privénetwerk gebruikt voor de WAN-interface, kies dan een IP-adres uit het publieke IP-bereik dat niet overlapt met IP-adressen die door andere netwerken worden gebruikt.
LAN-interface: Voor het LAN-netwerk kunt u een privé IP-bereik uit de volgende RFC 1918-adresruimtes gebruiken:

```
* 10.0.0.0/8
* 172.16.0.0/12
* 192.168.0.0/16
```

Zorg ervoor dat u subnetmaskers toepast die geschikt zijn voor uw netwerkvereisten en vermijd het gebruik van IP-adressen die mogelijk conflicteren met andere apparaten in uw netwerk.

### Stap 1: Eerste login

1. Open een webbrowser (Edge of Chrome) op een computer in hetzelfde netwerk als de Proxmox-server.

2. Typ het IP-adres van de Proxmox-server in de adresbalk van de browser en druk op Enter.

3. U wordt begroet met het Proxmox inlogscherm. Log in met de gebruikersnaam 'root' en het wachtwoord dat u hebt ingesteld tijdens de installatie.

   ![Inlogscherm Proxmox](link-naar-afbeelding)

### Stap 2: Root wachtwoord wijzigen

1. Nadat u bent ingelogd, wordt u gevraagd om het wachtwoord voor de 'root'-gebruiker te wijzigen. Voer een nieuw sterk wachtwoord in en bevestig het.

2. Het nieuwe wachtwoord is nu ingesteld voor de 'root'-gebruiker. Documenteer en zorg ervoor dat u dit wachtwoord opslaat in een veilige password manager voor toekomstig gebruik.

### Stap 3: Aanmaken van een storage pool

1. Klik in de linkerzijbalk van de Proxmox webinterface op 'Datacenter' en vervolgens op 'Storage'.

2. Klik op de knop 'Add' om een nieuwe storage pool toe te voegen.

3. Voer een naam in voor de storage pool en selecteer het gewenste type opslag (bijvoorbeeld 'ZFS', 'LVM', 'Directory', etc.).

4. Configureer de gewenste opties voor de storage pool, zoals de locatie van de opslag, grootte, compressie-instellingen, enzovoort.

5. Klik op 'Create' om de storage pool aan te maken.

### Stap 4: Configuratie van netwerkinterfaces

1. Klik in de linkerzijbalk van de Proxmox webinterface op 'Datacenter' en vervolgens op 'Network'.

2. Klik op de knop 'Create' om een nieuwe netwerkinterface te configureren.

3. Voer een naam in voor de netwerkinterface (bijvoorbeeld 'WAN') en selecteer het gewenste netwerkmodel (bijvoorbeeld 'Bridge' voor een fysieke interface of 'OVSBridge' voor een virtuele interface).

4. Configureer de gewenste netwerkinstellingen, zoals het toewijzen van de juiste fysieke netwerkadapter en het instellen van het IP-adres en de subnetmaskers voor de WAN-interface.

5. Herhaal dezelfde stappen om een tweede netwerkinterface te configureren voor het LAN-netwerk.

6. Zodra beide netwerkinterfaces zijn geconfigureerd, kunt u verder gaan met het instellen van de firewallregels en het routeren van verkeer tussen de WAN- en LAN-netwerken.

## Clusterconfiguratie voor hoge beschikbaarheid

De configuratie van een cluster voor hoge beschikbaarheid in Proxmox omvat:

- Het toevoegen van extra Proxmox-hosts aan het cluster.
- Configuratie van gedeelde opslag (bijv. via NFS of Ceph) voor het delen van virtuele machinebestanden tussen de hosts.
- Het configureren van failover-instellingen om automatische herstart van virtuele machines op beschikbare hosts mogelijk te maken bij uitval van een host.

## Opslagconfiguratie en -optimalisatie

- Gebruik van RAID-opstellingen voor redundantie en gegevensbescherming.
- Optimalisatie van opslagprestaties door gebruik te maken van SSD-cache of tiering.
- Implementatie van thin provisioning om efficiënter gebruik te maken van opslagruimte.

## Migratie van virtuele machines

- Gebruik van Proxmox-migratiefuncties om virtuele machines naadloos te verplaatsen tussen verschillende hosts binnen het cluster.
- Planning van migraties tijdens periodes van lage werkbelasting om de impact op de prestaties te minimaliseren.

## Integratie met monitoringtools voor prestatiebewaking

- Configuratie van Proxmox-integratie met monitoringtools zoals Prometheus en Grafana voor het bewaken van de prestaties van hosts en virtuele machines.
- Instellen van waarschuwingen en meldingen voor kritieke gebeurtenissen en prestatieproblemen.