---
title: iOS-apparaten inschrijven - Apple Configurator en Configuratieassistent
titleSuffix: Intune on Azure
description: In dit onderwerp leest u hoe u Apple Configurator kunt gebruiken om iOS-apparaten die bedrijfseigendom zijn in te schrijven met Configuratieassistent.
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 07/28/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6d384cd0-b662-41e7-94f5-0c96790ab20a
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: fb3ea2fbd8d710bcb8eccac9b4512ce8ba941fc2
ms.sourcegitcommit: 7674efb7de5ad54390801165364f5d9c58ccaf84
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/05/2017
---
# <a name="enroll-ios-devices-with-apple-configurator"></a>iOS-apparaten inschrijven met Apple Configurator

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune ondersteunt het inschrijven van iOS-apparaten met behulp van het hulpprogramma [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) dat wordt uitgevoerd op een Mac-computer. Inschrijving met Apple Configurator vereist dat u voor elk iOS-apparaat een USB-verbinding instelt met een Mac-computer voor het instellen van een zakelijke inschrijving. U kunt apparaten op twee manieren apparaten inschrijven bij Intune met Apple Configurator:
- **Inschrijving met iOS-configuratieassistent**: het apparaat wordt naar de fabrieksinstelling teruggezet en voorbereid voor inschrijving tijdens het uitvoeren van Configuratieassistent.
- **Directe inschrijving**: het apparaat wordt niet teruggezet naar de fabrieksinstellingen en het apparaat wordt via iOS-instellingen geregistreerd. Deze methode ondersteunt apparaten **zonder gebruikersaffiniteit**.

Inschrijven met Apple Configurator kan niet worden gebruikt met de [apparaatinschrijvingsmanager](device-enrollment-manager-enroll.md).

## <a name="prerequisites"></a>Vereisten

- Fysieke toegang tot iOS-apparaten
- [MDM-instantie instellen](mdm-authority-set.md)
- [Een Apple MDM-pushcertificaat](apple-mdm-push-certificate-get.md)
- Apparaatserienummers (alleen inschrijving met de iOS-configuratieassistent)
- USB-verbindingskabels
- Mac waarop [Apple Configurator 2.0](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) wordt uitgevoerd

## <a name="create-an-apple-configurator-profile-for-devices"></a>Een Apple Configurator-profiel maken voor apparaten

Met een inschrijvingsprofiel voor apparaten worden de instellingen tijdens het inschrijven gedefinieerd. Deze instellingen worden slechts eenmaal toegepast. Volg deze stappen om een inschrijvingsprofiel te maken om iOS-apparaten in te schrijven met Apple Configurator.

1. Meld u aan bij Azure Portal.
2. Kies **Meer services** > **Bewaking en beheer** > **Intune**.
3. Kies **Apparaatinschrijving** > **Apple-inschrijving**.
4. Selecteer **AC-profielen** in **Instellingen van de inschrijving met Apple Configurator beheren**.
5. Selecteer **Maken** op de blade **Apple Configurator-inschrijvingsprofielen**.
6. Typ een **naam** en **beschrijving** voor het profiel (voor administratieve doeleinden). Gebruikers zien deze gegevens niet. U kunt dit veld Naam gebruiken om een dynamische groep te maken in Azure Active Directory. Gebruik de profielnaam om de parameter enrollmentProfileName te definiëren om apparaten aan dit inschrijvingsprofiel toe te wijzen. Meer informatie over dynamische Azure Active Directory-groepen.

  ![Schermafbeelding van het scherm Profiel maken met Inschrijven met gebruikersaffiniteit geselecteerd](./media/apple-configurator-profile-create.png)

7. Geef de **gebruikersaffiniteit** op:
   - **Inschrijven met gebruikersaffiniteit**: het apparaat moet aan een gebruiker worden gekoppeld met de iOS-configuratieassistent en kan vervolgens toegang krijgen tot gegevens en e-mail van het bedrijf. Gebruikersaffiniteit is vereist voor beheerde apparaten die eigendom zijn van gebruikers en waarvoor de bedrijfsportal moet worden gebruikt voor services als het installeren van apps.
   - **Inschrijven zonder gebruikersaffiniteit**: het apparaat is niet gekoppeld aan een gebruiker. Gebruik deze relatie voor apparaten waarmee taken worden uitgevoerd zonder toegang tot lokale gebruikersgegevens. Apps waarvoor een gebruikersrelatie is vereist, zoals de bedrijfsportal-app die wordt gebruikt voor het installeren van LOB-apps, zullen niet werken. Vereist voor directe inschrijving.

6. Selecteer **Maken** om het profiel op te slaan.

## <a name="setup-assistant-enrollment"></a>Inschrijving met iOS-configuratieassistent

### <a name="add-apple-configurator-serial-numbers"></a>Apple Configurator-serienummers toevoegen

**Apple Configurator-serienummers toevoegen aan Intune**

