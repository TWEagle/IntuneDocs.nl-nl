---
title: iOS-apps inpakken met de App Wrapping Tool | Microsoft Intune
description: Gebruik de informatie in dit onderwerp om meer te leren over het inpakken van uw iOS-apps zonder de code van de app zelf te wijzigen. Bereid de apps voor, zodat u de Mobile App Management-beleidsregels kunt toepassen.
keywords: 
author: karthikaraman
ms.author: karaman
manager: angrobe
ms.date: 09/19/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 99ab0369-5115-4dc8-83ea-db7239b0de97
ms.reviewer: oldang
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c67a5042fd177a4c5bd897092e84281db0977f5e
ms.openlocfilehash: 2c187b61b8fe25b2870d0cbc62f8352494583fc2


---

# iOS-apps voorbereiden voor Mobile Application Management met de Intune App Wrapping Tool
Wijzig met de **Microsoft Intune App Wrapping Tool voor iOS** de werking van interne iOS-apps, door functies van de app te beperken zonder dat u de code van de app zelf wijzigt.

Het hulpprogramma is een Mac OS-opdrachtregelprogramma waarmee een 'wrapper' (soort schil) rond een app wordt gemaakt. Wanneer een app is verwerkt, kunt u de app-functionaliteit wijzigen met [Mobile Application Management-beleid](configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console.md) dat u configureert.

Zie [Microsoft Intune App Wrapping Tool voor iOS](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios) als u het hulpprogramma wilt downloaden.



