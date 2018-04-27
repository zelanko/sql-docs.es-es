---
title: Habilitar o deshabilitar la recopilación de datos de uso y bloqueará la creación de informes de operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Este artículo explica cómo controlar si los datos de informes de errores y uso se recopilan y se envían a Microsoft.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 035195a03dea60f097a9de88ceb869fe53398c35
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar o deshabilitar la recopilación de datos de uso para [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Cómo deshabilitar los informes de telemetría

[!INCLUDE[name-sos](../includes/name-sos-short.md)] recopila datos de uso y lo envía a Microsoft para ayudar a mejorar nuestros productos y servicios. Para obtener más información, lea la [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

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