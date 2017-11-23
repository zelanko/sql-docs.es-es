---
title: SQLDescribeCol y SQLColAttribute | Documentos de Microsoft
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
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6044ca37e00d96c4a86fb5e9740ec6dfc824ca51
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol y SQLColAttribute
**SQLDescribeCol** y **SQLColAttribute** se usan para recuperar metadatos del conjunto de resultados. La diferencia entre estas dos funciones es que **SQLDescribeCol** siempre devuelve los mismos cinco fragmentos de información (una columna nombre, tipo de datos, precisión, escala y aceptación de valores NULL), mientras **SQLColAttribute** devuelve un único fragmento de información solicitada por la aplicación. Sin embargo, **SQLColAttribute** puede devolver una selección mucho más completa de metadatos, que incluye esta característica de una columna, Mostrar tamaño, actualización y funciones de búsqueda.  
  
 Muchas aplicaciones, especialmente aquellas que sólo muestre los datos, requieren que solo los metadatos devueltos por **SQLDescribeCol**. Para estas aplicaciones, es más rápido utilizar **SQLDescribeCol** de **SQLColAttribute** porque la información se devuelve en una sola llamada. Otras aplicaciones, especialmente los que actualizan los datos, necesitan los metadatos adicionales devueltos por **SQLColAttribute** y, por tanto, use las dos funciones. Además, **SQLColAttribute** admite metadatos específicos del controlador; para obtener más información, vea [tipos de datos específicos del controlador, Descriptor de tipos, información de tipos, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Una aplicación puede recuperar metadatos del conjunto de resultados en cualquier momento después de que se ha preparado o ejecuta una instrucción y antes del cursor sobre el resultado del conjunto se cierra. Muy pocas aplicaciones requieren metadatos del conjunto de resultados después de prepara la instrucción y antes de que se ejecute. Si es posible, las aplicaciones deben esperar a recuperar los metadatos hasta después de que se ejecuta la instrucción, porque algunos orígenes de datos no pueden devolver metadatos para instrucciones preparadas y emular esta capacidad en el controlador a menudo es un proceso lento. Por ejemplo, el controlador podría generar un conjunto mediante la sustitución de resultados de fila cero la **donde** cláusula de una **seleccione** instrucción con la cláusula **WHERE 1 = 2** y ejecutar el instrucción resultante.  
  
 Los metadatos a menudo son costosos de recuperar del origen de datos. Por este motivo, los controladores deben almacenar en caché los metadatos que recuperan del servidor y contener para siempre y cuando el cursor sobre el resultado del conjunto está abierto. Además, las aplicaciones deben solicitar solo los metadatos que sea absolutamente necesitan.
