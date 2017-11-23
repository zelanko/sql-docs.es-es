---
title: Las aplicaciones personalizadas | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe974d13b438cdb7fe010a35621665557cf2af8d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="custom-applications"></a>Aplicaciones personalizadas
Aplicaciones personalizadas suelen realizan una tarea específica para algunos de los DBMS. Por ejemplo, una aplicación puede recuperar datos de un DBMS único y generar un informe, o pueden transferir datos entre varios DBMS. Lo que estas aplicaciones tienen en común es que estos DBMS se conocen antes de escribir la aplicación y no suelen cambiar durante la vida útil de la aplicación.  
  
 Por lo tanto, la aplicación personalizada requiere interoperabilidad poca o ninguna. El desarrollador de aplicaciones puede elegir un controlador único para cada DBMS y el código directamente a los controladores. La aplicación sin ningún riesgo puede contener código específico del controlador para aprovechar las capacidades de los controladores e incluso puede realizar llamadas a la API de base de datos nativo para usar la funcionalidad no admitida por ODBC.  
  
 El problema de interoperabilidad principales de la mayoría de las aplicaciones personalizada es si el DBMS de destino cambia en el futuro. Si es así, se puede simplificar este proceso al escribir código más interoperable comenzar con. Sin embargo, estos cambios en DBMS es poco frecuente y normalmente conlleva una gran cantidad de trabajo. Por este motivo, los desarrolladores de aplicaciones personalizadas rara vez eligen aumentar la interoperabilidad a costa de funcionalidad; por lo general deciden codificar esa funcionalidad cuando cambian de DBMS.
