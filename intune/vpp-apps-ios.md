---
title: Apps beheren die zijn gekocht via het iOS-volumeaankoopprogramma in Microsoft Intune
titlesuffix: ''
description: Meer informatie over hoe u apps kunt synchroniseren die u via het volumeaankoopprogramma in de iOS Store hebt gekocht, hoe u deze apps in Microsoft Intune kunt beheren en hoe u het gebruik ervan kunt bijhouden.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/14/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 51d45ce2-d81b-4584-8bc4-568c8c62653d
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: bd9915f3120e2fee2b487fbfff0d775a9d50ef8a
ms.sourcegitcommit: 21db583d6a9d3c15a8a8ee5579309dff1cfe1f8b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/16/2018
---
# <a name="how-to-manage-ios-apps-purchased-through-a-volume-purchase-program-with-microsoft-intune"></a>iOS-apps beheren die zijn aangeschaft via een volumeaankoopprogramma met Microsoft Intune


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

De iOS App Store biedt u de mogelijkheid meerdere licenties te kopen voor een app die u wilt uitvoeren binnen uw bedrijf. Door meerdere exemplaren aan te schaffen, kunt u apps in uw bedrijf efficiënt beheren.

Microsoft Intune kan u op de volgende manieren helpen bij het beheren van meerdere exemplaren van apps die u via dit programma hebt gekocht:

- Licentiegegevens rapporteren vanuit de App Store.
- Bijhouden hoeveel van de licenties u hebt gebruikt.
- Niet meer exemplaren van de app installeren dan waar u recht op hebt.

U kunt twee methoden gebruiken voor het toewijzen van apps die zijn gekocht via het volume-aankoopprogramma:

### <a name="device-licensing"></a>Apparaatlicenties

Wanneer u een app aan apparaten toewijst, wordt er één app-licentie gebruikt en deze blijft gekoppeld aan het apparaat waaraan u de licentie hebt toegewezen.

Wanneer u apps aan een apparaat toewijst die zijn gekocht via het volume-aankoopprogramma, hoeft de eindgebruiker van het apparaat geen Apple-id te verstrekken voor toegang tot de Store.

### <a name="user-licensing"></a>Gebruikerslicenties

Wanneer u een app aan gebruikers toewijst, wordt er één app-licentie gebruikt en gekoppeld aan de gebruiker. De app kan worden uitgevoerd op meerdere apparaten die eigendom zijn van de gebruiker (met een limiet die door Apple wordt bepaald).

Wanneer u een app aan gebruikers toewijst die is gekocht via het volume-aankoopprogramma, moet elke eindgebruiker een geldige en unieke Apple-id hebben voor toegang tot de App Store.

Verder kunt u met Intune boeken die u hebt gekocht via het volume-aankoopprogramma van Apple (VPP) synchroniseren, beheren en toewijzen. Zie [E-boeken in iOS beheren die u via een volume-aankoopprogramma hebt aangeschaft](vpp-ebooks-ios.md) voor meer informatie.

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Volume-purchased apps voor iOS-apparaten beheren

### <a name="supports-apple-volume-purchase-program-volume-purchased-apps-for-ios-devices"></a>Ondersteunt apps die zijn gekocht via het Apple Volume Purchase Program voor iOS-apparaten

