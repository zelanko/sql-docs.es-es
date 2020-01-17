---
title: Habilitación o deshabilitación de la recopilación de datos de uso y los informes de bloqueo
titleSuffix: Azure Data Studio
description: En este artículo se explica cómo controlar si se recopilan datos de informes de uso y de bloqueo y se envían a Microsoft.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 416c22aa04e289e7959e41924344666e4329ecf1
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957009"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitación o deshabilitación de la recopilación de datos de uso de [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Cómo deshabilitar los informes de telemetría

[!INCLUDE[name-sos](../includes/name-sos-short.md)] recopila datos de uso y los envía a Microsoft para ayudar a mejorar los productos y servicios. Para obtener más información, vea la [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Si no quiere enviar datos de uso a Microsoft, puede establecer el valor *telemetry.enableTelemetry* en *false*.

Para silenciar todos los eventos de telemetría de [!INCLUDE[name-sos](../includes/name-sos-short.md)], en **Archivo** > **Preferencias** > **Configuración**, agregue la siguiente opción:

```json
    "telemetry.enableTelemetry": false
```

**Aviso importante**: Esta opción requiere que [!INCLUDE[name-sos](../includes/name-sos-short.md)] se reinicie para surtir efecto. 

## <a name="how-to-disable-crash-reporting"></a>Cómo deshabilitar los informes de bloqueo

Para deshabilitar los informes de bloqueo, en **Archivo** > **Preferencias** > **Configuración**, agregue la siguiente opción:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso importante**: Esta opción requiere que [!INCLUDE[name-sos](../includes/name-sos-short.md)] se reinicie para surtir efecto.

## <a name="additional-resources"></a>Recursos adicionales
- [Configuración de área de trabajo y usuario](settings.md)
