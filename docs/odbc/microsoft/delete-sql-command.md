---
title: DELETE - Comando SQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303556"
---
# <a name="delete---sql-command"></a>ELIMINAR, comando SQL
Marca los registros para su eliminación.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis de lenguaje nativo de Visual FoxPro para este comando. Para obtener información específica del controlador, consulte Comentarios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DESDE [ *DatabaseName!*] *TableName*  
 Especifica la tabla en la que se marcan los registros para su eliminación.  
  
 *¡Databasename!* especifica el nombre de una base de datos que contiene la tabla si la base de datos contenedora no es la base de datos especificada con el origen de datos. Debe incluir el nombre de una base de datos que contenga la tabla si la base de datos no es la base de datos especificada con el origen de datos. Incluya el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de la tabla.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 Especifica que Visual FoxPro marque solo determinados registros para su eliminación.  
  
 *FilterCondition* especifica los criterios que deben cumplir los registros para que se marquen para su eliminación. Puede incluir tantas condiciones de filtro como desee, conectándolas con el operador AND u OR. También puede utilizar el operador NOT para invertir el valor de una expresión lógica, o puede utilizar **EMPTY**( ) para comprobar si hay un campo vacío.  
  
## <a name="remarks"></a>Observaciones  
 Si SET DELETED se establece en ON, todos los comandos que incluyen un ámbito omiten los registros marcados para su eliminación.  
  
 DELETE: SQL utiliza el bloqueo de registros al marcar varios registros para su eliminación en tablas abiertas para el acceso compartido. Esto reduce la contención de registros en situaciones multiusuario, pero puede disminuir el rendimiento. Para obtener el máximo rendimiento, abra la tabla para uso exclusivo.  
  
## <a name="driver-remarks"></a>Observaciones del conductor  
 Cuando la aplicación envía la instrucción ODBC SQL DELETE al origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando DELETE de Visual FoxPro sin traducción.  
  
## <a name="see-also"></a>Consulte también  
 [Comando de eliminaciones de Set](../../odbc/microsoft/set-deleted-command.md)