U kunt meerdere licenties voor iOS-apps kopen via het [Apple-VPP voor bedrijven (Volume Purchase Program)](http://www.apple.com/business/vpp/) of het [Apple VPP voor onderwijs (Volume Purchase Program)](http://volume.itunes.apple.com/us/store). Hiervoor moet u een Apple VPP-account via de website van Apple instellen en het Apple VPP-token uploaden naar Intune.  U kunt uw gegevens over volume-aankopen vervolgens synchroniseren met Intune en het gebruik bijhouden van uw via het volume-aankoopprogramma gekochte apps.

### <a name="supports-business-to-business-volume-purchased-apps-for-ios-devices"></a>Ondersteunt apps die zijn gekocht via het business-to-business-volumeaankoopprogramma voor iOS-apparaten

Daarnaast kunnen externe ontwikkelaars privé apps distribueren naar geautoriseerde Volume Purchase Program for Business-leden die zijn opgegeven in iTunes Connect. Deze VPP for Business-leden kunnen zich aanmelden bij de Volume Purchase Program App Store en hun apps kopen. VPP for Business-apps die door de gebruiker zijn gekocht, worden gesynchroniseerd naar hun Intune-tenant.

## <a name="before-you-start"></a>Voordat u begint
Voordat u begint, moet u een VPP-token van Apple verkrijgen en dit uploaden naar uw Intune-account. Bovendien moet u op de hoogte zijn van het volgende:

* U kunt meerdere VPP-tokens koppelen aan uw Intune-account.
* Als u eerder een VPP-token hebt gebruikt voor een ander product, moet u een nieuw token voor gebruik met Intune genereren.
* Elke token is één jaar geldig.
* Standaard wordt Intune twee keer per dag gesynchroniseerd met de Apple VPP-service. U kunt op elk gewenst moment een handmatige synchronisatie starten.
* Voordat u begint met het gebruik van Apple VPP met Intune, verwijdert u eventuele bestaande VPP-gebruikersaccounts die zijn gemaakt met andere MDM-leveranciers (Mobile Device Management). Uit veiligheidsoverwegingen worden deze gebruikersaccounts niet met Intune gesynchroniseerd. Er worden alleen gegevens uit de Apple VPP-service gesynchroniseerd die zijn gemaakt met Intune.
* Intune ondersteunt het toevoegen van maximaal 256 VPP-tokens.
* Met het DEP-programma (Device Enrollment Profile) van Apple wordt de MDM-registratie (Mobile Device Management) geautomatiseerd. Met DEP kunt u bedrijfsapparaten op afstand configureren. U kunt zich registreren voor het DEP-programma met hetzelfde programma-agentaccount dat u hebt gebruikt voor VPP van Apple. De Apple Deployment Programs-id is uniek voor programma's die worden vermeld op de website [Apple Deployment Programs](https://deploy.apple.com) en kan niet worden gebruikt voor het aanmelden bij Apple-services, zoals de iTunes Store.
* Wanneer u VPP-apps met behulp van het gebruikerslicentiemodel toewijst aan gebruikers of apparaten (met gebruikersaffiniteit), moet elke Intune-gebruiker zijn gekoppeld aan een unieke Apple ID of een e-mailadres wanneer ze de voorwaarden en bepalingen van Apple op hun apparaat accepteren. Als u een apparaat instelt voor een nieuwe Intune-gebruiker, configureert u dit met de unieke Apple-id of het e-mailadres van de desbetreffende gebruiker. De Apple-id of het e-mailadres en de Intune-gebruiker vormen een uniek paar dat kan worden gebruikt op maximaal vijf apparaten.
* Een VPP-token wordt alleen ondersteund voor gebruik met één Intune-account tegelijk. Gebruik hetzelfde VPP-token niet voor meerdere tenants van Intune.
* Wanneer u VPP-apps met behulp van het gebruikerslicentiemodel toewijst aan gebruikers of apparaten (met gebruikersaffiniteit), moet elke Intune-gebruiker zijn gekoppeld aan een unieke Apple ID of een e-mailadres wanneer ze de voorwaarden en bepalingen van Apple op hun apparaat accepteren.
Als u een apparaat gaat instellen voor een nieuwe Intune-gebruiker, moet u het apparaat configureren met de unieke Apple ID of het e-mailadres van die gebruiker. De Apple-id of het e-mailadres en de Intune-gebruiker vormen een uniek paar dat kan worden gebruikt op maximaal vijf apparaten.

>[!IMPORTANT]
>Nadat u het VPP-token hebt geïmporteerd in Intune, kunt u hetzelfde token niet in een andere oplossing voor apparaatbeheer importeren. Dit kan leiden tot verlies van licentietoewijzngen en gebruikersrecords.

## <a name="to-get-and-upload-an-apple-vpp-token"></a>Een Apple VPP-token verkrijgen en uploaden

1. Meld u aan bij de [Azure-portal](https://portal.azure.com).
2. Kies **Alle services** > **Intune**. Intune bevindt zich in de sectie **Controle en beheer**.
1.  Kies in het deelvenster **Intune** de optie **Mobiele apps** > **iOS VPP-tokens** onder **Installatie**.
2.  Selecteer **Maken** in het deelvenster met de lijst VPP-tokens.
4. Geef in het deelvenster **VPP-token maken** de volgende gegevens op:
    - **VPP-tokenbestand**: meld u aan voor het VPP-programma voor bedrijven of voor het VPP-programma voor onderwijs als u dit nog niet hebt gedaan. Nadat u bent aangemeld, downloadt u het Apple VPP-token voor uw account en selecteert u dit hier.
    - **Apple ID**: voer de Apple ID in van het account dat aan het VPP is gekoppeld.
    - **Land/regio**: selecteer VPP-store voor uw land.  Intune synchroniseert VPP-apps voor alle landinstellingen uit de opgegeven store uit het land waar de VPP geldt.
        > [!WARNING]  
        > Als u het land wijzigt, worden de metagegevens en store-URL van de apps bijgewerkt bij de volgende synchronisatie met de Apple-service voor de apps die met deze token zijn gemaakt. De app wordt niet bijgewerkt als deze niet bestaat in de store van het nieuwe land.

    - **Type VPP-account**: u hebt de keuze uit **Bedrijven** of **Onderwijs**.
    - **Automatische updates voor apps**: kies **Aan** of **Uit** om automatische updates in of uit te schakelen. Wanneer deze optie is ingeschakeld, worden alle apps die zijn aangeschaft voor het opgegeven token, bijgewerkt via de Intune-service wanneer het apparaat wordt ingecheckt.
Updates voor de VPP-app worden gedetecteerd in de App Store en automatisch doorgestuurd naar het apparaat wanneer dit wordt ingecheckt.
4. Selecteer **Maken** wanneer u klaar bent.

Het token wordt weergegeven in het deelvenster met de lijst met tokens.

U kunt de gegevens waarover Apple beschikt, op elk gewenst moment synchroniseren met Intune door **Nu synchroniseren** te kiezen.

## <a name="to-assign-a-volume-purchased-app"></a>Een app toewijzen die is gekocht via het volume-aankoopprogramma

1.  Kies in het deelvenster **Intune** de optie **Mobiele apps** > **Apps** onder **Beheren**.
2.  Kies in het deelvenster met de lijst met apps de app die u wilt toewijzen en kies **Toewijzingen**.
3.  Kies in het deelvenster ***App-naam*** - **Toewijzingen** de optie **Groep toevoegen** en kies in het deelvenster **Groep toevoegen** een **Toewijzingstype**. Kies ook de Azure AD-gebruikers- of apparaatgroepen waaraan u de app wilt toewijzen.
5.  Voor elke groep die u hebt geselecteerd, kiest u de volgende instellingen:
    - **Type**: kies of de app **Beschikbaar** is (eindgebruikers kunnen de app installeren vanaf de bedrijfsportal) of **Vereist** (de app wordt automatisch geïnstalleerd).
    - **Licentietype**: kies uit **Gebruikerslicenties** of **Apparaatlicenties**.
6.  Als u klaar bent, kiest u **Opslaan**.


>[!NOTE]
>Er wordt een lijst met apps weergegeven die zijn gekoppeld aan een token. Als u een app hebt die aan meerdere VPP-tokens is gekoppeld, wordt dezelfde app meerdere keren weergegeven; eenmaal voor elk token.

## <a name="end-user-prompts-for-vpp"></a>Eindgebruikerprompts voor VPP

De eindgebruiker wordt in een aantal scenario’s gevraagd om de VPP-app te installeren. De volgende tabel beschrijft elke voorwaarde:

| # | Scenario                                | Uitnodigen voor Apple VPP-programma                              | Vraag om app-installatie | Vraag om Apple ID |
|---|--------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------------------|
| 1 | BYOD - gebruiker met licentie                             | J                                                                                               | J                                           | J                                 |
| 2 | Corp - gebruiker met licentie (apparaat niet onder supervisie)     | J                                                                                               | J                                           | J                                 |
| 3 | Corp - gebruiker met licentie (apparaat onder supervisie)         | J                                                                                               | N                                           | J                                 |
| 4 | BYOD – apparaat met licentie                           | N                                                                                               | J                                           | N                                 |
| 5 | CORP - apparaat met licentie (apparaat niet onder supervisie)                           | N                                                                                               | J                                           | N                                 |
| 6 | CORP - apparaat met licentie (apparaat onder supervisie)                           | N                                                                                               | N                                           | N                                 |
| 7 | Kioskmodus (apparaat onder supervisie) - apparaat met licentie | N                                                                                               | N                                           | N                                 |
| 8 | Kioskmodus (apparaat niet onder supervisie) - apparaat met licentie   | --- | ---                                          | ---                                |

> [!Note]  
> Het is niet aan te raden om VPP-apps toe te wijzen aan apparaten in de kioskmodus met de VPP-gebruikerslicenties.

## <a name="revoking-app-licenses-and-deleting-tokens"></a>App-licenties intrekken en tokens verwijderen 

<!-- 820863 -->  
Voor een bepaald apparaat met een of meer iOS-apps uit het volume-aankoopprogramma (VPP) kunt u de gekoppelde op een apparaat gebaseerde app-licenties voor het apparaat intrekken. Als u een app-licentie intrekt, wordt de desbetreffende VPP-app niet van het apparaat verwijderd. Als u een VPP-app wilt verwijderen en een licentie wilt vrijmaken, moet u het toewijzingstype van de VPP-app instellen op **Verwijderen**. Als u een app verwijdert die was toegewezen aan een gebruiker, maakt Intune de gebruiker of apparaatlicentie vrij en wordt de app van het apparaat verwijderd.

>[!NOTE]
>Intune haalt alle licenties op voor iOS VPP-apps die door gebruikers zijn gelicentieerd wanneer een medewerker niet langer bij een bedrijf werkt en geen lid meer is van de AAD-groepen.

<!-- 820879 -->  
U kunt tokens van het iOS-volume-aanschafprogramma (VPP) verwijderen via de console. Dit kan nodig zijn als er dubbele exemplaren van een VPP-token zijn. Als u een token verwijdert, worden ook alle eraan gekoppelde apps en toewijzingen verwijderd. Als u een token verwijdert, worden de app-licenties echter niet ingetrokken en worden er geen apps verwijderd. 

>[!NOTE]
>Intune kan geen applicenties intrekken nadat een token is verwijderd. 

<!-- 820870 -->  
Als u de licenties van alle VPP-apps van een bepaald VPP-token wilt intrekken, moet u eerst alle app-licenties intrekken die aan het token zijn gekoppeld. Daarna verwijdert u het token.

## <a name="further-information"></a>Meer informatie

Wanneer een gebruiker met een in aanmerking komend apparaat voor de eerste keer probeert een VPP-app op een apparaat te installeren, wordt de gebruiker gevraagd om deel te nemen aan het volume-aankoopprogramma van Apple. Deelname aan het programma moet plaatsvinden voordat de installatie van de app wordt uitgevoerd. De uitnodiging om deel te nemen aan het Apple Volume Purchase Program vereist dat de gebruiker de iTunes-app op het iOS-apparaat kan gebruiken. Als u een beleid hebt ingesteld om de iTunes Store-app uit te schakelen, werkt de gebruikerslicentie niet voor VPP-apps. U kunt dit probleem oplossen door het beleid te verwijderen, zodat de iTunes-app is toegestaan, of door een licentie te verlenen op basis van het apparaat.

## <a name="next-steps"></a>Volgende stappen

Zie [How to monitor apps](apps-monitor.md) (Apps controleren) voor meer informatie over het controleren van app-toewijzingen.
