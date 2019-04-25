---
title: Comando de actualización - SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbd5ec98791d782fe7ad1fdb1e1884b646dcf9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632562"
---
# <a name="update---sql-command"></a>Comando de SQL de actualización
Actualiza los registros en una tabla con nuevos valores.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativa para este comando. Para obtener información específica del controlador, vea **controlador comentarios**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 UPDATE [ *DatabaseName1!*] *TableName1*  
 Especifica la tabla en la que se actualizan los registros con los nuevos valores.  
  
 *DatabaseName1!* Especifica el nombre de una base de datos distinta de la base de datos especificado con el origen de datos que contiene la tabla. Debe incluir el nombre de la base de datos que contiene la tabla si la base de datos no es actual. Incluir el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de tabla.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica las columnas que se actualizan y sus valores nuevos. Si se omite la cláusula WHERE, se actualiza cada fila de la columna con el mismo valor.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 Especifica los registros que se actualizan con nuevos valores.  
  
 *FilterCondition* especifica los criterios que los registros deben cumplir para que se actualice con nuevos valores. Puede incluir como muchas condiciones de filtro como desee, conectan con AND u operador OR. También puede usar el operador NOT para anular el valor de una expresión lógica, o puede usar **vacía**() para comprobar si un campo vacío.  
  
## <a name="remarks"></a>Comentarios  
 UPDATE - SQL puede actualizar solo los registros en una sola tabla.  
  
 A diferencia de reemplazo, actualización - SQL utiliza el bloqueo de registros al actualizar varios registros en tablas abiertos para el acceso compartido. Esto reduce la contención de registros en situaciones multiusuario, pero puede reducir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para exclusivo utilice o **MANADA**() para bloquear la tabla.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción UPDATE de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando FoxProUPDATE Visual sin traducción.  
  
## <a name="see-also"></a>Vea también  
 [ELIMINAR, comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
