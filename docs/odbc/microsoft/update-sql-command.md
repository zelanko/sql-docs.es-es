---
title: "Comando de SQL de actualización - | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fb2e4d3e3010eaba53b36de383c3365d82db289
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="update---sql-command"></a>Comando de SQL de actualización:
Actualiza los registros en una tabla con nuevos valores.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo para este comando. Para obtener información específica del controlador, consulte **controlador comentarios**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTUALIZACIÓN [ *DatabaseName1!*] *TableName1*  
 Especifica la tabla en la que se actualizan los registros con los nuevos valores.  
  
 *¡DatabaseName1!* Especifica el nombre de una base de datos que no sea la base de datos especificada con el origen de datos que contiene la tabla. Debe incluir el nombre de la base de datos que contiene la tabla si la base de datos no es actual. Incluir el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de tabla.  
  
 ESTABLECER *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica las columnas que se actualizan y sus nuevos valores. Si se omite la cláusula WHERE, se actualiza cada fila de la columna con el mismo valor.  
  
 DONDE *FilterCondition1*[AND &#124; O *FilterCondition2*...]  
 Especifica los registros que se actualizan con nuevos valores.  
  
 *FilterCondition* especifica los criterios que deben cumplir los registros para actualizarse con los nuevos valores. Se pueden incluir muchas condiciones de filtro como desee, conectan con la operación AND o OR (operador). También puede usar el operador NOT para invertir el valor de una expresión lógica, o puede usar **vacía**() para comprobar si un campo vacío.  
  
## <a name="remarks"></a>Comentarios  
 UPDATE - SQL puede actualizar solo los registros en una sola tabla.  
  
 A diferencia de reemplazo, UPDATE - SQL utiliza el bloqueo de registros al actualizar varios registros en tablas abierto para el acceso compartido. Esto reduce la contención del registro en situaciones multiusuario, pero puede reducir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para exclusivo use o **genealógico**() para bloquear la tabla.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción UPDATE de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando FoxProUPDATE Visual sin traducción.  
  
## <a name="see-also"></a>Vea también  
 [ELIMINAR, comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
