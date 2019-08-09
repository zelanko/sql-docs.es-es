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
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 71ed86e9ad076a41099eaf4e56fe67a25b5f2c21
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958946"
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
