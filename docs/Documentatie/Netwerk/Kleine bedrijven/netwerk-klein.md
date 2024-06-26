---
title: Netwerkarchitectuur voor een Klein Bedrijf
subtitle:
description:
icon:
status: # nieuw updated outdated
search:
  boost: 2 
---

# Netwerkarchitectuur voor een Klein Bedrijf

1. **Internet Service Provider (ISP):** Het bedrijf ontvangt internetconnectiviteit via een ADSL-modem van Telesur, dat fungeert als de toegangspoort tot het internet.

2. **Firewall (pfSense):** De pfSense firewall wordt gebruikt om het netwerk te beschermen tegen ongeautoriseerde toegang vanaf externe bronnen en om het interne netwerkverkeer te beheren. Het fungeert als de primaire gateway voor het interne netwerk.

3. **Opslag en Backup (Synology DS224+):** De Synology DS224 wordt gebruikt voor opslag en back-updoeleinden. Het biedt gecentraliseerde opslagmogelijkheden voor bestanden en gegevens van het bedrijf en fungeert mogelijk ook als een back-upoplossing voor belangrijke bedrijfsgegevens.

4. **Switch:** Een switch wordt gebruikt om meerdere netwerkapparaten met elkaar te verbinden en het netwerkverkeer tussen deze apparaten te routeren. Het fungeert als een lokale verbindingshub voor de werkstations, de accesspoint en andere netwerkapparaten.

5. **Access Point voor Draadloos Netwerk:** Een draadloos accesspoint wordt gebruikt om draadloze connectiviteit te bieden aan de medewerkers van het bedrijf. Het accesspoint zendt een draadloos signaal uit voor verbinding met draadloze apparaten zoals laptops, smartphones en tablets. Het draadloze netwerk opereert bijvoorbeeld op het subnet 192.168.1.0/24.

6. **Werkstations:** Er zijn 3 tot 5 werkstations aanwezig die worden gebruikt door de medewerkers van het bedrijf. Deze werkstations zijn verbonden met het interne netwerk en hebben toegang tot gedeelde bronnen, internet en andere netwerkapparaten.

7. **Draadloos Gastennetwerk:** Een apart gastennetwerk wordt geïmplementeerd bijvoorbeeld op het subnet 10.0.1.0/24 voor klanten en bezoekers van het bedrijf. Dit netwerk is gescheiden van het interne netwerk van het bedrijf en biedt alleen internettoegang zonder toegang tot interne bronnen of gevoelige informatie.

Hier is een vereenvoudigd diagram van het netwerkarchitectuur:

```mermaid
graph TD;
    A[Telesur ADSL Modem] -->|Ethernet| B[pfSense Firewall];
    B -->|Ethernet| C[Switch];
    C -->|Ethernet| D[Synology DS224+];
    C -->|Ethernet| E[Access Point];
    C -->|Ethernet| F[Werkstations];
    F -->|Wi-Fi| E;
    G[Draadloos Gasten Netwerk] -->|Wi-Fi| E;
```

Dit diagram toont de verbindingen tussen de verschillende netwerkcomponenten en de stroom van gegevens door het netwerk. De firewall fungeert als een centraal punt voor de netwerkbeveiliging, terwijl de switch zorgt voor connectiviteit tussen alle apparaten in het netwerk.

