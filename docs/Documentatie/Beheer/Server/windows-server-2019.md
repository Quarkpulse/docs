---
title: Windows Server 2019 R2
subtitle:
description:
icon:
status: # nieuw updated outdated
search:
  boost: 2 
---

# Windows Server 2019 R2

## Installatie van Windows Server 2019 R2 in Proxmox

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

## Setup van Domain Controller en DHCP Server

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

## Setup van Active Directory

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

## Setup van File Server

1. Aanmaken van gedeelde mappen:

   - Open de "Server Manager" en klik op "File and Storage Services" > "Shares".
   - Klik op "Tasks" en selecteer "New Share".
   - Selecteer het pad naar de map die je wilt delen en configureer de gewenste machtigingen voor gebruikers en groepen.

2. Configuratie van toegangscontrole voor bestands- en maptoegang:

   - Ga terug naar "File and Storage Services" > "Shares".
   - Klik met de rechtermuisknop op de gedeelde map en kies "Properties".
   - Navigeer naar het tabblad "Security" en klik op "Edit" om de machtigingen voor gebruikers en groepen te configureren.
   - Voeg gebruikers en groepen toe en wijs de gewenste machtigingen toe, zoals lezen, schrijven, uitvoeren, enzovoort.

## Beveiligingsbeleid en gebruikersrechten

1. Configuratie van wachtwoordbeleid, accountvergrendeling en auditbeleid:

   - Open de "Group Policy Management" console en bewerk het relevante GPO.
   - Ga naar "Computer Configuration" > "Windows Settings" > "Security Settings" > "Account Policies".
   - Configureer het wachtwoordbeleid, accountvergrendeling en auditbeleid volgens de beveiligingsvereisten van je organisatie.

2. Toewijzen van specifieke gebruikersrechten:

   - Binnen dezelfde GPO, navigeer naar "Computer Configuration" > "Windows Settings" > "Security Settings" > "Local Policies" > "User Rights Assignment".
   - Wijs specifieke gebruikersrechten toe aan gebruikers en groepen, zoals het recht om de computer af te sluiten, het recht om de tijd te wijzigen, enzovoort.

## Back-up en herstelprocedures

1. Configuratie van Windows Server-back-up:

   - Open de "Server Manager" en navigeer naar "Windows Server Backup".
   - Klik op "Local Backup" en volg de wizard om een back-upschema te maken voor het regelmatig maken van back-ups van belangrijke gegevens.

2. Testen van herstelprocedures:

   - Maak een testomgeving of virtuele machine en probeer een herstel uit met behulp van de gemaakte back-ups.
   - Documenteer de herstelprocedure en zorg ervoor dat alle belangrijke gegevens met succes kunnen worden hersteld in geval van een noodsituatie.