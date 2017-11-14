---
title: "Agregar funciones, la función CALC y la palabra clave NEW | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f24280f155fd5ec6bd86b8486b0f8f77338d8eb6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Las funciones de agregado, la función CALC y la palabra clave NEW
La forma de datos admite las funciones siguientes: Es el nombre asignado al capítulo que contiene la columna que se trabajará en el *alias de capítulo*.  
  
 Un alias de capítulo puede ser completo, que consta de cada nombre de la columna de capítulo a la izquierda en el capítulo que contiene el *nombre de columna,* todas separadas por puntos. Por ejemplo, si el capítulo principal, Cap1, contiene un capítulo secundario, Cap2, tiene una columna de cantidad, amt, entonces el nombre completo sería chap1.chap2.amt.  
  
|Funciones de agregado|Description|  
|-------------------------|-----------------|  
|SUM (*alias de capítulo*. *nombre de la columna*)|Calcula la suma de todos los valores de la columna especificada.|  
|AVG (*alias de capítulo*. *nombre de la columna*)|Calcula el promedio de todos los valores de la columna especificada.|  
|MAX (*alias de capítulo*. *nombre de la columna*)|Calcula el valor máximo de la columna especificada.|  
|MIN (*alias de capítulo*. *nombre de la columna*)|Calcula el valor mínimo de la columna especificada.|  
|RECUENTO (*alias de capítulo*[. *nombre de la columna*])|Cuenta el número de filas en el alias especificado. Si se especifica una columna, solo las filas para los que esa columna es distinto de Null se incluyen en el recuento.|  
|STDEV (*alias de capítulo*. *nombre de la columna*)|Calcula la desviación estándar de la columna especificada.|  
|CUALQUIER (*alias de capítulo*. *nombre de la columna*)|Un valor de la columna especificada. ALGUNA tiene un valor de predicción sólo cuando el valor de la columna es el mismo para todas las filas del capítulo.<br /><br /> **Tenga en cuenta** si la columna no contiene el mismo valor para todas las filas en el capítulo, el comando SHAPE devuelve arbitrariamente uno de los valores con el valor de la función ANY.|  
  
|expresión calculada|Description|  
|---------------------------|-----------------|  
|CALC (*expresión*)|Calcula una expresión arbitraria, pero sólo en la fila de la **Recordset** que contiene la función CALC. Cualquier expresión mediante estos [de Visual Basic para aplicaciones (VBA) funciones](../../../ado/guide/data/visual-basic-for-applications-functions.md) está permitido.|  
  
|NUEVA palabra clave|Description|  
|-----------------|-----------------|  
|NUEVA *tipo de campo* [(*ancho* &#124; *escala* &#124; *precisión* &#124; *error* [, *escala* &#124; *error*])]|Agrega una columna vacía del tipo especificado a la **conjunto de registros**.|  
  
 El *tipo de campo* pasa con la palabra clave NEW puede ser cualquiera de los siguientes tipos de datos.  
  
|Tipos de datos OLE DB|Tipo de datos de ADO equivalentes|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|AdBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|excepto adVarNumeric|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adLongVarBinary adBinary, AdVarBinary,|  
|DBTYPE_STR|Cada, parámetros, adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBData|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 Cuando el nuevo campo es de tipo decimal (en OLE DB, DBTYPE_DECIMAL, o en ADO, adDecimal), debe especificar los valores de precisión y escala.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)

