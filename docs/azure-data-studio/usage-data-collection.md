---
title: Habilitar o deshabilitar la recopilación de datos de uso y bloqueo reporting de Azure Data Studio | Microsoft Docs
description: En este artículo se explica cómo controlar si el uso y bloqueo de datos de informes se recopilan y se envían a Microsoft.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b0a5adf802ab07e05f1041b1385044e2d580db32
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356486"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar o deshabilitar la recopilación de datos de uso para [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Cómo deshabilitar los informes de telemetría

[!INCLUDE[name-sos](../includes/name-sos-short.md)] recopila datos de uso y lo envía a Microsoft para ayudar a mejorar nuestros productos y servicios. Para obtener más información, lea el [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Si no desea enviar datos de uso a Microsoft, puede establecer el *telemetry.enableTelemetry* si se establece en *false*.

Para silenciar todos los eventos de telemetría de [!INCLUDE[name-sos](../includes/name-sos-short.md)], desde **archivo** > **preferencias** > **configuración**, agregue la siguiente opción:

```json
    "telemetry.enableTelemetry": false
```

**Aviso importante**: esta opción requiere un reinicio de [!INCLUDE[name-sos](../includes/name-sos-short.md)] surta efecto. 

## <a name="how-to-disable-crash-reporting"></a>Cómo deshabilitar los informes de bloqueo

Para deshabilitar los informes de bloqueo, de **archivo** > **preferencias** > **configuración**, agregue la siguiente opción:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso importante**: esta opción requiere un reinicio de [!INCLUDE[name-sos](../includes/name-sos-short.md)] surta efecto.

## <a name="additional-resources"></a>Recursos adicionales
- [Configuración de área de trabajo y usuario](settings.md)
