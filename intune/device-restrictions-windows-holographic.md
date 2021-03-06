---
title: Instellingen van Microsoft Intune voor apparaatbeperkingen voor Windows Holographic for Business
titleSuffix: ''
description: Meer informatie over de Intune-instellingen die u kunt gebruiken voor het beheren van apparaatinstellingen en functionaliteit op apparaten met Windows Holographic for Business.
keywords: ''
author: vhorne
ms.author: victorh
manager: dougeby
ms.date: 3/6/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 694b81434a95f48abc98f5012460523420df58cc
ms.sourcegitcommit: df60d03a0ed54964e91879f56c4ef0a7507c17d4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/22/2018
---
# <a name="microsoft-intune-windows-holographic-for-business-device-restriction-settings"></a>Instellingen voor apparaatbeperkingen voor Microsoft Intune Windows Holographic for Business

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

De volgende instellingen voor apparaatbeperking worden ondersteund op apparaten met Windows Holographic for Business, zoals Microsoft Hololens.

## <a name="general"></a>Algemeen

- **Registratie handmatig ongedaan maken**: hiermee kan de gebruiker het werkplekaccount handmatig van het apparaat verwijderen.
- **Cortana**: hiermee schakelt u de spraakassistent Cortana in en uit.
- **Geolocatie**: hiermee geeft u aan of op het apparaat gegevens van locatieservices kunnen worden gebruikt.



## <a name="password"></a>Wachtwoord
-   **Wachtwoord**: hiermee geeft u aan dat de eindgebruiker een wachtwoord moet invoeren voor toegang tot het apparaat.
    -   **Wachtwoord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status**: hiermee geeft u aan dat de gebruiker een wachtwoord moet opgeven om het apparaat te ontgrendelen.



## <a name="app-store"></a>App Store

-   **Apps uit Store automatisch bijwerken**: apps die zijn geïnstalleerd vanuit Microsoft Store, kunnen automatisch worden bijgewerkt.
-   **Installatie van vertrouwde app**: voor apps die zijn ondertekend met een vertrouwd certificaat is sideloaden mogelijk.
-   **Ontgrendeling voor ontwikkelaars**: de eindgebruiker mag instellingen voor Windows-ontwikkelaars wijzigen, zoals het toestaan van sideloaden van apps.

## <a name="edge-browser"></a>Microsoft Edge-browser

-   **Microsoft Edge-browser**: hiermee staat u het gebruik van de Edge-webbrowser toe op het apparaat.
-   **Cookies**: hiermee kunnen internetcookies in de browser op het apparaat worden opgeslagen.
-   **Pop-ups**: hiermee kunt u pop-upvensters in de browser blokkeren (alleen van toepassing op Windows 10-desktop).
-   **Zoeksuggesties**: hiermee kan de zoekmachine sites voorstellen wanneer er zoektermen worden getypt.
-   **Wachtwoordbeheer**: hiermee schakelt u de functie Wachtwoordbeheer van Microsoft Edge in of uit.
- **Do Not Track-headers verzenden**: hiermee configureert u de Microsoft Edge-browser zodanig, dat verzoeken om niet gevolgd te worden, worden verzonden naar websites die gebruikers bezoeken.

## <a name="windows-defender-smart-screen"></a>Windows Defender Smart Screen

- **SmartScreen voor Microsoft Edge**: schakel Edge SmartScreen in voor toegang tot site- en bestanddownloads.

## <a name="search"></a>Zoeken
- **Zoeklocatie**: geef op of een zoekactie locatiegegevens mag gebruiken. informatie


## <a name="cloud-and-storage"></a>Cloud en opslag
-   **Microsoft-account**: hiermee staat u toe dat de gebruiker een Microsoft-account aan het apparaat kan koppelen.

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

-   **Bluetooth**: hiermee bepaalt u of de gebruiker Bluetooth op het apparaat kan inschakelen en configureren.
-   **Bluetooth-detectie**: hiermee geeft u aan dat het apparaat kan worden gedetecteerd door andere Bluetooth-apparaten.
-   **Aankondigingen via Bluetooth**: hiermee geeft u aan dat het apparaat aankondigingen via Bluetooth kan ontvangen.

## <a name="control-panel-and-settings"></a>Configuratiescherm en instellingen

- **Systeemtijd wijzigen**: hiermee voorkomt u dat de eindgebruiker de datum en tijd van het apparaat wijzigt.

## <a name="reporting-and-telemetry"></a>Rapportage en telemetrie

- **Gebruiksgegevens delen**: selecteer het niveau voor het verzenden van diagnostische gegevens.