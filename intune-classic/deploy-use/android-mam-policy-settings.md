---
title: MAM-beleidsinstellingen voor Android
description: In dit onderwerp worden de beleidsinstellingen voor het beheren van mobiele apps voor Android-apparaten beschreven.
keywords: ''
author: mattbriggs
ms.author: mabrigg
manager: dougeby
ms.date: 04/18/2016
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5dbb702a-1df5-4637-95c9-77a5f0b1a0e3
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: andcerat
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: ca72391720023720cec43234d599e23888e1cc59
ms.sourcegitcommit: df60d03a0ed54964e91879f56c4ef0a7507c17d4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/22/2018
---
# <a name="android-app-protection-policy-settings-in-microsoft-intune"></a>Instellingen voor beveiligingsbeleid voor apps voor Android in Microsoft Intune

> [!IMPORTANT]
De inhoud op deze pagina is nu grotendeels verouderd, omdat het Intune-app-beveiligingsbeleid volledig naar Azure Portal is gemigreerd. Lees meer informatie over het [Intune-app-beveiligingsbeleid voor Android in Azure Portal](https://docs.microsoft.com/intune/app-protection-policy-settings-android).

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

De in dit onderwerp beschreven beleidsinstellingen voor apps kunnen worden [geconfigureerd](create-and-deploy-mobile-app-management-policies-with-microsoft-intune.md) op de blade **Instellingen** in Azure Portal.
Er zijn twee soorten beleidsinstellingen, namelijk instellingen voor herlocatie van gegevens en instellingen voor toegang. In dit onderwerp verwijst de term _**door beleid beheerde apps**_ naar apps die zijn geconfigureerd met een beveiligingsbeleid voor apps.

##  <a name="data-relocation-settings"></a>Instellingen voor herlocatie van gegevens

| Instelling | Gebruik | Standaardwaarde(n) |
|------|------|------|
| **Back-ups van Android voorkomen** | Kies **Ja** om te voorkomen dat deze app back-ups van werk- of schoolgegevens in de [Android-back-upservice](https://developer.android.com/google/backup/index.html) maakt. Kies **Nee** om toe te staan dat deze app een back-ups maakt van werk- of schoolgegevens.| Ja |
| **App mag gegevens overdragen naar ander apps** | Geef aan welke apps gegevens uit deze app kunnen ontvangen: <ul><li> **Door beleid beheerde apps**: overdracht alleen toestaan naar andere door beleid beheerde apps.</li> <li>**Alle apps**: overdracht naar alle apps toestaan. </li> <li>**Geen**: geen gegevensoverdracht naar apps toestaan, met inbegrip van andere door beleid beheerde apps.</li></ul> <p>Er zijn enkele uitzonderingsapps en -services waar Intune gegevens naar mag overbrengen. Zie [Uitzonderingen voor gegevensoverdracht](#Data-transfer-exemptions) voor een volledige lijst met apps en services.| Alle apps |
| **App mag gegevens ontvangen van andere apps** | Geef aan welke apps gegevens naar deze app kunnen overdragen: <ul><li>**Door beleid beheerde apps**: overdracht alleen toestaan vanuit andere door beleid beheerde apps.</li><li>**Alle apps**: gegevensoverdracht vanuit alle apps toestaan.</li><li>**Geen**: geen gegevensoverdracht vanuit apps toestaan, met inbegrip van andere door beleid beheerde apps. </li></ul> <p>Er zijn enkele uitzonderingsapps en -services van waaruit Intune gegevensoverdracht mag toestaan. Zie [Uitzonderingen voor gegevensoverdracht](#Data-transfer-exemptions) voor een volledige lijst met apps en services. | Alle apps |
| **'Opslaan als' voorkomen** | Kies **Ja** als u het gebruik van de optie Opslaan als wilt uitschakelen in deze app. Selecteer **Nee** als u het gebruik van de optie Opslaan als wilt toestaan. <p><br>**Selecteer naar welke opslagservices bedrijfsgegevens kunnen worden opgeslagen** <br>Gebruikers kunnen naar de geselecteerde services opslaan (OneDrive voor Bedrijven, SharePoint en lokale opslag). Alle andere services worden geblokkeerd.</p> | Nee <br><br> 0 geselecteerd |
| **Knippen, kopiëren en plakken met andere apps beperken** | Geef op wanneer knip-, kopieer- en plakbewerkingen voor deze app kunnen worden gebruikt. U kunt kiezen uit: <ul><li>**Geblokkeerd**: geen knip-, kopieer- en plakbewerkingen toestaan tussen deze app en andere apps.</li><li>**Door beleid beheerde apps**: alleen knip-, kopieer- en plakbewerkingen toestaan tussen deze app en andere door beleid beheerde apps.</li><li>**Door beleid beheerde apps met Plakken in**: knippen en kopiëren toestaan tussen deze app en andere door beleid beheerde apps. Gegevens uit alle apps mogen in deze app worden geplakt.</li><li>**Elke app**: geen beperkingen voor knip-, kopieer- en plakbewerkingen vanuit en naar deze app. | Elke app |
|**Weergave van webinhoud beperken tot beheerde browser** | Kies **Ja** om af te dwingen dat webkoppelingen in de app worden geopend in de Managed Browser-app. <br><br> Voor apparaten die niet zijn geregistreerd bij Intune, kunnen de webkoppelingen in door beleid beheerde apps alleen worden geopend in de Managed Browser-app. <br><br> Als u Intune gebruikt voor het beheer van uw apparaten, raadpleegt u [Internettoegang beheren met beheerde-browserbeleid met Microsoft Intune](manage-internet-access-using-managed-browser-policies.md). | Nee |
| **Appgegevens versleutelen** | Kies **Ja** om versleuteling van werk- of schoolgegevens in deze app in te schakelen. Intune gebruikt een 128-bit OpenSSL-AES-versleutelingsmethode samen met het Android Keystore-systeem om appgegevens veilig te versleutelen. Gegevens worden synchroon versleuteld tijdens I/O-taken voor bestanden. Inhoud van de apparaatopslag wordt altijd versleuteld. <br><br> De versleutelingsmethode is **niet** gecertificeerd volgens FIPS 140-2.  | Ja |
| **Synchroniseren van contactpersonen uitschakelen** | Kies **Ja** om te voorkomen dat de app gegevens opslaat in de systeemeigen Contactpersonen-app op het apparaat. Kies **Nee** om ervoor te zorgen dat de app gegevens kan opslaan in de systeemeigen Contactpersonen-app op het apparaat. <br><br>Als u selectief wilt wissen om werk- of schoolgegevens uit de app te verwijderen, worden contactpersonen verwijderd die rechtstreeks vanuit de app met de systeemeigen Contactpersonen-app worden gesynchroniseerd. Contactpersonen die vanuit het systeemeigen adresboek zijn gesynchroniseerd met een andere externe bron, kunnen niet worden gewist. Dit is momenteel alleen van toepassing op de Microsoft Outlook-app. | Nee |
| **Afdrukken uitschakelen** | Kies **Ja** om te voorkomen dat de app werk- of schoolgegevens afdrukt. | Nee |

  >[!NOTE]
  >De versleutelingsmethode voor de instelling **Appgegevens versleutelen** is **niet** gecertificeerd volgens FIPS 140-2.


  ## <a name="data-transfer-exemptions"></a>Uitzonderingen voor gegevensoverdracht

  Er zijn een aantal uitzonderingsapps en -platformservices waar het Intune beveiligingsbeleid voor apps gegevensoverdracht naar en van kan toestaan. Alle door Intune beheerde apps voor Android moeten bijvoorbeeld gegevens kunnen overdragen van en naar Google Text-to-Speech, zodat tekst op het scherm van uw mobiele apparaat hardop kan worden voorgelezen. Deze lijst kan worden gewijzigd en reflecteert de services en apps die als nuttig voor beveiligde productiviteit worden beschouwd.

  ### <a name="full-exemptions"></a>Volledige uitzonderingen

  Voor deze apps en services is gegevensoverdracht naar en van Intune-beheerde apps volledig toegestaan.

  |Naam van app/service | Beschrijving |
  | ------ | ---- |
  | com.android.phone | Systeemeigen phone-app
  | com.android.vending | Google Play Store |
  | com.android.documentsui | Android Documentkiezer|
  | com.google.android.webview | [WebView](https://developer.android.com/reference/android/webkit/WebView.html), dat nodig is voor veel apps, inclusief Outlook. |
  | com.android.webview |[WebView](https://developer.android.com/reference/android/webkit/WebView.html), dat nodig is voor veel apps, inclusief Outlook.|
  | com.google.android.tts | Google Tekst naar spraak |
  | com.android.providers.settings | Systeeminstellingen Android |
  | com.azure.authenticator | Azure Authenticator-app, die vereist is voor een geslaagde verificatie in veel scenario's. |
  | com.microsoft.windowsintune.companyportal | Intune Bedrijfsportal|

  ### <a name="conditional-exemptions"></a>Voorwaardelijke uitzonderingen
  Voor deze apps en services is gegevensoverdracht naar en van Intune-beheerde apps onder bepaalde voorwaarden toegestaan.

  |Naam van app/service | Beschrijving | Uitzonderingsvoorwaarde|
  | ------ | ---- | --- |
  | com.android.chrome | Google Chrome-browser | Chrome wordt gebruikt voor een aantal webweergaveonderdelen op Android 7.0+ en is nooit verborgen. Gegevensstroom naar en van de app is echter altijd beperkt.
  | com.skype.raider | Skype | Voor de Skype-app zijn alleen bepaalde acties die in een telefonische oproep resulteren toegestaan. |
  | com.android.providers.media | Android media-inhoudsprovider | Voor de media-inhoudsprovider is alleen de actie beltoonselectie toegestaan. |
  | com.google.android.gms; com.google.android.gsf | Google Play-Services-pakketten | Voor deze pakketten zijn Google Cloud Messaging-acties zoals pushmeldingen toegestaan. |



##  <a name="access-settings"></a>Toegangsinstellingen

| Instelling | Gebruik | Standaardwaarde(n) |
|------|------|------|
| **Pincode is vereist voor toegang** | Kies **Ja** om een pincode te vereisen voor gebruik van deze app. De eerste keer dat de gebruiker de app uitvoert in een aan werk of school gerelateerde context, wordt de gebruiker gevraagd deze pincode in te stellen. Standaardwaarde = **Ja**.<br><br> Configureer de volgende instellingen voor pincodesterkte: <ul><li>**Aantal pogingen voordat pincode opnieuw wordt ingesteld**: geef het aantal pogingen voor de gebruiker op om de pincode in te voeren voordat de gebruik deze opnieuw moet instellen. Standaardwaarde = **5**.</li><li> **Eenvoudige pincode toestaan:** kies **Ja** als gebruikers eenvoudige pincodes mogen gebruiken, zoals 1234 of 1111. Kies **Nee** als ze geen eenvoudige tekenreeksen mogen gebruiken. Standaardwaarde = **Ja**. </li><li> **Lengte van de pincode:** geef het minimale aantal cijfers op waaruit een pincode moet bestaan. Standaardwaarde = **4**. </li><li> **Vingerafdruk in plaats van pincode toestaan (Android 6.0+)**: selecteer **Ja** als de gebruiker in plaats van een pincode [vingerafdrukverificatie](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) mag gebruiken voor toegang tot apps. Standaardwaarde = **Ja**.</li></ul> Op Android-apparaten kunt u gebruikers hun identiteit laten aantonen met behulp van [Android-vingerafdrukverificatie](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) in plaats van een pincode. Wanneer gebruikers deze app proberen te gebruiken via hun werk- of schoolaccount, moeten ze hun vingerafdruk in plaats van een pincode gebruiken. </li></ul>| Pincode vereisen: Ja <br><br> Pogingen om pincode opnieuw in te stellen: 5 <br><br> Eenvoudige pincode toestaan: Ja <br><br> Lengte pincode: 4 <br><br> Vingerafdruk toestaan: Ja |
| **Bedrijfsreferenties vereisen voor toegang** | Kies **Ja** om te vereisen dat gebruikers zich aanmelden met hun werk- of schoolaccount in plaats van een pincode voor toegang tot apps. Als u deze waarde op **Ja** instelt, overschrijft dit de vereisten voor de pincode of Touch-ID.  | Nee |
| **Verhinderen dat beheerde apps op gekraakte of geroote apparaten worden uitgevoerd** |Kies **Ja** om te voorkomen dat deze app wordt uitgevoerd op jailbroken of geroote apparaten. De gebruiker kan deze app nog steeds gebruiken voor privétaken maar moet voor het openen van werk- of schoolgegevens in deze app een ander apparaat gebruiken. | Ja |
| **Toegangsvereisten opnieuw controleren na (minuten)** | Configureer de volgende instellingen: <ul><li>**Time-out**: dit is het aantal minuten waarna de (eerder in het beleid gedefinieerde) toegangsvereisten opnieuw worden gecontroleerd. Wanneer een beheerder bijvoorbeeld invoeren van een pincode inschakelt in het beleid, moet een gebruiker die een MAM-app opent een pincode invoeren. Wanneer u deze instelling gebruikt, hoeft de gebruiker nog **30 minuten** (standaardwaarde) geen pincode in te voeren voor een MAM-app.</li><li>**Offline respijtperiode**: het aantal minuten dat MAM-apps offline kunnen worden uitgevoerd. Geef de tijd (in minuten) op waarna de toegangsvereisten voor de app opnieuw worden gecontroleerd. Standaardwaarde = **720** minuten (12 uur). Nadat deze periode is verstreken, is gebruikersverificatie voor AAD vereist om de app te blijven uitvoeren.</li></ul>| Time-out: 30 <br><br> Offline: 720 |
| **Offline interval (in dagen) voordat app-gegevens worden gewist** | Na dit aantal dagen (gedefinieerd door de beheerder) van offline uitvoeren, wordt selectief wissen door de app zelf uitgevoerd. Dit is dezelfde wisbewerking die door de beheerder kan worden gestart in de werkstroom MAM wissen. <br><br> | 90 dagen |
| **Schermopname en Android Assistant blokkeren (Android 6.0+)** | Kies **Ja** om schermopnames en gebruik van de **Android Assistent**-functies van het apparaat te blokkeren bij gebruik van deze app. Als u **Ja** kiest, wordt ook de voorbeeldafbeelding van de app-schakelbaar vervaagd bij gebruik van deze app in combinatie met een werk- of schoolaccount. | Nee |
| **Pincode apparaat uitschakelen wanneer de pincode voor het apparaat wordt beheerd** | Kies **Ja** om de pincode voor het apparaat uit te schakelen wanneer een apparaatvergrendeling wordt gedetecteerd op een geregistreerd apparaat. | Nee |
