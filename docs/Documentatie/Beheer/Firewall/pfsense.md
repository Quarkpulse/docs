---
title: pfSense Firewall
subtitle:
description:
icon:
status: # nieuw updated outdated
search:
  boost: 2 
---

# pfSense (Firewall)

   pfSense is een populaire open-source firewalloplossing die krachtige functies biedt voor netwerkbeveiliging en -beheer. Hier volgen gedetailleerde instructies voor beginners om pfSense te installeren en in te stellen binnen de Proxmox-omgeving:

## Installatie van pfSense in Proxmox

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

## Setup van pfSense

   1. Nadat de installatie is voltooid, start de virtuele machine opnieuw op en volg de setup-wizard van pfSense:
      - Kies de gewenste configuratieoptie (bijv. "Quick/Easy Install").
      - Configureer de netwerkinterfaces:
         - Wijs het WAN-interface toe aan het externe netwerk (bijvoorbeeld de internetverbinding).
         - Wijs het LAN-interface toe aan het interne netwerk (bijvoorbeeld het lokale LAN).
      - Configureer het LAN IP-adres en subnetmasker.
   2. Voltooi de setup-wizard en log in op de webinterface van pfSense met de standaard referenties (standaard gebruikersnaam: "admin", standaard wachtwoord: "pfsense").

## Definiëren van toegangsregels en -beleid

   1. Navigeer naar het "Firewall" menu en selecteer "Rules".
   2. Voeg nieuwe firewallregels toe om het inkomende en uitgaande verkeer te beheren:
      - Maak regels voor het toestaan of blokkeren van specifieke poorten of protocollen.
      - Configureer regels voor het toestaan van verkeer van specifieke bronnen naar specifieke bestemmingen.
   3. Controleer en pas de standaard firewallregels aan volgens de beveiligingsvereisten van uw netwerk.

## Instellen van VPN-verbindingen

   1. Navigeer naar het "VPN" menu en selecteer "IPsec" of "OpenVPN" afhankelijk van uw voorkeur voor VPN-protocol.
   2. Configureer een nieuwe VPN-server of -client volgens uw vereisten:
      - Voor IPsec: Configureer fase 1 en fase 2 instellingen, evenals gebruikersaccounts.
      - Voor OpenVPN: Genereer en distribueer certificaten, configureer VPN-profielen en gebruikersauthenticatie.

## Monitoring en logboekregistratie

   1. Navigeer naar het "Diagnostics" menu en selecteer "System Logs" om systeem- en firewalllogboeken te bekijken.
   2. Configureer logging-niveaus en bewaar instellingen voor het bijhouden van gebeurtenissen en het oplossen van problemen.

## IDS en IPS configuratie

   1. Navigeer naar het "Services" menu en selecteer "Intrusion Detection".
   2. Configureer de IDS/IPS-instellingen, inclusief regelsets en detectieprofielen, om potentiële bedreigingen te identificeren en te blokkeren.

## Configuratie van verkeersvorming (QoS)

   1. Navigeer naar het "Firewall" menu en selecteer "Traffic Shaper" om Quality of Service (QoS) regels te configureren.
   2. Wijs prioriteiten toe aan specifieke soorten verkeer (bijv. VoIP, video, web) om de netwerkprestaties te verbeteren.

## Configuratie van netwerksegmentatie en VLAN's

   1. Navigeer naar het "Interfaces" menu en selecteer "VLANs" om virtuele LAN's te maken en netwerksegmentatie te implementeren.
   2. Wijs VLAN-tags toe aan specifieke interfaces en configureer VLAN-firewallregels om het verkeer tussen VLAN's te beheren.