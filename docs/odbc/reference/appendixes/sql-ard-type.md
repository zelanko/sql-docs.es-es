---
title: SQL_ARD_TYPE | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e3d3ba38947babc5e7335fd38a63db18943b31f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
El identificador de tipo SQL_ARD_TYPE se usa para indicar que los datos en un búfer será del tipo especificado en el campo SQL_DESC_CONCISE_TYPE de la descartar. SQL_ARD_TYPE se escribe en el *TargetType* argumento de una llamada a **SQLGetData** en lugar de un tipo de datos específico y permite escribir una aplicación para cambiar los datos del búfer cambiando el descriptor campo. Este valor asocia el tipo de datos de la  *\*TargetValuePtr* búfer para el campo descriptor. (SQL_ARD_TYPE no se especifica en una llamada a **SQLBindCol** o **SQLBindParameter** porque ya está asociado a los campos SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE y se puede cambiar el tipo de búfer enlazado en cualquier momento cambiando cualquiera de esos campos.)  
  
 El identificador de tipo SQL_ARD_TYPE puede utilizarse para especificar valores no predeterminados para la precisión de segundos de tipos de datos interval e iniciales y escriba los valores de escala y precisión de los datos SQL_C_NUMERIC. Para obtener más información, consulte [reemplazar predeterminado a la izquierda y la precisión de segundos para tipos de datos Interval](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) y [reemplazar predeterminado precisión y escala para los tipos de datos numéricos](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), más adelante en este apéndice.
