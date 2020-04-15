---
title: ACTUALIZAR - Comando SQL ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307646"
---
# <a name="update---sql-command"></a>Comando de SQL de actualización
Actualiza los registros de una tabla con nuevos valores.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis de lenguaje nativo de Visual FoxPro para este comando. Para obtener información específica del controlador, consulte **Comentarios del controlador**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTUALIZAR [ *DatabaseName1!*] *NombreDeTabla1*  
 Especifica la tabla en la que los registros se actualizan con nuevos valores.  
  
 *DatabaseName1!* especifica el nombre de una base de datos distinta de la base de datos especificada con el origen de datos que contiene la tabla. Debe incluir el nombre de la base de datos que contiene la tabla si la base de datos no es la actual. Incluya el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de la tabla.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica las columnas que se actualizan y sus nuevos valores. Si omite la cláusula WHERE, cada fila de la columna se actualiza con el mismo valor.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 Especifica los registros que se actualizan con nuevos valores.  
  
 *FilterCondition* especifica los criterios que los registros deben cumplir para actualizarse con nuevos valores. Puede incluir tantas condiciones de filtro como desee, conectándolas con el operador AND u OR. También puede utilizar el operador NOT para invertir el valor de una expresión lógica, o puede utilizar **EMPTY**( ) para comprobar si hay un campo vacío.  
  
## <a name="remarks"></a>Observaciones  
 UPDATE: SQL solo puede actualizar registros en una sola tabla.  
  
 A diferencia de REPLACE, UPDATE - SQL utiliza el bloqueo de registros al actualizar varios registros en tablas abiertas para el acceso compartido. Esto reduce la contención de registros en situaciones multiusuario, pero puede reducir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para uso exclusivo o utilice **FLOCK**( ) para bloquear la tabla.  
  
## <a name="driver-remarks"></a>Observaciones del conductor  
 Cuando la aplicación envía la instrucción SQL ODBC UPDATE al origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando Visual FoxProUPDATE sin traducción.  
  
## <a name="see-also"></a>Consulte también  
 [DELETE - Comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
