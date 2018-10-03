---
title: Agregar funciones, la función CALC y la palabra clave NEW | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76fbb95117b1aae982242f24dc2cb1e815bc2356
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625933"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Las funciones de agregado, la función CALC y la palabra clave NEW
La forma de datos admite las funciones siguientes. El nombre asignado al capítulo que contiene la columna que se opera es la *alias de capítulo*.  
  
 Un alias de capítulo puede ser un nombre completo, que consta de cada nombre de columna de capítulo iniciales al capítulo que contiene el *nombre de columna,* todas separadas por puntos. Por ejemplo, si el capítulo principal, Cap1, contiene un capítulo secundario, Cap2, tiene una columna de cantidad, amt, entonces el nombre completo sería chap1.chap2.amt.  
  
|Funciones de agregado|Descripción|  
|-------------------------|-----------------|  
|SUM (*alias de capítulo*. *nombre de columna*)|Calcula la suma de todos los valores de la columna especificada.|  
|AVG (*alias de capítulo*. *nombre de columna*)|Calcula el promedio de todos los valores de la columna especificada.|  
|MAX (*alias de capítulo*. *nombre de columna*)|Calcula el valor máximo de la columna especificada.|  
|MIN (*alias de capítulo*. *nombre de columna*)|Calcula el valor mínimo de la columna especificada.|  
|RECUENTO (*alias de capítulo*[. *nombre de columna*])|Cuenta el número de filas en el alias especificado. Si se especifica una columna, solo las filas para los que esa columna es distinto de Null se incluyen en el recuento.|  
|STDEV (*alias de capítulo*. *nombre de columna*)|Calcula la desviación estándar de la columna especificada.|  
|CUALQUIER (*alias de capítulo*. *nombre de columna*)|Un valor de la columna especificada. ALGUNA tiene un valor de predicción solo cuando el valor de la columna es el mismo para todas las filas en el capítulo.<br /><br /> **Tenga en cuenta** si la columna no contiene el mismo valor para todas las filas en el capítulo, el comando SHAPE arbitrariamente devuelve uno de los valores que sea el valor de la función ANY.|  
  
|Expresión calculada|Descripción|  
|---------------------------|-----------------|  
|CALC (*expresión*)|Calcula una expresión arbitraria, pero solo en la fila de la **Recordset** que contiene la función CALC. Cualquier expresión mediante estos [Visual Basic para aplicaciones (VBA) funciones](../../../ado/guide/data/visual-basic-for-applications-functions.md) está permitido.|  
  
|NUEVA palabra clave|Descripción|  
|-----------------|-----------------|  
|NUEVO *tipo de campo* [(*ancho* &#124; *escala* &#124; *precisión* &#124; *error*[, *escala* &#124; *error*])]|Agrega una columna vacía del tipo especificado a la **Recordset**.|  
  
 El *tipo de campo* pasa con la palabra clave NEW puede ser cualquiera de los siguientes tipos de datos.  
  
|Tipos de datos OLE DB|Equivalentes del tipo de datos de ADO|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
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
