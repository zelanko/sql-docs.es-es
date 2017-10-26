---
title: Habilitar nuevos tipos de datos estableciendo ExtendedAnsiSQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5161224a5d4fe3f0bf2af200a5cff3e1ea4e1008
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar a nuevos tipos de datos estableciendo ExtendedAnsiSQL
Dos nuevos tipos de datos están disponibles en las bases de datos de Jet 4.0 cuando está activado el indicador de ExtendedAnsiSQL: SQL_DECIMAL de ODBC y SQL_NUMERIC. La precisión y escala predeterminadas son 18 y 0, respectivamente. Datos que se tiene acceso a través de ODBC que se escribe como SQL_DECIMAL de ODBC o SQL_NUMERIC se asignarán a Microsoft Jet Decimal en lugar de moneda.  
  
 Cuando la marca ExtendedAnsiSQL está desactivada, no se puede crear tablas con tipos decimales o numeric y estos tipos no aparecerán en SQLGetTypeInfo(). Sin embargo, si la tabla contiene los nuevos tipos de datos, puede utilizar con los tipos de datos correcto.

