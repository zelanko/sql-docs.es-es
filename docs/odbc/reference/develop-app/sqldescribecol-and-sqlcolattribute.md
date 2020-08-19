---
description: SQLDescribeCol y SQLColAttribute
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de375ea207e8e393fa36c9795ebf0e3ca5f428b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424507"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol y SQLColAttribute
**SQLDescribeCol** y **SQLColAttribute** se usan para recuperar los metadatos del conjunto de resultados. La diferencia entre estas dos funciones es que **SQLDescribeCol** siempre devuelve los mismos cinco fragmentos de información (el nombre de una columna, el tipo de datos, la precisión, la escala y la nulabilidad), mientras que **SQLColAttribute** devuelve una única parte de la información solicitada por la aplicación. Sin embargo, **SQLColAttribute** puede devolver una selección mucho más rica de metadatos, como la distinción de mayúsculas y minúsculas de una columna, el tamaño de la pantalla, la actualización y la capacidad de búsqueda.  
  
 Muchas aplicaciones, especialmente aquellas que solo muestran datos, requieren solo los metadatos devueltos por **SQLDescribeCol**. Para estas aplicaciones, es más rápido usar **SQLDescribeCol** que **SQLColAttribute** , ya que la información se devuelve en una sola llamada. Otras aplicaciones, especialmente las que actualizan datos, requieren los metadatos adicionales devueltos por **SQLColAttribute** y, por tanto, usan ambas funciones. Además, **SQLColAttribute** admite metadatos específicos del controlador; para obtener más información, vea [tipos de datos específicos del controlador, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Una aplicación puede recuperar los metadatos del conjunto de resultados en cualquier momento después de preparar o ejecutar una instrucción y antes de que se cierre el cursor sobre el conjunto de resultados. Muy pocas aplicaciones requieren metadatos del conjunto de resultados una vez preparada la instrucción y antes de que se ejecute. Si es posible, las aplicaciones deben esperar para recuperar los metadatos hasta que se ejecute la instrucción, porque algunos orígenes de datos no pueden devolver metadatos para las instrucciones preparadas y la emulación de esta funcionalidad en el controlador suele ser un proceso lento. Por ejemplo, el controlador puede generar un conjunto de resultados de cero filas reemplazando la cláusula **Where** de una instrucción **Select** por la cláusula **donde 1 = 2** y ejecutando la instrucción resultante.  
  
 Los metadatos suelen ser caros de recuperar del origen de datos. Por este motivo, los controladores deben almacenar en caché los metadatos que recuperen del servidor y mantenerlos mientras esté abierto el cursor sobre el conjunto de resultados. Además, las aplicaciones deben solicitar solo los metadatos que realmente necesitan.
