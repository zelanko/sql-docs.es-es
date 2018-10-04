---
title: ELIMINAR, comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 674c2d9d259d09456bc97edc4a6b9e842f9a4519
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676203"
---
# <a name="delete---sql-command"></a>ELIMINAR, comando SQL
Marca los registros para su eliminación.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativa para este comando. Para obtener información específica del controlador, vea la sección Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DESDE [ *DatabaseName!*] *TableName*  
 Especifica la tabla en la que los registros se marcan para su eliminación.  
  
 *¡DatabaseName!* Especifica el nombre de una base de datos que contiene la tabla si la base de datos que lo contiene no es la base de datos especificado con el origen de datos. Debe incluir el nombre de una base de datos que contiene la tabla si la base de datos no es la base de datos especificado con el origen de datos. Incluir el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de tabla.  
  
 DONDE *FilterCondition1*[AND &#124; o *FilterCondition2*...]  
 Especifica que Visual FoxPro marcar determinados registros para su eliminación.  
  
 *FilterCondition* especifica los criterios que los registros deben cumplir para que se ha marcado para su eliminación. Puede incluir como muchas condiciones de filtro como desee, conectan con AND u operador OR. También puede usar el operador NOT para anular el valor de una expresión lógica, o puede usar **vacía**() para comprobar si un campo vacío.  
  
## <a name="remarks"></a>Comentarios  
 Si SET DELETED está establecida en ON, los registros marcados para su eliminación se omiten todos los comandos que incluyen un ámbito.  
  
 ELIMINAR: usa SQL bloqueo de registros al marcar varios registros para su eliminación en tablas abierto para el acceso compartido. Esto reduce la contención de registros en situaciones multiusuario, pero puede reducir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para su uso exclusivo.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción DELETE de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando de Visual FoxPro eliminar sin traducción.  
  
## <a name="see-also"></a>Vea también  
 [Comando de eliminaciones de Set](../../odbc/microsoft/set-deleted-command.md)
