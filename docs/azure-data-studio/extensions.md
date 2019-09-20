---
title: Incorporación de extensiones
titleSuffix: Azure Data Studio
description: Agregue extensiones de Extensions Marketplace a Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: e114c4991d5f3df10537e459263b49152c466f99
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70274824"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>Ampliación de la funcionalidad de [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Las extensiones de [!INCLUDE[name-sos](../includes/name-sos-short.md)] proporcionan una manera sencilla de agregar más funcionalidad a la instalación base de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. 

Las extensiones las proporciona el equipo de Azure Data Studio (Microsoft), así como la comunidad de terceros (los usuarios). Para más información sobre la creación de extensiones, vea [Creación de extensiones](extension-authoring.md).


## <a name="add-azure-data-studio-extensions"></a>Incorporación de extensiones de Azure Data Studio

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.\
    También puede acceder rápidamente al administrador de extensiones si presiona `Ctrl+Shift+X` (Windows/Linux) o `Command+Shift+X` (Mac).\
    ![Icono del Administrador de extensiones](media/extensions/extension-manager-icon.png)

2. Seleccione una extensión disponible para ver sus detalles.
    ![Detalles de la extensión](media/extensions/extension-details.png)

3. Seleccione la extensión que quiera e **instálela**.

4. Una vez instalada, seleccione **Recargar** para habilitar la extensión en Azure Data Studio (solo es necesario cuando se instala una extensión por primera vez).


## <a name="access-installed-azure-data-studio-extensions"></a>Acceso a las extensiones instaladas de Azure Data Studio

Cada extensión mejora la experiencia en Azure Data Studio de manera diferente. Como resultado, el punto de entrada de las extensiones puede variar. Consulte la documentación individual de la extensión instalada para obtener información sobre cómo se puede acceder a sus características una vez instalada.
