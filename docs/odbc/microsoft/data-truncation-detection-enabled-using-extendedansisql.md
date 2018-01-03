---
title: "Detección de truncamiento de datos habilitada con ExtendedAnsiSQL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f36a9de5b1ce9ca269511bb0a2a641d201ed37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando se activa la marca de ExtendedAnsiSQL y la aplicación consiste en Insertar datos en un carácter o una columna binaria y los datos se truncan, se detectará el truncamiento. Cuando la marca ExtendedAnsiSQL está desactivada, los datos se truncan sin previo aviso, tal como estaba en versiones anteriores de los controladores de base de datos de escritorio de ODBC.
