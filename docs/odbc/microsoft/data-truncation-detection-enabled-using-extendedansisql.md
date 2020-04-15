---
title: Detección de truncamiento de datos habilitada mediante ExtendedAnsiSQL Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280706"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando la marca ExtendedAnsiSQL está activada y la aplicación está insertando datos en una columna char o binaria y los datos se truncan, se detectará el truncamiento. Cuando la marca ExtendedAnsiSQL está desactivada, los datos se truncan sin previo aviso, como en versiones anteriores de los controladores de base de datos de escritorio ODBC.
