---
title: ELIMINAR, comando SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea0b09d77b6d2df8ddd525df17526573b6a1e1be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="delete---sql-command"></a>ELIMINAR, comando SQL
Marca registros para su eliminación.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo para este comando. Para obtener información específica del controlador, vea la sección Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DESDE [ *DatabaseName!*] *TableName*  
 Especifica la tabla en la que los registros se marcan para su eliminación.  
  
 *¡DatabaseName!* Especifica el nombre de una base de datos que contiene la tabla si la base de datos que lo contiene no es la base de datos especificada con el origen de datos. Debe incluir el nombre de una base de datos que contiene la tabla si la base de datos no es la base de datos especificada con el origen de datos. Incluir el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de tabla.  
  
 DONDE *FilterCondition1*[AND &#124; o *FilterCondition2*...]  
 Especifica que Visual FoxPro marcar sólo algunos registros para su eliminación.  
  
 *FilterCondition* especifica los criterios que deben cumplir los registros para estar marcado para su eliminación. Se pueden incluir muchas condiciones de filtro como desee, conectan con la operación AND o OR (operador). También puede usar el operador NOT para invertir el valor de una expresión lógica, o puede usar **vacía**() para comprobar si un campo vacío.  
  
## <a name="remarks"></a>Comentarios  
 Si SET DELETED se establece en ON, todos los comandos que incluyen un ámbito omite registros marcados para su eliminación.  
  
 ELIMINAR - utiliza SQL bloqueo de registros al marcar varios registros para su eliminación en tablas abierto para el acceso compartido. Esto reduce la contención del registro en situaciones multiusuario, pero puede reducir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para su uso exclusivo.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción DELETE de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando Eliminar de Visual FoxPro sin traducción.  
  
## <a name="see-also"></a>Vea también  
 [Comando de eliminaciones de Set](../../odbc/microsoft/set-deleted-command.md)