1. Maak een lijst met twee kolommen met door komma's gescheiden waarden (.csv) zonder koptekst. Plaats het serienummers in de linkerkolom en de details in de rechterkolom. Een lijst kan momenteel maximaal 500 rijen bevatten. In een teksteditor ziet de .csv-lijst er ongeveer zo uit:

    F7TLWCLBX196, apparaatdetails</br>
    DLXQPCWVGHMJ,apparaatdetails

   [Lees hier meer informatie over het vinden van het serienummer van een iOS-apparaat](https://support.apple.com/HT204073).
2. Kies in Intune in Azure Portal achtereenvolgens**Apparaatinschrijving** en **Apple-inschrijving**.
3. Selecteer **Apple Configurator-apparaten** onder **Instellingen van de inschrijving met Apple Configurator beheren**.
4. Selecteer **Toevoegen**.
5. Selecteer een **inschrijvingsprofiel** om toe te passen op de serienummers die u importeert. Als u een bestand met nieuwe details importeert dat de bestaande details overschrijft, selecteert u **Details voor bestaande id's overschrijven**.
6. Ga naar het CSV-bestand met de serienummers en selecteer **Toevoegen**.

### <a name="reassign-a-profile-to-device-serial-numbers"></a>Opnieuw een profiel toewijzen aan apparaatserienummers

U wijst een inschrijvingsprofiel toe als u iOS-serienummers voor inschrijving met Apple Configurator importeert. Met Intune kunt u ook vanaf twee plaatsen in Azure Portal profielen toewijzen.
- **Apple Configurator-apparaten**
- **AC-profielen**

#### <a name="assign-from-apple-configurator-devices"></a>Toewijzen vanaf Apple Configurator-apparaten
1. Kies in Intune in Azure Portal achtereenvolgens**Apparaatinschrijving** en **Apple-inschrijving**.
3. Selecteer op de blade **Apple Configurator-apparaten** de seriële nummers waaraan u een profiel wilt toewijzen en selecteer vervolgens **Profiel toewijzen**.
4. Selecteer op de blade **Profiel toewijzen** het **nieuwe profiel** dat u wilt toewijzen en selecteer vervolgens **Toewijzen**.

#### <a name="assign-from-profiles"></a>Toewijzen vanaf profielen
1. Kies in Intune in Azure Portal achtereenvolgens**Apparaatinschrijving** en **Apple-inschrijving**.
2. Kies **AC-profielen** en selecteer vervolgens het profiel waaraan u serienummers wilt toewijzen.
3. Kies **Toegewezen apparaten** in de profielblade en kies vervolgens **Toewijzen**.
4. Filter op de serienummers die u aan het profiel wilt toewijzen, selecteer de apparaten en kies **Toewijzen**.

### <a name="export-the-profile"></a>Het profiel exporteren
Nadat u het profiel hebt gemaakt en de serienummers toegewezen, moet u het profiel vanuit Intune als een URL exporteren. Vervolgens importeert u het profiel in Apple Configurator op een Mac om het met apparaten te implementeren.

1. Kies in Intune in Azure Portal **Apparaatinschrijving** > Apple-inschrijving** > **AC-profielen**. Kies ten slotte het te exporteren profiel.
2. Selecteer **Profiel exporteren** op de blade voor het profiel.
3. Kopieer de profiel-URL. U kunt deze vervolgens later aan Apple Configurator toevoegen om het Intune-profiel te definiëren dat wordt gebruikt door iOS-apparaten.

  Vervolgens importeert u in de volgende procedure dit profiel in Apple Configurator om het Intune-profiel te definiëren dat door iOS-apparaten wordt gebruikt.

### <a name="enroll-devices-with-setup-assistant"></a>Apparaten inschrijven met Configuratieassistent

1.  Open **Apple Configurator2** op een Mac-computer. Kies in de menubalk **Apple Configurator 2** en vervolgens **Voorkeuren**.
  > [!WARNING]
  > Apparaten worden tijdens het inschrijvingsproces teruggezet naar de fabrieksinstellingen. U kunt het apparaat het beste opnieuw instellen en inschakelen. U moet het apparaat verbinden wanneer het scherm **Hallo** wordt weergegeven.

2. Selecteer in het deelvenster met **voorkeuren** **Servers** en kies het plusteken (+) om de wizard voor de MDM-server te starten. Kies **Volgende**.
3. Voer de **Hostnaam of URL** en de **inschrijvings-URL** in voor de MDM-server onder iOS-apparaten inschrijven via Configuratieassistent in Microsoft Intune. Voer voor de inschrijvings-URL de profiel-URL voor inschrijving in die u hebt geëxporteerd uit Intune. Kies **Volgende**.  

  De waarschuwing 'Server-URL is niet geverifieerd' kunt u zonder problemen negeren. Als u wilt doorgaan, kiest u **Volgende** totdat de wizard is voltooid.
4.  Verbind de mobiele iOS-apparaten met de Mac-computer met een USB-adapter.
5.  Kies **Voorbereiden**. Selecteer in het deelvenster **iOS-apparaat voorbereiden** de optie **Handmatig** en kies vervolgens **Volgende**.
6. Selecteer in het deelvenster **Registreren bij MDM-server** de naam van de server die u hebt gemaakt en kies vervolgens **Volgende**.
7. Selecteer in het deelvenster **Apparaten onder supervisie plaatsen** het toezichtsniveau en kies **Volgende**.
8. Kies de **organisatie** in het deelvenster **Een organisatie maken** of maak een nieuwe organisatie en kies vervolgens **Volgende**.
9. Kies in het deelvenster **iOS-configuratieassistent configureren** de stappen die de gebruiker te zien krijgt en kies vervolgens **Voorbereiden**. Voer een verificatie uit om de vertrouwensinstellingen bij te werken als dit wordt gevraagd.  
10. Zodra het iOS-apparaat klaar is met de voorbereidingen, kunt u de USB-kabel verwijderen.  

### <a name="distribute-devices"></a>Apparaten distribueren
De apparaten zijn nu gereed voor bedrijfsinschrijving. Schakel de apparaten uit en distribueer ze naar gebruikers. Wanneer gebruikers hun apparaten inschakelen, wordt Configuratieassistent gestart.

Nadat gebruikers hun apparaten hebben ontvangen, moeten ze Configuratieassistent voltooien. Op apparaten die zijn geconfigureerd met gebruikersaffiniteit kan de bedrijfsportal-app worden geïnstalleerd en uitgevoerd om apps te downloaden en apparaten te beheren.

## <a name="direct-enrollment"></a>Directe inschrijving
Wanneer u iOS-apparaten rechtstreeks inschrijft via Apple Configurator, kunt u een apparaat inschrijven zonder het serienummer van het apparaat in te voeren. U kunt ook het apparaat een naam geven voor identificatiedoeleinden voordat Intune de naam van het apparaat vastlegt tijdens de inschrijving. De bedrijfsportal-app wordt niet ondersteund voor rechtstreeks ingeschreven apparaten. De fabrieksinstellingen hoeven niet te worden teruggezet.

Apps waarvoor een gebruikersrelatie is vereist, zoals de bedrijfsportal-app die wordt gebruikt voor het installeren van LOB-apps, kunnen niet worden geïnstalleerd.

### <a name="export-the-profile-as-mobileconfig-to-ios-devices"></a>Het profiel als .mobileconfig exporteren naar iOS-apparaten
1. Meld u aan bij Azure Portal.
2. Kies **Meer services** > **Bewaking en beheer** > **Intune**.
3. Download het inschrijvingsprofiel op de blade **Profiel exporteren** naar [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) om dit direct als een beheerprofiel te pushen naar iOS-apparaten.
4. Bereid het apparaat met behulp van de volgende stappen voor met Apple Configurator.
  1. Open Apple Configurator 2.0 op een Mac-computer.
  2. Verbind het iOS-apparaat met de Mac-computer met behulp van een USB-kabel. Sluit Foto's, iTunes en andere apps die voor het apparaat worden geopend wanneer het apparaat wordt gedetecteerd.
  3. Kies in Apple Configurator het verbonden iOS-apparaat en kies vervolgens de knop **Toevoegen**. Opties die kunnen worden toegevoegd aan het apparaat, worden weergegeven in de vervolgkeuzelijst. Kies **Profielen**.
  4. Gebruik de bestandskiezer om het .mobileconfig-bestand te selecteren dat u uit Intune hebt geëxporteerd. Kies vervolgens **Toevoegen**. Het profiel wordt toegevoegd aan het apparaat. Als het apparaat niet onder supervisie is, vereist de installatie acceptatie op het apparaat.
5. Voer de volgende stappen uit om het profiel op het iOS-apparaat te installeren. Het apparaat moet de Configuratieassistent al hebben uitgevoerd en gereed zijn voor gebruik. Als inschrijving app-implementaties omvat, moet op het apparaat een Apple-id zijn ingesteld, omdat de app-implementaties vereisen dat u met een Apple-id bent aangemeld voor de App Store.
   1. Ontgrendel het iOS-apparaat.
   2. Kies in het dialoogvenster **Profiel installeren** voor **Beheerprofiel** de optie **Installeren**.
   3. Geef zo nodig een wachtwoordcode of Apple-id op.
   4. Accepteer de **Waarschuwing** en kies **Installeren**.
   5. Accepteer de **Externe waarschuwing** en kies **Vertrouwen**.
   6. Wanneer in het vak **Profiel geïnstalleerd** wordt bevestigd dat het profiel is geïnstalleerd, kiest u **Gereed**.

6. Open **Instellingen** op het iOS-apparaat en ga naar **Algemeen** > **Apparaatbeheer** > **Beheerprofiel**. Controleer of de profielinstallatie wordt weergegeven en controleer vervolgens de iOS-beleidsbeperkingen en geïnstalleerde apps. Het kan 10 minuten duren voordat beleidsbeperkingen en apps worden weergegeven op het apparaat.

7. Apparaten distribueren. Het iOS-apparaat is nu ingeschreven bij Intune en wordt beheerd.