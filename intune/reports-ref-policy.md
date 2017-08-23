---
title: Beleid | Microsoft Docs
description: Naslagonderwerp voor de categorie Beleid van entiteitverzamelingen in de Intune-datawarehouse-API.
keywords: Intune-datawarehouse
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: D5ADB9D8-D46A-43BD-AB0F-D6927508E3F4
ms.reviewer: jeffgilb
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 6af0ff1f463c153e62f6df63ce811076c5f692f2
ms.sourcegitcommit: addf6a40caa22c22adfd2e2eff7d666cd1877e3c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2017
---
# <a name="reference-for-policy-entities"></a>Naslag voor beleidsentiteiten

De categorie **Beleid** bevat entiteiten voor mobiele apparaten waarmee gegevens worden bijgehouden, zoals:

  -  Inventarisatie van apparaatconfiguratieprofielen, app-configuratieprofielen en nalevingsbeleid  
  -  Aantal apparaten met de status Geslaagd, In behandeling, Mislukt of Fout per dag  
  -  Aantal gebruikers met de status Geslaagd, In behandeling, Mislukt of Fout per dag  
  -  Cumulatief aantal apparaten met de status Geslaagd, In behandeling, Mislukt of Fout  

## <a name="policy"></a>Beleid

De entiteit **Policy** bevat apparaatconfiguratieprofielen, app-configuratieprofielen en nalevingsbeleid. U kunt het beleid met MDM (Mobile Device Management) toewijzen aan een groep in uw onderneming.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| PolicyKey |Een unieke sleutel voor het beleid in het datawarehouse |123 |
| PolicyId |Een unieke id van het beleid in het datawarehouse |b66bc706-ffff-7437-0340-032819502773 |
| PolicyName |De naam van het beleid |"Windows 10 Baseline" |
| PolicyVersion |De versie van het beleid. Wanneer het beleid wordt gewijzigd, wordt er een nieuwere versie gemaakt. |1, 2, 3 |
| IsDeleted |Geeft aan of de beleidsrecord is bijgewerkt.  Waar: het beleid heeft een nieuwe record met bijgewerkte velden. Onwaar: de meest recente record voor het beleid. |Waar/onwaar |
| StartDateInclusiveUTC |De datum en tijd in UTC waarop het beleid is gemaakt in het datawarehouse |11/23/2016 12:00:00 AM |
| DeletedDateUTC |De datum en tijd in UTC waarop IsDeleted is gewijzigd in Waar |11/23/2016 12:00:00 AM |
| RowLastModifiedDateTimeUTC |De datum en tijd in UTC waarop het beleid het laatst is gewijzigd in het datawarehouse |11/23/2016 12:00:00 AM |

## <a name="policytype"></a>PolicyType

De entiteit **PolicyType** bevat typen apparaatconfiguratieprofielen, app-configuratieprofielen en nalevingsbeleid. U kunt het beleid met MDM (Mobile Device Management) toewijzen aan een groep in uw onderneming.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| PolicyTypeId |Een unieke id van het beleid in het bronsysteem |123 |
| PolicyTypeKey |Een unieke id van het beleid in het datawarehouse |1 |
| PolicyTypeName |De naam van het beleidstype |Windows 10 Compliance policy |

## <a name="deviceconfiguration"></a>DeviceConfiguration

De entiteit **DeviceConfigurationProfileDeviceActivity** bevat het aantal apparaten met de status geslaagd, in behandeling, mislukt of fout per dag. Het aantal weerspiegelt de apparaatconfiguratieprofielen die zijn toegewezen aan de entiteit. Als een apparaat bijvoorbeeld voor alle toegewezen beleidsregels de status Geslaagd heeft, wordt de teller voor die status met één opgehoogd voor die dag. Als aan een apparaat twee profielen zijn toegewezen, één met de status Geslaagd en het andere profiel met de status Fout, wordt de teller Geslaagd met één opgehoogd en wordt het apparaat in de foutstatus geplaatst. De entiteit geeft voor de afgelopen 30 dagen aan hoeveel apparaten op een bepaalde dag een bepaalde status hebben.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| DateKey |De datum waarop het inchecken van het apparaatconfiguratieprofiel is vastgelegd in het datawarehouse |20160703 |
| In behandeling |Aantal unieke apparaten met de status In behandeling |123 |
| Geslaagd |Aantal unieke apparaten met de status Geslaagd |12 |
| Fout |Aantal unieke apparaten met de status Fout |10 |
| Mislukt |Aantal unieke apparaten met de status Mislukt |2 |

## <a name="userconfiguration"></a>UserConfiguration

De entiteit **UserConfigurationProfileDeviceActivity** bevat het aantal gebruikers met de status Geslaagd, In behandeling, Mislukt of Fout per dag. Het aantal weerspiegelt de apparaatconfiguratieprofielen die zijn toegewezen aan de entiteit. Als een gebruiker bijvoorbeeld voor alle toegewezen beleidsregels de status Geslaagd heeft, wordt de teller voor die status met één opgehoogd voor die dag. Als aan een gebruiker twee profielen zijn toegewezen, één met de status Geslaagd en het andere profiel met de status Fout, wordt de gebruiker in de foutstatus geplaatst.  De entiteit **UserConfigurationProfileDeviceActivity** geeft voor de afgelopen 30 dagen aan hoeveel gebruikers op een bepaalde dag een bepaalde status hebben.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| DateKey |De datum waarop het inchecken van het apparaatconfiguratieprofiel is vastgelegd in het datawarehouse |20160703 |
| In behandeling |Aantal unieke gebruikers met de status In behandeling |123 |
| Geslaagd |Aantal unieke gebruikers met de status Geslaagd |12 |
| Fout |Aantal unieke gebruikers met de status Fout |10 |
| Mislukt |Aantal unieke gebruikers met de status Mislukt |2 |

## <a name="policytypeactivity"></a>PolicyTypeActivity

De entiteit **PolicyTypeActivity** bevat het cumulatieve aantal apparaten met de status Geslaagd, In behandeling, Mislukt of Fout. Deze statuswaarden verwijzen naar een apparaatconfiguratieprofiel, app-configuratieprofiel of nalevingsbeleid per dag.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| DateKey |De datum waarop het inchecken van het apparaatconfiguratieprofiel is vastgelegd in het datawarehouse |20160703 |
| PolicyKey |Beleidssleutel, kan worden samengevoegd met Policy om de naam van het beleid op te halen |Windows 10 baseline |
| PolicyTypeKey |Het type beleidssleutel, kan worden samengevoegd met PolicyType om de naam van het beleidstype op te halen |Windows10Compliance Policy |
| In behandeling |Aantal unieke apparaten met de status In behandeling |123 |
| Geslaagd |Aantal unieke apparaten met de status Geslaagd |12 |
| Fout |Aantal unieke apparaten met de status Fout |10 |
| Mislukt |Aantal unieke apparaten met de status Mislukt |2 |