---
title: Opmerkingen bij de release van Microsoft Intune | Microsoft Intune
description: Opmerkingen bij de Intune-release
keywords: 
author: Staciebarker
ms.author: stabar
manager: angrobe
ms.date: 09/08/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: db9479b2-582d-4a1a-9fbc-fbfc6c680e6f
ms.reviewer: jeffgilb
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f1147e5fe766bc4642439c4ad23b2fdfbf74bb03
ms.openlocfilehash: da476088435d6ef8bd58ecad1b221254a30858cc


---

# Opmerkingen bij de release van Microsoft Intune
Microsoft Intune is een geïntegreerde cloudoplossing voor clientbeheer die voorziet in hulpprogramma's, rapporten en upgradelicenties voor de nieuwste versie van Windows. Dit helpt ook uw computers up-to-date en beveiligd te houden. Bovendien kunt u met Intune mobiele apparaten in het netwerk beheren via Exchange ActiveSync of rechtstreeks via Intune. In de volgende opmerkingen bij de release staat belangrijke informatie en worden bekende problemen in Microsoft Intune beschreven.


## Android-gebruikers kunnen geen e-mail verzenden wanneer voorwaardelijke toegang voor Exchange Online is geïmplementeerd

**Probleem**: gebruikers die op hun apparaten werken met Samsung Android 5.1.1 en hoger, kunnen geen e-mail verzenden wanneer voorwaardelijke toegang voor Exchange Online is ingesteld. Samsung bevestigt dat het probleem te maken heeft met de ingebouwde e-mailclient in Android 5.1.1 en hoger, en zoekt momenteel naar een oplossing.

**Tijdelijke oplossing 1:** adviseer gebruikers de Outlook-app voor Android te gebruiken.

**Tijdelijke oplossing 2:** u kunt ook deze stappen volgen zodat betrokken gebruikers e-mail kunnen verzenden:

1. Plaats elke betrokken gebruiker in een beveiligingsgroep in de sectie 'Uitgesloten groepen' van het beleid voor voorwaardelijke toegang voor Exchange Online.
2. Laat de gebruiker tijdelijk e-mail synchroniseren met de ingebouwde e-mailclient.
3. Verwijder de betrokken gebruiker uit de uitgesloten groep en controleer of de gebruiker nu e-mail kan verzenden.

Microsoft blijft nauw met Samsung samenwerken aan een oplossing of aanvullende tijdelijke oplossingen.



## Het wijzigen van brontoegangsprofielen tussen groepen voor iOS en Android kan mislukken
**Probleem:** wanneer u brontoegangsprofielen voor e-mail of het Simple Certificate Enrollment Protocol (SCEP) tussen groepen wijzigt, kan er een profielconflict optreden, waardoor het wijzigen mislukt. Stel, u hebt een bestaand e-mailprofiel dat verwijst naar een lokale Exchange-server, met als doel Groep A. Vervolgens maakt u een nieuw e-mailprofiel dat verwijst naar Exchange Online, met als doel Groep B. Wanneer u gebruikers van groep A naar groep B verplaatst, blijft het lokale Exchange-e-mailprofiel op de apparaten behouden en wordt geprobeerd het e-mailprofiel van Exchange Online te installeren dat groep B als doel heeft.

Op dat moment wordt een van de volgende scenario’s van kracht: 
* Als e-mailprofiel A en B identiek zijn, verwerpt het apparaat e-mailprofiel B omdat e-mailprofiel B al e-mailprofiel A bevat.
* Als e-mailprofiel A anders is dan e-mailprofiel B, zoals hier het geval is, heeft het apparaat twee e-mailprofielen.

> [!NOTE]
> De hostnaam en het kenmerk die voor de gebruikersnaam worden gebruikt, worden gecontroleerd om het ene e‑mailprofiel van het andere te onderscheiden.

In beide gevallen is het brontoegangsprofiel (e-mailprofiel) niet van het apparaat verwijderd om te voorkomen dat de toegang van een gebruiker tot e-mail of het SCEP-certificaat van een client wordt verwijderd.

**Tijdelijke oplossing:** geen.

