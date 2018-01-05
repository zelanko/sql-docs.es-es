---
title: "Habilitar o deshabilitar la recopilación de datos de uso y bloqueará la creación de informes de operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Este artículo explica cómo controlar si los datos de informes de errores y uso se recopilan y se envían a Microsoft."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae620951028ba8e0e82f89c4251238c92bc614ca
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar o deshabilitar la recopilación de datos de uso para[!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Cómo deshabilitar los informes de telemetría

[!INCLUDE[name-sos](../includes/name-sos-short.md)]recopila datos de uso y lo envía a Microsoft para ayudar a mejorar nuestros productos y servicios. Para obtener más información, lea la [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Si no desea enviar datos de uso a Microsoft, puede establecer la *telemetry.enableTelemetry* si se establece en *false*.

Para silenciar todos los eventos de telemetría de [!INCLUDE[name-sos](../includes/name-sos-short.md)], de **archivo** > **preferencias** > **configuración**, agregue la opción siguiente:

```json
    "telemetry.enableTelemetry": false
```

**Aviso importante**: esta opción requiere un reinicio de [!INCLUDE[name-sos](../includes/name-sos-short.md)] surta efecto. 

## <a name="how-to-disable-crash-reporting"></a>Cómo deshabilitar los informes de bloqueo

Para deshabilitar informe de bloqueo de **archivo** > **preferencias** > **configuración**, agregue la opción siguiente:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso importante**: esta opción requiere un reinicio de [!INCLUDE[name-sos](../includes/name-sos-short.md)] surta efecto.

## <a name="additional-resources"></a>Recursos adicionales
- [Configuración de área de trabajo y usuario](settings.md)