---
title: SQLDescribeCol y SQLColAttribute ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299765"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol y SQLColAttribute
**SQLDescribeCol** y **SQLColAttribute** se utilizan para recuperar metadatos del conjunto de resultados. La diferencia entre estas dos funciones es que **SQLDescribeCol** siempre devuelve los mismos cinco elementos de información (nombre de una columna, tipo de datos, precisión, escala y nulabilidad), mientras que **SQLColAttribute** devuelve una sola pieza de información solicitada por la aplicación. Sin embargo, **SQLColAttribute** puede devolver una selección mucho más completa de metadatos, incluida la sensibilidad a mayúsculas y minúsculas de una columna, el tamaño de visualización, la capacidad de actualización y la capacidad de búsqueda.  
  
 Muchas aplicaciones, especialmente las que solo muestran datos, solo requieren los metadatos devueltos por **SQLDescribeCol**. Para estas aplicaciones, es más rápido usar **SQLDescribeCol** que **SQLColAttribute** porque la información se devuelve en una sola llamada. Otras aplicaciones, especialmente las que actualizan los datos, requieren los metadatos adicionales devueltos por **SQLColAttribute** y, por lo tanto, usan ambas funciones. Además, **SQLColAttribute** admite metadatos específicos del controlador; Para obtener más información, vea [Tipos de datos específicos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)del controlador, Tipos de descriptor, Tipos de información, Tipos de diagnóstico y atributos .  
  
 Una aplicación puede recuperar metadatos del conjunto de resultados en cualquier momento después de que se haya preparado o ejecutado una instrucción y antes de que se cierre el cursor sobre el conjunto de resultados. Muy pocas aplicaciones requieren metadatos de conjunto de resultados después de preparar la instrucción y antes de que se ejecute. Si es posible, las aplicaciones deben esperar para recuperar metadatos hasta después de ejecutar la instrucción, porque algunos orígenes de datos no pueden devolver metadatos para instrucciones preparadas y emular esta capacidad en el controlador suele ser un proceso lento. Por ejemplo, el controlador podría generar un conjunto de resultados de fila cero reemplazando la cláusula **WHERE** de una instrucción **SELECT** por la cláusula WHERE 1 **a 2** y ejecutando la instrucción resultante.  
  
 Los metadatos suelen ser costosos de recuperar del origen de datos. Por este motivo, los controladores deben almacenar en caché los metadatos que recuperan del servidor y mantenerlos mientras el cursor sobre el conjunto de resultados esté abierto. Además, las aplicaciones deben solicitar solo los metadatos que necesitan absolutamente.
