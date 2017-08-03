---
title: Energieverbruikoptimalisatie verhindert toegang tot e-mail | Microsoft Docs
description: Informatie over het uitschakelen van energieverbruikoptimalisatie voor Android om ervoor te zorgen dat uw e-mail wordt opgehaald.
keywords: 
author: barlanmsft
ms.author: barlan
manager: angrobe
ms.date: 07/07/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: ad713f18-40a9-421f-aa2b-f8c21028d57c
searchScope: User help
ROBOTS: 
ms.reviewer: maxles
ms.suite: ems
ms.custom: intune-enduser
ms.openlocfilehash: d94e3a79af1951debc4dd04413efff8f4c716545
ms.sourcegitcommit: d2a4f4477b3bf90aac6a9db77d41747e64ad7df4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2017
---
# <a name="outlook-wont-sync-managed-email-when-battery-optimization-for-android-is-turned-on"></a>Outlook synchroniseert beheerde e-mail niet wanneer de energieverbruikoptimalisatie voor Android is ingeschakeld

> [!IMPORTANT]
> Dit probleem wordt hier beschreven omdat hierover een toenemend aantal klantrapporten is ontvangen. Als dit probleem zich blijft voordoen nadat u deze stappen hebt uitgevoerd, neem dan contact op met [uw IT-beheerder](https://portal.manage.microsoft.com) voor meer informatie.

Door uw apparaat bij Intune te registreren, kunt u profiteren van de toegang tot bedrijfsbronnen. Een van de meest voorkomende bronnen is toegang tot e-mail. Een probleem dat we hebben gezien met toegang tot e-mail via Outlook voor Android-apparaten is wanneer de energieverbruikoptimalisatie is ingeschakeld. Energieverbruikoptimalisatie wordt mogelijk automatisch ingeschakeld om uw apparaat zo lang mogelijk ingeschakeld te houden. Energieverbruikoptimalisatie kan u op deze manier deels helpen omdat deze probeert automatisch e-maildownloads te stoppen.

Het Microsoft Intune-team werkt actief aan een oplossing voor dit probleem. Een manier om te voorkomen dat het apparaat de energiebesparende modus activeert, is door ervoor te zorgen dat de batterij steeds voor meer dan 30% is geladen. Als u het probleem wilt voorkomen wanneer de energiebesparende modus wordt geactiveerd, moet u de bedrijfsportal en Outlook verwijderen uit de lijst met apps die worden beïnvloed door energieverbruikoptimalisatie en instellingen voor energiebesparing .

Er zijn veel Android-apparaten die door veel fabrikanten worden gemaakt. We kunnen niet de exacte stappen documenteren die u moet uitvoeren voor elk apparaat. Mogelijk moet u deze maatregelen alleen in uw systeeminstellingen nemen of ook in bepaalde fabrikantspecifieke instellingen. We hebben enkele algemene voorbeelden gegeven hoe u dit probleem op Android-apparaten kunt oplossen.

## <a name="unmodified-android-devices"></a>Ongewijzigde Android-apparaten

Veel fabrikanten voegen wijzigingen toe aan hun Android-apparaten. Dit kan invloed hebben op bepaalde manieren waarop u met het apparaat communiceert, zoals thema's en meldingen. Google maakt doorgaans niet van dit soort wijzigingen in hun telefoons. Op een Google Pixel-apparaat met Android 7.0 of hoger moet u bijvoorbeeld deze stappen volgen voor het verwijderen van deze apps uit de energieverbruikoptimalisatie:

1. Open **instellingen**.
2. Tik op **Batterij** > **Meer** > **Batterijoptimalisatie**.
3. Tik op Pijl-omlaag en vervolgens op**Niet optimaliseren**.
4. Selecteer de bedrijfsportal- en Outlook-apps en schakel energieverbruikoptimalisatie uit.

## <a name="samsung-devices"></a>Samsung-apparaten

Voor andere soorten Android-apparaten, zoals Samsung-apparaten met Android 7.0 of hoger, zou u andere stappen moeten uitvoeren om de Outlook- en bedrijfsportal-apps uit de energieverbruikoptimalisatie te verwijderen.

1. Open **instellingen**.
2. Tik op **Menu (...)**  > **Speciale toegang** > **Batterijgebruik optimaliseren**.
3. Selecteer **Alle apps** uit de vervolgkeuzelijst.
4. Selecteer **Uit** op de wisselknop naast de bedrijfsportal- en Outlook-apps en schakel energieverbruikoptimalisatie uit.

Als u een Samsung-apparaat met een lagere Android-versie gebruikt, zou u als volgt te werk moeten gaan om deze apps uit de energieverbruikoptimalisatie te verwijderen.

1. Open **instellingen**.
2. Tik op **Apparaatonderhoud** > **Batterij** > **Ongecontroleerde apps**.
3. Klik op **Apps toevoegen**.
4. Selecteer de bedrijfsportal- en Outlook-apps en klik op **Gereed**.

## <a name="oneplus-devices"></a>OnePlus-apparaten

Een ander voorbeeld om deze instellingen op een andere manier te vinden is via het zoeken in de systeeminstellingen. Op een OnePlus 3 met Android 7.1.1 bijvoorbeeld, moet u deze stappen volgen: 

1. Open **Systeeminstellingen**. 
2. Tik op de knop **Zoeken**. Deze lijkt op een vergrootglas rechtsbovenaan het scherm. 
3. Type **batterijoptimalisatie** in het zoekvak, selecteer vervolgens in het scherm**Instellingen** dat verschijnt, de optie **Batterijoptimalisatie**. 
4. Tik op **Batterij** > **Batterijoptimalisatie**.
5. Selecteer de bedrijfsportal- en Outlook-apps en selecteer vervolgens **Niet optimaliseren**. Tik op **Gereed**.

<!--On a OnePlus 5 device with Android 7.1.1, you would follow these steps to remove these apps from battery optimization:
1. Open **Settings**.
2. Tap **Battery** > **Battery optimization**.
3. Select the Company Portal and Outlook apps, then select **Don’t optimize**. Tap **Done**.-->

Nog hulp nodig? Neem contact op met uw IT-beheerder. Ga naar de [bedrijfsportalwebsite](http://portal.manage.microsoft.com) voor de betreffende contactgegevens.