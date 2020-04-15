---
title: Tipos de datos de Paradox ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290935"
---
# <a name="paradox-data-types"></a>Tipos de datos de Paradox
El controlador ODBC Paradox asigna tipos de datos Paradox a tipos de datos SQL ODBC. En la tabla siguiente se enumeran todos los tipos de datos de Paradox y se muestran los tipos de datos SQL ODBC a los que están asignados.  
  
|Tipo de datos Paradox|Tipo de datos de ODBC|  
|-----------------------|--------------------|  
|Alfanuméricos|SQL_VARCHAR|  
|AUTOINCREMENTO[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEN[2]|SQL_LONGVARBINARY|  
|LOGICAL[1]|SQL_BIT|  
|LARGO[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|DINERO[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|TIEMPO[1]|SQL_TIMESTAMP|  
|TIMESTAMP[1]|SQL_TIMESTAMP|  
  
 [1] Válido sólo para las versiones 5 de Paradox. *x*.  
  
 [2] Válido sólo para las versiones 4 de Paradox. *x* y 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos SQL ODBC. Todas las conversiones en el Apéndice D de la *referencia del programador ODBC* se admiten para los tipos de datos SQL ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente se muestran las limitaciones en los tipos de datos de Paradox.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Alfanuméricos|La creación de una columna ALPHANUMERIC de longitud cero o no especificada devuelve realmente una columna de 255 bytes.|  
|BYTES|Si inserta NULL en una columna binaria con el controlador Paradox5, se cambia a 0.|  
|LONG|El valor negativo máximo admitido por el controlador Paradox para el tipo de datos Long en Paradox 5. *x* no es -2-31 (-2147483648), como debería ser ya que Long se asigna al tipo de datos ODBC SQL_INTEGER. El valor negativo máximo admitido para Long es en realidad -2-31 + 1 (-2147483647).|  
|timestamp|Cuando el controlador Paradox inserta un valor en una columna TIMESTAMP y, a continuación, se recupera de la columna, el valor recuperado puede diferir del valor insertado hasta 1 segundo debido al redondeo.|  
  
 Puede encontrar más limitaciones en los tipos de datos en [Limitaciones](../../odbc/microsoft/data-type-limitations.md)de tipos de datos .
