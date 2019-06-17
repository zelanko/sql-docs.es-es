---
title: SQLDescribeCol y SQLColAttribute | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149027"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol y SQLColAttribute
**SQLDescribeCol** y **SQLColAttribute** se usan para recuperar metadatos del conjunto de resultados. Es la diferencia entre estas dos funciones que **SQLDescribeCol** siempre devuelve el mismas cinco piezas de información (una columna nombre, tipo de datos, precisión, escala y la nulabilidad), mientras **SQLColAttribute** devuelve un solo dato solicitado por la aplicación. Sin embargo, **SQLColAttribute** puede devolver una selección mucho más completa de metadatos, incluidos la diferenciación de una columna, mostrar el tamaño, la posibilidad de actualización y funciones de búsqueda.  
  
 Muchas aplicaciones, especialmente aquellas que solo muestran datos, requieren solo los metadatos devueltos por **SQLDescribeCol**. Para estas aplicaciones, es más rápido utilizar **SQLDescribeCol** que **SQLColAttribute** porque la información se devuelve en una sola llamada. Otras aplicaciones, especialmente aquellas que actualizan datos, requieren los metadatos adicionales devueltos por **SQLColAttribute** y, por tanto, usar ambas funciones. Además, **SQLColAttribute** es compatible con los metadatos específicos del controlador; para obtener más información, consulte [los tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Una aplicación puede recuperar metadatos del conjunto de resultados en cualquier momento después de preparación o ejecución de una instrucción y antes del cursor sobre el resultado del conjunto se cierra. Muy pocas aplicaciones exigen que los metadatos del conjunto de resultados después de prepara la instrucción y antes de ejecutarlo. Si es posible, las aplicaciones deben esperar para recuperar metadatos hasta después de ejecutar la instrucción, ya que algunos orígenes de datos no pueden devolver metadatos para instrucciones preparadas y emular esta capacidad en el controlador a menudo es un proceso lento. Por ejemplo, el controlador podría generar un conjunto mediante la sustitución de resultados de fila cero la **donde** cláusula de una **seleccione** instrucción con la cláusula **WHERE 1 = 2** y ejecutar el instrucción resultante.  
  
 A menudo son costoso recuperar del origen de datos de metadatos. Por este motivo, los controladores deben almacenar en caché los metadatos que recuperar del servidor y contener para siempre y cuando el cursor sobre el resultado establecido es abierto. Además, las aplicaciones deben solicitar solo los metadatos que necesitan realmente.