## Wanneer u een Windows 8.1-apparaat registreert dat moet worden geverifieerd met een proxyserver, mislukt het inschrijvingsproces zonder zichtbare oorzaak
**Probleem:** wanneer u een Windows 8.1-apparaat inschrijft en het apparaat moet tijdens het inschrijvingsproces worden geverifieerd bij een proxyserver, mislukt de inschrijving als de referenties voor de proxyserver niet zijn opgeslagen in de cache van het apparaat. Wanneer de referenties voor de proxyserver niet in de cache van het apparaat zijn opgeslagen, wordt het inschrijvingsproces opgeschort totdat de gebruiker de referenties invoert. De vraag om de proxyserverreferenties op te geven wordt echter niet weergegeven tijdens het registratieproces. Hierdoor kan het registratieproces niet worden geverifieerd bij de proxyserver. Er wordt geen zichtbare indicatie van deze fout weergegeven voor de gebruiker.

**Tijdelijke oplossing:** voor Windows 8.1-apparaten die moeten worden geregistreerd in een netwerk waarvoor het gebruik van een geverifieerde proxyserver is vereist, moet u de referenties voor de proxyserver instellen en opslaan voordat het apparaat wordt geregistreerd. Ga als volgt te werk om de referenties in te stellen en op te slaan op een Windows 8.1-apparaat:

1.  Open Internet Explorer op het Windows 8.1-apparaat.
2.  Als u wordt gevraagd om de referenties voor de proxyserver, voert u de referenties in en kiest u vervolgens de optie **Mijn referenties onthouden**.
3.  Het apparaat inschrijven.

## Inschrijving van Windows Phone 8.1-apparaten bij Microsoft Intune mislukt wanneer apparaatverificatie is ingeschakeld in AD FS
**Probleem:** wanneer u een Windows Phone 8.1-apparaat registreert, mislukt de registratie als de optionele instelling voor apparaatverificatie is ingeschakeld als onderdeel van het algemene verificatiebeleid in Active Directory Federation Services (AD FS).

**Tijdelijke oplossing:** schakel de apparaatverificatie uit op de AD FS-server door de optie **Apparaatverificatie inschakelen** uit te schakelen in **Algemeen verificatiebeleid bewerken**. Zie [Verificatiebeleid configureren](http://technet.microsoft.com/library/dn486781.aspx) voor meer informatie.


## De Microsoft Intune App Wrapping Tool voor Android bevat geen ingebouwde mogelijkheid om het programma te verwijderen
**Probleem:** de **Microsoft App Wrapping Tool voor Android** heeft geen ingebouwde functionaliteit voor het verwijderen van het hulpprogramma.

**Tijdelijke oplossing:** blader naar de locatie waar u het hulpprogramma hebt geïnstalleerd en verwijder de map. De standaardlocatie voor de installatie is: **C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool**. Zie [Android-apps voorbereiden voor beheer met de App Wrapping Tool](/intune/deploy-use/prepare-android-apps-for-mobile-application-management-with-the-microsoft-intune-app-wrapping-tool) voor meer informatie over de App Wrapping Tool.

## Hulp op afstand is niet beschikbaar op computers met Windows 8 of Windows 8.1
**Probleem:** in deze release is de functie Hulp op afstand niet beschikbaar op computers met Windows 8 of Windows 8.1.

**Tijdelijke oplossing:** geen.

## Waarschuwingsmeldingen voor geadresseerden die automatisch worden toegevoegd, werken niet
**Probleem:** als een geadresseerde automatisch aan een waarschuwingsmelding wordt toegevoegd, ontvangt deze de melding mogelijk niet altijd.

**Tijdelijke oplossing:** om ervoor te zorgen dat geadresseerden meldingen ontvangen, moet u geadresseerden handmatig toevoegen aan waarschuwingsmeldingen.

## Taalondersteuning in de Azure-portal
De Azure-portal biedt ondersteuning voor de volgende talen: Chinees (Vereenvoudigd), Chinees (Traditioneel), Duits, Engels, Frans, Hongaars, Italiaans, Japans, Koreaans, Nederlands, Pools, Portugees (Brazilië), Portugees (Portugal), Russisch, Spaans, Tsjechisch, Turks en Zweeds.

De Intune-beheerconsole en de interface voor mobiele gebruikers worden ondersteund in de talen Deens, Fins, Grieks, Noors en Roemeens, en in alle talen die worden ondersteund door de Azure-portal.



<!--HONumber=Oct16_HO2-->