## Stap 1. Voldoen aan de vereisten voor het gebruik van de App Wrapping Tool
Lees [dit blogbericht](http://social.technet.microsoft.com/wiki/contents/articles/34339.skype-for-business-online-enable-your-tenant-for-modern-authentication.aspx) voor meer informatie over vereisten en het instellen daarvan.

|Vereiste|Meer informatie|
|---------------|--------------------------------|
|Ondersteunde hulpmiddelenset en besturingssysteem|U moet de App Wrapping Tool uitvoeren op een Mac met OS X 10.8.5 of hoger, waarop de XCode-hulpmiddelenset versie 5 of hoger is geïnstalleerd.|
|Handtekeningcertificaat en inrichtingsprofiel|U moet over een Apple-handtekeningcertificaat en -inrichtingsprofiel beschikken. Zie de [Apple-documentatie voor ontwikkelaars](https://developer.apple.com/) voor meer informatie.|
|Een app verwerken met de App Wrapping Tool|Apps moeten zijn ontwikkeld en ondertekend door uw bedrijf of een onafhankelijke softwareleverancier (ISV). U kunt dit hulpprogramma niet gebruiken om apps uit de Apple Store te verwerken. Apps moeten zijn geschreven voor iOS 8.0 of hoger. Apps moeten ook de Position Independent Executable-indeling (PIE) hebben. Zie de Apple-documentatie voor ontwikkelaars voor meer informatie over de PIE-indeling. Tot slot moet de app de extensie **.app** of **.ipa** hebben.|
|Apps die de Wrapping Tool niet kan verwerken|Versleutelde apps, niet-ondertekende apps en apps met uitgebreide bestandskenmerken.|
|Rechten instellen voor uw app|Voordat u de app verpakt, moet u rechten instellen zodat de app naast de standaardmachtigingen en -mogelijkheden ook over andere machtigingen en -mogelijkheden beschikt. Zie [App-rechten instellen](#setting-app-entitlements) voor instructies.|

## Stap 2. De App Wrapping Tool installeren

1.  Download de bestanden voor de App Wrapping Tool vanuit de opslagplaats van **Microsoft Intune App Wrapping Tool for iOS** [die op GitHub wordt gehost](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios), naar een lokale map op een Mac OS-computer.

2.  Dubbelklik op het installatiebestand **Microsoft Intune App Wrapping Tool for iOS.dmg**. Er wordt een venster met de gebruiksrechtovereenkomst weergegeven. Lees het document zorgvuldig door.

3. Kies **Akkoord** om de gebruiksrechtovereenkomst te accepteren. Hiermee wordt het pakket aan uw computer gekoppeld.

4.  Open het **IntuneMAMPackager**-pakket en sla de bestanden op in een lokale map op uw Mac OS-computer. U bent gereed om de App Wrapping Tool uit te voeren.

## Stap 3. De App Wrapping Tool uitvoeren
* Open op de Mac OS-computer een Terminal-venster en navigeer naar de map waarin u de bestanden van de App Wrapping Tool hebt opgeslagen. Het uitvoerbare programma heet **IntuneMAMPackager** en bevindt zich in **IntuneMAMPackager/Contents/MacOS**. U moet de opdracht als volgt uitvoeren:

    ```
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i /<path of input app>/<app filename> -o /<path to output folder>/<app filename> -p /<path to provisioning profile> -c <SHA1 hash of the certificate> [-b [<output app build string>]] [-v] [-e] [-x /<array of extension provisioning profile paths>]

    ```

    > [!NOTE]
    > Sommige parameters zijn optioneel, zoals wordt weergegeven in de onderstaande tabel.

    **Voorbeeld:** met de volgende voorbeeldopdracht voert u de App Wrapping Tool uit voor een app met de naam **MyApp.ipa**. Er zijn een inrichtingsprofiel en SHA-1-hash opgegeven. De verwerkte app wordt gemaakt, krijgt de naam **MyApp_Wrapped.ipa** en wordt opgeslagen in de map Bureaublad van de gebruiker.

    ```
    ./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i ~/Desktop/MyApp.ipa -o ~/Desktop/MyApp_Wrapped.ipa -p ~/Desktop/My_Provisioning_Profile_.mobileprovision -c 12A3BC45D67EF8901A2B3CDEF4ABC5D6E7890FAB  -v true
    ```
    U kunt de volgende opdrachtregeleigenschappen gebruiken met de App Wrapping Tool:

    |Eigenschap|Gebruik|
  |------------|--------------------|
  |**-i**|`<Path of the input native iOS application file>`. De bestandsnaam moet eindigen op .app of .ipa. |
  |**-o**|`<Path of the wrapped output application>` |
  |**-p**|`<Path of your provisioning profile for iOS apps>`|
  |**-c**|`<SHA1 hash of the signing certificate>`|
    |-h|Hiermee wordt gedetailleerde informatie weergegeven over het gebruik van de beschikbare opdrachtregeleigenschappen voor de App Wrapping Tool.|
  |-v|(Optioneel, maar handig) Hiermee worden uitgebreide berichten naar de console uitgevoerd.|
  |-e | (Optioneel) Gebruik deze eigenschap om ervoor te zorgen dat ontbrekende rechten worden verwijderd wanneer de app door de App Wrapping Tool wordt verwerkt. Zie de sectie App-rechten instellen voor meer informatie.|
  |-xe| (Optioneel) Hiermee wordt informatie afgedrukt over de IOS-extensies in de app en de rechten die nodig zijn voor het gebruik ervan. Zie de sectie App-rechten instellen voor meer informatie. |
  |-x| (Optioneel) `<An array of paths to extension provisioning profiles>`. Gebruik deze eigenschap als uw app extensie-inrichtingsprofielen nodig heeft.|
  |-f |(Optioneel) `<Path to a plist file specifying arguments.>` Gebruik deze eigenschap vóór het [PLIST](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/PropertyLists/Introduction/Introduction.html)-bestand als u ervoor kiest om de PLIST-sjabloon te gebruiken om de rest van de IntuneMAMPackager-eigenschappen op te geven: -i, -o, -p enzovoort. Zie de sectie Een PLIST-bestand gebruiken voor het invoeren van argumenten voor meer informatie. |
  |-b|(Optioneel) Gebruik -b zonder argument als u wilt dat de verpakte uitvoerapp dezelfde bundelversie krijgt als de invoerapp (niet aanbevolen). <br/><br/> Gebruik `-b <custom bundle version>` als u wilt dat de verpakte app een aangepaste CFBundleVersion krijgt. Als u ervoor kiest om een aangepaste CFBundleVersion op te geven, raden we u aan om de CFBundleVersion van de oorspronkelijke app te verhogen door de minst significante component te verhogen, bijvoorbeeld 1.0.0 -> 1.0.1. |


###Een PLIST-bestand gebruiken voor het invoeren van argumenten
U kunt de App Wrapping Tool op een eenvoudige manier uitvoeren door de opdrachtargumenten in een [PLIST](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/PropertyLists/Introduction/Introduction.html)-bestand op te nemen. Een PLIST-bestand heeft een indeling die vergelijkbaar is met die van een XML-bestand en kan worden gebruikt om opdrachtregelargumenten in te voeren in een formulierinterface.

Open in de map **IntuneMAMPackager/Contents/MacOS** `Parameters.plist`een lege PLIST-sjabloon met een teksteditor of Xcode. Voer uw argumenten in voor de volgende sleutels:

| PLIST-sleutel |  Standaardwaarde| Opmerkingen |
|------------------|--------------|-----|
| Pad van invoerapp-pakket  |leeg| Gelijk aan -i. |
| Pad van uitvoerapp-pakket |leeg| Gelijk aan -o.|
| Pad van inrichtingsprofiel |leeg| Gelijk aan -p. |
| SHA-1-certificaat-hash |leeg| Gelijk aan -c. |
| Uitgebreid ingeschakeld |onjuist| Gelijk aan -v. |
| Ontbrekende rechten verwijderen | onjuist| Gelijk aan -c.|
| Standaardbuild voorkomen |onjuist | Komt overeen met het gebruik van -b zonder argumenten. |
|Tekenreeks voor build overschrijven | leeg| De aangepaste CFBundleVersion van de verpakte uitvoerapp |
|Paden van extensie-inrichtingsprofielen | leeg| Een matrix van extensie-inrichtingsprofielen voor de app.
  

Voer tot slot de IntuneMAMPackager uit met het PLIST-bestand als het enige argument:

```
./IntuneMAMPackager –f Parameters.plist
```

* Nadat de verwerking is voltooid, wordt het bericht **De toepassing is verpakt** weergegeven.

    Zie [Foutberichten](prepare-ios-apps-for-mobile-application-management-with-the-microsoft-intune-app-wrapping-tool.md#error-messages) voor hulp als er een fout optreedt.

*   De ingepakte app wordt opgeslagen in de uitvoermap die u eerder hebt opgegeven. U kunt de app nu uploaden naar [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] en deze koppelen aan een beheerbeleid voor mobiele apps.

    > [!IMPORTANT]
    > Wanneer u een verpakte app uploadt, kunt u proberen een oudere versie van de app bij te werken als er al een oudere (ingepakte of oorspronkelijke) versie was geïmplementeerd in Intune. Als er een fout optreedt, uploadt u de app als een nieuwe app en verwijdert u de oudere versie.

    U kunt de app nu voor de [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)]-groepen implementeren en de app wordt op het apparaat uitgevoerd met de app-beperkingen die u opgeeft.

## Foutberichten en logboekbestanden
Gebruik de volgende informatie voor het oplossen van problemen die zich voordoen met de App Wrapping Tool.

### Foutberichten
Als de App Wrapping Tool niet kan worden voltooid, wordt mogelijk een van de volgende foutberichten weergegeven in de console:

|Foutbericht|Meer informatie|
|-----------------|--------------------|
|U moet een geldig iOS-inrichtingsprofiel opgeven.|Uw inrichtingsprofiel is mogelijk niet geldig. Controleer of u de juiste machtigingen hebt voor apparaten en of uw profiel correct is gemaakt voor ontwikkeling of distributie. Uw inrichtingsprofiel kan ook zijn verlopen.|
|Geef een geldige naam op voor een invoerapp.|Zorg dat u de juiste naam opgeeft voor de invoerapp.|
|Geef een geldig pad naar de uitvoerapp op.|Zorg dat het pad naar de uitvoerapp dat u hebt opgegeven bestaat en correct is.|
|Geef een geldig inrichtingsprofiel voor invoer op.|Zorg dat u een geldige naam en extensie voor het inrichtingsprofiel hebt opgegeven. Er ontbreken mogelijk rechten in uw inrichtingsprofiel of mogelijk hebt u de opdrachtregeloptie **–p** niet toegevoegd.|
|De invoerapp die u hebt opgegeven, is niet gevonden. Geef een geldige naam en een geldig pad op voor de invoerapp.|Zorg dat het pad naar uw invoerapp geldig is en bestaat. Zorg dat de invoerapp op die locatie bestaat.|
|Het inrichtingsprofielbestand voor invoer dat u hebt opgegeven, is niet gevonden. Geef een geldige inrichtingsprofielbestand voor invoer op.|Zorg dat het pad naar het inrichtingsbestand voor invoer geldig is en dat het opgegeven bestand bestaat.|
|De appmap voor uitvoer die u hebt opgegeven, is niet gevonden. Geef een geldig pad naar de uitvoerapp op.|Zorg dat het opgegeven uitvoerpad geldig is en bestaat.|
|App voor uitvoer heeft geen IPA-extensie.|Alleen apps met de extensies **.app** en **.ipa** worden geaccepteerd door de App Wrapping Tool. Zorg dat uw bestand voor uitvoer een geldige extensie heeft.|
|Er is een ongeldig handtekeningcertificaat opgegeven. Geef een geldig handtekeningcertificaat van Apple op.|Zorg dat u het juiste handtekeningcertificaat hebt gedownload vanuit de Apple-portal voor ontwikkelaars. Uw certificaat is mogelijk verlopen of misschien ontbreekt er een openbare of persoonlijke sleutel. Als uw Apple-certificaat en inrichtingsprofiel kunnen worden gebruikt om een app correct te ondertekenen in Xcode, zijn deze ook geldig voor de App Wrapping Tool.|
|De opgegeven app voor invoer is ongeldig. Geef een geldige app op.|Zorg dat u een geldige iOS-app hebt die is gecompileerd als APP of IPA-bestand.|
|De opgegeven app voor invoer is versleuteld. Geef een geldige niet-versleutelde app op.|De App Wrapping Tool ondersteunt geen versleutelde apps. Geef een niet-versleutelde app op.|
|De opgegeven app voor invoer die u hebt opgegeven, heeft geen Position Independent Executable-indeling (PIE). Geef een geldige app in de PIE-indeling op.|Position Independent Executable-apps (PIE) kunnen worden geladen op een willekeurig geheugenadres wanneer ze worden uitgevoerd. Dit kan beveiligingsvoordelen hebben. Zie de Apple-documentatie voor ontwikkelaars voor meer informatie.|
|De opgegeven app voor invoer is al ingepakt. Geef een geldige niet-ingepakte app op.|U kunt een app die al is verwerkt door het hulpprogramma, niet opnieuw verwerken. Als u wilt een app opnieuw wilt verwerken, moet u het hulpprogramma uitvoeren met de oorspronkelijke versie van de app.|
|De app voor invoer die u hebt opgegeven, is niet ondertekend. Geef een geldige ondertekende app op.|De App Wrapping Tool vereist dat apps zijn ondertekend. Raadpleeg de documentatie voor ontwikkelaars voor meer informatie over hoe u een ingepakte app ondertekent.|
|De app voor invoer die u hebt opgegeven, moet de indeling .ipa of .app hebben.|Alleen de extensies .app en .ipa worden geaccepteerd door de App Wrapping Tool. Zorg dat uw invoerbestand een geldige extensie heeft en is gecompileerd als bestand met de extensie .app of .ipa.|
|De app voor die u hebt opgegeven, is al ingepakt en heeft de meest recente beleidssjabloonversie.|De App Wrapping Tool pakt een bestaande ingepakte app met de meest recente beleidssjabloonversie niet opnieuw in.|
|WAARSCHUWING: u hebt geen SHA1-certificaat-hash opgegeven. Zorg dat uw verpakte app is ondertekend voordat u deze implementeert.|Zorg dat u een geldige SHA1-hash opgeeft na de opdrachtregeleigenschap **–c**. |

### Logboekbestanden voor de App Wrapping Tool
Apps die zijn verpakt met de App Wrapping Tool genereren logboeken die worden geschreven naar de console van het iOS-clientapparaat. Deze informatie is nuttig voor situaties waarin u een probleem ondervindt met de app en wilt achterhalen of dit probleem te maken heeft met de App Wrapping Tool. Als u deze informatie wilt ophalen, gebruikt u de volgende stappen:

1.  Reproduceer het probleem door de app uit te voeren.

2.  Verzamel de uitvoer van de console door de instructies van Apple voor [foutopsporing in geïmplementeerde iOS-apps](https://developer.apple.com/library/ios/qa/qa1747/_index.html)te volgen.

3.  Filter de opgeslagen logboeken op beperkingen voor apps door het volgende script in te voeren in de console:

    ```
    grep “IntuneAppRestrictions” <text file containing console output> > <required filtered log file name>
    ```
    U kunt de gefilterde logboeken naar Microsoft verzenden.

    > [!NOTE]
    > In het logboekbestand komt het item 'build version' overeen met de buildversie van Xcode.

    Ingepakte apps bieden gebruikers ook de optie om logboeken rechtstreeks vanaf het apparaat te verzenden nadat de app is vastgelopen. Gebruikers kunnen u de logboeken toesturen, zodat u ze kunt onderzoeken en indien nodig kun doorsturen naar Microsoft.


### Certificaat-, inrichtingsprofiel- en verificatievereisten

De App Wrapping Tool kan alleen volledig functioneren als aan bepaalde vereisten wordt voldaan.

|Vereiste|Details|
|---------------|-----------|
|Inrichtingsprofiel|**Controleer of het inrichtingsprofiel geldig is voordat u het toevoegt**. De App Wrapping Tool controleert niet of het inrichtingsprofiel is verlopen bij het verwerken van een iOS-app. Als een verlopen inrichtingsprofiel is opgegeven, voegt de App Wrapping Tool het verlopen inrichtingsprofiel toe en weet u niet dat er een probleem is tot de installatie van de app op een iOS-apparaat mislukt.|
|Certificaat|**Controleer of het certificaat geldig is voordat u het opgeeft**. De App Wrapping Tool controleert niet of het certificaat is verlopen bij het verwerken van iOS-apps. Als de hash voor een verlopen certificaat is opgegeven, verwerkt en ondertekent het hulpprogramma de app, maar kan de app niet worden geïnstalleerd op apparaten.<br /><br />**Controleer of het certificaat dat is verstrekt voor het ondertekenen van de verpakte app, overeenkomt met het certificaat in het inrichtingsprofiel**. De App Wrapping Tool controleert niet of het certificaat in het inrichtingsprofiel overeenkomt met het certificaat dat is opgegeven voor het ondertekenen van de verpakte app.|
|Verificatie|Versleuteling werkt alleen als een apparaat een pincode heeft. Op apparaten waarop u een verpakte app hebt geïmplementeerd, wordt de gebruiker gevraagd om zich opnieuw te verifiëren bij [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] wanneer deze de statusbalk van het apparaat aanraakt. Het standaardbeleid in een verpakte toepassing is *verificatie bij opnieuw opstarten*. iOS verwerkt elke externe melding (zoals een telefoongesprek) door de app af te sluiten en deze vervolgens opnieuw op te starten.


## App-rechten instellen
Voordat u de app verpakt, kunt u **rechten** verlenen zodat de app over meer machtigingen en mogelijkheden beschikt dan standaard het geval is.  Voor de ondertekening van de programmacode wordt gebruikgemaakt van een **rechtenbestand** om speciale machtigingen in uw app (bijvoorbeeld de toegang tot een gedeelde sleutelketen) op te geven. Specifieke app-services, ook wel **mogelijkheden** genoemd, worden in Xcode ingeschakeld tijdens het ontwikkelen van de app. Wanneer de mogelijkheden eenmaal zijn ingeschakeld, worden deze weergegeven in uw rechtenbestand. Zie [Mogelijkheden toevoegen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) in de bibliotheek voor iOS-ontwikkelaars voor meer informatie over rechten en mogelijkheden. Zie [Ondersteunde mogelijkheden](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/SupportedCapabilities/SupportedCapabilities.html) voor een volledige lijst met ondersteunde mogelijkheden.

### Ondersteunde mogelijkheden voor de App Wrapping Tool voor iOS

|Mogelijkheid|Beschrijving|Aanbevolen richtlijnen|
|--------------|---------------|------------------------|
|App-groepen|Gebruik app-groepen zodat meerdere apps toegang kunnen krijgen tot gedeelde containers en sta aanvullende communicatie tussen processen van de verschillende apps toe.<br /><br />Als u app-groepen wilt inschakelen, opent u het deelvenster **Mogelijkheden** en klikt u op de schakelaar **AAN** in het gedeelte **App-groepen **. U kunt app-groepen toevoegen of bestaande app-groepen selecteren.|Pas omgekeerde DNS-notatie toe wanneer u app-groepen gebruikt:<br /><br />*group.com.companyName.AppGroup*|
|Achtergrondmodi|Wanneer u achtergrondmodi inschakelt, kan uw iOS-app op de achtergrond actief blijven.||
|Gegevensbescherming|Met de gegevensbescherming voegt u een beveiligingsniveau toe aan bestanden die op schijf zijn opgeslagen door de iOS-app. De gegevensbescherming maakt gebruik van de ingebouwde versleutelingshardware die aanwezig is op de specifieke apparaten en waarmee bestanden in een versleutelde indeling op de schijf worden opgeslagen. Uw app moet worden ingericht voor het gebruik van de gegevensbescherming.||
|Aankopen binnen apps|Bij aankopen binnen apps wordt een winkel rechtstreeks in uw app opgenomen en kunt u verbinding maken met de winkel en veilig betalingen van de gebruiker verwerken. U kunt aankopen binnen apps gebruiken voor het ontvangen van betalingen voor uitgebreide functionaliteit of voor aanvullende inhoud die kan worden gebruikt met uw app.||
|Het delen van sleutelketens|Wanneer u het delen van sleutelketens inschakelt, kan uw app wachtwoorden in de sleutelketen delen met andere apps die door uw team zijn ontwikkeld.|Pas omgekeerde DNS-notatie toe wanneer u gebruikmaakt van het delen van sleutelketens:<br /><br />*com.companyName.KeychainGroup*|
|Persoonlijke VPN|Sta een persoonlijk VPN toe zodat uw app een aangepaste systeemconfiguratie voor VPN kan maken en beheren met Network Extension Framework.||
|Pushmeldingen|Met de Apple Push Notification-service (APNs) kan de gebruiker via een app die actief is op de achtergrond worden geïnformeerd dat er een bericht is voor de gebruiker.|Voor pushmeldingen hebt u een app-specifiek inrichtingsprofiel nodig.<br /><br />Volg de stappen in de [Apple-documentatie voor ontwikkelaars](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).|
|Configuratie van draadloze accessoires|Wanneer u de configuratie van draadloze accessoires inschakelt, wordt External Accessory Framework aan uw project toegevoegd en kunt u met uw app MFi Wi-Fi-accessoires configureren.||

### De stappen voor het inschakelen van rechten

1.  U schakelt als volgt mogelijkheden in uw app in:

    1.  Navigeer in Xcode naar het doel van uw app en klik op het deelvenster **Mogelijkheden**

    2.  Schakel de gewenste mogelijkheden in. Zie [Mogelijkheden toevoegen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) in de bibliotheek voor iOS-ontwikkelaars voor gedetailleerde informatie over elke mogelijkheid en het bepalen van de juiste waarden.

    3.  Noteer de id's die u tijdens de procedure hebt gemaakt.

    4.  Bouw en onderteken uw app zodat deze kan worden verpakt.

2.  U schakelt als volgt rechten in uw inrichtingsprofiel in:

    1.  Meld u aan bij het Apple Developer Member Center.

    2.  Maak een inrichtingsprofiel voor uw app. Zie [De vereisten voor de Intune App Wrapping Tool voor iOS ophalen](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/) voor instructies.

    3.  Schakel in het inrichtingsprofiel dezelfde rechten in als in uw app. U moet dezelfde id's gebruiken die u bij het ontwikkelen van de app hebt opgegeven.

    4.  Voer de wizard voor inrichtingsprofielen uit en download het bestand.

3.  Zorg ervoor dat u aan alle vereisten hebt voldaan en verpak de app.

### Het oplossen van veelvoorkomende problemen met rechten
Als door de App Wrapping Tool voor iOS een fout met de rechten wordt weergegeven, voert u de volgende probleemoplossingsstappen uit.

|Probleem|Oorzaak|Oplossing|
|---------|---------|--------------|
|Het parseren van rechten die zijn gegenereerd uit de invoertoepassing is mislukt.|Het rechtenbestand dat is opgehaald uit de app kan niet door de App Wrapping Tool worden gelezen. Het rechtenbestand is mogelijk ongeldig.|Controleer het rechtenbestand voor uw app. Volg hiervoor de instructies die hieronder staan beschreven. Controleer bij de inspectie van het rechtenbestand op ongeldige syntaxis. Het bestand moet de XML-indeling hebben.|
|Er ontbreken rechten in het inrichtingsprofiel (de ontbrekende rechten worden weergegeven). Verpak de app opnieuw met een inrichtingsprofiel dat deze rechten bevat.|De rechten die zijn ingeschakeld in het inrichtingsprofiel en de mogelijkheden die zijn ingeschakeld in de app komen niet overeen. Dit verschil geldt ook voor de id's die zijn gekoppeld aan de specifieke mogelijkheden (app-groepen, toegang tot de sleutelketen, enzovoort).|Over het algemeen is het mogelijk om een nieuw inrichtingsprofiel te maken waarmee dezelfde mogelijkheden kunnen worden ingeschakeld als voor de app. Wanneer de id’s van het profiel en de app niet overeenkomen, worden deze, indien mogelijk, door de App Wrapping Tool vervangen. Als u nog steeds deze foutmelding krijgt nadat u een nieuw inrichtingsprofiel hebt gemaakt, kunt u de rechten van de app verwijderen met de parameter **–e** (zie het gedeelte De parameter–e gebruiken om rechten te verwijderen uit een app, hieronder).|

### De bestaande rechten van een ondertekende app zoeken
U kunt als volgt de bestaande rechten van een ondertekende app en inrichtingsprofiel bekijken:

1.  Ga naar het IPA-bestand en wijzig de extensie in .zip.

2.  Pak het ZIP-bestand uit. De map Payload met daarin uw app-bundel wordt weergegeven.

3.  Controleer als volgt de rechten voor de app-bundel met het hulpprogramma voor het ondertekenen van de programmacode:

    ```
    $ codesign -d --entitlements :- "Payload/YourApp.app"
    ```
    hierbij staat `YourApp.app` voor de werkelijke naam van uw .app-bundel.

4.  Controleer met het beveiligingsprogramma de rechten van het inrichtingsprofiel dat in de app is opgenomen:

    ```
    $ security -D -i "Payload/YourApp.app/embedded.mobileprovision"
    ```
    hierbij staat `YourApp.app` voor de werkelijke naam van uw .app-bundel.

### De parameter –e gebruiken om rechten te verwijderen uit een app
Met deze opdracht worden ingeschakelde mogelijkheden in de app verwijderd die niet worden vermeld in het rechtenbestand. Als u mogelijkheden verwijdert die worden gebruikt door de app, kan dit de app beschadigen. Een voorbeeld van waar u mogelijkheden met ontbrekende rechten kunt verwijderen, is als u een app van een leverancier hebt die standaard beschikt over alle mogelijkheden.

```
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager –i /<path of input app>/<app filename> -o /<path to output folder>/<app filename> –p /<path to provisioning profile> –c <SHA1 hash of the certificate> -e
```

## Beveiliging en privacy voor de App Wrapping Tool
Gebruik de volgende best practices voor beveiliging en privacy wanneer u de App Wrapping Tool gebruikt.

-   Het handtekeningcertificaat, het inrichtingsprofiel en de Line-of Business-app die u opgeeft, moeten zich op de Mac OS-computer bevinden waarop u ook de App Wrapping Tool uitvoert. Als de bestanden zich in een UNC-pad bevinden, moet u ervoor zorgen dat ze toegankelijk zijn vanaf de Mac OS-computer. Het pad moet worden beveiligd via IPSec- of SMB-ondertekening.

    De verpakte toepassing die in de [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)]-console is geïmporteerd, moet zich op dezelfde computer bevinden als waarop u het hulpprogramma uitvoert. Als het bestand zich op een UNC-pad bevindt, moet u zorgen dat het toegankelijk is op de computer waarop de [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)]-console wordt uitgevoerd. Het pad moet worden beveiligd via IPSec- of SMB-ondertekening.

-   De omgeving waarnaar de App Wrapping Tool wordt gedownload vanuit de GitHub-opslagplaats, moet zijn beveiligd via IPSec- of SMB-ondertekening.

-   De app die u verwerkt, moet afkomstig zijn van een betrouwbare bron zodat bescherming tegen aanvallen gewaarborgd is.

-   Zorg dat de map voor uitvoer die u in de App Wrapping Tool hebt opgegeven is beveiligd, in het bijzonder als het een externe map is.

-   iOS-apps die een dialoogvenster voor het uploaden van bestanden bevatten, kunnen gebruikers toestaan om beperkingen voor knippen, kopiëren en plakken die gelden voor de app, te omzeilen. Zo kan een gebruiker het dialoogvenster voor het uploaden van bestanden bijvoorbeeld gebruiken om een schermopname van de app-gegevens te uploaden.

-   Wanneer gebruikers de documentenmap op hun apparaat bewaken vanuit een verpakte app, zien ze mogelijk een map met de naam **.msftintuneapplauncher**. Als deze map wordt gewijzigd of verwijderd, kan dit van invloed zijn op de goede werking van beperkte apps.

### Zie tevens
- [Bepalen hoe u apps met Microsoft Intune voorbereidt op Mobile Application Management](decide-how-to-prepare-apps-for-mobile-application-management-with-microsoft-intune.md)</br>
- [Instellingen en functies op uw apparaten beheren met Microsoft Intune-beleid](manage-settings-and-features-on-your-devices-with-microsoft-intune-policies.md)</br>
- [De SDK gebruiken om apps geschikt te maken voor Mobile Application Management](use-the-sdk-to-enable-apps-for-mobile-application-management.md)



<!--HONumber=Oct16_HO2-->

