---
title: SQLColAttributes (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f4fae186ea7880325f6e3a96aae29f1edef07e1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel de núcleo  
  
 Devuelve información del descriptor para una columna de un conjunto de resultados. Información del descriptor se devuelve como una cadena de caracteres, un valor de dependiente de descriptor de 32 bits o un valor entero.  
  
> [!NOTE]  
>  **SQLColAttributes** no se puede usar para devolver información acerca de la columna de marcador (columna 0).  
  
 El controlador ODBC de Visual FoxPro admite todos los *fDescType* valores. En la tabla siguiente incluye comentarios en la implementación del controlador de valores seleccionados.  
  
|*fDescType*|Comentario|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Devuelve FALSE: Visual FoxPro no tiene ningún campo de contador.|  
|SQL_COLUMN_CASE_SENSITIVE|Siempre devuelve TRUE si el tipo de columna es de carácter.|  
|SQL_COLUMN_LABEL|Devuelve el nombre de columna, que también se devuelve por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Devuelve TRUE si el tipo de columna es moneda (representado por una "Y" en el lenguaje de Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_QUALIFIER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_SEARCHABLE|Devuelve SQL_UNSEARCHABLE para las columnas de tipo General; Estas columnas no se puede usar en una cláusula WHERE.<br /><br /> No establezca devuelve SQL_SEARCHABLE para las columnas de tipo carácter o Memo con NOCPTRANS; Estas columnas se pueden utilizar en una cláusula WHERE con cualquier operador de comparación.<br /><br /> Devuelve SQL_ALL_EXCEPT_LIKE para todos los demás tipos de columna; Estas columnas se pueden utilizar en una cláusula WHERE con todos los operadores de comparación excepto similar.|  
|SQL_COLUMN_TABLE_NAME|Siempre devuelve una cadena vacía.|  
  
 Para obtener más información, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) en el *referencia del programador de ODBC*.

