---
title: Llamadas de procedimiento ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282235"
---
# <a name="procedure-calls"></a>Llamadas a procedimientos
Un *procedimiento* es un objeto ejecutable almacenado en el origen de datos. Normalmente, se trata de una o varias instrucciones SQL compiladas. La secuencia de escape para llamar a un procedimiento es  
  
 •**?=** *Nombre-procedimiento*de**llamada** [**[***[ parámetro*][ **{****,**[*parámetro*]]... **)**]**}**  
  
 donde *procedure-name* especifica el nombre de un procedimiento y *el parámetro* especifica un parámetro de procedimiento.  
  
 Para obtener más información acerca de la secuencia de escape de llamada de procedimiento, vea Secuencia de escape de [llamada](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) de procedimiento en apéndice C: gramática SQL.  
  
 Un procedimiento puede tener cero o más parámetros. También puede devolver un valor, como se indica en el marcador de parámetro opcional **?** al principio de la sintaxis. Si *parameter* es una entrada o un parámetro de entrada/salida, puede ser un literal o un marcador de parámetro. Sin embargo, las aplicaciones interoperables siempre deben usar marcadores de parámetros porque algunos orígenes de datos no aceptan valores de parámetroliterales. Si *parameter* es un parámetro de salida, debe ser un marcador de parámetro. Los marcadores de parámetro deben enlazarse con **SQLBindParameter** antes de que se ejecute la instrucción de llamada al procedimiento.  
  
 Los parámetros de entrada y de entrada/salida pueden omitirse de las llamadas a procedimiento. Si se llama a un procedimiento con paréntesis pero sin ningún parámetro, como por ejemplo, el *nombre-procedimiento*de llamada () , el controlador indica al origen de datos que utilice el valor predeterminado para el primer parámetro. Si el procedimiento no tiene ningún parámetro, esto podría hacer que el procedimiento falle. Si se llama a un procedimiento sin paréntesis, como por ejemplo, *"nombre-procedimiento de*llamada", el controlador no envía ningún valor de parámetro.  
  
 Pueden especificarse literales para los parámetros de entrada y de entrada/salida en llamadas a procedimiento. Por ejemplo, supongamos que el procedimiento **InsertOrder** tiene cinco parámetros de entrada. La siguiente llamada a **InsertOrder** omite el primer parámetro, proporciona un literal para el segundo parámetro y utiliza un marcador de parámetro para los parámetros tercero, cuarto y quinto:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Tenga en cuenta que si se omite un parámetro, la coma que lo delimita de otros parámetros debe seguir apareciendo. Si se omite un parámetro de entrada o de entrada/salida, el procedimiento usa el valor predeterminado del parámetro. Otra forma de especificar el valor predeterminado de un parámetro de entrada o entrada/salida es establecer el valor del búfer de longitud/indicador enlazado al parámetro en SQL_DEFAULT_PARAM.  
  
 Si se omite un parámetro de entrada/salida o si se proporciona un literal para el parámetro, el controlador descarta el valor de salida. Del mismo modo, si se omite el marcador de parámetro para el valor devuelto de un procedimiento, el controlador descarta dicho valor devuelto. Finalmente, si una aplicación especifica un parámetro de valor devuelto para un procedimiento que no devuelve ningún valor, el controlador establece el valor del búfer de longitud/indicador enlazado al parámetro en SQL_NULL_DATA.  
  
 Supongamos que el procedimiento PARTS_IN_ORDERS crea un conjunto de resultados que contiene una lista de pedidos que contienen un número de pieza determinado. El código siguiente llama a este procedimiento para el número de pieza 544:  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 Para determinar si un origen de datos admite procedimientos, una aplicación llama a **SQLGetInfo** con la opción SQL_PROCEDURES.  
  
 Para obtener más información acerca de los procedimientos, vea [Procedimientos](../../../odbc/reference/develop-app/procedures-odbc.md).
