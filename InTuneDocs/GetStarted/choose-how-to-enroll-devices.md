---
title: Kiezen hoe u mobiele apparaten registreert |Microsoft Intune
description: Bepalen hoe u mobiele apparaten in Intune kunt registreren door enkele eenvoudige vragen te beantwoorden
keywords: 
author: NathBarn
manager: angrobe
ms.date: 07/25/2016
ms.topic: article
ms.prod: 
ms.service: 
ms.technology: 
ms.assetid: cac62b64-3f8b-47ae-aa66-970c7ba15466
ms.reviewer: dagerrit
translationtype: Human Translation
ms.sourcegitcommit: c671610b9c56d8b92d126d9902cce9c8c689ed63
ms.openlocfilehash: aac4eee56ec7326b2ce466d19b580aa5f1388aea


---

# Kiezen hoe u mobiele apparaten registreert

Aan de hand van uw antwoorden op de volgende vragen kan worden bepaald welke registratiemethode u het best kunt gebruiken voor de apparaten die u beheert.

## **Gebruiken werknemers hun eigen apparaten of worden de apparaten geleverd door uw organisatie?**

  - **Apparaten van gebruikers** -'Bring your own device' (BYOD) inschrijven
  - **Bedrijfsapparaten** - COD-inschrijving

> [!div class="button"]
[BYOD-inschrijving >](#what-byod-devices-can-your-users-enroll)   [COD-inschrijving >](#are-your-company-owned-devices-shared-or-do-they-have-dedicated-users)

## **Welke BYOD-apparaten kunnen uw gebruikers inschrijven?**

> [!div class="button"]
[Android](/intune/deploy-use/set-up-android-management-with-microsoft-intune) [iOS en Mac](/intune/deploy-use/set-up-ios-and-mac-management-with-microsoft-intune) [Windows 10 Mobile en Window Phone](/intune/deploy-use/set-up-windows-phone-management-with-microsoft-intune) [Windows-pc’s](/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune)

## **Worden de bedrijfseigen apparaten gedeeld of hebben deze apparaten toegewezen gebruikers?**

> [!div class="button"]
[Gedeeld >](#what-operating-system-are-your-shared-devices-running)   [Specifiek >](#how-will-you-manage-dedicated-ios-devices)


## **Welk besturingssysteem wordt uitgevoerd op uw gedeelde apparaten?**

  > [!div class="button"]
  [Windows >](/intune/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune) [Android >](/intune/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune) [iOS >](#how-will-you-manage-shared-ios-devices)

## **Hoe beheert u uw gedeelde iOS-apparaten?**

  > [!div class="button"]
  [iOS DEP-registratie >](/intune/deploy-use/ios-device-enrollment-program-in-microsoft-intune) [Directe iOS-registratie >](/intune/deploy-use/ios-direct-enrollment-in-microsoft-intune) [DEM-registratie >](/intune/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune)

  - **Het Device Enrollment Program (DEP) van Apple**: u kunt voor iOS-apparaten die zijn aangeschaft of worden beheerd met DEP een registratieprofiel gebruiken. Wanneer gebruikers hun apparaat voor het eerst inschakelen, downloadt het apparaat het DEP-profiel en wordt het apparaat geregistreerd bij de profiel-DEP.

  - **Apple Configurator op een Mac**: Apple Configurator is een Apple-toepassing die wordt uitgevoerd op een Mac-computer. U kunt uw iOS-apparaten met een USB-kabel aansluiten op de Mac om een registratieprofiel op het apparaat te installeren. Als u de fabrieksinstellingen van het apparaat kunt terugzetten om ze te registreren, gebruikt u Registratie van configuratieassistent. Als u de fabrieksinstellingen van het apparaat niet wilt terugzetten, gebruikt u Direct registratie.

  - **Beheerfunctie voor apparaatregistratie**: met de beheerfunctie voor apparaatregistratie (DEM) van Intune kan een manager of beheerder een groot aantal mobiele apparaten registreren met één gebruikersaccount. Deze apparaten kunnen geen gebruikersaffiniteit (ofwel toegewezen gebruikers) hebben, en kunnen alleen worden geregistreerd na installatie van en aanmelding bij de bedrijfsportal-app.

## **Hoe beheert u uw specifieke iOS-apparaten?**

  > [!div class="button"]
  [Label met IMEI >](/intune/deploy-use/specify-corporate-owned-devices-with-international-mobile-equipment-identity-imei-numbers) [iOS DEP](/intune/deploy-use/ios-device-enrollment-program-in-microsoft-intune) [iOS-Configuratieassistent](/intune/deploy-use/ios-setup-assistant-enrollment-in-microsoft-intune) [Code met IMEI](/intune/deploy-use/specify-corporate-owned-devices-with-international-mobile-equipment-identity-imei-numbers)

  U kunt apparaten in bedrijfseigendom met toegewezen gebruikers op de volgende manieren registreren:

  - **Het Device Enrollment Program (DEP) van Apple**: u kunt voor iOS-apparaten die zijn aangeschaft of worden beheerd met DEP een registratieprofiel gebruiken. Wanneer gebruikers hun apparaat voor het eerst inschakelen, downloadt het apparaat het DEP-profiel en wordt het apparaat geregistreerd bij Intune.

  - **Apple Configurator op een Mac**: Apple Configurator is een Apple-toepassing die wordt uitgevoerd op een Mac-computer. U kunt uw iOS-apparaten met een USB-kabel aansluiten op de Mac om een registratieprofiel op het apparaat te installeren. Als u de fabrieksinstellingen van het apparaat kunt terugzetten om ze te registreren, gebruikt u Registratie van configuratieassistent.

  - **Label met IMEI-nummer**: door de IMEI-nummers (International Mobile Equipment Identity) van bedrijfseigen apparaten te importeren, kunt u ze in Intune labelen als apparaten die eigendom zijn van het bedrijf. Gebruikers kunnen hun apparaten vervolgens registreren als een persoonlijk apparaat door de bedrijfsportal te installeren voor toegang tot bedrijfsresources, zoals e-mail, apps en gegevens.



<!--HONumber=Aug16_HO1-->

